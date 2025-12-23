# So sánh fetch thuần vs React Query / SWR

- Cache
- Revalidate
- Background refetch

## Chi tiết câu trả lời

Fetch thuần vs data fetching libraries.

### Fetch thuần

- Manual: useEffect, state management.
- No cache, error handling basic.
- Boilerplate code.

### React Query / SWR

- **Cache**: Automatic caching, stale-while-revalidate.
- **Revalidate**: Background refetch, focus revalidate.
- **Background refetch**: Update data silently.

Libraries reduce boilerplate, handle edge cases.
