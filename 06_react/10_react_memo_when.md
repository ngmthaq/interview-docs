# React.memo dùng khi nào?

- Component pure
- Props ổn định
- Không hiệu quả nếu props luôn thay đổi

## Chi tiết câu trả lời

React.memo optimize re-renders.

### Component pure

- Output chỉ phụ thuộc props.
- Không side effects, không internal state.

### Props ổn định

- Props không thay đổi thường xuyên.
- Shallow comparison đủ.

### Không hiệu quả nếu props luôn thay đổi

- Nếu props object/array mới mỗi render, memo vô ích.
- Cost của comparison > benefit.
- Use khi props stable hoặc custom compare function.

React.memo shallow compare props; use callback cho deep compare.
