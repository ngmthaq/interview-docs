# 29. How do you work with paths and the file system safely? (Junior)

The **`path`** module builds cross-platform file paths, and **`fs`** performs file operations — combined carefully to avoid bugs and vulnerabilities.

```ts
import path from "path";
import { readFile } from "fs/promises";

// Cross-platform join (handles / vs \ separators)
const configPath = path.join(__dirname, "config", "app.json");

// Useful helpers
path.basename("/a/b/c.txt"); // "c.txt"
path.extname("c.txt"); // ".txt"
path.resolve("src", "index.js"); // absolute from cwd
```

**Path-traversal safety** — never trust user input in a path:

```ts
const base = "/var/uploads";
const requested = path.join(base, req.params.file);

// Ensure the resolved path stays inside base — blocks "../../etc/passwd"
if (!path.resolve(requested).startsWith(path.resolve(base))) {
  throw new Error("Invalid path");
}
```

**Notes:**

- Use `path.join`/`resolve` — never concatenate with `"/"` manually (breaks on Windows).
- Check existence with `fs.access` or handle the error; avoid the race-prone `fs.exists`.
- Prefer `fs/promises` for async operations in servers.

**Key point:** use `path.join`/`resolve` for portable paths, and always validate that user-supplied paths resolve **inside** an allowed base directory to prevent path-traversal attacks.
