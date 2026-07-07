# 17. How do you structure a large Express app? (Senior)

As apps grow, a single `app.ts` becomes unmaintainable. Organize by **layers** (or by feature) with clear separation of concerns.

```
src/
├── app.ts            # create app, register global middleware
├── server.ts         # bootstrap: listen, graceful shutdown
├── routes/           # route definitions (thin)
├── controllers/      # parse req, call services, shape res
├── services/         # business logic (framework-agnostic)
├── repositories/     # data access (DB queries / ORM)
├── middlewares/      # auth, validation, error handler
├── models/           # schemas / entities
└── config/           # env loading, constants
```

**Principles:**

- **Thin routes → controllers → services → repositories.** Business logic must not live in route handlers.
- **Separate `app` from `server`** — export `app` (for testing with supertest) and start listening in `server.ts`.
- **Dependency injection** or simple module imports to keep layers testable.
- Group by **feature/domain** (`/users`, `/orders`) for very large codebases (vertical slices).

**Key point:** split responsibilities into routes → controllers → services → repositories, keep business logic out of handlers, and separate `app` (testable) from `server` (bootstrap) — this keeps large Express apps maintainable and unit-testable.
