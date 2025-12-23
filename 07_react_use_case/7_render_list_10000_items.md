# Render danh sách 10.000 item

- Virtualization (react-window)
- Pagination
- Memo hóa item

## Chi tiết câu trả lời

Optimize large list rendering.

### Virtualization

- Render only visible items.
- react-window: Efficient scrolling.

### Pagination

- Load data in pages.
- Reduce DOM nodes.

### Memo hóa item

- React.memo cho item components.
- useMemo cho expensive computations.

Virtualization best cho very large lists.
