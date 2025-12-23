# Flash sale bị overselling, bạn xử lý thế nào?

Gợi ý hướng trả lời:

- Transaction + row-level lock
- Optimistic locking (version)
- Redis + Lua script
- Queue (Kafka / RabbitMQ)

## Chi tiết câu trả lời

Để xử lý vấn đề overselling trong flash sale, chúng ta cần đảm bảo tính nhất quán và ngăn chặn việc bán quá số lượng tồn kho. Dưới đây là các phương pháp chi tiết:

### 1. Transaction + Row-level Lock

- Sử dụng database transaction để đảm bảo atomicity: tất cả các thao tác (kiểm tra tồn kho, giảm số lượng, tạo đơn hàng) phải thành công hoặc thất bại cùng nhau.
- Áp dụng row-level lock (SELECT FOR UPDATE) để khóa hàng tồn kho cụ thể, ngăn chặn các transaction khác truy cập đồng thời.
- Ưu điểm: Đơn giản, đảm bảo consistency.
- Nhược điểm: Có thể gây blocking, giảm performance dưới tải cao.

### 2. Optimistic Locking (Version)

- Thêm cột version vào bảng tồn kho.
- Khi update, kiểm tra version hiện tại có khớp với version đọc ban đầu không. Nếu không, rollback và retry.
- Ưu điểm: Không lock, performance tốt hơn.
- Nhược điểm: Có thể có conflict, cần retry logic.

### 3. Redis + Lua Script

- Sử dụng Redis để lưu trữ tồn kho (atomic operations).
- Viết Lua script để kiểm tra và giảm tồn kho trong một atomic operation.
- Ưu điểm: Nhanh, atomic, phù hợp với high concurrency.
- Nhược điểm: Cần sync với database, phức tạp hơn.

### 4. Queue (Kafka / RabbitMQ)

- Đưa các request mua hàng vào queue.
- Xử lý tuần tự từng request, kiểm tra tồn kho trước khi xử lý.
- Ưu điểm: Đảm bảo order, dễ scale.
- Nhược điểm: Latency cao, không realtime.

Tùy vào scale và requirements, chọn phương pháp phù hợp. Thường kết hợp nhiều cách.
