# Một API bị gọi quá nhiều, gây load DB

- CacheInterceptor
- TTL
- Cache key strategy

## Chi tiết câu trả lời

Cache để reduce DB load.

### CacheInterceptor

- Built-in interceptor cache response.
- @UseInterceptors(CacheInterceptor)
- Global hoặc per route.

### TTL

- Time To Live: Cache expiry time.
- Set per key hoặc global.
- Balance freshness vs performance.

### Cache key strategy

- Default: URL + params.
- Custom: Include user ID, locale.
- Hash complex keys.
- Invalidate wisely.

Sử dụng Redis store cho distributed cache.