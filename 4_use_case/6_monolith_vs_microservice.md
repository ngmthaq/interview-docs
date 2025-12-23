# Khi nào dùng monolith, khi nào microservice?

- Monolith: team nhỏ, domain đơn giản
- Microservice: scale độc lập, team lớn
- Nhấn mạnh **cost & complexity**

## Chi tiết câu trả lời

Lựa chọn giữa monolith và microservice:

### Monolith

- **Khi nào dùng**: Team nhỏ (<10 người), domain đơn giản, startup giai đoạn đầu.
- **Ưu điểm**: Đơn giản development, deployment, debugging. Shared code, data consistency.
- **Nhược điểm**: Khó scale, tight coupling, single point of failure.

### Microservice

- **Khi nào dùng**: Team lớn, domain phức tạp, cần scale độc lập, high availability.
- **Ưu điểm**: Independent scaling, technology diversity, fault isolation.
- **Nhược điểm**: Complexity cao (distributed systems, service discovery, orchestration), cost vận hành, testing khó.

**Cost & Complexity**: Microservice tăng complexity (network calls, data consistency, monitoring) và cost (infrastructure, DevOps). Chỉ dùng khi benefits outweigh costs. Bắt đầu với monolith, refactor thành microservice khi cần.
