# 32. What are Symbols? (Mid)

A **`Symbol`** is a **unique, immutable primitive** often used as a non-colliding object key. Every symbol is distinct, even with the same description.

```js
const a = Symbol("id");
const b = Symbol("id");
a === b; // false — always unique

const user = {
  name: "Ada",
  [a]: 123, // symbol-keyed property
};
user[a]; // 123
```

**Why use symbols as keys:**

- **No name collisions** — safe for adding metadata to objects you don't own.
- **Hidden from ordinary enumeration** — skipped by `for...in`, `Object.keys`, `JSON.stringify` (accessible via `Object.getOwnPropertySymbols`).

**Well-known symbols** customize built-in behavior:

```js
class Range {
  constructor(start, end) {
    this.start = start;
    this.end = end;
  }
  *[Symbol.iterator]() {
    // makes it iterable
    for (let i = this.start; i <= this.end; i++) yield i;
  }
}
[...new Range(1, 3)]; // [1, 2, 3]
```

Others: `Symbol.asyncIterator`, `Symbol.toPrimitive`, `Symbol.hasInstance`.

**Global registry:** `Symbol.for("key")` returns a shared symbol across the app.

**Key point:** symbols are unique primitives used as collision-free, non-enumerable object keys (great for metadata), and well-known symbols like `Symbol.iterator` hook into built-in language behavior; `Symbol.for` shares symbols via a global registry.
