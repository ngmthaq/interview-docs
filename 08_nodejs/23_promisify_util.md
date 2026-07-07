# 23. How do you convert callbacks to promises? (Mid)

Legacy Node APIs use error-first callbacks. **`util.promisify`** wraps them into promise-returning functions for `async/await`.

```ts
import { promisify } from "util";
import fs from "fs";

// Turn callback-style readFile into a promise
const readFileAsync = promisify(fs.readFile);
const data = await readFileAsync("file.txt", "utf8");
```

**Manual promisification** (for full control):

```ts
function delay(ms: number): Promise<void> {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
```

**Notes:**

- Many core modules already ship promise versions — prefer `fs/promises`, `dns/promises`, `stream/promises` over promisifying yourself.
- `promisify` expects the **error-first** signature `(err, result)`; non-standard callbacks need a custom wrapper or `promisify.custom`.
- The reverse — `util.callbackify` — turns an async function back into a callback style.

**Key point:** `util.promisify` adapts error-first callback APIs to promises for `async/await`; check for a built-in `*/promises` module first, and hand-roll a `new Promise` wrapper only for non-standard callback signatures.
