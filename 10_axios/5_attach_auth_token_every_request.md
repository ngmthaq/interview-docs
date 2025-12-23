# Gắn Authorization token cho mọi request

- Request interceptor
- Tránh set token thủ công từng API

## Chi tiết câu trả lời

Attach auth token globally.

### Request interceptor

- Add Authorization header.
- From localStorage or store.

### Tránh set token thủ công từng API

- Centralized.
- DRY principle.

Secure and convenient.
