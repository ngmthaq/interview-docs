# Service quá nhiều logic, controller quá mỏng — có ổn không?

- Controller nên làm gì?
- Service nên làm gì?
- Khi nào cần tách domain service / application service

## Chi tiết câu trả lời

Vấn đề cân bằng logic giữa controller và service.

### Controller nên làm gì?

- Xử lý HTTP concerns: routing, request/response mapping.
- Validation input, authentication.
- Gọi service và trả response.
- Giữ mỏng, chỉ orchestrate.

### Service nên làm gì?

- Chứa business logic.
- Tương tác DB, external services.
- Transform data, apply rules.
- Có thể dày nếu logic phức tạp.

### Khi nào cần tách domain service / application service

- **Domain service**: Logic nghiệp vụ thuần túy, không phụ thuộc framework.
- **Application service**: Orchestrate domain services, handle use cases.
- Tách khi service quá lớn (>200-300 lines), hoặc có nhiều responsibilities.

Không ổn nếu controller quá mỏng (chỉ pass-through) hoặc service quá dày. Cân bằng theo Single Responsibility.