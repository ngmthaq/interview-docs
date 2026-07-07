# 17. Explain the Repository pattern. (Mid → Senior)

**Repository** abstracts data access behind a **collection-like interface**, so business logic doesn't know whether data comes from a SQL DB, an API, or memory.

```ts
interface UserRepository {
  findById(id: number): Promise<User | null>;
  save(user: User): Promise<void>;
}

// Swappable implementation — Postgres, Mongo, in-memory, etc.
class SqlUserRepository implements UserRepository {
  async findById(id: number) {
    /* SELECT ... */ return null;
  }
  async save(user: User) {
    /* INSERT/UPDATE ... */
  }
}

// Business logic depends only on the interface
class UserService {
  constructor(private repo: UserRepository) {}
  async promote(id: number) {
    const user = await this.repo.findById(id);
    // ...domain logic, storage-agnostic
  }
}
```

**Benefits:**

- Decouples **domain logic from persistence** — swap DBs without touching services.
- Easy to test with an **in-memory repository** (no real DB).
- Centralizes query logic in one place.

**Watch out (Senior):** don't over-abstract — if you're just wrapping an ORM 1:1, the extra layer may add little value.
