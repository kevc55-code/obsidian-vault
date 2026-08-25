---
type: audit
audit-kind: link
project: FSBO-Hub
status: archived
archived: true
date: 2026-06-23
last-verified: 2026-06-23
---

# ByOwnerHub Network Link Audit
**Date:** 2026-06-23  
**Auditor:** Claude (Cowork)  
**Scope:** 33 sites across the ByOwnerHub network (original 24 + 9 added mid-audit)

---

## Legend
| Symbol | Meaning |
|--------|---------|
| ✅ Valid | Site/link loads correctly |
| ❌ Broken | 404, 403, chrome connection error, or "site not found" |
| ⚠️ Mismatch | Link resolves but content doesn't match anchor text |
| 🔄 Redirects | URL redirects to a different path (link still works) |
| 🚨 Threat | NordVPN Threat Protection flagged as malicious/parked |
| 🏷️ Wrong Site | Domain resolves but belongs to an unrelated third party |

---

## Part 1 — Site-Level Status (All Audited Homepages)

| Site | Status | Issue / Notes |
|------|--------|---------------|
| byownerhub.com | ✅ Valid | Homepage live. Contains **many broken outbound links** to its own hub network — see Part 2. |
| flatfee.byownerhub.com | ❌ Broken | Chrome connection error — site does not load at all. |
| firsttimebuyer.byownerhub.com | ✅ Valid | All sub-pages checked; external links (LendingTree, Credible, Nolo, LegalZoom, USLegalForms) all valid. |
| ftb.byownerhub.com | ❌ Broken | "Site not found" — subdomain does not exist. |
| car.byownerhub.com | ✅ Valid | Homepage and state sub-pages live. Government form PDFs verified for CA, FL, NY. See Part 3 for details. |
| frbo.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |
| condo.byownerhub.com | ✅ Valid | Only external link is LendingTree — valid. |
| commercial.byownerhub.com | ✅ Valid | Homepage live. Links to several broken internal subdomains — see Part 2. |
| estate.byownerhub.com | ✅ Valid | External links (EstateSales.net, MaxSold, EBTH, 1-800-GOT-JUNK) all valid. State sub-pages load but have no external gov links. |
| land.byownerhub.com | ❌ Broken | 403 Forbidden. |
| boat.byownerhub.com | ❌ Broken | 403 Forbidden. |
| rv.byownerhub.com | ✅ Valid | Links to boat.byownerhub.com (403) and moto.byownerhub.com (broken) — see Part 2. |
| mobile.byownerhub.com | ✅ Valid | External links (MHVillage, LendingTree) valid. |
| vacation.byownerhub.com | ✅ Valid | Only external link is LendingTree — valid. |
| funeral.byownerhub.com | ❌ Broken | 403 Forbidden. |
| divorce.byownerhub.com | ❌ Broken | 403 Forbidden. |
| probate.byownerhub.com | ❌ Broken | 403 Forbidden. |
| trust.byownerhub.com | ✅ Valid | Homepage and state sub-pages live. External link (Trust & Will) valid. No gov form links. |
| llc.byownerhub.com | 🚨 Threat | NordVPN Threat Protection blocked — likely parked/hijacked domain. |
| lien.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |
| auction.byownerhub.com | 🚨 Threat | NordVPN Threat Protection blocked — likely parked/hijacked domain. |
| foreclosure.byownerhub.com | ✅ Valid | External link (auction.com) valid. |
| eviction.byownerhub.com | ✅ Valid | Links to two broken internal subdomains — see Part 2. |
| inspection.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |
| 55plus.byownerhub.com | ✅ Valid | Only external link is LendingTree — valid. |
| biz.byownerhub.com | ✅ Valid | Homepage live. All 50 state sub-pages return 403. Links to 3 broken subdomains — see Part 2. |
| buyer.byownerhub.com | ✅ Valid | Links to two broken internal subdomains — see Part 2. |
| closinghub.com | 🏷️ Wrong Site | This is an **unrelated Minnesota title company** — not a ByOwnerHub property. Any link from the network pointing here goes to a competitor. |
| investor.byownerhub.com | ✅ Valid | Only external link is LendingTree — valid. |
| landlordhub.com | 🏷️ Wrong Site | **GoDaddy parked domain listed for sale at $5,000.** Not a ByOwnerHub property. |
| moto.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |
| relocation.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |
| trademark.byownerhub.com | ❌ Broken | Chrome connection error — site does not load. |

---

## Part 2 — Broken Outbound Links on Live Sites

These are links found on **live** ByOwnerHub pages that point to broken destinations.

| Site | Page | Link Text | URL | Status | Issue |
|------|------|-----------|-----|--------|-------|
| byownerhub.com | Homepage | Flat Fee MLS | https://flatfeemlshub.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Timeshare Exit | https://timeshare.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | New Build Hub | https://newbuild.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | FRBO Hub | https://frbo.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Landlord Hub | https://landlordhub.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Closing Hub | https://closinghub.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Inspection Hub | https://inspectionhub.byownerhub.com/ | 🚨 Threat | NordVPN blocks as threat |
| byownerhub.com | Homepage | Solar Hub | https://solar.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Contractor Hub | https://contractor.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Mortgage Hub | https://mortgage.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Rent / FRBO | https://rent.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | STR Hub | https://str.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Vacant Land | https://land.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Foreclosure Hub | https://foreclosure.byownerhub.com/ | ✅ Valid | — |
| byownerhub.com | Homepage | Probate Hub | https://probate.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Eviction Hub | https://eviction.byownerhub.com/ | ✅ Valid | — |
| byownerhub.com | Homepage | Divorce Hub | https://divorce.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Funeral Hub | https://funeral.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| byownerhub.com | Homepage | Trust Hub | https://trust.byownerhub.com/ | ✅ Valid | — |
| byownerhub.com | Homepage | LLC Hub | https://llc.byownerhub.com/ | 🚨 Threat | NordVPN blocks as threat |
| byownerhub.com | Homepage | Lien Hub | https://lien.byownerhub.com/ | ❌ Broken | Chrome connection error |
| byownerhub.com | Homepage | Auction Hub | https://auction.byownerhub.com/ | 🚨 Threat | NordVPN blocks as threat |
| buyer.byownerhub.com | Homepage | Flat Fee MLS Hub | https://flatfee.byownerhub.com/ | ❌ Broken | Chrome connection error |
| buyer.byownerhub.com | Homepage | Closing Hub | https://closing.byownerhub.com/ | ❌ Broken | Chrome connection error |
| commercial.byownerhub.com | Homepage | Closing Hub | https://closing.byownerhub.com/ | ❌ Broken | Chrome connection error |
| commercial.byownerhub.com | Homepage | Land Hub | https://land.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| commercial.byownerhub.com | Homepage | Lien Hub | https://lien.byownerhub.com/ | ❌ Broken | Chrome connection error |
| eviction.byownerhub.com | Homepage | Lien Hub | https://lien.byownerhub.com/ | ❌ Broken | Chrome connection error |
| eviction.byownerhub.com | Homepage | FRBO Hub | https://rent.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| rv.byownerhub.com | Homepage | Boat Hub | https://boat.byownerhub.com/ | ❌ Broken | 403 Forbidden |
| rv.byownerhub.com | Homepage | Moto Hub | https://moto.byownerhub.com/ | ❌ Broken | Chrome connection error |
| biz.byownerhub.com | Homepage | LLC Hub | https://llc.byownerhub.com/ | 🚨 Threat | NordVPN blocks as threat |
| biz.byownerhub.com | Homepage | Lien Hub | https://lien.byownerhub.com/ | ❌ Broken | Chrome connection error |
| biz.byownerhub.com | Homepage | Trademark Hub | https://trademark.byownerhub.com/ | ❌ Broken | Chrome connection error |
| biz.byownerhub.com | All state pages | All 50 state sub-pages | https://biz.byownerhub.com/states/* | ❌ Broken | All return 403 Forbidden |
| landlord.byownerhub.com | Homepage | All 50 state links | https://landlord.byownerhub.com/{state} | ❌ Broken | All state sub-pages (e.g., /california, /texas) return chrome connection error despite homepage loading |
| insurance.byownerhub.com | Homepage | By State | https://insurance.byownerhub.com/states/ | ❌ Broken | 403 Forbidden |

---

## Part 3 — Government Form Link Verification (car.byownerhub.com state pages)

| Site | Page | Link Text | URL | Status | Issue / Correct URL |
|------|------|-----------|-----|--------|---------------------|
| car.byownerhub.com | /states/california | Official state form | https://www.dmv.ca.gov/portal/uploads/2020/06/reg135.pdf | ✅ Valid | CA REG 135 Bill of Sale — confirmed live. |
| car.byownerhub.com | /states/florida | Official state form | https://www.flhsmv.gov/pdf/forms/82040.pdf | ✅ Valid | FL HSMV 82040 — confirmed live. |
| car.byownerhub.com | /states/new-york | Official state form | https://dmv.ny.gov/forms/mv912.pdf | ✅ Valid | NY MV-912 — confirmed live. |
| car.byownerhub.com | /states/illinois | Official state form | https://www.ilsos.gov/publications/pdf_publications/vsd703.pdf | 🔄 Redirects | Redirects to /content/dam/publications/pdf_publications/vsd703.pdf — still resolves, but URL should be updated to the canonical path. |
| car.byownerhub.com | /states/texas | Texas DMV — Vehicle Title Transfer | https://www.txdmv.gov/ | ⚠️ Mismatch | Anchor text implies a title transfer–specific page, but links to the TxDMV homepage. Page content references Form 130-U but no direct link to it. Correct form URL: https://www.txdmv.gov/sites/default/files/form_files/130-U.pdf |

---

## Part 4 — Additional Internal Subdomain Checks

These subdomains were discovered as outbound links from audited pages and checked opportunistically.

| Subdomain | Status | Notes |
|-----------|--------|-------|
| landlord.byownerhub.com | ✅ Homepage only | All 50 state sub-pages return chrome-error |
| closing.byownerhub.com | ❌ Broken | Chrome connection error — distinct from closinghub.com |
| flatfeemlshub.byownerhub.com | ❌ Broken | 403 Forbidden — distinct from flatfee.byownerhub.com |
| inspectionhub.byownerhub.com | 🚨 Threat | NordVPN Threat Protection blocked — distinct from inspection.byownerhub.com |
| closinghub.byownerhub.com | ❌ Broken | 403 Forbidden |
| landlordhub.byownerhub.com | ❌ Broken | 403 Forbidden — distinct from landlord.byownerhub.com |
| timeshare.byownerhub.com | ❌ Broken | Chrome connection error |
| newbuild.byownerhub.com | ❌ Broken | Chrome connection error |
| rent.byownerhub.com | ❌ Broken | 403 Forbidden |
| str.byownerhub.com | ❌ Broken | Chrome connection error |
| mortgage.byownerhub.com | ❌ Broken | Chrome connection error |
| solar.byownerhub.com | ❌ Broken | Chrome connection error |
| contractor.byownerhub.com | ❌ Broken | Chrome connection error |
| insurance.byownerhub.com | ✅ Homepage only | /states/ sub-pages return 403 |

---

## Summary — High-Priority Issues

| Priority | Finding | Affected Sites |
|----------|---------|---------------|
| 🔴 Critical | **3 subdomains blocked by NordVPN as threats** (likely parked/hijacked): llc, auction, inspectionhub | byownerhub.com, biz.byownerhub.com |
| 🔴 Critical | **landlordhub.com is a GoDaddy-parked domain for sale** — any internal link pointing there goes to a domain broker | Discovered during audit |
| 🔴 Critical | **closinghub.com is an unrelated Minnesota title company** — brand/URL confusion | Discovered during audit |
| 🔴 Critical | **All 50 state sub-pages broken on biz.byownerhub.com** (403) and **landlord.byownerhub.com** (connection error) | biz, landlord hubs |
| 🟠 High | **12 subdomains completely unreachable** (chrome-error or 403): flatfee, ftb, frbo, land, boat, funeral, divorce, probate, lien, inspection, moto, relocation, trademark | byownerhub.com homepage, rv, eviction, commercial, buyer |
| 🟠 High | **byownerhub.com homepage has 13+ broken outbound links** to its own hub network | byownerhub.com |
| 🟡 Medium | **Illinois car form URL redirects** — old path still works but should be updated to canonical URL | car.byownerhub.com/states/illinois |
| 🟡 Medium | **Texas car page mentions Form 130-U but only links to TxDMV homepage** — no direct form link | car.byownerhub.com/states/texas |
| 🟢 Low | insurance.byownerhub.com /states/ sub-pages return 403 | insurance.byownerhub.com |
