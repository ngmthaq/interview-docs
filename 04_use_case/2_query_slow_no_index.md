# Query rất chậm nhưng **không được thêm index**

- Rewrite query
- Giảm dữ liệu trả về
- Denormalize
- Cache kết quả

## Chi tiết câu trả lời

Khi query chậm nhưng không được thêm index, chúng ta cần tối ưu hóa theo các cách khác:

### 1. Rewrite Query

- Sử dụng JOIN thay vì subquery nếu phù hợp.
- Tránh SELECT \*, chỉ select các cột cần thiết.
- Sử dụng EXISTS thay vì IN cho subquery.
- Tối ưu WHERE clause: tránh function trên cột indexed (nếu có), sử dụng proper operators.

### 2. Giảm dữ liệu trả về

- Phân trang (LIMIT/OFFSET) để giảm số rows.
- Thêm filter chặt chẽ hơn trong WHERE.
- Sử dụng aggregate functions sớm để giảm data volume.

### 3. Denormalize

- Tạo bảng denormalized với data pre-computed.
- Thêm cột redundant để tránh JOIN phức tạp.
- Sử dụng materialized views nếu database hỗ trợ.

### 4. Cache kết quả

- Cache query results trong Redis/Memcached.
- Sử dụng application-level cache.
- Cache ở database level nếu có.

Kết hợp các phương pháp này có thể cải thiện performance đáng kể mà không cần index.
