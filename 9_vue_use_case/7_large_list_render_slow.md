# List lớn (5.000–10.000 item) render chậm

- `key` đúng
- Virtual scroll
- Pagination

## Chi tiết câu trả lời

Large list rendering.

### `key` đúng

- Unique, stable key.
- Avoid index.

### Virtual scroll

- Render visible items.
- Libraries like vue-virtual-scroller.

### Pagination

- Load chunks.
- Reduce DOM size.

Virtual scroll best for large lists.
