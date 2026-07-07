# 9. Explain prototypes and prototypal inheritance. (Mid)

Every JS object has an internal link (`[[Prototype]]`, accessed via `__proto__`) to another object — its **prototype**. When you access a property, JS walks up this **prototype chain** until it finds it.

```js
const animal = {
  speak() {
    return "sound";
  },
};
const dog = Object.create(animal); // dog's prototype is animal
dog.speak(); // 'sound' — found on prototype
```

**Constructor functions & `.prototype`:**

```js
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function () {
  return `${this.name} speaks`;
};

const cat = new Animal("Cat");
cat.speak(); // 'Cat speaks' — method lives on Animal.prototype (shared, not copied)
```

**`class` is syntactic sugar** over this:

```js
class Dog {
  speak() {
    return "woof";
  }
}
// Dog.prototype.speak is the actual method
```

**Key point:** JS inheritance is **prototypal** — objects delegate to other objects via the prototype chain. Methods are stored once on the prototype and shared, not duplicated per instance.
