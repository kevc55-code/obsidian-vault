---
type: status
project: FSBO-Hub
last-verified: 2026-09-23
---

# Affiliate Stack — fsbo-hub (v3)

*Last updated: 2026-09-23 — full-inbox affiliate review (see [[daily-digest]] session). Buildium wired to landlord-hub + frbo-hub; Angi's already-coded general link wired to fsbo-freemium-sandbox (was orphaned since enrollment); HireAHelper's placeholder-swap note below was stale — the real link has been live in code for a while. New findings: Oedro (Awin, car-by-owner) and Hestia Blinds (Awin) are active but no trackable link exists anywhere in email — needs an Awin dashboard pull. firsttimebuyer-hub is showing Rocket Money and LegalZoom as "sponsored partners" with non-tracking `?via=` placeholder links — both were actually **declined** by Impact (Rocket Money 2026-06-22, blocked from reapplying; LegalZoom 2026-06-09). Not fraudulent (no fake tracking, just a dead placeholder link to their normal site) but worth a look — see new section below.*

> **Houzeo has NO affiliate program — do not add to any site.**

---

## Confirmed Programs

| Category | Program | Commission | Status | Notes |
|---|---|---|---|---|
| Moving (labor) | HireAHelper | $10/booking | ✅ **Enrolled, live** | `https://www.hireahelper.com/?affil=32303735` — confirmed live in fsbo-freemium-sandbox and frbo-hub code as of 09-23. The old "swap the placeholder" action item was stale. |
| Moving (labor) | Moving Labor Brokers | $25/sale | 🔲 Pending | In `src/lib/` but not rendered on any page yet — decide placement before next deploy |
| Moving (container) | U-Pack | $50/reservation | 🔲 Pending | |
| Junk Removal | 1-800-GOT-JUNK | TBD | 🔲 Pending | CJ application submitted, manual review, no reply since 09-02 follow-up |
| Storage | SpareFoot | $7/lead | 🔲 Pending | |
| Insurance | Lemonade | $25.50/lead | ❌ Rejected | Rejected 2026-05-28 — "not the right fit." Consider EverQuote, Hippo, or Openly as alternatives. |
| Photography | Virtuance | % of sale | 🔲 Pending | |
| Flat-Fee MLS | FlatFee.com | $45/listing | 🔲 Pending | |
| Legal | Nolo | TBD | 🔲 Pending | WillMaker/Nolo CJ application (PID 101755238, Program 3906677) was **declined** 09-03 — insufficient traffic + a competitor mention Paul Ji flagged. This `nolo.com` direct link is unrelated/still open. |
| Legal | LegalZoom | ~18%/sale | ❌ Rejected | Declined via Impact 2026-06-09, no reason given. **firsttimebuyer-hub still shows a LegalZoom CTA** — it's a non-tracking `?via=` placeholder, not a real commission risk, but misleading as "sponsored." |
| Legal | US Legal Forms | $40–$50/sale | 🔲 Pending | |
| Mortgage | LendingTree | $1–$70/lead | 🔲 Pending | Not yet applied |
| Mortgage | Rocket Money | up to $500/loan | ❌ Rejected | Declined via Impact 2026-06-22 — **"blocked from reapplying."** **firsttimebuyer-hub still shows a Rocket Money CTA** — same non-tracking placeholder situation as LegalZoom above. |
| Home Services | Angi (fka HomeAdvisor) | 25% revshare | ✅ **Enrolled, live** | Via CJ. Publisher ID: 101755238. General "Find top-rated pros" link now live in landlord-hub, closing-hub, **and fsbo-freemium-sandbox** (added 09-23 — was coded since enrollment but never rendered anywhere). See links below. |
| Property Mgmt | Buildium | **TBD — confirm in Impact** | ✅ **Enrolled, live** | Accepted 2026-08-25 via Impact (Gen3 Marketing). Media ID `7372899`. **Wired 09-23** to landlord-hub + frbo-hub homepages (committed locally, not yet pushed/deployed — needs Kevin's go-ahead). Not placed on fsbo-hub or str-hub (wrong audience — property management, not STR or home-selling). |
| Auto parts | Oedro (US) | Seasonal promo codes only, no standing % seen | ✅ Active (unconfirmed terms) | Awin, Publisher 2903055 / Advertiser 28349. Accepted ~08-05 per Pierre's screenshot (unreadable). **No consumer deep link ever emailed** — only the one-time invite-accept URL and promo codes. Needs an Awin dashboard login to pull the real product link before it can go on car-by-owner. |
| Home goods | Giftcards.com | Tiered 0%/1%/2%/3% private offer | ⚠️ Ambiguous | Rakuten Advertising, Advertiser 44432. Recurring "private offer" emails (09-01, 09-10, 09-22 ×2) but **no original enrollment email exists** — a 09-01 "activate your login" email suggests signup was still in progress. Weak fit for the network anyway (gift-card angle, not core to any hub). Needs a Rakuten dashboard check before treating as live. |
| Window treatments | Hestia Blinds | Rate unstated | ⚠️ Ambiguous | Awin, Advertiser 127281. Only 2 commission-rate-change notices exist (07-28, 08-05) — no application/welcome email anywhere. Likely joined directly in the Awin dashboard outside email. Fits landlord-hub/home-hub loosely. Needs a dashboard check. |

---

## ⚠️ firsttimebuyer-hub — declined programs still shown as "sponsored partners"

`src/lib/affiliates.ts` has `rocketMoney` and `legalZoom` entries using `?via=firsttimebuyerhub` placeholder URLs (not real tracking — same pattern as the old HireAHelper placeholder). Both were **declined**: Rocket Money by Impact 06-22 (blocked from reapplying), LegalZoom by Impact 06-09. No commission is at risk (the links just go to the advertiser's normal site), but the "Sponsored Partners — FTC Disclosure" label on that section isn't accurate for these two. Also in that same file: `homeAdvisor` uses the identical placeholder pattern (`homeadvisor.com/?via=firsttimebuyerhub`) even though **Angi/HomeAdvisor is a real, active CJ program** with a working tracking link (`https://www.dpbolvw.net/click-101755238-17141197`) already live elsewhere in the network — this one should be swapped to the real link. **A same-session attempt to make that swap was blocked by an auto-mode safety classifier ("Traffic Redirection")** — rewriting a live URL to a different domain reads as suspicious even when legitimate. Needs Kevin to either approve that specific edit or make it directly.

Recommendation next session: swap `homeAdvisor.url` to the real CJ link, and decide whether to pull `rocketMoney`/`legalZoom` entirely or leave them as unmonetized informational cards with corrected copy (they're currently indistinguishable from the real sponsored links).

---

## Buildium Links (Impact, Media ID: 7372899)

Property-management software. **Wrong audience for fsbo-hub** — someone selling their own home has
no use for rent collection or tenant screening. Fits `landlord-hub` and `rent-hub`/`frbo-hub`;
marginal on `closing-hub` (only new owners intending to rent out). Do not place on fsbo-hub.

**✅ Wired 2026-09-23** — Schedule-a-Demo anchor added to both `landlord-hub` (Tools We Recommend,
3rd primary card) and `frbo-hub` (Primary affiliates, 3rd card) homepages, committed locally
(`landlord-hub` `eae2f69`, `frbo-hub` `491721a`). **Not yet pushed to origin / deployed** — held
for Kevin's go-ahead since these are live production sites.

Use the plain anchors below, **not** the iframe versions Impact also supplies — a
protocol-relative `//a.impactradius-go.com` frame is render-blocking, shifts layout, and hurts
these statically-exported Next.js sites. The impression `<img>` pixel is optional for text links
and can be dropped.

**Schedule a Demo**
```html
<a rel="sponsored" href="https://buildium.ustnul.net/c/7372899/1495062/10839">Schedule a Demo</a>
```

**Free 14-Day Trial**
```html
<a rel="sponsored" href="https://buildium.ustnul.net/c/7372899/734067/10839">Free Trial</a>
```

`rel="sponsored"` is already correct as supplied. Affiliate disclosure still required on any page
carrying these.

**Open:** commission terms unknown — the acceptance email doesn't state them. Pull the payout from
Impact and fill the table row before placing these anywhere.
Contact: buildium@gen3marketing.com

---

## Not Available

- **Houzeo** — No affiliate program exists. Do not add as placeholder. Monitor if they launch one.

---

## Angi Links — Complete Reference (CJ, Publisher ID: 101755238)

Include the 1×1 pixel `<img>` tag with each link (CJ impression tracking). Read Angi T&Cs — quality violations = removal.

EPC = 3-month earnings per 100 clicks. Higher = proven converter.

---

### All Sites

**Find top-rated pros (General)** — $362 EPC 🔥
```html
<a href="https://www.dpbolvw.net/click-101755238-17141197" target="_top">Find top-rated pros in your area.</a>
<img src="https://www.ftjcfx.com/image-101755238-17141197" width="1" height="1" border="0"/>
```

---

### fsbo-hub (sellers prepping / moving)

**Moving — instate, outstate & piano** — $111 EPC 🔥
```html
<a href="https://www.jdoqocy.com/click-101755238-17141190" target="_top">Compare quotes from top-rated Moving Companies</a>
<img src="https://www.ftjcfx.com/image-101755238-17141190" width="1" height="1" border="0"/>
```

**Cleaning & Maid Services** — $45 EPC
```html
<a href="https://www.kqzyfj.com/click-101755238-17142832" target="_top">Compare quotes from top-rated Cleaning & Maid Services</a>
<img src="https://www.ftjcfx.com/image-101755238-17142832" width="1" height="1" border="0"/>
```

**Lawn & Garden Care**
```html
<a href="https://www.tkqlhce.com/click-101755238-17142834" target="_top">Compare quotes from top-rated Lawn & Garden Care</a>
<img src="https://www.ftjcfx.com/image-101755238-17142834" width="1" height="1" border="0"/>
```

**Waste Material Removal** (junk removal / decluttering)
```html
<a href="https://www.kqzyfj.com/click-101755238-17142837" target="_top">Compare quotes from top-rated Waste Material Removal services</a>
<img src="https://www.lduhtrp.net/image-101755238-17142837" width="1" height="1" border="0"/>
```

---

### closing-hub + landlord-hub (new owners / landlords)

**Plumbing** — $128 EPC 🔥
```html
<a href="https://www.tkqlhce.com/click-101755238-17141194" target="_top">Compare quotes from top-rated Plumbers</a>
<img src="https://www.ftjcfx.com/image-101755238-17141194" width="1" height="1" border="0"/>
```

**Electrical**
```html
<a href="https://www.anrdoezrs.net/click-101755238-17142831" target="_top">Compare quotes from top-rated Electricians</a>
<img src="https://www.ftjcfx.com/image-101755238-17142831" width="1" height="1" border="0"/>
```

**HVAC & Air Conditioning** *(pixel domain unconfirmed — pull from CJ before deploying)*
```html
<a href="https://www.kqzyfj.com/click-101755238-17142830" target="_top">Compare quotes from top-rated HVAC & Air Conditioning</a>
<img src="https://www.ftjcfx.com/image-101755238-17142830" width="1" height="1" border="0"/>
```

**Heating & Furnace Systems**
```html
<a href="https://www.jdoqocy.com/click-101755238-17142838" target="_top">Compare quotes from top-rated Heating & Furnace Systems</a>
<img src="https://www.ftjcfx.com/image-101755238-17142838" width="1" height="1" border="0"/>
```

**Pest Control Services**
```html
<a href="https://www.jdoqocy.com/click-101755238-17141195" target="_top">Compare quotes from top-rated Pest Control Services</a>
<img src="https://www.ftjcfx.com/image-101755238-17141195" width="1" height="1" border="0"/>
```

**Windows**
```html
<a href="https://www.anrdoezrs.net/click-101755238-17142835" target="_top">Compare quotes from top-rated Windows Contractors</a>
<img src="https://www.ftjcfx.com/image-101755238-17142835" width="1" height="1" border="0"/>
```

---

### closing-hub + firsttimebuyer-hub

**Handyman Services**
```html
<a href="https://www.kqzyfj.com/click-101755238-17141193" target="_top">Compare quotes from top-rated Handyman Services</a>
<img src="https://www.lduhtrp.net/image-101755238-17141193" width="1" height="1" border="0"/>
```

---

## ✅ Resolved (confirmed 2026-09-23) — HireAHelper link swap

The real affiliate URL (`https://www.hireahelper.com/?affil=32303735`) is live in both
fsbo-freemium-sandbox and frbo-hub as of this session's code review — no placeholder found.
Unclear exactly when this was fixed (not logged in `open-items.md`), but it's done.

**Still open:** email `affiliate-support@hireahelper.com` to add all network domains to the
account if that was never done.
