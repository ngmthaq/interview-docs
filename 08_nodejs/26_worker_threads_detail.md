# 26. How do worker_threads share data? (Senior)

**`worker_threads`** run JavaScript in parallel threads within one process. Communication happens by **message passing** or **shared memory**.

```ts
// main.ts
import { Worker } from "worker_threads";

const worker = new Worker("./worker.js", { workerData: { n: 40 } });
worker.on("message", (result) => console.log("fib =", result));

// worker.js
import { parentPort, workerData } from "worker_threads";
function fib(n) {
  return n < 2 ? n : fib(n - 1) + fib(n - 2);
}
parentPort.postMessage(fib(workerData.n)); // CPU work off the main thread
```

**Data transfer options:**

- **`postMessage(value)`** — clones the value (structured clone) between threads.
- **Transferables** — move an `ArrayBuffer` with zero copy (ownership transfers).
- **`SharedArrayBuffer`** — genuine shared memory both threads read/write (use `Atomics` for safe coordination).

**Practical notes:**

- Threads are **not free** — spawning has overhead; reuse a **worker pool** (e.g. `piscina`) for many tasks.
- Best for **CPU-bound** work (hashing, parsing, image processing), not I/O (the event loop already handles that well).

**Key point:** `worker_threads` parallelize CPU-bound work; exchange data via `postMessage` (cloned), transferable `ArrayBuffer`s (moved), or `SharedArrayBuffer` (shared) — and pool workers to amortize their startup cost.
