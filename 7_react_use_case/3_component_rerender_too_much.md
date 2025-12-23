# Component re-render quá nhiều

- Xác định nguyên nhân
- React DevTools Profiler
- React.memo / useCallback / useMemo

## Chi tiết câu trả lời

Debug và fix excessive re-renders.

### Xác định nguyên nhân

- Props change, state change, parent re-render.
- Console.log trong render.

### React DevTools Profiler

- Record performance.
- See render counts, time.
- Identify bottlenecks.

### React.memo / useCallback / useMemo

- React.memo prevent re-render nếu props same.
- useCallback memoize functions.
- useMemo memoize values.

Profile trước, optimize sau.
