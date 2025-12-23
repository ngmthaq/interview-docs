# Race condition khi call API

- Cancel request
- Ignore stale response

## Chi tiết câu trả lời

Handle API race conditions.

### Cancel request

- AbortController cancel old requests.
- Latest request wins.

### Ignore stale response

- Check request ID/timestamp.
- Only update nếu latest.

Prevent wrong data from old requests.
