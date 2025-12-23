# Database Index: Hoạt động, Cách đánh và Khi nào sử dụng

## Index là gì?

Index (chỉ mục) là một cấu trúc dữ liệu được tạo ra để tăng tốc độ truy vấn dữ liệu trong database. Giống như mục lục trong sách, index giúp database engine nhanh chóng tìm được vị trí của dữ liệu mà không cần phải scan toàn bộ bảng.

## Cách Index hoạt động

### Cấu trúc cơ bản

Index thường được implement bằng cấu trúc **B-Tree** (Balanced Tree), cho phép:

- Tìm kiếm trong O(log n) thay vì O(n)
- Duy trì thứ tự sắp xếp
- Hỗ trợ range queries hiệu quả

### Quá trình hoạt động

#### 1. Khi không có Index (Table Scan)

```sql
SELECT * FROM users WHERE age = 25;
```

- Database phải đọc từng row từ đầu đến cuối
- Độ phức tạp: O(n)
- Thời gian tăng tuyến tính theo số lượng records

#### 2. Khi có Index

```sql
-- Có index trên cột age
SELECT * FROM users WHERE age = 25;
```

- Database sử dụng index để nhanh chóng định vị
- Độ phức tạp: O(log n)
- Thời gian tăng logarit theo số lượng records

### Ví dụ minh họa

```sql
-- Bảng users không có index
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    email VARCHAR(100)
);

-- Insert 1 triệu records
-- Query: SELECT * FROM users WHERE age = 25;
-- Phải scan 1 triệu rows → rất chậm

-- Tạo index
CREATE INDEX idx_age ON users(age);
-- Query tương tự giờ chỉ cần vài bước lookup → nhanh
```

## Các loại Index

### 1. Primary Index (Clustered Index)

```sql
-- Tự động tạo khi định nghĩa PRIMARY KEY
CREATE TABLE users (
    id INT PRIMARY KEY,  -- Clustered index
    name VARCHAR(100)
);
```

- Dữ liệu trong bảng được sắp xếp theo index này
- Mỗi bảng chỉ có 1 clustered index
- Rất nhanh cho range queries

### 2. Secondary Index (Non-Clustered Index)

```sql
-- Index riêng biệt, không ảnh hưởng đến thứ tự dữ liệu
CREATE INDEX idx_name ON users(name);
CREATE INDEX idx_email ON users(email);
```

### 3. Composite Index (Multi-column Index)

```sql
-- Index trên nhiều cột
CREATE INDEX idx_name_age ON users(name, age);
```

- Thứ tự cột quan trọng
- Hiệu quả cho queries có điều kiện trên cả 2 cột
- Cũng hiệu quả cho queries chỉ có điều kiện trên cột đầu tiên

### 4. Unique Index

```sql
CREATE UNIQUE INDEX idx_email_unique ON users(email);
```

- Đảm bảo tính duy nhất
- Tự động tạo khi có UNIQUE constraint

### 5. Partial Index

```sql
-- Chỉ index một phần dữ liệu thỏa mãn điều kiện
CREATE INDEX idx_active_users ON users(name) WHERE status = 'active';
```

### 6. Functional Index

```sql
-- Index trên kết quả của function
CREATE INDEX idx_lower_email ON users(LOWER(email));
```

## Cách đánh Index

### 1. Index đơn cột

```sql
-- Syntax cơ bản
CREATE INDEX index_name ON table_name(column_name);

-- Ví dụ cụ thể
CREATE INDEX idx_user_age ON users(age);
CREATE INDEX idx_user_email ON users(email);
```

### 2. Composite Index

```sql
-- Index nhiều cột
CREATE INDEX idx_user_name_age ON users(name, age);

-- Thứ tự quan trọng:
-- Query hiệu quả: WHERE name = 'John'
-- Query hiệu quả: WHERE name = 'John' AND age = 25
-- Query KHÔNG hiệu quả: WHERE age = 25 (thiếu cột đầu)
```

### 3. Index với thứ tự sắp xếp

```sql
-- Ascending (mặc định)
CREATE INDEX idx_user_age_asc ON users(age ASC);

-- Descending
CREATE INDEX idx_user_age_desc ON users(age DESC);

-- Mixed
CREATE INDEX idx_user_name_age_mixed ON users(name ASC, age DESC);
```

### 4. Tạo Index trong khi tạo bảng

```sql
CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    order_date DATE,
    total DECIMAL(10,2),

    INDEX idx_user_id (user_id),
    INDEX idx_order_date (order_date),
    INDEX idx_user_date (user_id, order_date)
);
```

## Khi nào cần đánh Index

### ✅ Nên đánh Index khi:

#### 1. Cột thường xuyên xuất hiện trong WHERE clause

```sql
-- Nếu thường query như này
SELECT * FROM users WHERE email = 'john@example.com';
-- Thì cần index: CREATE INDEX idx_email ON users(email);
```

#### 2. Cột được sử dụng để JOIN

```sql
-- Query JOIN thường xuyên
SELECT u.*, o.*
FROM users u
JOIN orders o ON u.id = o.user_id;
-- Cần index: CREATE INDEX idx_user_id ON orders(user_id);
```

#### 3. Cột được sử dụng trong ORDER BY

```sql
-- Query với ORDER BY
SELECT * FROM orders ORDER BY order_date DESC;
-- Cần index: CREATE INDEX idx_order_date ON orders(order_date);
```

#### 4. Cột được sử dụng trong GROUP BY

```sql
-- Query với GROUP BY
SELECT status, COUNT(*) FROM orders GROUP BY status;
-- Cần index: CREATE INDEX idx_status ON orders(status);
```

#### 5. Range queries thường xuyên

```sql
-- Query với range
SELECT * FROM orders WHERE order_date BETWEEN '2024-01-01' AND '2024-12-31';
-- Cần index: CREATE INDEX idx_order_date ON orders(order_date);
```

### ❌ Không nên đánh Index khi:

#### 1. Bảng có ít dữ liệu (< 1000 rows)

```sql
-- Bảng nhỏ, table scan nhanh hơn index scan
CREATE TABLE settings (
    id INT PRIMARY KEY,
    key VARCHAR(50),
    value VARCHAR(200)
);
-- Chỉ có vài chục rows → không cần thêm index
```

#### 2. Cột có tính selective thấp

```sql
-- Cột chỉ có 2-3 giá trị duy nhất
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    gender ENUM('male', 'female', 'other')  -- Không nên index
);
```

#### 3. Cột thường xuyên bị UPDATE

```sql
-- Cột được update liên tục
CREATE TABLE page_views (
    id INT PRIMARY KEY,
    page_url VARCHAR(200),
    view_count INT  -- Cột này thường xuyên thay đổi
);
-- Index trên view_count sẽ làm chậm UPDATE operations
```

#### 4. Bảng có tần suất INSERT/UPDATE/DELETE cao

```sql
-- Bảng log được insert liên tục
CREATE TABLE access_logs (
    id INT PRIMARY KEY,
    user_id INT,
    action VARCHAR(100),
    timestamp DATETIME
);
-- Quá nhiều index sẽ làm chậm INSERT
```

## Chiến lược Index tối ưu

### 1. Phân tích Query Patterns

```sql
-- Sử dụng EXPLAIN để phân tích
EXPLAIN SELECT * FROM users WHERE email = 'john@example.com';

-- Kết quả cho biết:
-- - Type: ALL (table scan) → cần index
-- - Type: ref (index scan) → đã có index tốt
-- - Rows: số lượng rows được examine
```

### 2. Composite Index Design

```sql
-- Query thường gặp
SELECT * FROM orders
WHERE user_id = 123
  AND status = 'pending'
  AND order_date > '2024-01-01';

-- Index tối ưu (thứ tự quan trọng)
CREATE INDEX idx_orders_optimal ON orders(user_id, status, order_date);

-- Nguyên tắc: cột có selectivity cao nhất đầu tiên
-- user_id (high selectivity) → status (medium) → order_date (range)
```

### 3. Index Covering

```sql
-- Query chỉ cần vài cột
SELECT name, email FROM users WHERE age = 25;

-- Covering index (chứa tất cả cột cần thiết)
CREATE INDEX idx_age_covering ON users(age, name, email);
-- Database không cần truy cập bảng gốc
```

### 4. Partial Index cho điều kiện đặc biệt

```sql
-- Chỉ quan tâm đến orders chưa hoàn thành
CREATE INDEX idx_pending_orders ON orders(user_id, order_date)
WHERE status IN ('pending', 'processing');
```

## Monitoring và Maintenance

### 1. Kiểm tra Index Usage

```sql
-- PostgreSQL
SELECT
    schemaname,
    tablename,
    indexname,
    idx_scan as index_scans,
    idx_tup_read as tuples_read,
    idx_tup_fetch as tuples_fetched
FROM pg_stat_user_indexes
ORDER BY idx_scan;

-- MySQL
SELECT
    OBJECT_NAME,
    INDEX_NAME,
    CARDINALITY,
    LAST_UPDATE
FROM information_schema.STATISTICS
WHERE TABLE_SCHEMA = 'your_database';
```

### 2. Tìm Index không sử dụng

```sql
-- Index ít được sử dụng → có thể xóa
SELECT indexname
FROM pg_stat_user_indexes
WHERE idx_scan < 10;
```

### 3. Rebuild Index định kỳ

```sql
-- Khi index bị fragmented
REINDEX INDEX idx_user_email;
REINDEX TABLE users;
```

## Best Practices

### 1. Thiết kế Index

- Tạo index dựa trên query patterns thực tế
- Ưu tiên cột có selectivity cao trong composite index
- Sử dụng covering index khi có thể
- Tránh over-indexing

### 2. Performance Considerations

```sql
-- Đo lường impact
-- Trước khi tạo index
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@test.com';

-- Sau khi tạo index
CREATE INDEX idx_email ON users(email);
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@test.com';
-- So sánh execution time và cost
```

### 3. Maintenance

- Monitor index usage định kỳ
- Drop unused indexes
- Rebuild fragmented indexes
- Update statistics thường xuyên

## Ví dụ thực tế

### E-commerce Database

```sql
CREATE TABLE products (
    id INT PRIMARY KEY,
    name VARCHAR(200),
    category_id INT,
    price DECIMAL(10,2),
    stock_quantity INT,
    created_at DATETIME,
    is_active BOOLEAN
);

-- Indexes cần thiết
CREATE INDEX idx_category ON products(category_id);              -- Filter by category
CREATE INDEX idx_price ON products(price);                      -- Price range queries
CREATE INDEX idx_active_category ON products(is_active, category_id); -- Active products by category
CREATE INDEX idx_created_at ON products(created_at);            -- Sort by date
CREATE INDEX idx_name_search ON products(name);                 -- Product search

-- Query examples
SELECT * FROM products WHERE category_id = 5 AND is_active = 1; -- Uses idx_active_category
SELECT * FROM products WHERE price BETWEEN 100 AND 500;         -- Uses idx_price
SELECT * FROM products WHERE name LIKE 'iPhone%';               -- Uses idx_name_search
```

Index là công cụ mạnh mẽ nhưng cần được sử dụng một cách thông minh. Hiểu rõ query patterns và đo lường performance là chìa khóa để tạo ra một index strategy hiệu quả.
