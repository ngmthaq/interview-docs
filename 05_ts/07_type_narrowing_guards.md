# 7. Type narrowing and type guards? (Mid)

**Narrowing** is how TypeScript shrinks a broad type to a specific one inside a branch, using runtime checks.

**Built-in guards:**

```ts
function f(x: string | number | Date | null) {
  if (typeof x === "string")
    x.toUpperCase(); // typeof
  else if (x instanceof Date)
    x.getTime(); // instanceof
  else if (x && "toFixed" in x) x.toFixed(); // in
  // truthiness check above removed null
}
```

**User-defined type guard** — a function returning `arg is Type`:

```ts
interface Cat {
  meow(): void;
}
function isCat(a: unknown): a is Cat {
  return typeof a === "object" && a !== null && "meow" in a;
}

if (isCat(pet)) pet.meow(); // narrowed to Cat
```

**Discriminated union narrowing** (best pattern) + **exhaustiveness** via `never`:

```ts
function area(s: Shape) {
  switch (s.kind) {
    case "circle":
      return Math.PI * s.r ** 2;
    case "square":
      return s.side ** 2;
    default:
      const _exhaustive: never = s; // ❌ compile error if a case is missed
      return _exhaustive;
  }
}
```
