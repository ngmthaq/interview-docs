# Interview Docs

A personal interview-prep knowledge base. Each topic lives in a numbered folder, and each folder holds **one question per markdown file** — a concise explanation, a TypeScript/JavaScript example, and a bolded key takeaway. Questions are ordered by difficulty (**fresher → junior → mid → senior**).

## Topics

| #   | Topic                 | Questions | Folder                                     |
| --- | --------------------- | --------- | ------------------------------------------ |
| 00  | Algorithms & DS       | 20        | [`00_algorithm`](00_algorithm)             |
| 01  | OOP & FP fundamentals | 20        | [`01_oop`](01_oop)                         |
| 02  | Design patterns       | 20        | [`02_design_patterns`](02_design_patterns) |
| 03  | Databases & ORM       | 35        | [`03_database`](03_database)               |
| 04  | JavaScript            | 35        | [`04_js`](04_js)                           |
| 05  | TypeScript            | 30        | [`05_ts`](05_ts)                           |
| 06  | React.js              | 35        | [`06_reactjs`](06_reactjs)                 |
| 07  | Vue.js                | 35        | [`07_vuejs`](07_vuejs)                     |
| 08  | Node.js               | 30        | [`08_nodejs`](08_nodejs)                   |
| 09  | Express.js            | 20        | [`09_expressjs`](09_expressjs)             |
| 10  | NestJS                | 30        | [`10_nestjs`](10_nestjs)                   |
| 11  | Next.js               | 30        | [`11_nextjs`](11_nextjs)                   |
| 12  | Nuxt.js               | 30        | [`12_nuxtjs`](12_nuxtjs)                   |

**Total: 370 questions** across 13 topics.

## What's inside

- **[00_algorithm](00_algorithm)** — Big O, time/space complexity, core data structures (arrays, linked lists, stacks, queues, hash tables, trees, graphs, heaps), binary search, sorting, recursion, two-pointer, sliding window, BFS/DFS, DP, greedy, backtracking.
- **[01_oop](01_oop)** — four pillars, composition vs inheritance, SOLID, polymorphism, `this` binding, OOP vs FP, mutability, pure functions.
- **[02_design_patterns](02_design_patterns)** — creational/structural/behavioral patterns (singleton, factory, builder, adapter, decorator, observer, strategy), DI, repository, MVC, anti-patterns.
- **[03_database](03_database)** — SQL vs NoSQL, normalization, ACID, transactions, indexes, joins, isolation levels, locking, sharding/replication, CAP, ORMs, N+1, Prisma (schema, client, migrations, relations, transactions, pooling, raw queries).
- **[04_js](04_js)** — scope, closures, `this`, prototypes, event loop, promises & combinators, async/await, HOFs, generators, Map/Set, Proxy, ES modules, symbols, event delegation.
- **[05_ts](05_ts)** — types vs interfaces, generics & constraints, narrowing, utility/mapped/conditional types, discriminated unions, `satisfies`, `as const`, assertion functions, branded & recursive types.
- **[06_reactjs](06_reactjs)** — JSX, hooks, lifecycle, context, memoization, reconciliation, error boundaries, SSR/hydration, server components, concurrent features, `useSyncExternalStore`, React 19 Actions.
- **[07_vuejs](07_vuejs)** — template syntax, directives, `v-model`, computed/watchers, Composition API, reactivity, composables, provide/inject, Router, Pinia, custom directives, `defineModel`, transitions, render functions.
- **[08_nodejs](08_nodejs)** — event loop phases, streams & backpressure, buffers, libuv thread pool, cluster/worker_threads, HTTP, security, testing, graceful shutdown, profiling, caching.
- **[09_expressjs](09_expressjs)** — routing, middleware, `req`/`res`, Router, error handling, REST design, validation, auth, CORS, security, app structure, testing, performance.
- **[10_nestjs](10_nestjs)** — modules/controllers/providers, DI, DTOs & pipes, guards, interceptors, request lifecycle, exception filters, custom providers, scopes, TypeORM, microservices, GraphQL, caching.
- **[11_nextjs](11_nextjs)** — App Router, file-based routing, server vs client components, rendering strategies, data fetching, Server Actions, caching layers, ISR, metadata/SEO, middleware, edge runtime, hydration.
- **[12_nuxtjs](12_nuxtjs)** — file-based routing, rendering modes, `useFetch`/`useAsyncData`, auto-imports, composables, `useState`, server routes, Nitro, SSR/hydration, modules, Pinia, prerendering, deployment.

## Conventions

- **One question per file**, zero-padded sequential numbering (`01_...md`, `02_...md`).
- File heading format: `# N. Question (Level)`.
- Content in **English** with **TypeScript** code examples (noted where concepts apply to Java/C#).
- Each file ends with a **bolded key takeaway**.
