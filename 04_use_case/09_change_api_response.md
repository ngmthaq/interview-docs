# Thay đổi response API nhưng không được break client cũ

- Versioning
- Backward compatible
- Feature flag

## Chi tiết câu trả lời

Để thay đổi API response mà không break clients:

### 1. Versioning

- API versioning: URL (/v1/, /v2/), header (Accept-Version), query param.
- Maintain multiple versions temporarily.
- Deprecate old versions gradually.

### 2. Backward Compatible

- Only add new fields, don't remove/change existing.
- Use default values cho new fields.
- Avoid breaking changes.

### 3. Feature Flag

- Use feature flags để enable new response conditionally.
- Roll out gradually, monitor impact.
- Allow rollback if issues.

Communicate changes với clients, provide migration guide.
