# 19. How does `this` work in OOP (JavaScript)? (Mid)

`this` refers to the object a method is called **on** — but in JS it's determined by **how the function is called**, not where it's defined. This trips up many developers.

```ts
class Timer {
  seconds = 0;

  tick() {
    this.seconds++;
  }
}

const t = new Timer();
const fn = t.tick;
fn(); // ❌ `this` is undefined — call site lost the object
```

**Ways to keep `this` bound:**

```ts
// 1. Arrow function — captures `this` lexically (from surrounding scope)
class Timer {
  seconds = 0;
  tick = () => {
    this.seconds++;
  }; // always bound to the instance
}

// 2. Explicit bind
const bound = t.tick.bind(t);

// 3. Call it as a method: t.tick()
```

**Interview takeaway:** unlike Java/C# where `this` is always the enclosing object, JS `this` is dynamic. Arrow methods or `.bind()` are the usual fixes, especially for callbacks and event handlers.
