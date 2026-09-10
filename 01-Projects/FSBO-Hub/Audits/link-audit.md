---
type: audit
audit-kind: link
project: FSBO-Hub
status: canonical
last-verified: 2026-09-07
---

# Network Link Audit — Latest Run

**Date:** 2026-09-07 (weekly scheduled run, baseline still 2026-07-13 — no `--update-baseline` run yet).

Sites: 38 | Pages: 3,328 | Unique external links: 3,612
**NEW failures: 32 reported → 6 real.** 24 false positives (fsbo internal `??` / code 0 transient, all live-verified 200 — count inflated this run, see note), 5 real external 404s, 1 recurring `ohio.gov`-family geo-block. Plus 1 ambiguous (`texas.gov` root 404 from this machine) and a **real stale deploy on auction-hub**. | total failures: 34 (2 already in baseline: `solar.byownerhub.com`, `homeinspector.org/findaninspector`) | resolved since baseline: 155 (unchanged).

Prev run (2026-09-01) archived to `Audits/archive/link-audit-2026-09-01.md`.
Full raw output: `buyer-hub/tools/network-audit/report.md` + `results.json` (sitting modified-but-uncommitted in the working tree).

> **Note on this run:** `audit.mjs` OOM-crashed on the first attempt (Node v25.8.1, "Fatal process out of memory: Zone"); re-run with `node --max-old-space-size=4096 audit.mjs` completed clean (exit 1 = new failures present). The memory pressure almost certainly drove the unusually high fsbo `??` count (24 vs. 6 on 09-01) — every one re-checked directly returned 200. Audit script/config not modified (task constraint).

## ⚪ False positives — no action, all 24 live-verified 200 (24 of the 32 NEW)

fsbo internal links logged `code: 0` (transient timeout under 16-way concurrency, worse this run due to the OOM/heap pressure), rendered `??` in the report — not real 404s. **All 24 re-checked directly → 200.** Sample: `/baton-rouge`, `/wichita`, `/dayton`, `/under-contract/texas`, `/under-contract/west-virginia`, `/charlotte/mint-hill`, `/dayton/beavercreek`, `/denver/arvada`, `/new-orleans/gretna`, `/tampa/palm-harbor`, `/fort-collins/loveland`, `/huntsville/athens`, `/san-diego/santee`, `/tulsa/sand-springs`, `/wichita/derby`, 3× `_next/static/chunks/.../{state}-fsbo-guide/page-*.js` assets, 2× `/{metro}/blog/{slug}`. Never in baseline, different pages each week — self-clear next run, no `--update-baseline` needed. `/under-contract/*` are the new 09-04 route ([[open-items]]) and resolve fine.

## 🔴 Real external link rot (5 of the 32 NEW) — owning repo: fsbo, firsttimebuyer

- **fsbo `/state-requirements/`** → `eforms.com/images/2018/08/Tennessee-Assoc-of-Realtors-Purchase-Agreement.pdf` → **404**. eForms retired the old `/images/*.pdf` files. **Replacement: `https://eforms.com/purchase-agreements/tn/`** (verified 200). Check the sibling state PDFs on the same page — likely the same rot pattern for any still pointing at `eforms.com/images/`.
- **fsbo metro pages** → 4× Redfin "recently sold" deep links → **404**: `/albany/` → `redfin.com/city/filter/property-type=house,include=sold-3mo/Albany-NY`; `/anchorage/` → same pattern `Anchorage-AK`; `/atlanta/` → `redfin.com/city/27677/GA/Atlanta/recently-sold`; `/bakersfield/` → filter pattern `Bakersfield-CA`. Redfin root + shallow `/city/{id}/{ST}/{City}` URLs return 200, but Redfin also intermittently answers 202 (bot challenge) — mixed signal. The `include=sold-3mo` filter-URL and `/recently-sold` path look like a **changed/dead Redfin URL scheme**. Only the alphabetically-first 4 metros flagged (dedupe / per-host cap in the crawler, or only some metros carry these links). **Needs:** US-browser verification, then either fix the link pattern in fsbo's metro-page template or add `www.redfin.com` to `allowlist.json` `bot_blocked_hosts`.
- **firsttimebuyer `/missouri/first-time-buyer-guide/`** → `mohousing.com/homeownership/` → **404** (root `mohousing.com/` is 200). Missouri Housing Development Commission reorganized; `www.mhdc.com/` is 200 but `/homeownership/` 404s. **Needs a real replacement** — current MHDC first-time-homebuyer / "First Place Loan" landing page (verify before applying).

## 🟡 Recurring geo-block — not user-facing (1 of the 32 NEW)

- `insurance.byownerhub.com/states/ohio/` → `insurance.ohio.gov/consumers/homeowner/homeowners-insurance-guide` → 404 **from this machine**. Same `ohio.gov`-family non-US geo-block documented 08-24 & 09-01 (`ohio.gov` / `ohiodnr.gov` / `odh.ohio.gov` already in `allowlist.json`). Fine for real US visitors. **Recommendation stands (unactioned since 09-01):** add `insurance.ohio.gov` to `allowlist.json` `geo_blocked_404_hosts`, then `node audit.mjs --update-baseline`. Not done here (task must not modify audit config).

## ❓ Ambiguous — verify from US (1 of the 32 NEW)

- `land.byownerhub.com/states/texas/` → `www.texas.gov/` **and** bare `texas.gov/` both → 404 from this machine. A state's root portal 404ing from one vantage fits the same Akamai/edge geo-discrimination pattern as `ohio.gov` — but not previously seen for Texas, so low confidence. **If geo:** allowlist `texas.gov` + `www.texas.gov`. **If genuinely dead:** land-hub's Texas page needs a real link (`https://gov.texas.gov/` or `https://www.tdhca.state.tx.us/`).

## ⚠️ Stale deploy — auction-hub (REAL, new characterization)

`auction.byownerhub.com` live homepage serves the **`main`** branch — `<title>` "AuctionHub — Buy Homes at Foreclosure Auction Without an Agent", the `%s | AuctionHub` title template, and the long meta description all match `origin/main` exactly. `origin/master` is **7 commits ahead** with the P3b/P8 SEO remediation that is **not live**: title/description shortening to SERP width, state-page content expansion (~185 → ~332 words), Organization/WebSite/CollectionPage JSON-LD, `/states` meta-description trims, and the `%s | Brand` template removal.

- Clean FF verified: `origin/main` is a strict ancestor of `origin/master` (7 commits, zero unique commits on `main`).
- **Fix:** FF `main` up to `origin/master` (`git push origin origin/master:main` from an up-to-date clone), which pushes the SEO work live — **or**, if auction-hub actually deploys from `master` and the build is merely stale, a CF Pages "Retry deployment". Kevin should confirm auction-hub's intended production branch: `new-build-hub` has the mirror-image drift (`master` ahead by 4) yet its live site *already* serves `master`, so the deploy-branch mapping is not consistent network-wide.

## ⚠️ Mirror-branch drift — 22 repos, unchanged, 3rd weekly run standing

All 22 pairs are **clean fast-forwards** (no diverged pair). Set first appeared 08-24, essentially frozen since 09-01.

- **`main` ahead / `master` lagging (18)** — deploy-from-`main`, live is current, cosmetic: frbo, commercial, str, mortgage, firsttimebuyer, flatfee, biz, estate, funeral, mobile, lien, llc, timeshare, inspection, trust, rv, eviction, moto.
- **`master` ahead / `main` lagging (4)**: **buyer** & **foreclosure** are `master`-pinned per [[network-audit-automation]] → live current, cosmetic; **auction** → live is stale (see above); **new-build** → `master` ahead by 4 but live already serves `master`, so only the `main` branch is stale (cosmetic).

Per [[network-audit-automation]] `main` is normally the deployed branch and drift is cosmetic — the resolved items below confirm live sites are current — but it has now persisted across three weekly runs without self-resyncing, and auction-hub proves the assumption isn't universal. Worth a batch resync in an interactive session (directional, per-repo — there is no single push that fixes all 22).

## ✅ Resolved / still-healthy since last run (2026-09-01)

- `landlord.byownerhub.com` still fully healthy — 51 pages, sitemap ✓ (recovered 09-01 after the 08-20 DNS + CF Pages cutover; stays clean).
- 08-24 orphan-sitemap gaps stay closed — buyer 57 / divorce 59 / estate 58 / funeral 58 pages, none re-flagged.
- Nothing *newly* resolved this run; `resolved since baseline` steady at 155.

## Per-site (this run)

| domain | pages | sitemap | bad internal |
|---|---|---|---|
| byownerhub.com | 6 | ✓ | 0 |
| fsbo.byownerhub.com | 1281 | ✓ | 24 (all false positives — transient `??`, live-verified 200) |
| car.byownerhub.com | 67 | ✓ | 0 |
| landlord.byownerhub.com | 51 | ✓ | 0 |
| rent.byownerhub.com | 54 | ✓ | 0 |
| buyer.byownerhub.com | 57 | ✓ | 0 |
| investor.byownerhub.com | 58 | ✓ | 0 |
| 55plus.byownerhub.com | 55 | ✓ | 0 |
| condo.byownerhub.com | 54 | ✓ | 0 |
| commercial.byownerhub.com | 66 | ✓ | 0 |
| firsttimebuyer.byownerhub.com | 52 | ✓ | 0 |
| flatfeemls.byownerhub.com | 64 | ✓ | 0 |
| closing.byownerhub.com | 61 | ✓ | 0 |
| biz.byownerhub.com | 56 | ✓ | 0 |
| boat.byownerhub.com | 61 | ✓ | 0 |
| divorce.byownerhub.com | 59 | ✓ | 0 |
| estate.byownerhub.com | 58 | ✓ | 0 |
| funeral.byownerhub.com | 58 | ✓ | 0 |
| insurance.byownerhub.com | 56 | ✓ | 0 |
| land.byownerhub.com | 56 | ✓ | 0 |
| mobile.byownerhub.com | 59 | ✓ | 0 |
| probate.byownerhub.com | 51 | ✓ | 0 |
| lien.byownerhub.com | 56 | ✓ | 0 |
| llc.byownerhub.com | 54 | ✓ | 0 |
| timeshare.byownerhub.com | 56 | ✓ | 0 |
| contractor.byownerhub.com | 56 | ✓ | 0 |
| inspection.byownerhub.com | 56 | ✓ | 1 (known `homeinspector.org/findaninspector` 404, in baseline) |
| trust.byownerhub.com | 56 | ✓ | 0 |
| relocation.byownerhub.com | 55 | ✓ | 0 |
| rv.byownerhub.com | 55 | ✓ | 0 |
| eviction.byownerhub.com | 56 | ✓ | 0 |
| moto.byownerhub.com | 56 | ✓ | 0 |
| trademark.byownerhub.com | 55 | ✓ | 0 |
| str.byownerhub.com | 67 | ✓ | 1 (known dead `solar.byownerhub.com` link, in baseline, unchanged) |
| mortgage.byownerhub.com | 56 | ✓ | 0 |
| new-build.byownerhub.com | 51 | ✓ | 0 |
| foreclosure.byownerhub.com | 51 | ✓ | 0 |
| auction.byownerhub.com | 52 | ✓ | 0 |

*(inspection shows 1 bad-internal in the report table but the failure is the external `homeinspector.org` link — both baseline items.)*

## Alias 301s — all ✅
flatfee → flatfeemls, newbuild → new-build, frbo → rent.

## Form CORS (fsbo /api/subscribe) — all ✅
biz, estate, str, eviction, moto façade origins all return 204 with correct ACAO.

## ✅ Resolved since baseline (155) — unchanged from 09-01

Large cleanup from the network-wide SEO remediation — mostly `hud.gov` state-page 404s (`/states/x_y` → `/states/x-y`), vital-records/boating/court-directory rot across ~20 states, and the condo/fsbo/investor orphan-sitemap fixes.

---
*Slack: attempted post to `#network-audit-results` this run — see session output for whether the connector was authenticated. Proposals for Kevin: (1) 🟢 FF auction-hub `main` → `origin/master` (verified clean FF, pushes P8 SEO live); (2) 🟢 add `insurance.ohio.gov` to `allowlist.json` geo-block list + re-baseline; (3) 🔴 replace the dead eForms TN PDF link with `eforms.com/purchase-agreements/tn/` + sweep siblings; (4) 🔴 Redfin recently-sold link pattern — fix or allowlist; (5) 🔴 mohousing.com/homeownership → current MHDC page; (6) 🔴 mirror-branch drift batch resync (22 repos, directional).*
