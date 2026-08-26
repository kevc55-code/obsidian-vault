---
type: home
last-verified: 2026-08-25
---

# Vault Home

> [!info] Requires Dataview + Templater
> The queries on this page are rendered by the **Dataview** plugin; `_Templates/` needs
> **Templater**. Both are installed and enabled on this machine.
> On a fresh clone they won't be — plugin *code* isn't committed, only the settings — so
> install both from *Settings → Community plugins → Browse* or these become inert code blocks.

## 📁 PARA

| Folder | Purpose |
|---|---|
| `00-Inbox` | Unsorted capture |
| `01-Projects` | Active work with an end state |
| `02-Areas` | Ongoing responsibilities (Finance, French-Learning, Job-Search, MTB) |
| `03-Resources` | Durable reference material |
| `04-Archive` | Inactive / superseded |
| `Decisions` | Standing decisions log |
| `_Templates` | Templater templates |

---

## 🚀 All Projects

```dataview
TABLE WITHOUT ID
  file.link            AS Project,
  status               AS Status,
  repo                 AS Repo,
  deploy-ready         AS "Deploy?",
  open-items           AS "Open",
  last-verified        AS "Verified"
FROM "01-Projects"
WHERE type = "project-index"
SORT last-verified DESC
```

---

## ⏳ Gone Stale (not verified in 30+ days)

```dataview
TABLE WITHOUT ID
  file.link                                        AS Note,
  type                                             AS Type,
  last-verified                                    AS "Last Verified",
  round((date(today) - date(last-verified)).days)  AS "Days Ago"
FROM "01-Projects" OR "02-Areas"
WHERE last-verified
  AND (date(today) - date(last-verified)) > dur(30 days)
  AND type != "session"
  AND !contains(file.folder, "archive")
SORT last-verified ASC
```

---

## 🕒 Latest Sessions (all projects)

```dataview
TABLE WITHOUT ID
  file.link  AS Session,
  project    AS Project,
  date       AS Date
FROM "01-Projects"
WHERE type = "session"
SORT date DESC
LIMIT 15
```

---

## 🔍 Audits

```dataview
TABLE WITHOUT ID
  file.link      AS Audit,
  project        AS Project,
  audit-kind     AS Kind,
  status         AS Status,
  last-verified  AS "Last Run"
FROM "01-Projects"
WHERE type = "audit" AND status = "canonical"
SORT last-verified DESC
```

---

## 📌 Status Notes

```dataview
LIST rows.file.link
FROM "01-Projects"
WHERE type = "status"
GROUP BY project
```
