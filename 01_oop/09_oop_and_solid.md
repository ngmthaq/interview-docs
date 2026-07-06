# 9. How do OOP principles relate to SOLID? (Senior)

SOLID is a set of design principles built **on top of** OOP to keep systems maintainable:

- **S** — Single Responsibility: one class, one reason to change (cohesion).
- **O** — Open/Closed: open to extension, closed to modification (polymorphism).
- **L** — Liskov Substitution: a subclass must be usable anywhere its parent is (correct inheritance).
- **I** — Interface Segregation: many small interfaces > one fat interface.
- **D** — Dependency Inversion: depend on abstractions, not concretions.

**Interview framing:** OOP gives you the *tools* (encapsulation, polymorphism, abstraction); SOLID tells you *how to use them well* so code stays extensible and testable.
