# 13. How do you implement authentication? (Mid)

Authentication verifies **who** the user is. Two common approaches in Express APIs:

**1. JWT (stateless)** — the client sends a signed token per request:

```ts
import jwt from "jsonwebtoken";

// Login — issue a token
app.post("/login", async (req, res) => {
  const user = await verifyCredentials(req.body);
  const token = jwt.sign({ sub: user.id }, process.env.JWT_SECRET, {
    expiresIn: "15m",
  });
  res.json({ token });
});

// Guard middleware — verify on protected routes
function authGuard(req, res, next) {
  const header = req.headers.authorization ?? "";
  const token = header.replace("Bearer ", "");
  try {
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(401).json({ error: "Invalid token" });
  }
}

app.get("/me", authGuard, (req, res) => res.json(req.user));
```

**2. Sessions (stateful)** — `express-session` + a cookie; server stores session state (often in Redis).

**Notes:** JWTs scale statelessly but can't be easily revoked (use short expiry + refresh tokens); sessions are revocable but need shared storage when clustered.

**Key point:** use JWTs (stateless, verified in a guard middleware) or server sessions (stateful, revocable) — protect routes with an auth middleware that populates `req.user`, and weigh revocation vs scalability.
