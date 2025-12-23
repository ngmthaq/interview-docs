# Xử lý retry thế nào để không tạo duplicate data?

- Idempotency key
- Unique constraint
- Exactly-once vs at-least-once

## Chi tiết câu trả lời

Để retry mà tránh duplicate:

### 1. Idempotency Key

- Generate unique key per request.
- Store key và result, return cached result nếu retry.
- Ưu điểm: Safe retries, no duplicates.

### 2. Unique Constraint

- Use database unique constraints.
- Handle constraint violations gracefully.
- Ưu điểm: Database-level protection.

### 3. Exactly-once vs At-least-once

- Exactly-once: Ensure operation happens only once (idempotency).
- At-least-once: May retry, but handle duplicates.
- Chọn based on system: exactly-once cho financial, at-least-once cho logs.

Implement proper error handling và logging.
