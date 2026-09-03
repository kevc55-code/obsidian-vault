---
type: status
project: FSBO-Hub
last-verified: 2026-09-03
---

# ByOwnerHub Network — Build Status

*Last updated: 2026-09-03 — see [[SESSION-2026-09-02]] for the full log. Hosting/deploy topology unchanged since 07-12 (still CF Pages network-wide except fsbo/car/landlord on Netlify, solar undeployed). A **"positioning + commission" copy/data sprint** landed 2026-09-02 on all three fsbo repos: production (`fsbo-freemium-sandbox`) got 6 pushed commits (homepage free/paid split + positioning module, commission figures derived from one shared `commission.ts`, a Stripe checkout error-logging fix), `fsbo-staging` independently re-built the same set and committed its previously-pending crawler-policy edit, and **fsbo-hub `main`'s `Hero.tsx` edit — uncommitted since 08-21 — finally got committed and pushed (`e659fd1`)**, clearing that item. car-by-owner shipped a page-level FTC-disclosure commit. Weekly link audit (09-01) and affiliate digest (09-02) already logged in [[open-items]]. Still open: `freemium-wip` 11 unpushed (4 weeks), the unrotated PAT (~41 days), mirror-branch drift ~21 repos. See [[unpushed-changes]], [[open-items]].*

---

## 🟢 Current State of Union (2026-09-02)

- **"Positioning + commission" sprint, 2026-09-02, all three fsbo repos.** Production (`fsbo-freemium-sandbox`) `master` `f955716` → `c2bb429`, 6 commits, all pushed: a homepage **positioning module** + a hero line **stating the free/paid split** outright; commission figures now **derived from median price in one place** (`src/lib/commission.ts`) and the metro page **shows both figures instead of one ambiguous number** (routes suburb page / `opengraph-image` / `SavingsCalculator` / `SchemaMarkup` through it, retires a drifted `types` field); and `fix(stripe)`: the checkout `catch` now **logs and surfaces the Stripe failure class** — the direct follow-up to the 2026-08-26 key-ID incident where a generic catch string hid a live-mode 401 for three weeks.
- **fsbo-staging independently re-built the same sprint** — `master` → `f3ce1c8`, 7 commits, all pushed / in sync. Includes committing `1bf2a10` (the AI-crawler / SearchAction edit that was sitting **uncommitted** as of 08-25) and `e84abb2` (its own preview-config name so it stops colliding with production in the tooling). Different hashes, same messages — the intended dev-first flow. Staging is now essentially level with production, lacking only the prod-specific Stripe error-logging commit.
- **fsbo-hub `main` — the Hero.tsx edit finally landed.** `e659fd1` "drop the metro hero CTAs and tighten the spacing" (2026-09-02) is the working-tree edit carried since **2026-08-21** across five vault checks — now committed **and pushed**, working tree clean, `main` in sync with `origin/main`. Item closed.
- **car-by-owner `main`** — `ba17a8d` (2026-09-02): page-level FTC affiliate disclosure above CTAs + a tidied Carfax note. Pushed, in sync.
- **Unchanged:** `fsbo-hub freemium-wip` still 11 commits unpushed (now 4 weeks / seven vault checks, deploy-readiness unverified since 07-12, likely superseded); `fsbo-freemium-sandbox`'s two untracked deploy scripts with the still-unrotated plaintext PAT (~41 days); buyer-hub's `tools/network-audit/{report.md,results.json}` holding the 09-01 audit run uncommitted; mirror-branch drift ~21 repos (persisted two weekly runs — batch sync overdue). No other repo moved.

---

## 🟢 Previous State of Union (2026-08-25)

- **Network-wide OG-image fix, 5 repos, all pushed** — 55plus-hub, boat-hub, closing-hub, condo-hub, investor-hub were all shipping `opengraph-image.tsx` routes that 404'd under static export (Search Console flagged it; any social share showed a broken preview). Root cause took two passes: removing `runtime = "edge"` (08-21) wasn't enough, because static export can't generate `ImageResponse` images at all regardless of runtime — the routes were deleted outright (08-23), falling back to the `og-default.png` already in `public/`. Swept the rest of the network for the same pattern: only one other hit, a dead `.bak` file in flatfee-hub. Rollout complete.
- **fsbo-freemium-sandbox (production) — 3 more commits, all pushed.** An AI-crawler robots.txt fix (this Netlify-hosted site was the only one in the network not blocking training crawlers — the other ~39 get it free from Cloudflare's managed robots.txt) plus removal of a broken homepage `SearchAction` pointing at a route that never existed. A state-blog 404 fix (22 state buckets redirect to their state guide instead of 404ing) plus a Boston FAQ split for cleaner schema. And, today (08-25), a build-pipeline fix to the manual-redeploy skip guard — **the commit message says this was silently blocking the switch to live Stripe keys**, since Netlify only applies new env vars on a fresh build and the old guard skipped manual redeploys with no code change. Worth checking with Kevin whether live Stripe keys are now actually live.
- **fsbo-staging caught up** — no longer "3 commits behind production": it now has the refund-revocation/resume and refund-guarantee-fix commits it was missing as of 08-21. It's 2 commits behind now (state-blog fix, build-skip fix), and has a **new uncommitted edit** independently re-implementing production's AI-crawler/SearchAction fix — same dev-first pattern as before.
- **Everything else unchanged since 08-21**: fsbo-hub `main`'s uncommitted `Hero.tsx` edit (now 4 days), `freemium-wip`'s 11 unpushed commits (now 3 weeks stale), the unrotated PAT in fsbo-freemium-sandbox's untracked deploy script (33 days), buyer-hub's uncommitted network-audit output. No other repo moved.

---

## 🟢 Previous State of Union (2026-08-21)

- **fsbo-freemium-sandbox (production) — feature sprint, 2026-08-19/20, all pushed.** Metro and suburb pages redesigned from a long article dump into a 4-step revealed tool (price it / list it / show & disclose / close), driven by shared state across the stepper, checklist tabs, and affiliate ServicesGrid (now keyed per-step instead of pooled). Along the way: a mobile-overflow bug fixed on every metro/suburb page (comps-estimator grid forced 587px inside a 375px viewport), a suburb-page bug fixed where state-specific checklist items were silently dropped (matched on the suburb's own slug instead of its parent metro), and a same-day production incident (fail-closed robots guard had shipped `Disallow: /` to fsbo.byownerhub.com) caught and fixed. Two new entitlement features also shipped: **refund revocation** (Stripe webhook now handles `charge.refunded`, flips purchase status, gates the download) and **passwordless cross-device resume** (email-a-link workspace restore, explicitly not a login — paid access still keys off the verified Stripe session). A same-day follow-up closed a loophole the refund feature exposed: the 30-day guarantee previously let anyone buy→download→refund→keep, now refundable only until first download. A Netlify build fix stopped every deploy from cold-building (build command was deleting the just-restored cache). Full detail: [[SESSION-2026-08-21]].
- **fsbo-staging now 3 commits behind production** — it independently built and verified the same metro/suburb redesign first (different commit hashes, same messages — that's the intended dev→prod flow) but doesn't yet have production's 3 newest commits (refund revocation/resume, refund-guarantee fix, Netlify build fix). Not urgent, staging never serves a live domain.
- **fsbo-hub `main` moved 2 commits on 08-19** that the same-day vault check didn't catch: a seller-progress workspace feature and a metro-page redesign mirroring production's. Plus a **new uncommitted edit** to `Hero.tsx` (removes hero CTA buttons, tightens padding) — looks like mid-port of the same redesign, not yet committed.
- **str-hub `master`'s 9-commit, 15-day-stale backlog is resolved** — no new commits, but it's now pushed and in sync with `origin/master`. Closes an item that had been carried across four vault-sync sessions.
- **Full-network branch sweep confirms nothing else is unpushed** — checked every local branch against its upstream (not just main/master) network-wide; only `fsbo-hub freemium-wip` (11, unchanged) and one pre-existing stale `claude/*` worktree branch remain ahead of origin anywhere. The two old 1-ahead items (`timeshare-hub`, `trademark-hub`, flagged 07-23) no longer show up — resolved at some point, dropped from open items.
- **PAT in `fsbo-freemium-sandbox/deploy_freemium_branch.ps1` still unrotated** — file mtime unchanged since 07-23, now 29 days.
- car-by-owner reconfirmed in sync with origin; buyer-hub's `tools/network-audit/{report.md,results.json}` still sitting as the same 2026-08-18 uncommitted run, no new audit since.
- **Still open, unchanged:** landlord-hub DNS still pointing at the dead Netlify site (no dashboard access from here to verify or fix — see item below), production-branch re-pointing decision (kept), solar hosting never stood up, GSC "Validate Fix" click for fsbo's duplicate-canonical set, `RESEND_API_KEY` needed on production for the new resume-link email to actually send, lead-sale-disclosure rollout scope still unclear.

---

## 🟢 Previous State of Union (2026-08-19)

- **Quiet period, mostly cleanup.** Since the 08-05 SEO-remediation wrap-up, only scattered link-fix commits landed: boat-hub (`f4fbdb5`, 16 dead/broken state agency links), landlord-hub (`ecb8876`, all 50 state lease-form links fixed after ezlandlordforms restructured its URLs), str-hub (`23ce82d`, fixed a CF Pages build that had been failing for a month by pinning `--legacy-peer-deps` for next-on-pages), car-by-owner (`8385113` WY DMV 403 fix, `ab3696c` MS/MT DMV wrong-agency fix). All pushed.
- **car-by-owner `main` now fully in sync with origin** — the 1 commit flagged unpushed 08-05 plus the 2 new fixes above are all pushed. car-by-owner had the most recent network activity as of this check.
- **fsbo-freemium-sandbox WIP resolved**: the large staged-but-uncommitted PDF-toolkit feature flagged 08-05 got committed and pushed as two commits (`5888d28` generate per-metro downloadable PDF toolkit gated behind purchase, `294ed74` give buyers more time to notice the toolkit download), both 2026-08-05. Working tree is clean now except the two untracked deploy scripts — **the plaintext GitHub PAT in `deploy_freemium_branch.ps1` is still there, unrotated, file mtime unchanged since 07-23 (27 days now).**
- **str-hub `master` and fsbo-hub `freemium-wip` unchanged** — still 9 and 11 commits unpushed respectively, same commit counts as 08-05. Neither has moved in two weeks.
- **Weekly network audit ran 2026-08-18** (`buyer-hub/tools/network-audit`, sitting modified-but-uncommitted in the repo's working tree as of this vault update — worth asking Kevin whether these should be committed each run or left as scratch going forward). Headline: **mirror-branch drift dropped from 23 repos (08-05/06) to zero** — no stale-deploy pairs detected this run. 4 new external-link failures: the already-tracked `nrec.nebraska.gov/SPCD.pdf` fsbo stale-deploy 404 is confirmed still live; a new `stlouiscountymo.gov` assessor 404 on fsbo's `/st-louis/` page; and `dph.illinois.gov`/`idoi.illinois.gov` Illinois state-agency 404s recurring on funeral-hub and insurance-hub (both were dismissed as crawler false positives in the 07-27 and 08-05/06 runs — now recurring twice, may be genuinely broken rather than flaky). str-hub's homepage still links a dead `solar.byownerhub.com` card (code 0 — expected, solar hosting still not stood up).
- **Still open** (unchanged from 08-05): production-branch re-pointing decision (kept, see [[open-items]] item 1), solar hosting never stood up, GSC "Validate Fix" click for fsbo's duplicate-canonical set, freemium launch gated on Stripe account + re-verified build, lead-sale-disclosure rollout scope still unclear.

---

## 🟢 Previous State of Union (2026-08-05)

- **Network-wide SEO remediation project (2026-07-27 → 08-04), driven by `buyer-hub/tools/seo-audit`** (a new custom auditor + baseline/ledger system, built because prior ad-hoc SEO passes shipped blind). Phases executed across ~39 repos: P1 locale-number-format (234→0), P2 title-duplicate criticals cleared, P3/P3a/P3b brand-title-template removal + per-page differentiated titles (~1,380 title defects cleared), P5 Organization+WebSite JSON-LD on all homepages, P7 meta-description SERP-width fixes (712→0 over five waves), P8 thin state-page content expansion (554→28 thin pages, 95% reduction), plus HowTo/CollectionPage/FAQPage/BlogPosting+BreadcrumbList/ItemList JSON-LD added where missing, and a homepage title/desc overflow fix across 21 repos. fsbo-hub blog posts got Article-family schema (previously had none). Full narrative: [[SESSION-2026-08-05]].
- **Parallel #bugs-channel fixes landed alongside**: firsttimebuyer-hub card-overflow fix, probate-hub Mississippi/Missouri court-finder link fixes, trademark-hub LegalZoom XML-response fix, moto-hub/probate-hub/trademark-hub 2026-07-30 batch, frbo-hub favicon-404 fix (dynamic icon route incompatible with static export), eviction-hub dead SC self-help link fixed.
- **Legal**: a "lead sale/sharing" privacy-policy disclosure clause was added to biz-hub, estate-hub, eviction-hub, fsbo-hub, moto-hub, str-hub — landed unevenly (only sites with active lead-gen forms, as best as can be told from commit history; not confirmed as an intentional full-network rule).
- **fsbo-hub `main` is back in sync with origin** (the 07-23 unpushed `ef035bb` welcome-email fix is now pushed). Branch `freemium-wip` grew from 9 to 11 commits ahead of origin (added a legal-disclosure commit and a welcome-email debug commit) — still unpushed, still not deploy-verified since the 07-23 merge.
- **str-hub has 9 unpushed commits on `master`** (P3b/P7/P8 SEO work + a same-day STR-permit-link fix batch, most recent 2026-08-04) — needs a push.
- **car-by-owner has 1 unpushed commit on `main`** (`b7b4286`, DMV/form link fixes for GA/MA/OK/WI/WY + TX form 130-U) — most recent activity in the whole network, 2026-08-05.
- **fsbo-freemium-sandbox**: still has the plaintext GitHub PAT in the untracked `deploy_freemium_branch.ps1`, unrotated 13 days after being flagged. Also now has a substantial *staged-but-uncommitted* feature in progress — "durable purchase records, server-verified paywall, state-scoped unlock" touches the Stripe checkout route, paywall gate, checklist components, and adds a new PDF-toolkit generator script.
- **Still open** (unchanged from 07-12/07-27): production-branch re-pointing decision (kept, see [[open-items]] item 1), solar hosting never stood up, GSC "Validate Fix" click for fsbo's duplicate-canonical set, freemium launch gated on Stripe account + re-verified build.

---

## 🟢 Previous State of Union (2026-07-12)

- **Legal entity: Byownerhub.com LLC** (New Mexico; 1209 Mountain Road Pl NE, Ste N, Albuquerque, NM 87110). Every site footer network-wide now shows `© Byownerhub.com LLC` + a link to byownerhub.com (sweep 2026-07-12, ~40 repos / 101 files).
- **Accessibility: network axe-clean.** ~1,300 WCAG 2.1 AA violations fixed; 36/36 CF sites + fsbo verified clean on live pages.
- **Email compliance done** (fsbo is the only PII collector): tokenized unsubscribe + RFC 8058 one-click live-verified; 5 sibling façade forms POST into fsbo's list with source tags; privacy pages everywhere relevant; deletion runbook in `buyer-hub/PRIVACY-REQUEST-RUNBOOK.md`.
- **Netlify (fsbo/rent/car) re-upped and current.** Census zip lookup fixed (`Netlify-Vary: query=zip` + ACS sentinel clamp). Env vars set except `RESEND_API_KEY`.
- **Alias 301s live** via Pages Function middleware: flatfee→flatfeemls, newbuild→new-build, frbo→rent.
- **new-build**: 50 real state guides live and indexed (were noindexed placeholders).
- **Freemium $99 toolkit**: branch `freemium-wip` deploy-ready (verified 2026-07-12), NOT deployed. Launch = merge→main + `STRIPE_SECRET_KEY`.
- **Still open**: production-branch re-pointing (mirror branches remain load-bearing), solar hosting, GSC sitemap submission — see [[open-items]].

---

## 🟢 Previous State of Union (2026-07-04)

Full-network link audit run 2026-07-03: crawled all 41 domains (~2,150 pages), status-checked every internal, cross-site, and external link (810 unique external). Full report: `buyer-hub/byownerhub-link-audit-2026-07-03.md` in the repo. Ground-truth summary:

**Hosting reality (corrects earlier notes):**
- **CF Pages:** apex + 36 subdomains. **Netlify:** `fsbo`, `car-by-owner`, `landlord` only (DNS: fsbo→fsbo-hub.netlify.app, landlord→byownerlandlordhub.netlify.app). Earlier note listing landlord/car as "CF Live" was wrong.
- **`relocation.byownerhub.com` — NOW LIVE** (2026-07-04) on CF Pages project `relocation-hub-344`. Was orphaned/undeployed before. Built as static export (`output: 'export'` → `out/`). NOTE: an earlier duplicate **Worker** named `relocation-hub` also exists from a failed attempt — delete it (superseded by the Pages project).
- **`solar.byownerhub.com` — NOT DEPLOYED anywhere.** No CF Pages project, no findable Netlify site. Earlier note claiming "stays on Netlify" was wrong. str-hub links a "Solar Hub" card at this dead domain. Needs hosting stood up.
- **new-build vs newbuild:** canonical flipped to **`new-build.byownerhub.com`** (dash) by commit `a158e85` on 2026-07-02, matching repo `new-build-hub` / project. Live 200. Old `newbuild.byownerhub.com` CNAME still serves the same project (duplicate — consider a 301).

**🔴 ROOT CAUSE of the recurring "stale deploy" problem (found this session):** every CF Pages project's **production branch is pinned to the OPPOSITE branch name** from what the repo pushes (`master`↔`main`). So normal pushes only ever built *previews* — production kept serving months-old builds. Worked around by mirror-pushing each repo's HEAD to both branch names (mirror branches on GitHub are now load-bearing — **do not delete**). Permanent fix = re-point production branch in each project's dashboard settings, then delete mirror branches.

**Fixes shipped + verified live this session:**
- apex: newbuild links corrected, Solar marked coming-soon, Relocation card added + set live
- `investor`: fix-and-flip 50-state grid retargeted `/fix-and-flip/<state>` → `/states/<state>` (were all 404); added missing `/privacy`, `/terms`, `/disclaimer`
- `commercial`: state-page "Qualified Intermediary" CTA → 1031exchangecorp.com (was dead `byownerhub.com/1031-exchange`)
- `foreclosure`: nav "How to Buy"/"Financing" → `/#how-to-buy`, `/#search` anchors (were 404 pages)
- `buyer`: homepage links canonical `flatfeemls.byownerhub.com` (was non-canonical `flatfee.`)
- `55plus`, `condo`: legal pages + states index restored (were 404 despite existing in code — stale-deploy symptom)
- `relocation`: built + deployed from scratch (Next 14.2.5→14.2.35, static export)

**⏳ Remaining open (all need Cloudflare dashboard — my API token is DNS-only):**
1. Re-point production branch on 6 projects: `55plus-hub`/`condo-hub`/`buyer-hub`/`foreclosure-hub` → `master`; `commercial-hub-523`/`investor-hub` → `main`. Then delete mirror branches.
2. Stand up hosting for **solar** (nothing exists).
3. Delete the leftover **relocation-hub Worker** (Pages project replaces it).
4. Add `flatfee → flatfeemls` 301 (Redirect Rule); optionally `newbuild → new-build` 301.
5. **GSC:** fsbo has 33 "Duplicate without user-selected canonical" — already fixed in code (canonical tags verified present on live pages, last-crawled 15–17 Jun predates the fix). Click **Validate Fix** in Search Console; no code change needed.

**External link rot:** 183 genuine 404s across the network (biggest: HUD reorg killed ~20 state homeownership links on `firsttimebuyer`; state DMV/boating/court/vital-records links on `boat`/`car`/`probate`/`funeral`/`land`). 235 "403" links are just bot-blocking (auction.com, HomeAdvisor, LegalZoom) — fine for real users. Full list in the audit report.

**Verified good:** `mailto:` is `byownerhubadmin@gmail.com` everywhere (zero rogue addresses); no site links any parked lookalike domain; canonical subdomain convention holds except the two fixes above.

---

## Status Key

| Symbol | Meaning |
|--------|---------|
| ✅ CF Live | On Cloudflare Pages, build confirmed, domain active |
| 🔶 CF Building | Connected to CF Pages, build succeeded, domain TBD |
| 🔷 CF Setup | In cf-setup-all.ps1 batch, not yet verified |
| 🟡 Netlify | Still on Netlify (do not touch until CF ready) |
| 🔲 Not deployed | On GitHub, no hosting connected yet |

---

## Platform Context

**Migration: COMPLETE (2026-07-01).** All 38 byownerhub repos are now on Cloudflare Pages.
- DNS CNAMEs fixed for 21 domains that were previously pending.
- `nodejs_compat` compatibility flag set across CF Pages projects.
- All 38 sites redeployed successfully after the flag + DNS fixes.
- **Exceptions (stay on Netlify):** `fsbo-hub` and `solar-hub` — not migrated. fsbo-hub remains too complex (Supabase, state grid) for Path A static export; solar-hub held back deliberately. See Tier 1 below.
- Prior root cause of early build failures: `next.config.js` (empty) overriding `next.config.mjs` (output: export) — fixed 2026-06-23 across 8 repos.

---

## Tier 0 — Network Hub

| URL | Repo | Status | Notes |
|-----|------|--------|-------|
| `byownerhub.com` | `byownerhub-hub` | ✅ **CF Live** | Confirmed live 2026-06-23. Homepage redesign in progress. |

---

## Tier 1 — Flagship (Netlify, do not migrate yet)

| URL | Repo | Pages | Status | Notes |
|-----|------|-------|--------|-------|
| `fsbo.byownerhub.com` | `fsbo-hub` | 1,273 | 🟡 **Netlify** | Live on Netlify. GSC verified. Sitemap submitted 2026-06-15. Complex site — Supabase wired, SavingsCalculator, state grid. Do NOT migrate until CF Path B (Workers runtime) is ready. `next.config.js` still has empty config — needs `output: 'export'` added before any CF Pages attempt. Confirmed staying on Netlify as of 2026-07-01 network-wide migration. Inline flatfee link added to `MLSComparison.tsx`; footer domain fixed `flatfee.byownerhub.com` → `flatfeemls.byownerhub.com` (commit `c3a038a`, 2026-07-01). |
| `car.byownerhub.com` | `car-by-owner` | 57+ | 🟡 **Netlify** | Live on Netlify. SSL active. GSC verified 2026-06-15. 10 state form child pages added 2026-07-01 (MV-912 NY, REG 135 CA, Form 130-U TX, HSMV 82040 FL, MV-4ST PA, BMV 3774 OH, VSD 703 IL, T-7 GA, MVR-1 NC, SUT-1 VA); sitemap updated; VA page factual error fixed. |

---

## Tier 2 — CF Pages Batch (19 repos from cf-setup-all.ps1)

*All rows below confirmed ✅ CF Live as of 2026-07-01 (DNS CNAMEs fixed + nodejs_compat flag set + redeployed network-wide). Prior per-repo build-fix notes kept for history.*

| URL | Repo | CF Project | Status | Build Fix Applied | Notes |
|-----|------|-----------|--------|-------------------|-------|
| `investor.byownerhub.com` | `investor-hub` | `investor-hub` | ✅ **CF Live** | next.config.js removed | State pages for all 50 states committed. LendingTree + Rocket Mortgage CTAs. fix-and-flip, brrrr, buy-and-hold, financing nav pages added to `src/app/` and pushed 2026-07-01. Root cause of nav 404s was `netlify.toml` misconfigured for server-render vs static export — fixed 2026-07-01. |
| `buyer.byownerhub.com` | `buyer-hub` | `buyer-hub` | ✅ **CF Live** | next.config.js removed | Build confirmed success 2026-06-23. |
| `55plus.byownerhub.com` | `55plus-hub` | `55plus-hub` | ✅ **CF Live** | main branch created | State pages committed. LendingTree + Rocket Mortgage CTAs. DNS CNAME fixed 2026-07-01. |
| `condo.byownerhub.com` | `condo-hub` | `condo-hub` | ✅ **CF Live** | next.config.js removed | DNS CNAME fixed 2026-07-01. |
| `rent.byownerhub.com` | `frbo-hub` | `frbo-hub` | ✅ **CF Live** | next.config.js removed | DNS CNAME fixed 2026-07-01. |
| `landlord.byownerhub.com` | `landlord-hub` | — | 🟡 **Netlify** | n/a | CORRECTION 2026-07-04: DNS points to `byownerlandlordhub.netlify.app` — this is on **Netlify**, not CF Pages. Serving fine. |
| `commercial.byownerhub.com` | `commercial-hub` | `commercial-hub-523` | ✅ **CF Live** | next.config.js removed | DNS CNAME fixed 2026-07-01. |
| `firsttimebuyer.byownerhub.com` | `firsttimebuyer-hub` | `firsttimebuyer-hub` | ✅ **CF Live** | next.config.js removed | Confirmed live 2026-06-29. ⚠️ firsttimebuyerhub.com (standalone) is NOT the correct URL. |
| `flatfee.byownerhub.com` | `flatfee-hub` | `flatfee-hub` | ✅ **CF Live** | opengraph fix done | Confirmed live 2026-06-29. ⚠️ flatfeemlshub.com (standalone) is NOT the correct URL. |
| `closing.byownerhub.com` | `closing-hub` | `closing-hub` | ✅ **CF Live** | opengraph fix done | Confirmed live 2026-06-29. ⚠️ closinghub.com (standalone) is an UNRELATED MN title company — do not link to it. |
| `biz.byownerhub.com` | `biz-hub` | `biz-hub` | ✅ **CF Live** | n/a | DNS CNAME fixed 2026-07-01. |
| `boat.byownerhub.com` | `boat-hub` | `boat-hub` | ✅ **CF Live** | n/a | DNS CNAME fixed 2026-07-01. 5 broken NVDC links fixed (`dcms.uscg.mil` → `dco.uscg.mil` NVDC eStorefront), commit `bba41bd` (2026-07-01). |
| `divorce.byownerhub.com` | `divorce-hub` | `divorce-hub` | ✅ **CF Live** | next.config.js removed | DNS CNAME fixed 2026-07-01. |
| `estate.byownerhub.com` | `estate-hub` | `estate-hub-2op` | ✅ **CF Live** | n/a | Tailwind palette fix done on Netlify previously. DNS CNAME fixed 2026-07-01. |
| `funeral.byownerhub.com` | `funeral-hub` | `funeral-hub` | ✅ **CF Live** | n/a | DNS CNAME fixed 2026-07-01. |
| `insurance.byownerhub.com` | `insurance-hub` | `insurance-hub` | ✅ **CF Live** | n/a | DNS CNAME fixed 2026-07-01. |
| `land.byownerhub.com` | `land-hub` | `land-hub` | ✅ **CF Live** | n/a | DNS CNAME fixed 2026-07-01. Riparian Rights section added to how-it-works guide, commit `195cb75` (2026-07-01). |
| `ftb.byownerhub.com` | `ftb-hub` | `ftb-hub` | ✅ **CF Live** | n/a | No domain configured previously. Likely duplicate of firsttimebuyer-hub. DNS CNAME fixed 2026-07-01. |

---

## Tier 3 — Now on CF Pages (migrated 2026-07-01)

*All repos below moved from GitHub-only/not-deployed to ✅ CF Live on 2026-07-01, except `solar-hub` which stays on Netlify (see Tier 1-style exception, noted in Platform Context above).*

| URL | Repo | Status | Notes |
|-----|------|--------|-------|
| `mobile.byownerhub.com` | `mobile-hub` | ✅ **CF Live** | next.config.js removed 2026-06-23. Migrated + DNS CNAME fixed 2026-07-01. |
| `probate.byownerhub.com` | `probate-hub` | ✅ **CF Live** | Private repo, complex content. Migrated + DNS CNAME fixed 2026-07-01. |
| `lien.byownerhub.com` | `lien-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `llc.byownerhub.com` | `llc-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `timeshare.byownerhub.com` | `timeshare-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. Candidate for kill per site-bucketing decision (open item). |
| `contractor.byownerhub.com` | `contractor-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `inspection.byownerhub.com` | `inspection-hub` | ✅ **CF Live** | Tailwind fix done. Migrated + DNS CNAME fixed 2026-07-01. |
| `trust.byownerhub.com` | `trust-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `solar.byownerhub.com` | `solar-hub` | 🔲 **Not deployed** | CORRECTION 2026-07-04: NOT on Netlify and NOT on CF Pages — no hosting exists anywhere. DNS does not resolve. `str-hub` links a "Solar Hub" card here → dead end. Needs a CF Pages project stood up from the `solar-hub` repo. |
| `relocation.byownerhub.com` | `relocation-hub` | ✅ **CF Live** | NEW 2026-07-04: deployed on CF Pages project `relocation-hub-344` (static export). Custom domain active. Leftover duplicate `relocation-hub` **Worker** should be deleted. |
| `rv.byownerhub.com` | `rv-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. Candidate for kill per site-bucketing decision (open item). |
| `eviction.byownerhub.com` | `eviction-hub` | ✅ **CF Live** | 'use client' fix done. Migrated + DNS CNAME fixed 2026-07-01. |
| `moto.byownerhub.com` | `moto-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. Candidate for kill per site-bucketing decision (open item). |
| `trademark.byownerhub.com` | `trademark-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `str.byownerhub.com` | `str-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `mortgage.byownerhub.com` | `mortgage-hub` | ✅ **CF Live** | Migrated + DNS CNAME fixed 2026-07-01. |
| `funeral.byownerhub.com` | `funeral-hub` | ✅ **CF Live** | Duplicate row of Tier 2 `funeral-hub` entry above — same repo, now confirmed CF Live 2026-07-01. |

**Total (corrected 2026-07-04): 37 subdomains + apex on CF Pages.** On **Netlify:** `fsbo-hub`, `car-by-owner`, `landlord-hub`. **Not deployed:** `solar-hub`. Newly live: `relocation-hub` (CF Pages, 2026-07-04).

---

## Key Technical Notes

### CF Pages Migration Wrap-Up (2026-07-01)
- All 38 repos confirmed on Cloudflare Pages.
- 21 domains had pending/misconfigured DNS CNAMEs — all fixed and pointed at CF Pages.
- `nodejs_compat` compatibility flag set on CF Pages projects (required for some Next.js API routes/edge runtime behavior).
- All 38 sites redeployed after the DNS + compat flag fixes.
- `fsbo-hub` and `solar-hub` intentionally excluded — remain on Netlify.

### Confirmed Build Fix (2026-06-23)
Having both `next.config.js` AND `next.config.mjs` in a repo causes Next.js to use `next.config.js` (CommonJS, takes precedence), silently ignoring the `output: 'export'` in the `.mjs` file. All CF Pages builds were failing with "Output directory 'out' not found." Fix: delete `next.config.js`. Applied to: byownerhub-hub, buyer-hub, commercial-hub, condo-hub, firsttimebuyer-hub, frbo-hub, landlord-hub, mobile-hub, divorce-hub.

### Domain Config Note
Several CF Pages projects were configured with standalone domains (not byownerhub.com subdomains):
- `closing-hub` → closinghub.com
- `firsttimebuyer-hub` → firsttimebuyerhub.com  
- `flatfee-hub` → flatfeemlshub.com
- `landlord-hub` → landlordhub.com

Verify whether these standalone domains are registered and DNS is on Cloudflare.

### fsbo-hub CF Pages Note
fsbo-hub has `next.config.js` with empty config and NO `next.config.mjs`. Before connecting to CF Pages: add `output: 'export'` to `next.config.js` (or add `next.config.mjs` and delete `.js`). Given complexity (Supabase, state grid, forms), may need Path B (Workers runtime) instead of Path A.
