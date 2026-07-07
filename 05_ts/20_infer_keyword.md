# 20. The `infer` keyword? (Senior)

`infer` declares a **type variable inside a conditional type** to _capture_ a piece of another type — pattern matching at the type level. It only appears in the `extends` clause of a conditional type.

```ts
type ElementType<T> = T extends (infer U)[] ? U : never;
type A = ElementType<string[]>; // string
```

**Extract a function's return type** (this is how `ReturnType` works):

```ts
type MyReturn<T> = T extends (...args: any[]) => infer R ? R : never;
type R = MyReturn<() => number>; // number
```

**Extract the first argument:**

```ts
type FirstArg<T> = T extends (a: infer A, ...rest: any[]) => any ? A : never;
type F = FirstArg<(id: string) => void>; // string
```

**Recursive `infer`** — unwrap deeply nested structures:

```ts
type DeepAwait<T> = T extends Promise<infer U> ? DeepAwait<U> : T;
type X = DeepAwait<Promise<Promise<number>>>; // number
```

**Multiple `infer` in one pattern** — split a tuple:

```ts
type Head<T> = T extends [infer H, ...infer _] ? H : never;
type H = Head<[1, 2, 3]>; // 1
```

**Mental model:** `infer X` = "match here and bind whatever it is to `X`" — like a capture group in a regex.
