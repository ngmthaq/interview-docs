# Response lỗi cần trả về enum code để frontend xử lý i18n

- Custom exception
- Global filter
- Chuẩn hoá error response

## Chi tiết câu trả lời

Error response với enum code cho i18n.

### Custom exception

- Tạo exception class với errorCode enum.
- Ví dụ: new BusinessException(ErrorCode.INSUFFICIENT_FUNDS)

### Global filter

- Global exception filter catch tất cả.
- Map exception sang standardized response.
- Include errorCode cho frontend translate.

### Chuẩn hoá error response

- Response format: { success: false, errorCode: 'INSUFFICIENT_FUNDS', message: '...' }
- Frontend dùng errorCode để show localized message.
- Consistent across APIs.

Giúp frontend handle errors flexibly.