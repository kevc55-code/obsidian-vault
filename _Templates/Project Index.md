<%*
const repo     = await tp.system.prompt("GitHub repo (owner/name)", "kevc55-code/");
const category = await tp.system.prompt("Category", "real-estate-network");
const parts    = tp.file.folder(true).split("/");
const i        = parts.indexOf("01-Projects");
const project  = (i >= 0 && parts.length > i + 1) ? parts[i + 1] : tp.file.folder(false);
if (tp.file.title !== "index") { try { await tp.file.rename("index"); } catch (e) {} }
-%>
---
type: project-index
project: <% project %>
repo: <% repo %>
category: <% category %>
status: active
deploy-ready: false
last-verified: <% tp.date.now("YYYY-MM-DD") %>
open-items: 0
---

# <% project %> — Project Reference

> **Repo:** `github.com/<% repo %>`
> **Stack:**
> **Current HEAD:**

---

## Session Protocol

1. Read this index at the start of every session for this project.
2. Update `last-verified` and `open-items` in the frontmatter after any session that changes the repo.

---

## Standing Rules

---

## Recent Work

---

## Sub-notes

```dataview
LIST
FROM "01-Projects/<% project %>"
WHERE type != "project-index"
SORT last-verified DESC
```
