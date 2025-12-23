# Component re-render quá nhiều

- Reactive dependency thừa
- Tránh `deep watch`
- Dùng `computed` thay `watch`

## Chi tiết câu trả lời

Excessive re-renders.

### Reactive dependency thừa

- Only track needed.
- Avoid unnecessary reactivity.

### Tránh `deep watch`

- Expensive.
- Use shallow if possible.

### Dùng `computed` thay `watch`

- Cached, efficient.

Profile and optimize.
