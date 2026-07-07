# 13. What is a deadlock and how do you avoid it? (Mid → Senior)

A **deadlock** happens when two transactions each hold a lock the other needs, so both wait forever.

```
Tx A: locks row 1 → wants row 2
Tx B: locks row 2 → wants row 1
→ circular wait = deadlock
```

```sql
-- Transaction A
BEGIN; UPDATE accounts SET ... WHERE id = 1; -- locks 1
       UPDATE accounts SET ... WHERE id = 2; -- waits for B

-- Transaction B (concurrently)
BEGIN; UPDATE accounts SET ... WHERE id = 2; -- locks 2
       UPDATE accounts SET ... WHERE id = 1; -- waits for A
```

**How DBs handle it:** they detect the cycle and **kill one transaction** (a "deadlock victim"), which must retry.

**How to avoid:**

- **Consistent lock ordering** — always access rows in the same order (e.g. by ascending id).
- Keep transactions **short**.
- Use lower isolation where safe; reduce lock scope.
- Add **retry logic** for the victim.
