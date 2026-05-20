# Nuxt

> Maintained by NuxtLabs (now part of Vercel since July 2025). The Vue meta-framework that matches Next.js feature-for-feature, with a gentler learning curve.

## Latest Version

**4.4.6** (May 18, 2026) — Current stable (latest) ⚠️ Security release — upgrade immediately  
**3.21.6** (May 18, 2026) — Maintenance; EOL extended to **July 31, 2026**  
**Nuxt 5** — in active development; powered by **Nitro v3 beta** (released March 11, 2026); no stable release date confirmed yet

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
- **Nuxt UI v4** — fully open-source component library (100+ components) backed by Vercel; **v4.6** (March–April 2026) adds a new `Sidebar` component and AI Chat components (`ChatReasoning`, `ChatTool`, `ChatShimmer`) for building AI chat interfaces
- **Nuxt Agent** (beta, April 29, 2026) — official AI agent at nuxt.com; grounded in the Nuxt MCP server (official docs, modules catalog, blog, deployment guides, GitHub issues); built with the AI SDK and Nuxt UI; accessible via `⌘I` or `/chat`
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

## v4.4.6 / v3.21.6 (May 18, 2026) ⚠️ Security + Bug Fixes

- ⚠️ **Security advisory** — multiple vulnerabilities patched; `@nuxt/rspack-builder` also updated; teams on 4.4.5 or earlier should upgrade immediately
- `vite`: use SPA entry for vite-node fallback; invalidate SSR module cache when modules are invalidated via plugin hooks
- `nuxt`: match deduplicated `resolveComponent` calls in JSX blocks; prefer framework's own builder/server deps
- `nuxt`: update `useFetch` key even when `watch: false` is set; handle errors when fetching the app manifest
- `nitro`: mark `@babel/plugin-syntax-typescript` as optional peer dep; add `.json` extension to payload cache items
- Maintenance backport to **v3.21.6** with same fixes

## v4.4.5 / v3.21.5 Patch (May 10, 2026)

- Freeze head during island plugin phase (prevents edge-case head state mutation in SSR islands)
- Inline CSS imported from non-Vue JS modules (Vite config fix for third-party CSS imports)
- Maintenance patch for the v3.21.x line with same fixes backported

## v4.4.3/4.4.4 Patch (April 29, 2026)

- **Performance fixes** — Nitro: directly import `nuxt` package version; Vite/webpack: use vfs for manifest + vite node server; skip key watcher when `useAsyncData` key is static; batch-resolve TypeScript hoist paths with cached base roots
- **Parallelise module load + cache jiti instances** (`@nuxt/kit`) — faster startup in complex projects
- v4.4.4 was published immediately after v4.4.3 with no changes due to a release script issue; both are identical

## v4.4 Highlights (March 12, 2026)

- **Custom `useFetch`/`useAsyncData` factories** — `createUseFetch` / `createUseAsyncData` for project-specific fetch composables with shared configuration
- **Vue Router v5 upgrade** — upgraded from Vue Router v4; improved type safety and performance in routing
- **Built-in accessibility announcer** — new `useAnnouncer` composable + `<NuxtRouteAnnouncer>` automatically announces navigation for assistive technologies
- **Typed layout props** — layouts can now declare typed `defineProps` for strongly typed parent-to-layout communication
- **Better import protection** — server-only import violations now show a full **trace** of the import chain and copy-pasteable fix suggestions (inspired by TanStack Start)
- **View Transitions types** — TypeScript types for View Transitions API added
- **`useCookie` refresh option** — new `refresh` option in `useCookie` composable
- **`useState` reset to default** — new helper to reset state to its default value
- **Build profiling** — `nuxi analyze` / `nuxi build --profile` generates flame graphs and Chrome traces for bundle analysis
- **Smarter payload handling** — new `payloadExtraction: 'client'` mode inlines full payload in initial HTML (avoids double-render for ISR/SWR routes); runtime in-memory LRU payload cache; `'client'` mode will be default in `compatibilityVersion: 5`
- **`unrouting` migration** — file-system route generation now uses `unrouting` (trie-based); dev server route updates up to **28x faster** when not adding/removing pages; route generation deterministic regardless of file ordering
- **Performance improvements** — **14,000x faster module ID parsing** (replaced `new URL()` + regex with `indexOf`/slice); NuxtLink visibility prefetching disabled in dev to reduce unnecessary Vite restarts
- **Improved `optimizeDeps` hints** — Nuxt now shows a clear, copy-pasteable `nuxt.config.ts` snippet when Vite discovers new dependencies at runtime
- **Normalised page component names (experimental)** — more predictable component naming
- **Extended v3 support** — Nuxt v3 EOL extended from Jan 31, 2026 to **July 31, 2026**
- **Nuxt 5 preparation** — `main` branch will begin receiving Nuxt 5 (Nitro v3) commits; upgrade path via `future.compatibilityVersion: 5`

## Nitro v3 Beta (March 11, 2026) — Powers Nuxt 5

Nitro v3 entered public beta on March 11, 2026. It is the server engine that will power Nuxt 5 and represents the biggest Nitro update since its creation. ~280K weekly npm downloads already on the beta.

**New features:**
- **Rolldown + Vite 8 integration** — first-class support; replaces the old Rollup/Vite pipeline for significantly faster builds
- **H3 v2 with `srvx`** — web-standard request handling (`Request`/`Response`-first); leaner APIs
- **Built-in task runner** — define and run tasks (`server/tasks/*.ts`) via CLI or API
- **Scheduled cron jobs** — built-in cron support (`scheduledTasks` in Nitro config); adapts per platform (Node uses Croner; Cloudflare uses Cron Triggers)
- **Cross-environment WebSocket support** — unified WebSocket API across all deployment targets

**Breaking changes in Nitro v3:**
- Node 16 dropped
- App config functionality removed (moved to Nuxt layer)
- Default caching behavior changed

**Status:** Nuxt 5 will ship with Nitro v3 once it's stable. Teams can already experiment with Nitro v3 APIs directly. Follow progress at [github.com/nuxt/nuxt/discussions/34504](https://github.com/nuxt/nuxt/discussions/34504).

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
