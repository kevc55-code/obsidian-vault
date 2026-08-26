<%*
// Name the file SESSION-YYYY-MM-DD unless it is already named that way.
const stamp = tp.date.now("YYYY-MM-DD");
if (!tp.file.title.startsWith("SESSION-")) {
  await tp.file.rename("SESSION-" + stamp);
}
// Derive the project from the path: 01-Projects/<Project>/Sessions/...
const parts = tp.file.folder(true).split("/");
const i = parts.indexOf("01-Projects");
const project = (i >= 0 && parts.length > i + 1) ? parts[i + 1] : "UNKNOWN";
-%>
---
type: session
project: <% project %>
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
