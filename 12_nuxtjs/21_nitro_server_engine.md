# 21. What is Nitro? (Senior)

**Nitro** is Nuxt 3's **server engine** — the runtime that powers server routes, SSR, and deployment. It's framework-agnostic and enables Nuxt to deploy almost anywhere.

**What Nitro provides:**

- **Server routes** — the `server/` directory (`defineEventHandler`, powered by **h3**).
- **Universal deployment** — auto-detects and builds for **many targets** (Node, Vercel, Netlify, Cloudflare Workers, Deno, static) with zero config changes.
- **Storage layer** — a unified KV/storage API (`useStorage`) across drivers (memory, Redis, filesystem).
- **Caching** — cached event handlers and route rules (`swr`, `cache`).
- **Auto code-splitting & tree-shaking** for the server bundle.

```ts
// A cached server route via Nitro
export default defineCachedEventHandler(
  async (event) => {
    return await expensiveQuery();
  },
  { maxAge: 60 }, // cache for 60 seconds
);
```

**Deployment presets:**

```ts
export default defineNuxtConfig({
  nitro: { preset: "cloudflare-pages" }, // or vercel, node-server, etc.
});
```

**Key point:** Nitro is Nuxt's server engine (built on h3) providing `server/` routes, a storage/caching layer, and — crucially — portable deployment presets that build the same app for Node, serverless, edge, or static targets without code changes.
