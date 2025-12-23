# Key trong list để làm gì?

- Giúp React reconcile chính xác
- Không dùng index làm key khi list thay đổi

## Chi tiết câu trả lời

Key trong list rendering.

### Giúp React reconcile

- Key giúp React identify items trong list.
- Khi list thay đổi, React dùng key để match old/new items.
- Tối ưu re-rendering, animations.

### Không dùng index làm key

- Index thay đổi khi insert/delete, gây re-render sai.
- React có thể reuse components sai, mất state.
- Dùng unique ID từ data (user.id, product.sku).

Key stable và unique đảm bảo correct reconciliation.
