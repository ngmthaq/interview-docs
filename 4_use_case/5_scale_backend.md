# Làm sao scale backend khi user tăng gấp 10?

- Stateless service
- Horizontal scaling
- Load balancer
- Cache + async processing

## Chi tiết câu trả lời

Để scale backend khi user tăng 10x:

### 1. Stateless Service

- Design services không lưu state locally.
- Store state in external storage (DB, cache).
- Ưu điểm: Easy horizontal scaling.
- Nhược điểm: Need external state management.

### 2. Horizontal Scaling

- Add more instances của service.
- Use container orchestration (Kubernetes).
- Ưu điểm: Linear scaling.
- Nhược điểm: Complexity in management.

### 3. Load Balancer

- Distribute traffic across instances.
- Use ALB, NGINX, hoặc cloud load balancers.
- Ưu điểm: Even distribution, failover.
- Nhược điểm: Single point of failure (mitigate with redundancy).

### 4. Cache + Async Processing

- Cache hot data to reduce DB load.
- Move heavy processing to background jobs.
- Ưu điểm: Improve response time, scale better.
- Nhược điểm: Eventual consistency.

Implement monitoring và auto-scaling để adapt dynamically.
