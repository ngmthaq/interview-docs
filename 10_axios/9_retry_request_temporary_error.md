# Retry request khi lỗi tạm thời

- Retry với backoff
- Chỉ retry với idempotent request
- Không retry 4xx

## Chi tiết câu trả lời

Retry failed requests.

### Retry với backoff

- Exponential backoff.

### Chỉ retry với idempotent request

- GET, PUT safe.

### Không retry 4xx

- Client errors not retryable.

Reliable API calls.
