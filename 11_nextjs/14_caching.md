# 14. Explain caching in Next.js. (Mid)

Next.js (App Router) has **multiple cache layers**. Understanding them is a common senior question.

**Four caches:**

1. **Request Memoization** — dedupes identical `fetch` calls **within a single render** pass.
2. **Data Cache** — persists `fetch` results **across requests** and deployments (controlled by `cache`/`revalidate`).
3. **Full Route Cache** — caches the rendered **HTML/RSC payload** of static routes at build time.
4. **Router Cache** — client-side cache of visited route segments for instant back/forward navigation.

```ts
fetch(url); // Data Cache: stored (static)
fetch(url, { cache: "no-store" }); // opt out — dynamic
fetch(url, { next: { revalidate: 60 } }); // time-based revalidation
```

**Invalidation:**

```ts
revalidatePath("/products"); // purge a route
revalidateTag("products"); // purge all fetches tagged "products"
```

**Notes:**

- Caches are **aggressive by default** — a frequent gotcha is stale data; opt out with `no-store` or `revalidate`.
- Next 15 changed some defaults (e.g. `fetch` and Route Handlers no longer cached by default).

**Key point:** Next.js layers Request Memoization, Data Cache, Full Route Cache, and Router Cache; control them with `fetch` options (`cache`/`revalidate`/`tags`) and purge with `revalidatePath`/`revalidateTag` — caching is aggressive, so opt out explicitly for dynamic data.
