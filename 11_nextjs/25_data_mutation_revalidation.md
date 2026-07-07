# 25. How do you revalidate data after a mutation? (Senior)

After a Server Action or Route Handler changes data, you must **invalidate the relevant caches** so users see fresh content.

```ts
"use server";
import { revalidatePath, revalidateTag } from "next/cache";

export async function updateProduct(id: string, data: FormData) {
  await db.product.update({ where: { id }, data: parse(data) });

  revalidatePath(`/products/${id}`); // purge a specific route
  revalidatePath("/products"); // and the list page
  // OR, if fetches were tagged:
  revalidateTag("products");
}
```

**Two invalidation tools:**

- **`revalidatePath(path)`** — purges the cache for a route (and re-renders on next visit).
- **`revalidateTag(tag)`** — purges every `fetch` that was tagged, across all routes — more surgical.

```ts
// tag a fetch so revalidateTag can target it
await fetch(url, { next: { tags: ["products"] } });
```

**Client-side refresh** — `router.refresh()` re-fetches the current route's server data without losing client state.

**Key point:** after mutations, call `revalidatePath` (route-scoped) or `revalidateTag` (tag-scoped across routes) from Server Actions to purge stale caches; tag fetches upfront for surgical invalidation, and use `router.refresh()` for client-triggered server re-fetches.
