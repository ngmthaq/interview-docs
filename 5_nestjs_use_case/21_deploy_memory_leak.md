# Deploy xong bị memory leak

- Provider scope
- EventEmitter
- Unclosed DB connection

## Chi tiết câu trả lời

Memory leak in production.

### Provider scope

- Singleton providers accumulate data.
- Use request-scoped nếu store request data.
- Clear references after use.

### EventEmitter

- Unclosed listeners accumulate.
- Use once() hoặc removeListener().
- Limit max listeners.

### Unclosed DB connection

- Pool connections not released.
- Use connection.release() hoặc try-finally.
- Monitor connection pool.

Profile với tools như clinic.js.