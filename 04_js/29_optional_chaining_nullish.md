# 29. Optional chaining and nullish coalescing. (Junior)

Two ES2020 operators that make handling missing values safer and more concise.

**Optional chaining `?.`** — short-circuits to `undefined` instead of throwing when accessing a property of `null`/`undefined`:

```js
const city = user?.address?.city; // undefined if user or address is null/undefined
user?.save?.(); // call only if the method exists
arr?.[0]; // safe index access
```

**Nullish coalescing `??`** — returns the right side only when the left is **`null` or `undefined`** (not other falsy values):

```js
const port = config.port ?? 3000; // 3000 only if port is null/undefined
```

**Why `??` beats `||`:**

```js
const count = 0;
count || 10; // 10  ❌ (0 is falsy but valid)
count ?? 10; // 0   ✅ (only null/undefined trigger the fallback)
```

`||` falls back on **any falsy** value (`0`, `""`, `false`); `??` only on nullish — important when `0`/`""`/`false` are legitimate values.

**Key point:** `?.` safely accesses nested properties/methods, short-circuiting to `undefined` instead of throwing; `??` provides defaults only for `null`/`undefined` (unlike `||`, which also triggers on `0`/`""`/`false`) — use `??` when falsy-but-valid values matter.
