# Một API chỉ cho phép gọi từ internal service

- API key
- mTLS
- Network policy

## Chi tiết câu trả lời

Secure internal API calls.

### API key

- Shared secret key.
- Validate in header/ query.
- Simple, nhưng kém secure nếu leak.

### mTLS

- Mutual TLS: Client và server verify certificates.
- Strong authentication.
- Prevent man-in-the-middle.

### Network policy

- Firewall rules, VPC.
- Allow only internal IPs.
- Kubernetes network policies.

Kết hợp multiple methods cho security.