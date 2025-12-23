# Token auth xử lý trong React thế nào?

- HttpOnly cookie
- Refresh token flow
- Silent refresh

## Chi tiết câu trả lời

Handle token auth.

### HttpOnly cookie

- Store access token in HttpOnly cookie.
- Secure against XSS.

### Refresh token flow

- Use refresh token get new access.
- Store refresh in secure cookie.

### Silent refresh

- Refresh token before expiry.
- Seamless user experience.

Secure token handling.
