# Làm sao bảo vệ backend khỏi tấn công cơ bản?

- Input validation
- Rate limit
- Authentication / Authorization
- HTTPS

## Chi tiết câu trả lời

Bảo vệ backend khỏi attacks:

### 1. Input Validation

- Validate/sanitize all inputs.
- Use whitelisting, parameterized queries.
- Prevent SQL injection, XSS.

### 2. Rate Limit

- Limit requests per IP/user.
- Prevent DoS attacks.

### 3. Authentication / Authorization

- Use strong auth (JWT, OAuth).
- Implement proper authorization.

### 4. HTTPS

- Encrypt traffic.
- Prevent man-in-the-middle.

Additional: WAF, security headers, regular audits.
