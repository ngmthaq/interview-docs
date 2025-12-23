# Một service quá nhiều if/else theo loại nghiệp vụ

- Strategy pattern
- Polymorphism
- State pattern

## Chi tiết câu trả lời

Để refactor nhiều if/else theo business type:

### 1. Strategy Pattern

- Define strategy interface.
- Implement concrete strategies cho mỗi type.
- Use factory để select strategy.
- Ưu điểm: Open for extension, clean code.

### 2. Polymorphism

- Create base class/abstract class.
- Subclass cho mỗi business type.
- Override methods.
- Ưu điểm: OOP principles, easy maintenance.

### 3. State Pattern

- Model states as classes.
- Transition between states.
- Ưu điểm: Handle complex state logic.

Refactor gradually, test thoroughly.
