# 19. How do you create custom decorators? (Mid)

Custom decorators extract or attach metadata cleanly, reducing boilerplate in handlers.

**Param decorator** — pull data off the request:

```ts
import { createParamDecorator, ExecutionContext } from "@nestjs/common";

export const CurrentUser = createParamDecorator(
  (data: unknown, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user; // set earlier by an auth guard
  },
);

// usage — cleaner than @Req() req then req.user
@Get("profile")
getProfile(@CurrentUser() user: User) {
  return user;
}
```

**Metadata decorator** — attach data read by a guard via `Reflector`:

```ts
export const Roles = (...roles: string[]) => SetMetadata("roles", roles);

@Roles("admin")
@UseGuards(RolesGuard)
@Delete(":id")
remove(@Param("id") id: string) { ... }
```

The `RolesGuard` reads it: `this.reflector.get("roles", context.getHandler())`.

**Key point:** use `createParamDecorator` for reusable request-extraction decorators (like `@CurrentUser()`) and `SetMetadata` for attaching metadata (like `@Roles()`) that guards read via `Reflector` — both reduce boilerplate and express intent declaratively.
