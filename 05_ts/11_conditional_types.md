# 11. Conditional types? (Senior)

A conditional type chooses between two types based on a relationship — a ternary at the type level:

```ts
type IsString<T> = T extends string ? "yes" : "no";
type A = IsString<string>; // "yes"
type B = IsString<number>; // "no"
```

**Distributive** over unions — when the checked type is a naked type parameter, it applies to each member:

```ts
type ToArray<T> = T extends any ? T[] : never;
type R = ToArray<string | number>; // string[] | number[]
```

Wrap in `[]` to **disable** distribution: `type X<T> = [T] extends [any] ? ... : ...`.

**With `infer`** — extract a type from within another:

```ts
type ElementType<T> = T extends (infer U)[] ? U : T;
type E = ElementType<number[]>; // number
```

**Real-world** — recursively unwrap nested promises:

```ts
type Unwrap<T> = T extends Promise<infer U> ? Unwrap<U> : T;
type U = Unwrap<Promise<Promise<string>>>; // string
```

Many built-ins are conditional types: `NonNullable`, `ReturnType`, `Extract`, `Exclude`.
