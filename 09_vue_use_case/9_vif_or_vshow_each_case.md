# `v-if` hay `v-show` trong từng trường hợp?

- `v-if`: condition hiếm thay đổi
- `v-show`: toggle thường xuyên

## Chi tiết câu trả lời

Conditional rendering choice.

### `v-if`

- Rare changes.
- Destroy/create DOM.

### `v-show`

- Frequent toggles.
- CSS display toggle.

Choose based on frequency.
