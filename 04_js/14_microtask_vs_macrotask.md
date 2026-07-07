# 14. Microtasks vs macrotasks? (Senior)

The event loop has **two queues** with different priorities.

- **Microtasks** — Promise callbacks (`.then`), `queueMicrotask`, `await` continuations, `MutationObserver`.
- **Macrotasks** — `setTimeout`, `setInterval`, `setImmediate`, I/O, UI events.

**Rule:** after each macrotask (and the initial script), the engine **drains the ENTIRE microtask queue** before the next macrotask.

```js
console.log("1");
setTimeout(() => console.log("2"), 0); // macrotask
Promise.resolve().then(() => console.log("3")); // microtask
console.log("4");

// Output: 1, 4, 3, 2
```

Order explained:

1. Sync: `1`, `4`.
2. Microtasks drain: `3`.
3. Next macrotask: `2`.

**Gotcha — microtask starvation:**

```js
function loop() {
  Promise.resolve().then(loop);
} // hogs the loop, blocks timers/rendering
```

**Key point:** microtasks always run before the next macrotask. This is why a resolved Promise beats `setTimeout(…, 0)`, and why chaining too many microtasks can starve rendering.
