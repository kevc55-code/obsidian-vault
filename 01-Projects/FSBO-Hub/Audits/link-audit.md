---
type: audit
audit-kind: link
project: FSBO-Hub
status: canonical
last-verified: 2026-09-01
---

# Network Link Audit — Latest Run

**Date:** 2026-09-01 (weekly scheduled run, baseline still 2026-07-13 — no `--update-baseline` run yet).

Sites: 38 | Pages: 3,275 | Unique external links: 3,546
**NEW failures: 7 reported → 0 real.** 6 false positives (transient `??`, all live-verified 200), 1 known `ohio.gov` geo-block. | total failures: 9 (2 already in baseline) | resolved since baseline: 155

**No real link rot** — no internal 404s, no new external rot, alias 301s + form CORS all green. Mirror-branch drift persists (~21 repos, cosmetic — see below).

Prev run (2026-08-24) archived to `Audits/archive/link-audit-2026-08-24.md`.
Full raw output: `buyer-hub/tools/network-audit/report.md` + `results.json`.

> **Note on this run:** the `report.md` on disk was transiently in a partial state mid-crawl (an earlier read showed 11 failures / no drift section); the authoritative completed run (exit 0, `bliwebm24`) is **7 failures + drift section present**, and that is what's triaged here.

**Slack posting DONE this run** — Kevin explicitly asked for it in-session (overriding the 2026-07-26 standing "Slack off"). Parent + 3 thread replies posted to `#network-audit-results` (parent ts `1788266323.222339`): 🟢 allowlist `insurance.ohio.gov` + re-baseline; 🔴 flag mirror-branch drift (~21 repos, options A/B/C); ℹ️ the 6 fsbo `??` are false positives, no action.

## ✅ Resolved since last run (2026-08-24)

- **`landlord.byownerhub.com` fully back** — 51 pages, sitemap ✓ this run (was **1 page / NO SITEMAP** on 08-24, a stale dead-Netlify snapshot). The 08-20 DNS + CF Pages custom-domain cutover ([[open-items]]) has fully propagated; the site now crawls clean.
- **08-24 orphan sitemap gaps closed** — buyer/divorce/estate/funeral-hub `/disclaimer` `/privacy` `/terms` no longer flagged (absent from this run's orphan list); page counts rose accordingly (buyer 54→57, divorce 56→59, estate 56→58, funeral 55→58). Confirms the same-day 08-24 fix commits (buyer `1d4ca22`, divorce `dc5b74d`, estate `ae62d2a`, funeral `5137ac1`) are deployed.

## ⚪ False positives — no action needed, all live-verified (6 of the 7 NEW)

Crawler logged status `??` (transient timeout under 16-way concurrency), not a real 404. Re-checked each directly → all **200**:
- fsbo: `/kansas-fsbo-guide` (on `/markets/`)
- fsbo: `/boston/framingham`, `/minneapolis/coon-rapids`, `/sarasota/venice` (suburb pages)
- fsbo: `/_next/static/chunks/app/north-carolina-fsbo-guide/page-219512b54683b68b.js` (asset on `/north-carolina-fsbo-guide/` — page itself 200)
- fsbo: `/dallas/blog/dallas-fort-worth-flat-fee-mls-comparison-2026` (on `/dallas/blog/`)

Never in baseline, not really failing — different pages each week (whichever timed out), so they self-clear next run. No `--update-baseline` needed.

## 🟡 Known geo-block — not a real user-facing break (1 of the 7 NEW)

- `insurance.byownerhub.com/states/ohio/` → `insurance.ohio.gov/consumers/homeowner/homeowners-insurance-guide` → 404 **from this machine**. Repeat from 08-24; cause now clear: **`insurance.ohio.gov` root AND `ohio.gov` root also 404 from here**, while a US-based web search returns the exact guide URL live with full content. Same `ohio.gov` non-US/datacenter geo-block already documented for `ohio.gov` / `ohiodnr.gov` / `odh.ohio.gov` ([[open-items]] 2026-07-13). The link is fine for real (US) visitors.
  - **Recommendation (next interactive session):** add `insurance.ohio.gov` to `buyer-hub/tools/network-audit/allowlist.json` geo-blocked hosts so it stops surfacing, then `node audit.mjs --update-baseline`. Not done here (task must not modify audit config).

## ⚠️ Mirror-branch drift — ~21 repos, unchanged from 08-24 (NOT resolved)

`origin/main ≠ origin/master` on: frbo, **buyer**, commercial, firsttimebuyer, flatfee, biz, **estate**, **funeral**, mobile, lien, llc, timeshare, inspection, trust, rv, eviction, moto, str, mortgage, new-build, foreclosure, auction. Same set as 08-24 (19) plus buyer/estate/funeral, which drifted when their 08-24 orphan-sitemap fixes landed on one branch only (e.g. buyer: main=`d58fec4` has the route files, master=`1d4ca22` also has the sitemap entry — buyer-hub deploys from `master`, so the fix is live regardless).

Per [[network-audit-automation]], `main` is the deployed branch (except the handful pinned to `master` like buyer/55plus/condo/foreclosure) and drift is cosmetic, not a live-serving problem — the resolved items above confirm the live sites are current. But the drift has now persisted across two weekly runs without self-resyncing. FF-safety (`git merge-base --is-ancestor`) not verified this pass. Worth a batch `git push origin main:master` (or the reverse per repo) in an interactive session.

## Per-site (this run)

| domain | pages | sitemap | bad internal |
|---|---|---|---|
| byownerhub.com | 6 | ✓ | 0 |
| fsbo.byownerhub.com | 1228 | ✓ | 6 (all false positives, see above) |
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
| inspection.byownerhub.com | 56 | ✓ | 0 |
| trust.byownerhub.com | 56 | ✓ | 0 |
| relocation.byownerhub.com | 55 | ✓ | 0 |
| rv.byownerhub.com | 55 | ✓ | 0 |
| eviction.byownerhub.com | 56 | ✓ | 0 |
| moto.byownerhub.com | 56 | ✓ | 0 |
| trademark.byownerhub.com | 55 | ✓ | 0 |
| str.byownerhub.com | 67 | ✓ | 1 (known dead solar.byownerhub.com link, tracked, unchanged) |
| mortgage.byownerhub.com | 56 | ✓ | 0 |
| new-build.byownerhub.com | 51 | ✓ | 0 |
| foreclosure.byownerhub.com | 51 | ✓ | 0 |
| auction.byownerhub.com | 52 | ✓ | 0 |

## Alias 301s — all ✅
flatfee → flatfeemls, newbuild → new-build, frbo → rent.

## Form CORS (fsbo /api/subscribe) — all ✅
biz, estate, str, eviction, moto façade origins all return 204 with correct ACAO.

## ✅ Resolved since baseline (155) — unchanged from 08-24

Large cleanup from the network-wide SEO remediation project — mostly `hud.gov` state-page 404s (the `/states/x_y` → `/states/x-y` reorg, now fully cleared), vital-records/boating/court-directory link rot across ~20 states, and the condo/fsbo/investor orphan-sitemap fixes.

---
*Slack integration posted this run to `#network-audit-results` — Kevin re-enabled it for this run in-session (thread `1788266323.222339`). The 2026-07-26 network-wide "Slack off" no longer applies to this channel.*
