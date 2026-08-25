# ByOwnerHub — Sequenced Build Plan
*Based on existing kevc55-code repos + Build Brief*
*Last updated: 2026-06-21*

---

## How to read this

Each phase is a working unit. Phases 1–2 are blockers for everything else. Within a phase, tasks are ordered by dependency. `TODO:` = human decision required before that task can be coded.

---

## PHASE 1 — Supabase + Shared Infrastructure
*Estimated effort: 3–5 days. Everything else depends on this.*

### 1.1 Supabase project setup
- Create Supabase project (or confirm existing one)
- Add env vars to Netlify: `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY` (server-side only, never client-exposed)
- Run initial migration:

```sql
CREATE TABLE geo_pages (
  id           uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  vertical     text NOT NULL,
  state        text NOT NULL,
  metro        text NOT NULL,
  slug         text NOT NULL UNIQUE,
  content      jsonb NOT NULL DEFAULT '{}',
  updated_at   timestamptz DEFAULT now()
);

CREATE TABLE affiliate_offers (
  id        uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  vertical  text NOT NULL,
  placement text NOT NULL,
  name      text NOT NULL,
  pitch     text,
  url       text NOT NULL,
  active    boolean DEFAULT true,
  sort      int DEFAULT 0
);

CREATE TABLE leads (
  id           uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  vertical     text NOT NULL,
  payload      jsonb NOT NULL,
  consent_text text NOT NULL,
  consent_ts   timestamptz NOT NULL,
  ip           text NOT NULL,
  network      text,
  status       text DEFAULT 'pending',
  created_at   timestamptz DEFAULT now()
);

CREATE INDEX ON geo_pages (vertical, state, metro);
CREATE INDEX ON affiliate_offers (vertical, placement) WHERE active = true;
CREATE INDEX ON leads (vertical, created_at);
```

### 1.2 `<GeoPage>` template component
- Location: `packages/ui/src/GeoPage.tsx` (or shared lib within monorepo, OR copy pattern into each hub for now if not monorepo)
- Props: `vertical`, `state`, `metro`, `content` (from Supabase `content` jsonb)
- Renders: local headline, incentives slot, regulations slot, average-cost slot, `<LeadForm>` or `<AffiliateBlock>` depending on vertical config
- Page file: `app/[state]/[metro]/page.tsx` with `generateStaticParams` pulling from `geo_pages` table
- ISR revalidation: 24h
- Ships with: `<title>`, `<meta description>`, canonical, JSON-LD LocalBusiness schema, sitemap entry

### 1.3 `<LeadForm>` component (TCPA-compliant)
- Location: `packages/ui/src/LeadForm.tsx`
- Required props: `vertical`, `advertiserName` (single named advertiser — FCC 2025 rule)
- Configurable qualifying fields via `fields` prop array (each field: name, label, type, required)
- Hardcoded consent block: "By submitting, I consent to be contacted by [advertiserName] regarding [vertical] services. I agree to the Terms of Service and Privacy Policy." + explicit checkbox
- On submit: POST to `/api/leads` route → stores to `leads` table (consent_text + consent_ts + IP) → calls lead-network adapter
- Client-side: no credentials, no network keys. API route only.
- Error states: network failure → show user-facing error, still store lead locally

### 1.4 Lead-network adapter (`lib/lead-networks/`)
- Interface: `postLead(vertical: string, payload: LeadPayload): Promise<LeadResult>`
- Adapter files (stub + TODO):
  - `modernize.ts` — home services (roofing, HVAC, windows, gutters) — TODO: apply + get API key
  - `profitise.ts` — cash-offer / motivated seller — TODO: apply + get API key
  - `index.ts` — routes by vertical to correct adapter
- Credentials: env vars only, never in client bundle

### 1.5 `<AffiliateBlock>` component
- Location: `packages/ui/src/AffiliateBlock.tsx`
- Props: `vertical`, `placement` (fetches matching rows from `affiliate_offers` at build time or via server component)
- Renders: partner card(s) — image, pitch text, CTA button
- Link attrs: `rel="sponsored noopener"`, click event fires to analytics
- A/B slot: if multiple active offers for same placement, rotate by session or render stacked (decide)
- TODO: populate `affiliate_offers` table with actual partner URLs and IDs per vertical

### 1.6 Analytics event spec
Standardize these events across all modules (Umami / Plausible):
- `lead_submit` → props: `vertical`, `network`, `metro`
- `affiliate_click` → props: `vertical`, `placement`, `partner_name`
- `geo_page_view` → props: `vertical`, `state`, `metro`

---

## PHASE 2 — Module B: New-Homeowner Hub
*Build before Module A. No lead-network dependency. Fast revenue. Existing closing-hub feeds it.*

**Repo:** new or subfolder in `byownerhub-hub` at `/new-homeowner/`
**Cross-link from:** `closing-hub` (at the moment of close — add CTA to closing checklist/confirmation page)

### Tasks

**2.1 Content structure**
- Route: `/new-homeowner/`
- Sub-routes: `/new-homeowner/[category]` for each of:
  - `home-security`, `home-warranty`, `internet-setup`, `appliances`, `furniture`, `lawn-care`, `pest-control`, `smart-home`

**2.2 "First 90 Days" interactive checklist**
- Client component — checklist items grouped by week (Week 1, Month 1, Month 3)
- Each item: checkbox + reveal animation → `<AffiliateBlock vertical="new-homeowner" placement={category}>`
- State: local (no auth needed), optional email capture at end for moving checklist PDF
- TODO: copy for each checklist item

**2.3 Affiliate slots to populate in `affiliate_offers`**
- Home security: Ring (Amazon Associates or Ring affiliate), SimpliSafe, ADT
- Home warranty: American Home Shield, Choice Home Warranty
- Internet/ISP: T-Mobile Home Internet, Xfinity (CJ Affiliate) — TODO: confirm programs
- Lawn care: TruGreen, Sunday Lawn (TODO: affiliate program check)
- Pest: Orkin, Terminix (TODO: affiliate program check)
- Smart home: Amazon (Associates), Best Buy (Impact)
- TODO: all of the above need program applications / ID confirmation

**2.4 SEO pages**
- `/new-homeowner/` — "First 90 days after closing your home"
- `/new-homeowner/home-security/` — "Best home security systems for new homeowners 2026"
- (one content page per category, each pulling `<AffiliateBlock>`)

**2.5 Cross-link wire-up**
- Add CTA to closing-hub post-close page: "What to do next → Your First 90 Days Guide"

**Acceptance criteria:**
- [ ] Checklist renders and each category reveals affiliate cards
- [ ] `affiliate_clicks` fires on every CTA
- [ ] closing-hub links to new-homeowner hub

---

## PHASE 3 — Module A: Home-Services Lead Gen (Roofing first)
*Clones the solar build. Uses GeoPage + LeadForm + Modernize adapter.*

**Repo:** `contractor-hub` (decision: rename/reposition as home-services hub, or keep contractor-hub and add roofing/HVAC as sub-verticals)
**TODO:** confirm repo strategy before building URL structure

### Tasks

**3.1 Seed `geo_pages` for roofing**
- Script to populate table: top 50 metros × roofing vertical
- Content jsonb fields: `avg_cost_low`, `avg_cost_high`, `local_incentives`, `common_issues`, `headline`
- TODO: data source for per-metro cost ranges (RSMeans, HomeAdvisor data, or AI-generated estimates with disclaimer)

**3.2 Roofing geo pages**
- Route: `/roofing/[state]/[metro]/` (e.g., `/roofing/tx/dallas/`)
- Renders `<GeoPage vertical="roofing">` with:
  - H1: "Roof Replacement Cost in [Metro] (2026)"
  - Cost range pulled from content jsonb
  - `<LeadForm vertical="roofing" advertiserName="TODO: Modernize">` qualifying fields:
    - Homeownership (yes/no)
    - ZIP code
    - Project type (replace / repair / inspect)
    - Urgency (emergency / within 3 months / planning ahead)
    - Roof size estimate (small / medium / large)
  - Supporting content: repair vs. replace, financing options, what to expect
- JSON-LD: `HomeAndConstructionBusiness` schema

**3.3 Modernize adapter**
- TODO: apply to Modernize (modernize.com/partners)
- TODO: get API credentials
- Wire `modernize.ts` adapter to roofing lead submissions

**3.4 Phase-in verticals** (after roofing converts)
- HVAC: clone roofing geo pages, update qualifying fields (system type, age, issue type)
- Windows: same pattern
- Gutters: same pattern
- Each is a new vertical slug, same `<GeoPage>` + `<LeadForm>` pattern

**Acceptance criteria:**
- [ ] `/roofing/tx/dallas/` (and 49 other metros) render, indexed, sitemapped
- [ ] Lead form submits → `leads` table row with consent stored
- [ ] Lead posts to Modernize (once API key obtained)
- [ ] TODO stubs clearly labeled where network not yet wired

---

## PHASE 4 — Module D: Cash-Offer Lead Gen
*Captures FSBO bounce traffic. High per-lead value. Wires to investor network.*

**Placement:** secondary/exit CTA on existing FSBO tools ("Need to sell fast instead?")
**Repo:** `investor-hub` (already exists — reposition as cash-offer comparison flow)

### Tasks

**4.1 Cash-offer landing page + comparison flow**
- Route: `/cash-offer/` or `investor-hub` root
- Flow: simple wizard (3 steps)
  - Step 1: property basics (address/ZIP, bedrooms, condition)
  - Step 2: situation (reason for selling: divorce / relocation / foreclosure / inherited / other; timeline; mortgage status)
  - Step 3: consent + submit (`<LeadForm vertical="cash-offer" advertiserName="TODO: network name">`)
- Post-submit: "You'll hear from [network] within X hours" confirmation

**4.2 Lead network**
- TODO: select investor/cash-offer network (options: HomeVestors, We Buy Houses, PropStream, or direct iBuyer API)
- Wire `profitise.ts` adapter (or new adapter) once selected

**4.3 FSBO tool integration**
- Add exit/secondary CTA to existing FSBO listing generator: "Need a fast close instead? Compare cash offers →"
- Add to net-proceeds calculator results: "See what cash buyers would offer"

**4.4 High-intent sub-pages**
- `/cash-offer/inherited-house/` → cross-feeds Module E (probate)
- `/cash-offer/divorce/` → cross-feeds Module F
- `/cash-offer/foreclosure/` → existing foreclosure-hub cross-link

**Acceptance criteria:**
- [ ] 3-step wizard completes and posts lead with consent stored
- [ ] FSBO tools have cash-offer CTA
- [ ] Sub-pages for inherited/divorce/foreclosure render and cross-link

---

## PHASE 5 — Module C: Landlord / Rent-By-Owner Hub
*Reuses forms infrastructure. Opens repeat-transactor audience.*

**Repo:** `landlord-hub` + `eviction-hub` (both exist — landlord-hub is primary, eviction-hub cross-links)

### Tasks

**5.1 State-specific lease generator**
- Existing forms pattern (reuse disclosure/forms finder architecture)
- Input: state, property type (single-family/multi-unit/condo), lease term, rent amount, deposit
- Output: state-specific lease template (plain text / copyable — NOT legal advice, add disclaimer)
- TODO: source/review state lease templates for accuracy

**5.2 Rent-increase notice generator**
- Input: state, current rent, new rent, effective date
- Output: notice text with state-required notice period pre-filled
- Cross-link to `/landlord/[state]/rent-increase-laws/` content page

**5.3 Rental application form builder**
- Generates a printable/linkable rental application
- Standard fields + state-specific fields where required

**5.4 Affiliate slots**
- Tenant screening: TransUnion SmartMove (affiliate program exists), RentPrep
- Landlord insurance: Steadily, NREIG — TODO: affiliate program applications
- Rent collection SaaS: Avail, TurboTenant, Rentec Direct — recurring commissions — TODO: apply
- Legal/eviction forms: US Legal Forms (existing partner — wire in here)

**5.5 eviction-hub integration**
- eviction-hub becomes the eviction-process content + legal forms cross-link
- CTA from landlord-hub tools → eviction-hub for process guides
- Affiliate: US Legal Forms eviction forms

**Acceptance criteria:**
- [ ] Lease generator produces state-correct output for all 50 states (or clear "coming soon" for unbuilt states)
- [ ] Screening/insurance/SaaS affiliate cards render
- [ ] eviction-hub cross-links are in place

---

## PHASE 6 — Lateral Modules (layer on existing repos)

These are lower effort — each existing repo gets a content strategy + affiliate/lead wiring, not a ground-up build.

| Module | Existing Repo | Primary Action | Key Affiliate/Lead |
|--------|--------------|----------------|--------------------|
| E — Probate/Inherited | `probate-hub`, `estate-hub` | Content: "just inherited a house — your options" + cash-offer CTA (Module D) | US Legal Forms probate, Module D lead form |
| F — Divorce | `divorce-hub` | Content: "selling the marital home" + buyout vs. sell tool | Cash-offer CTA, Module C lease gen if keeping property |
| G — Senior downsizing | `55plus-hub` | Expand content: downsizing guide + Module B new-homeowner hub cross-link for buyers | Moving services affiliate, senior-move-manager — TODO: programs |
| H — EV/Electrification | `solar-hub` expansion | EV charger install geo pages, heat pump geo pages — same `<GeoPage>` + `<LeadForm>` | TODO: EV charger install network (Qmerit?) |
| I — By Owner extensions | `rv-hub`, `boat-hub`, `biz-hub`, `moto-hub` | Each gets listing template config + relevant affiliate set | TODO: vertical-specific affiliate programs |

---

## Decisions needed before coding starts

These are the `TODO:` items that block specific phases. Group them by urgency:

**Block Phase 1:**
- [ ] Confirm Supabase project (new vs. existing, which plan)
- [ ] Confirm whether repos stay independent or move toward monorepo / shared package

**Block Phase 2:**
- [ ] Affiliate program applications: SimpliSafe, ADT, home warranty cos, ISPs, lawn/pest
- [ ] Confirm new-homeowner hub lives at `byownerhub-hub/new-homeowner/` vs. new domain

**Block Phase 3:**
- [ ] Apply to Modernize (or alternative home-services network)
- [ ] Confirm `contractor-hub` repo strategy (rename? repurpose?)
- [ ] Data source for per-metro roofing cost ranges

**Block Phase 4:**
- [ ] Select cash-offer/investor network and apply
- [ ] Confirm `investor-hub` is the right repo for this

**Block Phase 5:**
- [ ] Landlord insurance affiliate applications (Steadily, NREIG)
- [ ] Rent collection SaaS affiliate applications (Avail, TurboTenant)
- [ ] Legal review process for lease generator templates

**Block Phase 6 (per module):**
- [ ] Senior moving / senior-move-manager affiliate programs
- [ ] EV charger network (Qmerit, or direct)
- [ ] RV/boat/business-for-sale affiliate/marketplace partners

---

## What NOT to do

- Do not rebuild FSBO listing generator, calculators, flyer/PDF generator, open-house kit, or solar lead-gen — they exist
- Do not create new standalone domains for these modules — build as subfolders/subdomains on existing authority domains
- Do not expose affiliate/network credentials client-side
- Do not add Houzeo anywhere (no affiliate program)
- Do not accept $0 contract from Impact for Rocket Money
- Do not deploy to Netlify until further notice (push to GitHub only)
- Do not render Moving Labor Brokers anywhere until placement is decided
