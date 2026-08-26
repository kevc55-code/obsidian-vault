<%*
const kind     = await tp.system.prompt("Audit kind (link | code | seo | a11y)", "link");
const parts    = tp.file.folder(true).split("/");
const i        = parts.indexOf("01-Projects");
const project  = (i >= 0 && parts.length > i + 1) ? parts[i + 1] : "UNKNOWN";
const archived = tp.file.folder(false) === "archive";
const stamp    = tp.date.now("YYYY-MM-DD");
const target   = archived ? `${kind}-audit-${stamp}` : `${kind}-audit`;
if (tp.file.title !== target) { try { await tp.file.rename(target); } catch (e) {} }
-%>
---
type: audit
audit-kind: <% kind %>
project: <% project %>
status: <% archived ? "archived" : "canonical" %>
last-verified: <% stamp %>
---

# <% project %> — <% kind %> audit

**Run:** <% stamp %>
**Scope:**
**Method:**

---

## 🔴 Real, actionable

## 🟡 Needs verification

## ✅ Resolved since last run

## ⚪ False positives

---

> Canonical note — overwrite in place on each run.
> To freeze a snapshot, create a new audit note inside `Audits/archive/`; the template
> date-stamps the filename and marks it `status: archived` automatically.
