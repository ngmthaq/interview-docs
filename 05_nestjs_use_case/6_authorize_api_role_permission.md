# Phân quyền API theo role / permission

- Guard
- Custom decorator (`@Roles()`)
- Thứ tự: Guard → Interceptor → Pipe → Controller

## Chi tiết câu trả lời

Authorization trong NestJS.

### Guard

- Implement CanActivate.
- Check permissions trước khi execute handler.
- Throw exception nếu unauthorized.

### Custom decorator (@Roles())

- Tạo decorator để set metadata trên handler.
- Guard đọc metadata để check roles.
- Linh hoạt, declarative.

### Thứ tự execution

- Guard → Interceptor → Pipe → Controller
- Guard: Authorization
- Interceptor: Logging, caching
- Pipe: Validation, transformation
- Controller: Business logic

Đảm bảo thứ tự để security trước.