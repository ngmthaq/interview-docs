# 17. Static vs instance members — what's the difference? (Junior → Mid)

- **Instance members** belong to a specific object; each instance has its own copy.
- **Static members** belong to the **class itself**, shared across all instances.

```ts
class User {
  static count = 0;          // shared by the whole class
  id: number;                // unique per instance

  constructor() {
    User.count++;            // access via class name
    this.id = User.count;    // access via instance
  }

  static reset() { User.count = 0; } // utility, no instance needed
}

new User(); new User();
console.log(User.count); // 2
```

**Use static for:**
- Counters / shared config
- Factory methods (`User.fromJSON(...)`)
- Pure utility helpers that don't need instance state

**Rule:** if a method doesn't use `this`, it's a candidate to be `static`.
