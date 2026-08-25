# Network Link Audit — Latest Run

**Date:** 2026-08-24 (weekly scheduled run, baseline still 2026-07-13 — no `--update-baseline` run yet).

Sites: 38 | Pages: 3,214 | Unique external links: 3,490
**NEW failures: 21 reported → 3 real external 404s (2 with replacements found), 11 real orphan-sitemap gaps, 7 false positives (verified live)** | total failures: 23 (2 already in baseline) | resolved since baseline: 155

Full raw output: `buyer-hub/tools/network-audit/report.md` + `results.json`.

**Slack posting skipped this run** — two independent reasons: (1) the `#network-audit-results` Slack MCP connection isn't authenticated in this non-interactive session, and (2) per [[bugs-feature-routines]], Kevin turned off all Slack integrations network-wide on 2026-07-26 — that instruction predates and supersedes the per-task Slack-posting step below. Proposals are listed here for direct action next session instead.

## 🔴 Real, actionable

**Orphan sitemap gaps (11)** — real bug, easy one-line-per-repo fix. Root cause: commit `d58fec4` (buyer-hub) and its siblings (`e8e9d6f` divorce-hub, `c7abf22` estate-hub, `c216f8f` funeral-hub — "add the privacy, terms and disclaimer pages the footer promised") added `/disclaimer`, `/privacy`, `/terms` route files but never added them to `sitemap.ts`, so they're live but Google-invisible. condo-hub and investor-hub already do this correctly (static entries, `priority: 0.3, changeFrequency: 'yearly'`) — same pattern to copy.
- `buyer-hub/src/app/sitemap.ts` — missing all 3, insert after line 9
- `divorce-hub/src/app/sitemap.ts` — missing all 3, insert after line 8
- `funeral-hub/src/app/sitemap.ts` — missing all 3, insert after line 8
- `estate-hub/src/app/sitemap.ts` — has `/privacy` (line 9) already; missing only `/disclaimer` and `/terms`

**External 404s (3)**
- `firsttimebuyer.byownerhub.com/california/first-time-buyer-guide/` → `www.calhfa.ca.gov/homeownership/programs/myhome.htm` 404. CalHFA restructured `/homeownership/` → `/homebuyer/`. **Verified live replacement: `https://www.calhfa.ca.gov/homebuyer/programs/myhome.htm`**
- same page → `www.calhfa.ca.gov/dreamforall/` 404. **Verified live replacement: `https://www.calhfa.ca.gov/dream/`**
- `insurance.byownerhub.com/states/ohio/` → `insurance.ohio.gov/consumers/homeowner/homeowners-insurance-guide` 404. Checked further: **the entire insurance.ohio.gov domain is 404ing right now**, including its root (stale `Last-Modified: 2023`) — looks like an agency-side migration in progress. No safe replacement found; recommend re-checking next cycle rather than guessing a URL.

## ⚪ False positives — no action needed, confirmed live in-browser (7 of the 21 NEW)

Flagged by the crawler as `[internal]` 404s but actually logged status `??` (transient/timeout), not a real 404:
- fsbo: `/charlotte/monroe`, `/las-vegas/laughlin`, `/philadelphia/doylestown`, `/san-antonio/cibolo` — all present in `suburbs.ts` with correct `metro_slug`, no code/data divergence found, live-verified 200.
- land: `/states/nebraska`, `/states/new-hampshire`, `/states/north-dakota` — all present in `states.ts`, live-verified 200.

These were never in baseline and aren't really failing, so they should just drop out of next week's run on their own — no `--update-baseline` needed.

## ⚠️ Mirror-branch drift — 19 repos (was 0 as of 08-18)

`origin/main ≠ origin/master` on: frbo, commercial, firsttimebuyer, flatfee, biz, mobile, lien, llc, timeshare, inspection, trust, rv, eviction, moto, str, mortgage, new-build, foreclosure, auction. Notable regression from the "first clean drift check in the audit's history" logged 08-18 ([[open-items]]). Per [[network-audit-automation]], `main` is the deployed branch and drift is cosmetic, not a live-serving problem — but going from 0 to 19 repos in one week is a bigger jump than the routine 1-4 seen elsewhere, worth Kevin's eyes rather than assuming it's fine everywhere. Full FF-safety verification (`git merge-base --is-ancestor`) wasn't run this pass.

## Per-site (this run)

| domain | pages | sitemap | bad internal |
|---|---|---|---|
| byownerhub.com | 6 | ✓ | 0 |
| fsbo.byownerhub.com | 1228 | ✓ | 4 (all false positives, see above) |
| car.byownerhub.com | 67 | ✓ | 0 |
| landlord.byownerhub.com | 1 | ✗ NONE | 0 |
| rent.byownerhub.com | 54 | ✓ | 0 |
| buyer.byownerhub.com | 54 | ✓ | 0 |
| investor.byownerhub.com | 58 | ✓ | 0 |
| 55plus.byownerhub.com | 55 | ✓ | 0 |
| condo.byownerhub.com | 54 | ✓ | 0 |
| commercial.byownerhub.com | 66 | ✓ | 0 |
| firsttimebuyer.byownerhub.com | 52 | ✓ | 0 |
| flatfeemls.byownerhub.com | 64 | ✓ | 0 |
| closing.byownerhub.com | 61 | ✓ | 0 |
| biz.byownerhub.com | 56 | ✓ | 0 |
| boat.byownerhub.com | 61 | ✓ | 0 |
| divorce.byownerhub.com | 56 | ✓ | 0 |
| estate.byownerhub.com | 56 | ✓ | 0 |
| funeral.byownerhub.com | 55 | ✓ | 0 |
| insurance.byownerhub.com | 56 | ✓ | 0 |
| land.byownerhub.com | 56 | ✓ | 3 (all false positives, see above) |
| mobile.byownerhub.com | 59 | ✓ | 0 |
| probate.byownerhub.com | 51 | ✓ | 0 |
| lien.byownerhub.com | 56 | ✓ | 0 |
| llc.byownerhub.com | 54 | ✓ | 0 |
| timeshare.byownerhub.com | 56 | ✓ | 0 |
| contractor.byownerhub.com | 56 | ✓ | 0 |
| inspection.byownerhub.com | 56 | ✓ | 0 |
| trust.byownerhub.com | 56 | ✓ | 0 |
| relocation.byownerhub.com | 55 | ✓ | 0 |
| rv.byownerhub.com | 55 | ✓ | 0 |
| eviction.byownerhub.com | 56 | ✓ | 0 |
| moto.byownerhub.com | 56 | ✓ | 0 |
| trademark.byownerhub.com | 55 | ✓ | 0 |
| str.byownerhub.com | 67 | ✓ | 1 (known solar-hub link, tracked, unchanged) |
| mortgage.byownerhub.com | 56 | ✓ | 0 |
| new-build.byownerhub.com | 51 | ✓ | 0 |
| foreclosure.byownerhub.com | 51 | ✓ | 0 |
| auction.byownerhub.com | 52 | ✓ | 0 |

## Alias 301s — all ✅
flatfee → flatfeemls, newbuild → new-build, frbo → rent.

## Form CORS (fsbo /api/subscribe) — all ✅
biz, estate, str, eviction, moto façade origins all return 204 with correct ACAO.

## ✅ Resolved since baseline (155)

Large cleanup, consistent with the recent network-wide SEO remediation project — mostly `hud.gov` state-page 404s (HUD's `/states/x_y` → `/states/x-y` reorg now fully cleared), vital-records/boating/court-directory link rot across ~20 states, and the condo/fsbo/investor orphan-sitemap fixes from the 07-20 session.

---
*Slack integration did not post this run — see note at top (auth unavailable + standing user instruction to keep Slack integrations off).*
