# 31. How does Prisma handle the N+1 problem? (Mid)

The **N+1 problem** — one query for a list, then one extra query per item for its relation — also applies to Prisma if you query in a loop.

```ts
// ❌ N+1 — 1 query for users + N queries for each user's posts
const users = await prisma.user.findMany();
for (const user of users) {
  user.posts = await prisma.post.findMany({ where: { authorId: user.id } });
}
```

**Fix 1 — `include`/`select`** (Prisma batches the relation into few queries):

```ts
const users = await prisma.user.findMany({
  include: { posts: true }, // Prisma fetches all posts efficiently
});
```

**Fix 2 — automatic query batching** with `relationLoadStrategy`:

```ts
// "join" — a single SQL JOIN (Postgres/MySQL)
const users = await prisma.user.findMany({
  relationLoadStrategy: "join",
  include: { posts: true },
});
// "query" (default) — separate but batched queries via WHERE IN
```

**Fix 3 — dataloader-style batching** — Prisma automatically **batches `findUnique` calls** in the same tick into a single `WHERE id IN (...)` query, which helps GraphQL resolvers.

**Key point:** avoid N+1 by fetching relations with `include`/`select` instead of looping; choose `relationLoadStrategy: "join"` for a single JOIN or the default batched queries, and rely on Prisma's automatic `findUnique` batching to collapse per-item lookups (e.g. in GraphQL resolvers).
