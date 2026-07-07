# 12. Synchronous vs asynchronous fs methods. (Junior)

Node's `fs` module offers **blocking** and **non-blocking** variants of most operations.

```js
const fs = require("fs");

// Synchronous — BLOCKS the event loop until done
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);

// Asynchronous callback — non-blocking
fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});

// Async promise (modern) — non-blocking + async/await
const { readFile } = require("fs/promises");
const data2 = await readFile("file.txt", "utf8");
```

**When to use which:**

- **Sync (`*Sync`)** — fine at **startup** (loading config once) before the server accepts traffic. Never in a request handler.
- **Async** — always in a running server; a sync call blocks the **single thread**, freezing all concurrent requests.

**Key point:** `*Sync` methods block the entire event loop, so restrict them to startup/CLI scripts; use the promise-based `fs/promises` API inside servers to stay non-blocking.
