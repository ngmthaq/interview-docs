# Props & Emit

- Props là read-only
- Emit event ngược lên cha
- Anti-pattern: mutate props

## Chi tiết câu trả lời

Props và emit trong Vue.

### Props là read-only

- Cha pass data xuống con.
- Con không mutate trực tiếp.
- Use emit để communicate ngược.

### Emit event ngược lên cha

- `$emit('event', data)`
- Cha listen `@event="handler"`

### Anti-pattern: mutate props

- Gây unpredictable behavior.
- Use local copy hoặc emit.
- Follow one-way data flow.

Props down, events up.
