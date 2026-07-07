# 1. What is Nuxt.js? (Fresher)

**Nuxt** is a **full-stack framework for Vue.js** — the Vue equivalent of Next.js. It adds structure and production features on top of Vue: **file-based routing**, multiple **rendering modes** (SSR, SSG, hybrid), a **server engine**, auto-imports, and build optimizations.

```vue
<!-- pages/index.vue — a route rendered on the server by default -->
<template>
  <h1>Welcome to Nuxt</h1>
</template>
```

**What Nuxt gives you over plain Vue:**

- **File-based routing** — files in `pages/` become routes (no manual Vue Router setup).
- **Rendering flexibility** — SSR, SSG, SPA, or per-route hybrid rendering.
- **Full-stack** — build a backend with the `server/` directory (Nitro engine).
- **Auto-imports** — components, composables, and Vue APIs imported automatically.
- **Batteries included** — data fetching, SEO, state, and a large module ecosystem.

Nuxt 3 is built on **Vue 3**, **Vite**, and **Nitro** (its server engine).

**Key point:** Nuxt is a full-stack Vue framework providing file-based routing, flexible rendering (SSR/SSG/hybrid), a Nitro server backend, and auto-imports — turning Vue from a UI library into a complete application framework.
