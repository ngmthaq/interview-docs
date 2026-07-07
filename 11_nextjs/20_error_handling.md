# 20. How do you handle errors in the App Router? (Mid)

The App Router uses **file conventions** to define error boundaries per route segment.

**`error.tsx`** — catches errors in a segment (must be a Client Component):

```tsx
"use client";

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

**`not-found.tsx`** — rendered when `notFound()` is called:

```tsx
import { notFound } from "next/navigation";

export default async function Page({ params }) {
  const post = await getPost((await params).slug);
  if (!post) notFound(); // renders the nearest not-found.tsx (404)
  return <article>{post.title}</article>;
}
```

**Hierarchy:**

- **`error.tsx`** — catches runtime errors in its segment and children; `reset()` retries.
- **`global-error.tsx`** — catches errors in the root layout.
- **`not-found.tsx`** — for 404s via `notFound()`.

**Key point:** define `error.tsx` (client boundary with `reset()`) for runtime errors per segment, `global-error.tsx` for the root, and `not-found.tsx` triggered by `notFound()` for 404s — error handling is expressed through file conventions scoped to route segments.
