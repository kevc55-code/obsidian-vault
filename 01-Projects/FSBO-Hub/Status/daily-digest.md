---
type: status
project: FSBO-Hub
last-verified: 2026-08-27
---

# Daily Inbox Digest — 2026-08-27

**7 threads in the last 2 days. 1 actionable (Buildium affiliate acceptance), 2 worth knowing (Stripe key-roll), 4 noise.**

## 🔴 Action required

### Buildium affiliate application accepted (Impact)
- **From:** notifications@app.impact.com — **Subject:** "Welcome to Buildium!" (2026-08-25)
- **Why it matters:** Buildium was a pending program in the affiliate backlog (targeted at landlord-hub and str-hub). The acceptance email carries **no commission terms** — it only says to log into Impact and add creatives. Program is managed by Gen3 Marketing (buildium@gen3marketing.com). Impact account ID references in the mail: 2017129 / 10839.
- **Recommended action:** Pierre/Kevin log into the Impact dashboard to record the actual payout terms (CPA vs revshare, cookie window), then place the Buildium "Schedule a Demo" / "14-day trial" text links or tracking links on landlord-hub and str-hub. Update `affiliate-stack` / open-items Affiliate Enrollments once terms are known. New open item opened below.

## 🟡 Worth knowing

- **Stripe — "Your Stripe verification link" + "An API key for your Stripe account was rotated"** (notifications@stripe.com, 2026-08-26, ~2 min apart). A key roll was requested and completed. Consistent with the 08-26 production-checkout remediation and the open 🔴 items on splitting/rotating the Stripe key across Netlify deploy contexts — appears intentional, no sign of compromise. Noting so the rotation is on record. (Link/code not reproduced here per digest policy.)

## ⚪ Noise

4 threads: two Slack sign-in / email-confirmation notifications (no account found for that address; confirmation code — not reproduced), and two Google "you shared account data with Claude / security alert" notices for the Gmail connector this digest itself uses.

---

## Cross-reference notes
- Buildium was already listed as a *pending* application in `open-items.md` → Affiliate Enrollments → By Program. The acceptance is genuinely new; a new 🔴 open item was added.
- The Stripe key activity maps onto existing open items ("Stripe key is shared across all Netlify deploy contexts", "confirm a live-mode Stripe webhook endpoint exists") — no new item opened.
