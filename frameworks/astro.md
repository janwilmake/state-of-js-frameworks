# Astro

> Maintained by the Astro core team (now part of Cloudflare since January 2026). The content-first framework that ships zero JavaScript by default. Ideal for marketing sites, docs, blogs, and content-heavy applications.

## Latest Version

**7.0.6** (July 2, 2026) — 🚀 **Current stable** — Astro 7 is now production-ready  
**7.0.0** (June 22, 2026) — Initial Astro 7 stable release  
**6.4.8** (June 17, 2026) — Final Astro 6.x stable (legacy; use Astro 7 for new projects)  
**Node.js 22+** required  
Backed by **Cloudflare** (acquired January 16, 2026)  
**~3.1M weekly npm downloads** (July 2026)

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

## v6.4.7 Patch (June 15, 2026)

- **i18n locale URL trailing-slash fix** — `getRelativeLocaleUrl`, `getAbsoluteLocaleUrl`, and `getAbsoluteLocaleUrlList` now correctly strip trailing slashes when `trailingSlash: 'never'` is configured
- **Double URL-encoded paths no longer 400** — on-demand routes correctly handle double-encoded characters (e.g., `%255B`) instead of rejecting with `400 Bad Request`; middleware now runs before rejection
- **Shadow DOM named slot fix** — JSX runtime no longer strips `slot` attribute from output, fixing named slot distribution in web components
- **Stale inline CSS fix** — editing CSS files in dev no longer leaves old styles in server-rendered `<style>` tags (FOUC fix)
- Wrangler config now includes JSON schema when running `astro add cloudflare`

## v6.4.5–6.4.6 Patches (June 9–10, 2026)

**6.4.6** (June 10, 2026):
- **Image dev-server rename fix** — renaming an image file while dev server is running no longer triggers a build error; Astro now correctly hot-reloads the image
- **`addAttribute` hardening** — drops attribute names containing invalid HTML spec characters (`"`, `'`, `>`, `/`, `=`, whitespace) to prevent attribute injection
- **`allowedDomains` origin validation** — validates request origin against `allowedDomains` before fetching prerendered error pages; falls back to `localhost` when no match

**6.4.5** (June 9, 2026):
- **`Astro.request.url` aligned with `Astro.url`** — previously `Astro.url` was updated with the forwarded origin while `Astro.request.url` retained the socket-derived URL, causing divergence behind TLS-terminating proxies; now both are consistent
- **Cloudflare build-time regression revert** — reverts a change to `isNode` runtime detection that caused a significant build time regression for Cloudflare adapter users with large prerendered sites

## v6.4.4 Patches (June 3, 2026)

- **`App.match()` percent-sequence fix** — no longer throws on request paths containing an invalid percent-encoded sequence
- **Client island HMR fix** — editing a `client:idle`/`client:load` component no longer causes a full backend program reload in dev
- **`getStaticPaths` `.html` suffix fix** — endpoints using `getStaticPaths` with `.html` in dynamic param values no longer fail with `NoMatchingStaticPathFound`
- **Domain i18n SSR fix** — `Astro.currentLocale` now correctly returns the domain's locale (not the default) on dynamic routes served from a mapped domain
- **`Astro.routePattern` casing fix** — route patterns now preserve original casing of dynamic parameter names (e.g., `[postId]` no longer lowercased to `[postid]`)

## v6.4.3 Patches (June 2, 2026)

- `devalue` dependency bumped to v5.8.1
- Dev toolbar accessibility audit fix for anchors inside closed `<details>` elements
- Additional minor bug fixes

## v6.4.0 Highlights (May 28, 2026) 🚀 New Minor

- **New `markdown.processor` API** — swap out the entire Markdown pipeline via config; default remains `unified()` so existing projects work without changes; existing top-level `markdown.remarkPlugins`, `markdown.rehypePlugins`, etc. still work but are now **deprecated** (will be removed in Astro 8.0); they are now configured directly on the processor
  ```js
  // astro.config.mjs
  import { unified } from '@astrojs/markdown-remark';
  import remarkToc from 'remark-toc';
  export default defineConfig({
    markdown: {
      processor: unified({ remarkPlugins: [remarkToc] }),
    },
  });
  ```
- **Sätteri — Rust-based Markdown processor** — new package providing a Markdown/MDX pipeline written in Rust; Astro's own testing showed **over 1 minute shaved off build times** for the Astro and Cloudflare docs sites; does **not** run remark/rehype plugins — if you rely on unified plugins, stay on `unified()` for now or port them to Sätteri's MDAST/HAST plugin system; **the Astro team has signaled Sätteri is the intended default in a future major release**
- **Cloudflare routing helpers** — `@astrojs/cloudflare` ships a `cloudflare()` helper for advanced routing: handles SESSION KV binding injection, static asset serving via ASSETS binding, prerendered error pages, and client address from `CF-Connecting-IP`; works with custom fetch handlers and Hono middleware
- **`@astrojs/mdx` 6.0** — major version of the MDX integration updated alongside Astro 6.4; includes Sätteri integration (`@astrojs/mdx@6.0.2` updates Sätteri to v0.8.0)

## v6.3.6–6.3.7 Patches (May 20–21, 2026)

**6.3.7** (May 21, 2026):
- Routine bug fixes and dependency bumps following the 6.3.6 patch cluster

**6.3.6** (May 20, 2026):
- Bug fixes and stability improvements; no breaking changes

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
  - **Astro 7 advanced to beta** — `7.0.0-beta.3` released June 9, 2026; `7.0.0-beta.4` released June 18, 2026 (via `npm install astro@beta`); not production ready but more stable than alpha

## Astro 7.0 Stable (June 22, 2026) 🚀

Astro 7 is production-ready as of June 22, 2026. **The headline: 15–61% faster builds.** This is the biggest performance release in Astro's history, powered by three concurrent improvements: Rust compiler, Rust Markdown pipeline (Sätteri), and Vite 8 + Rolldown.

**Full release highlights:**
- **Vite 8 upgrade** — Vite 8 ships [Rolldown](https://rolldown.rs/) (Rust-based bundler replacing both esbuild and Rollup); 10–30× faster than Rollup in benchmarks; auto-converts existing `esbuild`/`rollupOptions` config via compatibility layer; most Vite plugins continue to work
- **Rust `.astro` compiler** — the Go-based compiler is removed; the Rust compiler (`@astrojs/compiler-rs`) is now the default and only option; **strict HTML parsing** — unclosed tags now throw errors instead of being silently fixed; remove `experimental.rustCompiler: true` flag if present
- **Sätteri Markdown processor** (default for `.md`) — Rust-based pipeline replaces unified/remark/rehype as the default; **build times cut by over 1 minute** on large docs sites; if you rely on remark plugins, opt back in explicitly:
  ```js
  import { unified } from '@astrojs/markdown-remark';
  export default defineConfig({ markdown: { processor: unified() } });
  ```
- **Advanced Routing (stable)** — `src/fetch.ts` entrypoint with full control over Astro's request pipeline; compose handlers, use Hono/other frameworks, proxy paths to external services; API follows Cloudflare Workers `fetch` handler pattern
- **Route Caching (stable)** — platform-agnostic caching API (`Astro.cache.set()`) with built-in `memoryCache()` provider; CDN cache providers for Netlify, Vercel, and Cloudflare ship alongside Astro 7
- **Agent-aware dev server** — detects coding agents, runs dev server in background, outputs structured JSON logs for machine-readable feedback; integrates with Claude Code, Cursor, Codex
- **Queued rendering** — new rendering strategy more effectively parallelizes render sections; meaningfully faster for large pages with many static sections

**Breaking changes from Astro 6:**
- **Rust compiler replaces Go compiler** — stricter HTML parsing; unclosed tags are errors; semantically invalid HTML is no longer corrected
- **Sätteri is the default Markdown processor** — if you use `markdown.remarkPlugins` / `markdown.rehypePlugins`, you must explicitly configure `unified()` as your processor
- **Vite 8 / Rolldown** — integrations using Vite internal APIs may need updates; project-level code largely unaffected

```bash
# Upgrade to Astro 7
npx @astrojs/upgrade   # recommended (handles most changes)
npm install astro@latest  # → 7.0.6
```

**v7.0.6** (July 2, 2026) — latest patch:
- Fix: missing CSS for virtual style modules (e.g., responsive image layout styles) in dev mode when JavaScript is disabled
- Fix: `security.checkOrigin` now applied consistently to Astro Actions and on-demand endpoints regardless of pipeline composition
- Fix: `<Picture inferSize>` no longer fails on rate-limited remote image servers (dimensions resolved once per render)
- Fix: `<script>` inside `Astro.slots.render()` no longer hoisted out of position
- Fix: attribute rendering hardened for custom elements

---

## v7.0.0-beta.4 (June 18, 2026) — Sätteri Becomes the Default

- **Sätteri is now the default Markdown processor in Astro 7** — the Rust-based `@astrojs/markdown-satteri` package replaces the unified (remark/rehype) pipeline as the default for `.md` files; significantly faster builds (Astro's own docs site saw over 1 minute shaved off); does **not** support remark/rehype plugins directly
- **Switching back to remark/rehype** — install `@astrojs/markdown-remark` and explicitly set it as your processor in `astro.config.mjs` if you rely on remark plugins; the old top-level `markdown.remarkPlugins`, `markdown.rehypePlugins` options still function but require the remark processor to be active
- **`allowedDomains` header validation fix** — spurious `Astro.request.headers` warning on prerendered pages when `security.allowedDomains` is configured now suppressed correctly (the `allowedDomains` check skips prerendered routes since they use synthetic requests)
- `npm install astro@beta` → **7.0.0-beta.4**

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

~3.1M weekly downloads (June 2026) — growing significantly faster than most frameworks in this cohort; up from ~1.33M in March 2026. Downloads understate adoption because Astro users often build static sites that don't need frequent deploys. GitHub stars: ~59K and growing. The Cloudflare acquisition and continued major releases signal long-term viability.

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
