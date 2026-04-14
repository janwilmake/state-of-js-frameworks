# Remix / React Router

> Maintained by Shopify. The framework that bet on web standards — and won. In 2024, Remix merged into React Router v7. Remix 3 is now a separate, pre-React project in active development.

## Current State (April 2026)

**Remix as a standalone React framework no longer exists.** The key facts:

- **React Router v7** (released November 2024) absorbed all of Remix v2's patterns — loaders, actions, nested routing, server rendering. This is the production-ready successor to Remix v2.
- **Remix 3** is a completely separate new framework, forking Preact (not React). It is under active development and has **no migration path from Remix v2**. If you're in the React ecosystem, Remix 3 is not for you — yet.

For teams evaluating "Remix", the practical question is: **React Router v7 in Framework Mode** vs. **Next.js 16**.

## React Router v7 — Latest Version

**v7.14.1** (April 13, 2026) — Current stable  
**v7.14.0** (April 2, 2026) — Added Vite 8 support  
28M+ weekly npm downloads (react-router package)  
Backed by **Shopify** (powers Hydrogen, Admin)

## Key Features (React Router v7 Framework Mode)

- **Loaders** — async server-side data fetching per route; co-located with components
- **Actions** — server-side mutations; forms work without JavaScript (progressive enhancement)
- **Nested routing** — fine-grained layouts and data loading trees
- **SSR-first** — everything server-renders by default; CSR is opt-in
- **Web Standards** — built on `Request`/`Response`, `FormData`, and `URL` APIs
- **File-based routing** — routes directory with loader/action co-location
- **Streaming** — built-in support via `defer()` and `<Await>`
- **Type safety** — generated types for `params`, `loaderData`, and `actionData`
- **Vite 8 support** (v7.14.0+) — stay current with Vite's ESM-first ecosystem
- **TypeScript 6 support** (v7.14.1+) — peer dep range includes TypeScript 6 pre-releases
- **Unstable RSC Framework Mode** — React Server Components support in active development; not yet production-ready
- **Zero vendor lock-in** — deploy to any Node.js, edge, or serverless environment

## Rendering Modes

| Mode | Description |
|---|---|
| SSR | Per-request server rendering (default) |
| SSG | Static pre-rendering via `loader` with `headers` returning long cache |
| CSR | Client-only via `clientLoader` / `clientAction` |
| Streaming | `defer()` + `<Await>` for progressive data delivery |

React Router v7 does **not** have ISR or PPR equivalents. Cache invalidation is handled at the CDN/edge layer by the developer.

## Deployment Targets

- **Node.js** — first-class via `@react-router/node`
- **Cloudflare Workers / Pages** — `@react-router/cloudflare`
- **Vercel** — `@react-router/vercel` adapter
- **Netlify** — community adapter
- **AWS Lambda** — community adapter
- **Custom** — build your own adapter via `createRequestHandler`

No platform lock-in. Adapters are thin wrappers around `Request`/`Response`.

## React Router v7 — Recent Releases

| Version | Date | Highlights |
|---|---|---|
| v7.14.1 | April 13, 2026 | TypeScript 6 peer dep support, race condition fix in `HydrateFallback`, normalize double-slashes in redirects |
| v7.14.0 | April 2, 2026 | **Vite 8 support**, memory leak fix in `turbo-stream`, pre-rendering with `v8_viteEnvironmentApi`, unstable RSC Framework Mode improvements |
| v7.13.2 | March 23, 2026 | Bug fixes |
| v7.13.0 | January 23, 2026 | `crossOrigin` prop on `<Links>`, origin check returns 400, glob matching fix |
| v7.12.0 | January 7, 2026 | 🔒 Security: CSRF protection, XSS fixes, CSRF in ScrollRestoration; `allowedActionOrigins` config |

## React Router v8 — In Planning

React Router v8 is in active planning (discussion opened October 2025). Expected changes:
- **ESM only** — drop CJS builds (Vite 7+ and Node 20.19+/22.12+ `require(esm)` enable this)
- **Drop Node 20** support (EOL April 2026)
- **React Server Components (RSC) Framework Mode** — experimental RSC support being developed for stabilization
- Expected sometime in 2026 once future flags stabilize

---

## Remix 3 (Experimental — Not Production Ready)

Remix 3 is a ground-up rebuild on Preact. Key points:
- **No React dependency** — uses Preact as the UI layer
- **No migration path** from Remix v2 or React Router v7
- **Batteries-included, bundler-free** design philosophy
- Expected early 2026 (pre-release); follow [remix.run](https://remix.run) for updates
- **Backed by Shopify** — well-funded but a significant architectural bet

**Recommendation:** Do not adopt Remix 3 for new production projects until it reaches stable release and the ecosystem matures.

## npm Download Trend

React Router (the package) has ~28M weekly downloads — more than Next.js — because it is used both as a standalone client router and as a full-stack framework. The framework mode (Remix-style) is a subset of this figure. Remix v2 downloads are declining as teams migrate to React Router v7.

## Trade-Off Assessment

**Choose React Router v7 when:**
- Web standards compliance and progressive enhancement matter (government, accessibility-critical apps)
- You want zero vendor lock-in and true deploy-anywhere portability
- Your team finds the Server Components mental model in Next.js too complex
- You're building content-heavy SSR apps with clear data/mutation boundaries
- You're already using TanStack ecosystem (excellent interop)

**Watch out for:**
- **No ISR/PPR** — cache-busting is your responsibility; this is fine for most apps but requires discipline
- **Smaller ecosystem** than Next.js for component libraries, CMS integrations, etc.
- **Remix 3 confusion** — the brand split is causing real confusion; make sure your team understands the React Router v7 vs. Remix 3 distinction
- **Fewer batteries than Next.js** — image optimization, font optimization, etc. require third-party solutions

## Support Policy

React Router v7 follows semantic versioning; minor releases are backward-compatible. Shopify maintains the project with active investment. No formal LTS policy, but stability is a core value.
