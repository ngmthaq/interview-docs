# useMemo vs useCallback

- useMemo: memoize **giá trị**
- useCallback: memoize **function**
- Không dùng bừa → tăng complexity

## Chi tiết câu trả lời

Memoization hooks.

### useMemo

- Memoize expensive computation.
- Return cached value nếu deps không đổi.
- useMemo(() => computeValue, [deps])

### useCallback

- Memoize function reference.
- Prevent unnecessary re-renders của children.
- useCallback(() => func, [deps])

### Không dùng bừa

- Chỉ dùng khi performance issue.
- Memoization có cost (memory, comparison).
- Profile trước khi optimize.

useMemo cho values, useCallback cho functions.
