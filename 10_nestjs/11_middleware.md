# 11. What is middleware in NestJS? (Junior)

**Middleware** runs **before** the route handler and before guards — it's the same concept as Express middleware, with access to `req`, `res`, and `next`.

```ts
import { Injectable, NestMiddleware } from "@nestjs/common";
import { Request, Response, NextFunction } from "express";

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log(`${req.method} ${req.originalUrl}`);
    next();
  }
}
```

Apply it in a module via `configure`:

```ts
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes("cats"); // or "*"
  }
}
```

**Middleware vs guards/interceptors:**

- **Middleware** — earliest, close to the raw request; good for logging, CORS, body tweaks.
- Doesn't have access to the `ExecutionContext` / handler metadata that guards and interceptors do.

**Key point:** Nest middleware is Express-style `(req, res, next)` logic configured per-route in a module's `configure()`; it runs first in the pipeline but lacks the handler-aware `ExecutionContext` that guards and interceptors provide.
