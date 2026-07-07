# 8. How do you fetch data in the App Router? (Junior)

In the App Router you fetch data **directly inside async Server Components** — no `getServerSideProps`/`getStaticProps`.

```tsx
// app/products/page.tsx
export default async function Products() {
  const res = await fetch("https://api.example.com/products");
  const products = await res.json();
  return (
    <ul>
      {products.map((p) => (
        <li key={p.id}>{p.name}</li>
      ))}
    </ul>
  );
}
```

**Caching is controlled per-fetch:**

```tsx
fetch(url); // cached indefinitely (static)
fetch(url, { cache: "no-store" }); // always fresh (dynamic/SSR)
fetch(url, { next: { revalidate: 3600 } }); // ISR — refresh hourly
fetch(url, { next: { tags: ["products"] } }); // tag for on-demand revalidation
```

**Notes:**

- The extended `fetch` **dedupes** identical requests within a render (request memoization).
- For DB access, call your ORM/client directly in the Server Component — no `fetch` needed.
- Fetch in **parallel** (`Promise.all`) to avoid waterfalls.

**Key point:** fetch directly in async Server Components using the extended `fetch` (auto-deduped), and control caching per call via `cache`/`revalidate`/`tags` — replacing the old `getServerSideProps`/`getStaticProps` data-fetching functions.
