# 21. What is the middleware pattern? (Junior)

**Middleware** are functions that sit in a **pipeline**, each receiving the request/response and a `next` callback to pass control along. It's how Express (and Koa, Connect) compose cross-cutting logic.

```ts
import express from "express";
const app = express();

// Logger middleware — runs for every request
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next(); // hand off to the next middleware/route
});

// Auth guard — can short-circuit the chain
function requireAuth(req, res, next) {
  if (!req.headers.authorization) return res.status(401).end();
  next();
}

app.get("/profile", requireAuth, (req, res) => res.json({ user: "me" }));
```

**Key ideas:**

- Each middleware either **calls `next()`** (continue) or **ends the response** (short-circuit).
- Order matters — they run top to bottom in registration order.
- **Error middleware** has 4 args `(err, req, res, next)` and catches errors passed via `next(err)`.

**Key point:** middleware is a chain of `(req, res, next)` functions for cross-cutting concerns (logging, auth, parsing); each one continues with `next()` or terminates the request, and order of registration defines execution order.
