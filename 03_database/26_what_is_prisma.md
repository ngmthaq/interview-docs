# 26. What is Prisma? (Fresher)

**Prisma** is a modern, **type-safe ORM** for Node.js/TypeScript. Instead of decorators on classes (TypeORM) or query builders, you define your data model in a **schema file**, and Prisma **generates** a fully-typed client.

**Three main parts:**

- **Prisma Schema** (`schema.prisma`) — declarative model definitions + datasource + generator.
- **Prisma Client** — auto-generated, type-safe query API tailored to your schema.
- **Prisma Migrate** — schema-driven migration tool.

```prisma
// schema.prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id    Int    @id @default(autoincrement())
  email String @unique
  name  String?
}
```

```ts
const users = await prisma.user.findMany(); // fully typed: User[]
```

**Why it stands out:**

- **End-to-end type safety** — queries, results, and relations are typed from the schema.
- **Autocompletion** and compile-time checks catch errors early.
- Supports PostgreSQL, MySQL, SQLite, SQL Server, MongoDB, CockroachDB.

**Key point:** Prisma is a schema-first, type-safe ORM — you declare models in `schema.prisma`, and it generates a typed Prisma Client plus migrations, giving end-to-end type safety from database to application code.
