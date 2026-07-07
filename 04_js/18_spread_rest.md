# 18. Spread vs rest operator? (Junior)

Both use `...`, but do opposite things depending on context.

**Spread — expands** an iterable into individual elements.

```js
const arr = [1, 2, 3];
const copy = [...arr]; // shallow copy
const merged = [...arr, 4, 5]; // [1,2,3,4,5]

const obj = { a: 1 };
const clone = { ...obj, b: 2 }; // { a:1, b:2 }

Math.max(...arr); // 3 (spread into args)
```

**Rest — collects** multiple elements into one array/object.

```js
function sum(...nums) {
  // gather args into array
  return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3); // 6

const [first, ...others] = [1, 2, 3]; // others = [2,3]
const { id, ...rest } = user; // rest = everything except id
```

**Key distinction:**

- **Spread** = unpack (right side / call site).
- **Rest** = pack (function params / left side of destructuring).

**Note:** spread makes a **shallow** copy — nested objects are still shared by reference.
