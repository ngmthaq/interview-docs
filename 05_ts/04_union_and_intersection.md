# 4. Union vs intersection types? (Fresher)

- **Union (`|`)** — value is **one of** several types ("OR").
- **Intersection (`&`)** — value is **all of** several types at once ("AND").

```ts
type Id = string | number; // union: either
type A = { name: string };
type B = { age: number };
type AB = A & B; // intersection: must have both
const p: AB = { name: "x", age: 1 };
```

With a union you can only access members **common to every member** until you narrow:

```ts
function print(x: string | number) {
  // x.toFixed(); ❌ not on string
  if (typeof x === "number") x.toFixed(); // ✅ narrowed
}
```

**Discriminated unions** — a shared literal "tag" makes narrowing clean:

```ts
type Shape = { kind: "circle"; r: number } | { kind: "square"; side: number };

function area(s: Shape) {
  switch (s.kind) {
    case "circle":
      return Math.PI * s.r ** 2;
    case "square":
      return s.side ** 2;
  }
}
```
