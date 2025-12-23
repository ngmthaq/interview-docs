# Backend trả 200 nhưng business error

- Kiểm tra response body
- Throw custom error
- Không chỉ dựa status code

## Chi tiết câu trả lời

Business errors in 200.

### Kiểm tra response body

- Check success flag.

### Throw custom error

- Treat as error.

### Không chỉ dựa status code

- HTTP != business success.

Handle business logic errors.
