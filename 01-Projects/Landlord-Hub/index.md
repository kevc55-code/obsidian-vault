---
tags: [project, landlord, active]
project: Landlord-Hub
status: active
stack: Next.js 14, TypeScript, Tailwind
updated: 2026-04-09
---

# Landlord Hub

Active landlord affiliate site. State landlord laws, tools, and property management resources.

## Status
54 static pages built (homepage + 50 states + 2 Next.js internals). Builds clean.

## Hero
"Manage Your Rental Property Without Overpaying for Software"

## Tech Stack
- Framework: Next.js 14.2.3 (App Router)
- Language: TypeScript
- Styling: Tailwind CSS + custom colors (navy: #0D1B2A, teal: #1B7FA3, gold: #E8A838, slate: #4A5568)
- Deploy: Netlify (@netlify/plugin-nextjs in netlify.toml) — not yet connected
- No DB — static data layer

## Repo
`C:\Users\kevc_\Documents\GitHub\landlord-hub` — branch: `main`

## Data Layer
- `src/lib/states.ts` — all 50 states: security deposit limit, notice-to-quit days, rent control status (statewide/city-only/none/banned, color-coded badge), required disclosures, eviction timeline, EZ Landlord Forms deep link per state
- EZ Landlord Forms URL pattern: `ezlandlordforms.com/documents/residential-lease-agreement/[state]-lease-agreement/?via=landlordhub` — not yet verified against live site
- `src/lib/tools.ts` — affiliate tools by category
- `src/app/[state]/page.tsx` — SSG with generateStaticParams() + generateMetadata()
- Affiliate links: `?via=landlordhub` — lead pick: TurboTenant

## Open Items
- Netlify deployment not yet connected
- EZ Landlord Forms deep-link URL pattern needs verification
- SEO meta tags not verified against search intent
- State law data accuracy review not done
- sitemap.xml for state pages (optional)
- Internal linking to related hubs
