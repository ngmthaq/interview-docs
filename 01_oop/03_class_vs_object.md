# 3. Difference between a Class and an Object? (Fresher)

- **Class** = the blueprint / template. It defines structure and behavior.
- **Object** = a concrete instance created from that class, with its own state.

```ts
class Car {
  constructor(public color: string) {}
}

const redCar = new Car('red');   // object
const blueCar = new Car('blue'); // another object
```

One class → many objects, each with independent state.
