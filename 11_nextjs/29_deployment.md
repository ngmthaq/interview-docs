# 29. How do you deploy a Next.js app? (Senior)

Next.js can deploy to many targets, each with trade-offs around its server features.

**Options:**

- **Vercel** — the first-party platform; zero-config support for SSR, ISR, Server Actions, edge middleware, image optimization, and preview deployments.
- **Self-hosted (Node server)** — `next build && next start` behind a reverse proxy; you manage scaling and caching.
- **Docker** — use the **`output: "standalone"`** build for a minimal image bundling only needed files.
- **Static export** — `output: "export"` produces pure static HTML (no SSR/ISR/Server Actions/Route Handlers).

```js
// next.config.js
module.exports = {
  output: "standalone", // slim, self-contained server bundle for Docker
};
```

**Considerations:**

- **ISR/caching** needs persistent or shared storage when running **multiple instances** (or a shared cache handler) — otherwise nodes diverge.
- **Edge middleware** requires a platform that supports the Edge Runtime.
- Set **environment variables** per environment; run **`next build`** in CI.

**Key point:** Vercel gives zero-config support for all features; self-hosting via `next start` or a `standalone` Docker image works too, but you must handle shared ISR/cache storage across instances and ensure the platform supports edge features — static export drops server-only capabilities.
