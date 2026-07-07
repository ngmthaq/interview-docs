# 23. Advanced useFetch: keys, caching, and options. (Senior)

Beyond basic usage, `useFetch`/`useAsyncData` have options that matter for correctness and performance.

```vue
<script setup>
const route = useRoute();

const { data, refresh, status } = await useFetch("/api/products", {
  key: `products-${route.params.id}`, // explicit cache key (avoid collisions)
  query: { page: 1 }, // reactive query params
  lazy: true, // don't block navigation; resolve after
  server: true, // fetch during SSR (default)
  immediate: true, // fetch right away
  default: () => [], // fallback while pending
  transform: (res) => res.items, // reshape the response
  pick: ["id", "name"], // keep only these fields in the payload
  watch: [() => route.params.id], // re-fetch when these change
});
</script>
```

**Key options:**

- **`key`** — dedupe/cache identity; set it explicitly for dynamic URLs.
- **`lazy`** — don't block route transition (pair with `pending` UI).
- **`transform`/`pick`** — shrink the SSR payload sent to the client.
- **`watch`** — auto-refetch on reactive dependency changes.
- **`refresh()` / `status`** — manual refetch and state (`idle`/`pending`/`success`/`error`).

**Gotcha:** don't destructure and pass a reactive URL as a plain string — use a getter (`() => \`/api/x/${id.value}\``) so it stays reactive.

**Key point:** control `useFetch` with `key` (cache identity), `lazy` (non-blocking), `transform`/`pick` (smaller payloads), and `watch` (auto-refetch) — and use getter functions for reactive URLs/params so refetching works correctly.
