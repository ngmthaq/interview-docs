# 2. Primary key vs Foreign key? (Fresher)

- **Primary key (PK)** — uniquely identifies each row in a table. Cannot be null, must be unique.
- **Foreign key (FK)** — a column that references the PK of another table, creating a relationship and enforcing **referential integrity**.

```sql
CREATE TABLE users (
  id   SERIAL PRIMARY KEY,        -- primary key
  name TEXT NOT NULL
);

CREATE TABLE orders (
  id       SERIAL PRIMARY KEY,
  user_id  INT REFERENCES users(id), -- foreign key
  total    NUMERIC
);
```

**Key points:**

- A FK guarantees you can't insert an order for a non-existent user.
- A table has **one** PK (possibly composite), but can have **many** FKs.
- PKs are automatically indexed; FKs often should be indexed too for join performance.
