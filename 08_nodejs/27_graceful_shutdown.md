# 27. How do you implement graceful shutdown? (Senior)

**Graceful shutdown** finishes in-flight requests and releases resources before exiting, instead of dropping connections. Essential in containerized/orchestrated environments.

```ts
const server = app.listen(3000);

async function shutdown(signal: string) {
  console.log(`${signal} received — shutting down`);

  // 1. Stop accepting new connections; finish existing ones
  server.close(async () => {
    // 2. Close resources: DB pools, message queues, etc.
    await db.end();
    await redis.quit();
    console.log("Cleanup done");
    process.exit(0);
  });

  // 3. Force-exit if cleanup hangs
  setTimeout(() => {
    console.error("Forced shutdown");
    process.exit(1);
  }, 10_000).unref();
}

process.on("SIGTERM", () => shutdown("SIGTERM")); // sent by Docker/K8s
process.on("SIGINT", () => shutdown("SIGINT")); // Ctrl+C
```

**Why it matters:**

- Kubernetes sends **`SIGTERM`**, then **`SIGKILL`** after a grace period — handle SIGTERM to drain cleanly.
- Prevents dropped requests, corrupted writes, and connection leaks during deploys/scaling.
- Always add a **timeout fallback** so a stuck cleanup can't hang forever.

**Key point:** on `SIGTERM`/`SIGINT`, stop accepting new work, let in-flight requests finish, close DB/cache/queue connections, and force-exit after a timeout — this makes rolling deploys and autoscaling zero-downtime.
