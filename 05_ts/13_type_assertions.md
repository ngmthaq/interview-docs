# 13. Type assertions (`as`) and `as const`? (Mid)

A **type assertion** tells the compiler "trust me, this is type X". It does **no runtime check or conversion** — purely a compile-time override.

```ts
const el = document.getElementById("app") as HTMLInputElement;
el.value; // compiler now allows it
```

**Assertion vs casting:** it does **not** convert values. `"5" as number` is a compile error; assertions only reinterpret, they don't transform.

**Prefer narrowing over asserting** — assertions can lie and cause runtime crashes:

```ts
const x = someUnknown as string; // dangerous if it's actually a number
if (typeof someUnknown === "string") {
  /* safe */
} // better
```

**`as const`** — a _const assertion_: makes everything deeply `readonly` and infers literal types:

```ts
const point = { x: 1, y: 2 } as const;
// { readonly x: 1; readonly y: 2 }  (not number)

const arr = [1, 2, 3] as const; // readonly [1, 2, 3] tuple
```

**Non-null assertion `!`** — asserts a value isn't `null`/`undefined`:

```ts
const val = map.get("k")!; // trust: not undefined
```

**Avoid `as any`** — it discards all safety. Reach for a proper guard instead.
