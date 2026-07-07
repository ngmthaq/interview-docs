# 28. How do you deploy a Nuxt app? (Senior)

Thanks to **Nitro**, Nuxt deploys to many targets — often with **zero config**, since Nitro auto-detects the platform.

**Build outputs:**

```bash
npx nuxi build      # SSR server → .output/  (run with: node .output/server/index.mjs)
npx nuxi generate   # static site → .output/public/  (CDN/static host)
```

**Deployment targets (Nitro presets):**

- **Node server** — `node .output/server/index.mjs` behind a reverse proxy.
- **Serverless** — Vercel, Netlify (auto-detected).
- **Edge** — Cloudflare Workers/Pages, Deno Deploy.
- **Static** — any static host / CDN (from `nuxi generate`).
- **Docker** — the self-contained `.output` directory.

```ts
// force a specific preset if not auto-detected
export default defineNuxtConfig({ nitro: { preset: "node-server" } });
```

**Considerations:**

- **SSR + caching (SWR/ISR)** across multiple instances needs a **shared cache/storage driver** (e.g. Redis via `nitro.storage`) so nodes stay consistent.
- Set **`runtimeConfig`** via `NUXT_` env vars per environment.

**Key point:** Nitro lets one Nuxt codebase deploy as a Node server, serverless, edge, static, or Docker image — often auto-detected, overridable via `nitro.preset`; for multi-instance SSR caching, configure a shared storage driver so ISR/SWR stays consistent.
