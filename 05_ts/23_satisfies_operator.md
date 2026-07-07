# 23. What is the `satisfies` operator? (Mid)

**`satisfies`** (TS 4.9+) checks that a value **conforms to a type** without **widening** it — you keep the precise inferred type while still validating the constraint. It's the best of both `: Type` and `as const`.

```ts
type Config = Record<string, string | number>;

// With a type annotation — value is widened to the annotation
const a: Config = { port: 3000, host: "localhost" };
a.port.toFixed(); // ❌ error — port is `string | number`, not number

// With satisfies — validated AND keeps precise inferred types
const b = { port: 3000, host: "localhost" } satisfies Config;
b.port.toFixed(); // ✅ port inferred as number
b.host.toUpperCase(); // ✅ host inferred as string
```

**Why it matters:**

- `: Type` **validates** but **widens** — you lose the specific literal/member types.
- `satisfies` **validates** the shape yet **preserves** what you actually wrote.

```ts
const palette = {
  primary: "#ff0000",
  secondary: "#00ff00",
} satisfies Record<string, string>;
// keys keep exact names; values keep string type — and typos are caught
```

**Key point:** `satisfies` validates a value against a type without widening it, so you get both compile-time checking of the constraint and the precise inferred types (literals, exact keys) — use it for config/palette objects where `: Type` would erase useful specificity.
