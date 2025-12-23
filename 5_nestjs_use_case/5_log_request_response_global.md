# Cần log toàn bộ request/response nhưng không sửa từng controller

- Interceptor
- Middleware khác Interceptor ở điểm nào?

## Chi tiết câu trả lời

Log request/response globally.

### Interceptor

- Implement NestInterceptor.
- Bind globally hoặc per controller.
- Can modify request/response, log details.
- Chạy sau guards, trước pipes.

### Middleware khác Interceptor ở điểm nào?

- **Middleware**: Chạy đầu tiên, trước routing. Không access execution context.
- **Interceptor**: Sau routing, có access controller/method. Can transform response.
- Middleware cho low-level (CORS, logging basic), Interceptor cho app-level (logging detailed).

Sử dụng interceptor cho logging toàn diện.