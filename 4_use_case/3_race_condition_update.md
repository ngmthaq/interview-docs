# Hai service cùng update một bản ghi, làm sao tránh race condition?

- Isolation level
- Optimistic / pessimistic lock
- Event-driven + eventual consistency

## Chi tiết câu trả lời

Để tránh race condition khi hai service update cùng record:

### 1. Isolation Level

- Sử dụng SERIALIZABLE isolation level để đảm bảo serial execution.
- Hoặc REPEATABLE READ để tránh lost updates.
- Ưu điểm: Database-level solution.
- Nhược điểm: Performance impact, potential deadlocks.

### 2. Optimistic / Pessimistic Lock

- Pessimistic: Lock record trước khi update (SELECT FOR UPDATE).
- Optimistic: Check version/timestamp trước update, retry nếu conflict.
- Ưu điểm: Control concurrency.
- Nhược điểm: Blocking hoặc retry logic.

### 3. Event-driven + Eventual Consistency

- Sử dụng event sourcing: ghi events thay vì direct update.
- Process events asynchronously để update state.
- Ưu điểm: High availability, no locks.
- Nhược điểm: Eventual consistency, phức tạp hơn.

Chọn approach dựa trên consistency requirements và performance needs.
