# Circular dependency giữa 2 module/service

- Nguyên nhân
- `forwardRef()` giải quyết gì?
- Khi nào nên **refactor kiến trúc thay vì forwardRef**

## Chi tiết câu trả lời

Circular dependency xảy ra khi hai module/service phụ thuộc lẫn nhau.

### Nguyên nhân

- Service A inject Service B, Service B inject Service A.
- Module A import Module B, Module B import Module A.
- Thường do thiết kế kiến trúc kém, logic nghiệp vụ lẫn lộn.

### `forwardRef()` giải quyết gì?

- Cho phép tham chiếu trước khi khai báo.
- Sử dụng `forwardRef(() => ServiceB)` trong constructor.
- Giải quyết tạm thời circular dependency ở runtime.

### Khi nào nên refactor thay vì forwardRef

- Khi circular dependency do thiết kế sai: Tách service, sử dụng events hoặc mediator pattern.
- Nếu dùng forwardRef nhiều, refactor để tránh phức tạp.
- Trong production, tránh forwardRef vì có thể gây lỗi runtime.

Refactor sớm để có kiến trúc sạch.