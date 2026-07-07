# 5. What are the key global objects in Node.js? (Fresher)

Node provides globals available in every module without importing.

- **`process`** — info about and control over the current process (env, args, exit).
- **`__dirname` / `__filename`** — absolute path of the current directory/file (CommonJS only).
- **`global`** / **`globalThis`** — the global namespace (like `window` in browsers).
- **`Buffer`** — handle raw binary data.
- **`console`**, **`setTimeout`**, **`setInterval`** — familiar utilities.

```js
console.log(process.argv); // CLI arguments
console.log(process.env.NODE_ENV); // environment variable
console.log(__dirname); // this file's folder

process.on("exit", (code) => {
  console.log(`Exiting with code ${code}`);
});
```

**`module`** and **`require`** are technically module-scoped (not truly global) but always available in CommonJS.

**Key point:** `process`, `Buffer`, `__dirname`, and `globalThis` are the everyday globals — `process` especially is the gateway to env vars, CLI args, and lifecycle events.
