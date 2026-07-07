# 13. What is libuv and the thread pool? (Mid)

**libuv** is the C library that gives Node its **event loop** and **asynchronous I/O**. Although JavaScript runs on one thread, libuv maintains a **thread pool** (default **4 threads**) to run certain blocking operations in the background.

**What uses the thread pool:**

- File system operations (`fs`).
- DNS lookups (`dns.lookup`).
- CPU-bound crypto (`crypto.pbkdf2`, `crypto.randomBytes`).
- Compression (`zlib`).

**What does NOT** (handled by the OS kernel, not the pool): network I/O — TCP/UDP/HTTP sockets use efficient OS mechanisms (epoll/kqueue).

```js
// Increase the pool size before any async work
process.env.UV_THREADPOOL_SIZE = "8";

const crypto = require("crypto");
for (let i = 0; i < 8; i++) {
  crypto.pbkdf2("pw", "salt", 100000, 64, "sha512", () => {
    console.log(`Hash ${i} done`); // parallelism limited by pool size
  });
}
```

**Key point:** libuv drives the event loop and offloads file/crypto/DNS/zlib work to a 4-thread pool (tunable via `UV_THREADPOOL_SIZE`), while network I/O uses the OS directly — this is how single-threaded Node achieves concurrency.
