# SvelteKit

> Maintained by the Svelte core team (Rich Harris et al., now at Vercel). The compiler-first full-stack framework with the best developer satisfaction scores in its class.

## Latest Version

**SvelteKit 2.58.0** (April 23, 2026) — Current stable  
**Svelte 5.x** (May 2026) — Underlying compiler  
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

## May 2026 Highlights

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

SvelteKit follows semantic versioning. The `2.x` series is currently stable. No formal LTS policy; patch releases are frequent and backward-compatible within a major version.
