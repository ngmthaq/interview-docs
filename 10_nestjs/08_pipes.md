# 8. What are pipes in NestJS? (Junior)

**Pipes** run **before** a handler to **transform** or **validate** incoming arguments. They operate on route parameters, query params, and bodies.

**Two use cases:**

- **Transformation** — convert input (string → number).
- **Validation** — check input and throw if invalid.

**Built-in pipes:** `ValidationPipe`, `ParseIntPipe`, `ParseUUIDPipe`, `ParseBoolPipe`, `DefaultValuePipe`.

```ts
@Get(":id")
findOne(@Param("id", ParseIntPipe) id: number) {
  // id is guaranteed to be a number, or a 400 is thrown
  return this.service.findOne(id);
}
```

**Custom pipe:**

```ts
@Injectable()
export class TrimPipe implements PipeTransform {
  transform(value: string) {
    return value?.trim();
  }
}
```

**Scope:** pipes can be applied per-parameter, per-handler (`@UsePipes`), per-controller, or globally (`app.useGlobalPipes`).

**Key point:** pipes transform and/or validate handler arguments before the handler runs — use built-ins like `ParseIntPipe`/`ValidationPipe` or write custom ones, applied at parameter, handler, controller, or global scope.
