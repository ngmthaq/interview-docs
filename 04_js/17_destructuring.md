# 17. What is destructuring? (Fresher → Junior)

**Destructuring** unpacks values from arrays or properties from objects into variables.

```js
// Array
const [first, second] = [1, 2]; // first=1, second=2
const [a, , c] = [1, 2, 3]; // skip elements: a=1, c=3
const [head, ...tail] = [1, 2, 3]; // head=1, tail=[2,3]

// Object
const { name, age } = { name: "Ann", age: 30 };
const { name: n } = user; // rename → n
const { role = "user" } = {}; // default value
```

**Nested & function params:**

```js
const {
  address: { city },
} = user; // nested

function greet({ name, greeting = "Hi" }) {
  return `${greeting}, ${name}`;
}
greet({ name: "Bob" }); // 'Hi, Bob'
```

**Swap without a temp variable:**

```js
let x = 1,
  y = 2;
[x, y] = [y, x]; // x=2, y=1
```

**Key point:** destructuring makes extracting values concise and is heavily used in function parameters, React props, and module imports.
