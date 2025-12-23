# Optimistic Lock vs Pessimistic Lock trong Database

## Tổng quan

Trong hệ thống cơ sở dữ liệu, khi nhiều transaction cùng truy cập và thay đổi dữ liệu, cần có cơ chế đồng bộ hóa để đảm bảo tính nhất quán và toàn vêng của dữ liệu. Hai phương pháp chính được sử dụng là **Optimistic Lock** (Khóa lạc quan) và **Pessimistic Lock** (Khóa bi quan).

## Pessimistic Lock (Khóa bi quan)

### Khái niệm

Pessimistic Lock hoạt động theo nguyên tắc "ngăn chặn xung đột trước khi nó xảy ra". Khi một transaction muốn thao tác với dữ liệu, nó sẽ khóa dữ liệu đó ngay lập tức để ngăn các transaction khác truy cập.

### Cách hoạt động

1. Transaction A muốn đọc/ghi dữ liệu
2. Hệ thống khóa dữ liệu đó ngay lập tức
3. Các transaction khác phải chờ cho đến khi Transaction A hoàn thành
4. Sau khi Transaction A commit/rollback, khóa được giải phóng

### Ví dụ SQL

```sql
-- Trong PostgreSQL
BEGIN;
SELECT * FROM accounts WHERE id = 1 FOR UPDATE;
-- Thực hiện các thao tác khác
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
COMMIT;
```

### Ưu điểm

- Đảm bảo tính nhất quán dữ liệu tuyệt đối
- Tránh được race condition
- Phù hợp với hệ thống có tần suất xung đột cao
- Dễ hiểu và implement

### Nhược điểm

- Giảm hiệu suất do blocking
- Có thể gây deadlock
- Không phù hợp cho hệ thống có nhiều người dùng đồng thời
- Thời gian chờ có thể dài

## Optimistic Lock (Khóa lạc quan)

### Khái niệm

Optimistic Lock hoạt động theo nguyên tắc "cho phép xung đột xảy ra, sau đó phát hiện và xử lý". Transaction không khóa dữ liệu khi đọc, mà chỉ kiểm tra xung đột khi commit.

### Cách hoạt động

1. Transaction A đọc dữ liệu cùng với version/timestamp
2. Thực hiện các thao tác trên dữ liệu local
3. Khi commit, kiểm tra version/timestamp có thay đổi không
4. Nếu không thay đổi: commit thành công
5. Nếu có thay đổi: rollback và retry

### Ví dụ với Version Field

```sql
-- Bảng có version field
CREATE TABLE accounts (
    id INT PRIMARY KEY,
    balance DECIMAL(10,2),
    version INT DEFAULT 0
);

-- Đọc dữ liệu
SELECT id, balance, version FROM accounts WHERE id = 1;
-- Giả sử version = 5

-- Cập nhật với kiểm tra version
UPDATE accounts
SET balance = balance - 100, version = version + 1
WHERE id = 1 AND version = 5;

-- Nếu affected rows = 0 thì có conflict
```

### Ví dụ với Timestamp

```sql
CREATE TABLE accounts (
    id INT PRIMARY KEY,
    balance DECIMAL(10,2),
    last_modified TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Đọc dữ liệu
SELECT id, balance, last_modified FROM accounts WHERE id = 1;

-- Cập nhật với kiểm tra timestamp
UPDATE accounts
SET balance = balance - 100,
    last_modified = CURRENT_TIMESTAMP
WHERE id = 1 AND last_modified = '2024-01-01 10:30:00';
```

### Ưu điểm

- Hiệu suất cao, không blocking
- Phù hợp cho hệ thống có nhiều người dùng đồng thời
- Không gây deadlock
- Scalability tốt

### Nhược điểm

- Phức tạp hơn trong implementation
- Cần retry logic khi có conflict
- Có thể gây starvation nếu conflict liên tục
- Cần thêm field để tracking (version, timestamp)

## So sánh chi tiết

| Tiêu chí             | Pessimistic Lock       | Optimistic Lock      |
| -------------------- | ---------------------- | -------------------- |
| **Performance**      | Thấp (do blocking)     | Cao (no blocking)    |
| **Concurrency**      | Thấp                   | Cao                  |
| **Complexity**       | Đơn giản               | Phức tạp hơn         |
| **Deadlock**         | Có thể xảy ra          | Không                |
| **Data Consistency** | Tuyệt đối              | Eventual (cần retry) |
| **Scalability**      | Hạn chế                | Tốt                  |
| **Resource Usage**   | Cao (do holding locks) | Thấp                 |

## Khi nào sử dụng

### Sử dụng Pessimistic Lock khi:

- Tần suất conflict cao
- Dữ liệu cực kỳ quan trọng (tài chính, y tế)
- Hệ thống có ít người dùng đồng thời
- Không thể chấp nhận retry

### Sử dụng Optimistic Lock khi:

- Tần suất conflict thấp
- Cần hiệu suất cao
- Hệ thống có nhiều người dùng đồng thời
- Có thể chấp nhận retry logic

## Ví dụ thực tế

### Banking System với Pessimistic Lock

```sql
-- Transfer tiền an toàn
BEGIN;
SELECT balance FROM accounts WHERE id = 1 FOR UPDATE;
SELECT balance FROM accounts WHERE id = 2 FOR UPDATE;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### E-commerce với Optimistic Lock

```sql
-- Cập nhật inventory
SELECT product_id, quantity, version FROM inventory WHERE product_id = 123;
-- version = 10, quantity = 50

-- Người dùng mua 2 sản phẩm
UPDATE inventory
SET quantity = 48, version = 11
WHERE product_id = 123 AND version = 10;

-- Nếu affected rows = 0, reload và retry
```

## Best Practices

### Cho Pessimistic Lock:

- Giữ transaction ngắn nhất có thể
- Luôn khóa theo thứ tự nhất định để tránh deadlock
- Sử dụng timeout để tránh chờ vô hạn
- Monitor deadlock và retry logic

### Cho Optimistic Lock:

- Implement retry logic với exponential backoff
- Giới hạn số lần retry
- Sử dụng version field thay vì timestamp khi có thể
- Cache version để giảm database calls

## Kết luận

Cả hai phương pháp đều có ưu nhược điểm riêng. Lựa chọn phụ thuộc vào:

- Tần suất conflict trong hệ thống
- Yêu cầu về performance và scalability
- Mức độ quan trọng của data consistency
- Khả năng implement và maintain

Trong thực tế, nhiều hệ thống sử dụng kết hợp cả hai phương pháp tùy theo từng use case cụ thể.
