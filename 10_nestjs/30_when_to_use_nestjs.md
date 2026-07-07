# 30. When should you (not) use NestJS? (Senior)

NestJS is powerful but not universal — knowing the trade-offs signals maturity.

**Use NestJS when:**

- **Large / enterprise apps** with many developers — the enforced structure keeps teams consistent.
- You want **built-in** DI, validation, guards, interceptors, testing, microservices, GraphQL, WebSockets.
- **TypeScript-first** teams comfortable with decorators and Angular-style architecture.
- Long-lived codebases where **maintainability** outweighs upfront speed.

**Reconsider when:**

- **Small services / simple APIs / prototypes** — the boilerplate and learning curve outweigh benefits; plain Express or Fastify is faster to ship.
- **Serverless functions** where cold-start time and bundle size matter (Nest's DI/reflection add overhead).
- The team is unfamiliar with **decorators/DI** and has no time to learn.

**Trade-offs:**

- **Pros:** structure, testability, ecosystem, consistency.
- **Cons:** boilerplate, learning curve, abstraction over the underlying platform, some runtime overhead.

**Key point:** choose NestJS for large, team-based, long-lived TypeScript apps that benefit from structure and batteries-included features; skip it for small services, prototypes, or latency-sensitive serverless where Express/Fastify's simplicity wins.
