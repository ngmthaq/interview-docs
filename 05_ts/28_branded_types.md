# 28. What are branded (nominal) types? (Senior)

TypeScript is **structurally typed** — two types with the same shape are interchangeable. **Branded types** simulate **nominal typing** to prevent mixing values that happen to share a structure (e.g. different kinds of IDs).

```ts
// Both are just strings structurally — easy to mix up
type UserId = string;
type OrderId = string;

function getUser(id: UserId) {}
getUser(someOrderId); // ❌ no error — but it's a bug!
```

**Branding** adds a phantom tag so the types become distinct:

```ts
type Brand<T, B> = T & { readonly __brand: B };

type UserId = Brand<string, "UserId">;
type OrderId = Brand<string, "OrderId">;

const asUserId = (id: string) => id as UserId;

function getUser(id: UserId) {}
getUser(asUserId("u1")); // ✅
getUser("o1" as OrderId); // ❌ OrderId is not assignable to UserId
```

**Notes:**

- The `__brand` field exists only at **compile time** — zero runtime cost.
- Use a smart constructor (that validates) to create branded values.
- Great for **IDs, units** (Meters vs Feet), and **validated** strings (Email, NonEmptyString).

**Key point:** branded types intersect a base type with a phantom tag (`T & { __brand }`) to make structurally-identical types nominally distinct — preventing bugs like passing an `OrderId` where a `UserId` is expected, at zero runtime cost.
