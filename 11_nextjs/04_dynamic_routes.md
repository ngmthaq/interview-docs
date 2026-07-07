# 4. What are dynamic routes? (Fresher)

**Dynamic routes** use **bracket folders** to capture URL segments as parameters — for pages whose path depends on data (a blog slug, a product id).

```
app/blog/[slug]/page.tsx      →  /blog/hello-world
app/shop/[category]/[id]/...  →  /shop/shoes/42
app/docs/[...slug]/page.tsx   →  /docs/a/b/c   (catch-all)
app/docs/[[...slug]]/page.tsx →  /docs  AND  /docs/a/b (optional catch-all)
```

Access the param via the `params` prop:

```tsx
// app/blog/[slug]/page.tsx
export default async function Post({ params }: { params: Promise<{ slug: string }> }) {
  const { slug } = await params; // params is async in Next 15
  const post = await getPost(slug);
  return <article>{post.title}</article>;
}
```

**Bracket types:**

- **`[id]`** — single dynamic segment.
- **`[...slug]`** — catch-all (one or more segments).
- **`[[...slug]]`** — optional catch-all (also matches the base path).

**Key point:** bracket folders create dynamic routes — `[id]` for one segment, `[...slug]` for catch-all, `[[...slug]]` for optional catch-all — and the captured values arrive via the `params` prop (awaited in Next 15).
