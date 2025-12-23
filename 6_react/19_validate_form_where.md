# Validate form ở đâu?

- Client
- Server
- Đồng bộ rule thế nào?

## Chi tiết câu trả lời

Form validation layers.

### Client validation

- Immediate feedback, UX tốt.
- Prevent invalid submits.
- Use libraries như Yup, Joi.

### Server validation

- Security: Never trust client.
- Business rules, data integrity.
- Return errors cho client.

### Đồng bộ rule

- Define validation schema once.
- Share giữa client/server nếu possible.
- Consistent error messages.

Client validation UX, server validation security.
