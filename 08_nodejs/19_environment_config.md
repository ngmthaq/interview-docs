# 19. How do you manage environment variables and config? (Mid)

Environment variables keep **secrets and per-environment settings** out of source code (the 12-factor approach).

```js
// Read via process.env — always strings (or undefined)
const port = Number(process.env.PORT) || 3000;
const dbUrl = process.env.DATABASE_URL;

if (!dbUrl) {
  throw new Error("DATABASE_URL is required"); // fail fast at startup
}
```

**Loading `.env` files locally:**

```js
// Node 20.6+ has built-in support:  node --env-file=.env app.js
// Or the classic library:
require("dotenv").config(); // loads .env into process.env
```

**Best practices:**

- **Never commit** `.env` or secrets — add to `.gitignore`; provide a `.env.example`.
- **Validate** required vars at startup (e.g. with `zod`) and fail fast.
- Coerce types — `process.env` values are always **strings**.
- Use `NODE_ENV` (`development` / `production` / `test`) to toggle behavior.
- In production, inject secrets via the platform (Kubernetes secrets, Vault), not files.

**Key point:** store config in `process.env`, load `.env` locally (built-in `--env-file` or `dotenv`), never commit secrets, and validate + type-coerce required variables at startup so misconfiguration fails immediately.
