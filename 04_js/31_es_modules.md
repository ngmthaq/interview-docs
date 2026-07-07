# 31. How do ES Modules (import/export) work? (Junior)

**ES Modules (ESM)** are JavaScript's standard module system — each file is its own scope, sharing code via `export`/`import`.

**Named exports** — many per file, imported by name:

```js
// utils.js
export function add(a, b) {
  return a + b;
}
export const PI = 3.14;

// app.js
import { add, PI } from "./utils.js";
import { add as sum } from "./utils.js"; // rename
import * as utils from "./utils.js"; // namespace
```

**Default export** — one per file:

```js
// User.js
export default class User {}

// app.js
import User from "./User.js"; // any name, no braces
```

**Key characteristics:**

- **Static** — imports are resolved at parse time (enabling tree-shaking); they're **hoisted**.
- **Live bindings** — imported values reflect later changes in the exporting module (unlike a copied value).
- **Strict mode** and **module scope** by default (no leaking to global).
- **Dynamic import** — `const mod = await import("./x.js")` loads on demand (code splitting).

**Key point:** ESM uses static, hoisted `import`/`export` (named or default) with live bindings and per-file scope, enabling tree-shaking; use `import()` for on-demand dynamic loading — the modern standard over CommonJS `require`.
