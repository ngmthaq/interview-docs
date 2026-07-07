# 3. CommonJS vs ES Modules in Node.js. (Fresher)

Two module systems Node supports for splitting code into files.

**CommonJS (CJS)** — the classic Node system:

```js
// math.js
function add(a, b) {
  return a + b;
}
module.exports = { add };

// app.js
const { add } = require("./math");
```

**ES Modules (ESM)** — the standard JavaScript syntax:

```js
// math.mjs
export function add(a, b) {
  return a + b;
}

// app.mjs
import { add } from "./math.mjs";
```

**Differences:**

- `require`/`module.exports` (CJS) vs `import`/`export` (ESM).
- CJS loads **synchronously**; ESM is **async** and statically analyzable (enables tree-shaking).
- Enable ESM via `.mjs`, or `"type": "module"` in `package.json`.
- `__dirname`/`__filename` exist in CJS; in ESM use `import.meta.url`.

**Key point:** CommonJS is Node's original synchronous system; ES Modules are the modern standard with static imports — pick one per project via `package.json` `"type"`.
