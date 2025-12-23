# Lưu token ở đâu?

- LocalStorage
- Cookie (HttpOnly)
- Trade-off bảo mật

## Chi tiết câu trả lời

Token storage.

### LocalStorage

- Persistent across sessions.
- Accessible từ JavaScript.
- Vulnerable XSS.

### Cookie (HttpOnly)

- Server set, client can't access.
- Secure against XSS.
- CSRF risk.

### Trade-off

- LocalStorage: Convenient, nhưng less secure.
- Cookies: Secure, nhưng CSRF protection needed.
- Use HttpOnly cookies cho security.

Consider refresh tokens separate.
