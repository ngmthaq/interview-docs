# 29. How do you control response serialization? (Senior)

To avoid leaking sensitive fields (like password hashes), Nest uses **`class-transformer`** with the **`ClassSerializerInterceptor`** to shape outgoing responses.

```ts
import { Exclude, Expose, Transform } from "class-transformer";

export class UserEntity {
  id: number;
  name: string;

  @Exclude() // never sent in responses
  password: string;

  @Expose({ name: "displayName" }) // rename in output
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}
```

Enable the interceptor (globally or per-controller):

```ts
app.useGlobalInterceptors(new ClassSerializerInterceptor(app.get(Reflector)));

@Get(":id")
findOne(): UserEntity {
  return this.usersService.findOne(id); // @Exclude fields stripped automatically
}
```

**Notes:**

- The handler must **return a class instance** (not a plain object) for decorators to apply.
- `@Exclude()` hides fields; `@Expose()` includes/renames; `@Transform()` reshapes values.

**Key point:** use `ClassSerializerInterceptor` + `class-transformer` decorators (`@Exclude`, `@Expose`, `@Transform`) to strip or reshape fields in responses — return entity **instances** so sensitive data like passwords never leaks to clients.
