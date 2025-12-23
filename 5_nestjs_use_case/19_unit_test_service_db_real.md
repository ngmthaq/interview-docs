# Unit test service nhưng dính DB thật

- Mock repository
- Testing module
- In-memory DB khi nào cần

## Chi tiết câu trả lời

Unit test without real DB.

### Mock repository

- Use jest.mock() hoặc @nestjs/testing.
- Mock repository methods.
- Test logic isolated.

### Testing module

- Test.createTestingModule().
- Override providers với mocks.
- Fast, isolated tests.

### In-memory DB khi nào cần

- Integration tests.
- Test real DB interactions.
- Use sqlite hoặc testcontainers.

Unit tests nên mock DB, integration test real DB.