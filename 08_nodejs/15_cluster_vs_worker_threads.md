# 15. Cluster module vs worker_threads. (Mid)

Both add parallelism, but differ in **isolation and use case**.

**`cluster`** — forks multiple **processes** sharing a server port, each with its own event loop and memory. Scales I/O-bound apps across CPU cores.

```js
const cluster = require("cluster");
const os = require("os");

if (cluster.isPrimary) {
  os.cpus().forEach(() => cluster.fork()); // one worker per core
} else {
  require("./server"); // each worker runs the HTTP server
}
```

**`worker_threads`** — multiple **threads** inside one process, able to **share memory** (`SharedArrayBuffer`). Best for CPU-bound work.

| | cluster | worker_threads |
| --- | --- | --- |
| Unit | Process | Thread |
| Memory | Isolated | Can share |
| Best for | Scaling I/O across cores | CPU-heavy computation |
| Communication | IPC messages | `postMessage` / shared memory |

**Note:** in production, a process manager (PM2) or the platform (Kubernetes) often replaces manual `cluster` usage.

**Key point:** use `cluster` (or PM2) to scale I/O-bound servers across cores as separate processes, and `worker_threads` for CPU-bound tasks needing shared memory within one process.
