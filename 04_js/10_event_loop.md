# 10. Explain the event loop. (Mid)

JavaScript is **single-threaded** but non-blocking. The **event loop** coordinates running code, handling async callbacks without blocking.

**Components:**

- **Call stack** — where functions execute (one at a time).
- **Web/Node APIs** — handle async work (timers, fetch, I/O) off the stack.
- **Task queues** — completed callbacks wait here.
- **Event loop** — when the stack is empty, it pushes the next queued callback onto the stack.

```js
console.log("1");
setTimeout(() => console.log("2"), 0); // async → queued
console.log("3");
// Output: 1, 3, 2
```

`setTimeout`'s callback waits in the queue until the synchronous code finishes — even with `0ms`.

**Microtasks vs macrotasks:**

- **Microtasks** (Promises, `queueMicrotask`) run **before** the next macrotask.
- **Macrotasks** (`setTimeout`, I/O, events) run one per loop tick.

**Key point:** sync code runs first, then all microtasks drain, then one macrotask — repeat. This is why Promises resolve before `setTimeout(…, 0)`.
