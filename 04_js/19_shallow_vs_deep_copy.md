# 19. Shallow copy vs deep copy? (Mid)

- **Shallow copy** — copies top-level properties; nested objects are still **shared by reference**.
- **Deep copy** — recursively copies everything; fully independent.

```js
const original = { name: "Ann", address: { city: "NYC" } };

// Shallow
const shallow = { ...original };
shallow.address.city = "LA";
console.log(original.address.city); // 'LA' — nested object shared! ⚠️

// Deep
const deep = structuredClone(original);
deep.address.city = "SF";
console.log(original.address.city); // unchanged ✅
```

**Ways to deep copy:**

```js
structuredClone(obj); // ✅ modern, handles Dates/Maps/etc.
JSON.parse(JSON.stringify(obj)); // ⚠️ loses functions, Dates, undefined, symbols
// or a library like lodash.cloneDeep
```

| Method                       | Depth   | Notes                |
| ---------------------------- | ------- | -------------------- |
| `{...obj}` / `Object.assign` | Shallow | Fast, nested shared  |
| `JSON` round-trip            | Deep    | Loses special types  |
| `structuredClone`            | Deep    | Best built-in option |

**Key point:** spread/`Object.assign` are shallow — a common source of bugs when mutating nested state (e.g. in React/Redux).
