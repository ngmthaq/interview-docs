# 30. How do you model and query relations in Prisma? (Mid)

Prisma models relations with the **`@relation`** attribute; the client fetches related data via **`include`**.

**One-to-many:**

```prisma
model User {
  id    Int    @id @default(autoincrement())
  posts Post[] // one user → many posts
}

model Post {
  id       Int  @id @default(autoincrement())
  author   User @relation(fields: [authorId], references: [id])
  authorId Int
}
```

**Many-to-many** (implicit — Prisma manages the join table):

```prisma
model Post { id Int @id @default(autoincrement()) tags Tag[] }
model Tag  { id Int @id @default(autoincrement()) posts Post[] }
```

**Querying relations:**

```ts
// include — fetch related records
const user = await prisma.user.findUnique({
  where: { id: 1 },
  include: { posts: { where: { published: true }, orderBy: { createdAt: "desc" } } },
});

// nested writes — create related rows in one call
await prisma.user.create({
  data: {
    email: "ada@x.com",
    posts: { create: [{ title: "First" }, { title: "Second" }] },
  },
});
```

**Key point:** define relations with `@relation` (one-to-many, one-to-one, or implicit many-to-many with an auto-managed join table), then fetch related data with `include` (filterable/sortable) and create connected rows via **nested writes** — all fully typed.
