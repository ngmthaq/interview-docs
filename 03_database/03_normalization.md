# 3. What is normalization? (Fresher → Junior)

**Normalization** is organizing tables to **reduce data redundancy** and avoid update anomalies, by splitting data into related tables.

**Un-normalized (redundant):**

```
orders(id, customer_name, customer_email, product, price)
-- customer_name/email repeated on every order → update anomalies
```

**Normalized:**

```sql
customers(id, name, email)
orders(id, customer_id, product, price) -- reference, no duplication
```

**Normal forms (common ones):**

- **1NF** — atomic values, no repeating groups.
- **2NF** — 1NF + no partial dependency on part of a composite key.
- **3NF** — 2NF + no non-key column depends on another non-key column.

**Benefits:** less duplication, consistent data, smaller storage.
**Trade-off:** more joins → sometimes we **denormalize** for read performance (see later question).
