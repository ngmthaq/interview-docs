# 2. NestJS vs Express. (Fresher)

Nest **runs on** Express (by default) but adds an architectural layer.

| Aspect       | Express                  | NestJS                            |
| ------------ | ------------------------ | --------------------------------- |
| Philosophy   | Minimal, unopinionated   | Opinionated, structured           |
| Language     | JS or TS                 | TypeScript-first                  |
| Architecture | You decide               | Modules / controllers / providers |
| DI           | Manual / third-party     | Built-in IoC container            |
| Boilerplate  | Low                      | Higher (decorators, modules)      |
| Best for     | Small apps, full control | Large/enterprise, teams           |

```ts
// Nest wraps Express-style routing in decorators
@Controller("users")
export class UsersController {
  @Get(":id")
  findOne(@Param("id") id: string) {
    return this.usersService.findOne(id);
  }
}
```

**Trade-off:** Express gives freedom but no guardrails — large teams drift into inconsistent structure. Nest enforces conventions and testability at the cost of more upfront boilerplate and a learning curve.

**Key point:** Express is a minimal library you architect yourself; NestJS is a full framework (on top of Express/Fastify) that imposes modular structure and DI — choose Nest for large, team-based apps and Express for small or highly custom ones.
