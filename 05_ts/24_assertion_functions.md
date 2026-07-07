# 24. What are assertion functions (`asserts`)? (Senior)

An **assertion function** uses the **`asserts`** return annotation to tell TypeScript that, if the function returns (doesn't throw), a condition holds — narrowing the type from that point on.

```ts
function assert(condition: unknown, msg?: string): asserts condition {
  if (!condition) throw new Error(msg);
}

function process(value: string | null) {
  assert(value !== null, "value is required");
  value.toUpperCase(); // ✅ narrowed to string after the assert
}
```

**Asserting a specific type** with `asserts x is T`:

```ts
function assertIsString(val: unknown): asserts val is string {
  if (typeof val !== "string") throw new Error("Not a string");
}

function handle(input: unknown) {
  assertIsString(input);
  input.trim(); // ✅ input is now string
}
```

**Assertion functions vs type guards:**

- A **type guard** (`x is T`) returns `boolean` — you branch on it (`if (isX(v))`).
- An **assertion function** (`asserts x is T`) **throws** on failure — narrowing continues linearly afterward, no `if` needed.

**Key point:** assertion functions annotated with `asserts condition` or `asserts x is T` narrow types by throwing on failure — unlike boolean type guards, they let subsequent code assume the condition, ideal for invariant/precondition checks.
