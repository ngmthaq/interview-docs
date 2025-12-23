# Debounce / Throttle trong React

- Search box
- Scroll / resize
- Kết hợp useCallback + useRef

## Chi tiết câu trả lời

Debounce/throttle optimize frequent events.

### Debounce

- Delay execution cho đến khi stop triggering.
- Ví dụ: Search input, wait user stop typing.

### Throttle

- Limit execution rate.
- Ví dụ: Scroll handler, execute mỗi 100ms.

### Kết hợp useCallback + useRef

- useRef store debounce/throttle function.
- useCallback memoize để tránh recreate.
- Cleanup trong useEffect nếu cần.

Implement với lodash hoặc custom functions.
