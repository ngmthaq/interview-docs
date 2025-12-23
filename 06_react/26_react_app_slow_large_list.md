# App React chậm khi render list lớn

- Virtualization (react-window)
- Memo
- Pagination

## Chi tiết câu trả lời

Optimize large lists.

### Virtualization

- Render only visible items.
- react-window: Windowing library.
- Performance cho 1000+ items.

### Memo

- React.memo prevent unnecessary re-renders.
- useMemo cho expensive computations.

### Pagination

- Load data in chunks.
- Infinite scroll hoặc page-based.

Combine techniques cho best performance.
