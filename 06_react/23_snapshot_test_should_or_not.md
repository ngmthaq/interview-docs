# Snapshot test nên hay không?

- Dùng cho UI ổn định
- Không lạm dụng

## Chi tiết câu trả lời

Snapshot testing.

### Dùng cho UI ổn định

- Capture component output.
- Detect unexpected changes.
- Good cho presentational components.

### Không lạm dụng

- Not catch logic bugs.
- Brittle: Update often.
- Supplement, not replace unit tests.

Use sparingly cho stable UI.
