# 10. What are transaction isolation levels? (Mid → Senior)

Isolation levels control **how much concurrent transactions can see each other's uncommitted work**, trading consistency for performance.

| Level                | Prevents                               |
| -------------------- | -------------------------------------- |
| **Read Uncommitted** | (nothing — allows dirty reads)         |
| **Read Committed**   | Dirty reads                            |
| **Repeatable Read**  | Dirty + non-repeatable reads           |
| **Serializable**     | Dirty + non-repeatable + phantom reads |

**The three anomalies:**

- **Dirty read** — reading another transaction's uncommitted change.
- **Non-repeatable read** — same row returns different values within one transaction.
- **Phantom read** — same query returns new rows because another transaction inserted.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN;
  SELECT SUM(balance) FROM accounts; -- consistent snapshot
COMMIT;
```

**Trade-off:** higher isolation = more correctness but more locking/contention. **Read Committed** is the common default; use **Serializable** for critical invariants (e.g. inventory, balances).
