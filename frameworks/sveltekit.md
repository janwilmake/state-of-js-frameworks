# SvelteKit

> Maintained by the Svelte core team (Rich Harris et al., now at Vercel). The compiler-first full-stack framework with the best developer satisfaction scores in its class.

## Latest Version

**SvelteKit 2.69.2** (July 8, 2026) — 🚀 Current stable  
**SvelteKit 2.69.0** (July 6, 2026) — New minor: `submitted` property on remote forms  
**SvelteKit 2.68.0** (July 2, 2026) — Previous minor  
**SvelteKit 2.67.0** (July 2, 2026) — Previous minor  
**SvelteKit 3.0.0-next.7** (July 7, 2026) — Pre-release preview (not production ready); Vite Environment API, Rolldown  
**Svelte 5.x** (July 2026) — Underlying compiler  
Built on **Vite 8** compatible; no webpack dependency

## Key Features

- **Compiler-based** — Svelte compiles components to vanilla JS at build time; no virtual DOM, no runtime framework overhead
- **Svelte 5 Runes** (stable) — `$state`, `$derived`, `$effect`, `$props` replace the old `$:` reactive syntax; more predictable, composable, TypeScript-friendly
- **File-based routing** — `+page.svelte`, `+page.server.ts`, `+layout.svelte`, `+server.ts` conventions
- **Load functions** — `load()` in `+page.server.ts` runs server-side; typed via auto-generated `$types`
- **Form Actions** — progressive enhancement built-in; forms work without JavaScript
- **Server-side error boundaries** (new in kit@2.54.0) — error boundaries now catch server-side errors, not just client-side
- **Type-narrowed params** (new in kit@2.55.0) — matcher-constrained params are now properly narrowed in `$app/types`, `$app/state`, and hooks
- **`svelte.config.js` functions** (new in svelte@5.54.0) — `css`, `runes`, `customElement` options can now be functions for per-file configuration
- **Svelte MCP** — Model Context Protocol integration for AI-assisted development via `sv` CLI and OpenCode
- **TypeScript 6.0 support** (new in kit@2.56.0) — SvelteKit now supports TypeScript 6.0
- **Remote Functions `query.live`** (new, experimental) — `query.live()` enables real-time streaming queries via async generators; server sends continuous updates to the client; `connected` property and `reconnect()` method expose connection state; multiple component instances share a single connection
- **Remote Functions improvements** (kit@2.56.0 — breaking changes) — `run()` method added to queries; `hydratable` transport for richer data types; `field.as(type, value)` for default form field values; server-gated client refreshes; several API stabilization changes
- **`form.submit` returns `boolean`** (new in kit@2.57.0) — indicates submission validity for enhanced remote form functions
- **Adapter system** — deploy anywhere via first-party and community adapters
- **Vite integration** — fast HMR, clear config, predictable build performance

## Rendering Modes

| Mode | Description |
|---|---|
| SSR | Per-request server rendering (default) |
| SSG | Static pre-rendering via `prerender = true` in `+page.server.ts` |
| SPA | Client-only via `ssr: false` in `svelte.config.js` |
| CSR | Per-page opt-out via `export const ssr = false` |
| Hybrid | Mix SSR/SSG/SPA per-route via page options |
| Edge SSR | Deploy SSR to Cloudflare Workers, Vercel Edge via adapters |

SvelteKit does not have ISR or PPR equivalents. Cache-control headers must be set manually in server `load` functions or via CDN configuration.

## Deployment Targets

- **Vercel** — `@sveltejs/adapter-vercel`; zero-config; experimental Bun runtime support (6.1.0)
- **Cloudflare Workers / Pages** — `@sveltejs/adapter-cloudflare`
- **Node.js** — `@sveltejs/adapter-node`
- **Netlify** — `@sveltejs/adapter-netlify`
- **Static** — `@sveltejs/adapter-static` → CDN/S3
- **AWS Lambda** — `@sveltejs/adapter-aws` (community)
- **Bun** — experimental via `@sveltejs/adapter-vercel` Bun runtime
- **Auto** — `@sveltejs/adapter-auto` detects environment at deploy time

## July 2026 Highlights

- **"What's New in Svelte: July 2026"** (July 1, 2026) — headline theme: configuration consolidation and SvelteKit 3 previews. Key changes that landed in June/July:
  - **SvelteKit config in `vite.config.js`** (new in kit@2.62.0) — you can now pass your SvelteKit config directly to the Vite plugin; `svelte.config.js` is no longer required; this is a preview of how SvelteKit 3 will **require** config to live in `vite.config.js`
  - **Experimental explicit environment variables** (new in kit@2.63.0) — declare and type env vars in one place; preview of how `$env/*` modules will work in SvelteKit 3
  - **Svelte CLI (`sv`) updates** — `sv@0.16.0`: demo template now uses `{const ...}` declaration tags; `sv create` scaffolds against `^2.62.0` with config in the Vite plugin by default; new experimental add-on to toggle experimental flags from CLI; `drizzle` and `better-auth` add-ons support new explicit env vars; new `defineEnv` and `svelteConfig` helpers in `sv-utils@0.3.0`
  - **Language tools** catch up with Svelte's new `{const ...}` declaration tags — whole toolchain now in sync

- **SvelteKit 2.69.2** (July 8, 2026) — **Latest stable**:
  - Fix: set `define` values on `globalThis` when running Vitest
  - Note: `@sveltejs/adapter-node@6.0.0-next.2` (July 6) and `@sveltejs/kit@3.0.0-next.7` (July 7) continue the SvelteKit 3 pre-release track; the next major introduces a **breaking change** to origin configuration — **`kit.prerender.origin` and the adapter-node `ORIGIN` environment variable are removed** in favor of a new `kit.paths.origin` config option; update your configuration when migrating to SvelteKit 3.

- **SvelteKit 2.69.1** (July 6, 2026):
  - ⚠️ **Security-adjacent** — Fix: prevent prototype pollution when deleting file inputs
  - Fix: prevent unhandled promise rejection in request handling

- **SvelteKit 2.69.0** (July 6, 2026):
  - **`submitted` property on remote forms** — `form.submitted` is now exposed as a reactive property; simplifies tracking whether a remote form has been submitted at least once (e.g., for showing validation errors only after first submit)
  - Fix: clear issues and touched states on form reset
  - Fix: return `undefined` from `fields.branch.issues()` when only leaf has issues

- **SvelteKit 2.68.0** (July 2, 2026) — minor release with improvements to remote functions and adapters

- **SvelteKit 2.67.0** (July 2, 2026) — minor release

- **SvelteKit 3.0.0-next.5 / next.6 / next.7** (July 5–7, 2026) — Pre-release track active; adapters progressing to next major pre-releases (`adapter-node@6.0.0-next.2`, `adapter-cloudflare@8.0.0-next.1`, `adapter-netlify@7.0.0-next.2`); not production ready

```bash
npm install @sveltejs/kit@latest   # → 2.69.2
```

---

## June 2026 Highlights

- **SvelteKit 2.66.0** (June 18, 2026) — **Latest stable**:
  - **Precompress prerendered `.md` and `.mdx` files** — adapters now pre-compress Markdown files at build time; meaningful for documentation sites served via `adapter-node`
  - **Boolean input optional warning** — warns when boolean form inputs (checkboxes) are not marked optional in form schemas; catches a common foot-gun
  - Fix: `query.live` reconnect stability — three fixes preventing deadlocks, value loss, and `for await` consumer drops during reconnection
  - Fix: blur active element before navigation component update so blur/focusout handlers fire with valid component data
  - Fix: `base` available in `$service-worker` during development
  - Fix: correct relative asset paths in error pages for missing `__data.json` requests
  - Fix: remove `types: ['node']` from generated tsconfig
  - Fix: prefer pages over endpoints when prerendering
  - Fix: restore snapshots after `afterNavigate` callbacks
  - Fix: `ws:` / `wss:` and `trusted-types-eval` as valid CSP sources
  - Fix: omit empty `file` inputs from remote form data
  - Fix: blank page in SPA mode when root layout `load()` throws
  - `npm install @sveltejs/kit@latest` → **2.66.0**

- **SvelteKit 2.65.2** (June 16, 2026) — **Patch release** (superseded by 2.66.0):
  - Fix: throw error when prerendering a root `+server.js` that returns a non-HTML response (previously silently misbehaved)
  - Fix: decode base64-serialized fetch bodies before caching for client-side replay
  - Fix: correctly access explicit dynamic public env vars from prerendered pages and service workers
  - Fix: allow `preloadCode` to be called during initial page load
  - Fix: send `cache-control: private, no-store` on remote function responses so personalized query results can never be cached by shared caches
  - Fix: preserve HTTP status and error body when a remote function request fails in transport

- **SvelteKit 2.65.0** (June 11, 2026) — **New minor release**:
  - **Queries can now refresh other queries** — a query handler can explicitly trigger a refresh of sibling queries; enables dependency-chain invalidations without manual coordination
  - Fix: deduplicate remote data fetched across multiple instances
  - Fix: skip client build entirely when all routes have CSR disabled (faster SSG builds)
- **SvelteKit 2.64.0** (June 8, 2026) — Commands can now receive `File` objects; fix: avoid server components being bundled when SSR is turned off for a route
- **SvelteKit 2.63.1** (June 2026) — `query.live` now uses SSE (Server-Sent Events) instead of polling; Windows `env.d.ts` import path fix (forward slashes); `$app/environment` warning fix with `explicitEnvironmentVariables`; improved explicit env var import handling
- **SvelteKit 3.0.0-next.4 / next.3 / next.1 / next.0** (June 5–11, 2026) — **Pre-release preview of SvelteKit 3** — major changes:
  - **Vite Environment API** — faster builds with Vite hook filters; more powerful SvelteKit adapters leveraging the Vite Environment API
  - **`data-sveltekit-*` option `'off'` removed** — use `false` instead (breaking change)
  - **Explicit env vars** — new `explicitEnvironmentVariables` feature (3.0.0-next.3)
  - **Query deduplication** — remote data deduped across component instances (3.0.0-next.3)
  - **Query cross-refresh** — queries can refresh other queries (3.0.0-next.3)
  - **Reset queries before navigation** when `invalidateAll` is set (3.0.0-next.4)
  - Adapters (`adapter-node`, `adapter-static`, `adapter-vercel`) bumped to v6/v7 next pre-releases requiring SvelteKit 3
  - `adapter-node` migrates from Rollup to **Rolldown** (Rust-based bundler from VoidZero/Cloudflare)
  - Paths resolve using Vite config `root` option instead of `process.cwd()` (better monorepo support)
  - `Response` helpers deprecated in favour of platform-provided alternatives
  - Not production ready; install with `npm install @sveltejs/kit@next`
- **"What's New in Svelte: June 2026"** (June 1, 2026) — official monthly recap published; highlights: improved forms, new long-lived remote query APIs (`query.live`), TypeScript 6 support in language-tools; **`run()` method removed** from remote queries in `2.61.0` — use `await query()` directly in all contexts; remote queries can now be awaited in event handlers, async callbacks, and module scope with cache deduping

## May 2026 Highlights

- **SvelteKit 2.60.1** (May 14, 2026) — `query.batch` cross-talk prevention fix; `svelte` and `devalue` dependency bumps
- **SvelteKit 2.60.0** (May 14, 2026) — `submit` and `hidden` form fields now accept numbers and booleans (not just strings); warn on unread `form` remote function validation issues; abort navigation after async rendering if obsolete; skip refreshing queries on full-page reload form submissions
- **SvelteKit 2.59.1** (May 5, 2026) — Windows drive-letter path resolution fix for route files; minor `RemoteCommand` output type fix; fixes for `form.fields.foo.as('checkbox', default_value)` and remote form default value resets on submit
- **`query.live` — Real-time streaming queries** — `kit@2.57` ships `query.live()` using async generators; enables real-time subscriptions (e.g., live notifications, live clocks) without WebSocket boilerplate; the server streams data, SvelteKit manages the connection lifecycle; community reception is very positive
- **`form.submit` returns `boolean`** — `kit@2.57.0` — form submit now signals validation outcome, reducing boilerplate in conditional submission flows
- **Svelte CLI Community Add-ons** (experimental, May 2026) — `sv` CLI now supports experimental community-contributed plugins; ecosystem extensibility without official package overhead; featured at ThoughtWorks Technology Radar May 2026
- **ThoughtWorks Technology Radar** — Svelte featured in the May 2026 edition as a framework to adopt

## April 2026 Highlights (latest: SvelteKit 2.58.0 — April 23, 2026)

- **`requested` API stabilization (2.58.0)** — `requested` in remote query handlers now requires a `limit` option and yields `{ arg, query }` entries instead of validated args directly; `RemoteQueryFunction` gains an optional third generic `Validated` for post-validation argument types; FOUC fix for CSR-only pages; form results correctly reset on redirect
- **TypeScript 6.0 support** — `kit@2.56.0` — SvelteKit now supports TypeScript 6.0
- **Remote Functions breaking changes (2.56.0)** — `run()` method added to queries; `hydratable` transport for richer data types; server-gated client-driven refreshes; `field.as(type, value)` default form field values; users upgrading from 2.55.x to 2.56.x must review the breaking change list
- **Server-side error boundaries** — `kit@2.54.0` allows error boundaries to catch errors thrown on the server during SSR, closing a long-standing gap with React's error boundary model
- **Type-narrowed params with matchers** — `kit@2.55.0` properly narrows param types when route matchers are used (e.g., `[id=integer]` narrows `id` to `string` matching the integer pattern)
- **Svelte MCP in OpenCode** — `sv@0.12.6` ships the Svelte MCP plugin config in `.opencode/` for AI-assisted development
- **`svelte.config.js` function options** — `svelte@5.54.0` allows `css`, `runes`, and `customElement` to be functions, enabling per-file or conditional configuration
- **New `svelte/motion` types exported** — `TweenOptions`, `SpringOptions`, `SpringUpdateOptions`, `Updater` are now public
- **Best practices guide** — new official [best practices guide](https://svelte.dev/docs/svelte/best-practices) added to the Svelte docs

## npm Download Trend

SvelteKit has ~1.5–2M weekly downloads — a fraction of Next.js but growing steadily. Developer satisfaction scores consistently lead the field (93%+ in State of JS surveys). The smaller download count reflects Vue/React ecosystem lock-in rather than quality issues. Teams that try SvelteKit tend to stay.

## Bundle Size Advantage

SvelteKit applications typically ship **20–40 KB** of JavaScript for a minimal app vs. **80–120 KB+** for an equivalent Next.js App Router app. This gap narrows on data-heavy applications but remains meaningful for content sites and SPAs.

## Trade-Off Assessment

**Choose SvelteKit when:**
- You're a solo developer or small team that wants the best DX-to-productivity ratio
- Bundle size and Core Web Vitals matter (e-commerce, content sites, SaaS MVPs)
- You find React's hooks mental model or Server Components complexity a barrier
- You're building a new project without legacy React constraints
- Progressive enhancement and accessibility are first-class concerns

**Watch out for:**
- **Smaller ecosystem** than React/Next.js — fewer UI component libraries, CMS plugins, auth integrations
- **Svelte 5 migration** — teams on Svelte 4 need to learn Runes; the old `$:` syntax is now legacy
- **No ISR** — you'll need to implement cache invalidation patterns yourself or use a CDN
- **Hiring** — far fewer Svelte developers in the job market vs. React; can be a constraint for teams scaling
- **Vercel ownership concern** — Rich Harris (Svelte creator) is a Vercel employee; while Svelte is MIT-licensed and community-driven, the incentive structure exists

## Support Policy

SvelteKit follows semantic versioning. The `2.x` series is currently stable. **SvelteKit 3** pre-releases started June 5, 2026 — based on Vite Environment API; no stable release date announced yet. No formal LTS policy; patch releases are frequent and backward-compatible within a major version.
