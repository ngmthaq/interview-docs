# N+1 Query Problem

**N+1 query problem** là hiện tượng khi ứng dụng thực hiện quá nhiều truy vấn SQL không cần thiết, thường xảy ra trong ORM (Object-Relational Mapping). Nó làm giảm hiệu năng vì thay vì chỉ cần một truy vấn để lấy dữ liệu, hệ thống lại thực hiện thêm N truy vấn phụ cho từng bản ghi.

---

## 🔎 Giải thích chi tiết

- **Khái niệm**  
  Vấn đề N+1 query xuất hiện khi bạn thực hiện một truy vấn để lấy danh sách đối tượng (ví dụ: tất cả _Users_), sau đó với mỗi đối tượng lại thực hiện thêm một truy vấn để lấy dữ liệu liên quan (ví dụ: _Posts_ của từng User).  
  → Kết quả: 1 truy vấn chính + N truy vấn phụ = N+1 truy vấn.

- **Ví dụ minh họa**  
  Bạn muốn lấy danh sách 10 người dùng cùng với bài viết của họ:

  - Truy vấn 1: `SELECT * FROM users;`
  - Sau đó, với mỗi user, ORM lại chạy: `SELECT * FROM posts WHERE user_id = ?;`  
    → Tổng cộng 11 truy vấn thay vì chỉ cần 1 truy vấn với `JOIN`.

- **Nguyên nhân**
  - ORM mặc định dùng **lazy loading** (chỉ tải dữ liệu khi cần).
  - Lập trình viên không tối ưu hóa cách lấy dữ liệu liên quan.
  - Quan hệ phức tạp giữa các bảng (One-to-Many, Many-to-Many).

---

## ⚡ Hậu quả

- **Hiệu năng kém**: Tốn thời gian và tài nguyên khi số lượng bản ghi lớn.
- **Tăng độ trễ**: Người dùng phải chờ lâu hơn để dữ liệu hiển thị.
- **Khó mở rộng**: Khi dữ liệu tăng, hệ thống dễ bị nghẽn.

---

## 🛠️ Cách khắc phục

- **Eager loading**: Lấy dữ liệu liên quan ngay trong một truy vấn (ví dụ dùng `JOIN` hoặc `fetch join`).
- **Batch fetching**: Gom nhiều truy vấn nhỏ thành một truy vấn lớn.
- **Tối ưu ORM**: Sử dụng các công cụ như `EntityGraph` trong JPA hoặc `select_related` trong Django.
- **Kiểm tra hiệu năng**: Dùng profiler hoặc query monitor để phát hiện N+1.

---

## 📊 So sánh Lazy vs Eager Loading

| **Cách tiếp cận** | **Đặc điểm**               | **Ưu điểm**                  | **Nhược điểm**                        |
| ----------------- | -------------------------- | ---------------------------- | ------------------------------------- |
| **Lazy loading**  | Chỉ tải dữ liệu khi cần    | Tiết kiệm tài nguyên ban đầu | Dễ gây N+1 query problem              |
| **Eager loading** | Tải dữ liệu liên quan ngay | Giảm số lượng truy vấn       | Có thể tải dư dữ liệu không cần thiết |
