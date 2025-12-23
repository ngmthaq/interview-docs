# Reactive object thay đổi nhưng UI không update

- Nguyên nhân:
  - Mất reactive khi destructuring
  - Dùng sai `ref` / `reactive`
- Giải pháp:
  - `toRefs`
  - `computed`

## Chi tiết câu trả lời

Reactive update issues.

### Nguyên nhân

- Destructuring mất reactivity.
- Mutate non-reactive object.

### Giải pháp

- `toRefs`: Preserve reactivity.
- `computed`: Derived state.

Always use reactive primitives correctly.
