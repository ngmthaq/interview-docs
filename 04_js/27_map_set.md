# 27. Map and Set vs objects and arrays. (Junior)

**`Map`** and **`Set`** are ES6 collections addressing limitations of plain objects/arrays.

**`Map`** — key/value pairs with **any key type** and insertion order:

```js
const map = new Map();
map.set("name", "Ada");
map.set(42, "number key");
map.set(obj, "object key"); // objects as keys — impossible with {}

map.get("name"); // "Ada"
map.has(42); // true
map.size; // 3
for (const [k, v] of map) { ... } // iterable
```

**`Set`** — unique values:

```js
const set = new Set([1, 2, 2, 3]);
set.size; // 3 (duplicates removed)
set.has(2); // true
[...new Set(array)]; // dedupe an array
```

**Map vs Object:**

- Map keys can be **any type** (objects, functions); object keys are strings/symbols.
- Map preserves **insertion order**, has a **`size`**, and is directly **iterable**.
- Map is optimized for **frequent additions/removals**; objects for structured records.

**Key point:** use `Map` for dictionaries with non-string keys, ordering, and frequent mutation (`size`, iterable); use `Set` for unique-value collections and deduping — both are iterable and often clearer than shoehorning data into `{}`/`[]`.
