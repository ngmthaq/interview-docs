# 7. Server Components vs Client Components. (Junior)

In the App Router, components are **Server Components by default**. You opt into client behavior with the **`"use client"`** directive.

**Server Components** (default):

- Render on the **server**; their JS is **not** shipped to the browser.
- Can be **async** and fetch data, access the DB, read secrets directly.
- **Cannot** use hooks (`useState`, `useEffect`) or browser APIs or event handlers.

**Client Components** (`"use client"`):

- Run in the browser; support **state, effects, event handlers**, browser APIs.
- Add to the JS bundle.

```tsx
// Server Component — fetches data, zero client JS
export default async function Page() {
  const posts = await db.getPosts();
  return <PostList posts={posts} />;
}

// Client Component — interactive
("use client");
export function LikeButton() {
  const [liked, setLiked] = useState(false);
  return <button onClick={() => setLiked(!liked)}>{liked ? "♥" : "♡"}</button>;
}
```

**Best practice:** keep components as Server Components; push `"use client"` to the **leaves** (small interactive widgets) to minimize bundle size.

**Key point:** Server Components (default) render on the server with no client JS and can fetch data directly; Client Components (`"use client"`) enable interactivity but add to the bundle — keep the tree server-first and isolate interactivity at the leaves.
