---
type: session
project: <% tp.file.folder(false) === "Sessions" ? tp.file.folder(true).split("/")[1] : tp.file.folder(false) %>
date: <% tp.date.now("YYYY-MM-DD") %>
last-verified: <% tp.date.now("YYYY-MM-DD") %>
---

# Session <% tp.date.now("YYYY-MM-DD") %>

## Context
<!-- What prompted this session; what state things were in at the start. -->

## Work Done
<!-- Commits, files touched, decisions made. Link repos and notes with wikilinks. -->

## Findings
<!-- Anything discovered that outlives this session. -->

## Follow-ups
<!-- Anything that should land in Status/open-items.md. -->

---

*Related:* [[index]] · [[open-items]]
