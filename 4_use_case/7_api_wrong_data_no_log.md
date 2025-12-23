# API trả về dữ liệu sai nhưng không log được lỗi

- Add structured logging
- Correlation ID
- Improve observability (metrics, tracing)

## Chi tiết câu trả lời

Khi API trả sai data mà không log lỗi:

### 1. Add Structured Logging

- Implement structured logging (JSON format) với levels (ERROR, WARN, INFO).
- Log request/response data, timestamps, user context.
- Use log aggregation tools (ELK stack).

### 2. Correlation ID

- Generate unique ID cho mỗi request, pass through all services.
- Log với correlation ID để trace request flow.
- Giúp debug issues across services.

### 3. Improve Observability (Metrics, Tracing)

- Add metrics: response time, error rates, throughput.
- Implement distributed tracing (Jaeger, Zipkin).
- Use monitoring tools (Prometheus, Grafana).

Kết hợp để identify và fix issues nhanh chóng.
