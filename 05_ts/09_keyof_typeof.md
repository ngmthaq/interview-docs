# 9. `keyof` and `typeof` operators? (Mid)

**`keyof`** produces a **union of an object type's keys**:

```ts
interface User {
  id: number;
  name: string;
}
type UserKey = keyof User; // "id" | "name"
```

**`typeof`** (in a _type_ position) grabs the **type of a runtime value**:

```ts
const config = { host: "localhost", port: 8080 };
type Config = typeof config; // { host: string; port: number }
```

**Combined** — a type-safe property getter, a classic use:

```ts
function get<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]; // T[K] = indexed access type
}
const u = { id: 1, name: "A" };
get(u, "name"); // string
get(u, "xyz"); // ❌ not a key of u
```

**`typeof` + `keyof` on an `as const` object** — derive a union from data:

```ts
const ROLES = ["admin", "user"] as const;
type Role = (typeof ROLES)[number]; // "admin" | "user"
```

**Note:** this is TypeScript's `typeof` in type context — different from JS's runtime `typeof` operator.
