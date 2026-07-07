# 1. What is NestJS? (Fresher)

**NestJS** is a **progressive, opinionated** Node.js framework for building scalable server-side applications. It's written in **TypeScript**, uses **decorators**, and is heavily inspired by Angular's architecture (modules, DI, providers).

```ts
import { Controller, Get } from "@nestjs/common";

@Controller("cats")
export class CatsController {
  @Get()
  findAll(): string {
    return "This returns all cats";
  }
}
```

**What Nest gives you over bare Express:**

- **Structure** — modules, controllers, providers enforce a consistent architecture.
- **Dependency Injection** — built-in IoC container.
- **TypeScript-first** — decorators and strong typing throughout.
- **Platform-agnostic** — runs on **Express** (default) or **Fastify** under the hood.
- **Batteries included** — validation, guards, interceptors, pipes, microservices, GraphQL, WebSockets.

**Key point:** NestJS is an opinionated, TypeScript-first framework layering Angular-style architecture (modules + DI + decorators) on top of Express/Fastify — it trades Express's freedom for structure, testability, and built-in enterprise features.
