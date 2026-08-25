---
type: status
project: FSBO-Hub
last-verified: 2026-05-22
---

# fsbo-hub — Known Bugs & Issues
_Last updated: 2026-05-22_

---

## 🔴 Pre-Deploy Blockers

### OG Image — Invalid URL on Windows
**File:** `src/app/[metro]/opengraph-image.tsx`
**Issue:** `@vercel/og` fails with `TypeError: Invalid URL` when building locally on Windows due to path format incompatibility. Build exits with code 1.
**Impact:** Dynamic OG images don't generate locally. On Netlify (Linux), this resolves automatically.
**Status:** Pre-existing. Does not affect Netlify deploy. Low priority until local build verification is needed.

---

## 🟡 Content / Copy Issues (pre-launch cleanup)

### Lead Paint Form — Possible Tenant/Landlord Copy in VF/DF Sections
**Metros flagged:** Minneapolis, Albuquerque, Boise, Bakersfield, Charlotte (and possibly others)
**Issue:** Lead paint disclosure sections may use "tenant"/"landlord" language instead of "seller"/"buyer" in VF or DF form sections — inconsistent across metros (some right in DF but wrong in VF, vice versa).
**Status:** 🔲 Needs audit — user reported 2026-05-25, then indicated current state may be correct. Verify before deploy.

### sameAs Schema Empty
**File:** `src/app/layout.tsx` (Organization JSON-LD)
**Issue:** `sameAs: []` — empty array. Should contain social profile URLs once accounts exist.
**Status:** 🔲 Pending — needs social accounts first.

---

## 🟡 Infrastructure

### Placeholder Affiliate URLs
**Issue:** Several affiliate entries in `src/lib/data.ts` still have `#` or placeholder URLs. Intentional — pending affiliate program approvals.
**Status:** 🔲 Update as programs are approved.

---

## 🟢 Resolved

| Bug | Fix | Commit |
|---|---|---|
| AI Advisor References — 20+ stale copy instances | All references already removed in prior sessions (verified 2026-05-22) | — |
| FAQ stale copy — "try the AI Advisor above" | Already fixed (references email contact, not AI Advisor) | — |
| ListingGenerator import — possibly unused | Confirmed IN USE (listing description tool, not chat) — kept | — |
| ChatMessage type — possibly dead | Already removed from types/index.ts | — |
| Disclosures.tsx — dead component | Confirmed still in use: imported in [metro]/page.tsx + [suburb]/page.tsx — NOT dead | — |
| IndexNow Plugin — wrong HOST | Already `byownerhub.com` (non-www) — no fix needed | — |
| Bug 10 — "Download Disclosures" CTA | Renamed to "Download {state} Forms" in Hero.tsx | `2f63477` |
| Bug 11 — Scroll to top on tab return | Removed scrollTop assignments, added `history.scrollRestoration = 'manual'` | `2f63477` |
| Lead paint wrong URL (lesr → selr) | Fixed LEAD_PAINT_URL + 10 hardcoded entries in data.ts | `b7ce5bb` |
| VF+DF duplicate render | Disclosures component removed from all pages | `2026-05-15` |
| IL backup links pointing to wrong forms | Removed url_alt from il-multi-board-contract and il-heating-cost | `eb5a913` |
