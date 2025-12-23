# External service thường xuyên timeout

- Timeout + retry
- Circuit breaker
- Fallback strategy

## Chi tiết câu trả lời

Khi external service timeout:

### 1. Timeout + Retry

- Set reasonable timeouts (e.g., 5-10s).
- Implement exponential backoff retry.
- Ưu điểm: Handle transient failures.

### 2. Circuit Breaker

- Open circuit after consecutive failures.
- Fail fast, prevent cascade.
- Ưu điểm: Protect system, allow recovery.

### 3. Fallback Strategy

- Provide default response hoặc cached data.
- Degrade gracefully.
- Ưu điểm: Maintain availability.

Monitor và alert on failures.
