# 1. What is Express.js? (Fresher)

**Express** is a minimal, unopinionated **web framework for Node.js**. It sits on top of the core `http` module and adds **routing**, **middleware**, and helpers for requests/responses — so you don't hand-write low-level server code.

```ts
import express from "express";

const app = express();

app.get("/", (req, res) => {
  res.send("Hello, Express!");
});

app.listen(3000, () => console.log("Listening on :3000"));
```

**What Express gives you over raw `http`:**

- **Routing** — map HTTP method + path to handlers (`app.get`, `app.post`, …).
- **Middleware pipeline** — compose reusable request-processing functions.
- **Convenience** — `res.json()`, `res.status()`, `req.params`, `req.query`, body parsing.

**Unopinionated** means Express doesn't dictate project structure, ORM, or folder layout — you choose. Frameworks like **NestJS** add that structure on top.

**Key point:** Express is a thin, flexible layer over Node's `http` module providing routing and middleware — the de-facto standard for building Node web servers and REST APIs.
