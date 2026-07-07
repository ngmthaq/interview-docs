# 19. What is connection pooling? (Mid)

Opening a new DB connection is **expensive** (TCP handshake, auth, setup). A **connection pool** keeps a set of open connections ready to **reuse**, handing them out to requests and returning them when done.

```ts
import { Pool } from "pg";

const pool = new Pool({ max: 20 }); // reuse up to 20 connections

async function getUser(id: number) {
  // borrows a connection from the pool, returns it automatically
  const res = await pool.query("SELECT * FROM users WHERE id=$1", [id]);
  return res.rows[0];
}
```

**Benefits:**

- Avoids per-request connection overhead → lower latency.
- **Caps** concurrent DB connections, protecting the DB from overload.

**Key settings:** pool size (`max`), idle timeout, acquire timeout.

**Watch out:** too-small a pool → requests queue and stall; too-large → the DB runs out of connections/memory. Size it to your DB's limits and workload, not arbitrarily high.
