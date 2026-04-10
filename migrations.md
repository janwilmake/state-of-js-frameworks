# Migration Guides

> Breaking changes and migration paths between major framework versions. Maintained by the Framework Tracker agent.

---

## Next.js

### Next.js 15.x → 16.x

**Released:** October 21, 2025  
**Effort:** Medium (2–4 hours for most projects)

#### Breaking Changes
- **React 19 required** — must upgrade from React 18; React 19 introduces breaking changes of its own (see React 19 migration guide)
- **`params` and `searchParams` are now Promises** — in App Router pages and layouts, `params` and `searchParams` props must be `await`ed; use the automated codemod
- **Minimum Node.js version** — Node.js 18.18+ required (Node 16/17 dropped)
- **Caching defaults changed** — `fetch()` requests are no longer cached by default; must explicitly opt in to caching with `cache: 'force-cache'` or `next: { revalidate: n }`
- **`cookies()` and `headers()` are now async** — must `await` these APIs

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

#### Notes
- Pages Router users: no breaking changes; Pages Router is in maintenance mode but fully supported
- Turbopack is stable for `next dev` in 16.x; opt in with `--turbopack` flag

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

### Nuxt 3.x → Nuxt 4.x

**Released:** July 16, 2025  
**Effort:** Low–Medium (2–4 hours; most changes are opt-in via compatibility mode)  
**Official guide:** [nuxt.com/docs/getting-started/upgrade](https://nuxt.com/docs/getting-started/upgrade)

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
Nuxt 5 (Nitro v3) is in early development. Teams can begin preparing via:
```ts
export default defineNuxtConfig({
  future: {
    compatibilityVersion: 5, // Experimental Nuxt 5 behaviors
  }
})
```

#### EOL Notes
- Nuxt 3 support extended to **July 31, 2026** (was January 31, 2026)
- Teams should target Nuxt 4 by July 2026

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
