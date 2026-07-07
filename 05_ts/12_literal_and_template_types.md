# 12. Literal types and template literal types? (Mid)

**Literal types** — a type that is one exact value, not the whole primitive:

```ts
let dir: "left" | "right"; // only these two strings
let flag: true; // only true
```

**Widening** — a `let` infers the wide type; `const` / `as const` keeps it narrow:

```ts
let a = "hi"; // string (widened)
const b = "hi"; // "hi" (literal)
let c = "hi" as const; // "hi"
```

**Template literal types** (TS 4.1+) — build string literal types from other types:

```ts
type Lang = "en" | "vi";
type Key = `t_${Lang}`; // "t_en" | "t_vi"

type Event = "click" | "hover";
type Handler = `on${Capitalize<Event>}`; // "onClick" | "onHover"
```

Combined with mapped types, this powers strongly-typed key transforms:

```ts
type EventHandlers<T extends string> = {
  [K in T as `on${Capitalize<K>}`]: () => void;
};
// EventHandlers<"click"> → { onClick: () => void }
```

Intrinsic string helpers: `Uppercase`, `Lowercase`, `Capitalize`, `Uncapitalize`.
