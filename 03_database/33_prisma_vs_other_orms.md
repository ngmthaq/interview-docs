# 33. Prisma vs TypeORM vs raw SQL. (Mid)

Choosing a data layer means weighing type safety, control, and ergonomics.

| Aspect         | Prisma                                    | TypeORM                                       | Raw SQL (e.g. `pg`)          |
| -------------- | ----------------------------------------- | --------------------------------------------- | ---------------------------- |
| Style          | Schema-first, generated client            | Class/decorator (Active Record & Data Mapper) | Hand-written queries         |
| Type safety    | Excellent (generated from schema)         | Partial (decorators, weaker inference)        | None (unless typed manually) |
| Migrations     | Prisma Migrate (schema-driven)            | Migration files / synchronize                 | Manual / external tool       |
| Learning curve | Low, opinionated                          | Moderate                                      | SQL knowledge                |
| Control        | Abstracted (escape hatch via `$queryRaw`) | Query builder + raw                           | Full                         |

**When to choose:**

- **Prisma** — TypeScript projects wanting strong type safety, great DX, and a clear schema; the modern default.
- **TypeORM** — if you prefer decorator/entity classes or need patterns Prisma lacks (e.g. deep Active Record style); common in NestJS.
- **Raw SQL / query builder (Kysely, Drizzle)** — maximum control, complex analytical queries, or minimal abstraction/overhead.

**Prisma's trade-offs:** less flexible for very complex/dynamic SQL (mitigated by `$queryRaw`), and it runs a query engine.

**Key point:** Prisma leads on type safety and DX with a schema-first model (ideal for most TypeScript apps); TypeORM suits decorator/entity styles, and raw SQL or lightweight builders (Kysely/Drizzle) win when you need full query control — Prisma's `$queryRaw` is its escape hatch for the complex cases.
