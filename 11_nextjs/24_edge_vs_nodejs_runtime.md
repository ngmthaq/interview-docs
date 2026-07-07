# 24. Edge Runtime vs Node.js Runtime. (Senior)

Next.js can run server code in two runtimes, selectable per route/middleware.

|            | Node.js Runtime (default)                 | Edge Runtime                                 |
| ---------- | ----------------------------------------- | -------------------------------------------- |
| APIs       | Full Node.js (fs, crypto, native modules) | Limited Web APIs subset                      |
| Cold start | Slower                                    | Near-instant                                 |
| Location   | Regional server                           | Globally distributed (close to user)         |
| Best for   | DB access, heavy libs, Node APIs          | Lightweight auth, redirects, personalization |

```ts
// Opt a Route Handler into the edge
export const runtime = "edge"; // or "nodejs" (default)

export async function GET() {
  return new Response("Hello from the edge");
}
```

**Trade-offs:**

- **Edge** — low latency worldwide and fast cold starts, but **can't** use many Node APIs or large/native dependencies, and has execution limits.
- **Node.js** — full ecosystem access (Prisma, native modules), better for database-heavy work.
- **Middleware** runs on the Edge Runtime by default.

**Key point:** the Node.js runtime offers full APIs for DB/heavy work; the Edge Runtime gives globally-distributed low latency and fast cold starts but only a limited Web API subset — choose per route via `export const runtime`, defaulting to Node for data-heavy logic.
