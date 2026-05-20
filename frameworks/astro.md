# Astro

> Maintained by the Astro core team (now part of Cloudflare since January 2026). The content-first framework that ships zero JavaScript by default. Ideal for marketing sites, docs, blogs, and content-heavy applications.

## Latest Version

**6.3.5** (May 18, 2026) — Current stable (latest patch)  
**6.3.3** (May 14, 2026) — ⚠️ Security fix (XSS in island slot names — upgrade to 6.3.5)  
**6.3.0** (May 7, 2026) — Latest minor release  
**7.0.0-alpha.0** (April 30, 2026) — Pre-release preview (not production ready)  
**Node.js 22+** required (breaking change from Astro 6)  
Backed by **Cloudflare** (acquired January 16, 2026)  
**~2.73M weekly npm downloads** (May 2026)

## Key Features

- **Zero JS by default** — pages are static HTML unless you opt in to interactivity
- **Islands architecture** — interactive components (React, Vue, Svelte, Solid, Preact) hydrate independently; the rest of the page is static
- **Content Collections** — type-safe content management with Zod validation
- **Live Content Collections** (stable in 6.0) — real-time data from external APIs via the unified content layer
- **Redesigned `astro dev`** (new in 6.0) — dev server rebuilt on Vite's Environment API; runs the exact production runtime in development (no more "works in dev, breaks in prod")
- **First-class Cloudflare Workers support** (new in 6.0) — uses Cloudflare's Vite plugin; test Cloudflare Workers APIs locally in dev
- **Built-in Fonts API** (new in 6.0) — zero-config font loading and optimization
- **Content Security Policy (CSP)** (stable in 6.0) — first meta-framework with built-in CSP; auto-hashes scripts/styles and generates correct headers
- **Experimental Rust compiler** (new in 6.0) — successor to the Go-based `.astro` compiler; already shows significant performance gains
- **Experimental Queued Rendering** — render pages in a controlled queue for large static builds
- **Experimental Route Caching** — cache route data across builds
- **Experimental custom logger** (new in 6.2) — structured JSON logging for AI coding agents and CI pipelines
- **SVG optimizer API** (new in 6.2) — first-class SVG optimization with configurable Svgo integration
- **`getFontFileURL()` helper** (experimental, new in 6.2) — resolve font file URLs from `fontData`; useful for Open Graph image generation with Satori
- **`server.allowedHosts` for preview servers** (new in 6.2) — prevents DNS rebinding attacks when previewing Cloudflare builds locally
- **Starlight** — official documentation site framework built on Astro
- **Framework-agnostic** — use React, Vue, Svelte, Solid, Preact, or plain HTML in the same project

## Rendering Modes

| Mode | Description |
|---|---|
| SSG | Static generation at build time (default for most pages) |
| SSR | Per-request server rendering via `output: 'server'` |
| Hybrid | Mix static and server-rendered pages via `export const prerender = false` |
| Islands | Static page with interactive component islands hydrating client-side |
| Edge SSR | Deploy SSR to Cloudflare Workers, Vercel Edge, Netlify Edge |

Astro's hybrid mode is a first-class feature: you define `prerender = true/false` per page. This makes it excellent for sites that are mostly static with a few dynamic pages.

## Deployment Targets

- **Cloudflare Workers / Pages** — `@astrojs/cloudflare`; first-class support; reference implementation for Cloudflare edge
- **Vercel** — `@astrojs/vercel`
- **Netlify** — `@astrojs/netlify`
- **Node.js** — `@astrojs/node`
- **Deno** — `@astrojs/deno`
- **Static** — default; output HTML to any CDN/S3

## v6.3.3–6.3.5 Patches (May 14–18, 2026)

**6.3.5** (May 18, 2026):
- **CSP fix** — `position` prop on `<Image>` / `<Picture>` was incorrectly invalidating CSP hashes; now correctly excluded from hash computation
- **Improved error messages** — more consistent and correct wording across build/runtime errors
- **Stale SSR content fix** — dev server now properly invalidates the SSR module runner cache when SSR-only modules change (e.g., `.astro` files in a monorepo outside the project root); previously returned stale content after edits

**6.3.4** (May 18, 2026):
- **`experimental.advancedRouting` — `fetchFile` option** — customize the app entry file path or disable generation entirely with `fetchFile: false`
- **`FetchState.response` property** — automatically set after `pages()` or `middleware()` completes for downstream inspection
- **`App.Providers` interface** — type custom context providers on `Astro` and `ctx` objects
- **`Fetchable` type export** — type the advanced routing entrypoint cleanly with `satisfies Fetchable`
- **Hono `cache()` middleware fix** — now follows the standard wrapper pattern correctly

**6.3.3** (May 14, 2026) 🔒 Security:
- **XSS fix** — slot names on hydrated island components were not HTML-escaped in SSR output; a dynamically named slot could cause reflected XSS; upgrade immediately if using SSR with Islands

## v6.3 Highlights (May 7, 2026)

- **Experimental Advanced Routing** — full control over the request pipeline via a `FetchState`-based app entry point (`src/app.ts`); compose individual handlers, bring your own framework (e.g., Hono), proxy specific paths to external services and let Astro handle the rest; follows the `fetch` handler pattern used by Cloudflare Workers, Deno, Bun, and Hono
- **Support redirects on external image URLs** — Astro now correctly follows redirects when processing external image URLs; previously external images returning 3xx would fail silently
- **SVG image processing disabled by default** — SVG images are no longer processed through the image pipeline by default; opt in explicitly with `image.svg: true` to avoid unintended transformations of SVG files
- **`consume()` method on `AstroCookies`** — new instance method marks cookies as consumed and returns `Set-Cookie` header values; replaces the now-deprecated `AstroCookies.consume(cookies)` static method
- **6.3.2 patch** (May 13) — rejects double-encoded URL paths with 400 instead of silently partial-decoding; fixes `&` showing as raw entity in `<meta>` tags in link previews; fixes `assetsPrefix` not available on `astro:config/server` build event
- **6.3.3 patch** (May 14) — minor bug fixes

## v6.2 Highlights (April 30, 2026)

- **SVG optimizer** — `experimental.svgOptimizer` passes `.astro` SVG imports through configurable Svgo optimization
- **Experimental Logger** — structured JSON logging via `experimental.logger`; integrates cleanly with AI agents and log aggregation pipelines
- **Experimental `getFontFileURL()`** — exported from `astro:assets`; resolves font file URLs from font data objects for use with Satori Open Graph image generation
- **`allowedHosts` for preview servers** — `server.allowedHosts` is now forwarded to adapter preview servers; prevents DNS rebinding attacks; important for `@astrojs/cloudflare` users
- **`"jsx"` option for `compressHTML`** — strips whitespace using JSX rules for consistent behavior across `.astro` and `.tsx` files
- **Astro 7 alpha launched** — `astro@7.0.0-alpha.0` released same day as 6.2:
  - **Vite 8 upgrade** — breaking for integrations depending on Vite internals; most user code unaffected
  - **Rust compiler is now the default and only compiler** — Go compiler removed; `experimental.rustCompiler` flag no longer needed; significantly faster build times
  - Install with `npm install astro@alpha` to test

## v6.0 Breaking Changes (March 10, 2026)

- **Node.js 22+ required** — drop Node 18/20 support
- **`Astro.glob()` removed** — use Content Collections or `import.meta.glob()` directly
- **Cloudflare adapter breaking changes** — `Astro.locals.runtime` removed; use platform APIs directly
- **Zod 4 upgrade** — Content Collections now use Zod v4; schemas may need updates
- **Several deprecated APIs removed** — see the [v6 upgrade guide](https://v6.docs.astro.build/en/guides/upgrade-to/v6/)

## Cloudflare Acquisition (January 2026)

On January 16, 2026, the Astro Technology Company team joined Cloudflare. Key implications:
- Framework remains **MIT-licensed and open-source**; deployable to all platforms
- Netlify, Vercel, and all other platforms continue to be supported
- **`workerd` integration** in Astro 6 is the first major output of this partnership
- Cloudflare's **Astro Ecosystem Fund** (backed by Webflow, Netlify, Wix, Sentry, Stainless) continues
- Astro will become the **reference implementation for content-driven sites on Cloudflare's edge**
- Development funding significantly increased — sustainability was the main concern for the indie framework

## npm Download Trend

~2.73M weekly downloads (May 2026) — growing significantly faster than most frameworks in this cohort; up from ~1.33M in March 2026. Downloads understate adoption because Astro users often build static sites that don't need frequent deploys. GitHub stars: ~59K and growing. The Cloudflare acquisition and continued major releases signal long-term viability.

## Trade-Off Assessment

**Choose Astro when:**
- You're building a content-driven site (marketing, docs, blog, portfolio)
- Core Web Vitals and Lighthouse scores are critical (zero-JS default is a huge advantage)
- You need to use multiple UI frameworks in the same project (migration, islands)
- You want the best Cloudflare Workers developer experience
- SEO-first sites where fast TTFB and small payloads are paramount

**Watch out for:**
- **Not suited for highly interactive apps** — SPAs, dashboards, real-time apps are better served by SvelteKit, Next.js, or React Router
- **Islands architecture has a coordination cost** — sharing state across islands requires a store (nanostores, etc.)
- **Breaking changes in major versions** — Astro 6 had a long breaking-change list (Node 22 requirement, Zod 4, removed APIs)
- **Cloudflare alignment** — while all platforms are supported, the long-term roadmap clearly favors Cloudflare Workers; factor this into your platform decision
- **Server-side apps need a mindset shift** — the static-first default requires explicit opt-ins for dynamic behavior

## Support Policy

Astro follows semantic versioning. No formal LTS policy. Major versions are well-spaced (5.x → 6.0 was ~12 months). The framework has a comprehensive upgrade CLI (`@astrojs/upgrade`) that handles most migrations automatically.
