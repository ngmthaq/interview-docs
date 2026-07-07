# 22. What are const assertions (`as const`)? (Mid)

**`as const`** tells TypeScript to infer the **narrowest, immutable** type — literal types instead of widened ones, and `readonly` for arrays/objects.

```ts
// Without as const
let a = "hello"; // type: string
const obj = { role: "admin" }; // type: { role: string }

// With as const
const b = "hello" as const; // type: "hello"
const config = { role: "admin" } as const;
// type: { readonly role: "admin" }
```

**Arrays become readonly tuples of literals:**

```ts
const routes = ["/home", "/about"] as const;
// type: readonly ["/home", "/about"]
type Route = (typeof routes)[number]; // "/home" | "/about"
```

**Common uses:**

- Derive a **union type** from an array of values (`typeof arr[number]`).
- Freeze **config objects** as immutable with literal types.
- Preserve **exact literals** for discriminated unions and function arguments.

```ts
const ACTIONS = ["create", "update", "delete"] as const;
type Action = (typeof ACTIONS)[number]; // "create" | "update" | "delete"
```

**Key point:** `as const` infers literal, deeply-`readonly` types instead of widened ones — ideal for turning a runtime array/object into a single source of truth from which you derive union types via `typeof x[number]`.
