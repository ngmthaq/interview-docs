# 23. What are database migrations? (Mid)

**Migrations** are versioned scripts that describe **incremental changes to the database schema** (add table, add column, create index). They keep every environment's schema in sync and under source control.

```ts
// Example migration (TypeORM style)
export class AddUserEmail1710000000000 {
  async up(q) {
    await q.query(`ALTER TABLE users ADD COLUMN email VARCHAR(255)`);
  }
  async down(q) {
    await q.query(`ALTER TABLE users DROP COLUMN email`);
  }
}
```

**Why they matter:**

- **Reproducible schema** across dev/staging/prod — no manual `ALTER TABLE` drift.
- **`up` / `down`** enable applying and rolling back changes.
- Teammates and CI apply the same ordered changes.

**Best practices:**

- Never edit an already-applied migration — write a new one.
- Make migrations **backward-compatible** for zero-downtime deploys (e.g. add column nullable first, backfill, then enforce NOT NULL).
- Keep data migrations separate from schema migrations when large.
