# 10. Mapped types? (Senior)

A mapped type builds a new object type by **iterating over the keys** of another with `[K in ...]`. This is how `Partial`, `Readonly`, etc. are implemented.

```ts
type MyPartial<T> = {
  [K in keyof T]?: T[K];
};
type MyReadonly<T> = {
  readonly [K in keyof T]: T[K];
};
```

**Modifiers** — add or strip `readonly` / `?` with `+` / `-`:

```ts
type Mutable<T> = {
  -readonly [K in keyof T]: T[K]; // remove readonly
};
type Concrete<T> = {
  [K in keyof T]-?: T[K]; // remove optional
};
```

**Key remapping** with `as` (TS 4.1+) — rename or filter keys:

```ts
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};
type G = Getters<{ name: string }>; // { getName: () => string }
```

Return `never` in the `as` clause to **filter keys out**:

```ts
type RemoveId<T> = { [K in keyof T as K extends "id" ? never : K]: T[K] };
```
