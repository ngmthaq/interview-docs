# Client spam API gây sập hệ thống

- Rate limiting
- API key / token
- Circuit breaker

## Chi tiết câu trả lời

Để bảo vệ khỏi client spam:

### 1. Rate Limiting

- Limit requests per user/IP/time window (e.g., 100 req/min).
- Use algorithms: Token bucket, Leaky bucket.
- Implement ở API gateway hoặc application level.

### 2. API Key / Token

- Require authentication cho sensitive APIs.
- Use JWT, OAuth cho authorization.
- Track usage per key.

### 3. Circuit Breaker

- Detect failures, stop calling failing service temporarily.
- Prevent cascade failures.
- Use patterns như Hystrix.

Kết hợp multiple layers cho robust protection.
