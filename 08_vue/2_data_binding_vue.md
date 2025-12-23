# Data binding trong Vue hoạt động thế nào?

- One-way binding
- Two-way binding (`v-model`)
- Khi nào không nên dùng `v-model`

## Chi tiết câu trả lời

Data binding trong Vue.

### One-way binding

- Data → template: `{{ message }}`, `:prop="value"`
- Unidirectional, predictable.

### Two-way binding (`v-model`)

- Sync data và input: `v-model="message"`
- Shortcut cho `:value` + `@input`.

### Khi nào không nên dùng `v-model`

- Custom components phức tạp.
- Control manual flow.
- Performance-critical cases.

Use appropriately cho UX.
