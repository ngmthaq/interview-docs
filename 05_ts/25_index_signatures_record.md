# 25. Index signatures and the Record type. (Mid)

An **index signature** describes objects whose keys aren't known ahead of time but share a value type.

```ts
interface StringMap {
  [key: string]: number; // any string key → number
}

const scores: StringMap = { math: 90, science: 85 };
scores.history = 78; // ✅ allowed
```

**`Record<K, V>`** — a cleaner utility for the same idea, with control over the key set:

```ts
type Scores = Record<string, number>; // like the index signature above

// Constrained keys — must include exactly these:
type Roles = Record<"admin" | "user" | "guest", string[]>;
const permissions: Roles = {
  admin: ["read", "write", "delete"],
  user: ["read", "write"],
  guest: ["read"],
}; // missing a key is a compile error
```

**Notes:**

- Index signature keys can be `string`, `number`, or `symbol` (and template literal types).
- Accessing an arbitrary key may yield `undefined` at runtime — enable **`noUncheckedIndexedAccess`** to reflect that in the type.
- Prefer **`Record<Union, V>`** when the key set is known/finite; use an index signature for truly open-ended keys.

**Key point:** index signatures (`[key: string]: V`) and `Record<K, V>` type dictionaries; use `Record` with a union key for a known, exhaustive key set (compiler enforces all keys) and an index signature for open-ended maps — enable `noUncheckedIndexedAccess` for safer lookups.
