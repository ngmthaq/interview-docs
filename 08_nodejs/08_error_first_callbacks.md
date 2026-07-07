# 8. What is the error-first callback pattern? (Junior)

Node's classic async convention: the callback's **first argument is an error** (or `null`), and results follow.

```js
const fs = require("fs");

fs.readFile("config.json", "utf8", (err, data) => {
  if (err) {
    console.error("Failed to read:", err.message);
    return; // always return after handling the error
  }
  console.log("Contents:", data);
});
```

**Rules:**

- Check `err` first; bail out early if it exists.
- On success, `err` is `null`/`undefined` and the data arguments are populated.
- Never throw inside async callbacks expecting a `try/catch` around the call to catch it — the stack has already unwound.

**Modern alternative** — promisify for `async/await`:

```js
const { readFile } = require("fs/promises");
const data = await readFile("config.json", "utf8"); // throws on error → try/catch
```

**Key point:** error-first callbacks `(err, result) => …` were Node's original async pattern; today `fs/promises` + `async/await` is preferred, but you must recognize the callback style in legacy code and libraries.
