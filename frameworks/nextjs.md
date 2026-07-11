# Next.js

> Maintained by Vercel. The dominant React meta-framework for production applications.

## Latest Version

**16.2.10** (July 1, 2026) — Latest stable patch (republishes `@next/swc-wasm-web` missed since 16.2.4; no code changes)  
**16.x** is the current LTS major (released October 21, 2025)  
**15.5.20** (July 1, 2026) — Latest 15.x patch (LTS until October 2026)  
**16.3** — In active preview (`npm install next@preview`); **NOT yet stable** as of July 9, 2026

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

## Next.js 16.3 Preview (Active — Stable Imminent)

**16.3.0-canary.76** (July 8, 2026) — Latest canary. **16.3.0-preview.5** also active. `npm install next@preview` to test. **16.3 stable has NOT shipped** as of July 9, 2026, despite the features being announced at Vercel Ship Berlin (June 25); the team is working through final stabilization of Instant Navigations. Based on community feedback the canary is getting heavy production testing (users reporting memory drops from ~20 GB to ~5 GB with Turbopack improvements alone). Notable features in 16.3 preview:
- **Instant Navigations** — Stream, Cache, or Block to make navigations SPA-fast while remaining server-driven; new `prefetch` behavior; **Partial Prefetching** for route shells
- **Bundled docs through `AGENTS.md`** — AI agents read version-matched docs from `node_modules`
- **First-party Skills** — agents drive multi-step workflows (dev loop, Cache Components adoption)
- **Agent Browser with React introspection** — `agent-browser` CLI drives a real browser, inspects React state
- **Actionable errors** — paste-ready fix prompts in the error overlay
- **A smaller, more focused MCP server** — diagnostics in, knowledge base out
- **Docs as Markdown** — append `.md` to any Next.js docs URL
- **Turbopack: Memory Eviction** — reclaim compiler memory during long dev sessions (huge DX win)
- **Turbopack: Persistent Cache for Builds** — reusable build cache across successive builds
- **Turbopack: Rust React Compiler** (experimental `turbopackRustReactCompiler`) — 20–50% compilation wins vs Babel transform on large apps like v0
- **`import.meta.glob`** — Vite-compatible glob imports in Turbopack
- **`next/root-params`** — new API for accessing root layout params
- **HTTP Cache-Control TTL-based invalidation** — `fetch()` now respects `Cache-Control` headers

**Estimated 16.3 stable release:** **Mid-to-late July 2026** — **16.3.0-canary.83** (July 10, 2026) is the latest canary; the preview branch is active (`npm install next@preview`). No stable release date announced yet; the team continues to stabilize Instant Navigations and Turbopack Memory Eviction. Community production testing of the canary has been very positive (significant memory drops reported). Watch [nextjs.org/blog](https://nextjs.org/blog).

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

- **16.2.10** (July 1, 2026) — Republishes `@next/swc-wasm-web` which was accidentally not published since 16.2.4; no other changes
- **15.5.20** (July 1, 2026) — Same purpose: republishes `@next/swc-wasm-web` for the 15.x line
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
| 15.x | LTS | Oct 21, 2026 | latest: 15.5.20 |
| 14.x | Ended | Oct 26, 2025 |
| 13.x | Ended | Dec 21, 2024 |
