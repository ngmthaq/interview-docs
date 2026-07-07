# 1. What is Node.js? (Fresher)

**Node.js** is a runtime that lets you run JavaScript **outside the browser**, built on Chrome's **V8** engine plus the **libuv** library for async I/O.

**Key characteristics:**

- **Single-threaded** event loop for JS, with a background thread pool (libuv) for I/O.
- **Non-blocking / asynchronous** I/O — great for network- and I/O-heavy apps.
- **Cross-platform** and package-rich via **npm**.

```js
// hello.js — run with: node hello.js
const os = require("os");
console.log(`Running on ${os.platform()} with Node ${process.version}`);
```

**Good fit:** APIs, real-time apps (chat, streaming), microservices.
**Poor fit:** heavy CPU-bound work (image/video processing, crypto mining) that blocks the single thread.

**Key point:** Node.js = V8 (runs JS) + libuv (async I/O) + core libraries, enabling server-side JavaScript with a non-blocking, event-driven model.
