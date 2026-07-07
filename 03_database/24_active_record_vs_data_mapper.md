# 24. Active Record vs Data Mapper — what's the difference? (Mid → Senior)

Two common ORM architectural styles.

**Active Record** — the model object **contains both data and persistence logic**. The entity knows how to save itself.

```ts
// Active Record (e.g. Sequelize, Laravel Eloquent, TypeORM ActiveRecord mode)
const user = new User();
user.name = "Ann";
await user.save(); // the entity persists itself
```

**Data Mapper** — entities are **plain objects**; a separate **repository/mapper** handles persistence. Domain logic is decoupled from the database.

```ts
// Data Mapper (e.g. Prisma, TypeORM repository mode, Hibernate)
const user = new User();
user.name = "Ann";
await userRepository.save(user); // repository persists the entity
```

|                   | Active Record     | Data Mapper                    |
| ----------------- | ----------------- | ------------------------------ |
| Coupling          | Entity tied to DB | Entity is persistence-ignorant |
| Simplicity        | Simpler for CRUD  | More boilerplate               |
| Testability / DDD | Harder            | Better (clean domain layer)    |

**Key point:** Active Record is faster to write for simple apps; Data Mapper scales better for complex domains and clean architecture (separates domain from persistence).
