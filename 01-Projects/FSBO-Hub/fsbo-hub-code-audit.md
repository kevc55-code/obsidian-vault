# FSBO-Hub Code Audit — 2026-06-26

## 🔴 Fix Before Next Push (Rule Violations Live in Prod)

### 1. Moving Labor Brokers is rendering on every state guide page
- File: `src/components/StateGuideAffiliates.tsx` line 19
- `<AffiliateCTA affiliate="movinglaborbrokers" />` is live
- Your rule: "NOT rendered anywhere until placement is decided"

### 2. Rocket Money banner is live on every metro page
- File: `src/app/[metro]/page.tsx` line 166
- `<AffiliateCTA affiliate="rocketmoney" variant="banner" />` rendering under Net Proceeds Calculator
- Your rule: "DO NOT accept $0 contract from Impact for Rocket Money"
- If you haven't signed a contract, this link earns nothing and shouldn't be live

---

## 🔶 SEO Gaps (Revenue/Traffic Impact)

### 3. 21 state guide pages missing
You have 30 of 50 states. Missing:
Alaska, Arkansas, Connecticut, Delaware, Hawaii, Idaho, Iowa, Kansas, Maine, Mississippi, Montana, New Hampshire, New Jersey, North Dakota, Rhode Island, South Carolina, South Dakota, Vermont, West Virginia, Wisconsin, Wyoming

### 4. 3 affiliates with no tracking links
These go direct to merchant homepages — zero attribution:
- `1800gotjunk` → https://www.1800gotjunk.com/ (commission: TBD)
- `nolo` → https://www.nolo.com/ (commission: TBD)
- `virtuance` → https://www.virtuance.com/ (commission: "% of sale")

You're sending traffic for free. Either get affiliate links or remove from the stack until enrolled.

---

## 🔶 Config / Infra

### 5. next.config.js is empty
```js
const nextConfig = {}
module.exports = nextConfig
```
Missing: `output: 'export'`, `trailingSlash: true`, `images: { unoptimized: true }`
Will fail CF Pages build if you ever migrate. Fix now so it's ready.

### 6. SUPABASE_SERVICE_ROLE_KEY unconfirmed in Netlify
Leads form and subscribe form silently fail if missing. Verify in Netlify dashboard → Site settings → Environment variables.

### 7. 136 uncommitted local changes
Full blog expansion (236 posts) + buyer/investor state page work is sitting locally undeployed.

---

## ✅ Already Clean
- IndexNow HOST — correctly set to `fsbo.byownerhub.com`
- HireAHelper link — live with correct affiliate URL
- Angi CJ links — wired into checklist items with tracking pixels
- Supabase lazy client — won't crash at build time if env vars missing
