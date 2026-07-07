# 6. What are generics? (Mid)

Generics let you write reusable code that is **parameterized over types** — preserving the type relationship between input and output instead of falling back to `any`.

```ts
function identity<T>(value: T): T {
  return value;
}
const n = identity(5); // T = number → n: number
const s = identity("hi"); // T = string → s: string
```

**Constraints** (`extends`) limit what `T` can be:

```ts
function longest<T extends { length: number }>(a: T, b: T): T {
  return a.length >= b.length ? a : b;
}
longest([1, 2], [1]); // ✅ arrays have length
longest(1, 2); // ❌ number has no length
```

**Generic interfaces / classes:**

```ts
interface Box<T> {
  value: T;
}
class Stack<T> {
  private items: T[] = [];
  push(x: T) {
    this.items.push(x);
  }
  pop(): T | undefined {
    return this.items.pop();
  }
}
```

**Default params:** `interface Box<T = string> { value: T }`.

**Why:** one implementation, many types, full type safety — no `any`, no casts.
