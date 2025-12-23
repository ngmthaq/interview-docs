# Nên throw exception ở đâu?

- Domain exception ≠ HTTP exception
- Map exception ở layer controller

## Chi tiết câu trả lời

Về exception handling:

### 1. Domain Exception ≠ HTTP Exception

- Throw domain-specific exceptions ở business logic (e.g., InsufficientFundsException).
- Don't expose domain details to clients.
- Ưu điểm: Clean separation of concerns.

### 2. Map Exception ở Layer Controller

- Catch domain exceptions ở controller layer.
- Map to appropriate HTTP status codes (400, 404, 500).
- Return user-friendly error messages.
- Ưu điểm: Consistent API responses, security.

Use global exception handlers cho consistency.
