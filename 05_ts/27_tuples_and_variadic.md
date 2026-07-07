# 27. Tuple types and variadic tuples. (Senior)

A **tuple** is a fixed-length array with a known type per position.

```ts
type Point = [number, number];
const p: Point = [10, 20];

// Labeled tuples (documentation only)
type RGB = [red: number, green: number, blue: number];

// Optional and rest elements
type Args = [name: string, age?: number, ...rest: string[]];
```

**Named use case — `useState`-style returns:**

```ts
function useToggle(): [boolean, () => void] {
  const [state, setState] = [false, () => {}];
  return [state, setState];
}
const [on, toggle] = useToggle(); // typed positionally
```

**Variadic tuples** — spread type parameters for flexible, typed composition:

```ts
// Type-safe concat that preserves element types
function concat<T extends unknown[], U extends unknown[]>(a: [...T], b: [...U]): [...T, ...U] {
  return [...a, ...b];
}

const result = concat([1, 2], ["a", "b"]);
// type: [number, number, string, string]
```

Variadic tuples power typing for `curry`, `bind`, and function-argument manipulation (`Parameters<T>`).

**Key point:** tuples fix length and per-position types (with optional/rest/labeled elements); variadic tuples (`[...T, ...U]`) spread type parameters to preserve exact element types through composition — enabling precise typing of concat, curry, and argument-forwarding utilities.
