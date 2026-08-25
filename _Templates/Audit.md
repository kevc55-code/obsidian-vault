---
type: audit
audit-kind: <% tp.system.prompt("Audit kind (link | code | seo | a11y)", "link") %>
project: <% tp.file.folder(false) === "Audits" ? tp.file.folder(true).split("/")[1] : tp.file.folder(false) %>
status: canonical
last-verified: <% tp.date.now("YYYY-MM-DD") %>
---

# <% tp.file.title %>

**Run:** <% tp.date.now("YYYY-MM-DD") %>
**Scope:**
**Method:**

---

## 🔴 Real, actionable

## 🟡 Needs verification

## ✅ Resolved since last run

## ⚪ False positives

---

> Canonical note — overwrite in place on each run.
> Snapshots worth freezing go to `Audits/archive/` with the run date in the filename.
