# Render list lớn

- `key` trong `v-for`
- Virtual scroll
- Pagination

## Chi tiết câu trả lời

Optimize large lists.

### `key` trong `v-for`

- Unique key cho reconciliation.
- Avoid index nếu list changes.

### Virtual scroll

- Render visible items only.
- Libraries như vue-virtual-scroller.

### Pagination

- Load data in chunks.
- Reduce DOM size.

Virtual scroll best cho 1000+ items.
