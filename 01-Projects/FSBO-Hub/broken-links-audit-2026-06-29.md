# ByOwnerHub Network — Broken Link Audit
*Audited: 2026-06-29 | Method: Homepage JS HEAD-request scan via Chrome*

---

## Summary

| Site | Links Checked | Broken | Status |
|------|--------------|--------|--------|
| byownerhub.com | 9 | 0 | ✅ Clean |
| investor.byownerhub.com | 59 | **7** | 🔴 Fix needed |
| buyer.byownerhub.com | 54 | 0 | ✅ Clean |
| car.byownerhub.com | 17 | 0 | ✅ Clean |
| 55plus.byownerhub.com | 56 | **4** | 🔴 Fix needed |
| condo.byownerhub.com | 55 | **3** | 🔴 Fix needed |
| rent.byownerhub.com | — | — | ❌ Site not loading (error page) |
| landlord.byownerhub.com | 52 | 0 | ✅ Clean |
| commercial.byownerhub.com | 59 | 0 | ✅ Clean |
| firsttimebuyerhub.com | — | — | ⚠️ Coming Soon page (no content) |
| flatfeemlshub.com | — | — | ❌ DNS/connection error |
| closinghub.com | — | — | ⚠️ Blank page (0 links rendered) |
| biz.byownerhub.com | 55 | 0 | ✅ Clean |
| boat.byownerhub.com | 63 | 0 | ✅ Clean |
| divorce.byownerhub.com | 56 | 0 | ✅ Clean |
| estate.byownerhub.com | 55 | 0 | ✅ Clean |
| funeral.byownerhub.com | 55 | 0 | ✅ Clean |
| insurance.byownerhub.com | 64 | 0 | ✅ Clean |
| land.byownerhub.com | 56 | 0 | ✅ Clean |

---

## Broken Links — Detail

### investor.byownerhub.com — 7 broken

**Content pages (pages not yet built):**
- `/fix-and-flip/` — 404
- `/brrrr/` — 404
- `/buy-and-hold/` — 404
- `/financing/` — 404

**Legal pages (missing):**
- `/disclaimer/` — 404
- `/privacy/` — 404
- `/terms/` — 404

**Root cause:** investor-hub nav links to strategy pages that don't have corresponding `src/app/` directories yet. Legal pages also not created.

---

### 55plus.byownerhub.com — 4 broken

- `/states/` — 404 (states directory page doesn't exist)
- `/disclaimer/` — 404
- `/privacy/` — 404
- `/terms/` — 404

**Root cause:** Legal pages not created. The `/states/` page is linked in nav but the directory index is missing (individual state pages may exist but the `/states/` hub page doesn't).

---

### condo.byownerhub.com — 3 broken

- `/disclaimer/` — 404
- `/privacy/` — 404
- `/terms/` — 404

**Root cause:** Legal pages not created.

---

## Corrected: 4 Sites Previously Flagged as "Access Issues" Are Actually Clean

The initial audit used incorrect standalone domain URLs. Correct URLs are all `*.byownerhub.com` subdomains:

| Wrong URL (used initially) | Correct URL | Status |
|---------------------------|-------------|--------|
| rent.byownerhub.com | **frbo.byownerhub.com** | ✅ Clean (55 links, 0 broken) |
| flatfeemlshub.com | **flatfee.byownerhub.com** | ✅ Clean (19 links, 0 broken) |
| closinghub.com | **closing.byownerhub.com** | ✅ Clean (62 links, 0 broken) |
| firsttimebuyerhub.com | **firsttimebuyer.byownerhub.com** | ✅ Clean (12 links, 0 broken) |

Note: `closinghub.com` (no subdomain) is actually an unrelated Minnesota title company — confirmed in prior audit 2026-06-23. Any internal network links pointing to `closinghub.com` or `www.closinghub.com` are going to a competitor's site.

---

## Pattern Analysis

**Legal pages (disclaimer/privacy/terms)** are missing from investor, 55plus, and condo — but present on landlord, commercial, biz, boat, divorce, estate, funeral, insurance, and land. The repos that have them likely share a template that includes them. The three missing repos need these three pages added.

**Content stubs** — investor-hub links to `/fix-and-flip/`, `/brrrr/`, `/buy-and-hold/`, `/financing/` which are planned content pages not yet written.

**55plus `/states/`** — the nav links to a states hub page that needs a directory index (`src/app/states/page.tsx`).

---

## Fix Priority

1. **Legal pages** — Add `/disclaimer/`, `/privacy/`, `/terms/` to: investor-hub, 55plus-hub, condo-hub (copy from any working hub repo)
2. **investor content pages** — Build or stub: `/fix-and-flip/`, `/brrrr/`, `/buy-and-hold/`, `/financing/`
3. **55plus `/states/`** — Add `src/app/states/page.tsx` as a state directory hub
4. **rent.byownerhub.com** — Debug CF Pages build for frbo-hub
5. **closinghub.com** — Debug why homepage renders blank
6. **flatfeemlshub.com** — Complete DNS/domain verification in CF Pages
