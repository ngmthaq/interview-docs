# 26. How does static site generation / prerendering work? (Senior)

Nuxt can **pre-render** routes to static HTML at build time via **`nuxi generate`** or `routeRules`, serving them from a CDN with no server.

```bash
npx nuxi generate   # crawls & pre-renders to .output/public
```

**Crawler-based prerendering:** Nuxt starts at `/` and follows `<NuxtLink>`s to discover routes. Routes not linked (e.g. dynamic pages) must be listed explicitly:

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  nitro: {
    prerender: {
      crawlLinks: true,
      routes: ["/sitemap.xml", "/blog/post-1", "/blog/post-2"],
    },
  },
  routeRules: {
    "/": { prerender: true }, // static
    "/blog/**": { prerender: true }, // static
    "/dashboard/**": { ssr: false }, // SPA
  },
});
```

**Hybrid advantage:** unlike a full static export, `routeRules` lets you pre-render some routes while others stay SSR or SPA — all in one build.

**ISR-like behavior:** on supported hosts, `routeRules: { '/news/**': { isr: 3600 } }` regenerates static pages periodically.

**Key point:** `nuxi generate` (or `prerender` route rules) pre-renders routes to static HTML by crawling links — list un-linked dynamic routes explicitly; `routeRules` enables **hybrid** builds (prerender + SSR + SPA + ISR) rather than an all-or-nothing static export.
