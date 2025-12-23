# `v-if` vs `v-show`

- `v-if`: tạo / huỷ DOM
- `v-show`: CSS display
- Trade-off performance

## Chi tiết câu trả lời

Conditional rendering.

### `v-if`

- Create/destroy DOM elements.
- Expensive nếu toggle thường.

### `v-show`

- Toggle CSS display.
- DOM always present.

### Trade-off performance

- `v-if`: Better cho rare changes.
- `v-show`: Better cho frequent toggles.

Choose based on use case.
