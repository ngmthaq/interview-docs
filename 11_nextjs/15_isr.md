# 15. What is Incremental Static Regeneration (ISR)? (Mid)

**ISR** lets you serve **statically generated** pages that are **updated in the background** after a set interval — without rebuilding the whole site. It combines SSG's speed with fresh-ish data.

```tsx
// App Router — time-based revalidation
export default async function Page() {
  const products = await fetch("https://api.example.com/products", {
    next: { revalidate: 60 }, // regenerate at most once per 60s
  }).then((r) => r.json());
  return <ProductGrid products={products} />;
}

// Or set for the whole route segment:
export const revalidate = 60;
```

**How it works:**

1. First request serves the cached static page.
2. After the `revalidate` window, the **next** request triggers a background regeneration.
3. Once regenerated, subsequent requests get the fresh version (stale-while-revalidate).

**On-demand ISR** — regenerate immediately on an event (e.g. CMS publish):

```ts
revalidatePath("/products"); // or revalidateTag("products")
```

**Key point:** ISR serves fast static pages and regenerates them in the background on a `revalidate` interval (or on-demand via `revalidatePath`/`revalidateTag`) — ideal for large content sites needing near-fresh data without full rebuilds.
