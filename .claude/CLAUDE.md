---
tags: [meta, context, claude]
updated: 2026-04-13
---

# Kevin — Project Context for Claude

## About Me
- Name: Kevin
- Role: Senior PM — energy, IoT, building optimization background
- Location: Basel, Switzerland (tri-border region CH/FR/DE)
- Entity: Wyoming LLC (consulting + side projects)
- Bank: Mercury

## Active Projects

### FSBO Hub / SkipTheAgent.com
- Domain: skiptheagent.com (fully renamed in all src files — contact email hello@skiptheagent.com still needs updating in Resend config + Netlify env vars)
- Repo: C:\Users\kevc_\Documents\GitHub\fsbo-hub
- Stack: Next.js 14.2.3 + TypeScript + Tailwind CSS + Supabase + Resend
- Deploy: Netlify via deploy.bat — NEVER use Vercel for this project
- Branch: main — commit 03abbda pushed 2026-04-13, Netlify deploy triggered
- Markets: 16 metros live (Boston, Chicago, Dallas-Fort Worth, Phoenix, Miami, Austin, Houston, Atlanta, Minneapolis–St. Paul, Philadelphia, Pittsburgh, Seattle, Denver, Tampa, Charlotte, Nashville)
- Model: Affiliate revenue (flat-fee MLS, movers, legal, storage)
- Forms: TWO systems — (1) src/lib/data.ts → Disclosures.tsx (live, older system, download_url field); (2) src/lib/forms.ts → FormsLibrary.tsx (newer, 111 forms, url + url_alt). Both now render on metro pages. eforms.com/images/ is primary source; esign.com wp-content/uploads/ is browser-broken — never use as primary url. Member-only forms use url: null.
- Open: Next.js upgrade to 14.2.35 (CVE-2025-55182); audit url_alt esign.com links; wire real affiliate URLs; update Resend/Netlify email config (env var still has old fsbohub.com address)

### FRBO Hub
- Repo: C:\Users\kevc_\Documents\GitHub\frbo-hub
- Stack: Next.js 14.2.3 + TypeScript + Tailwind CSS, @netlify/plugin-nextjs
- Status: 54 static pages built (homepage + 50 states). Netlify not yet connected.
- Model: Affiliate (for-rent-by-owner — lease tools, tenant screening)
- Lead pick: TurboTenant

### FTB Hub
- Repo: C:\Users\kevc_\Documents\GitHub\ftb-hub
- Stack: Next.js 14.2.3 + TypeScript + Tailwind CSS, @netlify/plugin-nextjs
- Status: 54 static pages built (homepage + 50 states). Netlify not yet connected.
- Model: Affiliate (first-time buyers — DPA programs, mortgage, inspection, insurance)
- Lead pick: Better Mortgage

### Landlord Hub
- Repo: C:\Users\kevc_\Documents\GitHub\landlord-hub
- Stack: Next.js 14.2.3 + TypeScript + Tailwind CSS, @netlify/plugin-nextjs
- Status: 54 static pages built (homepage + 50 states). Netlify not yet connected.
- Model: Affiliate (active landlords — property management, tenant screening)
- Lead pick: TurboTenant
- Note: EZ Landlord Forms deep-link URL pattern not yet verified

### Probate Hub
- Repo: C:\Users\kevc_\Documents\GitHub\probate-hub
- Stack: Next.js 14.2.3 + TypeScript + Tailwind CSS, @netlify/plugin-nextjs
- Status: 54 static pages built (homepage + 50 states). Netlify not yet connected.
- Model: Affiliate (inherited property / probate sales — flat-fee MLS, legal forms, estate sales)
- Lead pick: Houzeo

### DirtPulse
- Stack: Next.js / Cloudflare

### Frontalier
- Stack: Next.js / Vercel

### OpenClaw
- Stack: WSL-based

### Consulting
- Senior PM consulting — energy, IoT, building optimization
- Covered under Wyoming LLC

## Key Conventions
- FSBO Hub deploys via deploy.bat to Netlify — never Vercel
- Check git log before assuming current state
- Prefer concise updates
- All hub sites share same pattern: Next.js App Router, static data layer (states.ts + tools.ts), [state] dynamic route

## Personal Context
- French: A1 level, targeting B2
- MTB: 2015 Trek Remedy 9 29er, Alps riding
- Obsidian vault: C:\Users\kevc_\Documents\ObsidianVault\
