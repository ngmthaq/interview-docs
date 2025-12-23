# Lưu token ở đâu?

- HttpOnly cookie
- Trade-off bảo mật

## Chi tiết câu trả lời

Token storage.

### HttpOnly cookie

- Secure, server-only.
- CSRF protection.

### Trade-off bảo mật

- Cookie: secure but complex.
- LocalStorage: convenient but vulnerable.

HttpOnly preferred.
