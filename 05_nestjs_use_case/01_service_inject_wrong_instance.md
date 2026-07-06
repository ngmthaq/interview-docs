# Một service bị inject sai instance, dữ liệu dùng chung bị lỗi

- Scope mặc định của provider là gì?
- Khi nào dùng:
  - Singleton (default)
  - Request-scoped
  - Transient
- Cách debug DI container

## Chi tiết câu trả lời

Vấn đề inject sai instance trong NestJS thường liên quan đến scope của provider.

### Scope mặc định của provider

- Mặc định là Singleton: Một instance duy nhất cho toàn bộ ứng dụng.
- Tất cả module sử dụng provider này sẽ nhận cùng instance.
- Dữ liệu dùng chung có thể gây lỗi nếu không cẩn thận.

### Khi nào dùng các scope khác

- **Singleton**: Cho stateless services, shared data (như config, cache).
- **Request-scoped**: Mỗi request HTTP có instance riêng. Dùng cho data phụ thuộc request (user context, transaction).
- **Transient**: Mỗi lần inject tạo instance mới. Dùng cho lightweight, stateless objects.

### Cách debug DI container

- Sử dụng `app.get()` để kiểm tra instance.
- Log trong constructor để xem số lần tạo instance.
- Kiểm tra module imports/exports.
- Sử dụng `@Inject()` với token để debug.

Chọn scope phù hợp để tránh lỗi dữ liệu dùng chung.