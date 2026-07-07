# 20. Express vs Koa, Fastify, and NestJS. (Senior)

Express is the default, but knowing the trade-offs shows depth.

| Framework   | Style                      | Highlights                                                                       |
| ----------- | -------------------------- | -------------------------------------------------------------------------------- |
| **Express** | Minimal, unopinionated     | Huge ecosystem, callback middleware, the de-facto standard                       |
| **Koa**     | Minimal, modern            | By the Express team; `async/await` middleware with a cleaner `ctx`, no built-ins |
| **Fastify** | Minimal, performance-first | Very fast, schema-based validation/serialization, plugin system                  |
| **NestJS**  | Opinionated, structured    | TypeScript-first, DI, modules/controllers/providers; runs on Express or Fastify  |

**When to choose what:**

- **Express** — maximum flexibility, mature ecosystem, team familiarity.
- **Koa** — want lean modern middleware without legacy baggage.
- **Fastify** — throughput-critical APIs with built-in schema validation.
- **NestJS** — large teams/enterprise apps wanting structure, DI, and conventions out of the box.

**Note:** Express's callback-based middleware and lack of built-in async error handling (pre-v5) are its main weaknesses; the others address these differently.

**Key point:** Express wins on ecosystem and flexibility; Koa modernizes its middleware, Fastify optimizes performance + schema validation, and NestJS adds enterprise structure/DI on top — pick based on performance needs, structure, and team size.
