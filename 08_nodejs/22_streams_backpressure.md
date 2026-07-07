# 22. What is backpressure in streams? (Mid)

**Backpressure** is the mechanism that stops a fast **producer** from overwhelming a slow **consumer**, preventing unbounded memory growth.

```js
// PROBLEM — ignoring the return value of write()
readable.on("data", (chunk) => {
  writable.write(chunk); // if buffer fills, data piles up in memory
});

// write() returns false when the internal buffer is full:
readable.on("data", (chunk) => {
  const ok = writable.write(chunk);
  if (!ok) {
    readable.pause(); // stop reading
    writable.once("drain", () => readable.resume()); // resume when flushed
  }
});
```

**The easy way** — `pipe`/`pipeline` handle backpressure automatically:

```js
const { pipeline } = require("stream/promises");
await pipeline(readable, writable); // pausing/resuming managed for you
```

**How it works:** each stream has a `highWaterMark` buffer threshold. When exceeded, `write()` returns `false`, signaling the source to pause until the `drain` event fires.

**Key point:** backpressure keeps producer and consumer in sync via `write()` returning `false` and the `drain` event — always use `pipeline`/`pipe` (which manage it automatically) instead of manually piping `data` chunks.
