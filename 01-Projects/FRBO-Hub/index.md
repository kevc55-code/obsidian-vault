---
type: project-index
project: FRBO-Hub
status: active
last-verified: 2026-04-09
tags: [project, frbo, active]
stack: Next.js 14, TypeScript, Tailwind
updated: 2026-04-09
---

# FRBO Hub

For-rent-by-owner affiliate site. Landlords listing rentals without a property manager.

## Status
54 static pages built (homepage + 50 states + 2 Next.js internals). Builds clean.

## Hero
"Rent Your Property Without Paying a Property Manager"

## Tech Stack
- Framework: Next.js 14.2.3 (App Router)
- Language: TypeScript
- Styling: Tailwind CSS + custom colors (navy: #0D1B2A, teal: #1B7FA3, gold: #E8A838, slate: #4A5568)
- Deploy: Netlify (@netlify/plugin-nextjs in netlify.toml) — not yet connected
- No DB — static data layer

## Repo
`C:\Users\kevc_\Documents\GitHub\frbo-hub` — branch: `main`

## Data Layer
- `src/lib/states.ts` — all 50 states: written lease required, lease term limits, required clauses, security deposit rules, rent control cities
- `src/lib/tools.ts` — affiliate tools by category
- `src/app/[state]/page.tsx` — SSG with generateStaticParams() + generateMetadata()
- Affiliate links: `?via=frbohub` — lead pick: TurboTenant

## Open Items
- Netlify deployment not yet connected
- SEO meta tags not verified against search intent
- State law data accuracy review not done
- sitemap.xml for state pages (optional)
- Internal linking to related hubs
