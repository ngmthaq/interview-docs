# 15. What are provider scopes? (Mid)

By default every provider is a **singleton** — one instance shared across the whole app. Nest offers other **injection scopes** when that's not desired.

```ts
import { Injectable, Scope } from "@nestjs/common";

@Injectable({ scope: Scope.REQUEST })
export class RequestScopedService {
  // A new instance per incoming request
}
```

**Three scopes:**

- **`DEFAULT` (singleton)** — one instance for the app lifetime. Fastest; the default.
- **`REQUEST`** — a new instance **per request**; useful when you need request-specific state (e.g. the current user, request-scoped DB transaction).
- **`TRANSIENT`** — a new instance **each time** it's injected (not shared between consumers).

**Trade-off — performance:**

- Request-scoped providers **bubble up**: any provider/controller depending on one also becomes request-scoped, adding per-request instantiation cost.
- Prefer singletons; reach for `REQUEST` scope only when you truly need per-request isolation.

**Key point:** providers are singletons by default; `Scope.REQUEST` gives a fresh instance per request (for request-specific state) and `Scope.TRANSIENT` per injection — but request scope propagates to dependents and costs performance, so use it sparingly.
