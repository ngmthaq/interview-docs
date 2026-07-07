# 15. Function overloads? (Mid)

Overloads let one function expose **multiple typed signatures**. You declare the signatures, then write **one implementation** that handles all of them.

```ts
function parse(x: string): string[];
function parse(x: number): number;
function parse(x: string | number): string[] | number {
  return typeof x === "string" ? x.split("") : x * 2;
}

const a = parse("abc"); // string[]
const b = parse(42); // number
```

The **implementation signature** is not callable from outside — only the overload declarations are visible to callers.

**Why not just a union return?** Overloads capture the **input→output relationship**. A union return loses it:

```ts
// union version: caller always gets string[] | number, must narrow
function bad(x: string | number): string[] | number {
  /* ... */
}
```

**Modern alternative** — conditional/generic types often express this more cleanly:

```ts
function parse2<T extends string | number>(x: T): T extends string ? string[] : number;
```

**Guideline:** reach for overloads when return type depends on argument type/shape in ways a single signature can't express; otherwise prefer generics or unions.
