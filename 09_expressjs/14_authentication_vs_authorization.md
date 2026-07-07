# 14. Authentication vs authorization in Express. (Mid)

- **Authentication** = _who are you?_ (verify identity — login, token).
- **Authorization** = _what are you allowed to do?_ (check permissions — roles, ownership).

They're separate middleware layers that run in order:

```ts
// 1. Authentication — identify the user
function authGuard(req, res, next) {
  const user = verifyToken(req);
  if (!user) return res.status(401).json({ error: "Unauthenticated" });
  req.user = user;
  next();
}

// 2. Authorization — check role/permission
function requireRole(role: string) {
  return (req, res, next) => {
    if (req.user.role !== role) {
      return res.status(403).json({ error: "Forbidden" });
    }
    next();
  };
}

app.delete("/users/:id", authGuard, requireRole("admin"), deleteUser);
```

**Status codes matter:**

- **401 Unauthorized** — not authenticated (missing/invalid credentials).
- **403 Forbidden** — authenticated but not permitted.

**Key point:** authentication (who you are, 401) precedes authorization (what you may do, 403); implement them as separate ordered middleware so identity is established before permissions are checked.
