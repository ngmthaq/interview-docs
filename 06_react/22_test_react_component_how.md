# Test component React thế nào?

- Unit test: Jest
- UI test: React Testing Library
- Không test implementation detail

## Chi tiết câu trả lời

Testing React components.

### Unit test

- Test logic isolated.
- Jest + mocking.

### UI test

- Test user interactions.
- React Testing Library: Query elements như user sees.
- Avoid enzyme (implementation detail).

### Không test implementation detail

- Test behavior, not internals.
- Refactor không break tests.

Integration tests cho component interactions.
