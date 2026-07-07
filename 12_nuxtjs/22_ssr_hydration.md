# 22. How does SSR and hydration work in Nuxt? (Senior)

**SSR flow:** the server renders the Vue app to HTML, sends it (fast first paint + SEO), then the client **hydrates** — Vue re-uses the existing DOM and attaches interactivity.

**The payload:** state fetched on the server (via `useFetch`/`useAsyncData`/`useState`) is serialized into the HTML as `__NUXT__` and reused on the client — so it **doesn't re-fetch** during hydration.

```vue
<script setup>
// Runs on the server; result is embedded in the payload and hydrated
const { data } = await useFetch("/api/products");
</script>
```

**Hydration mismatches** occur when server and client render differently:

- Non-deterministic values (`Date.now()`, `Math.random()`).
- Browser-only APIs (`window`) during render.
- Invalid HTML nesting.

**Fixes:** wrap in `<ClientOnly>`, defer to `onMounted`, or guard with `import.meta.client`.

**Optimization:** Nuxt supports **lazy/islands hydration** — `<NuxtIsland>` and lazy hydration components hydrate only when needed, reducing client JS.

**Key point:** Nuxt renders HTML on the server, embeds fetched state in the `__NUXT__` payload, then hydrates without re-fetching; avoid hydration mismatches (non-deterministic/browser-only code) with `<ClientOnly>`/`onMounted`, and use islands/lazy hydration to cut client JS.
