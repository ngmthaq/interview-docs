# 15. How do runtimeConfig and environment variables work? (Mid)

**`runtimeConfig`** exposes environment values to your app, distinguishing **server-only** secrets from **client-exposed** public values.

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    apiSecret: "", // server-only (private)
    public: {
      apiBase: "/api", // available on client + server
    },
  },
});
```

Values are overridden at runtime by matching **`NUXT_`** env vars:

```bash
NUXT_API_SECRET=xxx           # → runtimeConfig.apiSecret
NUXT_PUBLIC_API_BASE=https://api.example.com  # → runtimeConfig.public.apiBase
```

Access it via `useRuntimeConfig()`:

```ts
// server-side — full access
const config = useRuntimeConfig();
await $fetch(url, { headers: { Authorization: config.apiSecret } });

// client-side — only `public` is available
const { apiBase } = useRuntimeConfig().public;
```

**Key rules:**

- **Top-level** keys are **server-only** (never sent to the browser).
- **`public`** keys are exposed to the client.
- Override with `NUXT_`-prefixed env vars at runtime (unlike build-time inlining).

**Key point:** `runtimeConfig` separates server-only secrets (top-level) from client-exposed values (`public`), read via `useRuntimeConfig()` and overridable at runtime with `NUXT_`-prefixed env vars — keep secrets out of `public`.
