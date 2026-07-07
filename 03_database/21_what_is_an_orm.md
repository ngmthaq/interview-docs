# 21. What is an ORM and what are its trade-offs? (Junior → Mid)

An **ORM (Object-Relational Mapper)** maps database tables to objects/classes in your code, so you work with objects instead of writing raw SQL.

```ts
// Raw SQL
const rows = await db.query("SELECT * FROM users WHERE id = $1", [1]);

// ORM (e.g. Prisma / TypeORM)
const user = await userRepository.findOne({ where: { id: 1 } });
```

**Benefits:**

- Less boilerplate; work in your language's objects.
- Handles mapping, relations, migrations, and basic validation.
- Reduces raw SQL injection risk (parameterized by default).
- Portable across DB engines.

**Trade-offs:**

- **Abstraction leaks** — complex queries are awkward; you may fall back to raw SQL.
- **Hidden performance costs** (N+1, over-fetching) if you don't understand the generated SQL.
- Learning curve and some overhead.

**Key point:** an ORM boosts productivity, but you must still understand the **SQL it generates** to keep it fast. Examples: Prisma, TypeORM, Sequelize (JS); Hibernate (Java); Entity Framework (C#).
