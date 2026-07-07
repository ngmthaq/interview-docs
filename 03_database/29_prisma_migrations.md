# 29. How do Prisma migrations work? (Junior)

**Prisma Migrate** turns changes to `schema.prisma` into **SQL migration files** that version your database schema.

**Development workflow:**

```bash
# After editing schema.prisma, create + apply a migration
npx prisma migrate dev --name add_user_role
```

This: (1) generates a timestamped SQL migration in `prisma/migrations/`, (2) applies it to the dev DB, and (3) regenerates Prisma Client.

**Production deployment:**

```bash
npx prisma migrate deploy   # applies pending migrations, no prompts
```

**Other commands:**

- **`prisma migrate reset`** — drop and recreate the DB, re-apply all migrations (dev only).
- **`prisma db push`** — sync schema to DB **without** a migration file (prototyping only — no history).
- **`prisma generate`** — regenerate the client after schema changes.
- **`prisma migrate status`** — show applied/pending migrations.

**Key distinctions:**

- **`migrate dev`** (development) generates history + applies; **`migrate deploy`** (CI/prod) only applies committed migrations.
- **`db push`** is for rapid prototyping — it doesn't create migration files, so avoid it once you need a migration history.

**Key point:** `prisma migrate dev` creates and applies versioned SQL migrations during development, while `prisma migrate deploy` applies committed migrations in production/CI; use `db push` only for prototyping (no history), and `prisma generate` to refresh the client.
