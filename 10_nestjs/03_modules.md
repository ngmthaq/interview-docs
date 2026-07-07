# 3. What are modules in NestJS? (Fresher)

A **module** is a class annotated with **`@Module()`** that groups related controllers and providers. Every Nest app has at least a **root module** (`AppModule`), and features are organized into their own modules.

```ts
import { Module } from "@nestjs/common";
import { CatsController } from "./cats.controller";
import { CatsService } from "./cats.service";

@Module({
  imports: [], // other modules this one depends on
  controllers: [CatsController], // request handlers
  providers: [CatsService], // injectable services
  exports: [CatsService], // make providers available to importers
})
export class CatsModule {}
```

**The four metadata keys:**

- **`controllers`** — handle incoming requests.
- **`providers`** — services/repositories, injectable within this module.
- **`imports`** — pull in other modules to use their exported providers.
- **`exports`** — expose this module's providers to modules that import it.

Modules are **singletons** — once created they're shared across the app.

**Key point:** modules (`@Module`) are the organizational unit of a Nest app, bundling controllers and providers; `imports`/`exports` wire modules together, and encapsulation means a provider is private unless explicitly exported.
