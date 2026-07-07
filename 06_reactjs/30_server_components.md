# 30. React Server Components (RSC)? (Senior)

Server Components **run only on the server** and send a serialized description of the UI to the client — they ship **zero JavaScript** to the browser. Popularized by Next.js App Router; part of React 19.

```tsx
// app/page.tsx — a Server Component (default in App Router)
async function Page() {
  const posts = await db.posts.findMany(); // runs on server, direct DB access
  return <PostList posts={posts} />;
}
```

**Server vs Client Components:**

|               | Server Component | Client Component (`"use client"`) |
| ------------- | ---------------- | --------------------------------- |
| Runs          | server only      | server (SSR) + client             |
| Ships JS      | ❌ none          | ✅ bundled                        |
| State/effects | ❌ no hooks      | ✅ `useState`/`useEffect`         |
| Data access   | direct (DB, fs)  | via API/props                     |
| Interactivity | ❌               | ✅ events, state                  |

**Benefits:**

- **Smaller bundles** — non-interactive UI ships no JS.
- **Direct backend access** — query the DB/filesystem without an API layer.
- **Secrets stay server-side** — API keys never reach the client.

**Rules:**

- Add `"use client"` to opt a component (and its imports) into the client.
- Server Components **can render** Client Components, but not vice-versa (pass them as `children`/props).
- No hooks, no browser APIs, no event handlers in Server Components.

**RSC vs SSR:** SSR renders Client Components to HTML then hydrates them. RSC components **never** hydrate — they aren't interactive and send no JS at all. The two work together.
