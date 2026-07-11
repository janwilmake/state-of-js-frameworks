# Remix / React Router

> Maintained by Shopify. The framework that bet on web standards — and won. In 2024, Remix merged into React Router v7. React Router v8 shipped June 17, 2026. Remix 3 is now a separate, pre-React project in active development.

## Current State (June 2026)

**Remix as a standalone React framework no longer exists.** The key facts:

- **React Router v8** (released June 17, 2026) is the current stable major, succeeding React Router v7. ESM-only, Node 22.22+, Vite 7+ required. The most boring major release ever — future flags smoothed the transition.
- **React Router v7** (released November 2024) is now in security-update support only. Teams on v7 should upgrade to v8.
- **React Router v6 and Remix v2 are now officially EOL** — no further security updates. Migrate to v7 or v8 now.
- **Remix 3** is a completely separate new framework, forking Preact (not React). It is under active development and has **no migration path from Remix v2**. If you're in the React ecosystem, Remix 3 is not for you — yet.

For teams evaluating "Remix", the practical question is: **React Router v8 in Framework Mode** vs. **Next.js 16**.

## React Router — Latest Version

**v8.2.0** (July 8, 2026) — **Current stable** 🚀 Latest minor  
**v8.1.0** (June 29, 2026) — Agent Skills in `create-react-router`, Observability Metadata  
**v8.0.1** (June 18, 2026) — `AppLoadContext` type removed; `react-router-dom` fully removed  
**v8.0.0** (June 17, 2026) — Initial v8 stable  
**v7.18.1** (June 2026) — Security/bug fix patch on v7 LTS line  
**v7.18.0** (June 16, 2026) — Final v7 minor (security updates only)  
28M+ weekly npm downloads (react-router package)  
Backed by **Shopify** (powers Hydrogen, Admin)  
**Yearly major release cadence** — v9 expected around May 2027 (aligned with Node 22 EOL)

## Key Features (React Router v8 Framework Mode)

- **Loaders** — async server-side data fetching per route; co-located with components
- **Actions** — server-side mutations; forms work without JavaScript (progressive enhancement)
- **Nested routing** — fine-grained layouts and data loading trees
- **SSR-first** — everything server-renders by default; CSR is opt-in
- **Web Standards** — built on `Request`/`Response`, `FormData`, and `URL` APIs
- **File-based routing** — routes directory with loader/action co-location
- **Streaming** — built-in support via `defer()` and `<Await>`
- **Type safety** — generated types for `params`, `loaderData`, and `actionData`
- **Vite 7+ required** (v8) — ESM-first, aligns with the broader ecosystem
- **TypeScript 6 support** — peer dep range includes TypeScript 6
- **Unstable RSC Framework Mode** — React Server Components support in active development; not yet production-ready in v8.0 but expected to stabilize in an early v8.x minor
- **Zero vendor lock-in** — deploy to any Node.js, edge, or serverless environment
- **ESM-only** (v8) — CJS builds dropped; Node 22.22+ / Vite 7+ enables this cleanly

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

## React Router — Recent Releases

| Version | Date | Highlights |
|---|---|---|
| **v8.2.0** | **July 8, 2026** | 🚀 **Current stable** — Web Streams default server entry for non-Node Framework mode apps (non-Node runtimes now use `renderToReadableStream` without needing a custom `entry.server.tsx`); Node apps can opt in via `future.unstable_enableNodeReadableStream`; `nub` package manager detection |
| **v8.1.0** | **June 29, 2026** | **Agent Skills** — `create-react-router` now scaffolds the React Router Agent Skill by default (prompt in interactive mode; `--no-agent-skills` to skip); **Observability Metadata** — new structured metadata on route responses for observability/tracing tools; several prerendering plugin bug fixes; Bun runtime `typegen` fix; Vite 8.1+ deprecation warning resolved |
| **v8.0.1** | **June 18, 2026** | Removes obsolete `AppLoadContext` type export left over from v7; `react-router-dom` package fully removed (import from `react-router` or `react-router/dom` instead) |
| **v8.0.0** | **June 17, 2026** | Initial v8 stable — ESM-only, Node 22.22+, React 19.2.7+, Vite 7+; yearly cadence; all `future.v8_*` flags now defaults; `tsdown` replaces `tsup` in build pipeline; v6 and Remix v2 officially EOL; `hasErrorBoundary` removed from route objects; `meta.data` removed (use `loaderData`) |
| **Remix 3 beta.4** | **June 5, 2026** | 🔬 **Remix 3 beta** (not production ready) — Breaking: middleware must now explicitly `next()` or return a `Response`; `createMiddleware()` helper for reusable chains; `remix/test` gains timeout + abort signal support; `MapTarget`/`MapHandler` removed from public types (use `Router`, `RouteBuilder`, `Action`, `Controller` instead) |
| v7.18.0 | June 16, 2026 | Final v7 stable (security updates only going forward) |
| v7.17.0 | June 4, 2026 | **Bundled docs for AI agents** — official Markdown docs now shipped inside `node_modules/react-router/docs`; AI coding agents can read docs locally without network |
| v7.16.0 | May 28, 2026 | Stabilize `future.v8_trailingSlashAwareDataRequests`; future flag warnings for v8 flags |
| v7.15.1 | May 14, 2026 | `unstable_useRouterState()` hook — consolidated active + pending router state access |
| v7.15.0 | May 5, 2026 | **API stabilizations pre-v8**; 15–30% server-side route matching perf improvement |
| v7.14.1 | April 13, 2026 | TypeScript 6 peer dep support, race condition fix in `HydrateFallback` |
| v7.14.0 | April 2, 2026 | **Vite 8 support**, memory leak fix in `turbo-stream`, RSC Framework Mode improvements |
| v7.13.0 | January 23, 2026 | `crossOrigin` prop on `<Links>`, origin check returns 400 |
| v7.12.0 | January 7, 2026 | 🔒 Security: CSRF protection, XSS fixes; `allowedActionOrigins` config |

## React Router v8 — What Changed

React Router v8 shipped June 17, 2026. It was deliberately boring — that's the point. If you've enabled all `future.v8_*` flags in your v7 project, the API surface is already v8.

**Baseline changes:**
- **ESM only** — CJS builds dropped; requires Node 22.22+ (or Bun); Vite 7+ required
- **Node 22.22+ minimum** — Node 20 (EOL April 2026) dropped; v8 aligns Node support with Active LTS + latest Maintenance LTS branch only
- **React 19.2.7+ required**
- **Vite 7+ required** — Vite 6 dropped (Vite 8 is current; Vite 7 remains the minimum)
- **ES2022 tsconfig target** — tsconfig `target`/`lib` fields updated across all packages

**Breaking API changes (v8.0.0–v8.0.1):**
- **`react-router-dom` package removed** — the v7 compatibility shim is gone; migrate imports: `RouterProvider`/`HydratedRouter` → import from `react-router/dom`; everything else → import from `react-router`
- **`AppLoadContext` type removed** (v8.0.1) — obsolete export from before middleware was always-enabled; use `RouterContextProvider` server context instead
- **`hasErrorBoundary` removed from route objects** — no longer accepted on `RouteObject`, `DataRouteObject`, `<Route>` JSX props, or `lazy` definitions; the router infers error boundary presence automatically
- **`meta.data` removed** — deprecated `data` field on `MetaArgs` removed; use `loaderData` on `MetaArgs` and each `MetaArgs.matches` item instead
- **All `future.v8_*` flags removed** — they are now defaults; remove them from your `react-router.config.ts`

**Going forward:**
- **Yearly major release cadence** — v9 expected ~May 2027, aligned with Node 22 EOL
- **RSC Framework Mode** — not yet stable in v8.0 but on track to stabilize in an early v8.x minor
- **React Router v7 continues security updates** (just like v6 did after v7 shipped)
- **React Router v6 and Remix v2 are now EOL** — no further security patches

**Upgrade from v7:**
```bash
# Enable all future flags in v7 first (if not done already)
# Then:
npm install react-router@8
# Remove all future.v8_* flags from your react-router.config.ts (they're now defaults)
```

---

## Remix 3 (Beta — Not Production Ready)

Remix 3 is at **beta.4** (June 5, 2026). Key points:
- **No React dependency** — built on Preact; components use web-native `EventTarget` patterns instead of React hooks
- **No migration path** from Remix v2 or React Router v7 — this is a net-new framework
- **Full-stack batteries-included** — routes, request handlers, middleware, sessions, auth, forms, uploads, assets, data/database management, UI components, theming, networking, tests — **one dependency**
- **"Unbundling"** — the runtime is the source of truth; no pre-runtime bundle analysis step; works naturally with AI coding agents because routes, controllers, middleware, tables, forms, and frames all have clear, predictable shapes
- **Native DOM mixins** — Remix provides DOM mixins instead of a React-like reconciler; works seamlessly with web components and third-party libraries
- **New brand & website** (May 6, 2026) — remix.run rebuilt on Remix 3 alpha itself, dropping React entirely for the production site; uses Three.js + GLSL shaders
- **Backed by Shopify** — well-funded; beta signals serious intent
- `npx remix@next new` to scaffold a Remix 3 project (beta)

**Recommendation:** Do not adopt Remix 3 for production until stable. Teams on Remix v2 should migrate to **React Router v7**, not Remix 3. Monitor [remix.run/blog](https://remix.run/blog) for stability updates.

## npm Download Trend

React Router (the package) has ~28M weekly downloads — more than Next.js — because it is used both as a standalone client router and as a full-stack framework. The framework mode (Remix-style) is a subset of this figure. Remix v2 downloads are declining as teams migrate to React Router v7.

## Trade-Off Assessment

**Choose React Router v8 when:**
- Web standards compliance and progressive enhancement matter (government, accessibility-critical apps)
- You want zero vendor lock-in and true deploy-anywhere portability
- Your team finds the Server Components mental model in Next.js too complex
- You're building content-heavy SSR apps with clear data/mutation boundaries
- You're already using TanStack ecosystem (excellent interop)
- You want a predictable yearly major release cadence

**Watch out for:**
- **No ISR/PPR** — cache-busting is your responsibility; this is fine for most apps but requires discipline
- **Smaller ecosystem** than Next.js for component libraries, CMS integrations, etc.
- **Remix 3 confusion** — the brand split is causing real confusion; React Router v8 = React ecosystem framework; Remix 3 = Preact-based experiment; make sure your team knows the difference
- **Fewer batteries than Next.js** — image optimization, font optimization, etc. require third-party solutions
- **ESM-only** in v8 — if you have legacy CJS infrastructure, test the Node 22.22+ `require(esm)` path before upgrading

## Support Policy

React Router v7 follows semantic versioning; minor releases are backward-compatible. Shopify maintains the project with active investment. No formal LTS policy, but stability is a core value.
