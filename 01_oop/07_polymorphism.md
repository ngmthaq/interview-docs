# 7. Explain polymorphism with a real example. (Mid)

Polymorphism lets you call the same method on different types and get type-specific behavior — without knowing the concrete type.

```ts
interface Shape {
  area(): number;
}

class Circle implements Shape {
  constructor(private r: number) {}
  area() { return Math.PI * this.r ** 2; }
}

class Square implements Shape {
  constructor(private s: number) {}
  area() { return this.s ** 2; }
}

function totalArea(shapes: Shape[]) {
  return shapes.reduce((sum, s) => sum + s.area(), 0);
}
```

`totalArea` works for **any** shape, present or future — adding a new shape requires **zero changes** to it. That's the Open/Closed Principle in action.
