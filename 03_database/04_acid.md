# 4. What are the ACID properties? (Junior)

ACID describes the guarantees a reliable **transaction** provides.

| Letter | Property    | Meaning                                                                       |
| ------ | ----------- | ----------------------------------------------------------------------------- |
| **A**  | Atomicity   | All steps succeed or none do (all-or-nothing)                                 |
| **C**  | Consistency | A transaction moves the DB from one valid state to another (constraints hold) |
| **I**  | Isolation   | Concurrent transactions don't corrupt each other                              |
| **D**  | Durability  | Once committed, data survives crashes                                         |

```sql
BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT; -- both updates apply, or neither (Atomicity)
```

**Why it matters:** in a money transfer, Atomicity ensures you never debit one account without crediting the other. ACID is the reason relational DBs are trusted for financial and critical data.
