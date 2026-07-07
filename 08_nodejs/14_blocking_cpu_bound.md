# 14. How do you handle CPU-bound / blocking work? (Mid)

Because JS runs on **one thread**, a long synchronous computation blocks the event loop — every other request stalls until it finishes.

```js
// BAD — blocks the loop for seconds
app.get("/report", (req, res) => {
  const result = crunchHugeDataset(); // synchronous, CPU-heavy
  res.json(result); // nothing else runs meanwhile
});
```

**Solutions:**

- **`worker_threads`** — run CPU work on a separate thread (best for in-process parallelism).
- **`child_process` / `cluster`** — separate processes.
- **Offload** to a queue + background service (BullMQ, a separate worker).
- **Chunk** the work and yield with `setImmediate` so I/O callbacks can interleave.

```ts
import { Worker } from "worker_threads";

app.get("/report", (req, res) => {
  const worker = new Worker("./crunch-worker.js");
  worker.postMessage(req.query);
  worker.on("message", (result) => res.json(result)); // loop stays free
});
```

**Key point:** never run heavy CPU work on the main thread — offload it to `worker_threads`, child processes, or a job queue so the event loop keeps serving requests.
