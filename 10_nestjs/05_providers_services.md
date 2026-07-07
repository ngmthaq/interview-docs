# 5. What are providers and services? (Fresher)

A **provider** is any class that can be **injected** as a dependency. The most common provider is a **service** — a class decorated with **`@Injectable()`** that holds business logic.

```ts
import { Injectable } from "@nestjs/common";

@Injectable()
export class CatsService {
  private cats: Cat[] = [];

  findAll(): Cat[] {
    return this.cats;
  }

  create(cat: Cat): Cat {
    this.cats.push(cat);
    return cat;
  }
}
```

Register it in a module's `providers`, then inject via the constructor:

```ts
@Controller("cats")
export class CatsController {
  constructor(private readonly catsService: CatsService) {} // injected
}
```

**Key ideas:**

- **`@Injectable()`** marks a class as manageable by Nest's IoC container.
- Providers include services, repositories, factories, helpers — anything injectable.
- By default providers are **singletons** (one instance per app).

**Key point:** providers are injectable classes (usually `@Injectable()` services holding business logic) managed by Nest's DI container; register them in a module and inject them through constructors — keeping logic out of controllers.
