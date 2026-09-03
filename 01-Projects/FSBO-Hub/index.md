---
type: project-index
project: FSBO-Hub
repo: kevc55-code/fsbo-hub
category: real-estate-network
status: active
deploy-ready: false
last-verified: 2026-09-03
open-items: 17
---

# FSBO Hub — Project Reference

> **Repo:** `github.com/kevc55-code/fsbo-hub`
> **Stack:** Next.js 14 (App Router) · TypeScript · Tailwind CSS · Netlify
> **Owner entity:** Byownerhub.com LLC (NM) — 1209 Mountain Road Pl NE, Ste N, Albuquerque, NM 87110
> **Current HEAD (main):** `e659fd1` — moved 2026-09-02 via `e659fd1` ("drop the metro hero CTAs and tighten the spacing"), which finally commits + pushes the `Hero.tsx` edit that had sat uncommitted since 2026-08-21. Prior moves: `8212ae6` (seller-progress workspace feature) and `5bd8207` (metro page redesign: "read as a tool, not an article"), both 2026-08-19. In sync with origin; working tree clean. See [[SESSION-2026-09-02]] and [[unpushed-changes]].
> **Branch `freemium-wip`:** $99 Stripe toolkit, still 11 commits ahead of origin (unpushed) as of 2026-09-02 — unchanged since 08-05. Deploy-readiness not re-verified since the 2026-07-12 check, now 5+ weeks stale (launch steps in [[open-items]] item 8). Note: this branch predates and is separate from production's actual freemium build, which lives in `fsbo-freemium-sandbox` and has already shipped Stripe checkout + refunds + entitlement (see [[SESSION-2026-08-21]]).

---

## Session Protocol

1. **Read this vault at the start of every fsbo-hub session** — index.md, unpushed-changes.md, metro-tracker.md, affiliate-stack.md.
2. **Update the vault after every session that changes the repo** — log new commits in unpushed-changes.md, update index.md Recent Work, reflect any affiliate or metro changes.

---

## Standing Rules

- **Houzeo has no affiliate program** — never add as a CTA, placeholder, or link anywhere in the network (fsbo-hub or any companion site). See [[affiliate-stack]] → "Not Available" section. Monitor if they ever launch a program.

---

## Network Overview

This project is one node in the **ByOwnerHub** owner-direct transaction network. The full network spans 7 subdomains under `byownerhub.com` plus 6 companion domains targeting related audiences.

**Subdomain network:** `fsbo` · `rent` · `car` · `land` · `mobile` · `commercial` · `boat`

**Companion domains:** LandlordHub.com · FRBOHub.com · FlatFeeMLSHub.com · FirstTimeBuyerHub.com · ProbateHub.com · ClosingHub.com

→ See [[network-status]] for current deploy status of all 13 network properties.
→ See [[affiliate-stack]] for the confirmed fsbo-hub affiliate program list (v3).
→ See [[open-items]] for pending decisions, deploy tasks, and code items.
→ See [[network-strategy]] for full subdomain table, priority build order, and go-live checklist.

---

## Architecture

### Routes (`src/app/`)

| Route                          | Purpose                                                                                                                                                |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `page.tsx`                     | Homepage — server component, full SEO metadata, Organization + WebSite schema, HomeZipForm client split                                                |
| `[metro]/page.tsx`             | Metro landing page — hero, checklist, forms library, comps estimator, suburbs grid, QuickStart 3-step section                                          |
| `[metro]/[suburb]/page.tsx`    | Suburb page — localized FSBO info, tools, SchemaMarkup with 3-level breadcrumb                                                                         |
| `[metro]/blog/page.tsx`        | Blog index for each metro                                                                                                                              |
| `[metro]/blog/[slug]/page.tsx` | Individual blog post — markdown renderer, related posts, affiliate sidebar                                                                             |
| `[metro]/opengraph-image.tsx`  | Dynamic OG image per metro                                                                                                                             |
| `houston-es/page.tsx`          | Spanish landing page — Houston                                                                                                                         |
| `san-antonio-es/page.tsx`      | Spanish landing page — San Antonio                                                                                                                     |
| `miami-es/page.tsx`            | Spanish landing page — Miami                                                                                                                           |
| `los-angeles-es/page.tsx`      | Spanish landing page — Los Angeles                                                                                                                     |
| `disclosure/`                  | Affiliate disclosure page                                                                                                                              |
| `tools/listing-description/`   | AI listing description generator tool                                                                                                                  |
| `tools/price-my-home/`         | Price my home estimator tool                                                                                                                           |
| `privacy/`, `terms/`           | Legal pages                                                                                                                                            |
| `unsubscribed/`                | Unsubscribe confirmation                                                                                                                               |
| `{state}-fsbo-guide/`          | 30 state-specific FSBO guides (AL, AZ, CA, CO, DC, FL, GA, IL, IN, KY, LA, MD, MA, MI, MN, MO, NE, NV, NM, NY, NC, OH, OK, OR, PA, TN, TX, UT, VA, WA) |
| `sitemap.ts`                   | Dynamic sitemap — all metros, suburbs, state guides, ES pages, blog                                                                                    |
| `robots.ts`                    | Dynamic robots.txt pointing to sitemap                                                                                                                 |

### API Routes (`src/app/api/`)

| Endpoint | Purpose |
|---|---|
| `/api/census` | Server-side proxy for Census API |
| `/api/chat` | AI chat endpoint |
| `/api/leads` | Lead capture |
| `/api/listing-description` | AI listing description generator |
| `/api/price-estimate` | AI price estimate tool |
| `/api/subscribe` | Email subscription |
| `/api/unsubscribe` | Email unsubscribe |
| `/api/zip-interest` | ZIP code interest tracking |

### Components (`src/components/`)

| Component               | Purpose                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `AIChat`                | AI-powered chat assistant                                                                                                                   |
| `AboutUs`               | About page content                                                                                                                          |
| `BlogPreview`           | Blog post preview cards                                                                                                                     |
| `CarSiteCrossPromo`     | **NEW 2026-05-15** — Small card linking to car.byownerhub.com. Rendered in Footer brand column. |
| `Checklist`             | FSBO selling checklist                                                                                                                      |
| `ChecklistAndForms`     | Combined checklist + forms view                                                                                                             |
| `CompsEstimator`        | Comparable sales estimator                                                                                                                  |
| `Disclosures`           | **REMOVED FROM PAGES** — component file still exists but no longer rendered on metro or suburb pages. Replaced by `FormsLibrary` (VF section). |
| `FAQSection`            | FAQ accordion                                                                                                                               |
| `Footer`                | Site footer (responsive grid) — now includes `CarSiteCrossPromo` |
| `FormsLibrary`          | Transaction forms library — `id="forms"` anchor, "View Form ↗" links, phase filter, email gate. Single forms section on all metro/suburb pages. |
| `GateWrapper`           | Email gate wrapper for CMA/tools                                                                                                            |
| `Hero`                  | Metro hero section                                                                                                                          |
| `HomeZipForm`           | Client component for zip-code entry on homepage (split from page.tsx for SSR)                                                               |
| `MLSComparison`         | MLS flat-fee comparison table                                                                                                               |
| `Nav`                   | Navigation bar (blog link + mobile menu)                                                                                                    |
| `NetProceedsCalculator` | Net proceeds calculator                                                                                                                     |
| `OfferComparison`       | Offer comparison tool                                                                                                                       |
| `SavingsCalculator`     | Commission savings calculator                                                                                                               |
| `SchemaMarkup`          | JSON-LD — HowTo + FAQPage + WebPage/BreadcrumbList. Accepts `pageUrl` + `parentMetro` props for correct suburb URLs and 3-level breadcrumbs |
| `ScrollToTop`           | Scroll-to-top button                                                                                                                        |
| `ServicesGrid`          | Affiliate services grid — grouped by FSBO phase                                                                                             |
| `SubscribeForm`         | Email subscribe form                                                                                                                        |
| `UsefulTip`             | Tip callout box                                                                                                                             |

### Data Layer (`src/lib/`)

| File | Contents |
|---|---|
| `data.ts` | 101 metros, 24 affiliates (12 active categories), METRO_FORMS mapping, STATES_WITH_GUIDE |
| `suburbs.ts` | 782 suburb entries across 44+ metros |
| `forms.ts` | State disclosure/contract form URLs — all 25 `url: null` entries are legitimately null (HOA-issued, attorney-drafted, or Canadian association member-only) |
| `blog.ts` | Blog post data and helpers (getBlogPost, getBlogPostsForMetro) |

### Types (`src/types/index.ts`)

Key types: `Metro` (includes `country: 'US' | 'CA'`), `Disclosure`, `AffiliateProgram`

`AffiliateCategory` values (12 active): `flat_fee_mls`, `moving`, `legal`, `storage`, `mortgage`, `inspection`, `insurance`, `title`, `photography`, `lockbox`, `attorney`, `cash-offer`

Note: `agent_referral` and `vendor` exist in the type definition but have no affiliates currently assigned.

### SEO / Indexing Infrastructure

| File | Purpose |
|---|---|
| `src/app/sitemap.ts` | Dynamic sitemap — generated from STATES_WITH_GUIDE + SUBURBS + METROS. Replaces next-sitemap |
| `src/app/robots.ts` | Dynamic robots.txt — always points to `byownerhub.com/sitemap.xml` (non-www) |
| `next-sitemap.config.js` | **Disabled** — postbuild script replaced with no-op. Was conflicting (www vs non-www) and overwriting robots.ts |
| `netlify/plugins/indexnow/index.js` | Netlify build plugin — pings Bing/DDG/Yandex via IndexNow after each deploy |
| `public/byownerhub-indexnow-2026.txt` | IndexNow key verification file |

---

## Sister Site — CarByOwner

> **Repo:** `C:\Users\kevc_\Documents\GitHub\car-by-owner` (local only — push to GitHub needed)
> **Stack:** Next.js 16 (App Router) · TypeScript · Tailwind CSS v4 · Netlify
> **Build:** Clean — 57 static pages (50 state guides + homepage + states index + bill-of-sale + how-it-works)
> **Status:** Phase 1 complete. Needs GitHub remote + Netlify deploy + domain.

### Overview

CarByOwner is a standalone site targeting the private car sale niche. Overlap with fsbo-hub audience (people doing owner-direct transactions). Phase 1 ships the core SEO moat: all 50 state guides.

### Architecture

| Route | Purpose |
|---|---|
| `/` | Homepage — hero, stats strip, featured state grid, tools section |
| `/states` | All 50 states index (compact card grid, alphabetical) |
| `/states/[state]` | Individual state guide — summary table, 7-step walkthrough, required forms, DMV links, cross-promo |
| `/bill-of-sale` | Interactive bill of sale generator — form → printable preview → print/PDF |
| `/how-it-works` | 4-phase seller guide (prepare → price → show → close) with printable checklist |

### Key components

| Component | Purpose |
|---|---|
| `Navbar` | Sticky nav with car icon logo, nav links, CTA |
| `Footer` | Brand, guides, tools, legal — includes ByOwnerHub cross-promo card |
| `StateCard` | Default (full card) + compact (list row) variants |
| `StatsSummaryTable` | Quick-reference fee/tax/notary/timeline table for state sidebar |
| `BillOfSaleForm` | Client component — form state → bill of sale preview → `window.print()` |
| `RealEstateCrossPromo` | Small card linking to byownerhub.com (appears in state guide sidebar) |

### Data layer (`src/lib/states.ts`)

`CAR_STATES` array — all 50 states with:
- `slug`, `name`, `abbr`, `emoji`
- `title_fee`, `sales_tax`
- `notary_required` (true: Louisiana, Texas)
- `bill_of_sale_required`, `odometer_required`
- `dmv_url` — official state DMV/title transfer page
- `bill_of_sale_url` — official state form PDF where available (FL, CA, IL, NY)
- `transfer_timeline` — days buyer has to register
- `notes` — state-specific quirks

Helpers: `getStateBySlug(slug)`, `getPopularStates()` (TX, CA, FL, NY, IL).

### Phase 2 backlog

- GitHub remote + Netlify deploy
- Domain (car.byownerhub.com)
- Google Search Console submission
- Blog content (SEO articles targeting "how to sell car privately in [state]")
- Price my car tool (integrate KBB or market data API)
- Listing writer tool (AI-assisted, same pattern as fsbo-hub listing-description)
- State pages: add emissions testing details per state
- Schema markup (HowTo + FAQPage on state guide pages)
- Email capture / lead generation

### Cross-promo integration

**fsbo-hub → CarByOwner:** `CarSiteCrossPromo.tsx` added to `Footer.tsx` brand column. Small card: car icon + "Also selling your car?" + link to car.byownerhub.com. Committed and pushed to `origin/main` as `4176814`.

**CarByOwner → fsbo-hub:** `RealEstateCrossPromo.tsx` appears in the sidebar of every state guide page (`/states/[state]`). Also a small card in the Footer. Links to byownerhub.com.

---

## Recent Work

### 2026-05-15 — Launch CarByOwner (Phase 1) + cross-promo integration

- **CarByOwner scaffolded** at `C:\Users\kevc_\Documents\GitHub\car-by-owner` — Next.js 16, Tailwind v4, 57 static pages, clean production build.
- **All 50 state guides built** — each with accurate title fees, sales tax rates, notary requirements, DMV URLs, bill of sale links, transfer timelines, and state-specific notes.
- **Interactive bill of sale generator** — client-side form with live preview and `window.print()` for PDF export. No server required.
- **Cross-promo wired both ways** — `CarSiteCrossPromo` in fsbo-hub Footer (committed + pushed `4176814`); `RealEstateCrossPromo` in car-by-owner state guide sidebars and Footer.
- **netlify.toml** added with `@netlify/plugin-nextjs` config.
- **Initial commit** `ecd433c` in car-by-owner repo. Needs GitHub remote.

### 2026-05-15 — Remove DF (Disclosures) section; remap all Forms anchors to `#forms`

**Branch:** `claude/sharp-noyce-46e225` — not yet pushed/merged.

- **`Disclosures` component removed from pages** — `[metro]/page.tsx` and `[metro]/[suburb]/page.tsx` no longer import or render `<Disclosures>`. Component file (`Disclosures.tsx`) still exists on disk but is now dead. `getFormsForMetro` import and `metroForms` variable also removed from both pages.
- **`FormsLibrary` gets `id="forms"`** — Added `id="forms"` to the `<section>` in `FormsLibrary.tsx` so the VF section is the single forms anchor target.
- **All `#disclosures` anchor refs updated to `#forms`** — Four locations updated:
  - `[metro]/page.tsx` sticky nav
  - `[metro]/[suburb]/page.tsx` sticky nav
  - `[metro]/[suburb]/page.tsx` hero CTA button (`href="#disclosures"` → `href="#forms"`)
  - `[metro]/blog/[slug]/page.tsx` "Download {state_code} Disclosure Forms" quick link
- **Suburb FAQ answer updated** — "Disclosures section below" → "Transaction Forms section below".
- **Open item #9 resolved** — The duplicate VF+DF render (forms.ts rendered in both FormsLibrary and Disclosures) is gone. Only FormsLibrary renders METRO_FORMS now.

---

### 2026-05-14 — Pierre QA remaining open items — watermarks, broken DF links, missing forms (`97e82be`)

- **TX (dallas/houston/austin) — TREC 40-10 → 40-11** — Third Party Financing Addendum superseded by form version 40-11. Updated form name and URL across all 3 TX metros.
- **TN VA/FHA addendum** — Replaced non-functional `tarnet.com` redirect with public rackcdn RF625 PDF (no watermark). Added `url_alt` pointing to same CDN copy.
- **TN HOA disclosure** — Set `url: null` (no standalone public PDF exists; embedded in TAR contract). "See source for form" now renders correctly in DF section instead of broken tarnet.com link.
- **FL sellers disclosure (miami/tampa/orlando)** — Replaced eforms.com watermarked 2017 PDF with official FAR SPDR-4 from My State MLS CDN (clean, current form).
- **MN well disclosure** — Replaced eforms.com copy with official Minnesota Dept of Health URL (`health.state.mn.us`). Updated both `url` and `url_alt`.
- **PA (philly + pittsburgh) ASR + mortgage contingency** — All 4 esign.com 404 entries replaced with working PAR ASR PDF from irp-cdn.multiscreensite.com. Mortgage contingency entries (Paragraph 8 of ASR) now link to same working ASR PDF.
- **AZ affidavit of value** — Confirmed azdor.gov URL valid; no change needed.
- **Montreal OACIQ declarations** — Already `url: null` (member-only, 403 Forbidden); no change needed.

---

### 2026-05-13 — Full multi-metro consistency pass + Bug 10/11 fixes (pushed to main)

- **NC Raleigh — HOA Addendum added** (`2f63477`) — Added `nc-ral-hoa-addendum` (NCAR Form 2A12-T) to match Charlotte. Both NC metros now have identical form sets.
- **AL cross-form additions** (`2f63477`) — Mobile gets `mobile-disclosure` (Seller's Property Disclosure, matching Birmingham). Birmingham gets `birmingham-buyer-advisory` (As-Is Addendum, matching Mobile). Both AL metros now have 4 forms each.
- **CA (4 metros), TX (3 metros), PA (2 metros)** — Audited and confirmed consistent, no changes needed.
- **Bug 10 resolved** (`2f63477`) — `Hero.tsx` CTA renamed from `Download {state} Disclosures` to `Download {state} Forms`. Suburb page already had the correct text from prior session. Bug 10 closed.
- **Bug 11 resolved** (`2f63477`) — `ScrollToTop.tsx` fixed: (1) added `history.scrollRestoration = 'manual'` on mount to prevent browser bfcache/history auto-scroll; (2) removed `document.documentElement.scrollTop = 0` and `document.body.scrollTop = 0` which used CSS `scroll-behavior: smooth` and could start a ~300ms smooth-scroll animation that completed asynchronously after a tab switch, producing the spurious scroll-to-top. Bug 11 closed.

### 2026-05-13 — Metro forms standardization audit (pushed to main)

- **FL Orlando — 6 missing forms added** (`72e8061`) — Added Radon Gas Disclosure, Property Tax Disclosure Summary (FS 689.261), Flood Disclosure (FD-1/FD-2), HOA Disclosure to Prospective Purchaser (FS 720.401), HOA Estoppel Certificate (FS 720.30851), and Documentary Stamp Tax Declaration to Orlando. All copied from Miami/Tampa with `fl-orl-` prefixed IDs. Lead paint was already present.
- **CA Sacramento url/url_alt swapped** (`72e8061`) — `ca-sac-purchase-agreement` had url/url_alt reversed vs all other CA metros. Fixed: First Tuesday form is now `url`, C.A.R. Dec 2018 version is `url_alt`. Notes updated to match SF/SD pattern.
- **NC mineral rights consistency** (`72e8061`) — Raleigh mineral rights disclosure changed from `required: false` to `required: true` to match Charlotte (more conservative value applied to both).
- **NC Charlotte missing agency disclosure** (`72e8061`) — Added `nc-char-agency` (Working With Real Estate Agents Disclosure) to Charlotte, matching Raleigh's `nc-ral-agency` form.
- **AL attorney_required** (`72e8061`) — Mobile set from `false` to `true` (Alabama is an attorney-required state; Birmingham was already `true`).
- **AL duplicate form IDs resolved** (`72e8061`) — Birmingham forms renamed `al-*` → `birmingham-*`; Mobile forms renamed `al-*` → `mobile-*`.
- **AL purchase contract standardized** (`72e8061`) — Both Birmingham and Mobile now use AAR CDN link as primary `url`, eforms.com as `url_alt`. Mobile's incorrect "No attorney required" note replaced with attorney budget note.

### 2026-05-13 — VF/DF revert, nav rename, lead paint fix, form link audit (pushed to main)

- **Reverted a9c28b8** (`222a451`) — Restored two-section VF + DF layout. `<Disclosures>` component back in both `[metro]/page.tsx` and `[metro]/[suburb]/page.tsx`. "View backup copy ↗" alt link restored in `FormsLibrary` FormCard expanded state.
- **Nav "Disclosures" → "Forms"** (`bab8b64`) — Desktop link and mobile menu label in `Nav.tsx`. `href="#disclosures"` unchanged.
- **IL backup links fixed** (`eb5a913`) — Removed `url_alt` from `il-multi-board-contract` (was pointing to a different form — generic IL Residential Purchase Agreement) and `il-heating-cost` (was pointing to landlord version, not seller disclosure). Stale note text on heating cost entry also cleaned up.
- **Lead paint alt set to primary** (`eb5a913`) — `LEAD_PAINT_ALT = LEAD_PAINT_URL` (same URL as backup). Later superseded by the URL fix below.
- **Suburb hero CTA rename** (`eb5a913`) — `Download {state} Disclosures` → `Download {state} Forms` in `[metro]/[suburb]/page.tsx`. *(See Bug A — may not have fully resolved.)*
- **ScrollToTop RAF removed** (`eb5a913`) — Removed `requestAnimationFrame(reset)` from `ScrollToTop.tsx`. RAF is suspended in background tabs and fires on tab-switch-back, causing scroll-to-top. *(See Bug B — not fully resolved.)*
- **Lead paint URL corrected — CRITICAL** (`b7ce5bb`) — Replaced `lesr_eng.pdf` (EPA Lessor/Lessee = RENTAL form) with `selr_eng.pdf` (EPA Seller's Disclosure = SALES form) across all 61 entries: `LEAD_PAINT_URL` constant in `forms.ts` (drives 51 metro lead paint entries) + 10 hardcoded `download_url` values in `data.ts` (MA, IL, TX, FL, WA, GA, MN, CO, NC, TN). Confirmed from EPA disclosure page: `epa.gov/lead/real-estate-disclosures-about-potential-lead-hazards`.

### 2026-05-08 — Form URL audit + CLAUDE.md (pushed to main)

- **CLAUDE.md added** — Multi-agent orchestration config (Haiku → Opus → Sonnet 5-step flow).
- **Form URL audit** — 14 edits to `src/lib/forms.ts`: TX TREC 40-10 draft→finalized, Lead Paint constants updated, TN VA/FHA and HOA disclosure URLs, FL sellers disclosure + FAR/BAR contract DF URLs (miami+tampa), MN 4 forms fixed, Montreal OACIQ url_alt nulled, PA standard agreement swapped + mortgage contingency added, AZ affidavit value + AAR contract DF fixed.
- **3 Chrome-verified URL corrections** — AZ Form 82162 direct PDF, Lead Paint ALT → EPA selr_eng.pdf, TN VA/FHA → tarnet.com (no public PDF exists).
- **PA/AZ redundancy investigated** — FormsLibrary (`forms.ts`) and Disclosures (`data.ts`) both render all 6-7 state forms for AZ and PA. Tracked as item #9 above (already existed) + new items 10-31 (AI advisor cleanup). Recommended fix: delete AZ/PA entries from `data.ts` DISCLOSURES.

### 2026-05-06 — Medium/low audit items resolved (4 commits, pushed to main)

- **Rate limiting** — Replaced broken in-memory Map rate limiters in `price-estimate` and `listing-description` routes with a Netlify Edge Function (`netlify/edge-functions/api-rate-limit.ts`). Edge functions use Deno's long-lived module scope; state actually persists across invocations unlike serverless function cold starts.
- **Dead routes deleted** — Removed `src/app/api/chat/route.ts` (was just returning 410). Removed `src/app/api/chat/` directory.
- **Legal page dates** — Replaced hardcoded `"March 2026"` strings in `disclosure/`, `privacy/`, `terms/` with `const LAST_UPDATED = 'May 2026'` at the top of each file.
- **Dead files removed** — Deleted `next-sitemap.config.js` (disabled, wrong www. domain). Removed `pdf-parse` and `next-sitemap` from `package.json` (zero imports in src/).
- **`/tools/listing-description`** — Rebuilt from confusing navigation stub into a real landing page with 3-step explainer. Fixed broken internal link (`/price-my-home` → `/tools/price-my-home`). Added canonical URL to metadata.
- **TypeScript cleanup** — Replaced both `eslint-disable-next-line @typescript-eslint/no-explicit-any` suppressions in AI routes with explicit `PricingAnswers` and `ListingFormData` interfaces.

### 2026-05-06 — Codebase audit fixes (5 commits, pushed to main)

- **`public/logo.png` created** — 512×512 PNG, satisfies Organization JSON-LD schema `logo` field. Was 404ing on every crawl.
- **AboutUs.tsx** — Metro count corrected from `'6'` to `'101'`.
- **next.config.js** — Removed stale `generateBuildId: () => 'build-' + Date.now()` override that was force-busting CDN cache on every deploy.
- **blog.ts dead links fixed** — 18 internal links pointing to 9 non-existent `/STATE-fsbo-guide` pages replaced with valid `/STATE/blog/SLUG` URLs (alaska, arkansas, connecticut, delaware, hawaii, idaho, iowa, kansas, maine).
- **Hardcoded `/boston` links fixed** — `disclosure/page.tsx`, `privacy/page.tsx`, `terms/page.tsx` back-links now point to `/`. MA guide nav logo now points to `/` (Boston-specific nav item and CTA left intentionally).
- **price-my-home metadata** — New `src/app/tools/price-my-home/layout.tsx` exports SEO metadata (page is `'use client'` and cannot export metadata directly). Title, description, canonical, OG, Twitter card all now populated.
- **OG image** — Already resolved in previous session: `public/og-default.png` exists, wired into `layout.tsx` openGraph. *(Updated open item #5 below.)*

### 2026-05-06 — State guide content, hreflang, blog metadata, forms audit

- **Hreflang — Canadian metros** — Added `hreflang="en-CA"` + `x-default` to all Canadian metro `generateMetadata` in `[metro]/page.tsx`. `isCA = metro.country === 'CA'` flag drives `alternates.languages`.
- **Blog metadata** — Added `canonical`, `openGraph.url`, `openGraph.siteName`, and `twitter: summary_large_image` to both `[metro]/blog/page.tsx` (index) and `[metro]/blog/[slug]/page.tsx` (post).
- **23 thin state guide pages fleshed out** — Inserted a full "The [State] FSBO Process — Step by Step" H2 section into all 23 thin state guides (AL, AZ, CA, CO, DC, IN, KY, LA, MD, MI, MN, MO, NE, NV, NM, NC, OH, OK, OR, TN, UT, VA + California). 6 H3 subsections each: pricing, disclosures, MLS listing, photography, offers, closing — all state-specific.
- **Email updated everywhere** — `hello@byownerhub.com` / `noreply@byownerhub.com` → `byownerhubadmin@gmail.com` in `disclosure/page.tsx`, `privacy/page.tsx`, `terms/page.tsx`, `FormsLibrary.tsx`, `email.ts`.
- **Forms audit complete** — Audited all 25 `url: null` entries in `forms.ts`. All legitimately null. No changes needed.
- **Core Web Vitals** — 96/100 mobile, 99/100 desktop. FCP 2.0s mobile is render-blocking + unused Tailwind — not critical.

### 2026-05-06 — Full SEO optimization pass

- **Homepage** — Converted `page.tsx` from `'use client'` to server component. Extracted `HomeZipForm.tsx` as client component. Added full `metadata` export: canonical `byownerhub.com`, OG, Twitter card, `Organization` + `WebSite` + `SearchAction` JSON-LD schema.
- **layout.tsx** — Added `metadataBase`, title template (`%s | ByOwnerHub`), OG `siteName`, Twitter `summary_large_image` fallback for all pages.
- **101 metro `seo_title` fields** — Rewrote all to include FSBO keyword, removed "ByOwnerHub.com" (was double-branding with layout template), capped at ≤60 chars.
- **30 state guide pages** — Added `alternates: { canonical }` and `twitter: { card: 'summary_large_image' }` to all 30 via automated script.
- **`SchemaMarkup` component** — Added `pageUrl` and `parentMetro` optional props. Suburb pages now get correct canonical URL in schema and a 3-level breadcrumb (Home → Metro → Suburb).
- **`sitemap.ts`** — Replaced hardcoded state guide list with dynamic generation from `STATES_WITH_GUIDE`. Added 4 Spanish pages. Single source of truth.
- **`next-sitemap` disabled** — Was running postbuild and generating `public/robots.txt` with wrong `www.` URL, overriding dynamic `app/robots.ts`.

### 2026-04-28

- **`065a705`** — Add IndexNow ping + next-sitemap for Bing/DDG/Yandex indexing.
- **`ae3b558`** / **`8fdffc0`** — Flesh out 7 state FSBO guides (TX, FL, WA, IL, GA, NY, PA).
- **`8300d08`** — Add 8 new affiliates: photography (Virtuance, BoxBrownie), lockbox (Master Lock, Supra eKEY), attorney (LegalZoom, Avvo), cash-offer (Opendoor, Offerpad).
- **`5e922cd`** / **`228134d`** — Add Spanish landing pages for San Antonio, Miami, LA, Houston.
- **`f41c5a8`** — Add QuickStart 3-step section to metro page; NY-specific callout in Disclosures.

### 2026-04-26

- **`4184960`** — Add inspection, title, mortgage, insurance categories + affiliates. New `ServicesGrid`.
- **`2118001`** — Wire `METRO_FORMS` into Disclosures component.
- **`024a6f2`** — Add `country` field to Metro type. Fix Canadian affiliate links.
- **`a4ef28d`** — Move Census API server-side via `/api/census` proxy.
- **`bc932f1`** — Internal linking: metro suburbs grid, suburb intro paragraphs.
- **`3c50df7`** — Add NetProceedsCalculator, CMA email gate, testimonials.

---

## Open Items

### Domain-deferred (action needed after byownerhub.com points at Netlify)
1. **Google Search Console** — Submit `https://byownerhub.com/sitemap.xml`. DNS TXT verification required.
2. **Bing Webmaster Tools** — Submit sitemap (IndexNow handles pings but sitemap still needs manual submission).
3. **Google Business Profile** — Not created yet.
4. **IndexNow plugin HOST** — `netlify/plugins/indexnow/index.js` uses `www.byownerhub.com`; canonical is non-www. Fix after domain is live.

### Active bugs
~~10. **Bug A — "Download Disclosures" CTA not fully renamed**~~ — **RESOLVED `2f63477`** Hero.tsx and suburb page both now say "Download {state} Forms".
~~11. **Bug B — Scroll-to-top on tab return**~~ — **RESOLVED `2f63477`** Root cause: `document.documentElement.scrollTop = 0` in ScrollToTop.tsx used CSS `scroll-behavior: smooth` and fired an async animation that completed after tab switch. Fixed: removed redundant scrollTop assignments, added `history.scrollRestoration = 'manual'`.

### Code (domain-independent, can fix any time)
5. **Placeholder affiliate URLs** — 11 affiliates still have `#` URLs. Expected/intentional — pending affiliate program approvals.
6. **`unsubscribed/page.tsx`** — No metadata export at all (not even noindex). Low priority.
7. **`sameAs: []`** — Empty array in Organization schema on homepage. Populate with social URLs once accounts exist.
8. **`FAQSection.tsx:31` stale copy** — "If your question isn't here, try the AI Advisor above — it knows the local rules." — AI Advisor no longer exists above the FAQ; text needs to be updated or removed.
~~9. **`Disclosures` renders `metroForms` twice**~~ — **RESOLVED 2026-05-15** `Disclosures` component removed from all pages. `FormsLibrary` (VF) is now the sole forms section. Dead file `src/components/Disclosures.tsx` can be deleted when confirmed no longer needed.
9b. **`src/components/Disclosures.tsx` dead file** — Component is no longer imported or rendered anywhere. Can be safely deleted once branch is merged and confirmed stable.
9c. **FL — `fl-orl-cdd` CDD Disclosure has no Miami/Tampa equivalent** — After 2026-05-15 cross-metro audit, Orlando is the only FL metro with a Community Development District disclosure (`fl-orl-cdd`). CDDs are also common in Hillsborough/Pasco (Tampa) and parts of Miami-Dade. Decide: add a matching CDD form to Miami and Tampa (copy `fl-orl-cdd` with `fl-*`-prefixed IDs and metro-specific notes), or leave Orlando-only if CDD prevalence doesn't warrant it for those metros.

### Content fixes — AI advisor references (audited 2026-05-08)

The AI chat feature was removed. The following instances of "AI advisor" / "AI chat" remain in the codebase and need to be cleaned up. **These are content/copy fixes, not functional bugs.** The listing description and price estimate tools still use Claude API — do NOT touch those.

**Legal pages (highest priority — these are user-facing policy documents):**

10. **`privacy/page.tsx:19`** — Remove bullet `• Chat messages — when you use the AI advisor feature...` from "Information We Collect" section.
11. **`privacy/page.tsx:36`** — Remove `Clever Real Estate` from affiliate examples list (already removed from site).
12. **`privacy/page.tsx:41–45`** — Remove entire "AI Chat (Powered by Claude)" section.
13. **`privacy/page.tsx:54`** — Remove sentence `We do not retain chat message history.` from "Data Retention".
14. **`terms/page.tsx:42`** — Remove `AI chat responses,` from the content description list in section 2.
15. **`terms/page.tsx:49–53`** — Remove entire "3. AI Advisor Disclaimer" section; renumber sections 4–11 → 3–10.

**Site-facing copy (medium priority — visible to users/crawlers):**

16. **`[metro]/opengraph-image.tsx:72`** — Remove `AI advisor ·` from OG image text (`Free disclosures · Flat fee MLS · AI advisor · No agent required`).
17. **`[metro]/blog/[slug]/page.tsx:184–185`** — Remove `→ Ask the AI Advisor` link (points to `#chat` anchor that no longer exists).
18. **`[metro]/blog/[slug]/page.tsx:245`** — Remove `and AI advisor` from CTA copy.
19. **`[metro]/blog/[slug]/page.tsx:260`** — Remove `and an AI advisor` from CTA copy.
20. **`[metro]/[suburb]/page.tsx:161`** — Remove `and AI advisor` from suburb meta description copy.
21. **`colorado-fsbo-guide/page.tsx:85`** — Remove `and AI advisor` from Denver CTA.
22. **`north-carolina-fsbo-guide/page.tsx:85`** — Remove `and AI advisor` from Charlotte CTA.
23. **`tennessee-fsbo-guide/page.tsx:85`** — Remove `and AI advisor` from Nashville CTA.

**Data/templates (lower priority — not directly user-facing):**

24. **`lib/blog.ts:394`** — Remove `*Use the [AI Advisor](/chicago#chat)...*` line from Chicago blog post.
25. **`lib/blog.ts:818`** — Remove `*Use the [AI Advisor](/seattle#chat)...*` line from Seattle blog post.
26. **`lib/email.ts:59`** — Remove `<li>Chat with the AI FSBO advisor (${state_code}-specific)</li>` from email template.
27. **`lib/data.ts:21`** — Remove `& AI advisor` from Boston SEO description.
28. **`lib/data.ts:106`** — Remove `and AI advisor` from Austin SEO description.
29. **`lib/data.ts:123`** — Remove `and AI advisor` from Houston SEO description.

**Dead code to verify:**

30. **`[metro]/page.tsx:13`** and **`[metro]/[suburb]/page.tsx:18`** — Both import `ListingGenerator from '@/components/AIChat'`. Verify whether `ListingGenerator` is rendered anywhere in these files. If unused, remove the import (and possibly the `AIChat` component itself if nothing else uses it).
31. **`types/index.ts:92`** — `ChatMessage` interface. The `/api/chat` route was deleted. Verify nothing else references this type; if dead, remove.

*(All other medium/low items from the audit were resolved in the 2026-05-06 cleanup passes above.)*

---

## Content Improvements — Queued

These are UX/content enhancements, not code bugs. Implement in a future session when ready.

### 1. Boston & Worcester — 6(d) Certificate collapsible notes

In the disclosure forms section for Boston (`/boston`) and Worcester (`/worcester`), add a collapsible "Notes" dropdown beneath the 6(d) Certificate form entry. Content:

> A 6(d) Certificate is a mandatory Massachusetts legal document (M.G.L. c. 183A, § 6(d)) for selling a condominium. It proves the seller is up-to-date on fees or discloses any outstanding balances, protecting the buyer and lender from the seller's unpaid condo debt. It must be notarized and recorded at the Registry of Deeds.

Bullet points to include:
- **Purpose:** Confirms all condo fees, special assessments, and fines are paid by the seller up to the closing date
- **Validity:** Required for transfer of ownership of a condominium in Massachusetts
- **"Clean" vs. "Dirty":** A "clean" certificate = no unpaid fees. A "dirty" certificate = outstanding charges that must be resolved before or at closing
- **Obtaining:** Seller typically orders from the condo association or property manager
- **Timing & Cost:** Request 7–14 days before closing. Costs $75–$250

**Implementation note:** Forms are now rendered exclusively by `src/components/FormsLibrary.tsx` using data from `src/lib/forms.ts`. The 6(d) entry already exists in `METRO_FORMS['boston']`. The `notes` field already exists on `TransactionForm` — render it as a `<details>/<summary>` collapsible in the `FormCard` expanded state in `FormsLibrary.tsx`.

---

### 2. Attorney-drafted documents — seller budget context

For all forms with `url: null` and attorney-drafted context (and any form explicitly described as attorney-drafted in `forms.ts`), add a brief inline callout explaining:
- Why an attorney is required to draft this document (state law, lender requirement, etc.)
- Typical cost range so sellers can budget their FSBO transaction
- Where to find an attorney (e.g., state bar referral, LegalZoom, Avvo)

**Example:** Virginia's HFA Financing Addendum is attorney-drafted. A seller seeing `url: null` with no context doesn't know whether to call an attorney or look for a public form. A short note like "Attorney-drafted — typically $150–$500 through a real estate attorney. Find VA real estate attorneys at [the Virginia State Bar](https://www.vsb.org/lawyer-search/)." removes that confusion.

**Scope:** Audit all entries in `src/lib/forms.ts` where `url: null` and the `notes` or surrounding context implies attorney involvement. Add a `budget_note` field (or extend the existing `notes` field) and surface it in `FormsLibrary.tsx` (`FormCard` expanded state) alongside the form entry.

---

*(All items above are content/UX enhancements — no bugs, no broken functionality.)*

---

## Stats

- **101** metros in data.ts
- **782** suburb entries in suburbs.ts
- **30** state FSBO guides
- **4** Spanish landing pages (Houston, San Antonio, Miami, Los Angeles)
- **24** affiliates in data.ts (12 active categories)
- **8** API routes
- **23** components
