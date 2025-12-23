# Race condition khi nhiều request update cùng entity

- Optimistic lock
- Version column
- Khi nào cần pessimistic lock

## Chi tiết câu trả lời

Handle concurrent updates.

### Optimistic lock

- Assume no conflict, check at commit.
- Throw exception nếu version changed.
- Retry logic ở application.

### Version column

- Add @Version column in entity.
- ORM auto increment on update.
- Detect concurrent changes.

### Khi nào cần pessimistic lock

- High contention, cannot tolerate conflicts.
- SELECT FOR UPDATE, lock row.
- Trade-off: Performance, blocking.

Chọn based on use case: optimistic cho low conflict, pessimistic cho critical.