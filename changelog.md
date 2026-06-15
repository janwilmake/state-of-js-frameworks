# Changelog

> Framework releases, announcements, and major events, newest first. Maintained by the Framework Tracker agent.

---

## 2026-06-15 (run: June 15, 2026)

### SvelteKit 2.65.0 + SvelteKit 3.0.0-next.4 (June 11, 2026) 🚀

**SvelteKit 2.65.0** (June 11, 2026) — Latest stable:
- **Queries can now refresh other queries** — a remote query handler can trigger a refresh of other named queries; enables clean dependency-chain invalidation without manual coordination or shared state
- Fix: deduplicate remote data fetched across multiple concurrent component instances of the same query
- Fix: skip client-side JavaScript build entirely when all routes have CSR disabled (speeds up SSG-only builds)
- `npm install @sveltejs/kit@latest` → **2.65.0**

**SvelteKit 3.0.0-next.4** (June 11, 2026) — Pre-release (not production ready):
- Fix: reset queries before navigating when `invalidateAll` is set — prevents stale query data from persisting across navigations that fully invalidate client state
- Install with `npm install @sveltejs/kit@next`

**SvelteKit 3.0.0-next.3** (in the same week):
- Carries forward all 3.0.0-next.0–next.2 changes (Vite Environment API, `data-sveltekit-*: false`, Rolldown in adapter-node) plus:
  - Remote data deduplication across component instances
  - Queries can refresh other queries (same feature as 2.65.0 stable, landed in pre-release first)
  - Explicit env vars support (`explicitEnvironmentVariables`)

> **June 2026 SvelteKit recap** (from ["What's New in Svelte: June 2026"](https://svelte.dev/blog/whats-new-in-svelte-june-2026)):
> - `2.61.0`: **`.run()` removed from remote queries** — breaking change; `await query()` works in all contexts now including event handlers, async callbacks, and module scope with shared cache deduplication
> - `2.60.0`: Remote form validation warnings, number/boolean form fields, abort stale renders
> - `2.63.1`: `query.live` switches from polling to SSE (Server-Sent Events)
> - `2.64.0`: Commands can receive `File` objects; SSR-disabled route bundling fix
> - `2.65.0`: Queries can refresh other queries (see above)

---

## 2026-06-13 (run: June 13, 2026)

### Angular 22.0.1 (June 10, 2026) + 22.1.0-next.0 Pre-release Track Opens 🔧

- **22.0.1** (June 10, 2026) — Routine bug fix patch on the 22.0.x line; no API changes; `npm install @angular/core@latest` → 22.0.1
- **21.2.17** (June 10, 2026) — Latest LTS security + bug fix patch on the v21 line
- **20.3.25** (June 10, 2026) — Latest LTS security patch on the v20 line
- **Angular VSCode Extension 22.0.1** (June 11, 2026) — fixes relative workspace TSDK path resolution; prevents external template inlay hints from showing in `.ts` files; corrects TSDK configuration inspection
- **22.1.0-next.0** (June 10, 2026) — First pre-release for the 22.1 minor track opens: `linkedSignal` gains a custom `set` option, JSONP support deprecated in `HttpClient`, foreign component / `@content` anchor ordering fixes, HTTP transfer cache now correctly skips uncacheable and credentialed requests

---

### Angular 22: Additional Breaking Changes Documented

Deep-dive coverage of the v22.0.0 release (June 3) via the community blog Ninja Squad reveals additional breaking changes beyond what was initially announced:

- **`ChangeDetectionStrategy.Default` → `Eager`; `OnPush` is now the default** — semantically a rename + default flip; `ng update` handles existing components automatically by adding `changeDetection: ChangeDetectionStrategy.Eager`
- **HTTP client uses Fetch API by default** — `withFetch()` deprecated and auto-removed by `ng update`; opt back into XHR with `withXhr()`
- **`canMatch` guards gain mandatory `currentSnapshot` parameter** — automated migration via `ng update`
- **`paramsInheritanceStrategy` defaults to `'always'`** ⚠️ — **no automated migration**; if your app relied on the old `'emptyOnly'` default, manually set `paramsInheritanceStrategy: 'emptyOnly'` in your `RouterModule.forRoot()` or `provideRouter()` config before upgrading
- **Webpack builders deprecated** — `@angular-devkit/build-angular` and `@ngtools/webpack` deprecated; removal in a future major; begin migration to `@angular/build:application` (esbuild + TSGo)
- **`injectAsync()`** — new async DI utility for lazy service loading via dynamic import

---

### React Router v7.17.0 (June 4, 2026) — Docs Bundled for AI Agents 📦

- **Official Markdown docs now shipped inside the npm package** — `node_modules/react-router/docs` now contains the official React Router documentation as Markdown files; AI coding agents (Cursor, Claude Code, Copilot etc.) and React Router agent skills can read docs locally without network access; excludes auto-generated API docs, community content, and tutorials
- Fix future flag warning URLs (previously pointed to incorrect documentation links)
- RSC route module server exports are excluded from client dependency optimizer when `future.unstable_optimizeDeps` is enabled (avoids incorrect server-side exports being bundled for the client)
- **Current stable: `npm install react-router@latest` → 7.17.0**
- React Router v8 remains imminent; v7.16–7.17 are final v7 stabilization releases

---

### Cloudflare Acquires VoidZero (June 4, 2026) 🌐 Ecosystem Event

- **VoidZero** (the team behind Vite, Vitest, Rolldown, Oxc, and Vite+) joined Cloudflare on June 4, 2026
- Vite remains MIT-licensed, vendor-agnostic, and built for everyone — this is the same open-governance model as the Astro acquisition in January 2026
- Directly benefits: **SvelteKit** (Vite-native), **Astro** (uses Vite Environment API), **Nuxt** (Vite-based build), **Next.js** (Turbopack competes, but some Vite-based features), **React Router** (Vite-based dev build), and the broader npm ecosystem
- SvelteKit 3.0 pre-release (`3.0.0-next.1`) adopts the Vite Environment API as a first-class feature
- With Cloudflare now controlling Astro, VoidZero (Vite), and having Astro as its reference content framework, **Cloudflare is positioned as the dominant force in the JS build tooling and edge deployment ecosystem**

---

## 2026-06-11 (run: June 11, 2026)

### Next.js 16.2.9 (June 9, 2026) + 16.3 Preview Branch Opens 🔜

- **v16.2.9** (June 9, 2026) — Empty release to correct the `next@latest` NPM dist-tag; Vercel's Trusted Publishing setup prevents direct dist-tag manipulation, so a new release was required. No code changes from 16.2.8.
- **16.3.0-preview.3** (June 10, 2026) — A dedicated `16.3.x-preview` release branch has been opened, with `npm install next@preview` available. Enables Turbopack filesystem cache for builds by default in non-stable releases. This is a strong signal the 16.3 release cycle is underway.
- **Vercel Ship — June 25, 2026** — Community speculation (Reddit r/nextjs) and the preview branch timing strongly suggest a **Next.js 16.3 stable release at or around Vercel Ship on June 25, 2026**.
- Current stable remains **16.2.9**; current 15.x remains **15.5.19** (June 1, 2026)

---

### Nuxt 4.4.8 / 3.21.8 (June 8, 2026) 🔥 macOS Dev Server Hotfix

- **4.4.8** hotfix released to address an issue running the Nuxt dev server on **macOS** introduced in 4.4.7 (June 2, 2026); macOS users on 4.4.7 should upgrade immediately
- **3.21.8** — corresponding maintenance patch on the v3 line
- No API changes; no breaking changes
  ```bash
  npm install nuxt@latest   # → 4.4.8
  ```
- Nuxt 3.x EOL: **July 31, 2026** — teams still on Nuxt 3 have ~7 weeks to migrate to Nuxt 4

---

### Astro 7.0.0-beta.3 (June 9, 2026) 🚀 Astro 7 Advances to Beta

- **Astro 7 graduated from alpha to beta** — `7.0.0-beta.3` released June 9, 2026; install with `npm install astro@beta`
- This marks a milestone: Astro 7 is now considered stable enough for integration authors and early adopters to test; not yet production-ready
- Key features in Astro 7 beta remain the same as alpha: Vite 8 as default, Rust compiler as the only compiler (Go compiler removed), stricter HTML parsing, `experimental.rustCompiler` flag removed
- `@astrojs/adapter-*` beta releases for Vercel, Node, and Cloudflare are published alongside

---

### Astro 6.4.5 / 6.4.6 (June 9–10, 2026) — Patch Cluster

**6.4.6** (June 10, 2026):
- Image file renaming in dev server no longer triggers build errors (hot-reload fix)
- `addAttribute` hardened — drops attribute names with invalid HTML spec characters to prevent injection
- `allowedDomains` origin validated before fetching prerendered error pages

**6.4.5** (June 9, 2026):
- `Astro.request.url` now stays in sync with `Astro.url` behind TLS-terminating proxies (previously they could diverge)
- Reverts a Cloudflare adapter `isNode` detection change that caused significant build time regressions on large prerendered sites

- **Current stable: `npm install astro@latest` → 6.4.6**

---

### SvelteKit 2.64.0 (June 8, 2026) — already captured

- `feat: allow commands to receive File objects` — remote function commands can now accept `File` instances directly (for file upload workflows)
- Fix: avoid server components being bundled when SSR is disabled for a route

---

## 2026-05-28 (run: May 28, 2026)

### Angular 22 — 4 Days to Stable (June 1, 2026) 🚀

- Angular 22 stable remains on track for the **week of June 1, 2026** — now **4 days away** as of today (May 28, 2026)
- `22.0.0-rc.0` (May 13, 2026) remains the only RC; no RC.1 issued — the RC has been clean and stable, a positive signal for the June 1 landing
- All confirmed v22 features stand: **stable Signal Forms**, selectorless components, OnPush as default for new projects, Zoneless as default for new projects, TypeScript 5.9 support, Vitest as primary test runner (stable)
- `ng update @angular/core@22 @angular/cli@22` will be the upgrade command — teams should have dependencies audited and pre-migration checklists ready
- Angular 21.x remains the latest stable (`21.2.14`, May 20, 2026) until v22 ships; Angular 21 is now in **LTS** (security patches only until May 19, 2027)

---

### Next.js 16.3 Canary — Progress Update (May 26–27, 2026)

- **16.3.0-canary.29** (May 26) and **16.3.0-canary.30** (May 27) — latest pre-release builds
- **canary.30 notable changes**:
  - Fix Firefox refresh loop on initial load of streaming pages in dev mode
  - React upgrade: `d5736f09-20260507` → `75b0945b-20260526` (React canary bump)
  - **`experimental.appShells` prefetch on client** — App Shell prefetches now triggered client-side; server responds to App Shell prefetches correctly
  - Docs: `next/root-params` API reference added; ISR with Cache Components + `experimental.partialFallbacks` guide
- **canary.29** — no notable user-facing changes; CI and infrastructure improvements
- **16.2.6 remains the latest stable** — no new stable patch since May 7, 2026
- Estimated stable for 16.3: late June or July 2026 based on current canary pace

---

## 2026-05-26 (run: May 26, 2026)

### React Router v8 — "In the Next Month or Two" Signal Strengthens 🔜

- **"React Router v8 and Beyond" talk published May 25, 2026** — Brooks Lybrand (Remix/React Router maintainer) delivered a public talk covering the v8 roadmap, migration path, and what teams can expect for the future of React Router
- No new stable v7.x release since v7.15.1 (May 14, 2026); v8 is being finalized
- **React Router v8 confirmed feature-complete**: all future flags are stabilized; the team is in final release preparation; the "in the next month or two" timeline from May 5 stands
- **Key v8 facts confirmed**: ESM-only; Vite 7+ minimum; RSC Framework Mode will **not** be stable in v8.0 but will stabilize in an early v8.x minor; `unstable_useRouterState()` from v7.15.1 will become `useRouterState()` in v8
- Teams should enable all `future.v8_*` flags now (especially `v8_passThroughRequests`, `v8_viteEnvironmentApi`) to prepare for a smooth upgrade

---

### Angular 22 — 6 Days to Stable (June 1, 2026) ⏳

- Angular 22 stable remains on track for the **week of June 1, 2026** — now 6 days away
- `22.0.0-rc.0` remains the latest pre-release; no RC.1 has been needed — stable signal for June 1 launch
- All confirmed v22 features remain: **stable Signal Forms**, selectorless components, OnPush as default for new projects, Zoneless as default for new projects, TypeScript 5.9 support, Vitest as default test runner
- Teams should have `ng update @angular/core@22 @angular/cli@22` queued and ready to run the week of June 1

---

## 2026-05-24 (run: May 24, 2026)

### Angular 21.2.14 (May 20, 2026) — LTS Security Patch

- **Latest stable patch on the Angular 21.x LTS line** — `21.2.14` released May 20, 2026; routine bug fixes and stability improvements
- Angular 21's active support period ended May 19, 2026; it is now in **LTS** (security patches only until May 19, 2027)
- **Angular 22 is now 8 days away** — week of June 1, 2026 stable target; RC.0 (May 13) remains the latest pre-release; feature-locked
- **Signal Forms confirmed stable in v22** (the most impactful Angular forms change since v6 Reactive Forms)
- Teams should upgrade to Angular 22 as soon as it ships; `ng update @angular/core@22 @angular/cli@22`

---

### Nuxt UI v4.8.0 (May 21, 2026) — Theme Prop Defaults + FTS5 Search 🚀

- **`Theme` component prop defaults** — the `<UTheme :props="{ ... }">` component can now override default prop values for all descendant components; pass a `props` object keyed by component name; explicit per-component props always win; themes can be nested (innermost wins); propagated via Vue `provide`/`inject`
  ```vue
  <UTheme :props="{ button: { color: 'neutral', size: 'lg' }, tooltip: { arrow: true } }">
    <!-- All UButton children default to neutral/lg unless explicitly overridden -->
  </UTheme>
  ```
- **`ContentSearch` async FTS5 search** — the `<UContentSearch>` component now supports server-side full-text search via the `search` prop and the `useSearchCollection` composable (ships with `@nuxt/content` v3.14.0); replaces client-side Fuse.js loading-all-content approach; returns highlighted snippets; live on nuxt.com and ui.nuxt.com
- **New component props** — `Avatar`/`AvatarGroup` and `Breadcrumb` gain a `color` prop; `Separator` gains a `position` prop; `ChatMessage` adds `body` slot and `color` prop; `ChatPrompt` adds `submitOnEnter` control; `Checkbox`/`RadioGroup`/`Switch` add `highlight` prop for error ring styling
- **`DashboardGroup` `storageOptions` prop** — persist sidebar group state to localStorage or sessionStorage
- **`CommandPalette` description search** — description fields are now included in search and highlighting
- ⚠️ **Breaking: `InputMenu.autocomplete` renamed to `mode`** — the boolean `autocomplete` prop (added in v4.6.0) collided with the HTML `autocomplete` attribute; renamed to `mode` accepting `'combobox' | 'autocomplete'` (defaults to `'combobox'`)
  ```diff
  - <UInputMenu autocomplete :items="items" />
  + <UInputMenu mode="autocomplete" :items="items" />
  ```
- Nuxt UI now has **125+ components** (up from 100+ at v4.0 launch)
- `npm install @nuxt/ui@latest` → 4.8.0

---

### Svelte 5.55.9 (May 20, 2026) — Compiler Patch

- Routine compiler bug fixes; no API changes
- `npm install svelte@latest` → 5.55.9
- SvelteKit 2.60.1 remains the latest stable kit release (May 14, 2026)

---

## 2026-05-22 (run: May 22, 2026)

### Astro 6.3.7 / 6.3.6 (May 20–21, 2026) — Patch Cluster Continues

- **6.3.7** (May 21, 2026) — Routine bug fixes and dependency updates; follows rapid release cadence of the 6.3.x line
- **6.3.6** (May 20, 2026) — Bug fixes and stability improvements; no breaking changes
- **Current stable**: `npm install astro@latest` → 6.3.7
- **Astro 7.0.0-alpha.1** (May 9, 2026) — Second alpha of the Astro 7 pre-release series; Vite 8 + Rust-only compiler track; `npm install astro@alpha` to test (not production ready)
- Note: Astro is now averaging **a new patch release every 1–2 days** in the 6.3.x cycle — high velocity signals active production use and a healthy security/quality posture

---

### SvelteKit 2.60.1 / 2.60.0 (May 14, 2026) 🚀 New Minor

- **2.60.0** (May 14, 2026) — New minor release:
  - **`submit` and `hidden` form fields now accept numbers and booleans** — previously only strings were accepted; reduces `toString()` boilerplate for numeric/boolean form data
  - **Warn on unread form remote function validation issues** — when a form remote function returns validation errors that are never accessed in the component, SvelteKit now emits a console warning; reduces silent validation failure bugs
  - **Abort navigation after async rendering if obsolete** — fix for edge case where an async render completing after a subsequent navigation would incorrectly apply its result
  - **Skip refreshing queries on full-page reload form submissions** — prevents unnecessary query re-fetches on traditional full-page form submissions
- **2.60.1** (May 14, 2026) — Immediate patch:
  - **`query.batch` cross-talk prevention** — fix for a bug where batched queries could interfere with each other's response handling
  - `svelte` and `devalue` dependency bumps
- **Latest stable**: `npm install @sveltejs/kit@latest` → 2.60.1

---

### Next.js 16.3 Canary Progress (May 2026) 🔬 In Development

- **No stable Next.js release** since 16.2.6 (May 7, 2026); canary builds active
- **Notable canary features in progress** (from canary.20–canary.25, May 9–22, 2026):
  - `experimental.appShells` — new feature flag for App Shell pattern; experimental
  - `instrumentationClientInject` — new config for injecting client-side instrumentation code
  - MCP `compile_route` tool — AI agent/MCP integration for compiling individual routes
  - Turbopack: fixes for subpath imports to external packages, crashing webpack loader error reporting
  - `bfcacheId` — opt out of back/forward cache state preservation per-navigation
  - `next internal static-routes-info` CLI command
  - HTTP Cache-Control headers now respected with TTL-based invalidation for `fetch()`
  - `Honor Suspense-above-body opt-in for dynamic generateViewport`
- **Estimated stable release**: unknown; canary pace suggests late June or July 2026 for 16.3

---

### Angular 22 — 10 Days to Stable (June 1, 2026)

- **22.0.0-rc.0** (May 13, 2026) — Angular 22 is feature-locked in Release Candidate status
- The RC milestone means no new features; only critical bug fixes until the **week of June 1, 2026** stable
- Teams should begin audit/preparation now:
  - Check for any deprecated APIs (Signal Forms replaces ReactiveFormsModule long-term; OnPush will be the new default)
  - Review `@angular/core@22 @angular/cli@22` upgrade path via `ng update`
  - If Zoneless was not yet adopted, Angular 22 makes it the default for **new projects** only — existing zone.js projects unaffected
- **Angular 21.2.13** remains the latest stable on the v21 LTS line; `npm install @angular/core@21` for production

---

## 2026-05-20 (run: May 20, 2026)

### Nuxt 4.4.6 / 3.21.6 (May 18, 2026) + 🔒 Nuxt Security Advisory

- **Nuxt 4.4.6** (May 18, 2026) — latest stable patch. Fixes:
  - `vite`: use SPA entry for vite-node fallback
  - `vite`: invalidate SSR module cache when modules are invalidated via plugin hooks
  - `nuxt`: match deduplicated `resolveComponent` calls in JSX blocks
  - `nuxt`: prefer framework's own builder/server deps over hoisted packages
  - `nuxt`: update `useFetch` key even when `watch: false` is set
  - `nitro`: mark `@babel/plugin-syntax-typescript` as optional peer dep
  - `nitro`: add `.json` extension to payload cache items
  - `nuxt`: handle errors when fetching the app manifest
- **Nuxt 3.21.6** (May 18, 2026) — corresponding maintenance backport to the v3.21.x line
- **🔒 Security advisory** — Netlify's changelog (May 19, 2026) discloses multiple vulnerabilities patched in Nuxt 4.4.6+ (for 4.x) and corresponding 3.x patches; `@nuxt/rspack-builder` also patched. Teams on Nuxt 4.4.5 or earlier should upgrade immediately.
  ```bash
  npm install nuxt@latest  # installs 4.4.6
  ```

### Nuxt Content v3.14.0 (May 18, 2026) — Full-Text Search + Type Improvements

- **`useSearchCollection` composable** — new FTS5 full-text search composable; built on SQLite FTS5 under the hood; returns reactive search results against any Nuxt Content collection with zero extra config
- **Custom properties on `ContentConfig`** — `ContentConfig` type now accepts arbitrary custom properties, enabling typed CMS-specific metadata
- **`NOT IN` added to `SQLOperator` type** — expands the type-safe query builder
- **Bug fixes**: slugify options now correctly passed to the transformer; preview mode skips collections without a source in the preview template

### Astro 6.3.5 / 6.3.4 (May 18, 2026) — Patch Cluster

**6.3.5** (May 18, 2026):
- **CSP fix** — `position` prop on `<Image>` and `<Picture>` components was incorrectly breaking Content Security Policy hashes; now fixed
- **Improved error messages** — more consistent, correct wording across build and runtime errors
- **Stale SSR content fix** — dev server now properly invalidates SSR module cache when SSR-only modules change (e.g., `.astro` files outside project root in a monorepo); previously returning stale responses after module changes

**6.3.4** (May 18, 2026):
- **`experimental.advancedRouting` — `fetchFile` option** — customize or disable the app entry file path (`src/app.ts` → custom path); `fetchFile: false` disables generation
- **`FetchState.response` property** — automatically set after `pages()` or `middleware()` completes, available for downstream inspection
- **`App.Providers` interface** — new namespace extension point for typing custom context providers on `Astro` and `ctx`
- **`Fetchable` type export** — new type for typing the advanced routing entrypoint (`satisfies Fetchable`)
- **Hono cache middleware fix** — `cache()` middleware now follows the standard wrapper pattern correctly
- **Latest stable: 6.3.5** — `npm install astro@latest` → 6.3.5

### Astro 6.3.3 (May 14, 2026) 🔒 Security Fix

- **🔒 XSS fix** — slot names on hydrated (island) components were not HTML-escaped in SSR output; a maliciously named slot could have resulted in a reflected XSS. Upgrade immediately if you use dynamic slot names with SSR.
  - Affected: Astro < 6.3.3 with SSR and Islands architecture
  - Fixed: [`astro@6.3.3`](https://github.com/withastro/astro/releases/tag/astro%406.3.3)

---

## 2026-05-18 (run: May 18, 2026)

### Angular 19 EOL Has Passed — Angular 21 Now in LTS ⚠️

- **Angular 19.x officially reached end-of-life on May 19, 2026** (yesterday) — Google has issued no further security patches for any 19.x release. Teams still running Angular 19 in production are on entirely unsupported software.
- **Angular 21.x active support ended May 19, 2026** — v21 now transitions fully to LTS (security patches only until May 19, 2027). No new features will ship on the v21 line.
- **Angular CLI 22.0.0-rc.0 released May 13, 2026** — Angular 22 is now in Release Candidate. The RC milestone means no new features will be added; only critical bug fixes and stability work remain before the **week-of-June-1, 2026** stable release.
- **Angular 21.2.13** (May 13, 2026) — latest stable patch on the 21.x line; upgrade immediately.

### React Router v7.15.1 (May 14, 2026) + v7.15.0 (May 5, 2026) 🚀 New Releases

**v7.15.0 (May 5, 2026):**
- **API stabilizations in preparation for React Router v8** — the team explicitly flagged this as a pre-v8 stabilization release. APIs previously marked as `unstable_` have been promoted to stable. If you were using any unstable APIs, this is the release to audit.
- **15–30% server-side route matching performance improvement** — cached flattened/ranked route branches during server-side matching; avoids redundant `matchRoutes` calls in Data/Framework Mode
- Route matching optimization for Framework/Data Mode (built on the fix for the earlier regression in 7.6.0)

**v7.15.1 (May 14, 2026):**
- **`unstable_useRouterState()` hook** — new consolidated hook (Data/Framework/RSC Mode) providing a single access point for both active and pending router states; designed to replace a collection of individual hooks (`useNavigation()`, `useFormAction()`, etc.) that will likely be deprecated in v8 and possibly removed in v9
  ```ts
  let { active, pending } = unstable_useRouterState();
  // replaces: useNavigation().formData, useNavigation().json, etc.
  ```
- **React Router v8 now expected "in the next month or two"** (per official v7.15.0 release notes — May 5, 2026); the stabilization work in 7.15.x is the final preparation; ESM-only, Node 20 dropped, RSC Framework Mode stabilization expected

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
