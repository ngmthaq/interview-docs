# Derived state nên đặt ở đâu?

- `computed`
- Không dùng `watch` để tính toán dữ liệu

## Chi tiết câu trả lời

Derived state placement.

### `computed`

- Cache, efficient.
- Reactive dependency.

### Không dùng `watch` để tính toán dữ liệu

- Watch cho side-effects.
- Computed cho derived values.

Computed best practice.
