# 18. Prototypal vs classical inheritance — how does JS differ? (Mid)

**Classical inheritance** (Java, C#): classes inherit from classes; objects are instances of classes.

**Prototypal inheritance** (JavaScript's real model): objects inherit directly from **other objects** via the **prototype chain**. The `class` keyword is _syntactic sugar_ over this.

```ts
const animal = {
  speak() {
    return "some sound";
  },
};

const dog = Object.create(animal); // dog's prototype IS animal
dog.speak(); // 'some sound' — found on the prototype chain
```

When you call `dog.speak()`, JS looks on `dog`, then walks up the prototype chain until it finds `speak`.

```ts
// class syntax compiles down to prototype wiring
class Animal {
  speak() {
    return "sound";
  }
}
class Dog extends Animal {}
// Dog.prototype.__proto__ === Animal.prototype
```

**Key point:** in JS there are no "real" classes under the hood — everything is objects linked to prototypes. Knowing this explains method resolution, `instanceof`, and monkey-patching.
