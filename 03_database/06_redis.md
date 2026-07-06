# Redis là gì?

**Redis** là một hệ quản trị cơ sở dữ liệu in-memory mã nguồn mở, lưu trữ dữ liệu dưới dạng key-value, thường dùng làm database, cache hoặc message broker. Nó nổi bật bởi tốc độ cực nhanh nhờ lưu dữ liệu trực tiếp trên RAM và hỗ trợ nhiều cấu trúc dữ liệu như string, hash, list, set, sorted set.

---

## 🔑 Tổng quan về Redis

- **Nguồn gốc**: Redis viết tắt từ _Remote Dictionary Server_
- **Kiểu dữ liệu hỗ trợ**: string, hash, list, set, sorted set
- **Cách lưu trữ**: dữ liệu chính nằm trên RAM để tăng tốc độ, nhưng có thể backup ra ổ cứng (RDB, AOF)
- **Tốc độ**: phản hồi dưới một phần nghìn giây, xử lý hàng triệu yêu cầu mỗi giây
- **Ứng dụng**: caching, session management, leaderboard, gaming, hệ thống real-time, IoT

---

## 📊 So sánh Redis với cơ sở dữ liệu truyền thống

| **Tiêu chí**              | **Redis**                             | **SQL Database**                            |
| ------------------------- | ------------------------------------- | ------------------------------------------- |
| **Kiểu dữ liệu**          | Key-Value, hỗ trợ cấu trúc nâng cao   | Bảng, quan hệ                               |
| **Tốc độ**                | Rất nhanh (RAM-based)                 | Chậm hơn (disk-based)                       |
| **Khả năng mở rộng**      | Dễ dàng scale theo chiều ngang        | Phức tạp hơn                                |
| **Tính bền vững dữ liệu** | Có backup nhưng ưu tiên tốc độ        | Ưu tiên tính toàn vẹn dữ liệu               |
| **Ứng dụng phổ biến**     | Cache, real-time apps, message broker | Quản lý dữ liệu lâu dài, nghiệp vụ phức tạp |

---

## ⚡ Ưu điểm nổi bật

- **Hiệu năng cao**: xử lý hàng triệu request/giây
- **Đa năng**: vừa làm cache, vừa làm database, vừa làm message broker
- **Hỗ trợ nhiều cấu trúc dữ liệu**: linh hoạt cho nhiều loại ứng dụng
- **Khả năng phục hồi**: backup dữ liệu trên ổ cứng khi sự cố

---

## 🚨 Hạn chế cần lưu ý

- **Dữ liệu trên RAM**: tốn chi phí nếu dữ liệu quá lớn
- **Không thay thế hoàn toàn SQL**: thiếu tính toàn vẹn và quan hệ phức tạp
- **Quản lý bộ nhớ**: cần tối ưu để tránh tràn RAM
