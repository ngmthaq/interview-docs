# 15. How do you handle CORS in Express? (Mid)

**CORS** (Cross-Origin Resource Sharing) is a browser security mechanism that blocks requests from a different **origin** (protocol + host + port) unless the server opts in with response headers.

```ts
import cors from "cors";

// Allow all origins (fine for public APIs, risky for authenticated ones)
app.use(cors());

// Restrict to specific origins (recommended)
app.use(
  cors({
    origin: ["https://app.example.com", "https://admin.example.com"],
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true, // allow cookies/Authorization
  }),
);
```

**Key concepts:**

- CORS is enforced by the **browser**, not the server — server-to-server calls are unaffected.
- **Preflight** — for non-simple requests the browser first sends an `OPTIONS` request; the `cors` middleware answers it automatically.
- With `credentials: true`, you **cannot** use `origin: "*"` — you must specify exact origins.

**Key point:** CORS is a browser-enforced policy; use the `cors` middleware to whitelist specific origins/methods, handle preflight `OPTIONS` automatically, and remember that `credentials: true` requires explicit origins (no wildcard).
