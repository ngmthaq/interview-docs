# 2. == vs === ? (Fresher)

- **`===`** (strict) — compares value **and** type, no conversion.
- **`==`** (loose) — performs **type coercion** before comparing.

```js
5 === "5"; // false (number vs string)
5 == "5"; // true  ('5' coerced to 5)

0 == false; // true  (coercion)
0 === false; // false

null == undefined; // true
null === undefined; // false
```

**Tricky coercions to know:**

```js
"" == 0; // true
[] == false; // true
null == 0; // false (special rule)
NaN == NaN; // false (NaN never equals itself)
```

**Rule:** always use **`===`** to avoid surprising coercion bugs. The one common exception: `x == null` is a handy way to check for **both** `null` and `undefined` at once.
