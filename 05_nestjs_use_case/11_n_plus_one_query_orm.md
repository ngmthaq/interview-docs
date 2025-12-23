# N+1 query khi dùng ORM

- Dấu hiệu
- `leftJoinAndSelect`
- Eager vs Lazy loading

## Chi tiết câu trả lời

N+1 query problem với ORM.

### Dấu hiệu

- Nhiều queries thay vì một.
- Ví dụ: Load users, then N queries for each user's posts.
- Slow performance, high DB load.

### leftJoinAndSelect

- Eager load relations trong một query.
- relations: ['posts'] trong find options.
- Trade-off: Load unnecessary data.

### Eager vs Lazy loading

- **Eager**: Load tất cả relations upfront.
- **Lazy**: Load on access (via proxy).
- Eager tránh N+1 nhưng có thể over-fetch.
- Lazy tránh over-fetch nhưng có thể N+1 nếu không cẩn thận.

Sử dụng dataloader hoặc batch loading để optimize.