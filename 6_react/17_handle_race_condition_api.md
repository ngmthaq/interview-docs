# Xử lý race condition khi call API

- Cancel request
- Ignore stale response
- useEffect cleanup

## Chi tiết câu trả lời

Race condition trong async operations.

### Cancel request

- AbortController cancel pending requests.
- Prevent state update từ old requests.

### Ignore stale response

- Check request ID hoặc timestamp.
- Only update nếu response mới nhất.

### useEffect cleanup

- Cleanup function cancel requests.
- Prevent memory leaks, wrong state.

Libraries như React Query handle automatically.
