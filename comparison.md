# Framework Comparison Matrix

> Last updated: May 18, 2026. Covers Next.js 16.2.6, React Router v7.15.1 / Remix 3 beta (Remix), Nuxt 4.4.5, SvelteKit 2.59.1, Astro 6.3.3, Angular 21.2.13 (v22 RC.0 released May 13 — stable week of June 1, 2026; Angular 19 EOL May 19 has now passed; Angular 21 now in LTS).

## Quick Decision Guide

| If you need… | Use |
|---|---|
| Largest React ecosystem + all rendering modes | **Next.js** |
| SSR + web standards + zero vendor lock-in | **React Router v7** |
| Vue + elegant hybrid rendering | **Nuxt** |
| Best DX + smallest bundles + compiler magic | **SvelteKit** |
| Content sites + zero JS by default | **Astro** |
| Enterprise scale + TypeScript-first + Google backing | **Angular** |

---

## Feature Matrix

| Feature | Next.js 16.2.6 | React Router v7.15.1 | Nuxt 4.4.5 | SvelteKit 2.59.1 | Astro 6.3.3 | Angular 21.2.13 |
|---|---|---|---|---|---|---|
| **Language** | JS/TS | JS/TS | JS/TS | JS/TS | JS/TS | **TypeScript only** |
| **UI Library** | React 19 | React 19 | Vue 3 | Svelte 5 | Any (React/Vue/Svelte/Solid) | Angular |
| **SSR** | ✅ | ✅ | ✅ | ✅ | ✅ (opt-in) | ✅ (Angular Universal) |
| **SSG** | ✅ | ⚠️ (manual cache) | ✅ | ✅ | ✅ (default) | ✅ |
| **ISR** | ✅ | ❌ | ✅ (`routeRules`) | ❌ | ❌ | ❌ |
| **PPR/Streaming** | ✅ (Cache Components, stable) | ✅ (`defer()`) | ⚠️ (partial) | ⚠️ (partial) | ❌ | ❌ |
| **Islands Architecture** | ❌ | ❌ | ❌ | ❌ | ✅ (first-class) | ❌ |
| **File-based Routing** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ (component router) |
| **Server Actions/Mutations** | ✅ (Server Actions) | ✅ (Actions) | ✅ (server functions) | ✅ (Form Actions) | ✅ (Actions) | ⚠️ (manual) |
| **Progressive Enhancement** | ⚠️ (partial) | ✅ (first-class) | ⚠️ (partial) | ✅ (first-class) | ✅ | ❌ |
| **Edge Deployment** | ✅ | ✅ | ✅ (Nitro) | ✅ (adapters) | ✅ (Cloudflare native) | ⚠️ (limited) |
| **Serverless** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Built-in Image Optimization** | ✅ | ❌ | ✅ (Nuxt Image) | ❌ | ✅ | ❌ |
| **Built-in Font Optimization** | ✅ | ❌ | ✅ | ❌ | ✅ (v6) | ❌ |
| **TypeScript DX** | ✅ | ✅ | ✅ | ✅ (excellent) | ✅ | ✅✅ (mandatory) |
| **AI/MCP Tooling** | ✅ (AGENTS.md, DevTools) | ❌ | ✅ (Nuxt Agent + MCP) | ✅ (Svelte MCP) | ✅ (Experimental Logger) | ✅ (Angular MCP) |
| **Built-in UI Library** | ❌ | ❌ | ✅ (Nuxt UI v4) | ❌ | ❌ | ✅ (Angular Material) |
| **Dependency Injection** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ (built-in DI) |
| **Built-in Forms** | ❌ (Server Actions) | ✅ (Actions) | ❌ | ✅ (Form Actions) | ✅ (Actions) | ✅ (Reactive + Signal Forms) |
| **Built-in HTTP Client** | ❌ (fetch) | ❌ (fetch) | ✅ (`$fetch`) | ❌ (fetch) | ❌ (fetch) | ✅ (`HttpClient`) |
| **Testing Framework** | Jest/Vitest | Vitest | Vitest | Vitest | Vitest | Karma→Vitest + TestBed |

---

## Rendering Strategy Comparison

| Framework | Default Mode | ISR | PPR | Streaming | Edge |
|---|---|---|---|---|---|
| **Next.js** | SSR (App Router) | ✅ | ✅ (Cache Components) | ✅ | ✅ |
| **React Router v7** | SSR | ❌ | ❌ | ✅ (`defer`) | ✅ |
| **Nuxt** | SSR | ✅ (`routeRules`) | ❌ | ⚠️ | ✅ |
| **SvelteKit** | SSR | ❌ | ❌ | ⚠️ | ✅ |
| **Astro** | SSG | ❌ | ❌ | ❌ | ✅ |
| **Angular** | SPA | ❌ | ❌ | ❌ | ⚠️ |

**Winner for rendering flexibility:** Next.js  
**Winner for simplicity:** Astro (SSG default) or React Router (clear SSR mental model)  
**Winner for hybrid per-route control:** Nuxt (`routeRules`)

---

## Bundle Size Comparison

Approximate JavaScript delivered to the browser for a minimal "Hello World" application:

| Framework | Min Bundle (gzipped) | Notes |
|---|---|---|
| **Astro** | ~0 KB | Static HTML, no JS unless islands used |
| **SvelteKit** | ~20–40 KB | Compiler eliminates runtime overhead |
| **React Router v7** | ~45–60 KB | React 19 runtime + router |
| **Next.js** | ~80–120 KB | React 19 + Next.js client runtime |
| **Nuxt** | ~60–90 KB | Vue 3 runtime + Nuxt client runtime |
| **Angular** | ~80–100 KB | Angular runtime (Signals helps, but baseline is large) |

> **Important caveat:** These numbers matter most for content sites and initial page loads. For complex applications, the delta shrinks as your own code dominates bundle size. React and Angular's ecosystems often add more third-party JS, widening the gap again.

---

## Learning Curve

| Framework | Initial Setup | Core Concepts | Mastery |
|---|---|---|---|
| **Astro** | ⭐ Easy | ⭐⭐ Moderate (Islands model) | ⭐⭐ Moderate |
| **SvelteKit** | ⭐ Easy | ⭐ Easy (Runes are intuitive) | ⭐⭐ Moderate |
| **React Router v7** | ⭐⭐ Moderate | ⭐⭐ Moderate (loaders/actions) | ⭐⭐ Moderate |
| **Nuxt** | ⭐⭐ Moderate | ⭐⭐ Moderate (auto-imports magic) | ⭐⭐⭐ Hard |
| **Next.js** | ⭐⭐ Moderate | ⭐⭐⭐ Hard (RSC mental model) | ⭐⭐⭐ Hard |
| **Angular** | ⭐⭐⭐ Hard | ⭐⭐⭐ Hard (DI, RxJS, Signals) | ⭐⭐⭐⭐ Very Hard |

---

## Ecosystem & Community (April 2026)

| Metric | Next.js | React Router | Nuxt | SvelteKit | Astro | Angular |
|---|---|---|---|---|---|---|
| **npm weekly downloads** | ~26M | ~28M (react-router) | ~2M | ~1.5–2M | ~2.73M | ~2.5M |
| **GitHub Stars** | ~138K | ~54K (RR) | ~60K | ~21K (kit) | ~57K | ~100K |
| **Stack Overflow questions** | Very High | High | Medium | Medium | Medium | Very High |
| **Job postings** | ⭐⭐⭐⭐ Very High | ⭐⭐⭐ High | ⭐⭐ Medium | ⭐⭐ Medium | ⭐ Low | ⭐⭐⭐⭐ Very High |
| **Component library ecosystem** | ⭐⭐⭐⭐ Excellent | ⭐⭐⭐ Good | ⭐⭐⭐ Good (Nuxt UI v4) | ⭐⭐ Growing | ⭐⭐ Limited | ⭐⭐⭐ Good (Material) |
| **CMS integrations** | ⭐⭐⭐⭐ Excellent | ⭐⭐ Limited | ⭐⭐⭐ Good | ⭐⭐ Limited | ⭐⭐⭐ Good | ⭐⭐ Limited |

---

## Corporate Backing & Long-Term Viability

| Framework | Backed By | Open Source License | Concern Level |
|---|---|---|---|
| **Next.js** | Vercel | MIT | ⚠️ Vendor alignment (Vercel-optimized features) |
| **React Router v7** | Shopify | MIT | ✅ Low — web standards focus, Shopify committed |
| **Nuxt** | NuxtLabs/Vercel | MIT | ⚠️ Vercel acquisition (July 2025) — independence uncertain |
| **SvelteKit** | Vercel (Rich Harris) | MIT | ⚠️ Key contributor at Vercel; community-driven |
| **Astro** | Cloudflare | MIT | ✅ Low — Cloudflare funding, MIT license, strong ecosystem fund |
| **Angular** | Google | MIT | ✅ Low — strategic investment, 6-month release cadence |

> **Pattern to note:** Vercel now has significant influence over Next.js, Nuxt, and SvelteKit. If Vercel platform lock-in is a concern, React Router v7, Astro, or Angular are the most independent options.

---

## Developer Satisfaction (State of JS 2025)

| Framework | Satisfaction | Usage | Awareness |
|---|---|---|---|
| **SvelteKit** | 93% | Growing | High |
| **Astro** | 90% | Growing | High |
| **Next.js** | 74% | Dominant | Universal |
| **React Router** | 72% | Very High | Universal |
| **Nuxt** | 71% | High (Vue ecosystem) | High |
| **Angular** | 58% | Enterprise dominant | Universal |

---

## When to Use Each Framework

### Next.js 16
✅ **Best for:** Complex React applications, full-stack SaaS, e-commerce, teams already invested in React  
❌ **Avoid for:** Simple static sites, teams new to React, projects needing platform independence

### React Router v7 (formerly Remix)
✅ **Best for:** SSR apps prioritizing web standards, accessibility, progressive enhancement, Shopify/Hydrogen  
❌ **Avoid for:** Static sites, complex caching requirements, teams expecting ISR/PPR out of the box

### Nuxt 4
✅ **Best for:** Vue teams, hybrid rendering needs, projects wanting Nuxt UI v4 components  
❌ **Avoid for:** React-only teams, projects needing the largest ecosystem possible

### SvelteKit 2
✅ **Best for:** DX-focused teams, performance-critical sites, small-to-medium projects, MVPs  
❌ **Avoid for:** Large teams requiring a broad hiring pool, projects with heavy React library dependencies

### Astro 6 / Astro 7 (alpha)
✅ **Best for:** Marketing sites, blogs, documentation, content-heavy sites, multi-framework migrations  
❌ **Avoid for:** Highly interactive SPAs, real-time dashboards, complex user applications  
⚡ **Watch:** Astro 6.3 (May 7, 2026) — experimental advanced routing with Hono support; Astro 7 alpha ships Vite 8 + Rust-only compiler; ~2.73M weekly npm downloads and growing fast

### Angular 21 → 22 (June 1, 2026)
✅ **Best for:** Enterprise applications, large teams, TypeScript-first codebases, Google/Firebase ecosystem  
❌ **Avoid for:** Small projects, teams without TypeScript expertise, content sites, performance-first consumer apps  
⚡ **Watch:** Angular 22 (week of June 1, 2026, **14 days away**) — RC.0 released May 13; **Signal Forms going stable** (confirmed), OnPush as default, selectorless components, Zoneless as default for new projects. ⚠️ **Angular 19.x EOL May 19, 2026 has now passed** — teams on v19 are on unsupported software; migrate to Angular 21 (now in LTS) immediately. **Angular 21 active support ended May 19** — LTS until May 2027.
