# 27. How do you define models in the Prisma schema? (Fresher)

The **`schema.prisma`** file declares your **models** (tables), fields, types, and attributes using Prisma Schema Language (PSL).

```prisma
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?  // optional (nullable)
  published Boolean  @default(false)
  views     Int      @default(0)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
  tags      String[] // scalar list (Postgres)

  @@index([authorId])       // model-level index
  @@map("posts")            // map to a differently-named table
}
```

**Field-level attributes:**

- **`@id`** — primary key; **`@default(...)`** — default value (`autoincrement()`, `now()`, `uuid()`, `cuid()`).
- **`@unique`** — unique constraint; **`@updatedAt`** — auto-set on update.
- **`@relation`** — define a relation; **`@map`** — map to a different column name.
- **`?`** marks optional (nullable); **`[]`** marks a list.

**Block-level attributes:** `@@index`, `@@unique`, `@@id` (composite key), `@@map`.

**Key point:** Prisma models are declared in PSL with typed fields and attributes — `@id`/`@default`/`@unique`/`@updatedAt` at the field level and `@@index`/`@@unique`/`@@map` at the model level — forming the single source of truth for both the database schema and the generated client.
