---
type: reference
project: FSBO-Hub
last-verified: 2026-06-21
---

# Netlify Credits — Step-by-Step Conservation Guide
*Last updated: 2026-06-21*

---

## Step 1 — Audit: which sites need Netlify vs Cloudflare Pages

Before touching anything, categorize your sites. Open a spreadsheet (or the network spreadsheet) and tag each hub with one of:

**Keep on Netlify** — site uses any of:
- Server-side rendering (SSR) via `@netlify/plugin-nextjs`
- Netlify Functions or API routes that run server-side
- Netlify Forms, Identity, or Edge Functions
- ISR (incremental static regeneration) with revalidation

**Move to Cloudflare Pages** — site is:
- Pure SSG (no runtime server needed)
- Content/informational only (no lead forms, no API routes)
- Could work as a fully static export

**Disconnect from Netlify entirely** — site is:
- Not live yet
- Not scheduled for work in the next 90 days
- Just a repo — no Netlify site needed right now

For your network, rough split:
- Most lateral hubs (content-only: probate-hub, estate-hub, divorce-hub, funeral-hub, etc.) → Cloudflare Pages candidates
- Active tool hubs (fsbo-hub, closing-hub, investor-hub, etc.) → stay on Netlify
- Unbuilt shells → disconnect from Netlify entirely

---

## Step 2 — Disable auto-deploys on inactive Netlify sites (do this first, takes 5 min)

This stops build minutes from burning on repos you're not actively working on.

1. Go to [app.netlify.com](https://app.netlify.com)
2. Click a site you want to pause
3. Go to **Site configuration → Build & deploy → Continuous deployment**
4. Under "Branches and deploy contexts", click **Edit settings**
5. Set "Production branch" auto-publishing to **off** — or click **Stop auto publishing** if that option is shown
6. Repeat for every inactive site

Alternatively, to fully freeze a site: **Site configuration → Build & deploy → Continuous deployment → Disconnect** — this unlinks the GitHub repo. The site stays live at its last deploy but no future pushes trigger builds.

---

## Step 3 — Restrict builds to main branch only (add to each active netlify.toml)

Open each active hub's `netlify.toml` and add/update this:

```toml
[build]
  publish = ".next"
  command = "npm run build"

# Only build production deploys on main — ignore all other branches
[context.production]
  publish = ".next"

[context.deploy-preview]
  ignore = "exit 0"   # never build deploy previews

[context.branch-deploy]
  ignore = "exit 0"   # never build branch deploys

[[plugins]]
  package = "@netlify/plugin-nextjs"
```

The two `ignore = "exit 0"` lines tell Netlify to skip the build entirely for PRs and non-main branches. This alone can cut build usage significantly on repos where you push feature branches.

---

## Step 4 — Add the file-change ignore rule to active sites

This skips the build when no relevant files changed (e.g., when you push a README update or a script file).

Add to `netlify.toml`:

```toml
[build]
  ignore = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- src/ app/ components/ public/ package.json next.config.mjs"
```

Adjust the path list to match what actually matters for that site. If none of those paths changed in a push, Netlify skips the build entirely.

---

## Step 5 — Use `[skip netlify]` in commit messages

When you push something that shouldn't trigger a build (config changes, documentation, script files), add this to the commit message:

```
git commit -m "Update build script [skip netlify]"
```

Netlify checks commit messages and skips the build if it sees `[skip netlify]` or `[netlify skip]`.

---

## Step 6 — Add build caching to active sites

Next.js build cache lives in `.next/cache`. Without caching, every build recompiles everything from scratch. Add this to `netlify.toml`:

```toml
[build]
  publish = ".next"
  command = "npm run build"

[build.environment]
  NEXT_TELEMETRY_DISABLED = "1"
  NODE_VERSION = "20"

# Cache node_modules and Next.js build cache between deploys
[[plugins]]
  package = "@netlify/plugin-nextjs"

[build.processing]
  skip_processing = false
```

Then create a `netlify-plugin-cache.toml` or use the built-in cache — Netlify automatically caches `.next/cache` when using `@netlify/plugin-nextjs` v5+. Confirm your plugin is up to date:

```bash
npm install @netlify/plugin-nextjs@latest
```

---

## Step 7 — Move static/content hubs to Cloudflare Pages

Do this for hubs that are pure content (no server-side needs).

### 7a. Convert the site to static export

In `next.config.mjs`, add:

```js
const nextConfig = {
  output: 'export',   // produces /out directory of static files
  trailingSlash: true,
  images: {
    unoptimized: true,  // required for static export (no image optimization server)
  },
}

export default nextConfig
```

**Note:** `output: 'export'` disables ISR, API routes, and middleware. Only use this for truly static content hubs with no server needs.

### 7b. Disconnect from Netlify

1. Netlify dashboard → site → **Site configuration → Build & deploy → Continuous deployment**
2. Click **Disconnect** (site stays live at last deploy — you can delete the Netlify site after Cloudflare is confirmed working)

### 7c. Set up on Cloudflare Pages

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages → Create application → Pages**
2. Click **Connect to Git**
3. Select the GitHub repo from `kevc55-code`
4. Build settings:
   - **Framework preset:** Next.js (Static HTML Export)
   - **Build command:** `npm run build`
   - **Build output directory:** `out`
5. Add environment variables if needed (from your Netlify env vars)
6. Click **Save and Deploy**

### 7d. Update DNS

If the site is on a custom domain:
1. In Cloudflare dashboard → Pages site → **Custom domains → Add a custom domain**
2. Enter the domain (e.g., `probate.byownerhub.com`)
3. Cloudflare will auto-create the DNS record since your DNS is already on Cloudflare
4. Remove the old Netlify DNS entry for that subdomain

---

## Step 8 — For Next.js sites with ISR on Cloudflare (optional, advanced)

If a site uses ISR but you still want it on Cloudflare to save Netlify credits, use the `@cloudflare/next-on-pages` adapter instead of `output: 'export'`.

```bash
npm install @cloudflare/next-on-pages
```

Build command in Cloudflare Pages: `npx @cloudflare/next-on-pages`
Output directory: `.vercel/output/static`

**Caveats:** not all Next.js features work on Cloudflare Workers runtime. Test thoroughly before switching a live site. Route handlers (API routes) work, but some Node.js APIs don't. Check the [compatibility list](https://opennext.js.org/cloudflare) before committing.

For most of your hubs this won't be needed — pure SSG is simpler and works fine.

---

## Priority order to do this week

1. **Today (15 min):** Go through Netlify dashboard and pause/disconnect all sites that aren't live or actively in development. Probably 20+ of your 41 repos.

2. **This week:** Add the `[context.deploy-preview] ignore = "exit 0"` and `[context.branch-deploy] ignore = "exit 0"` blocks to every active site's `netlify.toml`. Push to each repo.

3. **When you have 30 min:** Pick 3–5 content-only hubs (good candidates: probate-hub, estate-hub, funeral-hub, divorce-hub, 55plus-hub). Convert to `output: 'export'`, set up on Cloudflare Pages, test, then disconnect from Netlify.

4. **Ongoing:** Use `[skip netlify]` in commit messages during development runs where you're pushing frequently.

---

## Quick reference — which setting does what

| Setting | Where | Saves |
|---------|-------|-------|
| Stop auto publishing | Netlify dashboard | All build minutes for that site |
| `ignore = "exit 0"` on previews/branches | netlify.toml | Build minutes from branch/PR pushes |
| File-change ignore rule | netlify.toml | Build minutes when non-code files change |
| `[skip netlify]` in commit | Commit message | That specific build |
| Move to Cloudflare Pages | Cloudflare dashboard | 100% of Netlify build minutes for that site |
| Build caching (plugin-nextjs v5) | npm + netlify.toml | Build time (fewer minutes per build) |
