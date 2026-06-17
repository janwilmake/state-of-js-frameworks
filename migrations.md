# Migration Guides

> Breaking changes and migration paths between major framework versions. Maintained by the Framework Tracker agent.

---

## Next.js

### Next.js 15.x → 16.x

**Released:** October 21, 2025  
**Effort:** Medium (2–4 hours for most projects)

#### Breaking Changes
- **React 19.2 required** — must upgrade from React 18; React 19 introduces breaking changes of its own (see React 19 migration guide)
- **`params` and `searchParams` are now Promises** — in App Router pages and layouts, `params` and `searchParams` props must be `await`ed; use the automated codemod
- **Minimum Node.js 20.9+** — Node.js 18 and older Node 20 versions dropped; TypeScript 5.1+ required
- **Caching defaults changed** — `fetch()` requests are no longer cached by default; must explicitly opt in to caching with `cache: 'force-cache'` or `next: { revalidate: n }`
- **`cookies()` and `headers()` are now async** — must `await` these APIs
- **`middleware.ts` deprecated → `proxy.ts`** — rename your `middleware.ts` file to `proxy.ts` and the exported function from `middleware` to `proxy`; the `edge` runtime is NOT supported in `proxy` (keeps using `middleware.ts` if you need edge runtime)
- **PPR (`experimental.ppr`) removed** — replaced by Cache Components (`"use cache"` directive); remove `experimental.ppr: true` from `next.config`; wait for migration guide before converting PPR code
- **Turbopack is now the default bundler** — `next dev` and `next build` use Turbopack by default; opt out with `--webpack` flag if custom webpack config is needed
- **Parallel routes require explicit `default.js`** — all parallel route slots need a `default.js`; build fails without them
- **`images.minimumCacheTTL` default changed** — from 60s to 4 hours (14400s)

#### Migration Steps
```bash
# Use the automated upgrade CLI (recommended)
npx @next/codemod@canary upgrade latest

# Or upgrade manually
npm install next@latest react@latest react-dom@latest
```

Key codemods available:
- `next-async-request-api` — converts `params`, `searchParams`, `cookies()`, `headers()` to async
- `next-og-import` — updates `next/server` ImageResponse imports

```bash
# Rename middleware file
mv middleware.ts proxy.ts
# Update the exported function name inside the file from `middleware` to `proxy`
```

#### Notes
- Pages Router users: no breaking changes; Pages Router is in maintenance mode but fully supported
- React Compiler (stable in 16.x) is opt-in; enable with `reactCompiler: true` in `next.config.ts`

---

### Next.js 14.x → 15.x

**Released:** October 21, 2024  
**Effort:** Low–Medium (1–2 hours)

#### Breaking Changes
- **`async` `params` in dynamic routes** — `params` became a Promise in RC; stable in 15.0
- **React 18.3 recommended** (React 19 support added, not required)
- **`next/server` `ImageResponse` renamed** — use codemod

---

### Next.js 13.x → 14.x

**Released:** October 26, 2023  
**Effort:** Low (30 min–1 hour)

#### Breaking Changes
- **`next export` removed** — use `output: 'export'` in `next.config.js`
- **`@next/font` removed** — use built-in `next/font`
- **`next/server` `ImageResponse` import** — use `next/og` instead
- **WASM target for `next-swc` removed**
- **Minimum Node.js: 18.17** (up from 16.14)

---

## Remix / React Router

### Remix v2 → React Router v7 (Framework Mode)

**Released:** November 2024  
**Effort:** Medium (4–8 hours for typical Remix v2 app)  
**Official guide:** [reactrouter.com/upgrading/remix](https://reactrouter.com/upgrading/remix)

#### What Changed
React Router v7 is the direct successor to Remix v2. Remix's features (loaders, actions, SSR, nested routing) are now in React Router itself.

#### Breaking Changes
- **Package change** — `@remix-run/*` packages → `react-router` and `@react-router/*`
- **Config file renamed** — `remix.config.js` → `react-router.config.ts`
- **Route module API** — minor changes to export conventions
- **Vite is now required** — the old Remix Compiler is removed

#### Migration Steps
```bash
# Install React Router v7
npm install react-router@latest

# Run the automated migration
npx @react-router/upgrade
```

The `@react-router/upgrade` CLI handles most of the package renaming and import updates automatically.

#### ⚠️ Remix 3 Warning
Remix 3 is **NOT** an upgrade path from Remix v2. It is a completely separate framework (forking Preact, not React). If you're a Remix v2 user, migrate to **React Router v7**, not Remix 3. There is no migration path to Remix 3 from any existing React framework.

---

### React Router v7 → v8 (Imminent — Mid-2026)

**Status:** Expected "in the next month or two" per official v7.15.0 release notes (May 5, 2026); v7.15.x stabilization work is the final preparation  
**Effort:** Low–Medium (mostly tooling changes)

#### Anticipated Breaking Changes
- **ESM only** — CJS builds dropped; requires Node 20.19+ / 22.12+ or Bun for `require(esm)` support
- **Drop Node 20 support** — Node 20 is EOL April 2026; Node 22 becomes the minimum
- **Vite 7+ required** — Vite 7 went ESM-only; v8 aligns with this

#### What Stays the Same
- Loaders, actions, nested routing, file-based routing
- All adapters and deployment targets
- RSC Framework Mode (may graduate from unstable to stable in v8)

No migration codemod announced yet. Watch the ["React Router v8 and Beyond" talk](https://www.youtube.com/watch?v=tIhqxwyTQ2M) (published May 25, 2026) for the full v8 roadmap. Monitor the [React Router v8 discussion](https://github.com/remix-run/react-router/discussions/14468) for timeline updates.

---

### Remix v1 → v2

**Released:** September 2023  
**Effort:** Medium  

#### Breaking Changes
- **`remix.config.js` changes** — many opt-in future flags from v1 became defaults in v2
- **Route file naming convention changed** — flat routes by default
- **`meta`, `links`, `handle` exports changed**
- **`CatchBoundary` removed** — use `ErrorBoundary` for both errors and 4xx responses

Use future flags in Remix v1 to incrementally adopt v2 behaviors before migrating.

---

## Nuxt

### Nuxt UI v4.7.x → v4.8.0 (May 21, 2026) — InputMenu Breaking Change

**Effort:** Minimal — one prop rename

#### Breaking Change
- **`InputMenu.autocomplete` prop renamed to `mode`** — the boolean `autocomplete` introduced in v4.6.0 conflicted with the standard HTML `autocomplete` attribute used for browser autofill. It is now renamed to `mode`, which accepts `'combobox' | 'autocomplete'` (defaults to `'combobox'`). The HTML `autocomplete` attribute now passes through to the inner input like other form components.

```diff
- <UInputMenu autocomplete :items="items" />
+ <UInputMenu mode="autocomplete" :items="items" />
```

No other breaking changes in v4.8.0. All other new features (`Theme` prop defaults, `ContentSearch` async search, new component props) are purely additive.

```bash
npm install @nuxt/ui@latest   # → 4.8.0
```

---

### Nuxt 4.4.5 → 4.4.6 (Security Patch — May 18, 2026)

**Effort:** Near-zero — `npm install nuxt@latest`

⚠️ **Upgrade immediately.** Multiple security vulnerabilities were patched in 4.4.6. Netlify's changelog (May 19, 2026) disclosed that Nuxt 4.4.5 and earlier contain security issues patched in 4.4.6+. `@nuxt/rspack-builder` is also patched in the corresponding release.

No API changes or breaking changes in this patch. Simply upgrade:
```bash
npm install nuxt@latest          # 4.x → 4.4.6
npx nuxt upgrade                  # alternative via nuxi
```

---

### Nuxt 3.x → Nuxt 4.x

**Released:** July 16, 2025  
**Effort:** Low–Medium (2–4 hours; most changes are opt-in via compatibility mode)  
**Official guide:** [nuxt.com/docs/getting-started/upgrade](https://nuxt.com/docs/getting-started/upgrade)  
> ⚠️ **Nuxt 3 EOL is July 31, 2026 — approximately 6 weeks from today (June 17, 2026).** After this date, no further security patches or bug fixes will be issued for the Nuxt 3.x line. Upgrade now.

#### Breaking Changes
- **`app/` directory convention** — source files now default to `app/` instead of project root; configure via `srcDir`
- **`useAsyncData` and `useFetch` return types changed** — `data` is no longer `null` by default; use `default: () => []` or similar
- **`useCookie` and `useHeaders` now return shallow refs** — deeply reactive access patterns may need updating
- **`NuxtLink` default behavior changes** — some edge-case behaviors changed
- **Nitro v2 (internal)** — if you use custom Nitro plugins, review compatibility

#### Migration Strategy (Recommended)
Nuxt 4 supports a **compatibility mode** that allows incremental adoption:

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  future: {
    compatibilityVersion: 4, // Opt into Nuxt 4 behaviors
  }
})
```

Enable this flag in a Nuxt 3 project, fix any resulting errors, then upgrade to Nuxt 4.

#### Preparing for Nuxt 5
Nuxt 5 (Nitro v3) is in **active beta development** as of March 11, 2026. Teams can begin preparing via:
```ts
export default defineNuxtConfig({
  future: {
    compatibilityVersion: 5, // Experimental Nuxt 5 behaviors
  }
})
```

**Nitro v3 breaking changes to anticipate for Nuxt 5:**
- **Node 16 dropped** — ensure Node 18+ (likely Node 20+ at Nuxt 5 stable time)
- **App config functionality removed** — moved to the Nuxt layer system
- **Default caching behavior changed** — review any Nitro-level cache configuration
- **H3 v2 request handling** — web-standard `Request`/`Response` APIs replace some H3 v1 patterns; server routes using low-level H3 APIs may need updates
- Task-based patterns in `server/tasks/` replace some workarounds for background jobs

#### EOL Notes
- Nuxt 3 support extended to **July 31, 2026** (was January 31, 2026)
- Teams should target Nuxt 4 by July 2026; Nuxt 5 is not yet available for migration

---

### Nuxt 2 → Nuxt 3

**Effort:** High (significant rewrite often required)  
Nuxt 2 is based on Vue 2 (Options API). Nuxt 3 uses Vue 3 (Composition API + `<script setup>`).

Key changes:
- Vue 2 → Vue 3 (breaking change for Options API patterns)
- `asyncData()` / `fetch()` → `useFetch()` / `useAsyncData()` composables
- Nuxt modules API completely rewritten
- Vuex → Pinia (or Nuxt's built-in `useState`)
- Custom server → Nitro

**Commercial support:** HeroDevs offers Never-Ending Support (NES) for Nuxt 2 if you cannot migrate immediately.

---

## SvelteKit

### SvelteKit 2.60.x → 2.61.x (Remote Functions: `.run()` Removed)

**Released:** June 2026  
**Effort:** Low (only affects projects using experimental Remote Functions that used `.run()`)

#### Breaking Change
- **`query.run()` method removed** — the `.run()` method added in kit@2.56.0 has been superseded. Use `await query()` directly in all contexts. Remote queries can now be awaited in event handlers, async callbacks, and module scope, with cache deduplication shared across reactive and non-reactive consumers.

```diff
- query(...).run();  // old pattern (kit@2.56–2.60)
+ await query(...);  // new pattern (kit@2.61+) — works everywhere
```

This change only affects code using experimental Remote Functions. Standard `load()`, form actions, and server endpoints are unaffected.

---

### SvelteKit 2.55.x → 2.56.x (Remote Functions Breaking Changes)

**Released:** May 2026  
**Effort:** Low–Medium (only affects projects using experimental Remote Functions)

#### Breaking Changes (Remote Functions only)
- **`run()` method added to queries; awaiting queries outside render is now disallowed** — calls to `await query()` must be inside a component render or `$effect`; use `.run()` for imperative invocations
- **Client-requested query refreshes require server permission** — the server must now explicitly grant or deny client-side refresh requests; protects against unbounded refresh storms
- **Object key sorting for remote function caching** — cache keys are now stable regardless of property insertion order; may invalidate existing caches on first deploy
- **`requested` API change** — now requires a `limit` option and yields `{ arg, query }` entries instead of validated args directly
- These changes only affect code in `.remote.ts` files using the experimental `remoteFunctions` feature; standard `load()`, `form actions`, and server endpoints are unaffected

#### Migration Steps
If you use Remote Functions, review the [SvelteKit 2.56.0 release notes](https://github.com/sveltejs/kit/releases/tag/%40sveltejs%2Fkit%402.56.0) and update:
1. Replace any `await query(...)` calls outside component render with `query(...).run()`
2. Add `limit` option to `requested` handlers and update destructuring to `{ arg, query }`
3. Review any client-side refresh logic to ensure server grants permission

---

### Svelte 4 → Svelte 5 (Runes)

**Released:** October 2024  
**Effort:** Medium–High depending on codebase size  
**Official guide:** [svelte.dev/docs/svelte/v5-migration-guide](https://svelte.dev/docs/svelte/v5-migration-guide)

#### Key Changes
The Svelte 5 Runes API is a significant but worthwhile upgrade:

| Old Syntax | New Syntax |
|---|---|
| `let count = 0` (reactive) | `let count = $state(0)` |
| `$: doubled = count * 2` | `let doubled = $derived(count * 2)` |
| `$: { ... }` (side effect) | `$effect(() => { ... })` |
| `export let prop` | `let { prop } = $props()` |
| `createEventDispatcher()` | Callback props via `$props()` |
| `<slot>` | `{@render children()}` with `Snippet` |

#### Migration Path
```bash
# Use the automated migration script
npx sv migrate svelte-5
```

The `sv migrate` CLI handles the majority of rune conversions automatically. Manual review is needed for:
- Complex reactive declarations
- Event dispatchers → callback props
- Slot content → Snippet pattern

#### Svelte 4 Compatibility
Svelte 5 ships with a **legacy mode** that maintains most Svelte 4 syntax. You can migrate incrementally, component by component. However, legacy mode will eventually be removed; plan a full migration.

---

### SvelteKit 1.x → 2.x

**Released:** January 2024  
**Effort:** Low (< 1 hour for most projects)

#### Breaking Changes
- **`resolve.transformPageChunk` moved** to `handle` hook
- **`beforeNavigate` / `afterNavigate` API changes** — `from` and `to` types simplified
- **Minimum Vite 5 and Node.js 18** required
- **`$env/dynamic/*` imports** — must use module context in some edge cases

```bash
npx svelte-migrate sveltekit-2
```

---

## Astro

### Astro 6.3.x → 6.3.7 (Security + Bug Fixes — May 14–21, 2026)

**Effort:** Zero — drop-in patch upgrade

⚠️ **Upgrade immediately if using SSR + Islands.** `astro@6.3.3` patched a reflected XSS where slot names on hydrated island components were not HTML-escaped in SSR output. `6.3.4` and `6.3.5` add further fixes (CSP `<Image>` prop bug, stale SSR module cache, advanced routing improvements). `6.3.6` and `6.3.7` are routine follow-up patches.

```bash
npm install astro@latest          # → 6.3.7
npx @astrojs/upgrade              # alternative
```

No API breaking changes in any 6.3.x patch.

---

### Astro 6.2.x → 6.3.x (Non-Breaking Minor)

**Released:** May 7, 2026  
**Effort:** Near-zero — all new features are opt-in experimental flags

#### Changes
- **Experimental Advanced Routing** — new `src/app.ts` entry point opt-in; existing projects unaffected unless you add this file
- **SVG processing disabled by default** — if your project relied on SVG images being processed by Astro's image pipeline, add `image: { svg: true }` to `astro.config.mjs`
- `AstroCookies.consume(cookies)` static method deprecated in favour of the instance method — adapters using the static form will see a deprecation warning; update when convenient

```bash
npx @astrojs/upgrade  # safe — no breaking changes
```

---

### Astro 6.x → 7.x (Beta — Not Yet Stable)

**Status:** Beta (`7.0.0-beta.3` — June 9, 2026); stable release expected mid-to-late 2026  
**Effort:** Low for most users; Medium for integration authors

#### Breaking Changes (from alpha)
- **Vite 8 upgrade** — breaking for Astro integrations that depend on Vite internal APIs; most project-level code is unaffected
- **Rust compiler is now the default and only compiler** — the previous Go compiler and `experimental.rustCompiler` flag are removed:
  - **More strict HTML parsing** — unclosed HTML tags now throw errors instead of being silently ignored
  - **Semantically invalid HTML is no longer corrected** — Astro 7 leaves invalid HTML to the browser, similar to `document.write()`
  - **Action required:** Remove `experimental.rustCompiler: true` from your `astro.config.mjs` (was the opt-in flag)

#### Migration Steps
```bash
# Test the beta (not for production)
npm install astro@beta

# When stable: remove the old experimental flag
# In astro.config.mjs, delete:
# experimental: { rustCompiler: true }  ← no longer needed
```

The `@astrojs/upgrade` CLI will handle this automatically when stable is released.

---

### Astro 5.x → 6.x

**Released:** March 10, 2026  
**Effort:** Medium (2–4 hours)  
**Official guide:** [v6.docs.astro.build/en/guides/upgrade-to/v6/](https://v6.docs.astro.build/en/guides/upgrade-to/v6/)

#### Breaking Changes
- **Node.js 22+ required** — drop Node 18 and 20
- **`Astro.glob()` removed** — migrate to Content Collections (`getCollection()`) or `import.meta.glob()`
- **Zod 4 upgrade** — Content Collection schemas using Zod must be checked for API changes
- **Cloudflare adapter**: `Astro.locals.runtime` removed — access platform APIs directly via `getRuntime(context.request)`
- **Several deprecated APIs removed** — check the [full breaking changes list](https://v6.docs.astro.build/en/guides/upgrade-to/v6/#breaking-changes)

#### Migration Steps
```bash
# Use the automated upgrade CLI
npx @astrojs/upgrade

# Or manual upgrade
npm install astro@latest
```

The `@astrojs/upgrade` CLI handles most import and API changes automatically.

#### Key `Astro.glob()` Migration

```js
// Before (Astro 5)
const posts = await Astro.glob('./posts/*.md');

// After (Astro 6) — using Content Collections (recommended)
import { getCollection } from 'astro:content';
const posts = await getCollection('posts');

// After (Astro 6) — using import.meta.glob
const posts = import.meta.glob('./posts/*.md', { eager: true });
```

---

### Astro 4.x → 5.x

**Released:** January 2025  
**Effort:** Medium

Key changes: Content Layer API stabilized (replaces experimental Content Collections v2), Server Islands stable, simplified adapter API.

---

## Angular

### Angular 21 → 22 ✅ (Stable since June 3, 2026; latest patch: 22.0.1)

**Status:** **Stable** — `22.0.1` released June 10, 2026 (patch); `22.0.0` was the major release June 3, 2026  
**Effort:** Low–Medium (most breaking changes are tool-assisted via `ng update`)

> ⚠️ Angular 19.x reached EOL on May 19, 2026. Angular 21 is in LTS (security-only until May 2027). Teams on v19 must migrate to v22 immediately.

#### Breaking Changes

**Automated migrations available (safe to run):**
- **`ChangeDetectionStrategy.Default` renamed to `Eager`; `OnPush` is now the default** — the `Default` strategy is renamed to `Eager`; new components generated by the CLI now use `OnPush` by default; `ng update` schematic automatically adds `changeDetection: ChangeDetectionStrategy.Eager` to all existing components that did not specify a strategy, preserving their previous behavior; **no behavioral change to existing apps** as long as you run `ng update`
- **HTTP client uses Fetch API by default** — `withFetch()` is now the default provider and is marked deprecated; the `ng update` migration removes `withFetch()` from your `app.config.ts`; if you need the legacy XMLHttpRequest behavior, the migration adds `withXhr()` automatically; improves SSR performance out of the box
- **`canMatch` router guards gain a mandatory third parameter `currentSnapshot`** — the function signature for `canMatch` now requires `(route, segments, currentSnapshot)`; automated migration provided via `ng update`
- **Signal Forms breaking changes (for v21 developer preview adopters)** — Signal Forms APIs previously marked `@developerPreview` are now stable with minor surface API changes; check Signal Forms API docs if you already adopted them in v21

**Manual fixes required (no automated migration):**
- **`paramsInheritanceStrategy` defaults to `'always'`** — previously the default was `'emptyOnly'`, meaning child routes only inherited parameters when they had none of their own; now **all** parent parameters are inherited by default; if your app relies on the old `'emptyOnly'` behavior (e.g., a child route intentionally shadowing a parent's `:id` param), you must manually set `paramsInheritanceStrategy: 'emptyOnly'` in your router configuration; **no codemod provided**
- **Webpack builders deprecated** — `@angular-devkit/build-angular`, `@ngtools/webpack`, and the `browser` / `browser-esbuild` builder targets are deprecated (not yet removed); if you have custom webpack configuration, begin planning migration to the application builder (`@angular/build:application`) which uses esbuild + TSGo; full removal in a future major version

#### Migration Steps
```bash
# Recommended: upgrade core and CLI together
ng update @angular/core@22 @angular/cli@22

# If you have Material or other Angular packages:
ng update @angular/material@22
```

The Angular CLI schematic handles template and component updates automatically. Review the official [Angular Update Guide](https://angular.dev/update-guide?v=21.0-22.0) for v21 → v22. **Pay particular attention to `paramsInheritanceStrategy`** — this is the only breaking change with no automated migration.

#### What Stays the Same
- Existing Zone.js projects work without changes
- All components using `ChangeDetectionStrategy.Default` (now `Eager`) continue to work after the automated `ng update` migration
- All `ReactiveFormsModule` (Reactive Forms) patterns continue to work; Signal Forms is additive, not a replacement
- `RouterModule` imports continue to work; standalone router approach is recommended for new code but not required

#### New Stable APIs in v22 (safe to adopt immediately)
- `signal()` / `computed()` / `effect()` forms — **Signal Forms** fully stable
- `httpResource()` / `rxResource()` — signal-integrated HTTP data fetching (replaces common RxJS patterns)
- `injectAsync()` — lazy-load services via dynamic import; `injectAsync(() => import('./service'))` returns a signal once resolved
- Angular Aria — accessible UI primitives
- Angular MCP Server full suite — `devserver.start/stop`, `ai_tutor`, `modernize`, `onpush_zoneless_migration`

#### Developer Preview in v22
- **`@boundary`** — template-level error boundaries; wrapping a component block in `@boundary` isolates failures so a single component crash doesn't take down the whole page; GA expected Q3 2026

---

### Angular 20 → 21

**Released:** November 19, 2025  
**Effort:** Low (< 1 hour; mostly additive)

```bash
ng update @angular/core @angular/cli
```

#### Changes
- Signals API enhancements (additive)
- Signal Forms developer preview (additive; no migration required)
- No major breaking changes in the public API

---

### Angular 19 → 20

**Released:** May 28, 2025  
**Effort:** Low

- `effect()`, `linkedSignal()`, `toSignal()` graduated to stable
- `provideZoneChangeDetection()` deprecated (not yet removed)
- `ng update @angular/core @angular/cli`

---

### Angular 17 → 18

**Effort:** Low–Medium  

Key changes:
- Zoneless change detection **opt-in** introduced (`provideExperimentalZonelessChangeDetection()`)
- New `@if`, `@for`, `@switch` block syntax stable (old `*ngIf`, `*ngFor`, `*ngSwitch` still work but deprecated)
- Non-destructive hydration stable

Use `ng update` for automated migrations. The Angular CLI handles most structural directive → block syntax migrations via schematics.

---

### Angular 15 → 16 (Signals Introduction)

**Released:** May 2023  
**Effort:** Low (Signals are additive, no migration required)

Angular 16 introduced Signals as a developer preview. No breaking changes; existing Zone.js code continues to work unchanged. Teams should begin evaluating Signals for new components.

---

### AngularJS (1.x) → Angular (2+)

This is a complete rewrite, not a migration. AngularJS reached end-of-life December 31, 2021.

Options:
- **Full rewrite** to Angular 21 (recommended for large orgs)
- **Hybrid migration** using `ngUpgrade` to incrementally replace AngularJS components with Angular components in the same app
- **HeroDevs NES** for AngularJS — commercial security patches if immediate migration is not feasible

---

## Cross-Framework Migrations

### Remix v2 → Next.js App Router

**Effort:** High (full rewrite of data patterns)

Key conceptual mappings:
| Remix | Next.js App Router |
|---|---|
| `loader()` | `async` Server Component or `fetch()` in RSC |
| `action()` | Server Action |
| `useLoaderData()` | Props passed from Server Component |
| Nested routes | `layout.tsx` + `page.tsx` hierarchy |
| `<Form>` | `<form>` + Server Action |
| `defer()` | `<Suspense>` + async Server Component |

### Next.js Pages Router → App Router

**Effort:** Medium–High (can be done incrementally)  
**Official guide:** [nextjs.org/docs/app/guides/migrating/app-router-migration](https://nextjs.org/docs/app/guides/migrating/app-router-migration)

Both routers can coexist in the same project. Migrate route by route:
- `pages/` still works in Next.js 16.x
- `app/` directory for new App Router routes
- `getServerSideProps` / `getStaticProps` → async Server Components
- `useRouter` (pages) → `useRouter` from `next/navigation` (app)
- API routes (`pages/api/`) → Route Handlers (`app/.../route.ts`) or Server Actions
