---
type: planning
project: FSBO-Hub
last-verified: 2026-06-21
---

# ByOwnerHub Network Strategy v3

## Parent Hub
byownerhub.com — routes all traffic, SEO authority builder

---

## Subdomain Network

| Subdomain | Focus | Monetization | Status |
|---|---|---|---|
| fsbo.byownerhub.com | FSBO homes — main content property | Form kits, attorney referrals, title cos | ✅ Built (currently at byownerhub.com root — needs subdomain migration) |
| rent.byownerhub.com | Rent by owner / FRBO | Lease templates, tenant screening affiliates | ✅ Built (frbo-hub repo) — needs Netlify deploy |
| car.byownerhub.com | Private-party auto sales | Carfax/AutoCheck affiliate, bill-of-sale kits | ✅ Built, SEO-optimized, DNS propagating |
| land.byownerhub.com | Vacant land FSBO | Survey referrals, title companies | ✅ Built (land-hub, 61 pages) — not pushed |
| mobile.byownerhub.com | Mobile / manufactured homes | Specialty lenders, park directories | ✅ Built (mobile-hub, 64 pages) — not pushed |
| commercial.byownerhub.com | Small commercial FSBO | LOI templates, broker co-op guides | ✅ Built (commercial-hub, 71 pages) — not pushed |
| boat.byownerhub.com | Boats / RVs / powersports | Hull insurance, marine survey referrals | ✅ Built (boat-hub, 67 pages) — not pushed |

---

## Companion Domains

| Domain | Audience | Status |
|---|---|---|
| LandlordHub.com | DIY landlords | ✅ Built (landlord-hub repo) |
| FRBOHub.com | Renters seeking private landlords | ✅ Owned — pairs with rent.byownerhub.com |
| FlatFeeMLSHub.com | Sellers wanting MLS without full commission | ✅ Built (flatfee-hub, 71 pages) — not pushed |
| FirstTimeBuyerHub.com | Unrepresented first-time buyers | ⚠️ Incomplete — build kept hitting rate limits |
| ProbateHub.com | Heirs selling inherited property | ✅ Built (probate-hub, 59 pages) — not pushed |
| ClosingHub.com | Buyers/sellers navigating closing | ✅ Built (closing-hub, 66 pages) — not pushed |

---

## Priority Build Order (from strategy doc)
1. fsbo.byownerhub.com — migrate existing content (low effort, highest priority)
2. rent.byownerhub.com — highest search vol after FSBO, content lifts from FSBO
3. FlatFeeMLSHub.com — massive affiliate opportunity
4. land.byownerhub.com — underserved niche, low competition
5. FirstTimeBuyerHub.com — captures buyer side of every FSBO transaction
6. car.byownerhub.com — large market, Carfax affiliate (IN PROGRESS)
7. ClosingHub.com — high-value title/escrow affiliate clicks

---

## Top Priority Affiliate Programs (from v3 doc)

| Program | Payout | Cookie | Best For |
|---|---|---|---|
| LendingTree | $1–$70/lead | 14 days | fsbo + FirstTimeBuyerHub |
| ~~Houzeo~~ | ~~$50–$200/sale~~ | — | ⛔ **NO AFFILIATE PROGRAM** — do not add anywhere |
| RentSpree | Per referral | 30 days | rent + LandlordHub |
| Buildium | 25% recurring + $10/lead | 60 days | LandlordHub — **BEST RECURRING** |
| Carfax | Per report | 30 days | car site |
| NOLO | 25–35%/sale | 120 days | fsbo legal forms — **LONGEST COOKIE** |
| Credible | $240/funded loan | 30 days | FirstTimeBuyerHub — **HIGHEST SINGLE PAYOUT** |

---

## Immediate Go-Live Blocklist

- [ ] fsbo.byownerhub.com — set up subdomain in Netlify, add CNAME in Porkbun
- [ ] rent.byownerhub.com — deploy frbo-hub to Netlify, add CNAME
- [ ] car.byownerhub.com — DNS propagating (CNAME added to Porkbun), SSL pending
- [ ] byownerhub.com root — build parent hub router page
- [ ] Apply to affiliate networks: Houzeo, LendingTree, RentSpree, Buildium, Carfax, NOLO
- [ ] Set NEXT_PUBLIC_SITE_URL env vars in Netlify for each site
- [ ] Submit sitemaps to Google Search Console after each deploy
