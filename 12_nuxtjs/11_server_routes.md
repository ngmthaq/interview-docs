# 11. What are server routes (API) in Nuxt? (Junior)

Nuxt has a built-in server powered by **Nitro**. Files in **`server/api/`** and **`server/routes/`** become backend endpoints — a full-stack app in one project.

```ts
// server/api/hello.ts  →  /api/hello
export default defineEventHandler((event) => {
  return { message: "Hello from the server" };
});
```

**Reading input:**

```ts
// server/api/users/[id].get.ts  →  GET /api/users/:id
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, "id");
  const query = getQuery(event);
  return await db.users.findById(id);
});

// server/api/users.post.ts  →  POST /api/users
export default defineEventHandler(async (event) => {
  const body = await readBody(event);
  return await db.users.create(body);
});
```

**Notes:**

- Suffix files with the HTTP method (`.get`, `.post`, `.delete`) to restrict them.
- `event` utilities: `readBody`, `getQuery`, `getRouterParam`, `setResponseStatus`, `getHeader`.
- These run **server-side only** — safe for DB access and secrets.

**Key point:** `server/api/` files (via Nitro's `defineEventHandler`) become backend endpoints with method suffixes (`.get`/`.post`); use `readBody`/`getQuery`/`getRouterParam` for input — giving Nuxt a full server layer for DB access and secret handling.
