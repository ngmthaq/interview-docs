# 5. Enums — and when to avoid them? (Fresher)

An `enum` is a named set of constants.

```ts
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
}
enum Status {
  Active = "ACTIVE", // string enum — readable at runtime
  Inactive = "INACTIVE",
}
```

**Numeric enums** get reverse mapping (`Direction[0] === "Up"`) but emit extra JS and allow any number to sneak in. **String enums** are safer and debuggable.

**`const enum`** — inlined at compile time, no generated object (smaller output), but has caveats with isolated builds:

```ts
const enum Color {
  Red,
  Blue,
}
let c = Color.Red; // compiles to: let c = 0;
```

**Modern alternative** — a union of string literals + `as const` object. No runtime code, fully tree-shakeable:

```ts
const Status = { Active: "ACTIVE", Inactive: "INACTIVE" } as const;
type Status = (typeof Status)[keyof typeof Status]; // "ACTIVE" | "INACTIVE"
```

**Rule:** prefer string enums or `as const` unions; avoid numeric enums in new code.
