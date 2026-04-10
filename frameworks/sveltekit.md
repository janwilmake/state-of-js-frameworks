# SvelteKit

> Maintained by the Svelte core team (Rich Harris et al., now at Vercel). The compiler-first full-stack framework with the best developer satisfaction scores in its class.

## Latest Version

**SvelteKit 2.55.0** (April 2026) — Current stable  
**Svelte 5.55.0** (April 2026) — Underlying compiler  
Built on **Vite**; no webpack dependency

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

## April 2026 Highlights

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
