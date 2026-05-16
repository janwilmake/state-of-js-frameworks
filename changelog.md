# Changelog

> Framework releases, announcements, and major events, newest first. Maintained by the Framework Tracker agent.

---

## 2026-05-16 (run: May 16, 2026)

### Angular 19 EOL Imminent — 3 Days Away (May 19, 2026) ⚠️

- **Angular 19.x reaches official end-of-life on May 19, 2026** — now just 3 days away. Google will issue **no further security patches, bug fixes, or updates** for any Angular 19.x release after this date. Teams still running Angular 19 in production are operating unsupported software.
- **Angular 21.x active support also ends May 19, 2026** — Angular 21 transitions to LTS status (security-only patches until May 19, 2027). No new features will ship on the v21 line.
- **Angular 22 targeted for the week of June 1, 2026** — 16 days away; currently at `22.0.0-next.12` canary (May 8). Expected features: stable Signal Forms, selectorless components, OnPush as default for new projects, Zoneless as default for new projects, Vitest migration tool promoted to stable.
- **No new stable releases across any major framework** since May 14: latest stable versions remain Next.js 16.2.6, React Router v7.14.1, Nuxt 4.4.5, SvelteKit 2.59.1, Astro 6.3.2, Angular 21.2.12.

### SvelteKit "What's New in Svelte: May 2026" (May 1, 2026)

- Official monthly Svelte recap published; highlights already captured in prior runs:
  - TypeScript 6.0 support (`kit@2.56.0`)
  - Community add-ons in the `sv` CLI (experimental) — first batch of community-contributed CLI plugins
  - Remote Functions: `form.submit()` returns `boolean` (`kit@2.57.0`), `field.as(type, value)` defaults
  - Svelte featured in the May 2026 **ThoughtWorks Technology Radar** (Adopt tier)

---

## 2026-05-14 (run: May 14, 2026)

### Astro 6.3 (May 7, 2026) + 6.3.2 patch (May 13, 2026) 🚀 New Minor

- **Experimental Advanced Routing** — the headline feature of 6.3; full control over the request pipeline via a `FetchState`-based app entry point (`src/app.ts`); compose handlers, proxy paths to external services, and use any fetch-handler-style framework (e.g., **Hono**); follows the same pattern as Cloudflare Workers, Deno, and Bun
  ```ts
  import { FetchState, astro } from 'astro/fetch';
  export default {
    fetch(request: Request) {
      const state = new FetchState(request);
      if (state.url.pathname.startsWith('/api')) {
        return fetch(new URL(state.url.pathname, 'https://api.example.com'));
      }
      return astro(state);
    }
  };
  ```
- **Support redirects on external image URLs** — Astro now follows 3xx redirects when fetching external images
- **SVG image processing disabled by default** — SVG files are no longer processed through the image pipeline by default; opt in with `image.svg: true`
- **New `AstroCookies.consume()` instance method** — replaces the deprecated static version; marks cookies consumed and returns `Set-Cookie` header values
- **6.3.2 patch** (May 13) — rejects double-encoded URL paths with 400 response; fixes `&` entity rendering in `<meta>` tags; fixes `assetsPrefix` missing on build config events
- **~2.73M weekly npm downloads** — significant growth from ~1.33M in March 2026; Astro is now within reach of Angular and SvelteKit in raw download volume

---

### Nuxt 4.4.5 / 3.21.5 (May 10, 2026)

- Freeze head during island plugin phase — prevents edge-case head mutation bug in components islands during SSR
- Inline CSS imported from non-Vue JS modules — Vite config fix for third-party CSS import edge cases
- Maintenance backport to v3.21.5 for the same fixes
- **Latest stable: `npm install nuxt@latest` → 4.4.5**

---

### SvelteKit 2.59.1 / 2.59.0 (May 5, 2026)

- **`RemoteCommand` output type fix** — `Promise` wrapper correctly unwrapped in output type inference
- **`form.fields.foo.as('checkbox', default_value)` fix** — default value now correctly applied for checkbox fields
- **Remote form default value reset** — forms with `field.as('text', defaultValue)` now correctly reset to the provided default value after submission (not to null)
- **Queries correctly started** — edge case where queries could fail to initialize resolved
- **Plain functions as overrides** — `updates` now accepts plain functions as overrides (not just factory functions)
- **Windows drive-letter path fix** (2.59.1) — resolves paths to route files containing a Windows drive letter correctly
- **Latest stable: `npm install @sveltejs/kit@latest` → 2.59.1**

---

### Angular 22 — Signal Forms Officially Confirmed STABLE (May 6, 2026)

- The Angular team (via angular.love and the Angular DevKit team) **officially confirmed** that Signal Forms will ship as **stable** in Angular 22 (week of June 1, 2026)
- This is the biggest Angular forms news since Reactive Forms in v6 — Signal Forms provide fine-grained per-field updates instead of full-form invalidation, aligning perfectly with Zoneless change detection
- ⚠️ **Angular 19.x EOL is May 19, 2026** — now only 5 days away; teams still on Angular 19 must upgrade to 21.x immediately
- Angular 22.0.0-next.12 (May 8, 2026) — latest canary continues active pre-release development

---

## 2026-05-12 (run: May 12, 2026)

### Angular 21.2.12 (May 6, 2026) — Latest Stable Patch

- **Signal input transform read-generic** — allow explicit `read` generic with signal input transforms for better type inference on transformed values
- **i18n flags no longer leak on errors** — fixed a bug where i18n flags propagated incorrectly on error paths
- **`ngSkipHydration` fix for LContainers** — SSR non-destructive hydration now correctly respects `ngSkipHydration` on components with projectable nodes inside `LContainer`
- **Sanitizer typings** — improved type signatures for the DOM sanitizer APIs
- **Security** — validate security-sensitive attributes in i18n bindings
- **Signal Forms: prohibit concurrent submits** — race condition fix; submitting a signal form while a submission is already in-flight is now blocked
- 📋 **22.0.0-next.12** (May 8, 2026) — latest pre-release canary; Angular 22 development actively progressing toward the June 1, 2026 stable target

---

### SvelteKit 2.58.0 (April 23, 2026) — `requested` API Stabilized

- **`requested` API finalized (breaking for 2.56/2.57 users)** — `requested` in remote query handlers now requires a `limit` option (as originally designed) and yields `{ arg, query }` entry objects instead of validated arguments directly; `RemoteQueryFunction` type gains an optional third generic `Validated` representing the post-validation argument type
- **FOUC fix for CSR-only pages** — styles and fonts are now loaded before client-side rendering starts, eliminating Flash of Unstyled Content
- **Form result reset on redirect** — form action results are correctly cleared when the response is a redirect
- **`resolve()` external URL guard** — calling `resolve` with an external URL now throws an error instead of silently misbehaving
- **SSI comment false-positive fix** — server-side include HTML comments (`<!-- virtual="..." -->`) no longer trigger false Svelte hydration mismatch warnings in `transformPageChunk`
- **`RemoteFormFields` nullable array typing** — correct type restored for nullable array fields when using `.as('checkbox')`

---

### Nitro v3 Beta (March 11, 2026) — Powers the Future Nuxt 5

- **Nitro v3 beta released** — ~280K weekly npm downloads already on the beta; adopted by TanStack Start, Vercel Workflows, and production apps like T3Chat
- **New features**: Rolldown + Vite 8 integration, H3 v2 with `srvx` (web-standard `Request`/`Response`), built-in task runner (`server/tasks/`), scheduled cron jobs, cross-environment WebSocket support
- **Breaking changes**: Node 16 dropped, app config removed, default caching behavior changed
- **Nuxt 5 dependency**: Nuxt 5 will ship with Nitro v3 and H3 v2; teams can prepare via `future.compatibilityVersion: 5` in Nuxt 4
- Progress tracked at [github.com/nuxt/nuxt/discussions/34504](https://github.com/nuxt/nuxt/discussions/34504)

---

## 2026-05-10 (run: May 10, 2026)

### Next.js 16.2.6 / 15.5.18 (May 7, 2026) 🔒 Critical Security Release

⚠️ **UPGRADE IMMEDIATELY** — This coordinated release addresses **13 security advisories** across denial of service, middleware/proxy bypass, SSRF, cache poisoning, and XSS. One advisory (CVE-2026-23870) is an upstream React Server Components vulnerability.

**Key CVEs:**
- **CVE-2026-23870** (High) — DoS in React Server Components; also patched in `react-server-dom-*` 19.0.6, 19.1.7, 19.2.6
- **CVE-2026-44574** (High) — Middleware/proxy bypass via dynamic route parameter injection; **no WAF mitigation possible**
- **CVE-2026-44578** (High) — SSRF in applications handling WebSocket upgrade requests
- **CVE-2026-44581** (High) — XSS via CSP nonces in App Router applications
- Middleware bypass via App Router segment-prefetch (GHSA-267c-6grr-h53f) and Pages Router i18n
- DoS via Cache Components connection exhaustion (GHSA-mg66-mrh9-m8jx) and Image Optimization API
- Additional cache poisoning and XSS vectors

**Critical note:** Vercel explicitly states WAF rules are **not sufficient** mitigation — patching is the only fix. Next.js 13.x and 14.x are affected with **no patches planned**; users must upgrade to 15.5.18 or 16.2.6.

```bash
npm install next@latest   # installs 16.2.6 (or pin to 15.5.18 for LTS)
```

---

### Angular 19 Reaches EOL (May 19, 2026)

- Angular 19.x officially reached end-of-life on **May 19, 2026**
- Google will no longer ship security patches, bug fixes, or updates for 19.x
- Teams still on Angular 19 are now running unsupported software; migrate to Angular 21 immediately
- **Angular 21.x active support also ended May 19, 2026** — v21 transitions to LTS (security patches only until May 2027)
- **Angular 22 expected week of June 1, 2026** — selectorless components, stable Signal Forms, OnPush as default, Zoneless as default for new projects, TypeScript 5.9 support

---

### Remix 3 Beta Preview (April 30, 2026) + New Brand (May 6, 2026)

- **Remix 3 beta preview released April 30, 2026** — the first testable release of the ground-up Preact-based rebuild
  - Full-stack batteries included: routes, middleware, sessions, auth, forms, uploads, database management, UI components, testing — one dependency
  - "Unbundling" philosophy — runtime is the source of truth; no pre-runtime bundle analysis step; explicitly designed to work well with AI coding agents
  - `npx remix@next new` to scaffold a project
  - **Not production ready**; no migration path from Remix v2 or React Router v7
- **A Brand New Remix (May 6, 2026)** — new remix.run website launched; built on Remix 3 alpha itself (no React on the site); features a Three.js + GLSL shader particle cloud

---

### Nuxt 4.4.4 / 4.4.3 (April 29, 2026)

- Patch release with performance improvements: Nitro direct import of `nuxt` package version, vfs manifest + vite node server, 14,000× faster module ID parsing via cached roots, parallelised module load with cached jiti instances
- v4.4.4 published immediately after v4.4.3 with no code changes (release script issue)
- **Nuxt 3.21.4** — corresponding maintenance backport for v3

---

### Nuxt Agent Beta (April 29, 2026) 🤖 New Feature

- Official AI agent at **nuxt.com** launched in Beta
- Grounded in the Nuxt MCP server (official docs, modules catalog, blog, deployment guides, GitHub issues across `nuxt`, `nuxt-modules`, `nuxt-content`)
- Built using the Vercel AI SDK and Nuxt UI components; accessible via `⌘I` on any nuxt.com page or at `/chat`
- Has native tools rendering as UI: module/template cards, hosting provider cards, blog post previews, StackBlitz playground links, GitHub issue search
- Web search via Anthropic's `web_search` used as a fallback only (not for doc-answerable questions)
- Plans: user accounts, persistent chat history, deeper site integration

---

### Astro 6.2 (April 30, 2026) + Astro 7 Alpha

- **Astro 6.2.0 released April 30, 2026**:
  - **SVG optimizer** (`experimental.svgOptimizer`) — pass imported SVGs through configurable Svgo
  - **Experimental Logger** — structured JSON output; integrates with AI coding agents and log aggregation
  - **Experimental `getFontFileURL()`** — resolve font file URLs from `fontData` for Satori OG image generation
  - **`allowedHosts` for preview servers** — forwarded to adapter preview; prevents DNS rebinding attacks
  - **`"jsx"` option for `compressHTML`** — JSX whitespace rules for consistent `.astro`/`.tsx` behavior
- **Astro 7.0.0-alpha.0 released April 30, 2026** (pre-release, not production ready):
  - **Vite 8 upgrade** — breaking for integrations depending on Vite internals
  - **Rust compiler is now the default and only compiler** — Go compiler removed; `experimental.rustCompiler` flag no longer needed; faster and more strict (unclosed HTML tags now throw errors)
  - `npm install astro@alpha` to test
- **Astro 6.2.2** (May 4, 2026) — patch: fix head metadata propagation in dev for Cloudflare adapter; fix build crash on animated AVIF images

---

### SvelteKit 2.57.0 / 2.56.0 (May 2026)

- **`query.live()` — Real-time streaming queries** — `query.live()` uses async generators to stream continuous updates from server to client; shared connection across component instances; `connected` property and `reconnect()` method; passive exponential-backoff reconnection; SSR returns the first yielded value and closes the stream
- **`form.submit` returns `boolean`** (2.57.0) — indicates submission validity for enhanced remote form functions
- **TypeScript 6.0 support** (2.56.0) — SvelteKit now supports TypeScript 6.0
- **Remote Functions breaking changes (2.56.0)**:
  - `run()` method added to queries; awaiting queries outside render is now disallowed
  - `hydratable` transport for richer data types in query results
  - Client-requested query refreshes must obtain server permission
  - `field.as(type, value)` for default form field values
  - `requested` now requires `limit` and yields `{ arg, query }` entries
- **Svelte CLI Community Add-ons** (experimental) — community-contributed `sv` plugins now supported
- **Svelte featured in ThoughtWorks Technology Radar** (May 2026) — in the "Adopt" section

---

## 2026-04-18 (run: April 18, 2026)

### Next.js 16.2.4 (April 15, 2026)
- Bug-fix backport patch; does **not** include canary features
- **Turbopack fixes**: Windows ARM64 Google Fonts fix (bumped `reqwest` to 0.13.2), filesystem watcher `follow_symlinks` config now correctly applied
- **Compiler fix**: `next.config` `defines` now supports boolean and number primitives (previously string-only)
- **Pages Router**: Safari `?ts=` cache-buster scoped to CSS/font assets only (was incorrectly applied to all assets)
- **Turbopack stability**: fixed recomputation loop via cell cleanup on error, shorter error messages for two internal graph operations
- Latest stable on the 16.x line; all 16.x users should upgrade

### Next.js 16 — Notable Features Recap (captured from v16.0 blog)
- **`middleware.ts` deprecated → `proxy.ts`** — rename clarifies network boundary; `proxy` runs in Node.js runtime only; `middleware.ts` with `edge` runtime continues to work
- **Cache Components** — replaced experimental PPR (`experimental.ppr`); uses `"use cache"` directive; enables static shells with streamed dynamic content
- **React Compiler (stable)** — auto-memoizes components at compile time (zero manual `useMemo`/`useCallback`); enabled via `reactCompiler: true`; follows React Compiler 1.0 stable release
- **React 19.2** — View Transitions, `useEffectEvent`, `Activity` (hide UI with `display:none` while maintaining state)
- **Turbopack default** — now default bundler for all new projects (dev + production); 2–5× faster production builds; 10× faster Fast Refresh

### Nuxt 4.4 — Additional Performance Details (from official blog post)
- **`unrouting` migration** — file-system route generation now uses `unrouting` (trie-based data structure); dev server route updates up to **28× faster** when not adding/removing pages; ~15% faster even when adding/removing; route generation is now deterministic (no longer sensitive to file ordering)
- **Smarter payload handling** — new `payloadExtraction: 'client'` experimental mode inlines full payload in initial HTML; avoids a second lambda spin-up for ISR/SWR cached routes in serverless environments; runtime in-memory LRU payload cache; `'client'` mode becomes default in `compatibilityVersion: 5`
- **14,000× faster module ID parsing** — single `indexOf` + slice replaces `new URL()` + regex chain; NuxtLink visibility prefetching disabled in dev (reduces unnecessary Vite dep-discovery restarts)

---

## 2026-04-16 (run: April 16, 2026)

### Angular 22 — Official Release Date Confirmed
- Angular's official release schedule at `angular.dev/reference/releases` confirms **v22.0 week of June 1, 2026**
- **Angular roadmap clarifications** (from `angular.dev/roadmap`):
  - **Zoneless change detection** is now listed as **production ready** in v21 — no longer "opt-in experimental"
  - **OnPush as default** — RFC is open ([GitHub discussion #66779](https://github.com/angular/angular/discussions/66779)); v22 will flip the default
  - **Vitest as primary test runner** — stable in v21; v22 will promote the Karma→Vitest migration guide to stable
  - **`httpResource`** and **Signal Forms** — listed as "available to experiment with"; both expected to mature or stabilize in v22
  - **Selectorless components** — confirmed on roadmap; simplify component consumption by removing selector strings
- ⚠️ **Angular 19.x LTS ends May 19, 2026** — now approximately **33 days away**; teams on v19 must upgrade immediately

### "State of Nuxt 2026" Talk Published
- Daniel Roe's "State of Nuxt 2026" talk (delivered at VueJS Amsterdam March 2026) was published on YouTube (April 14, 2026)
- No new product announcements beyond the Nuxt 4.4 release already covered
- Key theme: Nuxt 5 (Nitro v3) continues on the `main` branch; teams should adopt `future.compatibilityVersion: 5` to begin testing

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
