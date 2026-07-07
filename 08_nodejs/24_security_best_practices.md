# 24. What are key Node.js security best practices? (Senior)

Server-side JS exposes real attack surface — here are the essentials.

**Input & injection:**

- **Validate/sanitize** all input (`zod`, `joi`); never build SQL with string concatenation — use **parameterized queries**.
- Avoid `eval`, and never pass user input to `child_process.exec` (command injection).

**Dependencies:**

- Run **`npm audit`** and tools like Snyk; keep deps patched (most Node vulnerabilities come from the dependency tree).
- Commit `package-lock.json`; beware typosquatting.

**HTTP hardening:**

- Use **`helmet`** to set secure headers; enforce **HTTPS**.
- Apply **rate limiting** and body-size limits to resist DoS.
- Configure **CORS** explicitly, not `*` for authenticated APIs.

**Secrets & auth:**

- Keep secrets in env/secret managers, never in code.
- Hash passwords with **bcrypt/argon2**; sign tokens with strong secrets and short expiry.
- Run the process as a **non-root** user.

```js
const helmet = require("helmet");
app.use(helmet());
app.use(express.json({ limit: "100kb" })); // cap payload size
```

**Key point:** validate input, use parameterized queries, audit and pin dependencies, harden HTTP with helmet/rate-limiting, keep secrets out of code, and hash passwords properly — most real-world Node breaches are injection or vulnerable dependencies.
