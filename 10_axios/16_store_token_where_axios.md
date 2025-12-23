# Lưu token ở đâu khi dùng Axios?

- HttpOnly cookie
- Memory
- Không nên dùng localStorage cho token nhạy cảm

## Chi tiết câu trả lời

Token storage.

### HttpOnly cookie

- Secure, server-side.

### Memory

- In-memory storage.

### Không nên dùng localStorage cho token nhạy cảm

- Vulnerable to XSS.

Secure token handling.
