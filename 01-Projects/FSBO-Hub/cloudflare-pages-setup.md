# Cloudflare Pages — Full Setup Guide
*For the ByOwnerHub network — Next.js 14 App Router sites*
*Last updated: 2026-06-21*

---

## Two paths — pick the right one per site

### Path A: Static Export (`output: 'export'`)
- Simplest. Cloudflare serves flat HTML/CSS/JS files. Zero runtime.
- Works for: pure content hubs, no API routes, no ISR, no server components that fetch at runtime
- Does NOT work for: API routes, server actions, middleware, ISR revalidation, dynamic routes that aren't pre-generated
- Build output: `/out` directory

### Path B: `@cloudflare/next-on-pages` (Workers runtime)
- More capable. Runs Next.js server logic on Cloudflare Workers (not Node.js).
- Works for: API routes, server components, dynamic routes, middleware
- Does NOT work for: some Node.js APIs, `fs` module, native Node bindings, `next/image` optimization without a loader
- Build output: `.vercel/output/static`
- Requires: `nodejs_compat` compatibility flag in Cloudflare

**For your hubs:** most content hubs → Path A. Hubs with lead forms / API routes → Path B or stay on Netlify.

---

## Prerequisites

- Cloudflare account (you already have one)
- DNS already on Cloudflare (you already have this)
- GitHub org `kevc55-code` connected to Cloudflare (do this once — see Step 1)

---

## Step 1 — Connect GitHub to Cloudflare (one-time)

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Select your account
3. Left sidebar → **Workers & Pages**
4. Click **Create application** → **Pages** → **Connect to Git**
5. Click **Connect GitHub**
6. GitHub OAuth prompt → authorize Cloudflare
7. Select **kevc55-code** organization
8. Choose **All repositories** or select specific ones — recommend "All" so you don't have to redo this for each hub

You only do this once. After that, every new Pages project just picks from the already-connected org.

---

## Path A — Static Export Setup (pure content hubs)

### A1. Code change: add `output: 'export'` to next.config.mjs

```js
// next.config.mjs
const nextConfig = {
  output: 'export',
  trailingSlash: true,       // Cloudflare Pages serves index.html in folders
  images: {
    unoptimized: true,       // no image optimization server with static export
  },
}

export default nextConfig
```

**Remove** `@netlify/plugin-nextjs` from your `netlify.toml` for this site — it's no longer needed (and will error on a static export build).

Also remove or update `netlify.toml`:
```toml
# netlify.toml — only needed if site still has a Netlify connection
# If fully migrated to Cloudflare, delete this file or leave it empty
```

### A2. Test the static build locally

```bash
cd your-hub
npm run build
# Should produce an /out directory, not a /.next directory
ls out/
# Should see index.html and static asset folders
```

If the build fails here, you have a server-side dependency that needs to be resolved before moving to static export. Common culprits:
- `generateStaticParams` missing on a dynamic route (required for static export)
- Server Actions in a form (not supported in static export)
- API route handlers (not supported in static export)

If any of these exist, the site belongs on Path B or stays on Netlify.

### A3. Create the Cloudflare Pages project

1. Cloudflare dashboard → **Workers & Pages → Create application → Pages**
2. **Connect to Git** → select the hub repo from `kevc55-code`
3. Build settings:
   - **Project name:** match the hub name (e.g., `probate-hub`)
   - **Production branch:** `main`
   - **Framework preset:** Next.js (Static HTML Export) — if this doesn't appear, select "None" and fill in manually
   - **Build command:** `npm run build`
   - **Build output directory:** `out`
4. **Environment variables** (if any) — add them here. Do NOT add Netlify-specific vars like `NETLIFY_*`
5. Click **Save and Deploy**

First deploy takes ~2–3 minutes. Cloudflare assigns a `*.pages.dev` preview URL.

### A4. Verify the deploy

- Open the `*.pages.dev` URL
- Check all pages render
- Check that internal links work (if trailingSlash is on, links should end with `/`)
- Check that images load

---

## Path B — `@cloudflare/next-on-pages` Setup (hubs with server logic)

### B1. Install the adapter

```bash
cd your-hub
npm install @cloudflare/next-on-pages
npm install --save-dev wrangler
```

### B2. Add `wrangler.toml` to the repo root

```toml
name = "your-hub-name"
compatibility_date = "2024-09-23"
compatibility_flags = ["nodejs_compat"]
pages_build_output_dir = ".vercel/output/static"
```

### B3. Update next.config.mjs

```js
// next.config.mjs
import { setupDevPlatform } from '@cloudflare/next-on-pages/next-dev'

// Only call setupDevPlatform in development
if (process.env.NODE_ENV === 'development') {
  await setupDevPlatform()
}

const nextConfig = {
  // Do NOT add output: 'export' here — next-on-pages handles this differently
}

export default nextConfig
```

### B4. Mark server components/routes with the edge runtime

Any server component or API route that runs server-side needs to explicitly declare the edge runtime:

```ts
// app/api/leads/route.ts
export const runtime = 'edge'

// app/some-page/page.tsx — if it uses server-side data fetching
export const runtime = 'edge'
```

Pages without this declaration will default to Node.js runtime, which is not available on Cloudflare Workers. The build will fail or the page will 500.

**What works on edge runtime:**
- `fetch()` ✅
- `Response`, `Request`, `Headers` ✅
- Supabase JS client (uses fetch under the hood) ✅
- Environment variables via `process.env` ✅

**What does NOT work:**
- `fs`, `path`, `os` — Node.js built-ins ❌
- `child_process` ❌
- Most native npm packages that use Node internals ❌

### B5. Test locally with Wrangler

```bash
# Build for Cloudflare
npx @cloudflare/next-on-pages

# Preview locally on Workers runtime (not Node.js)
npx wrangler pages dev .vercel/output/static
```

This simulates exactly what Cloudflare will run. Test all routes before deploying.

### B6. Create the Cloudflare Pages project

1. Cloudflare dashboard → **Workers & Pages → Create application → Pages → Connect to Git**
2. Select the repo
3. Build settings:
   - **Build command:** `npx @cloudflare/next-on-pages`
   - **Build output directory:** `.vercel/output/static`
   - **Framework preset:** None (don't use the Next.js preset here — it uses the wrong build command)
4. **Settings → Functions → Compatibility flags:**
   - Add `nodejs_compat` to both Production and Preview
   - Set **Compatibility date** to `2024-09-23` or later
5. Add environment variables
6. Deploy

---

## Custom domains (works for both paths)

Since your DNS is already on Cloudflare, this is frictionless — no CNAME propagation wait.

### Adding a subdomain

1. Cloudflare Pages dashboard → your project → **Custom domains**
2. Click **Set up a custom domain**
3. Enter the subdomain: e.g., `probate.byownerhub.com`
4. Cloudflare detects the domain is already in your account and auto-creates the DNS record
5. Click **Activate domain** — live immediately, no wait

### Adding an apex domain (e.g., `ProbateHub.com`)

1. Same flow — **Custom domains → Set up a custom domain**
2. Enter the apex: `probatehub.com`
3. Cloudflare will ask you to set a CNAME or ALIAS record — if the domain is in Cloudflare DNS already it auto-wires; if not, add the CNAME manually pointing to your `*.pages.dev` URL
4. SSL provisioned automatically

### Removing the old Netlify domain

Once Cloudflare is confirmed live on the custom domain:
1. Netlify dashboard → site → **Domain management**
2. Remove the custom domain from the Netlify site
3. If Netlify had a CNAME record in your DNS — delete it from Cloudflare DNS panel (it's replaced by the Pages CNAME now)

---

## Environment variables

Each Cloudflare Pages project has its own env vars. Migrate from Netlify:

1. Netlify site → **Site configuration → Environment variables** — screenshot or copy all vars
2. Cloudflare Pages project → **Settings → Environment variables**
3. Add each var. Set scope:
   - **Production** — only on main branch deploys
   - **Preview** — on all branch deploys
   - **All environments** — both

For secrets (API keys, Supabase service role key): add as "Secret" type — encrypted, not visible after save.

**Important for Path B sites with Supabase:**
- `SUPABASE_URL` — add to Cloudflare env vars
- `SUPABASE_SERVICE_ROLE_KEY` — add as Secret, never expose client-side
- In your code, access via `process.env.SUPABASE_SERVICE_ROLE_KEY` in server/edge routes only

---

## `next/image` on Cloudflare Pages

The built-in Next.js image optimizer doesn't work on Cloudflare (it needs a Node.js server). Options:

**Option 1 — Unoptimized (fine for most hubs):**
```js
// next.config.mjs
images: {
  unoptimized: true,
}
```

**Option 2 — Cloudflare Images loader (if you want optimization):**
```js
images: {
  loader: 'custom',
  loaderFile: './lib/cloudflare-image-loader.js',
}
```
```js
// lib/cloudflare-image-loader.js
export default function cloudflareLoader({ src, width, quality }) {
  return `https://your-zone.com/cdn-cgi/image/width=${width},quality=${quality || 75}/${src}`
}
```
Requires Cloudflare Images to be enabled on your account (paid feature, $5/mo for 100k images).

For content hubs, `unoptimized: true` is fine. For hubs with lots of property images or photos, consider Cloudflare Images.

---

## Build caching on Cloudflare Pages

Cloudflare Pages automatically caches `node_modules` between builds (unlike some CI systems). You don't need to configure this manually. Build times are typically 30–90 seconds for a Next.js site after the first cold build.

---

## Which hubs to migrate first (recommended order)

**Easiest wins — pure content, no server needs:**
1. `probate-hub` — content only
2. `estate-hub` — content only
3. `funeral-hub` — content only
4. `divorce-hub` — content only
5. `55plus-hub` — content only (just pushed a fix — good time to migrate)

**Path B candidates (have or will have API routes):**
- `closing-hub` — has/will have lead capture
- `investor-hub` — cash-offer flow (Module D)
- `contractor-hub` — lead form (Module A)

**Stay on Netlify for now:**
- `fsbo-hub` — complex, lots of tools
- Any hub with existing Netlify Functions

---

## Gotchas specific to your stack

**`netlify.toml` confusion:** When a repo is connected to Cloudflare Pages, Cloudflare ignores `netlify.toml` entirely. You don't need to delete it (it won't cause errors) but it also won't do anything. Your Cloudflare build settings are in the dashboard and `wrangler.toml` (for Path B only).

**`@netlify/plugin-nextjs` in package.json:** Fine to leave in `package.json` — Cloudflare won't call it. But clean it up eventually so `npm install` doesn't pull an unused dep.

**Dynamic routes require `generateStaticParams` for Path A:**
```ts
// app/[state]/[metro]/page.tsx — required for static export
export async function generateStaticParams() {
  const pages = await getGeoPages() // your Supabase fetch
  return pages.map(p => ({ state: p.state, metro: p.metro }))
}
```
Without this, the build will fail with "Page is missing `generateStaticParams`".

**Branch previews:** Cloudflare Pages auto-builds every branch push by default, just like Netlify. To restrict to main only:
Cloudflare Pages project → **Settings → Builds & deployments → Branch control** → set Preview branches to "None".

---

## Verifying a successful migration checklist

- [ ] `*.pages.dev` URL renders correctly
- [ ] Custom domain resolves and shows green SSL
- [ ] All internal links work (check with site crawler or manually)
- [ ] No console errors in browser
- [ ] Old Netlify site still live as fallback (don't delete until Cloudflare confirmed)
- [ ] DNS removed from Netlify after Cloudflare domain confirmed
- [ ] Netlify site disconnected from GitHub repo (or deleted)
- [ ] Build minutes no longer being consumed on Netlify for that repo
