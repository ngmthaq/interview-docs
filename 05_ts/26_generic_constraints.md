# 26. How do generic constraints work? (Mid)

**Constraints** (`extends`) restrict what a generic type parameter can be, so you can safely use its members while staying generic.

```ts
// Without a constraint, you can't access .length (T could be anything)
function longest<T extends { length: number }>(a: T, b: T): T {
  return a.length >= b.length ? a : b;
}

longest("hello", "hi"); // ✅ strings have length
longest([1, 2], [3]); // ✅ arrays have length
longest(10, 20); // ❌ numbers have no length
```

**`keyof` constraint** — type-safe property access:

```ts
function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]; // return type is precisely T[K]
}

const user = { name: "Ada", age: 36 };
getProp(user, "name"); // string
getProp(user, "email"); // ❌ "email" is not a key of user
```

**Default type parameters:**

```ts
interface ApiResponse<T = unknown> {
  data: T;
  status: number;
}
```

**Key point:** `T extends Constraint` narrows a generic so you can access guaranteed members; `K extends keyof T` enables type-safe, precisely-typed property access (`T[K]`), and `<T = Default>` supplies fallback type arguments — constraints make generics both flexible and safe.
