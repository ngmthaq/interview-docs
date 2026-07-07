# 22. Explain truthy/falsy and type coercion. (Junior)

**Falsy values** (only 8) — everything else is truthy:

```js
(false, 0, -0, 0n, "", null, undefined, NaN);
```

```js
if ("") {
} // skipped (falsy)
if ("0") {
} // runs — non-empty string is truthy
if ([]) {
} // runs — empty array is truthy!
if ({}) {
} // runs — objects are always truthy
```

**Type coercion — implicit conversion:**

```js
"5" + 1; // '51'  (+ with string → concatenation)
"5" - 1; // 4     (- forces numeric)
"5" * "2"; // 10
true + 1; // 2     (true → 1)
[] + {}; // '[object Object]'
```

**The `+` operator** favors string concatenation if either operand is a string; other math operators coerce to number.

**Safe conversions (be explicit):**

```js
Number("5"); // 5
String(5); // '5'
Boolean(0); // false
parseInt("5px", 10); // 5
```

**Key point:** understand falsy values and that `+` concatenates with strings. Prefer **explicit conversion** over relying on coercion.
