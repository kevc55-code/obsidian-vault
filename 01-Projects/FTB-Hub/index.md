---
type: project-index
project: FTB-Hub
status: active
last-verified: 2026-04-09
tags: [project, ftb, active]
stack: Next.js 14, TypeScript, Tailwind
updated: 2026-04-09
---

# FTB Hub

First-time buyer affiliate site. DPA programs, tools, and state-by-state guidance.

## Status
54 static pages built (homepage + 50 states + 2 Next.js internals). Builds clean.

## Hero
"Buy Your First Home Without Getting Ripped Off"

## Tech Stack
- Framework: Next.js 14.2.3 (App Router)
- Language: TypeScript
- Styling: Tailwind CSS + custom colors (navy: #0D1B2A, teal: #1B7FA3, gold: #E8A838, slate: #4A5568)
- Deploy: Netlify (@netlify/plugin-nextjs in netlify.toml) — not yet connected
- No DB — static data layer

## Repo
`C:\Users\kevc_\Documents\GitHub\ftb-hub` — branch: `main`

## Data Layer
- `src/lib/states.ts` — all 50 states: HFA name/URL, DPA programs (name, max assistance, income limit note, link), transfer tax rate + note, attorney required at closing
- `src/lib/tools.ts` — affiliate tools by category
- `src/app/[state]/page.tsx` — SSG with generateStaticParams() + generateMetadata()
- Affiliate links: `?via=ftbhub` — lead pick: Better Mortgage

## Open Items
- Netlify deployment not yet connected
- SEO meta tags not verified against search intent
- State law data accuracy review not done
- sitemap.xml for state pages (optional)
- Internal linking to related hubs
