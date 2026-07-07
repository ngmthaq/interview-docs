# 18. What is the child_process module? (Mid)

**`child_process`** spawns **separate OS processes** to run system commands or other scripts, enabling parallel work outside the main event loop.

**Four methods:**

- **`spawn`** — streams output; best for **large/continuous** output or long-running processes.
- **`exec`** — buffers output into a callback; convenient for **short** commands (⚠️ shell injection risk, buffer size limit).
- **`execFile`** — like `exec` but runs a file directly (no shell — safer).
- **`fork`** — special case that spawns a **new Node process** with an IPC channel for messaging.

```js
const { spawn } = require("child_process");

const ls = spawn("ls", ["-lh", "/usr"]);
ls.stdout.on("data", (chunk) => console.log(`out: ${chunk}`));
ls.stderr.on("data", (chunk) => console.error(`err: ${chunk}`));
ls.on("close", (code) => console.log(`exited with ${code}`));
```

⚠️ Avoid passing **user input** to `exec` (shell injection). Prefer `execFile`/`spawn` with an args array.

**Key point:** `child_process` runs external commands or Node scripts in separate processes — use `spawn` for streaming, `fork` for Node-to-Node IPC, and avoid `exec` with untrusted input.
