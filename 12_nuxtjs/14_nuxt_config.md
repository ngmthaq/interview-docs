# 14. What is nuxt.config.ts? (Mid)

**`nuxt.config.ts`** is the central configuration file controlling modules, rendering, runtime config, build, and app-wide settings.

```ts
export default defineNuxtConfig({
  // Register modules
  modules: ["@nuxtjs/tailwindcss", "@pinia/nuxt"],

  // Global head defaults
  app: {
    head: { title: "My App", meta: [{ name: "description", content: "..." }] },
  },

  // Per-route rendering rules (hybrid)
  routeRules: {
    "/": { prerender: true },
    "/admin/**": { ssr: false },
  },

  // Runtime configuration (env-driven)
  runtimeConfig: {
    apiSecret: process.env.API_SECRET, // server-only
    public: {
      apiBase: process.env.API_BASE, // exposed to the client
    },
  },

  // CSS, build, nitro, vite options...
  css: ["~/assets/main.css"],
});
```

**Key sections:** `modules`, `app.head`, `routeRules`, `runtimeConfig`, `css`, `nitro`, `vite`, `ssr`.

**Key point:** `nuxt.config.ts` is the single source of app configuration — registering modules, setting head defaults, defining hybrid `routeRules`, exposing `runtimeConfig`, and tuning build/server behavior via a typed `defineNuxtConfig` object.
