# 17. How do you handle errors globally in Node.js? (Mid)

Beyond local `try/catch`, Node exposes **process-level events** for errors that escape.

```js
// Synchronous errors never caught anywhere
process.on("uncaughtException", (err) => {
  console.error("Uncaught:", err);
  // State may be corrupt — log, then exit and let a supervisor restart
  process.exit(1);
});

// Rejected promises with no .catch
process.on("unhandledRejection", (reason) => {
  console.error("Unhandled rejection:", reason);
  process.exit(1);
});
```

**Best practices:**

- Treat `uncaughtException` as a **last resort** — the process is in an unknown state, so log and **restart** (via PM2/Kubernetes) rather than resuming.
- Prefer local handling: `try/catch` around `await`, `.catch()` on promises, and check `err` in callbacks.
- Distinguish **operational errors** (bad input, network failure — handle gracefully) from **programmer errors** (bugs — crash and fix).
- In Express, use an **error-handling middleware** `(err, req, res, next)`.

**Key point:** handle errors locally where possible; use `uncaughtException`/`unhandledRejection` only to log and gracefully exit, then rely on a process supervisor to restart — never keep serving from a corrupted state.
