# 16. What are Express security best practices? (Mid)

Express is minimal, so security is **your** responsibility. Layer these defenses:

```ts
import helmet from "helmet";
import rateLimit from "express-rate-limit";

app.use(helmet()); // secure HTTP headers
app.use(express.json({ limit: "100kb" })); // cap body size
app.use(
  rateLimit({ windowMs: 60_000, max: 100 }), // throttle abuse
);
app.disable("x-powered-by"); // hide Express fingerprint
```

**Checklist:**

- **`helmet`** — sets headers (CSP, HSTS, X-Frame-Options, etc.).
- **Rate limiting** — resist brute-force and DoS.
- **Input validation** — Zod/Joi; parameterized DB queries (no SQL injection).
- **CORS** — whitelist origins, don't blanket-allow.
- **HTTPS** — terminate TLS (proxy or Node).
- **Secrets** in env vars; hash passwords with **bcrypt/argon2**.
- **Body-size limits** and avoid leaking stack traces in production error responses.
- Keep **dependencies patched** (`npm audit`).

**Key point:** harden Express with helmet, rate limiting, input validation, parameterized queries, strict CORS, HTTPS, and hidden error internals — the framework won't secure itself, so apply these layers explicitly.
