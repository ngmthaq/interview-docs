# JWT nhưng user bị logout ngẫu nhiên

- Access token vs Refresh token
- Clock skew
- Token rotation

## Chi tiết câu trả lời

JWT logout issues.

### Access token vs Refresh token

- Access token: Short-lived (15min), cho API access.
- Refresh token: Long-lived, renew access token.
- Logout: Invalidate refresh token.

### Clock skew

- Time difference giữa server/client.
- Set nbf/exp với buffer time.
- Sync clocks hoặc use NTP.

### Token rotation

- On refresh, issue new access + refresh token.
- Invalidate old tokens.
- Prevent replay attacks.

Implement proper token management.