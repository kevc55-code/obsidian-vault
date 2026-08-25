# FSBO-Hub SEO Remediation Plan
**Written:** 2026-07-26 · **Updated:** 2026-07-27 with three GSC exports
**Status:** Phase 0 partially done (data pulled, not yet committed to repo)

> ⚠️ **2026-07-27 data changed the plan's premise. Read this block before executing anything below.**
>
> **1. Blog rewriting is largely the wrong lever.** Only **13 of 236** fsbo blog posts have *any*
> impressions in 3 months (53 impressions total). Critically, the `{city}-home-seller-disclosure-requirements`
> family that *does* appear already ranks at **position 5–11** — they are not failing on quality,
> they are failing on **demand**. No amount of rewriting manufactures search volume.
> The real split is demand vs. no-demand, not indexed vs. unindexed, and not thin vs. thick.
> **Sole genuine content-quality case: the Miami flat-fee post — 30 impr, pos 68.**
>
> **2. fsbo is 1.2% of the network.** Network-wide 3mo: 28,028 impressions, 20 clicks.
> divorce 9,850 · insurance 5,290 · eviction 3,035 · trust 2,030 · closing 1,315 · rv 911 (5 clicks,
> best converter) · **fsbo 336**. Phases 1–3 (linter, data fixes, templates) are worth far more
> pointed at divorce+insurance (54% of impressions). **Open decision — user's call, not made yet.**
>
> **3. Network position is drifting worse while impressions double.** 66.1 (07-17) → 69.6 (07-25),
> impressions 1,100/day → 2,909/day. Top queries are all generic YMYL heads at pos 61–92
> (`homeowners insurance california` 190 impr @85, `revocable trust` 175 @92). Signature of ranking
> for more head terms we can't win. Branded: **1 query, 7 impressions.**
>
> **4. Two flat-fee subdomains exist** — `flatfee` (81 impr) and `flatfeemls` (52). Likely
> self-cannibalization; resolve before any Phase 5 flat-fee work.
>
> **5. Indexing improved but the number is stale.** 35% → **57%** indexed (1,260 of 2,226);
> Discovered–not-indexed 1,177 → 550. **But the Coverage chart is frozen at ~07-11** (identical values
> 07-11→07-24), so it predates the 07-19 noindex and 07-20 enrichment. **Do not credit those fixes.**
>
> **6. The 44 duplicate-canonical pages need re-crawling, not re-fixing.** 38 of 44 were last crawled
> in **June** — pre-enrichment. Per-URL status is 42 Pending / 2 Failed (the summary export's
> issue-level "Failed" is misleading). Action: request validation + resubmit sitemaps.
> Composition: 19 suburb (2.4% of 779 — enrichment looks to be holding), **6 state guides**,
> 5 blog posts, 3 metro, 2 blog indexes (will self-resolve to noindex).
> ↳ **Worth investigating: why 6 of ~50 hand-built state guides read as duplicates.**
> ↳ Checked and rejected: trailing-slash canonical variance. Every flagged URL matches its own repo's
>   `trailingSlash` config (`divorce/eviction/insurance/moto/closing` = true; `fsbo/trust` = unset).
>
> **Also outstanding:** 28 404s · 181 pages-with-redirect · 45 alternate-canonical.
>
> **Note on GSC exports:** the Coverage summary export contains **no per-URL lists**. To get URLs you
> must drill into a single reason in the Pages report and export from that view (as was done for the
> duplicate-canonical list).

---

## 0. Why this exists / what was NOT fixed before

Recurring confusion: we closed a thin-content workstream on 07-19/07-20 and assumed "SEO" was
handled. It wasn't. Precise delta:

**Already fixed (do not redo):**
- Suburb *body copy* thin content — Census enrichment, 741/779 suburbs have real ACS-backed prose (`707b11c`)
- State citation links across divorce/rv/eviction/insurance/trust hubs
- Blog *index* pages (`/{metro}/blog`) noindexed (`bd6054d`)

**Never in scope, still broken (this plan):**
- Title / meta-description formulas (all ~1,100 fsbo pages)
- Blog post structured data — template emits **none**
- Blog post *content* quality and length
- `getSuburbCensusFacts()` ZIP-selection bug
- Copy defects and data errors, never systematically scanned

**Root cause of the wasted cycles:** every prior pass shipped blind — no baseline, no automated
detection, no before/after diff. Phase 0 and 1 exist to end that. **Do not skip them to "save time."**

---

## Ground truth (verified 2026-07-26)

| Fact | Value |
|---|---|
| Blog posts | 236, all in `src/lib/blog.ts` (14,757 lines) |
| Repos with a blog.ts | fsbo-hub only |
| Median post length | ~604 words; **max ~1,200; zero posts over 1,200** |
| Posts with any GSC impression | **~19 of 236** |
| Near-duplicate family | ~104 posts: `how-to-sell-fsbo-{city}-{state}-2026` |
| Suburb pages | 779 (`SUBURBS`), all one template |
| Blog template structured data | **none** — no Article, no FAQPage, no dateModified |
| Encoding corruption in blog.ts | none (verified, 0 suspect chars) |
| GSC (fsbo property, 3mo to 07-24) | 525 impr, 6 clicks, avg pos 39.6, plateaued at ~34 for 3 weeks |

---

## Phase 0 — Baseline & instrumentation
**Gate: nothing else starts until this is committed.**

1. Save the 2026-07-26 GSC export permanently to `tools/seo/baseline/2026-07-26/`
   (Chart/Queries/Pages/Devices/Countries CSVs). The 07-13 and 07-19 exports are **already lost** —
   they only ever lived in temp dirs. Stop doing that.
1b. **Pull a fresh GSC Coverage/Indexing export** and save it alongside. Split the 236 blog posts by
   index status (indexed / crawled-not-indexed / discovered-not-crawled). **This gates Phase 4** —
   see the blocking question there. Do not start rewriting before this number exists.
2. Scaffold `tools/seo/audit.mjs` (see Phase 1) + `npm run seo:audit`.
3. Run it against current `out/`, commit `tools/seo/baseline/2026-07-26/audit.json`.

**Standing rule from here on: no SEO change ships without a before/after audit diff in the commit message.**

---

## Phase 1 — Build the linter (do NOT read 236 files by hand)

`tools/seo/audit.mjs` walks the built static output and emits `report.json` + ranked markdown.
This is the workhorse for every phase below — it finds the defects so we stop fixing from memory.

**Per-URL checks:**
- Title: pixel-width estimate (not char count), duplicates, and **% of title that is boilerplate
  shared by >50 pages** ← this is the metric that catches the current template
- Meta description: length, duplicates, missing
- H1: present, unique, intent-consistent with title
- Structured data: present + correct type per page class (metro / suburb / blog / guide)
- Canonical: present and self-referential
- Word count + **near-duplicate clustering** (MinHash/shingles) across all 236 posts *and* 779 suburb pages
- Internal links in/out → orphan detection

**Data-sanity checks:**
- `median_home_price` vs Census `medianHomeValue` divergence > 40% → flag
- Savings math (3% of median) consistency between H1, meta, FAQ, stat tiles
- Ratio-bucket boundary cases in `getSuburbIntro()` (0.85 / 1.15 / 1.5)
- Per-suburb ZIP spread: flag where mapped ZIPs disagree by >20 points on homeownership/income

**Copy-defect regex ruleset:**
- `{acronym ending in MLS} MLS` (catches "the CRMLS MLS", "the NorthstarMLS MLS")
- Doubled words, double spaces, mixed straight/curly quotes
- Stale year literals (`2024`, `2025`) in user-facing copy
- Unresolved template vars, literal `undefined` / `NaN` / `$0`
- Spell-check against a whitelist of real-estate + place-name terms

**Deliverable:** ranked defect list. Everything after this fixes what the report says, not what we remember.

---

## Phase 2 — Data-correctness fixes
*(Before titles — Phase 3's formulas may cite these values.)*

**2A. `getSuburbCensusFacts()` — `src/lib/suburbs.ts:4308`**
Currently returns the **first ZIP in sorted order** that has data. On Staten Island that's 10301
(North Shore) → reports 46% owner-occupied for a borough that's ~70%. 13 of 14 SI ZIPs have data.
Moreno Valley (4 of 7) and Bloomington MN (4 of 4) have the same arbitrary selection.
→ Replace with population-weighted average across all mapped ZIPs; single-ZIP fallback unchanged.
→ Aggravating factor: the page then claims these are *"real, local figures, not a metro-wide
estimate"* — a wrong number carrying an accuracy claim is worse than no number.

**2B. `getSuburbIntro()` — `src/lib/suburbs.ts:1036`**
- `"the ${mls_name} MLS"` → double acronym on every CRMLS/NorthstarMLS suburb
- "one of the more affordable communities" fires for Staten Island at $590k because the bucket is
  purely ratio-to-metro. Make thresholds absolute-price-aware, not just relative.

**2C. `median_home_price` audit** — 779 hand-entered values. These drive the H1 savings figure on
every suburb page, so a stale one is a visible false claim. Reconcile against Census; fix outliers.

**2D. Network sweep** — same defect classes (`X MLS MLS`, stale years) across the other repos.

---

## Phase 3 — Template-level SEO fixes
**Highest leverage in the whole plan: ~1,100 pages from ~6 file edits. Do not hand-write pages.**

**3A. Title formula — `suburbs.ts:1027`**
Current: `{Name} FSBO Guide — Sell Your Home Without an Agent in {ST}`
→ 37 of ~64 chars are identical across all 779 pages. Google truncates around 55–60, so what
survives is mostly boilerplate and the only differentiator is the first two words.
Worse, it says "FSBO Guide" while actual demand is verb-phrase seller intent:
`sell house staten island` (22 impr), `sell my moreno valley house` (10), `sell my home cranberry township` (5).
→ New formula: front-load intent verb + geo, drop the constant tail, ≤575px.
→ Verify uniqueness + length across all 779 via the audit, not by eyeballing.

**3B. Meta description formula — `suburbs.ts:1028`** — same treatment.

**3C. Blog post template — `src/app/[metro]/blog/[slug]/page.tsx`**
Add Article schema, FAQPage where applicable, `dateModified`, BreadcrumbList. Currently **zero**
structured data, while suburb/metro pages get `SchemaMarkup`. Single highest-value template edit.

**3D. Metro page titles** — audit first; likely the same boilerplate pattern.

**3E. Suburb FAQ scaffold — `[metro]/[suburb]/page.tsx:81`**
Five questions, identical across all 779 pages, variables swapped. Once 3C ships FAQPage schema
sitewide, 779 identical answer sets become a *scaled-content* signal rather than an asset.
Vary by `attorney_required`, price tier, and census data.

---

## Phase 4 — Blog content: every post gets a disposition

**Superseded framing (was wrong):** "leave the zero-impression posts alone." That treats thin content
as neutral. It isn't — quality is assessed partly at the *site* level, so 217 thin near-duplicates
plausibly suppress the whole domain including the pages we do care about. **Nothing stays as-is.**

**Also wrong: the "weeks of work" estimate.** That assumed human writing speed. Generation is fast
and cheap. The actual constraints are (a) fact-verification, (b) tokens, (c) scaled-content risk.

### Blocking question — resolve in Phase 0 before committing to a rewrite

**Are these posts even indexed?** As of the 07-19 Coverage export (sitewide, 7 days old, **re-pull
before relying on it**): 767 of 2,182 pages indexed (35%); 1,177 in "Discovered — currently not
indexed," i.e. never crawled. **For an unindexed page, content quality is not the bottleneck** —
rewriting it changes nothing until it gets crawled, and the real fix is crawl budget + internal
linking. Pull a fresh Coverage export, split the 236 by index status, and let that split size the
REWRITE bucket. Skipping this risks a third consecutive pass fixing the wrong layer.

### Disposition buckets — all 236 get exactly one

- **REWRITE** — the ~19 with impressions, plus any the index-status split shows are indexed and
  demand-validated. 1,500–2,500 words, comparison tables, cited sources, FAQ schema.
  Anchor case: `/miami/blog/miami-fsbo-flat-fee-mls-comparison-2026` — 54 impr at pos 84. Title
  already matches the query exactly, so **this is not a title problem**: 1,100 prose-only words,
  prices buried in paragraphs, no table, no schema, competing against Beycome/Houzeo.
- **CONSOLIDATE** — the ~104 `how-to-sell-fsbo-{city}-{state}` family. Rewriting near-duplicates
  individually preserves the duplication at 2,000 words instead of 600. Merge into strong
  state-level posts with genuinely local city sections; 301 the retired URLs.
- **PRUNE / NOINDEX** — remainder with no demand and no consolidation target. `noindex, follow`,
  same treatment the blog indexes got in `bd6054d`. Removes the site-level drag without pretending
  we'll ever enrich them.

### Cost model (replaces "weeks")

| Constraint | Reality |
|---|---|
| Writing | Not the bottleneck. Fast and cheap. |
| **Verification** | **The real cost.** Every post asserts local facts — transfer taxes, disclosure law, MLS names, fee ranges. Precedent: the state-citation rollout verified every URL individually and caught multiple lookalike/scam domains (`oscn.online`, `vvv.jud.ct.gov`) that bulk-filling would have shipped. Budget 5–15 min per fact-asserting post. |
| Tokens | Full 236-post rewrite ≈ several million all-in. CONSOLIDATE + PRUNE collapse most of it. |
| Scaled-content risk | 236 uniformly-generated posts recreates the exact signal we're fixing. Vary structure per post, not just variables. |

---

## Phase 5 — Intent gaps (new content, only after 1–4 land)

- **Owner financing.** Ranking pos 23–30 today with *zero* content on the subject
  (`owner financing homes for sale bloomington` 5 impr @23.4, +3 related queries). Cheapest available win.
  Open question first: are those queries Bloomington **MN** or **IN/IL**? Resolve before writing.
- **Flat-fee-MLS city tier.** `flat fee mls miami` is the single biggest query (40 impr) and there is
  **no dedicated city page anywhere in the network** — `flatfee-hub` is state-only (`/states/[state]`,
  no city routes). Decide: add a city tier to flatfee-hub, or own it from fsbo-hub. Don't build both.

---

## Phase 6 — Verify & measure

1. Full rebuild; re-run audit; diff vs the 07-26 baseline. **Gate: zero new defects.**
2. Resubmit sitemap; GSC URL Inspection on the 5 target pages.
3. Re-export GSC at **+14d (~08-10)** and **+30d (~08-26)**, save to `tools/seo/baseline/`, diff
   against the committed baseline. Align the +30d check with the existing mid-Aug checkpoint.

---

## Execution order (non-negotiable)

```
0 → 1 → 2 → 3 → 4 → 5 → 6
```
Phases 2 and 3 both edit `suburbs.ts`; **2 before 3** so title formulas can use corrected data.
One commit per phase minimum. Never bundle.

## Estimated effort

| Phase | Effort |
|---|---|
| 0 Baseline | 30 min |
| 1 Linter | 2–4 h (the investment that pays for everything else) |
| 2 Data fixes | 2–3 h |
| 3 Templates | 3–4 h |
| 4 Tier A blogs | 1–2 days |
| 4 Tier B decision | 3–4 h |
| 5 Intent gaps | 1 day |
| 6 Verify | 1 h + 30d wait |

## What NOT to do

- **Don't write content before the linter runs.** That's how the last three passes fixed the wrong things.
- **Don't hand-edit 779 suburb pages or 236 posts.** Everything at template/data level first.
- **Don't touch the 25-subdomain → subdirectory consolidation question.** Still parked, still unrelated.
- **Don't expect movement inside 14 days.** Position has been flat at ~34 for three weeks; that's the
  baseline to beat, and re-checking sooner will just produce noise.

## Tomorrow's first three commands

1. Copy the GSC CSVs out of temp into `tools/seo/baseline/2026-07-26/` and commit.
2. Scaffold `tools/seo/audit.mjs` with the Phase 1 check list.
3. Run it, commit `audit.json`, and read the ranked defect report **before touching anything else.**
