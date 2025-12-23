# XSS trong Vue có xảy ra không?

- Template auto-escape
- Nguy hiểm với `v-html`

## Chi tiết câu trả lời

XSS in Vue.

### Template auto-escape

- Safe by default.
- HTML escaped.

### Nguy hiểm với `v-html`

- Raw HTML injection.
- Sanitize input.

Vue secure if used correctly.
