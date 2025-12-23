# API bị lộ dữ liệu nhạy cảm

- Validate authorization
- Mask data
- Audit log

## Chi tiết câu trả lời

Bảo vệ sensitive data:

### 1. Validate Authorization

- Check user permissions before returning data.
- Use RBAC/ABAC.
- Ưu điểm: Prevent unauthorized access.

### 2. Mask Data

- Mask/hide sensitive fields (e.g., credit card numbers).
- Show partial data only.
- Ưu điểm: Reduce exposure.

### 3. Audit Log

- Log all access to sensitive data.
- Monitor suspicious activities.
- Ưu điểm: Detect breaches, compliance.

Encrypt data at rest/transit.
