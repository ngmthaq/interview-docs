# Validate request nhưng logic validate phức tạp

- DTO + `class-validator`
- Custom Pipe
- Domain validation khác gì request validation?

## Chi tiết câu trả lời

Validation phức tạp trong NestJS.

### DTO + class-validator

- Sử dụng DTO với decorators (@IsString, @IsEmail).
- Tự động validate input.
- Dễ cho simple rules.

### Custom Pipe

- Tạo pipe tùy chỉnh extends ValidationPipe.
- Thêm logic phức tạp: check DB, business rules.
- Transform data nếu cần.

### Domain validation khác gì request validation?

- **Request validation**: Validate format, required fields (ở boundary).
- **Domain validation**: Validate business rules, invariants (ở domain layer).
- Request validation ngăn invalid input, domain validation đảm bảo consistency.

Kết hợp cả hai cho robust validation.