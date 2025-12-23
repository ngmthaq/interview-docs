# Chuyển trang nhưng vẫn giữ state cũ

- URL query
- Global state
- localStorage / sessionStorage

## Chi tiết câu trả lời

Persist state across navigation.

### URL query

- Store state in URL params.
- Shareable, bookmarkable.

### Global state

- Redux/Zustand persist state.
- Survive navigation.

### localStorage / sessionStorage

- Persist to browser storage.
- Survive page refresh.

Choose based on persistence needs.
