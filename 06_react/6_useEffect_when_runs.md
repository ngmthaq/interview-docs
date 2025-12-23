# useEffect chạy khi nào?

- Dependency array
- Cleanup function dùng khi nào?
- Lỗi phổ biến: infinite loop

## Chi tiết câu trả lời

useEffect cho side effects.

### Dependency array

- []: Chạy một lần after mount.
- [deps]: Chạy khi deps thay đổi.
- Không có: Chạy mỗi render (avoid).

### Cleanup function

- Return function từ useEffect.
- Chạy before unmount hoặc before next effect.
- Dùng cho: Clear timers, cancel requests, remove listeners.

### Lỗi phổ biến: infinite loop

- Quên dependency array.
- Object/array trong deps tạo reference mới mỗi render.
- Fix: useCallback, useMemo, hoặc move outside.

useEffect chạy after render, non-blocking.
