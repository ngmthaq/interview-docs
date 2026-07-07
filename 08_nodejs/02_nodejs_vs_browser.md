# 2. How does Node.js differ from browser JavaScript? (Fresher)

Both run JavaScript on V8, but the **environment and available APIs** differ.

| Aspect                       | Browser                 | Node.js                          |
| ---------------------------- | ----------------------- | -------------------------------- |
| Global object                | `window`                | `global` / `globalThis`          |
| DOM / `document`             | Yes                     | No                               |
| File system, network sockets | Restricted              | Full access (`fs`, `net`)        |
| Modules                      | ES Modules              | CommonJS + ES Modules            |
| APIs                         | `fetch`, `localStorage` | `process`, `Buffer`, `__dirname` |

```js
// Works only in Node — no DOM here
console.log(process.cwd()); // current working directory
console.log(__dirname); // folder of this file

// Works only in browser
// document.querySelector("#app");
```

**Key point:** the language is the same, but Node.js swaps browser/DOM APIs for server capabilities (file system, processes, networking) — code is not automatically portable between the two.
