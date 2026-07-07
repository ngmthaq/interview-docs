# 2. Nuxt vs plain Vue (Vue + Vite). (Fresher)

Nuxt **builds on** Vue, adding framework-level structure and server capabilities.

| Aspect        | Plain Vue (Vite)                      | Nuxt                                    |
| ------------- | ------------------------------------- | --------------------------------------- |
| Routing       | Manual Vue Router config              | File-based (`pages/`)                   |
| Rendering     | Client-only (SPA) by default          | SSR / SSG / hybrid                      |
| Data fetching | Manual (`fetch`/axios in `onMounted`) | `useFetch` / `useAsyncData` (SSR-aware) |
| SEO           | Poor (empty SPA shell)                | Strong (server-rendered HTML)           |
| Backend       | Separate project                      | Built-in `server/` (Nitro)              |
| Imports       | Explicit                              | Auto-imported                           |

```vue
<script setup>
// Nuxt: SSR-aware data fetching, no manual router/store wiring
const { data } = await useFetch("/api/products");
</script>
```

**When to choose which:**

- **Plain Vue SPA** — internal tools/dashboards with no SEO need and simple routing.
- **Nuxt** — public sites needing SEO, SSR/SSG, or a full-stack setup.

**Key point:** plain Vue is a client-side library you wire up yourself; Nuxt is a full framework adding file-based routing, SSR/SSG, SSR-aware data fetching, a built-in server, and auto-imports — choose Nuxt for SEO/full-stack needs, plain Vue for simple SPAs.
