# Angular

> Maintained by Google. The batteries-included, TypeScript-first enterprise framework that has staged a significant comeback since v16 with the Signals API and a complete DX overhaul.

## Latest Version

**21.2.12** (May 6, 2026) — Current stable patch  
**21.2.0** (February 23, 2026) — Current stable minor  
**21.0.0** (November 19, 2025) — Major release  
**v22.0** — Officially scheduled week of **June 1, 2026** (confirmed per `angular.dev/reference/releases`)  
**22.0.0-next.12** (May 8, 2026) — Latest pre-release canary  
🔴 **Angular 19.x EOL on May 19, 2026** — **3 days away** (today is May 16); no more patches from Google after that date; teams on v19 must upgrade immediately  
⚠️ **Angular 21.x active support ends May 19, 2026** — v21 transitions to LTS (security patches only until May 2027); Angular 22 expected week of June 1, 2026 (16 days away)  
✅ **Signal Forms going STABLE in Angular 22** — confirmed by the Angular team (week of June 1, 2026)

## Key Features

- **Signals API (stable)** — `signal()`, `computed()`, `effect()`, `linkedSignal()`, `toSignal()`; fine-grained reactivity replacing Zone.js; the Angular team's most important architectural shift since v2
- **Signal Forms** (developer preview, v21) — new form API built on Signals; `FormRoot`, `transformedValue`, and more in v21.2; replaces `ReactiveFormsModule` long-term
- **Zoneless change detection** — opt-in in v21; `provideZoneChangeDetection()` deprecated; future default
- **`ChangeDetectionStrategy.Eager`** (new in v21.2) — new strategy for Signals-based components
- **Arrow functions in templates** (new in v21.2) — inline arrow functions directly in component templates
- **Exhaustive `@switch` type-checking** (new in v21.2) — compiler validates `@switch` exhaustiveness
- **Selectorless components** (roadmap, expected v22) — components without `selector` property; used directly in templates
- **Angular MCP Server** (v21) — Model Context Protocol tools for AI-assisted development (Cursor, Claude Code, etc.)
- **Angular Aria package** (developer preview, v21) — accessibility utilities and ARIA management
- **Angular DevTools** — route visualization and Signal graph inspection
- **Standalone components** (stable since v15) — no NgModules required for most use cases
- **`@for` / `@if` / `@switch`** block syntax (stable since v17) — replaces `*ngFor`, `*ngIf`, `*ngSwitch` directives
- **Built-in HTTP client** — `HttpClient` with interceptors, typed responses, and request deduplication
- **Angular CLI (`ng`)** — scaffolding, testing, building, deployment; one of the best CLIs in the ecosystem
- **TypeScript mandatory** — Angular is TypeScript-first; no optional JS mode

## Rendering Modes

| Mode | Description |
|---|---|
| SPA | Default client-side rendering; full Angular application in the browser |
| SSR | Via Angular Universal (built into `@angular/core` since v17); `ng add @angular/ssr` |
| SSG | Static pre-rendering via Angular SSR with `prerender` option |
| Hydration | Non-destructive hydration (stable since v17); replaces full client re-render |

Angular's SSR story has improved dramatically in recent releases but is less mature than Next.js or Nuxt. It is still primarily an SPA framework with SSR added on top.

## Deployment Targets

- **Node.js** — Angular Universal / Angular SSR
- **Static CDN** — `ng build --output-path dist/` → any CDN
- **Docker / self-hosted** — well-supported
- **Vercel, Netlify, AWS** — via Node.js adapters or static output
- **Firebase / Google Cloud** — first-class; Google uses Angular for many products
- **Angular Universal** — custom server (Express, Fastify) for SSR

## v21 Highlights (November 19, 2025)

- **Signal Forms developer preview** — new signal-based form API; `FormRoot`, `FormControl`, `transformedValue`
- **Angular MCP Server** — Cursor and Claude Code integration for AI-assisted Angular development
- **Angular Aria developer preview** — built-in accessibility utilities
- **Signals formatter in DevTools** — custom formatters for inspecting signal values
- **Regular expressions in templates** — `@let isValid = /\d+/.test(val)`
- **CLDR v47 upgrade** — improved currency and date formatting
- **Animation improvements** — enter/leave DOM animations API

## v21.2.12 Patch (May 6, 2026)

- **Signal input transform read-generic fix** — `allow explicit read generic with signal input transforms` for better type inference
- **i18n flags no longer leak on errors** — bug fix for internationalization-related error state propagation
- **`ngSkipHydration` respected in LContainers** — SSR hydration fix for projected nodes inside LContainers
- **Sanitizer typings fix** — improved sanitizer type signatures
- **Signal security** — `validate security-sensitive attributes in i18n bindings` improvement
- **Signal Forms** — `prohibit concurrent submits in signal forms` (prevents double-submit race conditions)
- **22.0.0-next.12** (May 8, 2026) — latest pre-release canary actively in development

## v21.2 Highlights (February 23, 2026)

- **Arrow functions in templates** — inline arrow functions; reduces need for component methods
- **Exhaustive `@switch` type-checking** — compile-time validation of switch completeness
- **`ChangeDetectionStrategy.Eager`** — new change detection strategy optimized for Signals components
- **Signal Forms improvements** — `FormRoot`, `transformedValue`, `submit()` returns `Promise<boolean>`, additional composability APIs
- **Prettier integration in Angular CLI** — new projects now include Prettier as a dev dependency with a `.prettierrc` file; `ng generate` and `ng update` automatically format changed files
- **TypeScript 6 beta support** — peer dependency range updated to include TypeScript 6 pre-releases
- **Resource composition** — `ResourceSnapshot` and resource composition APIs added
- **Location strategy trailing slash** — new location strategy option for trailing slash handling

## v22 Preview (Scheduled Week of June 1, 2026)

Based on the official Angular roadmap (`angular.dev/roadmap`), confirmed team announcements, and community signals:
- **Stable Signal Forms** — **officially confirmed stable** (angular.love / Angular team, May 6, 2026); fine-grained updates for large forms; aligned with Zoneless change detection; replaces `ReactiveFormsModule` as the recommended form API going forward
- **Selectorless components** — define components without a `selector`; use directly in templates; improves refactorability and type safety; reduces cognitive overhead of managing string selectors
- **OnPush as default** — Angular CLI will generate new components with `ChangeDetectionStrategy.OnPush`; RFC discussion open; existing components unaffected
- **Zoneless as default for new projects** — `Zone.js` removed from new project scaffolding; Zoneless was production-ready in v21; existing Zone.js projects continue to work unchanged
- **TypeScript 5.9 support**
- **`debounced()` signal primitive** — native debouncing for signals without bridging to RxJS; simplifies typeahead and search patterns
- **`resource()` improvements** — stronger signal-native async data loading story; reduces `toObservable`/`toSignal` bridging
- **Vitest as primary test runner (stable)** — Vitest graduated to stable in Angular v21; v22 will promote the Karma→Vitest migration tool to stable and make Vitest the default in new projects
- **Angular MCP Server enhancements** — continued investment; Google AI Studio, Gemini CLI, and Antigravity IDE integrations planned
- **`httpResource`** — new HTTP composable built on the Resource API; in "available to experiment with" status
- **Route-level render mode** — configure SSR/pre-render/CSR per individual route (already production-ready; expected as prominent in v22 docs)

## npm Download Trend

~2.5M weekly npm downloads. Angular is the third most downloaded frontend framework after React and Vue. State of JS 2025 satisfaction: **58%** (up from 42% in 2023), reflecting the genuine DX improvement from Signals. Enterprise adoption remains strong: ~45% of Fortune 500 companies use Angular for internal applications.

## Angular's "Renaissance"

Angular 18–21 represents a multi-year turnaround from a framework perceived as boilerplate-heavy and declining:
- **Signals** replaced Zone.js's "magic" with explicit, predictable reactivity
- **Standalone components** eliminated NgModule ceremony
- **Block syntax** (`@if`, `@for`, `@switch`) replaced structural directives
- **Non-destructive hydration** made SSR practical
- **Angular Language Service** dramatically improved IDE experience
- **Satisfaction scores** rose from ~40% (2022) to ~58% (2025) in State of JS

This trajectory is genuine. Angular is no longer the "legacy enterprise choice" — it's a modern framework worth evaluating for new projects, especially when enterprise scale and team structure matter.

## Trade-Off Assessment

**Choose Angular when:**
- You're building enterprise-scale applications with large teams (10+ developers)
- TypeScript everywhere and strict architecture are non-negotiable requirements
- You need the batteries-included approach (routing, forms, HTTP, DI, testing — all built in)
- Your organization has existing Angular investment and expertise
- Accessibility and ARIA compliance are first-class requirements (Angular Aria)
- You're building AI-powered applications and want strong tooling support

**Watch out for:**
- **Bundle size** — ~80 KB gzipped for a minimal app vs ~42 KB for React; meaningful for performance-critical consumer apps
- **Learning curve** — Dependency Injection, decorators, RxJS, and Signals together create a steep initial ramp
- **Zone.js complexity** — even with Signals, Zone.js is still the default; zoneless migration requires deliberate effort
- **Slower ecosystem** — fewer UI component libraries than React; Material Design is good but not as versatile as shadcn/Tailwind
- **Over-engineered for small projects** — Angular's structure is a strength at scale but overhead for a CRUD MVP

## Support Policy

| Release | Status | Active Ends | LTS Ends |
|---|---|---|---|
| 22.x | Expected ~June 1, 2026 | ~Nov 2026 | ~May 2028 |
| 21.x | **LTS** (as of May 19, 2026) | May 19, 2026 | May 19, 2027 |
| 20.x | LTS | Nov 19, 2025 | Nov 28, 2026 |
| 19.x | **EOL** (May 19, 2026) | May 28, 2025 | May 19, 2026 |

Angular releases a new major version every 6 months. Each major version receives 6 months of active support followed by 12 months of LTS (security patches only). This predictable schedule is a significant advantage for enterprise planning.
