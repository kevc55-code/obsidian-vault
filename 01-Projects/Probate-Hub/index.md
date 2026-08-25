---
tags: [project, probate, active]
project: Probate-Hub
status: active
stack: Next.js 14, TypeScript, Tailwind
updated: 2026-04-09
---

# Probate Hub

Inherited property / probate real estate affiliate site.

## Status
54 static pages built (homepage + 50 states + 2 Next.js internals). Builds clean.

## Hero
"Sell an Inherited Property Without the Overwhelm"

## Tech Stack
- Framework: Next.js 14.2.3 (App Router)
- Language: TypeScript
- Styling: Tailwind CSS + custom colors (navy: #0D1B2A, teal: #1B7FA3, gold: #E8A838, slate: #4A5568)
- Deploy: Netlify (@netlify/plugin-nextjs in netlify.toml) — not yet connected
- No DB — static data layer

## Repo
`C:\Users\kevc_\Documents\GitHub\probate-hub` — branch: `main`

## Data Layer
- `src/lib/states.ts` — all 50 states: small estate threshold + note, attorney required, avg timeline, key forms with statute citations, court finder URL
- `src/lib/tools.ts` — affiliate tools by category (List the Property, Legal & Probate Forms, Estate Sale Services)
- `src/app/[state]/page.tsx` — SSG with generateStaticParams() + generateMetadata()
- Affiliate links: `?via=probatehub` — lead pick: Houzeo (flat-fee MLS)

## Open Items
- Netlify deployment not yet connected
- SEO meta tags not verified against search intent
- State law data accuracy review not done
- sitemap.xml for state pages (optional)
- Internal linking to related hubs
