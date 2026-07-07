# 7. process.nextTick vs setImmediate vs setTimeout. (Junior)

All three defer work, but run at different points in the loop.

- **`process.nextTick(cb)`** — runs **before** the event loop continues, after the current operation. Highest priority (a microtask, drained before Promises even).
- **`setImmediate(cb)`** — runs in the **check** phase, after the poll phase completes.
- **`setTimeout(cb, 0)`** — runs in the **timers** phase after the minimum delay elapses.

```js
console.log("start");
setImmediate(() => console.log("immediate"));
setTimeout(() => console.log("timeout"), 0);
process.nextTick(() => console.log("nextTick"));
Promise.resolve().then(() => console.log("promise"));
console.log("end");

// start, end, nextTick, promise, timeout, immediate
```

⚠️ **Overusing `process.nextTick`** can starve the event loop — its queue is fully drained before I/O runs, so recursive `nextTick` calls block everything.

**Key point:** `nextTick` (and Promises) fire before the loop proceeds; `setImmediate` fires in the check phase; `setTimeout(…, 0)` in the timers phase — nextTick has the highest priority and must be used carefully.
