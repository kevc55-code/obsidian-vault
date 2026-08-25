---
type: project-index
project: <% tp.file.folder(false) %>
repo: <% tp.system.prompt("GitHub repo (owner/name)") %>
category: <% tp.system.prompt("Category", "real-estate-network") %>
status: active
deploy-ready: false
last-verified: <% tp.date.now("YYYY-MM-DD") %>
open-items: 0
---

# <% tp.file.folder(false) %> — Project Reference

> **Repo:** `github.com/<% tp.frontmatter.repo %>`
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
FROM "01-Projects/<% tp.file.folder(false) %>"
WHERE type != "project-index"
SORT last-verified DESC
```
