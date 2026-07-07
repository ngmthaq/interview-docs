# 5. How do you navigate between pages? (Fresher)

Next.js provides **client-side navigation** that swaps content without a full page reload, keeping shared layouts mounted.

**Declarative — the `<Link>` component:**

```tsx
import Link from "next/link";

export default function Nav() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/blog/hello">Blog Post</Link>
      <Link href={{ pathname: "/shop", query: { sort: "price" } }}>Shop</Link>
    </nav>
  );
}
```

**Programmatic — the `useRouter` hook** (client components):

```tsx
"use client";
import { useRouter } from "next/navigation"; // note: next/navigation, not next/router

export function LoginButton() {
  const router = useRouter();
  return <button onClick={() => router.push("/dashboard")}>Login</button>;
}
```

**Notes:**

- `<Link>` **prefetches** routes in the viewport for instant navigation.
- In the App Router, import from **`next/navigation`** (`useRouter`, `usePathname`, `useSearchParams`), not the old `next/router`.

**Key point:** use `<Link href>` for declarative navigation (with automatic prefetching) and `useRouter().push()` from `next/navigation` for programmatic navigation — both do client-side transitions that preserve shared layouts.
