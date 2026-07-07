# 6. What rendering modes does Nuxt support? (Junior)

Nuxt can render each part of your app differently — a core feature.

- **Universal / SSR (default)** — HTML rendered on the **server per request**, then hydrated on the client. Good SEO + fast first paint.
- **SPA / Client-side** — rendered only in the browser (`ssr: false`). Like a plain Vue app; good for private dashboards.
- **SSG (Static)** — pre-rendered to static HTML at **build time** via `nuxi generate`. Fastest; served from a CDN.
- **Hybrid rendering** — different rules **per route** via `routeRules`.

```ts
// nuxt.config.ts — hybrid rendering per route
export default defineNuxtConfig({
  routeRules: {
    "/": { prerender: true }, // SSG
    "/blog/**": { swr: 3600 }, // cached SSR (stale-while-revalidate)
    "/admin/**": { ssr: false }, // SPA
    "/api/**": { cors: true },
  },
});
```

**Choosing:** marketing/blog → SSG/SWR; personalized → SSR; private app → SPA.

**Key point:** Nuxt supports SSR (default, per-request), SPA (`ssr: false`), and SSG (build-time), plus **hybrid** rendering configured per route with `routeRules` (`prerender`, `swr`, `ssr`) — letting one app mix strategies by path.
