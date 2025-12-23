# Khi nào component re-render?

- State change
- Props change
- Parent re-render

## Chi tiết câu trả lời

Triggers cho re-render.

### State change

- setState hoặc useState setter.
- Trigger re-render component đó và descendants.

### Props change

- Parent pass new props.
- Reference change (objects/arrays) trigger re-render.

### Parent re-render

- Parent re-render → children re-render mặc định.
- React.memo hoặc shouldComponentUpdate optimize.

Re-render không luôn mean DOM update; React diff Virtual DOM.
