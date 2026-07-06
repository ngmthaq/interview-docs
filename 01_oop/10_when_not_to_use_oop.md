# 10. When would you NOT use OOP? What are its trade-offs? (Senior)

A senior answer shows OOP isn't a silver bullet.

**When OOP may be overkill:**
- Simple scripts / data-transformation pipelines → functional style is cleaner.
- Highly concurrent systems → mutable shared object state causes race conditions; immutability (functional) is safer.
- Performance-critical / data-oriented code → object graphs add indirection and cache-unfriendly memory layout.

**Trade-offs of OOP:**
- Over-abstraction: too many layers, interfaces, and indirection ("enterprise" bloat).
- Deep inheritance trees become fragile and hard to reason about.
- Mutable state makes concurrency harder.

**Balanced take:** Modern codebases are usually **multi-paradigm** — OOP for domain modeling and boundaries, functional style for data flow and pure logic. Pick the paradigm that makes the specific problem simplest.
