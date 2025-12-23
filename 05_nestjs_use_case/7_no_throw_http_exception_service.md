# Không muốn throw `HttpException` trong service

- Domain exception
- Exception filter
- Mapping domain → HTTP response

## Chi tiết câu trả lời

Tách biệt domain và HTTP exceptions.

### Domain exception

- Throw exceptions cụ thể domain (InsufficientFundsException).
- Không phụ thuộc HTTP framework.
- Chứa business context.

### Exception filter

- Implement ExceptionFilter.
- Catch exceptions, transform thành HTTP response.
- Có thể global hoặc per exception type.

### Mapping domain → HTTP response

- Filter map domain exception sang HTTP status (400, 404).
- Trả error message user-friendly.
- Centralized error handling.

Giữ domain layer pure, HTTP concerns ở boundary.