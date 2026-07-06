# Transaction trong Database

## 1. Transaction là gì?

**Transaction (giao dịch)** là một tập hợp các thao tác cơ sở dữ liệu (SQL operations) được thực thi như **một đơn vị công việc duy nhất**.

Nguyên tắc:

- **Hoặc tất cả cùng thành công (COMMIT)**
- **Hoặc tất cả cùng thất bại và quay về trạng thái ban đầu (ROLLBACK)**

Transaction giúp đảm bảo dữ liệu **nhất quán, an toàn**, ngay cả khi:

- Hệ thống crash
- Exception xảy ra
- Mất kết nối giữa chừng

---

## 2. ACID – Nền tảng của Transaction

Transaction tuân theo 4 nguyên tắc **ACID**:

### 2.1 Atomicity (Tính nguyên tử)

- Transaction là một khối không thể chia nhỏ.
- Một bước fail → toàn bộ transaction rollback.

### 2.2 Consistency (Tính nhất quán)

- Dữ liệu trước và sau transaction phải thỏa:
  - Database constraints
  - Foreign key
  - Business rules

### 2.3 Isolation (Tính cô lập)

- Các transaction chạy song song không ảnh hưởng lẫn nhau.
- Ngăn các hiện tượng:
  - Dirty Read
  - Non-repeatable Read
  - Phantom Read

### 2.4 Durability (Tính bền vững)

- Khi transaction đã commit, dữ liệu được lưu vĩnh viễn.
- Crash hệ thống không làm mất dữ liệu đã commit.

---

## 3. Khi nào cần dùng Transaction?

### 3.1 Nhiều thao tác ghi có liên quan logic

Ví dụ:

- Chuyển tiền giữa 2 tài khoản
- Tạo order + order items
- Tạo user + gán role
- Trừ stock + tạo đơn hàng

Nguyên tắc:

> Nếu 1 bước fail → tất cả phải rollback

---

### 3.2 Khi cần đảm bảo tính toàn vẹn dữ liệu

Ví dụ:

- Không trừ tiền nếu tạo order thất bại
- Không tạo order nếu stock không đủ
- Không ghi log thanh toán nếu payment fail

---

### 3.3 Khi có concurrent request (đồng thời)

- Nhiều request cùng đọc / ghi một bản ghi
- Nguy cơ **race condition**

Transaction là nền tảng để kiểm soát các tình huống này.

---

## 4. Race Condition là gì?

**Race Condition** xảy ra khi **nhiều transaction hoặc request đồng thời truy cập và ghi cùng một dữ liệu**, dẫn đến kết quả sai hoặc không nhất quán.

### Ví dụ điển hình

- Sản phẩm còn `stock = 1`
- 2 user cùng lúc gửi request mua hàng
- Cả 2 đều đọc `stock = 1`
- Cả 2 đều trừ stock
- Kết quả: `stock = -1`

---
