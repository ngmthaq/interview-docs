# 27. How do you optimize Nuxt performance? (Senior)

Nuxt is fast by default; large apps benefit from deliberate tuning.

**JS & components:**

- **Lazy-load components** — prefix with `Lazy` (`<LazyHeavyChart />`) to defer their JS until rendered.
- **Islands / lazy hydration** — `<NuxtIsland>` and lazy-hydration wrappers hydrate only when needed.
- **`<ClientOnly>`** for browser-only widgets to skip SSR work.

**Data & payload:**

- Use **`pick`/`transform`** in `useFetch` to shrink the SSR payload.
- Prefer **`prerender`/`swr`** route rules over live SSR where possible.
- Cache server routes with **`defineCachedEventHandler`**.
- Fetch in **parallel** to avoid waterfalls.

**Assets:**

- **`@nuxt/image`** for responsive, optimized images; **`@nuxt/fonts`** to self-host fonts.
- Enable **payload extraction** for static routes.

**Analysis:** run `nuxi analyze` to inspect bundle size.

**Key point:** speed up Nuxt with lazy components/hydration, `<ClientOnly>`, smaller SSR payloads (`pick`/`transform`), cached/prerendered routes (`routeRules`, `defineCachedEventHandler`), and optimized images/fonts — measure with `nuxi analyze` to target real bottlenecks.
