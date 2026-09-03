---
type: status
project: FSBO-Hub
last-verified: 2026-09-03
---

# Network — Unpushed Changes

*Last updated: 2026-09-03 (see [[SESSION-2026-09-02]] for full detail)*

---

## 🔴 Currently unpushed / uncommitted

**fsbo-hub `freemium-wip`** — still 11 commits ahead of `origin/freemium-wip`, unchanged since 08-05 (same commits: `831a09f`, `7c82d32`, `01e822c`, `a953599`, `bd6054d`, `588daec`, `707b11c`, `ef035bb`, `0dbf67d` merge, `d630097`, `721c175`). **Deploy-readiness still not re-verified** — the 07-12 check now predates ~8 weeks and seven separate vault-check sessions. Likely superseded in practice by production's real Stripe/freemium build on `fsbo-freemium-sandbox` — see [[open-items]] item 8.

**fsbo-freemium-sandbox** — two untracked deploy scripts remain (`deploy.bat`, `deploy_freemium_branch.ps1`), unchanged since 07-23; the latter still has the plaintext PAT, **still not rotated (~41 days)**. Also a staged-but-uncommitted one-line `.claude/launch.json` rename (`"fsbo-hub"` → `"fsbo-production"`, matches staging's `e84abb2`) — trivial. `master` itself is fully pushed and in sync with origin at **`c2bb429`** (6 more commits 2026-09-02 — Stripe checkout error-logging fix, homepage positioning module + free/paid hero split, commission-figure single-basis refactor — see [[SESSION-2026-09-02]]).

## ✅ Resolved 2026-09-02

**fsbo-hub `main` — Hero.tsx edit committed + pushed.** The uncommitted `src/components/Hero.tsx` edit carried since 2026-08-21 (drops the two metro-hero CTA buttons, tightens vertical padding) is now `e659fd1` "refactor(hero): drop the metro hero CTAs and tighten the spacing", **pushed**. `main` in sync with `origin/main` at `e659fd1`; working tree clean.

**fsbo-staging — pending crawler-policy edit committed; caught up to production.** The uncommitted `src/app/page.tsx` + `src/app/robots.ts` edit flagged 2026-08-25 is now committed as `1bf2a10`. `master` moved to `f3ce1c8` (7 commits 2026-09-02, all pushed / in sync with `origin/master`): the crawler-policy commit, its own preview-config name (`e84abb2`), and an independent re-build of production's positioning-module + free/paid-hero + commission-single-basis set (same messages, different hashes). Staging now lacks only production's prod-specific Stripe error-logging commit (`2feef13`).

**car-by-owner `main`** — `ba17a8d` (2026-09-02, page-level FTC disclosure above CTAs + Carfax note tidy) pushed; `main` in sync with origin.

## ✅ Resolved 2026-08-21

**str-hub `master`** — the 9-commit backlog that had been stale since 08-05 (15+ days) is now pushed, `master` in sync with `origin/master`. No new commits — just a push. (str-hub's `main` branch fix `23ce82d`, 08-05, CF Pages build/legacy-peer-deps, was already separately pushed and unrelated to this backlog.)

## ✅ Resolved since 08-05

**car-by-owner `main`** — the `b7b4286` commit flagged 08-05 is now pushed, plus two more DMV-link fixes landed and pushed: `8385113` (WY DMV 403, Akamai-blocked county page) and `ab3696c` (MS/MT DMV links pointed at wrong/dead agency pages), both dated 2026-08-05/06. Fully in sync with origin.

**fsbo-freemium-sandbox** — the large staged-but-uncommitted PDF-toolkit feature flagged 08-05 is now committed and pushed: `5888d28` ("generate per-metro downloadable PDF toolkit, gate it behind purchase") and `294ed74` ("give buyers more time to notice the toolkit download"), both 2026-08-05. `master` is in sync with `origin/master`. Untracked `deploy.bat` and `deploy_freemium_branch.ps1` remain (⚠️ the latter still contains the plaintext GitHub PAT flagged 2026-07-23 — see [[open-items]], still not rotated 27 days later, file mtime unchanged).

## ✅ Other pushed fixes this period (2026-08-05 → 08-06)

- **boat-hub** `f4fbdb5` — 16 dead/broken state agency links (Official Site/Agency, Lien Search).
- **landlord-hub** `ecb8876` — all 50 state lease-form links were 404ing after ezlandlordforms restructured their URLs; fixed.

## ℹ️ funeral-hub — trivial local branch staleness, not real drift

Local `master` branch pointer is 2 commits behind `origin/master` (`01e752e`, `95dadc8` — both already-recorded events from the 07-04 funeral-hub merge). `main` is in sync. This is just the local clone not being fast-forwarded, not unpushed work — origin already has everything. No action needed.

## ✅ Network-wide SEO remediation, pushed (2026-07-27 → 08-04)

~39 repos got an 8-phase SEO pass (title/meta formulas, JSON-LD schema, thin-content expansion, locale/copy-defect fixes) driven by `buyer-hub/tools/seo-audit`. Full phase breakdown in [[network-status]] and [[SESSION-2026-08-05]]. Confirmed pushed for every repo except str-hub `master` (still unpushed, see above).

## ✅ Pushed 2026-07-21/23 (carried forward, unchanged)

- **eviction-hub** `207d802` + `6109d90` — real court citation links, all 49 remaining states.
- **insurance-hub** `9e7bfb6` + `b5853fb` — real state DOI citation links, all 50 states.
- **trust-hub** `05758ca` + `ee60eed` — real probate-court citation links, all 50 states.
- **rv-hub** `d7132b7` — state page title/meta rewrite + real FAQ content (closes GSC rec #1).

## ✅ Everything else: committed + pushed as of 2026-08-19

Verified across the rest of the ~40-repo network (excluding `equiconnected`) — every branch tracked against its upstream. Only str-hub `master` and fsbo-hub `freemium-wip` remain ahead of origin. No other tracked file has uncommitted changes except cosmetic line-ending noise in a couple of repos and buyer-hub's network-audit output (below).

## ℹ️ fsbo-hub — large pile of untracked scratch files (not flagged as a problem)

`fsbo-hub`'s working tree still has ~35 untracked local artifacts (xlsx/pptx/pdf exports, slide JPGs, one-off audit scripts, JSON scan results) plus a `tsconfig.tsbuildinfo` build artifact. Not gitignored, likely intentionally kept local. No action needed.

## ℹ️ buyer-hub — network-audit output, tracked but modified-uncommitted

`tools/network-audit/report.md` and `results.json` **are tracked in git** (last committed `0a37719`, 07-28) — correcting the prior vault note that called these "untracked by design." The working tree currently holds the fresh 2026-08-18 weekly-audit run as an uncommitted modification on top of that commit. Worth asking Kevin whether the intent is to commit each week's run or leave it as scratch — as-is, `git log` on these files understates how current the audit data actually is. Findings from this run are in [[open-items]] and [[network-status]].

**fsbo-hub branches:**
- `main` — production (Netlify auto-deploys), in sync with origin at `5bd8207`; one uncommitted `Hero.tsx` edit locally (see above).
- `freemium-wip` — older $99 Stripe toolkit paywall design, now also carries all July content/GSC fixes. 11 commits ahead of origin, not deployed, likely superseded by production's real freemium build on `fsbo-freemium-sandbox`. See [[open-items]] item 8.

**Correction, 2026-08-21:** `fsbo-hub` is NOT actually production — `fsbo-freemium-sandbox` is (confirmed by Kevin 2026-08-19, see [[fsbo-repo-map]]). `fsbo-hub main`'s Netlify site still exists and is live-served separately; verify which domain it actually serves before assuming it's fsbo.byownerhub.com.
