# User đổi filter liên tục → API bị gọi nhiều

- Debounce / throttle
- Cancel request cũ
- Cache kết quả

## Chi tiết câu trả lời

Handle frequent filter changes.

### Debounce / throttle

- Debounce: Wait user stop, then fetch.
- Throttle: Limit fetch rate.

### Cancel request cũ

- AbortController cancel pending requests.
- Prevent race conditions.

### Cache kết quả

- Cache responses.
- Return cached nếu same filter.

Combine để optimize API calls.
