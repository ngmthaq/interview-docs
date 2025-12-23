# User đổi filter liên tục → gọi API chồng nhau

- Cancel request cũ
- Ignore stale response

## Chi tiết câu trả lời

Handle rapid filter changes.

### Cancel request cũ

- Abort previous requests.

### Ignore stale response

- Check if latest.

Avoid race conditions.
