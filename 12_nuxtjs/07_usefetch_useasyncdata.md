# 7. useFetch vs useAsyncData vs $fetch. (Junior)

Nuxt provides SSR-aware data-fetching composables that **run on the server** during SSR and **transfer the result** to the client (avoiding a double fetch).

**`useFetch`** — the high-level composable for API calls:

```vue
<script setup>
const { data, pending, error, refresh } = await useFetch("/api/products");
</script>
```

**`useAsyncData`** — wrap any async logic (multiple calls, custom clients):

```vue
<script setup>
const { data } = await useAsyncData("user-posts", async () => {
  const [user, posts] = await Promise.all([$fetch("/api/user"), $fetch("/api/posts")]);
  return { user, posts };
});
</script>
```

**`$fetch`** — the raw HTTP client (Nitro's ofetch); use it inside handlers/events, **not** directly in setup for initial data (it would fetch twice — once on server, once on client).

**Key differences:**

- `useFetch(url)` ≈ `useAsyncData(url, () => $fetch(url))` — a convenient wrapper.
- Both **cache by key** and dedupe during SSR; `$fetch` alone does not.

**Key point:** use `useFetch` for simple API calls and `useAsyncData` for custom/combined async logic — both are SSR-aware (fetch once on the server, hydrate the client); reserve raw `$fetch` for event handlers and inside those composables.
