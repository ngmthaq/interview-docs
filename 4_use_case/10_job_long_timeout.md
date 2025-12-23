# Job xử lý lâu làm request bị timeout

- Background job
- Queue
- Async processing
- Polling / webhook

## Chi tiết câu trả lời

Khi job dài gây timeout:

### 1. Background Job

- Move processing to background threads/workers.
- Return immediate response với job ID.
- Ưu điểm: Non-blocking, better UX.

### 2. Queue

- Push job to queue (RabbitMQ, SQS).
- Workers process asynchronously.
- Ưu điểm: Decoupling, scalability.

### 3. Async Processing

- Use async/await patterns.
- Process in parallel nếu possible.
- Ưu điểm: Efficient resource usage.

### 4. Polling / Webhook

- Client polls for status hoặc register webhook for notification.
- Ưu điểm: Real-time updates without long connections.

Chọn based on use case: polling cho simple, webhook cho complex.
