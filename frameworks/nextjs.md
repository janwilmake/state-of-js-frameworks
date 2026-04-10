# Next.js

> Maintained by Vercel. The dominant React meta-framework for production applications.

## Latest Version

**16.2.3** (April 8, 2026) — Latest stable patch  
**16.x** is the current LTS major (released October 21, 2025)  
**15.5.15** (April 8, 2026) — Latest 15.x security patch (LTS until October 2026)

## Key Features

- **App Router** (stable since v13) — file-system routing with React Server Components, layouts, nested routing, Server Actions
- **Pages Router** — now in maintenance mode; still fully supported
- **Turbopack** — Rust-based bundler; stable for `next dev`; production builds in beta on 16.x
- **React Server Components (RSC)** — first-class support; the default rendering model in App Router
- **Partial Prerendering (PPR)** — experimental static shell + streaming dynamic content in one response
- **Server Actions** — production-ready for forms and mutations
- **React 19** — required for Next.js 16.x

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

- **CVE-2026-23869** — security vulnerabilities patched in 16.2.3 and 15.5.15 (April 8, 2026); all users should upgrade
- **CVE-2025-66478** — critical RCE in RSC protocol (December 2025); patched in 15.x and 16.x
- **CVE-2025-55184 / CVE-2025-55183** — DoS and source code exposure in RSC (December 2025); patched

## Support Policy

| Release | Status | EOL |
|---|---|---|
| 16.x | Active LTS | ~Oct 2027 |
| 15.x | LTS | Oct 21, 2026 |
| 14.x | Ended | Oct 26, 2025 |
| 13.x | Ended | Dec 21, 2024 |
