# 4. What are the req and res objects? (Fresher)

Every handler receives **`req`** (the incoming request) and **`res`** (the outgoing response). They wrap Node's raw `http.IncomingMessage`/`ServerResponse` with convenient helpers.

**Common `req` properties:**

```ts
req.params; // route params — /users/:id  → { id: "42" }
req.query; // query string — ?page=2      → { page: "2" }
req.body; // parsed body (needs express.json())
req.headers; // request headers
req.method; // "GET", "POST", ...
req.path; // URL path
```

**Common `res` methods:**

```ts
res.send("text or buffer"); // send a response
res.json({ ok: true }); // send JSON (sets Content-Type)
res.status(404).json({ ... }); // set status code (chainable)
res.redirect("/login"); // 302 redirect
res.set("X-Custom", "value"); // set a header
res.end(); // end with no body
```

**Key point:** `req` exposes input (`params`, `query`, `body`, `headers`) and `res` sends output (`json`, `send`, `status`, `redirect`) — methods are chainable (`res.status(201).json(...)`), and body parsing requires the `express.json()` middleware.
