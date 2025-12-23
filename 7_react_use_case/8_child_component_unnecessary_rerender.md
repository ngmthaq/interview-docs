# Component con không cần re-render nhưng vẫn render lại

- Props reference thay đổi
- useCallback
- useMemo cho object / array props

## Chi tiết câu trả lời

Prevent unnecessary child re-renders.

### Props reference thay đổi

- Objects/arrays recreated mỗi render.
- Child see new reference, re-render.

### useCallback

- Memoize function props.
- Prevent child re-render nếu function same.

### useMemo cho object / array props

- Memoize object/array props.
- Stable references.

Fix prop stability.
