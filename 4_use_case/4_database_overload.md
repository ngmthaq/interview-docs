# Database quá tải khi traffic tăng đột biến

- Read replica
- Cache (Redis)
- Rate limit
- Degrade tính năng không quan trọng

## Chi tiết câu trả lời

Để xử lý database overload khi traffic spike:

### 1. Read Replica

- Tạo read replicas để offload read queries.
- Route read queries to replicas, write to master.
- Ưu điểm: Scale reads easily.
- Nhược điểm: Replication lag, eventual consistency.

### 2. Cache (Redis)

- Cache frequently accessed data in Redis.
- Use cache-aside, write-through patterns.
- Ưu điểm: Reduce DB load, fast access.
- Nhược điểm: Cache invalidation complexity.

### 3. Rate Limit

- Implement rate limiting ở application level.
- Queue requests hoặc reject excess.
- Ưu điểm: Protect system from overload.
- Nhược điểm: May affect user experience.

### 4. Degrade tính năng không quan trọng

- Disable non-critical features during peak.
- Serve static responses hoặc cached data.
- Ưu điểm: Maintain core functionality.
- Nhược điểm: Reduced features temporarily.

Kết hợp multi-layer approach cho best results.
