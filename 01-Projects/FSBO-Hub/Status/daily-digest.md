---
type: status
project: FSBO-Hub
last-verified: 2026-09-03
---

# Daily Inbox Digest — 2026-09-03

**10 email threads + Slack scan of 4 channels (~5 in-window messages) reviewed (last ~2 days). 2 actionable.** 7 worth knowing, ~3 noise. No new Slack channels.

## 🔴 Action required

### [email] no-reply@bitwarden.com (2026-09-02) — Bitwarden new-device login from a Brazil IP

Two emails to `byownerhubadmin@gmail.com` on 2026-09-02 ~09:52 UTC: *"Your Bitwarden Verification
Code"*, then 17 seconds later *"New Device Logged In From Chrome Extension"*. The login came from a
new device at an IP (`187.14.51.59`) that geolocates to Brazil — not Kevin's usual US location and
not Pierre's France location. The email-OTP was cleared within seconds, so whoever authenticated
also had access to this inbox at that moment.

**Why it matters:** Bitwarden is the network's password vault — maximum blast radius. [[vault-credential-exposure]]
still tracks un-rotated exposed tokens, so an unexplained vault login from an unexpected country is
the trigger to act on now, not wait out.

**Recommended action:** Kevin/Pierre confirm whether either of you (or automated tooling) logged
into Bitwarden via a Chrome extension on 09-02. If not: change the master password, deauthorize all
sessions (web vault → Account Settings → Deauthorize Sessions), verify 2FA, and rotate the
highest-value secrets in the vault. New open item opened 2026-09-03.

### [email] paul.ji@internetbrands.com (2026-09-02) — WillMaker (Nolo) publisher application needs a reply

Reply on the Byownerhub.com LLC WillMaker publisher application (CJ PID 101755238): the publisher
is asking (a) how many site visits our sites generate and (b) the URLs where WillMaker / Nolo
products would be listed, before advancing the application.

**Why it matters:** Nolo (120-day cookie) is a tracked *pending* program in the affiliate backlog
(`open-items.md` → Affiliate Enrollments → By Program). This is that application actively moving
forward; it goes cold without a reply.

**Recommended action:** Pierre replies with network traffic figures (or a representative subset —
fsbo + top hubs) and the specific pages where Nolo/WillMaker links would sit (fsbo state guides,
divorce-hub). New open item opened 2026-09-03, cross-referenced to the Nolo line.

## 🟡 Worth knowing

- **[email] pvulliez@gmail.com — "Fwd: Alison US CA has invited you to join their program"** — Awin
  affiliate invite. Kevin and Pierre already agreed to skip it ("Doesn't really fit anywhere");
  reply sent 09-03. No action.
- **[email] notifications@app.impact.com — "Login Alert from Impact.com"** — unusual-login notice
  for a sign-in from Mulhouse, France (Desktop/Windows). Matches Pierre's known location; almost
  certainly him. No action.
- **[email] RyanMulligan@carfax.com — Carfax partnership thread resurfaced** — no new message. Last
  activity 2026-06-26: Carfax answered our pricing questions ($23.99/report = our cost, margin to
  be built in) and the thread then went quiet on our side. Carfax / AutoCheck is a tracked pending
  "by program" affiliate for car-by-owner — revive if still wanted.
- **[email] pvulliez@gmail.com — "Fwd: CycleTrader.com Partner Request"** — forwarded partner-request
  acknowledgement (09-01). Already tracked: "CycleTrader Partners application submitted (pending)."
- **[email] noreply@rakutenadvertising.com — "Activate your Rakuten Advertising Login"** —
  login-activation email (48h link). Noted in the 09-02 digest; still pending activation. Act on it
  in the mailbox directly only if joining Rakuten is intended.
- **[#bugs] Pierre Vulliez (2026-09-01)** — LandlordHub "Get State Lease Forms" bug confirmed fixed
  site-wide; Kevin's 08-31 old-code fix did it. Already tracked as resolved.
- **[#network-audit-results] Kevin Cross (2026-09-01)** — weekly audit: 38 sites, 0 real failures.
  Two proposals still awaiting an in-thread approval: (1) allowlist `insurance.ohio.gov` (geo-block
  false alarm), (2) resolve mirror-branch drift on ~21 repos (persisting 2 weeks). Already tracked.

## ⚪ Noise

~3 across both sources — Claude.com onboarding marketing and the Resend product newsletter (email);
`#feature-requests` had only channel-join lines. `slack_search_channels` found no new non-archived channels.

---

*Two new open items opened 2026-09-03 (Bitwarden login; WillMaker/Nolo application). Prior open items — FlexOffers declined (09-02), Buildium terms (08-27), the two 08-26 Stripe items — remain open in `open-items.md`.*
