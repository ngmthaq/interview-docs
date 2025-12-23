# Chia state theo module thế nào?

- Domain-based store
- Tránh global store quá lớn

## Chi tiết câu trả lời

Organize state.

### Domain-based store

- Separate stores per domain.
- User store, product store.

### Tránh global store quá lớn

- Split into modules.
- Lazy load nếu cần.

Modular state maintainable.
