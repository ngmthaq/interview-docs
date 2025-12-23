# Code khó test, phụ thuộc DB / external service

- Dependency Injection
- Interface / abstraction
- Mock / stub

## Chi tiết câu trả lời

Để làm code dễ test hơn:

### 1. Dependency Injection

- Inject dependencies (DB, services) qua constructor.
- Use DI containers (Spring, etc.).
- Ưu điểm: Easy mocking, loose coupling.

### 2. Interface / Abstraction

- Define interfaces cho external dependencies.
- Code against interfaces, not implementations.
- Ưu điểm: Testable, flexible.

### 3. Mock / Stub

- Use mocking frameworks (Mockito, Jest).
- Mock external calls, stub responses.
- Ưu điểm: Fast, isolated tests.

Write unit tests cho logic, integration tests cho external deps.
