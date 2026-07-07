# 10. What are interceptors in NestJS? (Junior)

**Interceptors** wrap handler execution, running logic **before and after** it. They implement `NestInterceptor` and use RxJS to transform the response stream.

**Use cases:** logging, response transformation, caching, timeouts, mapping exceptions.

```ts
import { CallHandler, ExecutionContext, Injectable, NestInterceptor } from "@nestjs/common";
import { Observable } from "rxjs";
import { map, tap } from "rxjs/operators";

@Injectable()
export class TransformInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const now = Date.now();
    return next.handle().pipe(
      map((data) => ({ data })), // reshape response  →  { data: ... }
      tap(() => console.log(`Took ${Date.now() - now}ms`)), // after handler
    );
  }
}
```

**`next.handle()`** returns an Observable of the handler's result — code **before** it runs pre-handler; operators **after** it run post-handler.

**Scope:** method, controller, or global (`app.useGlobalInterceptors`).

**Key point:** interceptors add before/after logic around handlers (logging, response shaping, caching, timeouts) using RxJS around `next.handle()` — the AOP layer of Nest, scoped from method to global.
