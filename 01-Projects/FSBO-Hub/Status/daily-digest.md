---
type: status
project: FSBO-Hub
last-verified: 2026-09-10
---

# Daily Inbox Digest — 2026-09-10

**1 email thread + 1 Slack item (4 channels scanned, last ~2 days). 0 actionable.** 1 worth knowing, 1 noise. No new Slack channels.

Quiet window. Gmail had a single new in-window thread — a product newsletter. The only new Slack signal since the last digest (09-06) is the 2026-09-07 weekly network audit post, which is already fully tracked in `open-items.md`. No digest ran 09-07 through 09-09, so this run also covers that gap; nothing actionable surfaced in it.

## 🔴 Action required

None.

Carried open, unchanged (see `open-items.md`, no new email or Slack activity on any of these in this window):
- **Bitwarden new-device login from a Brazil IP (2026-09-02)** — still unconfirmed, now **8 days**. Standing recommendation holds: if nobody confirms it was them, default to rotating the master password and deauthorizing sessions rather than waiting further.
- **WillMaker / Nolo publisher application** (paul.ji@internetbrands.com) — awaiting Paul's reply; nothing owed from our side.
- **FlexOffers reapplication declined** (🔴 09-02) — decline-reason email to support@flexoffers.com still open.
- **Buildium affiliate terms** (🔴 08-27) — still needs Impact login to record payout terms.
- **Network audit (2026-09-07 run)** — 6 real issues + proposals sit in `open-items.md` and in the `#network-audit-results` thread awaiting in-thread approval: auction-hub stale deploy (clean FF ready), eForms TN link rot (replacement found), `insurance.ohio.gov` geo-block allowlisting (3rd run unactioned), 4× Redfin "recently sold" 404s (needs US check), `mohousing.com/homeownership/` 404 (needs current MHDC page), `texas.gov` root 404 (needs US check), 22-repo mirror-branch drift.

## 🟡 Worth knowing

- **[#network-audit-results] Weekly network audit — 2026-09-07** (Claude routine). 38 sites, 3,328 pages checked. 32 new failures → 6 real; 24 are fsbo `??` crawler false positives (all live-verified 200, count inflated by an `audit.mjs` OOM this run, re-ran clean). No approvals posted in the 8-reply thread yet. Already captured in `open-items.md` — listed above under carried-open for visibility, not a new item.

## ⚪ Noise

1 item across both sources: **[email]** "Connect Claude to Gmail, Slack, and the rest of your stack" from `no-reply@email.claude.com` (2026-09-08) — product newsletter.

## Run notes

- Gmail query `in:inbox newer_than:2d` → 1 thread total.
- Slack: `#bugs`, `#feature-requests`, `#network-audit-results`, `#all-byownerhub-re` all scanned. `#bugs` newest message is 2026-09-01 (Kevin: old-code fix note); `#feature-requests` has only join messages. `#network-audit-results` newest is the 2026-09-07 audit post; its 8-reply thread is all auto-posted proposals — no human approvals.
- `#all-byownerhub-re`: newest entry is this task's own 2026-09-06 digest post (skipped per instructions). No digest posted 09-07 to 09-09.
- `slack_search_channels` query `a` → only `#all-byownerhub-re` and `#network-audit-results`, both already on the scan list; no new channel to add.
- No vault open items opened or changed. `index.md` 🔴 count unchanged.
