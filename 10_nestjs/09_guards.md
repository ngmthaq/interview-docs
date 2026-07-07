# 9. What are guards in NestJS? (Junior)

**Guards** decide whether a request is **allowed to proceed** to the handler. They implement `CanActivate` and return `true`/`false` (or throw). Their primary use is **authentication and authorization**.

```ts
import { CanActivate, ExecutionContext, Injectable } from "@nestjs/common";

@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    return Boolean(request.headers.authorization); // allow only if present
  }
}
```

Apply it:

```ts
@UseGuards(AuthGuard)
@Get("profile")
getProfile() { ... }
```

**Key ideas:**

- Guards run **after** middleware but **before** interceptors/pipes.
- Return `false` → Nest throws `403 Forbidden`; throw an exception for custom responses.
- Scope: method, controller, or global (`app.useGlobalGuards`).
- The `ExecutionContext` gives access to the request, handler, and class metadata (used with `Reflector` for role-based checks).

**Key point:** guards implement `CanActivate` to permit or deny requests (auth/authorization); they run before pipes/interceptors, can be scoped from method to global, and use `ExecutionContext` + `Reflector` for role-based access control.
