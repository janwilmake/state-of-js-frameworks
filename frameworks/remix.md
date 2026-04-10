# Remix / React Router

> Maintained by Shopify. The framework that bet on web standards — and won. In 2024, Remix merged into React Router v7. Remix 3 is now a separate, pre-React project in active development.

## Current State (April 2026)

**Remix as a standalone React framework no longer exists.** The key facts:

- **React Router v7** (released November 2024) absorbed all of Remix v2's patterns — loaders, actions, nested routing, server rendering. This is the production-ready successor to Remix v2.
- **Remix 3** is a completely separate new framework, forking Preact (not React). It is under active development and has **no migration path from Remix v2**. If you're in the React ecosystem, Remix 3 is not for you — yet.

For teams evaluating "Remix", the practical question is: **React Router v7 in Framework Mode** vs. **Next.js 16**.

## React Router v7 — Latest Version

**v7.5+ (ongoing, 2026)** — stable, production-ready  
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
