# Next.js

> Maintained by Vercel. The dominant React meta-framework for production applications.

## Latest Version

**16.2.9** (June 9, 2026) — Latest stable patch  
**16.x** is the current LTS major (released October 21, 2025)  
**15.5.19** (June 1, 2026) — Latest 15.x patch (LTS until October 2026)

## Key Features

- **App Router** (stable since v13) — file-system routing with React Server Components, layouts, nested routing, Server Actions
- **Pages Router** — now in maintenance mode; still fully supported
- **Turbopack** — Rust-based bundler; stable for both `next dev` and `next build` (production builds stable as of 16.x); default bundler for all new projects
- **React Server Components (RSC)** — first-class support; the default rendering model in App Router
- **Cache Components** — replaced experimental PPR in Next.js 16; static shell + streaming dynamic content; uses `"use cache"` directive
- **React Compiler (stable)** — automatic memoization of components; enabled via `reactCompiler: true` in `next.config.ts`; no manual `useMemo`/`useCallback` needed
- **Server Actions** — production-ready for forms and mutations
- **React 19.2** — required for Next.js 16.x; includes View Transitions, `useEffectEvent`, and Activity component
- **`proxy.ts`** — replaces deprecated `middleware.ts`; clarifies network boundary; Node.js runtime only (edge runtime continues to use `middleware.ts`)

## Rendering Modes

| Mode | Description |
|---|---|
| SSR | Per-request server rendering (default in App Router) |
| SSG | Static generation at build time |
| ISR | Incremental Static Regeneration — revalidate on a timer or on-demand |
| CSR | Client-only via `"use client"` components |
| PPR (experimental) | Static outer shell served immediately; dynamic inner streamed in |

## Deployment Targets

- **Vercel** — native, zero-config; best DX and full feature support
- **Node.js** — `next start` or standalone output mode
- **Docker / self-hosted** — well-supported
- **Edge (Middleware)** — Cloudflare Workers, Vercel Edge, Deno Deploy via adapters
- **Static export** — `output: 'export'` for CDN/S3 deployment (limits dynamic features)
- **OpenNext / Adapters API (stable in 16.2)** — enables deployment to any cloud (AWS, Cloudflare, etc.) via community adapters

## Next.js 16.3 Canary (In Development)

**16.3.0-canary.61** (June 23, 2026) — Latest canary. A dedicated `16.3.x-preview` release branch is open; the preview tag (`npm install next@preview`) enables Turbopack filesystem cache for builds by default in non-stable releases. **Vercel Ship Berlin is June 25, 2026** (London event was June 17 — recap at vercel.com/blog/vercel-ship-2026-recap); the London keynote focused on agentic infrastructure, eve framework, and Vercel Services (launching July 1) but did not announce Next.js 16.3 stable. **16.3 stable remains imminent** — the Berlin event (June 25) is the next likely announcement opportunity. Notable features landing in canary/preview:
- **`experimental.appShells`** — App Shell prefetching pattern (experimental flag)
- **`instrumentationClientInject`** — client-side instrumentation injection config
- **MCP `compile_route` tool** — AI/MCP agent can compile individual routes
- **HTTP Cache-Control TTL-based invalidation** — `fetch()` now respects `Cache-Control` headers for TTL-based revalidation
- **`next/root-params`** — new API for accessing root layout params
- **ISR with Cache Components + `experimental.partialFallbacks`** — partial fallback rendering in ISR builds
- React canary bump: upgraded to `43bcbf80-20260603`
- Turbopack: continued bug fixes; 200+ improvements in progress

**Estimated 16.3 stable release:** **Late June 2026** — a `16.3.x-preview` branch opened June 10 and Vercel Ship is June 25, strongly suggesting 16.3 stable will land around that event.

## v16.2 Highlights (March 18, 2026)

- **~400% faster `next dev` startup** with Turbopack
- **~50% faster rendering**
- **Stable Adapters API** — third-party platforms can customise the build process; enables OpenNext collaboration
- **Server Fast Refresh** — fine-grained hot reloading for server components
- **Browser Log Forwarding** — dev terminal shows browser errors; key for AI agent debugging
- **Hydration Diff Indicator** — clear server/client diff in the error overlay
- **`--inspect` for `next start`** — attach Node.js debugger to production server
- **Agent DevTools (experimental)** — gives AI agents terminal access to React DevTools
- **`AGENTS.md` in `create-next-app`** — scaffold AI-ready projects by default
- **`unstable_catchError()`** — granular component-level error boundaries
- **Redesigned 500 error page**
- **Subresource Integrity (SRI)** for JS assets
- **Tree shaking of dynamic imports**

## npm Download Trend

Next.js is the most-downloaded React meta-framework by a wide margin. npm weekly downloads have grown consistently over the past 5 years. Estimated market share: ~67% of new enterprise React projects in 2026.

## Trade-Off Assessment

**Choose Next.js when:**
- You need the richest React ecosystem and broadest community support
- Your team is already React-native
- You need flexible rendering (SSR + SSG + ISR + PPR) in one framework
- AI-assisted development is a priority (largest training corpus, best tooling)
- You need robust e-commerce, SaaS, or content platform support

**Watch out for:**
- **Vercel coupling** — some features (e.g. advanced ISR, edge middleware optimisations) work best on Vercel; OpenNext/Adapters API is improving this story
- **App Router complexity** — Server Components + Client Components mental model has a steep learning curve (~1-2 weeks to become productive for new developers)
- **Frequent breaking changes** between majors — budget 2–4 hours per major upgrade
- **Over-engineered for simple static sites** — Astro is likely a better fit

## Security Notes

- **16.2.9** (June 9, 2026) — Empty release to fix `next@latest` NPM dist-tag (Trusted Publishing constraints prevent direct dist-tag updates; a new release was required); no code changes from 16.2.8
- **16.2.7 / 15.5.19** (June 1, 2026) — Bug-fix backport patch; all users on 16.x and 15.x should upgrade
- **16.2.6 / 15.5.18** (May 7, 2026) — ⚠️ Coordinated release addressing **13 security advisories** including:
  - **CVE-2026-23870** — High: DoS in React Server Components (upstream React issue); patched in `react-server-dom-*` 19.x.6
  - **CVE-2026-44578** — High: SSRF in applications using WebSocket upgrades
  - **CVE-2026-44574** — High: Middleware/proxy bypass via dynamic route parameter injection (no WAF mitigation possible)
  - **CVE-2026-44581** — High: XSS via CSP nonces in App Router
  - Middleware/proxy bypass via App Router segment-prefetch routes (GHSA-267c-6grr-h53f)
  - Middleware/proxy bypass via Pages Router i18n (additional advisory)
  - DoS via connection exhaustion in Cache Components (GHSA-mg66-mrh9-m8jx)
  - DoS via Image Optimization API (GHSA-h64f-5h5j-jqjh)
  - Cache poisoning and additional XSS vectors
  - ⚠️ **WAF rules are not sufficient** — Vercel explicitly states these vulnerabilities cannot be reliably blocked at the WAF layer; patching is the only complete mitigation
  - **Next.js 13.x and 14.x are also affected** — no patches planned; users must upgrade to 15.5.18 or 16.2.6
- **CVE-2026-23869** — security vulnerabilities patched in 16.2.3 and 15.5.15 (April 8, 2026)
- **CVE-2025-66478** — critical RCE in RSC protocol (December 2025); patched in 15.x and 16.x
- **CVE-2025-55184 / CVE-2025-55183** — DoS and source code exposure in RSC (December 2025); patched

## Support Policy

| Release | Status | EOL |
|---|---|---|
| 16.x | Active LTS | ~Oct 2027 |
| 15.x | LTS | Oct 21, 2026 |
| 14.x | Ended | Oct 26, 2025 |
| 13.x | Ended | Dec 21, 2024 |
