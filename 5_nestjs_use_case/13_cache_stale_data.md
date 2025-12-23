# Cache bị stale data

- Cache eviction
- Write-through vs Write-around
- Khi nào chấp nhận eventual consistency

## Chi tiết câu trả lời

Handle stale cache data.

### Cache eviction

- TTL expiry.
- Manual invalidate on update.
- LRU for memory cache.

### Write-through vs Write-around

- **Write-through**: Update DB và cache cùng lúc.
- **Write-around**: Update DB, invalidate cache.
- Write-through đảm bảo consistency, chậm hơn.

### Khi nào chấp nhận eventual consistency

- Non-critical data (news feed).
- High read/write ratio.
- User tolerate slight staleness.

Monitor cache hit rate, adjust strategy.