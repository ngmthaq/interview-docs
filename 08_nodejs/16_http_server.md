# 16. How does a Node.js HTTP server work? (Mid)

The core **`http`** module creates a server without any framework. It's an `EventEmitter` that fires a callback per incoming request.

```ts
import http from "http";

const server = http.createServer((req, res) => {
  // req: IncomingMessage (Readable stream) — method, url, headers, body chunks
  // res: ServerResponse (Writable stream)
  if (req.url === "/health" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ status: "ok" }));
  } else {
    res.writeHead(404).end("Not Found");
  }
});

server.listen(3000, () => console.log("Listening on :3000"));
```

**Key ideas:**

- `req` is a **readable stream** — a request body (POST/PUT) arrives as `data` chunks you must collect.
- `res` is a **writable stream** — `writeHead` sets status/headers, `end` sends the body.
- Frameworks like **Express** wrap this with routing, middleware, and body parsing.

**Key point:** `http.createServer` handles each request via a callback where `req`/`res` are streams; Express and friends are conveniences layered on top of this same core API.
