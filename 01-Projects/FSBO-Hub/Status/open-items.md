---
type: status
project: FSBO-Hub
last-verified: 2026-09-10
---

# ByOwnerHub Network — Open Items

*Verified current 2026-09-10 — vault-sync: **no repo activity network-wide since 2026-09-05** (`git log --all --since` empty across every repo). Nothing shipped, nothing new committed or pushed. **Correction:** the 🔴 "plaintext GitHub PAT in `fsbo-freemium-sandbox/deploy_freemium_branch.ps1`" item (below, 2026-07-23) is **resolved on disk** — that file was rewritten 2026-08-26 to remove the hardcoded PAT and read `$env:GH_TOKEN` from an encrypted SecretManagement vault. It was part of a 2026-08-25/26 credential overhaul (9 tokens flagged "burned", encrypted `ops` vault, global secret-blocking pre-commit hook, ops scripts moved out of the Obsidian vault) — see updated item and [[network-status]]. Provider-side rotation of the 9 tokens still shows pending in the ops-scripts README, not verifiable from here. Ties to [[vault-credential-exposure]]. The 09-07 weekly-audit findings below are unchanged and still awaiting triage/approval.*
*Previously: 2026-09-07 — weekly link audit ([[link-audit]]): 32 new failures reported → 6 real. 24 are fsbo internal `??` false positives (transient, all live-verified 200 — count inflated by an `audit.mjs` OOM this run). **Real:** 5 external 404s (eForms TN purchase-agreement PDF → replacement found `eforms.com/purchase-agreements/tn/`; 4× Redfin "recently sold" deep links — fix pattern or allowlist; `mohousing.com/homeownership/` → needs current MHDC page) + the recurring `insurance.ohio.gov` `ohio.gov`-family geo-block (still unactioned since 09-01). Ambiguous: `texas.gov` root 404 from this machine (likely geo). **Real stale deploy:** `auction.byownerhub.com` serves `main`; `origin/master` is 7 P3b/P8-SEO commits ahead and not live — clean FF verified. Mirror-branch drift now 22 repos, 3rd weekly run standing, all clean FFs, mostly cosmetic. New 🔴 section below. See [[network-status]].*
*Previously: 2026-09-05 — vault-sync re-run: one more commit closed out the 09-03/04 sprint on both fsbo product repos — `feat(nav): surface the deadline tracker from the homepage and nav` (production `22b2643` → `4bf79a7`, staging `6441f7e` → `cb86a99`, both pushed, both dated 2026-09-04 evening). Adds a `/under-contract` state index, a homepage card, nav links, and the sitemap entry — closes the follow-up item below about the under-contract route being orphaned from `sitemap.ts`. See [[network-status]]. No other repo moved: fsbo-hub `main` still `e659fd1`, car-by-owner still `ba17a8d`, both in sync; buyer-hub's uncommitted `tools/network-audit/` files are still the 2026-09-01 run. Unchanged open: `freemium-wip` 11 unpushed, unrotated PAT (~44 days), mirror-branch drift ~21 repos.* one more commit closed out the 09-03/04 sprint on both fsbo product repos — `feat(nav): surface the deadline tracker from the homepage and nav` (production `22b2643` → `4bf79a7`, staging `6441f7e` → `cb86a99`, both pushed, both dated 2026-09-04 evening). Adds a `/under-contract` state index, a homepage card, nav links, and the sitemap entry — closes the follow-up item below about the under-contract route being orphaned from `sitemap.ts`. See [[network-status]]. No other repo moved: fsbo-hub `main` still `e659fd1`, car-by-owner still `ba17a8d`, both in sync; buyer-hub's uncommitted `tools/network-audit/` files are still the 2026-09-01 run. Unchanged open: `freemium-wip` 11 unpushed, unrotated PAT (~44 days), mirror-branch drift ~21 repos.*
*Previously: 2026-09-04 — daily inbox digest ([[daily-digest]]): quiet day, 1 actionable, no new open items. The 2026-09-02 Bitwarden new-device login from a Brazil IP is **still unresolved** — no confirmation from Kevin or Pierre two days on; 🔴 item below unchanged. WillMaker/Nolo (🔴 below): Pierre replied 09-03 with traffic context + placement pages and answered a follow-up about the Trust & Will listing ("not partnering currently… can remove it") — the item's action is now done, awaiting Paul Ji's response; may need to drop the Trust & Will link from fsbo / divorce-hub if they require it. Worth knowing: Empathy (post-loss / estate-settlement support platform) sent a partnership follow-up — Pierre registered interest and they want a call; someone signed up for Umami Cloud analytics (supersedes the long-stalled Plausible plan); the Carfax car-by-owner thread is still unanswered on our side since 2026-06-26; Alison/Awin invite declined (closed).*
*Previously: 2026-09-03 — vault-sync re-run: no repo activity since the 2026-09-02 "positioning + commission" sprint. Full-network scan confirmed fsbo-freemium-sandbox `c2bb429`, fsbo-staging `f3ce1c8`, fsbo-hub `main` `e659fd1`, car-by-owner `ba17a8d` all in sync with origin.*
*Previously: 2026-09-03 — daily inbox digest ([[daily-digest]]): two new 🔴 opened. (1) Unexplained Bitwarden new-device login on 2026-09-02 from an IP (`187.14.51.59`) that geolocates to Brazil — not Kevin (US) or Pierre (Mulhouse FR); verify or treat as vault compromise. (2) WillMaker/Nolo (Internet Brands, CJ PID 101755238) publisher application has a live info request outstanding (site-visit stats + placement URLs) — reply needed to keep it alive. Worth knowing: Alison/Awin invite declined by K+P (reply sent); Impact.com login alert = Pierre's Mulhouse location; Carfax partner thread resurfaced with no new message, ball in our court since 2026-06-26; Rakuten Advertising activation still pending.*
*Previously: 2026-09-02 — daily inbox digest ([[daily-digest]]): FlexOffers affiliate reapplication came back **declined** (Pierre hit "application ... has been declined" in `#all-byownerhub-re` 09-01; Kevin: "I think we were declined"). One new 🔴 item opened below. Also worth knowing: LandlordHub "Get State Lease Forms" bug confirmed fixed site-wide by Pierre (Kevin's 08-31 old-code fix); CycleTrader Partners application submitted (pending); Rakuten Advertising login-activation email seen. Weekly audit 09-01 already logged in the line below.*
*Previously: 2026-09-01 — weekly link audit ([[link-audit]]): no real link rot. 7 new failures reported, 0 real — 6 transient `??` false positives (all live-verified 200), 1 known `ohio.gov` geo-block (`insurance.ohio.gov` OH page; fine for US visitors — recommend allowlisting it next interactive session). No 🔴 link item opened. Resolved since 08-24: `landlord.byownerhub.com` fully back (51 pages + sitemap, was 1-page/NO-SITEMAP stale Netlify snapshot); 08-24 orphan sitemap gaps confirmed closed. NOT resolved: mirror-branch drift still ~21 repos (same set as 08-24 + buyer/estate/funeral) — persisted across two weekly runs, cosmetic per [[network-audit-automation]] but worth a batch sync. Slack posting resumed this run (Kevin's in-session call, overriding the 2026-07-26 "Slack off") — parent + 3 replies in `#network-audit-results` thread `1788266323.222339`, awaiting approvals.*
*Previously: 2026-08-27 — daily inbox digest: Buildium affiliate application accepted via Impact (no terms in the email). One new 🔴 item opened. Stripe key-roll notifications on 08-26 look intentional (map to existing open items), no new item.*
*Previously: 2026-08-26 — production checkout had been returning 500 to every visitor since at least 08-04: the Stripe key ID was set instead of the secret key. Fixed and redeployed. Two new 🔴 items opened (deploy-context key sharing, unverified live webhook endpoint).*
*Previously: 2026-08-25 — see [[SESSION-2026-08-25]]. Network-wide OG-image fix landed (5 repos). Production (fsbo-freemium-sandbox) shipped a build-pipeline fix explicitly noted as having blocked switching to live Stripe keys — new 🔴 item below asking Kevin to confirm. fsbo-staging caught back up on refund/resume, now re-building the AI-crawler fix independently.*
*Previously: 2026-08-24 — weekly link audit ([[link-audit]]): 21 new failures, 11 real (orphan sitemap gaps on buyer/divorce/estate/funeral-hub), 3 real external 404s (2 with replacements found), 7 false positives, 155 resolved. Mirror-branch drift jumped 0→19 repos, worth a look. See 🔴 section below.*

---

## 🔴 Open — network audit (2026-09-07 run), see [[link-audit]]

- **auction-hub stale deploy (REAL).** `auction.byownerhub.com` live serves `origin/main`; `origin/master` is 7 commits ahead with P3b/P8 SEO (title/desc SERP-width trims, state-page content ~185→~332 words, Organization/WebSite/CollectionPage JSON-LD) — **not live**. Clean FF verified (`main` strict ancestor of `master`). Fix: FF `main` → `origin/master` (`git push origin origin/master:main`), or CF Pages retry if it deploys from `master`. Also confirm auction-hub's intended prod branch — `new-build-hub` has the opposite drift yet already serves `master`, so the mapping isn't consistent.
- **Real external link rot** (not yet applied):
  - fsbo `/state-requirements/` → `eforms.com/images/2018/08/Tennessee-Assoc-of-Realtors-Purchase-Agreement.pdf` 404 → replace with `https://eforms.com/purchase-agreements/tn/` (verified 200); sweep sibling state PDFs on that page.
  - fsbo metro pages → 4× Redfin "recently sold" deep links 404 (`/albany/`, `/anchorage/`, `/atlanta/`, `/bakersfield/`) — `include=sold-3mo` filter / `/recently-sold` URL scheme looks dead; Redfin also bot-gates (202). Verify from US, then fix the metro-template link pattern or add `www.redfin.com` to `allowlist.json` `bot_blocked_hosts`.
  - firsttimebuyer `/missouri/first-time-buyer-guide/` → `mohousing.com/homeownership/` 404 (root 200) — needs the current MHDC first-time-buyer / First Place Loan page.
- **`insurance.ohio.gov` geo-block** — recurring 3rd run, still unactioned: add to `allowlist.json` `geo_blocked_404_hosts` + `node audit.mjs --update-baseline`. Fine for US visitors.
- **`texas.gov` / `www.texas.gov` root → 404 from this machine** (land-hub TX page) — ambiguous, likely Akamai geo like `ohio.gov`. Verify from US; allowlist if geo, else swap in a live TX portal link.
- **Mirror-branch drift: 22 repos, unchanged, 3rd weekly run standing.** All clean FFs. 18 are `main`-ahead (deploy-from-`main`, cosmetic); buyer + foreclosure `master`-pinned (cosmetic); auction stale (above); new-build `main`-lagging but live=`master` (cosmetic). Needs a directional per-repo batch resync — no single push fixes all 22.
- **Slack**: post attempted to `#network-audit-results` this run (thread `1788266323.222339`) — see session log for connector auth status.
- Full report: `buyer-hub/tools/network-audit/report.md` + `results.json` (modified-but-uncommitted in the working tree; not yet triaged/applied — action next interactive session or via the Slack-approval execute routine).

## 🔴 NEW 2026-09-03 — Bitwarden new-device login from a Brazil IP (verify or treat as vault compromise)

Source: two emails to `byownerhubadmin@gmail.com` on 2026-09-02 ~09:52 UTC from
`no-reply@bitwarden.com` — *"Your Bitwarden Verification Code"*, then 17 seconds later
*"New Device Logged In From Chrome Extension"*. The device was new; the source IP
`187.14.51.59` geolocates to Brazil (Telefônica/Vivo) — not Kevin's usual US location and
not Pierre's France (Mulhouse) location. The email-OTP challenge was cleared within seconds,
so whoever authenticated also had access to the `byownerhubadmin` inbox at that time.

**Why it matters:** Bitwarden is the network's password vault — the maximum-blast-radius
account. [[vault-credential-exposure]] tracks 9 exposed tokens (4× Cloudflare, 4× GitHub,
1× Netlify) that were scrubbed from disk by 2026-08-26 but whose **provider-side rotation
still shows pending** in the ops-scripts README. An unexplained vault login from an
unexpected country is the trigger to act on, not wait out.

**Recommended action:**
1. Kevin/Pierre confirm whether either of them — or any automated tooling — logged into
   Bitwarden via a Chrome extension on 2026-09-02.
2. If not confirmed: change the Bitwarden master password, deauthorize all sessions
   (web vault → Account Settings → Deauthorize Sessions), verify 2FA is enabled, and rotate
   the highest-value secrets stored in the vault (the tokens tracked in
   [[vault-credential-exposure]] are already overdue).
3. Record the outcome here either way.

## 🔴 NEW 2026-09-03 — WillMaker (Nolo / Internet Brands) publisher application needs a reply

Source: email from `paul.ji@internetbrands.com` (2026-09-02), *"Re: WillMaker publisher
application — Byownerhub.com LLC (CJ PID 101755238)"*. The publisher is asking (a) how many
site visits our sites generate and (b) the URLs where WillMaker / Nolo products would be
listed, before advancing the application.

This is the *"Nolo (120-day cookie!) — fsbo, divorce"* line in Affiliate Enrollments → By
Program moving forward — not a duplicate, it's a live application with a specific info
request outstanding that goes cold without a response.

**Recommended action:** Pierre replies with network traffic figures (or a representative
subset — fsbo + top hubs) and the specific pages where Nolo/WillMaker links would sit (fsbo
state guides, divorce-hub). Update the Nolo line once enrolled.

**Update 2026-09-04:** Pierre replied on 09-03 — sent the traffic context (network is new this
year, volume modest but growing, content-first) and placement pages, then answered a follow-up
from Paul Ji about the Trust & Will listing on the site ("not partnering with them currently…
we can remove it if necessary to allow us to join"). The outstanding info request is now
answered; **ball is in Paul's court.** Next possible action on us: pull the Trust & Will
link/CTA from fsbo and divorce-hub if Internet Brands makes that a condition of approval.
Keep this open until the application resolves (accepted / declined).

---

## 🔴 NEW 2026-09-02 — FlexOffers reapplication was declined

Source: `#all-byownerhub-re` Slack, 2026-09-01. Pierre logged into FlexOffers and got
*"The application matching this email address has been declined. If you have any questions,
please contact support@flexoffers.com."* Kevin: *"I think we were declined by flexoffers."*
Pierre's theory: possibly too many application attempts on the same email. He notes some of
those advertisers appear reachable via Impact instead.

FlexOffers was carried in the Affiliate Enrollments backlog below as *"⚠️ Reapplication needed:
email support@flexoffers.com (sites now live)"* — this updates that status from "reapply" to
"reapplied → declined."

**Recommended action:**
1. Email `support@flexoffers.com` asking the decline reason and whether re-application is
   possible (mention the multiple-attempts theory; a single fresh application from a clean
   email may be the fix).
2. In parallel, inventory which FlexOffers-only advertisers the network actually wanted and
   check for the same programs on Impact or CJ; re-route those rather than waiting on FlexOffers.
3. Update the FlexOffers line in Affiliate Enrollments → Priority Applications once resolved.

## 🔴 NEW 2026-08-27 — Buildium affiliate application accepted (Impact), no terms recorded yet

"Welcome to Buildium!" from `notifications@app.impact.com` (2026-08-25) confirms Buildium accepted
the affiliate application. Buildium was a **pending** program in the Affiliate Enrollments backlog
below (targeted at landlord-hub and str-hub). The acceptance email contains **no commission terms** —
it only instructs logging into Impact and adding creatives. Program managed by Gen3 Marketing
(`buildium@gen3marketing.com`); Impact IDs referenced: 2017129 / 10839.

**Recommended action:** log into the Impact dashboard, record actual payout terms (CPA vs revshare,
cookie window), then place Buildium tracking links ("Schedule a Demo" / "14-day trial") on
landlord-hub and str-hub. Move Buildium from "By Program (pending)" to "Enrolled" in this file and
update [[affiliate-stack]].

## ✅ Resolved 2026-08-26 — production checkout was 500ing; the Stripe key *ID* had been set, not the key

**Root cause:** Stripe's dashboard shows each API key with an identifier (`mk_1Tvaj…`) next to
the secret (`sk_live_…`). The **ID** was pasted into `STRIPE_SECRET_KEY` in Netlify, so every
`checkout.sessions.create` returned **401 StripeAuthenticationError — "Invalid API Key provided:
mk_1Tvaj…"**. Every visitor clicking the $99 button got "Failed to create checkout session".
Live keys were therefore never working in production, despite being "set".

**Why it hid for three weeks:**
- The route's `catch` returned a generic string, leaking no cause to the browser.
- **Stripe's request log showed nothing.** An unrecognised key can't be attributed to an account,
  so the 401s never appeared under our logs — last entry was 2026-08-04. This is the misleading
  part: an empty Stripe log looked like "no traffic", not "auth failing".
- The 08-25 manual redeploy was **skipped** by the build guard — it rebuilt 08-23's commit
  (`33c0ef2`) in an identical 94s. The guard fix (`f955716`) only shipped at 08:28 that day.

**Found** 2026-08-26 in the **Netlify function log** (`Stripe checkout error:`), which had been
recording the full exception all along. **Fixed** by setting the real `sk_live_…` and redeploying;
three genuine 87–95s builds ran on 08-26, which also confirms manual redeploys now build properly.

> **Lesson:** if a Stripe call fails and *nothing* appears in Stripe's request log, the request
> never reached Stripe. Look at the server log, not the Stripe dashboard.

## 🔴 NEW 2026-08-26 — Stripe key is shared across all Netlify deploy contexts

`STRIPE_SECRET_KEY` holds one value for Production, Deploy Previews, Branch deploys, and Preview
Server & Agent Runners. With a live key that means **any preview or branch deploy can take real
payments** — and fsbo-staging exists precisely to test checkout. Split it: `sk_live_` on
Production only, `sk_test_` on preview contexts, Local left empty (`.env.local` supplies it).
Same for `STRIPE_WEBHOOK_SECRET`, which is a different value per mode.

## 🔴 NEW 2026-08-26 — confirm a live-mode Stripe webhook endpoint exists

**Not yet verified.** Webhook endpoints do not carry over from test mode, and server-side checkout
never worked in live mode until today — so the live endpoint may never have been created. Without
it, payments succeed and entitlements never grant: the customer pays $99 and gets nothing. Check
dashboard.stripe.com/webhooks for an endpoint targeting
`https://fsbo.byownerhub.com/api/stripe/webhook` handling `checkout.session.completed` and
`charge.refunded`, and confirm `STRIPE_WEBHOOK_SECRET` matches that endpoint's signing secret.

## ✅ Resolved 2026-08-25 — network-wide OG-image 404s (55plus/boat/closing/condo/investor-hub)

`opengraph-image.tsx` routes in these 5 repos 404'd under static export (Search Console flagged it; social shares showed broken previews). Two-pass fix: removing `runtime = "edge"` (08-21) didn't work — static export can't generate `ImageResponse` images at all — so the routes were deleted (08-23), falling back to each site's existing `og-default.png`. Swept the rest of the network for the same pattern: only one other hit, a dead `flatfee-hub/.../opengraph-image.tsx.bak` file, not live. Rollout complete, all pushed.

## ✅ Resolved 2026-08-25 — fsbo-freemium-sandbox SEO/content fixes (production, pushed)

- **AI-crawler robots.txt block added** (`1cd6b5c`) — this Netlify-hosted site was the only one in the network not blocking AI-training crawlers (the other ~39 get it free from Cloudflare's managed robots.txt); now blocks the same nine bots the rest of the network does.
- **Broken homepage `SearchAction` removed** (`1cd6b5c`) — pointed at a search route that never existed; Google was crawling the literal `{search_term_string}` template and logging 404s in Search Console.
- **22-state blog-index 404s fixed** (`33c0ef2`) — `/{state}/blog` was never generated for states with no metro hub, only the individual `/{state}/blog/{slug}` posts; now redirects to the state guide.
- **Boston offer-terms FAQ split** (`33c0ef2`) — one dense Q&A (Use & Occupancy / cash offers / PMI) split into three, each with its own FAQPage schema entry.

## ✅ Resolved 2026-08-25 — fsbo-staging caught up on refund/resume commits

No longer "3 commits behind production" as of 08-21 — staging's `master` now has the refund-revocation/resume feature and the refund-guarantee-loophole fix. Still 2 behind (the state-blog fix and the build-skip fix above), and separately has an **uncommitted** local edit re-implementing the AI-crawler/SearchAction fix (`1cd6b5c`) independently — same dev-first pattern as previous sessions, not yet committed on staging.

**⚠️ CORRECTION, 2026-08-19 PM (Pierre's live re-check + verified here):** two items marked "resolved/pushed" earlier this session are NOT actually live. See new 🔴 section immediately below — this supersedes the "Other pushed fixes this period" note further down for car-by-owner and landlord-hub specifically. boat-hub IS confirmed clean live (verified Ohio/Arizona/New Hampshire match source).

---

## ✅ Resolved same day — network audit (2026-08-24 run) actionable items

- **11 orphan sitemap gaps** on buyer-hub, divorce-hub, estate-hub, funeral-hub — `/disclaimer`, `/privacy`, `/terms` route files existed and were live but never registered in `sitemap.ts`. Fixed, build-verified (generated `sitemap.xml` confirmed to include the new URLs), and pushed: buyer-hub `1d4ca22`, divorce-hub `dc5b74d`, estate-hub `ae62d2a` (only needed `/disclaimer`+`/terms`, `/privacy` was already there), funeral-hub `5137ac1`.
- **2 real external 404s, replacements applied**: firsttimebuyer-hub's California guide — CalHFA reorganized its URLs, `calhfa.ca.gov/homeownership/programs/myhome.htm` → `calhfa.ca.gov/homebuyer/programs/myhome.htm` and `calhfa.ca.gov/dreamforall/` → `calhfa.ca.gov/dream/`. Fixed, build-verified, pushed `fca7e3f`.
- **1 real external 404, still open, no replacement found**: `insurance.ohio.gov/consumers/homeowner/homeowners-insurance-guide` (insurance-hub OH page) — the entire insurance.ohio.gov domain is currently 404ing, looks like an agency-side migration in progress. Re-check next cycle.
- **7 false positives** (fsbo suburb pages ×4, land state pages ×3) — crawler logged transient `??` status, not real 404s; all live-verified 200. No action needed, should self-clear next run.
- **Mirror-branch drift jumped 0 → 19 repos** (was a clean 0 as of 08-18), still open — not touched by this fix pass: frbo, commercial, firsttimebuyer, flatfee, biz, mobile, lien, llc, timeshare, inspection, trust, rv, eviction, moto, str, mortgage, new-build, foreclosure, auction. Note: firsttimebuyer-hub's CalHFA fix above pushed to `main` only, so its drift with `master` is now 1 commit wider. Likely cosmetic (main is the deployed branch per [[network-audit-automation]]) but the size of the jump is new — worth a look before assuming it's fine everywhere. FF-safety not yet verified.
- **Slack posting skipped** (connector unauthenticated in this session, and Kevin turned off all Slack integrations 2026-07-26 — see [[bugs-feature-routines]]).

---

## ✅ Resolved 2026-08-20 — car-by-owner CF Pages build was failing outright (not just stale)

Follow-up on the 2026-08-19 "not live" finding below: car-by-owner turned out to have **migrated to Cloudflare Pages** at some point (contradicts older memory calling it Netlify — a stale `netlify.toml` was still sitting in the repo unused, same landmine class as landlord-hub's pre-07-23 issue). Kevin pulled the CF Pages build log, which showed the actual cause: every deploy was failing at `npx @cloudflare/next-on-pages` with an ERESOLVE conflict (next-on-pages@1.13.16 wants `@cloudflare/workers-types` ^4.x, auto-installed wrangler@4.124.0 wants ^5.x as peer) — neither pinned in package.json, so both resolve fresh at build time and collide. **Identical root cause to str-hub's `23ce82d` (2026-08-05).** Fixed the same way: added `.npmrc` with `legacy-peer-deps=true`, dropped the stale `netlify.toml` (`5e7e030`). Build succeeded, deploy went live within ~2 min. **Live-verified all previously-flagged items now correct in production**: GA T-7 form page (`/states/georgia/t-7-bill-of-sale`) 200 with correct dor.georgia.gov link, MA/ND/SD/WI/WY/TX/OK/MS/MT dmv links all match fixed source, Illinois duplicate "Official state form" link confirmed gone (form-guide section intact). This closes out car-by-owner's half of the item below — **only landlord-hub's DNS issue remains open.**

## ✅ Resolved 2026-08-20 — landlord-hub DNS cutover finally complete

Root cause was two-layered, both fixed by Kevin directly in the Cloudflare dashboard this session:
1. **DNS**: `landlord.byownerhub.com` CNAME was still pointed at `byownerlandlordhub.netlify.app` (DNS only/grey-cloud) — the dead Netlify site, serving a ~68-day-stale cached snapshot from before landlord-hub ever moved to CF Pages. Fixed by editing the record to target `landlord-hub.pages.dev` with Proxy status = Proxied.
2. **CF Pages Custom Domain registration** (the actual [[byownerhub-network-layout]] "canonical-domain cutover trap" — the part that never held from the 07-23 attempt): a proxied DNS CNAME alone wasn't sufficient — Cloudflare's edge didn't know to route `landlord.byownerhub.com` to the `landlord-hub` Pages project without it being registered on the project's own Custom Domains tab, which produced a 522 (edge-to-origin timeout) even after DNS was corrected. That tab only had `forrent.byownerhub.com` (Active) and a bogus, never-resolving `landlordhub.byownerhub.com` (stuck "Verifying" since 07-23 — recommend deleting, violates the no-"hub"-in-subdomain naming rule and nothing points to it). Added `landlord.byownerhub.com` there directly; verified within minutes.

**Live-verified all 50 states** against the fixed source (`ecb8876`): zero mismatches, every "Get [State] Lease Forms" link now resolves to the correct ezlandlordforms.com URL. Confirmed via direct browser click-through earlier the same day that this was broken ("Page Not Found | ezLandlordForms") before the fix, then reconfirmed working after.

**Process lesson for the next canonical-domain cutover**: DNS CNAME + Proxied status is necessary but not sufficient for a CF Pages custom domain — always also check/add the hostname on the Pages project's own Custom Domains tab, or it'll 522 even with correct DNS. This closes the item below fully — car-by-owner's half closed 2026-08-20 (see above), landlord-hub's half closed here.

## 🔴 STR-hub, boat-hub bug lists — CONFIRMED RESOLVED live (2026-08-19)

Cross-checked Pierre's full 2026-07/08 bug dump (STRHub 8-city permit 404s, BoatHub 16-state agency/lien-search links, CarHub DMV links, LandlordHub lease forms) against git history and live production:
- **str-hub**: all 8 flagged cities (NYC, LA, SF, Chicago, Miami Beach, Nashville, Denver, Seattle) fixed in `481f923`/`fa640b8`. Matches Pierre's own "all fixed now" note.
- **boat-hub**: all 16 flagged states fixed in `f4fbdb5`, live-verified (Ohio, Arizona, New Hampshire spot-checked, match source exactly).

---

## 🔴 Open — network audit (2026-08-18 run), see [[network-status]]

- **New**: `stlouiscountymo.gov/.../assessor/` 404 on fsbo-hub's `/st-louis/` page — not yet applied.
- **Recurring, may not be a false positive anymore**: `dph.illinois.gov/topics-services/birth-death-other-records.html` (funeral-hub Illinois) and `idoi.illinois.gov/consumers/consumerinsurance/homeownerrenter.html` (insurance-hub Illinois) — both were dismissed as crawler flukes in the 07-27 and 08-05/06 runs after manual verification found them live; now failing a third time across two different sites. Worth a fresh manual check before dismissing again.
- **Confirmed still live**: the already-tracked `nrec.nebraska.gov/pdf/forms/SPCD.pdf` fsbo stale-deploy 404 (see item below) — the crawler independently found it broken on 9 fsbo pages including `/omaha/`, `/new-orleans/gretna/`, `/omaha/papillion/`.
- **✅ Mirror-branch drift: 23 repos (08-05/06) → 0 (08-18).** No stale-deploy pairs detected this run — first clean drift check in the audit's history.
- str-hub homepage's dead `solar.byownerhub.com` link is expected/known (item 2 below, solar hosting never stood up) — not a new issue, confirms it's still broken.
- Full report: `buyer-hub/tools/network-audit/report.md` (sitting modified-but-uncommitted in the repo working tree as of this update, not yet triaged/applied — action next interactive session).

## 🔴 Open — network audit (2026-08-05/06 run), see [[link-audit]]

- **5 real dead external links** with verified-live replacements found (jccal.org Birmingham revenue, mecknc.gov Charlotte assessor, mcohio.org Dayton auditor, hennepin.us→hennepincounty.gov Minneapolis property map, mdot.maryland.gov→dnr.maryland.gov MD boat registration — the last one was pointed at the wrong agency entirely, not just link rot). Not yet applied — action next interactive session.
- **Real content bug, fsbo-hub**: `/new-orleans/gretna/` (Gretna, LA) shows an incorrect "Omaha FSBO Transaction Forms" section citing Nebraska disclosure law — a suburb-slug collision in `forms.ts`'s flat alias map (`'gretna': 'omaha'`), same bug class as the earlier Columbus-OH/GA collision but a different data structure that fix didn't cover. Legal-accuracy issue, needs Kevin's call on fix pattern.
- **fsbo-hub stale deploy (Netlify)**: production still serves a `nrec.nebraska.gov` SPCD form URL that was fixed in source 2026-07-23 (`dc0cf79`) — build is >2 weeks stale on at least this file. Worth a fresh push/redeploy check.
- **str-hub Nashville STR link** — already fixed, just sitting in the 9 unpushed `master` commits noted below.
- 6 reported failures were false positives (transient crawler errors), verified live: `dph.illinois.gov`, `idoi.illinois.gov`, and 4 fsbo suburb pages.
- Mirror-branch drift jumped to **23 repos** (was 4-6 in recent runs) — tail of the SEO remediation project's heavy `main`-only pushes. Batch sync needed, not verified FF-safe per-repo yet.
- Not new, unchanged: **landlord.byownerhub.com** sitemap/robots still 404 (stale Netlify build, awaiting Kevin's DNS-cutover decision).
- **Slack posting skipped** (connector unauthenticated in this session, and Kevin turned off all Slack integrations 2026-07-26 — see [[bugs-feature-routines]]). All proposals are in [[link-audit]] for direct action instead.

## ✅ Resolved 2026-08-21 — str-hub `master`'s stale backlog got pushed

The 9-commit, 15-day-stale `master` backlog (SEO P3b/P7/P8 + a same-day STR-permit-link fix batch, most recent commit still 2026-08-04) is now pushed — `master` is in sync with `origin/master`. No new commits landed; it was simply pushed. Closes an item carried across four vault-sync sessions.

## 🔴 NEW 2026-08-21 — fsbo-freemium-sandbox (production) shipped a feature sprint

08-19/20: metro/suburb pages redesigned into a 4-step revealed tool; a mobile-overflow bug and a suburb-checklist state-specific-items bug both fixed; a same-day production incident (fail-closed robots guard shipping `Disallow: /`) caught and fixed; two new entitlement features — **refund revocation** via Stripe `charge.refunded` webhook, and **passwordless cross-device resume** (email-a-link workspace restore); a refund-guarantee loophole closed (refundable only until first download, was previously refundable regardless); a Netlify build-cache fix. All pushed, all live. Full detail: [[SESSION-2026-08-21]].

- [ ] **Verify `RESEND_API_KEY` is set on production** — the new resume-link email silently no-ops without it (saves succeed, reports `emailed:false`).
- [ ] **Verify Stripe's `charge.refunded` webhook event is actually subscribed to** in the Stripe dashboard — the revocation code assumes it fires; if the event isn't subscribed, refunds won't revoke access.
- **fsbo-staging is now 3 commits behind production** — has the redesign (independently re-implemented, same messages/different hashes — the intended dev-first workflow) but not the 3 newest commits (refund revocation/resume, refund-guarantee fix, build-cache fix). Not urgent, staging never serves a live domain.

## 🔴 STILL unpushed as of 2026-09-02 — fsbo-hub `freemium-wip` unchanged

- **fsbo-hub `freemium-wip`** — still 11 commits ahead of `origin/freemium-wip`, unchanged since 08-05. Deploy-readiness still not re-verified since the 07-12 check — now ~8 weeks and seven vault-check sessions running. Note: this branch is increasingly moot — production's real freemium/Stripe build lives in `fsbo-freemium-sandbox` and has already shipped checkout + refunds + entitlement (see above). Worth asking Kevin whether `freemium-wip` should just be abandoned. See item 8 below.
- ~~**fsbo-hub `main` has a new uncommitted edit** — `src/components/Hero.tsx`~~ **RESOLVED 2026-09-02** — committed + pushed as `e659fd1` ("drop the metro hero CTAs and tighten the spacing") after sitting uncommitted since 08-21. `main` in sync with origin, working tree clean.
- Full detail in [[unpushed-changes]].

## ✅ Resolved 2026-09-03/04 — "under-contract / contract-stage" sprint (fsbo product repos, pushed)

See [[SESSION-2026-09-03]]. Production (`fsbo-freemium-sandbox`) `master` `c2bb429` → `22b2643`, **18 commits, all pushed / in sync with origin** (15 dated 09-03, 3 dated 09-04). `fsbo-staging` `master` `f3ce1c8` → `6441f7e`, **17 commits, all pushed**, independently re-built (same messages, different hashes). Delivered:

- **Contract-stage model + workspace DeadlineTracker** (`a2b7c23`, `7f1e6af`, `1992ca5`, `b378865`) — persists into the saved paid-tier workspace.
- **Per-state under-contract pages** (`265968a`), linked from state guides + metros (`4698e84`).
- **State requirements matrix** route (`2b40b21`; `1acfb87` same-day coverage-claim correction).
- **Partner co-branding** — co-branded landing template (`1421805`) + `?ref=` carried through to the Stripe session and the `purchases` row (`4744791`).
- **Copy/routing** — attorney-state offer variant (`49f5f9d`), flat-fee → MLS-comparison handoff (`ef105ee`).
- **Cookieless analytics + three funnel events** (`eaa34a6`).
- **AI-route error handling** — `1ef9ecb` stopped the generic "AI service error" catch string; `22b2643` (09-04) then fixed the real cause of the 400s: a **missing `anthropic-workspace-id` header**. Same failure mode as the 08-26 Stripe key-ID incident.
- **Price tool** (09-04) — `fcd1487` stop requiring an optional metro, `b058de3` clear the error between steps.

**Follow-ups (need a human eye):**
- [ ] **Live-verify the AI tools** (listing-description, price-estimate) on fsbo.byownerhub.com — `22b2643` claims the `anthropic-workspace-id` header was the 400 cause.
- [x] ~~**Confirm the new under-contract + state-requirements routes are in `sitemap.ts` output** and not orphaned.~~ **RESOLVED 2026-09-04** — `4bf79a7` added the missing `/under-contract` sitemap entry (`/state-requirements` was already present) and gave both routes a path in from the homepage and nav, which they'd shipped without. See [[network-status]].
- [ ] **Confirm the `purchases` row tolerates `?ref=`** — the column exists in production Supabase and the webhook handler doesn't choke when `ref` is absent (non-referral purchases).

## ✅ Resolved 2026-09-02 — "positioning + commission" sprint (fsbo repos, pushed)

See [[SESSION-2026-09-02]]. Production (`fsbo-freemium-sandbox`) `master` `f955716` → `c2bb429`, 6 commits pushed: homepage **positioning module** + hero line **stating the free/paid split**; commission figures **derived from median price in one place** (`src/lib/commission.ts`), metro page **shows both figures instead of one ambiguous number** (retires a drifted `types` field); and `2feef13` **fix(stripe): log and surface the failure class on checkout errors** — the code follow-up to the 2026-08-26 key-ID incident (the generic catch string that hid a live-mode 401 for three weeks). `fsbo-staging` independently re-built the same set (`master` → `f3ce1c8`, 7 commits pushed) and committed its previously-pending AI-crawler/SearchAction edit (`1bf2a10`). `car-by-owner` shipped `ba17a8d` (page-level FTC disclosure above CTAs).

## ✅ Resolved (found no longer outstanding, 2026-08-21) — the 07-23 1-ahead items

A full-network branch-vs-upstream sweep (every local branch, not just main/master) found `timeshare-hub` and `trademark-hub`'s single unpushed contrast-fix commits (flagged 07-23) no longer show up as ahead of origin — resolved at some point between then and now, untracked when it happened. Dropped from open items.

## ✅ Resolved 2026-08-05, confirmed still resolved 2026-08-19

- **car-by-owner `main`** — the `b7b4286` commit flagged 08-05 plus two more DMV-link fixes (`8385113` WY, `ab3696c` MS/MT) are all pushed. Fully in sync with origin.
- **fsbo-freemium-sandbox staged WIP** — the PDF-toolkit feature flagged 08-05 as staged-but-uncommitted is now committed and pushed (`5888d28`, `294ed74`, both 2026-08-05).

## 🔴 Open — the lead-sale/sharing disclosure rollout looks incomplete

A "legal: disclose lead sale/sharing in privacy policy" commit landed in only 6 of ~39 repos (biz-hub, estate-hub, eviction-hub, fsbo-hub, moto-hub, str-hub) between 07-27 and 08-04. Unclear from commit history alone whether this is intentionally scoped to sites with active lead-gen/affiliate forms, or a partial rollout that stalled. Needs Kevin's call on whether the other ~33 repos need the same clause.

## ✅ Resolved — 2026-08-04 #bugs-channel batch

- **frbo-hub**: favicon 404 on every page fixed (`42520f2`) — dynamic icon route was incompatible with static export. This closes the 07-27 open item "own icon.tsx route 404s live" — it was a real bug, not a stale-deploy/cache artifact as first suspected.
- **eviction-hub**: dead South Carolina eviction self-help link fixed (`e005614`) — closes the 07-27 open item that had no replacement found at the time.
- **probate-hub**: Mississippi + Missouri court-finder links corrected (`3072604`, `9eb690c`, `4b1fdfc` — stale `.php` path 404s, falls back to homepage).
- **trademark-hub**: LegalZoom link was serving raw XML (dead S3 path) on homepage/FAQ/footer — fixed by dropping the dead `?via=byownerhub` affiliate param (`d16a238`, `09539ef`).
- **moto-hub**, **trademark-hub**, **probate-hub**: additional unspecified "bug fixes from #bugs channel 2026-07-30" batch commits.
- **biz-hub**: NDA checklist now delivers via instant download instead of an unconditional-success email flow (`fa07d6b`).
- **firsttimebuyer-hub**: "View guide" button overflow fixed on long HFA program names (`c4cc3db`).

## ✅ Resolved — network-wide SEO remediation project (2026-07-27 → 08-04)

Ran per [[seo-remediation-plan-2026-07-27]] across ~39 repos, driven by a new `buyer-hub/tools/seo-audit` linter/ledger. Phases: P1 locale-number-format (234→0), P2 title-duplicate criticals cleared, P3/P3a/P3b brand-title-template removal + differentiated titles (~1,380 defects cleared), P5 Organization+WebSite JSON-LD on all homepages, P7 meta-description SERP-width fixes (712→0), P8 thin state-page content expansion (554→28 thin pages, 95% reduction), plus HowTo/CollectionPage/FAQPage/BlogPosting+BreadcrumbList/ItemList JSON-LD added where missing, and a homepage title/desc overflow fix across 21 repos. Full narrative in [[SESSION-2026-08-05]] and [[network-status]]. **Note:** the plan itself (see [[seo-remediation-plan-2026-07-27]] header) flagged that fsbo is only 1.2% of network impressions and recommended prioritizing divorce/insurance instead — worth checking with Kevin whether that reprioritization happened or the phases just ran network-wide regardless.

## 🔴 Open — network audit (2026-07-27 run), see [[link-audit]]

- [x] ~~**boat-hub**: 2 dead state-gov links~~ **FIXED + PUSHED same session** (`407a357`) — MA boat registration → `mass.gov/orgs/boat-and-recreation-vehicle-registration-and-titling-bureau`, NH DMV → `dmv.nh.gov`. Both verified live in-browser and in the built static output before push.
- [x] ~~**Mirror-branch drift, 5 clean-FF repos**~~ **SYNCED same session** — firsttimebuyer-hub (`c4cc3db`), biz-hub (`74cb5f2`), estate-hub (`f4c40b8`), moto-hub (`def3007`), str-hub (`d04b60a`) all pushed `master` up to match `main`, re-verified clean FF immediately before each push.
- [x] ~~**eviction-hub**: SC eviction self-help page dead~~ **FIXED 2026-08-04** (`e005614`) — see resolved section above.
- [x] ~~**frbo-hub** (rent.byownerhub.com): own `icon.tsx` route 404s live~~ **FIXED 2026-08-04** (`42520f2`) — was a real bug (dynamic icon route incompatible with static export), not a cache artifact as first suspected. See resolved section above.
- [x] ~~**funeral-hub** — diverged branches~~ **MERGED + PUSHED same session** (`01e752e`) — no actual conflicts (different files: `data.ts` vital-records links vs. `layout.tsx`/`states/[state]/page.tsx` SEO trims), merged master into main, build verified clean, then pushed `main` and fast-forwarded `master` to match. Both branches now identical.
- Not new, unchanged: **landlord.byownerhub.com** sitemap/robots still 404 (stale Netlify build, awaiting Kevin's DNS-cutover decision) and **solar.byownerhub.com** hosting still not stood up (item 2 below).

## 🔴 Open — code tasks (2026-07-13 audit findings)

- [x] ~~External-link burn-down: 147 dead links~~ **DONE 2026-07-13 (same session)** — all fixed across 13 repos, every replacement verified live, pushed dual-branch: fsbo `01e822c` (TREC OP-H + 9 assessors), firsttimebuyer `dcd566e` (HUD reorg: /states/x_y/homeownership → /states/x-y, + 14 housing agencies), boat `a4fcb8a`, funeral `7d51444`, mobile `13f0c3e` (HUD manufactured-home-resources), probate `1d0db4b`, car `dd82fe5`, investor `bc2c848`, condo `d4c2d15` (entp.hud.gov condo lookup), biz `fd80e49`, land `5eaa42e`, inspection `de49000`, trademark `2a66040`. Dead `?via=` tags dropped where no live affiliate deal. EXCEPTIONS left as-is: ohio.gov / ohiodnr.gov / odh.ohio.gov / dps.mn.gov links — those hosts serve 404 to non-US traffic (verified in-browser), can't be validated from here; added to audit `geo_blocked_404_hosts`. Re-run `node audit.mjs --update-baseline` next interactive session after CF deploys settle.
- [x] ~~9 orphan pages missing from sitemaps~~ **DONE + PUSHED 2026-07-20** — fsbo `588daec` (unsubscribed, tools/listing-description, tools/price-my-home), condo `e4c4269`, investor `7bfaa09` (disclaimer/privacy/terms ×3 each). Also pushed same day: fsbo suburb-page Census enrichment (`a953599`), blog-index noindex (`bd6054d`), divorce-hub court-citation links for all 51 states (`6d5e617`, `d4ca46d`).
- [x] ~~RV title/meta rewrite (GSC rec #1)~~ **DONE + PUSHED 2026-07-21** — rv-hub `d7132b7`, state page title/meta rewrite + real FAQ content.
- [ ] KEY LESSON (build tooling): >6 parallel `next build`s on this machine exhausts worker threads (exit 3221226505 / os error 1450) — batch ≤4 or go serial. And `git add src app components` silently stages NOTHING if any pathspec is missing — add paths individually.

## ✅ Resolved (code-complete, not yet pushed) — 2026-07-20 fsbo GSC indexing fixes

- **Suburb pages enriched with real Census data** (`a953599`) — closes root cause in [[fsbo-suburb-thin-content]]: the intro generator only had 5 fields and 4 price-ratio buckets, producing near-identical prose at scale. Reversed the unused `ZIP_TO_SUBURB` map, extended it with 416 more real ZIP matches (GeoNames public DB), wired `getSuburbIntro()` to append real Census ACS facts (median household income, homeownership rate) per suburb ZIP. 688/779 suburbs (88%) now get differentiated content; the other 12% fall back to old copy. **Not pushed** — see [[unpushed-changes]].
- **Metro blog index pages always noindexed, still followed** (`bd6054d`) — GSC was flagging these navigational shells (title + 1-2 post links) as "Crawled - not indexed." Nobody searches "metro blog index," so no ranking value lost; still followed so link equity reaches the real posts. **Not pushed.**
- **3 orphan pages added to sitemap** (`588daec`) — `/unsubscribed`, `/tools/listing-description`, `/tools/price-my-home`. **Not pushed.**

## ✅ Resolved — parallel freemium/Stripe build on fsbo main (2026-07-23)

The 2026-07-20 discovery (uncommitted duplicate Stripe paywall build sitting on `main`) resolved itself by abandonment, not merge: `main`'s WIP (`src/app/api/stripe/*`, `checkout/success`, `checkout/cancel`) was never committed and no longer exists anywhere in `main`'s history or working tree (reflog shows no trace of it being added or discarded — it was evidently deleted from the working tree directly). `freemium-wip`'s original Stripe implementation (unchanged since `0a82f8d`, 2026-07-09) remains canonical. Today `main` was merged into `freemium-wip` (`0dbf67d`, clean, no conflicts) to fold in the real content fixes from both branches. **Net result: `freemium-wip` is now 9 commits ahead of `origin/freemium-wip`, unpushed — see [[unpushed-changes]] and [[SESSION-2026-07-23]] §3.** Its 2026-07-12 "deploy-ready" verification predates these 9 commits and should be re-run before relying on it for item 8 below.

## ✅ RESOLVED ON DISK 2026-08-26 — plaintext GitHub PAT in `fsbo-freemium-sandbox/deploy_freemium_branch.ps1`

**Original (2026-07-23):** the new `kevc55-code/fsbo-freemium-sandbox` repo (seeded from fsbo-hub's `freemium-wip` as an isolated Stripe sandbox) had an **untracked** `deploy_freemium_branch.ps1` with a **live-looking GitHub PAT in plaintext** (`ghp_v078...`). Correctly excluded from the git commit, but sat in plaintext on local disk. The vault then carried this as unresolved across ~6 weeks of sessions, repeatedly stating "file mtime unchanged since 07-23, not rotated."

**Correction (found 2026-09-10):** the file was **rewritten 2026-08-26** (mtime confirms; the "unchanged since 07-23" claim was wrong from that date on). The hardcoded PAT is **gone** — the script now does `. "C:\Users\kevc_\Documents\ops-scripts\_secrets.ps1"` and uses `$env:GH_TOKEN`, resolved at runtime from an encrypted PowerShell SecretManagement vault (`ops`), into the current process only. The other untracked script, `deploy.bat`, never held a token.

**Broader context — 2026-08-25/26 credential-hygiene overhaul** (`C:\Users\kevc_\Documents\ops-scripts\README.md`): a machine-wide scan found **9 credentials** exposed in never-version-controlled local scripts (plus the original vault commit): 4 Cloudflare tokens (consolidated onto `CF_API_TOKEN`; DNS-scoped one kept as `CF_API_TOKEN_2`), 4 GitHub credentials (2 classic PATs + 2 OAuth tokens, all → `GH_TOKEN`), 1 Netlify PAT (`NETLIFY_TOKEN`). All ops scripts rewritten to resolve tokens from the encrypted `ops` vault (nothing written to disk/registry). Scripts moved out of the Obsidian vault to `…\ops-scripts` (vault `.gitignore` now blocks `*.ps1`/`*.bat`/`*.zip`). Global pre-commit hook at `~/.githooks/pre-commit` (`git config --global core.hooksPath`) now blocks any commit containing a CF/GitHub/Netlify/AWS/Stripe/Slack token or private key, network-wide.

**Still open:** provider-side rotation. The ops-scripts README still instructs "rotate all nine at the provider" — whether that has happened is not verifiable from this machine. Tracked in [[vault-credential-exposure]]. See [[SESSION-2026-07-23]] §4 for the original find.

## 🔴 NEW — 4 repos with unpushed local commits (2026-07-23)

- **fsbo-hub `main`** — 1 ahead (`ef035bb`, welcome-email domain fix).
- **fsbo-hub `freemium-wip`** — 9 ahead (see resolved item above + [[unpushed-changes]] for full list).
- **timeshare-hub** — 1 ahead (`ec14573`, contrast fix, low risk).
- **trademark-hub** — 1 ahead (`6db6542`, contrast fix, low risk).

## 🔴 Open — network audit (2026-07-23 run), see [[link-audit]]

42 new failures (38 external 404s, 4 mirror-branch drift, all proposed/flagged in Slack `#network-audit-results` for approval). The 2026-07-20 run's open question is resolved: **inspection.byownerhub.com** sitemap failure was a crawler fluke (clean this run); **landlord.byownerhub.com** is a real issue — still served by a 31-day-stale Netlify build, not Cloudflare Pages as an unpushed local commit assumes. Flagged in Slack for Kevin's call, not auto-fixed. No `--update-baseline` run yet.

**Slack integration added this run:** channel `#network-audit-results` now gets the weekly proposed-fixes report; a new hourly cloud routine ("Network audit — execute approved fixes", routine `trig_015a8iarCgBYE6gZ9v3t8qEg`) watches it and executes anything Kevin approves in-thread (repo access via the `Claude_Code_Remote` connector's `add_repo`, so it can reach any of the 38 network repos on demand). The weekly `network-link-audit` scheduled task's SKILL.md was updated to post proposals there going forward.

## ✅ Resolved — 2026-07-21/23 citation-link content batch (pushed)

Same pattern across 4 repos — replaced generic prose with real state court/DOI citation links, in two passes each:
- **divorce-hub** `6d5e617`+`d4ca46d` (already logged 2026-07-20) — all 51 states/DC.
- **eviction-hub** `207d802`+`6109d90` — all 49 remaining states.
- **insurance-hub** `9e7bfb6`+`b5853fb` — all 50 states, also dropped a stale "2024" year claim.
- **trust-hub** `05758ca`+`ee60eed` — all 50 states, probate courts.

## ✅ Automation added 2026-07-13

- **Weekly network audit**: `buyer-hub/tools/network-audit/audit.mjs` (committed 9a2f630) + scheduled task `network-link-audit` (Mondays 08:30). Crawls all sites, checks internal/cross-site/external links, alias 301s, form CORS, orphan pages (repo routes vs sitemap), mirror-branch drift. Baseline-diff: only NEW failures alert; report → vault `FSBO-Hub/Audits/link-audit.md` (canonical; point-in-time snapshots go to `Audits/archive/`). Baseline seeded 2026-07-13 with 157 known failures. Interactive fixes should end with `node audit.mjs --update-baseline`.

## ✅ Resolved — 2026-07-13 Pierre's site review (all pushed, CF deploys in flight)

- **buyer-hub offer-letter guide enriched** (Pierre's content suggestions): fixtures-convey rule in item 7 Personal Property; earnest-money dollar guidance ($1,000 standard / $5,000+ strong signal); inspection-threshold tactic; appraisal-shortfall cash warning (`cb2968c`).
- **str-hub: 7 dead city permit URLs fixed** (NYC, LA, Chicago, Miami Beach, Denver, Seattle, Phoenix — all verified 200) + **Phoenix content corrected**: city switched from registration to a required $250/yr STR permit in Nov 2023, page wrongly said "no permit required" (`4f3a114`). Austin's link was already correct (it legitimately goes to Development Services); Nashville's 403 is bot-blocking, fine for users.
- **eviction-hub: dead Nolo + LegalZoom article links replaced** with verified-200 successors; dropped meaningless `?via=` (no live affiliate deal) (`71b32cf`).
- **lien-hub: dead Nolo mechanics-lien link replaced** (`7aa8f24`).
- **mobile-hub: 21st Mortgage CTAs swapped to Vanderbilt Mortgage** (Kevin's call) — 21stmortgage.com confirmed DOWN FOR EVERYONE 1+ week (third-party monitor), not geo-blocking; company still exists, prose mentions kept, revisit if their site returns (`e70bdfc`). vanderbiltmortgage.com 301s to vmf.com (vmf 403s bot probes but serves real users).
- **rv-hub Good Sam/Progressive fix wasn't live** — CF webhook dropped the morning push; re-triggered with empty commit (`e3eeb6e`). Verify live.
- **land-hub riparian rights: NOT missing** — Pierre missed it; live on /how-it-works since 2026-07-01.
- **fsbo: 21 orphaned state guides registered + 33 dead metro links killed** (`7c82d32`, live-verified). STATES_WITH_GUIDE in data.ts was missing the guides added 2026-06-27 → absent from sitemap (1,204→1,225 URLs) and /markets. All 51 guides now use data-derived StateMetroGrid; 13 hero breadcrumbs to inactive metros → /markets. RULE: new guides MUST be added to STATES_WITH_GUIDE.

## ✅ Resolved — 2026-07-13 housekeeping + link fixes

- **4 pending "LLC as site operator" wording edits committed+pushed** — `55plus-hub`, `condo-hub`, `commercial-hub`, `boat-hub`.
- **`buyer-hub`'s 3 reference docs now tracked in git** (commit `dd5126e`).
- **Dead NADA Guides valuation links fixed network-wide** — `nadaguides.com` (old J.D. Power-acquired valuation site) started 301-redirecting to a dead `nada.org/nadaguides.html` 404. Found via a user screenshot. Replaced all 12 "Check NADA Value" CTAs (9 in `boat-hub`, 3 in `moto-hub`) with the correct live J.D. Power page per vehicle type (`jdpower.com/boats`, `/rvs`, `/motorcycles` — all verified 200). Dropped the now-meaningless `?via=` tracking param since there's no confirmed live affiliate deal with J.D. Power; label changed "NADA Guides" → "J.D. Power" to match. Built clean, pushed both repos.
- **Dead Good Sam / Progressive RV insurance links fixed in rv-hub** — `goodsam.com/rv-insurance/` and `progressivecommercial.com/rv-insurance/` both 404. Found via user report. Fixed to the real current pages: `goodsam.com/insurance` and `progressive.com/rv-insurance/` (both verified 200); dropped dead `?via=` tracking params (7 references across layout/homepage/how-it-works/state pages). Full external-link sweep of rv-hub afterward found nothing else dead (rvtrader.com's 403 is CloudFront bot/geo-blocking, not a broken link). Built clean, pushed (`a40137f`).
- **boat-hub's RV content-cannibalization fixed (Kevin approved)** — boat-hub's `/vehicles/rvs` page and 50 per-state "Boat, RV & Powersports Title Guide" pages duplicated rv.byownerhub.com's dedicated RV state guides. Deleted the RV content page, dropped "RV" from state-guide titles/H1s/JD Power tagline, pointed nav+footer "RVs" link out to rv.byownerhub.com, added a Pages Function 301 (`/vehicles/rvs` → rv.byownerhub.com) so old bookmarks/indexed URLs don't 404. Powersports content kept (no dedicated powersports-hub exists). Built clean (66 static pages, was 67), pushed (`7b28698`).

## 🔴 Open — Kevin-only tasks

0. [x] ~~4 CF Pages projects not building~~ **ROOT-CAUSED + FIXED 2026-07-14** (Kevin pasted the eviction-hub build log): these 4 projects use the legacy build command `npx @cloudflare/next-on-pages`, which resolves the LATEST next-on-pages (1.13.16) → hard ERESOLVE vs wrangler 4.110 (workers-types v4 vs v5 peer conflict) → every build failed in ~23s before touching our code. Fix: pinned `@cloudflare/next-on-pages@1.13.7 + wrangler@3.114.14 + workers-types@4.x` as exact devDependencies so npx uses the local install (mobile `e0c8c8d`, eviction `b5b3a0d`, rv `e2f2f51`, lien `3c0f97a`). NOTE: eviction/rv/lien are static-export sites — next-on-pages is unnecessary for them; when convenient, switch their dashboard build command to `npx next build` (output dir `out`) and the pins can be dropped. mobile-hub genuinely needs next-on-pages (edge og-image route). **ALL 4 CONFIRMED LIVE 2026-07-14** — stale markers gone from rv/eviction/lien/mobile production; every queued fix (Pierre's items + link burn-down) is deployed.
0b. [x] ~~next.js version drift~~ **DONE 2026-07-14** — swept all ~40 repos; 26 were on vulnerable 14.x (<14.2.35): 55plus, auction, boat, closing, condo, contractor, eviction, firsttimebuyer, foreclosure, frbo, funeral, inspection, insurance, investor, landlord, lien, moto, new-build, probate, rv, solar, str, timeshare, trademark (spec was ^14.2.29 but lockfile pinned 14.2.29), trust, vacation. All bumped to `^14.2.35`, lockfiles updated, `next build` passed on every one (serial builds), committed and pushed — current branch + mirror (main↔master) where both exist on origin (18 repos), pushes staggered 20s for CF webhooks. Already-patched repos verified at 14.2.35 via lockfile: biz, buyer, byownerhub, commercial, divorce, estate, fsbo, land, llc, mobile, mortgage, flatfee, relocation. car-by-owner is on next 16.2.6 (not affected). fsbo-hub needed no rebuild (already patched), so the opengraph-image Windows workaround wasn't needed.
1. [x] ~~Re-point production branch on 6 CF Pages projects~~ **VERIFIED CORRECT 2026-07-14** — Kevin checked all 6 in the dashboard (55plus/condo/buyer/foreclosure on master; commercial-hub-523/investor on main). RESOLUTION ON MIRROR BRANCHES: **keep them, do NOT delete.** Other projects (e.g. eviction-hub, per its 2026-07-13 build log) build production from the mirror name (master) while the repo works on main — a full ~19-project re-point sweep isn't worth it under the fsbo-focus strategy. Standing process instead: always dual-push (main+master) — session tooling does this — and the weekly network audit alerts on any main≠master drift, which is the failure mode deletion was meant to prevent.
2. [ ] **Stand up hosting for `solar.byownerhub.com`** — no CF Pages project or Netlify site exists; DNS doesn't resolve. `str-hub` links a dead "Solar Hub" card. Create a Pages project from the `solar-hub` repo.
3. [ ] **Delete the leftover `relocation-hub` Worker** — superseded by the `relocation-hub-344` Pages project (now live). Both build from the same repo.
4. [ ] **GSC: click "Validate Fix"** on fsbo's 33 "Duplicate without user-selected canonical" — already fixed in code (canonicals verified live; Google's data pre-dates the fix).
5. [x] ~~GSC sitemaps~~ **CONFIRMED DONE by Kevin 2026-07-20** — the 07-07 `sitemap_errors.json` (all 38 properties 403) and this item were stale; Kevin confirmed sitemaps are submitted. Not independently re-verified via API (no service-account key file on this machine to re-run `submit_sitemaps.py`) — taking his word as authoritative over the old file snapshot.
6. [ ] **Set `RESEND_API_KEY`** on Netlify (Functions scope) when welcome emails are wanted — currently silently skipped.
7. [ ] **Supabase free tier auto-pauses when idle** (project `sdqfrkzujrqrjcznpcld`) — all API calls fail silently while paused. Upgrade or keep-alive before real email collection at volume.
8. [ ] **Freemium launch via `freemium-wip` — likely superseded, needs Kevin's call.** ⚠️ **2026-08-21 update:** production already has a live Stripe freemium build, shipped through the separate `fsbo-freemium-sandbox` repo (see [[open-items]] "NEW 2026-08-21" section above and [[SESSION-2026-08-21]]) — Stripe checkout, `purchases` table with server-verified entitlement, refund revocation, and passwordless resume are all live on fsbo.byownerhub.com today. That supersedes the localStorage-only design this item describes. `freemium-wip` (11 commits unpushed, unverified since 07-12) may just be dead weight at this point — worth confirming with Kevin whether it should be abandoned rather than merged.

## ✅ Resolved — Sessions 8–10 (2026-07-07 → 07-12) — detail in [[SESSION-2026-07-12]]

- **Alias 301s LIVE** via Pages Function `functions/_middleware.js`: `flatfee→flatfeemls`, `newbuild→new-build`, `frbo→rent` (closes old item 4; `_redirects` host rules silently no-op without domain attachment).
- **Network-wide WCAG 2.1 AA**: ~1,300 axe violations → 0; 36/36 CF sites verified clean live; fsbo too.
- **fsbo email compliance**: tokenized unsubscribe + RFC 8058 one-click verified in production; consent microcopy; 5 sibling forms POST to fsbo `/api/subscribe` (CORS); privacy pages on all collecting sites; deletion runbook `buyer-hub/PRIVACY-REQUEST-RUNBOOK.md`.
- **Byownerhub.com LLC** (NM) formed — address on legal pages + email footers; **2026-07-12 network-wide footer sweep**: every footer `© Byownerhub.com LLC` + visible link to byownerhub.com (~40 repos, 101 files; landlord/probate had no © line at all).
- **Netlify re-upped**; fsbo fully live-verified. Census zip fixed (`Netlify-Vary: query=zip` + ACS sentinel clamp). `CENSUS_API_KEY`/`ANTHROPIC_API_KEY` set.
- **new-build**: 50 real state guides live (were noindexed placeholders).
- **relocation**: legal pages added. **freemium-wip**: merged with main, hardened, deploy-ready.

## ✅ Resolved — Session 7 Link Audit + Fixes (2026-07-03/04)

Full-network audit (41 domains, ~2,150 pages, 810 external links checked). Report: `buyer-hub/byownerhub-link-audit-2026-07-03.md`. Fixes shipped + verified live:
- **apex** — corrected newbuild links, Solar → coming-soon, added Relocation card (live).
- **investor-hub** — fix-and-flip 50-state grid retargeted `/fix-and-flip/<state>` → `/states/<state>` (were all 404); added `/privacy`, `/terms`, `/disclaimer` (were missing from repo).
- **commercial-hub** — state-page "Qualified Intermediary" CTA → 1031exchangecorp.com (was dead `byownerhub.com/1031-exchange`).
- **foreclosure-hub** — nav "How to Buy"/"Financing" → homepage anchors `/#how-to-buy`, `/#search` (were 404 pages).
- **buyer-hub** — homepage now links canonical `flatfeemls.byownerhub.com` (was `flatfee.`).
- **55plus-hub / condo-hub** — legal pages + states index restored (were 404 in production despite existing in code — the stale-deploy symptom).
- **relocation-hub** — deployed from scratch on CF Pages (`relocation-hub-344`), Next 14.2.5→14.2.35, static export, custom domain live.
- **ROOT CAUSE identified:** CF Pages production branches pinned to opposite branch name (master↔main) → pushes only built previews → months of stale production. Worked around via mirror branches; permanent fix = item 1 above.
- **External rot logged:** 183 real 404s (HUD state pages on firsttimebuyer; state DMV/boating/court/vital-records on boat/car/probate/funeral/land). 235 "403s" are just bot-blocking, fine for users. Full list in report.

---

## ✅ Resolved — CF Pages Migration COMPLETE (2026-07-01)

All 38 byownerhub repos now on Cloudflare Pages. DNS CNAMEs fixed for 21 pending domains. `nodejs_compat` flag set across CF Pages projects. All 38 sites redeployed. `fsbo-hub` and `solar-hub` deliberately stay on Netlify. See `network-status.md` for full per-repo table — the "🔴 Critical — Verify CF Pages Domains" and "🔶 CF Pages — Next Batch" sections below are now superseded by this.

## ✅ Resolved — Session 6 Site Fixes (2026-07-01)

- **investor-hub** — fix-and-flip, brrrr, buy-and-hold, financing nav pages added to `src/app/` and pushed. Root cause of nav 404s was `netlify.toml` misconfigured for server-render vs static export — fixed.
- **boat-hub** — 5 broken NVDC links fixed (`dcms.uscg.mil` → `dco.uscg.mil` NVDC eStorefront). Commit `bba41bd`.
- **land-hub** — Riparian Rights section added to how-it-works guide. Commit `195cb75`.
- **fsbo-hub** — Contextual flatfee inline link added to `MLSComparison.tsx`. Footer domain fixed `flatfee.byownerhub.com` → `flatfeemls.byownerhub.com`. Commit `c3a038a`.
- **car-by-owner** — 10 state form child pages added (MV-912 NY, REG 135 CA, Form 130-U TX, HSMV 82040 FL, MV-4ST PA, BMV 3774 OH, VSD 703 IL, T-7 GA, MVR-1 NC, SUT-1 VA). Sitemap updated. VA page factual error fixed.

---

## ✅ Resolved — investor-hub + buyer-hub State Pages (2026-06-25)

**investor-hub `src/lib/states.ts`** — Expanded from stub (`name/slug/abbreviation` only) to full per-state data:
- `propertyTaxRate` — effective annual rate for all 50 states
- `landlordFriendly` — `high | medium | low` with state-specific notes
- `topMarkets` — 2–3 top investor cities per state
- `investorNote` — 44–55 word state-specific market intelligence (rent control laws, eviction process, cap rate ranges, employment drivers)
- `attorneyRequired` — fixes previously hardcoded "Title companies handle closing" which was wrong for 15+ states

**investor-hub `src/app/states/[state]/page.tsx`** — Updated to render all new fields:
- "At a Glance" now shows property tax rate, landlord climate badge, top markets, correct closing language
- New "Market Intelligence" section renders `investorNote` uniquely per state
- Meta description now includes property tax rate and top markets (differentiates search results)

**buyer-hub `src/lib/states.ts`** — Added 5 new fields to all 50 states:
- `medianHomePrice` — state median home price
- `savingsEstimate` — formatted 3% commission savings at median (range: $4,950–$24,600)
- `inspectionDays` — standard inspection contingency period per state
- `transferTaxNote` — who pays, how much, state-specific
- `buyerTip` — state-specific practical tip (radon, septic, mineral rights, option period, etc.)

**buyer-hub `src/app/states/[state]/page.tsx`** — Updated:
- Hero now shows savings estimate prominently ("Save $X,XXX at the state median price")
- Key info box adds inspection period and savings to the data grid
- Transfer tax note added as separate box
- 8 steps are now partially state-specific (step 5 mentions inspection period, step 6 embeds the state-specific buyerTip, step 8 is attorney vs title company conditional)
- Meta description now includes savings estimate and inspection period

**No code pushed** — all changes are local.

---

## ✅ Resolved — CF Pages Migration (2026-06-23)

**Root cause found and fixed:** All CF Pages builds were failing because `next.config.js` (empty, CommonJS) takes precedence over `next.config.mjs` (with `output: 'export'`). Deleted `next.config.js` from 8 repos.

- byownerhub.com → **LIVE** on CF Pages ✅
- investor-hub → CF build confirmed success ✅
- buyer-hub → CF build confirmed success ✅
- 55plus-hub, condo-hub, frbo-hub, landlord-hub, commercial-hub, firsttimebuyer-hub → builds triggered ✅

---

## ✅ Resolved — Prior Sessions

- **investor-hub bad commit** — master reset to good commit via GitHub API (2026-06-23)
- **State pages** — investor-hub and 55plus-hub both have `/states/[state]` pages for all 50 states (2026-06-23)
- **main branches** — created on 55plus-hub, buyer-hub, condo-hub, investor-hub (were master-only) (2026-06-23)
- **eviction-hub** — `'use client'` boundary added; `NoticeEmailForm.tsx` extracted as client component (2026-06-20)
- **closing-hub** — Real homepage built (LendingTree + Angi primary, Old Republic + First American secondary) (2026-06-20)
- **landlord-hub** — Real homepage built (RentSpree + Angi primary, Avail + NOLO secondary) (2026-06-20)
- **fsbo-hub** — `NetworkPromo.tsx` committed + pushed (2026-06-20)
- **estate-hub + inspection-hub** — Tailwind `theme.colors.slate` → `theme.extend.colors.charcoal` palette fix (2026-06-20)
- **All 32 repos** — on GitHub as private repos under `kevc55-code` (2026-06-19)
- **fsbo.byownerhub.com + car.byownerhub.com** — Live on Netlify, GSC verified, sitemaps submitted (2026-06-15)

---

## ✅ Superseded — CF Pages Domain Verification / Next Batch (resolved 2026-07-01)

Both sections below are superseded by the 2026-07-01 CF Pages migration completion (see top of file). All 38 repos are now CF Live with DNS CNAMEs fixed; kept here for history only.

<details>
<summary>🔴 (old) Critical — Verify CF Pages Domains</summary>

The following CF Pages projects were configured with domains that need verification:

- [x] `closing-hub` → closinghub.com — DNS fixed 2026-07-01
- [x] `firsttimebuyer-hub` → firsttimebuyerhub.com — DNS fixed 2026-07-01
- [x] `flatfee-hub` → flatfeemlshub.com — DNS fixed 2026-07-01
- [x] `landlord-hub` → landlordhub.com — DNS fixed 2026-07-01
- [x] `buyer.byownerhub.com`, `investor.byownerhub.com`, etc. — confirmed resolving 2026-07-01

</details>

<details>
<summary>🔶 (old) CF Pages — Next Batch (~20 repos not yet connected)</summary>

**Priority:** mobile-hub, probate-hub, inspection-hub, contractor-hub, trust-hub, estate-hub, solar-hub
**Then:** lien-hub, llc-hub, timeshare-hub, rv-hub, eviction-hub, divorce-hub, moto-hub, trademark-hub, str-hub, funeral-hub, mortgage-hub, insurance-hub, biz-hub

All of the above (except solar-hub, which stays on Netlify) are now ✅ CF Live as of 2026-07-01.

</details>

---

## 🔶 fsbo-hub — CF Pages Migration (when ready)

fsbo-hub is the flagship and most complex site. Current state: live on Netlify, `next.config.js` has empty config.

Before migrating:
- [ ] Add `output: 'export'`, `trailingSlash: true`, `images: { unoptimized: true }` to `next.config.js` (or replace with `next.config.mjs`)
- [ ] Confirm Supabase API routes can work as static export (or switch to Path B / Workers runtime)
- [ ] SUPABASE_SERVICE_ROLE_KEY — confirm set in CF Pages env vars after migration
- [ ] IndexNow HOST — update from `www.byownerhub.com` to `fsbo.byownerhub.com`
- [ ] Test build locally before deploying to CF Pages
- [ ] Keep Netlify live as fallback until CF is confirmed

---

## 🔶 byownerhub.com — UX Redesign

Homepage redesign in progress (2026-06-23):
- [ ] Categorized hub grid (Sell / Buy / Rent / Vehicles / Support / Legal)
- [ ] FSBO flagship hero CTA
- [ ] Intent chooser (6 tiles)
- [ ] Remove undifferentiated "coming soon" chip wall

---

## 🔶 Affiliate Enrollments

### Enrolled ✅
- [x] HireAHelper — $10/booking — `https://www.hireahelper.com/?affil=32303735`
  - [ ] Email `affiliate-support@hireahelper.com` to register all new network domains as they go live
- [x] Angi (via CJ, Pub ID: 101755238) — 25% revshare — enrolled 2026-05-27

### Hard Rules
- ⚠️ **Houzeo** — NO affiliate program. Never add as CTA anywhere in the network.
- ⚠️ **Rocket Money (Impact)** — Do NOT accept $0 contract
- ⚠️ **Moving Labor Brokers** — $25/sale — NOT rendered on any page yet. Decide placement before next deploy.

### Priority Applications (pending)
- [ ] LendingTree (via CJ) — $1–$70/lead — apply for: fsbo, buyer, flatfee, firsttimebuyer, closing, mortgage, land, mobile, commercial, biz
- [ ] Credible — $240/funded loan — firsttimebuyer, mortgage, buyer
- [ ] FlexOffers — ⚠️ Reapplication needed: email support@flexoffers.com (sites now live)

### By Program
- [ ] Buildium — landlord, str
- [ ] RentSpree — frbo, landlord, str
- [ ] Carfax / AutoCheck — car
- [ ] EverQuote, Hippo, PolicyGenius, Kin, Neptune Flood — insurance
- [ ] LegalZoom — fsbo, probate, lien, llc, trust, estate, divorce, eviction, trademark
- [ ] Nolo (120-day cookie!) — fsbo, divorce
- [ ] US Legal Forms — fsbo, eviction, trademark
- [ ] Trust & Will — probate, trust, estate, funeral
- [ ] Levelset — lien — $50–$200/signup (email to apply)
- [ ] ZenBusiness + Bizee (via CJ) — llc, biz
- [ ] Wesley Financial — timeshare — $50–$300/lead (apply directly)
- [ ] EnergySage + SunRun — solar
- [ ] Good Sam + LightStream — rv
- [ ] Thumbtack — contractor, inspection
- [ ] Virtuance — fsbo (photography)
- [ ] FlatFee.com — flatfee, fsbo
- [ ] U-Pack — fsbo (moving container)
- [ ] SpareFoot — fsbo (storage)
- [ ] 1-800-GOT-JUNK — fsbo (junk removal)
- [ ] BoatUS — boat
- [ ] Cycle Trader + Progressive — moto
- [ ] Bestow Life Insurance — funeral
- [ ] Fabric by Gerber Life + PolicyGenius — trust

---

## 🔴 Google Search Console — Sitemaps (HIGHEST LEVERAGE OPEN TASK as of 2026-07-01)

- [x] `https://fsbo.byownerhub.com/sitemap.xml` — ✅ Submitted 2026-06-15
- [x] `https://car.byownerhub.com/sitemap.xml` — ✅ Submitted 2026-06-15
- [ ] **~35 network sites still NOT submitted to GSC.** Now that all 38 repos are CF Live (2026-07-01), this is manual, per-property work only Kevin can do in Search Console (domain verification + sitemap submission). Flagged as the single highest-leverage remaining task.

---

## 🔶 Plausible Analytics

- [ ] Install not done yet (confirmed still pending as of 2026-07-01)
- [ ] Add Plausible script to each site (or confirm wired in shared template)
- [ ] Create separate property per subdomain in Plausible dashboard
- [ ] Verify pageview data flowing after each deploy

---

## 🔶 Other Open Items (carried forward, 2026-07-01)

- [ ] **`sameAs` social profiles in Organization schema** — still empty across the network, waiting on real social URLs from Kevin.
- [ ] **Stripe paywall ($99 document toolkit)** — not yet built.
- [ ] **MH Village zip search broken** — issue is on MH Village's side; follow up with them.
- [ ] **Author bylines + About page** — not done.
- [ ] **Site bucketing decisions pending** — fold closing-hub / flatfee-hub into fsbo-hub; kill moto-hub, rv-hub, timeshare-hub, boat-hub, biz-hub.

---

## 🔶 Cloudflare Pages Build Budget

Free tier: **500 builds/month total** across all projects.
With 19+ repos connected, burns fast during active dev. During sprints, prefer iterating locally before pushing to CF.
- Current usage: ~15–20 builds consumed in migration/debug session 2026-06-23
- Request limit increase if needed: https://forms.gle/eX6pXvit1wBv77Yw5

---

## ✅ Resolved — fsbo-hub Blog Expansion (2026-06-25)

All 236 blog posts in `src/lib/blog.ts` expanded from ~150–350 word stubs to full articles.

**Final word count distribution:**
- `<400w`: **0 posts** (was 64 when expansion began this session)
- `400–600w`: 130 posts
- `600+w`: 106 posts
- Total: 236 posts

**Batches completed this session (12–17):**
- Batch 12: Arkansas (4), Kansas (3), Iowa (2), Colorado Springs (2), Fort Collins (2), Wisconsin disclosure
- Batch 13: North Dakota (2), South Dakota (2), Vermont (2), Rhode Island, Idaho (2)
- Batch 14: Alaska (2), Anchorage (2), Eugene OR (2), Mobile AL (2), Huntsville AL (2), Montgomery AL (2), Provo UT (2)
- Batch 15: Worcester MA (2), Springfield MA (2), Madison WI, Honolulu (2), Hawaii state (2)
- Batch 16: Winnipeg (2), Calgary (2), Vancouver BC (2), Toronto (2), Montreal (2)
- Batch 17: Buffalo disclosure, Arkansas disclosure, Kansas (2), Wichita (2), Cleveland disclosure, Greensboro disclosure, Knoxville (2)

**No code pushed** — all changes are local to `src/lib/blog.ts` on the filesystem.

---

## 🔶 fsbo-hub Code Open Items

- [ ] SUPABASE_SERVICE_ROLE_KEY — confirm set in Netlify env vars (leads + subscribe forms depend on it)
- [x] IndexNow HOST — fixed to `fsbo.byownerhub.com` (prior session)
- [x] Moving Labor Brokers — removed from StateGuideAffiliates.tsx (2026-06-26, local not pushed)
- [x] Rocket Money — removed from [metro]/page.tsx (2026-06-26, local not pushed)
- [x] next.config.js — updated with output: 'export', trailingSlash, unoptimized images (2026-06-26, local not pushed)
- [x] 21 state guide pages — **ALL COMPLETE** as of 2026-06-27 (session 4). All 51 directories (50 states + DC) now have page.tsx. Pages written: CT, NJ, IA, WI, SC, AR, KS, ME, ID, MS, DE, RI, AK, HI, ND, SD, VT, NH, WV, MT, WY. **Not pushed yet.**
- [ ] 3 affiliates with no tracking links — 1-800-GOT-JUNK, Nolo, Virtuance (commission TBD)
- [ ] HVAC pixel domain — confirm from CJ (link 17142830, kqzyfj.com click) before deploying closing-hub / landlord-hub
- [ ] Item 9c: FL CDD disclosure for Miami + Tampa (currently Orlando-only)
- [ ] `'use client'` sweep — eviction-hub was fixed; audit other repos with interactive forms
