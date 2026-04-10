# Nuxt

> Maintained by NuxtLabs (now part of Vercel since July 2025). The Vue meta-framework that matches Next.js feature-for-feature, with a gentler learning curve.

## Latest Version

**4.4.2** (March 12, 2026) — Current stable (latest)  
**3.21.2** (March 12, 2026) — Maintenance; EOL extended to **July 31, 2026**  
**Nuxt 5** — in early development; targets Nitro v3 upgrade; no release date confirmed

## Key Features

- **Nuxt 4 (stable since July 2025)** — improved project organization (`app/` directory), smarter data fetching, better type safety
- **Auto-imports** — components, composables, and utilities auto-imported; zero boilerplate
- **Nitro server engine** — powers SSR, SSG, edge functions, and API routes; Nitro v2 in Nuxt 4
- **Universal rendering** — SSR, SSG, hybrid, SPA, and ISR (via `routeRules`) in a single config
- **`useFetch` / `useAsyncData`** — composables for server/client data fetching with automatic deduplication
- **Custom `useFetch` / `useAsyncData` factories** (new in 4.4) — create project-specific fetch composables
- **Vue Router v5** (new in 4.4) — upgraded from Vue Router v4
- **Accessibility announcer** (new in 4.4) — built-in route-change announcements for screen readers
- **Typed layout props** (new in 4.4) — type-safe props for Nuxt layouts
- **Build profiling** (new in 4.4) — `nuxi build --profile` for bundle analysis
- **Nuxt UI v4** — fully open-source component library (100+ components) backed by Vercel
- **NuxtLabs joins Vercel** (July 2025) — Nuxt now part of the Vercel ecosystem; development accelerated

## Rendering Modes

| Mode | Description |
|---|---|
| SSR | Per-request server rendering (default) |
| SSG | Static generation at build time via `nuxt generate` |
| ISR | Per-route revalidation via `routeRules: { '/path': { isr: 60 } }` |
| SPA | Client-only via `ssr: false` or per-route `routeRules` |
| Hybrid | Mix SSR/SSG/ISR/SPA per-route via `routeRules` in `nuxt.config.ts` |
| Edge SSR | Deploy SSR to Cloudflare Workers, Vercel Edge, Deno via Nitro |

The `routeRules` hybrid model is one of Nuxt's strongest differentiators — no other framework makes per-route rendering strategy this ergonomic.

## Deployment Targets

- **Vercel** — native (NuxtLabs is now part of Vercel); zero-config deployment
- **Cloudflare Workers / Pages** — via Nitro Cloudflare preset
- **Netlify** — via Nitro Netlify preset
- **Node.js** — `nuxt build` + `node .output/server/index.mjs`
- **Static** — `nuxt generate` → CDN/S3
- **AWS Lambda** — via Nitro AWS preset
- **Bun** — via Nitro Bun preset (experimental)
- **Deno Deploy** — via Nitro Deno preset

Nitro's preset system means Nuxt can deploy virtually anywhere. One codebase, many targets.

## v4.4 Highlights (March 12, 2026)

- **Custom `useFetch`/`useAsyncData` factories** — define project-specific fetch composables with shared configuration
- **Vue Router v5 upgrade** — improved type safety and performance in routing
- **Built-in accessibility announcer** — `<NuxtRouteAnnouncer>` automatically announces navigation for assistive technologies
- **Typed layout props** — layouts can now declare typed `defineProps` for strongly typed parent-to-layout communication
- **Build profiling** — `nuxi analyze` / `nuxi build --profile` improvements
- **Smarter payload handling** — reduced payload size, better deduplication
- **Extended v3 support** — Nuxt v3 EOL extended from Jan 31, 2026 to **July 31, 2026**
- **Nuxt 5 preparation** — `main` branch will begin receiving Nuxt 5 (Nitro v3) commits; upgrade path via `future.compatibilityVersion: 5`

## npm Download Trend

Nuxt is the dominant Vue meta-framework with no real competitors. Vue's ecosystem (~5–6M weekly downloads for Vue core) feeds directly into Nuxt adoption. Nuxt download numbers have grown steadily, particularly in European enterprise teams who prefer Vue's gentler learning curve over React. The NuxtLabs/Vercel acquisition should accelerate tooling investment.

## Trade-Off Assessment

**Choose Nuxt when:**
- Your team knows or prefers Vue over React
- You want the ergonomic `routeRules` hybrid rendering system
- You need a first-class component library (Nuxt UI v4 is excellent)
- You're building content-heavy sites that benefit from auto-imports and zero boilerplate
- You want flexible deployment without vendor lock-in (Nitro presets)

**Watch out for:**
- **Smaller ecosystem than Next.js** — fewer third-party integrations, less Stack Overflow content
- **Nuxt 5 is coming** — teams starting projects today should evaluate compatibility mode (`future.compatibilityVersion: 5`) to smooth eventual migration
- **Vercel acquisition concerns** — NuxtLabs is now part of Vercel; while Nuxt remains open-source, long-term independence is less certain than before
- **Auto-imports magic** — powerful but can confuse IDEs and make code harder to debug in complex projects; explicit imports are always an option

## Support Policy

| Release | Status | EOL |
|---|---|---|
| 4.x | Stable (Active Development) | 6 months after Nuxt 5 release |
| 3.x | Maintenance (security + critical bugs) | July 31, 2026 |
| 2.x | Unsupported (commercial via HeroDevs NES) | June 30, 2024 |
