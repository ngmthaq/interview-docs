# Computed vs Watch

- Computed: derived state, cache
- Watch: side-effect, async
- Không dùng watch để thay computed

## Chi tiết câu trả lời

Computed và watch trong Vue.

### Computed

- Tính toán từ reactive data.
- Cache, chỉ re-compute khi dependency change.
- Sync, return value.

### Watch

- Observe data change.
- Run side-effect, async operations.
- Không return value.

### Không dùng watch để thay computed

- Computed cho derived values.
- Watch cho effects như API calls.
- Computed efficient hơn cho UI.

Use computed cho performance.
