# `ref` vs `reactive`

- `ref`: primitive, đơn giá trị
- `reactive`: object
- `.value` hoạt động thế nào?

## Chi tiết câu trả lời

Reactive primitives.

### `ref`

- Wrap primitive values.
- Access via `.value`.
- Auto-unwrap in template.

### `reactive`

- Make object reactive.
- Direct access properties.
- Deep reactivity.

### `.value` hoạt động thế nào?

- Proxy access reactive value.
- Vue track dependencies.
- Trigger updates.

Choose based on data type.
