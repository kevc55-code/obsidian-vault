---
type: status
project: FSBO-Hub
last-verified: 2026-08-26
---

# Affiliate Stack — fsbo-hub (v3)

*Last updated: 2026-08-26 — Buildium added (Property Mgmt, enrolled, placement undecided).*

> **Houzeo has NO affiliate program — do not add to any site.**

---

## Confirmed Programs

| Category | Program | Commission | Status | Notes |
|---|---|---|---|---|
| Moving (labor) | HireAHelper | $10/booking | ✅ **Enrolled** | Link: `https://www.hireahelper.com/?affil=32303735` — replace `?via=fsbohub` with this |
| Moving (labor) | Moving Labor Brokers | $25/sale | 🔲 Pending | In `src/lib/` but not rendered on any page yet — decide placement before next deploy |
| Moving (container) | U-Pack | $50/reservation | 🔲 Pending | |
| Junk Removal | 1-800-GOT-JUNK | TBD | 🔲 Pending | |
| Storage | SpareFoot | $7/lead | 🔲 Pending | |
| Insurance | Lemonade | $25.50/lead | ❌ Rejected | Rejected 2026-05-28 — "not the right fit." Consider EverQuote, Hippo, or Openly as alternatives. |
| Photography | Virtuance | % of sale | 🔲 Pending | |
| Flat-Fee MLS | FlatFee.com | $45/listing | 🔲 Pending | |
| Legal | Nolo | TBD | 🔲 Pending | |
| Legal | LegalZoom | ~18%/sale | 🔲 Pending | |
| Legal | US Legal Forms | $40–$50/sale | 🔲 Pending | |
| Mortgage | LendingTree | $1–$70/lead | 🔲 Pending | Not yet applied |
| Mortgage | Rocket Money | up to $500/loan | 🔲 Pending | |
| Home Services | Angi (fka HomeAdvisor) | 25% revshare | ✅ **Enrolled** | Via CJ. Publisher ID: 101755238. Contact: affiliate@angi.com. See links below. |
| Property Mgmt | Buildium | **TBD — confirm in Impact** | ✅ **Enrolled** | Accepted 2026-08-26 via Impact (Gen3 Marketing). Media ID `7372899`. **Landlord/FRBO audience only — not fsbo-hub.** Placement undecided. See links below. |

---

## Buildium Links (Impact, Media ID: 7372899)

Property-management software. **Wrong audience for fsbo-hub** — someone selling their own home has
no use for rent collection or tenant screening. Fits `landlord-hub` and `rent-hub`/`frbo-hub`;
marginal on `closing-hub` (only new owners intending to rent out). Do not place on fsbo-hub.

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

## Action Needed — HireAHelper Link Swap

The `?via=fsbohub` placeholder on HireAHelper links in fsbo-hub needs to be replaced with the real affiliate URL:
`https://www.hireahelper.com/?affil=32303735`

Also email `affiliate-support@hireahelper.com` to add all network domains once they're live.
