# Thêm feature mới nhưng sợ phá code cũ

- Open/Closed Principle
- Feature flag
- Regression test

## Chi tiết câu trả lời

Để add feature an toàn:

### 1. Open/Closed Principle

- Design code open for extension, closed for modification.
- Use inheritance, composition.
- Ưu điểm: Minimal changes to existing code.

### 2. Feature Flag

- Wrap new feature behind flag.
- Enable gradually, monitor.
- Ưu điểm: Easy rollback, A/B testing.

### 3. Regression Test

- Comprehensive test suite.
- Run tests before/after changes.
- Use CI/CD for automated testing.
- Ưu điểm: Catch breaking changes early.

Code review, pair programming cũng giúp.
