# 26. What are generators and iterators? (Mid)

An **iterator** is an object with a `next()` method returning `{ value, done }`. A **generator** is a function (`function*`) that produces an iterator, pausing at each **`yield`**.

```js
function* idGenerator() {
  let id = 1;
  while (true) {
    yield id++; // pauses here, resumes on next()
  }
}

const gen = idGenerator();
gen.next().value; // 1
gen.next().value; // 2
```

**The iterable protocol** — anything with `[Symbol.iterator]` works with `for...of` and spread:

```js
const range = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
    yield 3;
  },
};
[...range]; // [1, 2, 3]
for (const n of range) console.log(n);
```

**Use cases:**

- **Lazy sequences** — produce values on demand (infinite streams, pagination).
- **Custom iteration** for your own data structures.
- Generators can also **receive** values via `next(value)` and delegate with `yield*`.

**Key point:** iterators expose `next() → { value, done }`; generators (`function*` + `yield`) create them with pausable, lazy execution — implement `[Symbol.iterator]` to make objects iterable with `for...of`/spread, ideal for on-demand and infinite sequences.
