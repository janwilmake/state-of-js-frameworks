# Changelog

> Framework releases, announcements, and major events, newest first. Maintained by the Framework Tracker agent.

---

## 2026-04-14 (run: April 14, 2026)

### React Router v7.14.1 (April 13, 2026)
- TypeScript 6 peer dependency support added to `@react-router/dev`
- Fix potential race condition in `HydrateFallback` rendering
- Normalize double-slashes in redirect paths
- **React Router v8 planning** — ESM-only, Node 20 dropped, RSC Framework Mode stabilization; expected sometime 2026

### React Router v7.14.0 (April 2, 2026)
- **Vite 8 support** added — aligns with Vite's ESM-first future
- Memory leak fix in `turbo-stream` encoding (`AbortSignal` listener not removed)
- Pre-rendering support for multiple server bundles via `v8_viteEnvironmentApi`
- Unstable RSC Framework Mode: pre-rendering + SPA mode, new route module exports, `<Link prefetch>` support

### Angular 21.2.x — Additional v21.2 Details
- **Prettier integration in Angular CLI** — new projects include Prettier as a dev dependency with `.prettierrc`; `ng generate` and `ng update` auto-format files
- **TypeScript 6 beta support** — `@angular/core` peer dep range now includes TypeScript 6 pre-releases
- **`ResourceSnapshot`** — new resource composition API for Signals
- **Location strategy trailing slash** — new trailing-slash location strategy option

---

## 2026-04-12 (run: April 12, 2026)

### Angular 21.2.8 (April 8, 2026)
- Patch release with bug fixes and stability improvements
- Latest stable on the 21.2.x line; all 21.x users should upgrade
- ⚠️ **Angular 19.x and 21.x active support both end May 19, 2026** — teams on v19 have ~5 weeks to migrate to v21; v21 then transitions to LTS (security patches until May 2027)

### Astro Together: London (April 9, 2026) 📣 Community Event
- Astro core team held a live showcase of new and upcoming Astro features
- Demonstrated future direction post-Astro 6.0
- Recordings expected on astro.build; watch for announcements from this event

---

## 2026-04-10 (run: April 10, 2026)

### Angular 21.2.7 (April 1, 2026)
- Patch release with stability and security fixes
- Latest stable on the 21.2.x line; all 21.x users should upgrade
- Angular 19.x LTS ends **May 19, 2026** — teams still on Angular 19 should plan migration to 21.x

### Nuxt UI v4.6.1 (April 3, 2026) / v4.6.0 (March 23, 2026)
- **New `Sidebar` component** — responsive application sidebar with three variants (`sidebar`, `floating`, `inset`) and three collapsible modes (`offcanvas`, `icon`, `none`)
- **New AI Chat components**: `ChatReasoning` (collapsible thinking blocks), `ChatTool` (tool invocation rows), `ChatShimmer` (streaming animation primitive) — integrate with the Vercel AI SDK
- Bug fixes for streaming detection and modal/slideover warnings

## 2026-04-08

### Next.js 16.2.3 (April 8, 2026) 🔒 Security Release
- **CVE-2026-23869** security vulnerability patched — all users on 16.x should upgrade immediately
- `next@16.2.3` and `next@15.5.15` both contain the security fix
- Additional bug fixes: stale ISR revalidation errors, HMR breakage with `manifest.ts`, styled-jsx race condition, asset deduplication

### SvelteKit 2.55.0 + Svelte 5.55.0 (April 2026)
- **Type-narrowed params with matchers** — route matcher-constrained params now properly type-narrowed in `$app/types`, `$app/state`, and hooks
- **New `svelte/motion` exports** — `TweenOptions`, `SpringOptions`, `SpringUpdateOptions`, `Updater` types now public
- **Best practices guide** — new official Svelte best practices documentation published

### SvelteKit 2.54.0 + Svelte 5.54.0 (April 2026)
- **Server-side error boundaries** — error boundaries now catch server-side errors during SSR (closes a long-standing gap)
- **`svelte.config.js` function options** — `css`, `runes`, `customElement` options can now be functions for conditional/per-file configuration
- **Svelte MCP for OpenCode** — `sv@0.12.6` includes OpenCode plugin config in `.opencode/` folder

### Astro 6.1.5 (April 8, 2026)
- UnoCSS revival in dev mode when used with client router
- Cloudflare `compatibility_date` now set to current date in `astro add cloudflare`
- Removed `dlv` dependency

---

## 2026-03-31

### What's New in Svelte: April 2026 Issue
- Monthly Svelte newsletter summarising all March/April changes
- Highlights: MCP in OpenCode, server-side error boundaries, config functions, type-narrowed params

---

## 2026-03-25

### Next.js Across Platforms: Adapters & OpenNext (March 25, 2026)
- Official blog post detailing the stable Adapters API introduced in 16.2
- OpenNext collaboration announced — shared tests across deployment providers
- Commitments to support AWS, Cloudflare, and other platforms as first-class targets

---

## 2026-03-18

### Next.js 16.2 (March 18, 2026) 🚀 Major Minor Release
- **~400% faster `next dev` startup** via Turbopack improvements
- **~50% faster rendering** (server-side)
- **Stable Adapters API** — platforms can customise the build process; enables OpenNext
- **Server Fast Refresh** — fine-grained hot reloading for server components
- **Browser Log Forwarding** — dev terminal shows browser errors; key for AI-agent debugging
- **Hydration Diff Indicator** — clear server/client diff in error overlay
- **`--inspect` for `next start`** — attach Node.js debugger to production server
- **Agent DevTools (experimental)** — AI agents get terminal access to React DevTools
- **`AGENTS.md` in `create-next-app`** — new projects scaffold with AI-ready config
- **`unstable_catchError()`** — component-level error boundaries
- **Redesigned default 500 error page**
- **SRI support for JS assets**
- **Tree shaking of dynamic imports**
- **Turbopack**: 200+ bug fixes, Web Worker Origin support, persistent cache improvements

---

## 2026-03-12

### Nuxt 4.4.0 / 4.4.2 (March 12, 2026)
- **Custom `useFetch`/`useAsyncData` factories** — project-specific fetch composables
- **Vue Router v5 upgrade** — from Vue Router v4; improved types and performance
- **Built-in accessibility announcer** — `<NuxtRouteAnnouncer>` for screen readers
- **Typed layout props** — `defineProps` in Nuxt layouts with full type safety
- **Build profiling** — improved `nuxi analyze` and `nuxi build --profile`
- **Smarter payload handling** — reduced payload size, better deduplication
- **Extended Nuxt 3 support** — EOL extended from Jan 31, 2026 to **July 31, 2026**
- **Nuxt 5 preview** — `main` branch will receive Nitro v3 commits; `future.compatibilityVersion: 5` available for early adopters

### Nuxt 3.21.2 (March 12, 2026)
- Maintenance release with backports from Nuxt 4.3

---

## 2026-03-10

### Astro 6.0 (March 10, 2026) 🚀 Major Release
- **Redesigned `astro dev`** — rebuilt on Vite's Environment API; production runtime in development
- **First-class Cloudflare Workers support** — Cloudflare Vite plugin integration
- **Built-in Fonts API** — zero-config font loading and optimization
- **Live Content Collections (stable)** — real-time external content via unified content layer
- **Content Security Policy (stable)** — first meta-framework with built-in CSP; auto-hashing
- **Experimental Rust compiler** — successor to Go compiler; early impressive results
- **Experimental Queued Rendering** — controlled rendering queue for large static builds
- **Experimental Route Caching** — cache route data across builds
- **Node.js 22+ required** (breaking change)
- **`Astro.glob()` removed** (breaking change)
- **Zod 4 upgrade** (breaking change for Content Collections)
- **`Astro.locals.runtime` removed** from Cloudflare adapter (breaking change)

---

## 2026-02-27

### Angular 21.2.0 (February 23, 2026)
- **Arrow functions in templates** — inline arrow functions in component templates
- **Exhaustive `@switch` type-checking** — compiler validates switch completeness
- **`ChangeDetectionStrategy.Eager`** — new strategy optimized for Signals-based components
- **Signal Forms improvements** — `FormRoot`, `transformedValue`, enhanced composability

---

## 2026-02-12

### Next.js: Building for an Agentic Future (February 12, 2026)
- Blog post from Vercel outlining Next.js direction for AI agents
- Preview of `next-browser` experimental package
- Strategy for browser log forwarding and agent-accessible DevTools

---

## 2026-01-22

### Nuxt 4.3.0 (January 22, 2026)
- Various improvements to developer experience and type safety
- Foundation for 4.4's custom fetch factories

---

## 2026-01-16

### Cloudflare Acquires Astro (January 16, 2026) 📣 Major Announcement
- All full-time Astro employees join Cloudflare
- Framework remains MIT-licensed; all platforms still supported
- Astro Ecosystem Fund (Webflow, Netlify, Wix, Sentry, Stainless) continues
- First major output: `workerd` integration in Astro 6 dev server
- Astro positioned as reference implementation for Cloudflare edge content sites

---

## 2026-01-14

### Angular 21.1.0 (January 14, 2026)
- Minor release with bug fixes and improvements following v21.0 launch

---

## 2025-11-19

### Angular 21.0.0 (November 19, 2025) 🚀 Major Release
- **Signal Forms developer preview** — new signal-based form API
- **Angular MCP Server** — AI-assisted development with Cursor and Claude Code
- **Angular Aria developer preview** — built-in accessibility utilities
- **Signals formatter** in Angular DevTools
- **Regular expressions in templates**
- **CLDR v47 upgrade**
- **CDK Drag&Drop improvement** — copy items between lists
- **Route visualization and Signal graph** in Angular DevTools

---

## 2025-10-21

### Next.js 16.0.0 (October 21, 2025) 🚀 Major Release
- Turbopack stable for `next dev`; production build beta
- React 19 required
- Caching improvements and routing enhancements
- Partial Prerendering (PPR) stabilization progress
- Current LTS major

---

## 2025-07-16

### Nuxt 4.0.0 (July 16, 2025) 🚀 Major Release
- Improved project organization (`app/` directory convention)
- Smarter data fetching
- Better type safety throughout
- All `compatibilityVersion: 4` features stabilized

### NuxtLabs Joins Vercel (July 2025)
- NuxtLabs team joins Vercel
- Nuxt UI v4 released as fully open-source (100+ components)
- Development investment increased

---

## 2024-11-01

### React Router v7.0.0 (November 2024) 🚀 Major Release
- **Remix features merged into React Router** — loaders, actions, SSR, nested routing
- Framework Mode enables full-stack Remix-style development
- Recommended upgrade path for all Remix v2 projects
- Shopify backing confirmed

---

## 2024-01-13

### Astro 5.0 (January 2025)
- Content Layer API stable
- Server Islands stable
- Simplified deployment model

---

_Older entries archived. This log covers significant releases and announcements from 2024 onward._
