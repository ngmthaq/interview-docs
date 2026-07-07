# 21. What are discriminated unions? (Mid)

A **discriminated (tagged) union** is a union of object types sharing a common **literal "discriminant" field**. TypeScript narrows to the exact member when you check that field — the idiomatic way to model "one of several shapes".

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number }
  | { kind: "rectangle"; width: number; height: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2; // narrowed to circle
    case "square":
      return shape.side ** 2;
    case "rectangle":
      return shape.width * shape.height;
  }
}
```

**Exhaustiveness checking** with `never`:

```ts
default: {
  const _exhaustive: never = shape; // compile error if a case is unhandled
  return _exhaustive;
}
```

**Why it's powerful:**

- The compiler **narrows** each branch to the right type — safe field access.
- Adding a new variant surfaces **compile errors** everywhere it's not handled (via the `never` check).

**Key point:** discriminated unions combine a shared literal tag (`kind`) with `switch`-based narrowing so TypeScript knows each branch's exact shape; pair with a `never` default for exhaustiveness — the safest pattern for modeling variant data.
