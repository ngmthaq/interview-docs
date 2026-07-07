# 6. Explain the Node.js event loop phases. (Junior)

The event loop (via **libuv**) processes callbacks in ordered **phases**, looping while there is work.

**Main phases (in order):**

1. **Timers** — `setTimeout` / `setInterval` callbacks whose time elapsed.
2. **Pending callbacks** — some deferred system/I/O callbacks.
3. **Poll** — retrieve new I/O events; execute I/O callbacks (the loop often waits here).
4. **Check** — `setImmediate` callbacks.
5. **Close callbacks** — e.g. `socket.on("close")`.

**Between every phase**, Node drains the **microtask queues**: `process.nextTick` first, then Promise callbacks.

```js
setTimeout(() => console.log("timeout"), 0);
setImmediate(() => console.log("immediate"));
Promise.resolve().then(() => console.log("promise"));
process.nextTick(() => console.log("nextTick"));

// Typical order: nextTick, promise, timeout, immediate
```

**Key point:** the loop runs phases (timers → poll → check → …) and flushes microtasks (`nextTick` > Promises) between each phase, which is why microtasks always beat `setTimeout`/`setImmediate`.
