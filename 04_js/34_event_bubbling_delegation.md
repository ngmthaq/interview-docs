# 34. Explain event bubbling, capturing, and delegation. (Mid)

When an event fires on an element, it travels through the DOM in **three phases**:

1. **Capturing** — from `document` down to the target.
2. **Target** — the element itself.
3. **Bubbling** — back up from the target to `document` (the default phase listeners fire in).

```js
// Default: bubbling phase
child.addEventListener("click", handler);

// Opt into the capturing phase:
parent.addEventListener("click", handler, { capture: true });

// Stop propagation
e.stopPropagation(); // halt further bubbling/capturing
```

**Event delegation** — leverage bubbling to handle many children with **one listener** on a parent:

```js
// Instead of a listener per <li>, one on the <ul>:
list.addEventListener("click", (e) => {
  const li = e.target.closest("li");
  if (li) console.log("Clicked", li.dataset.id);
});
```

**Why delegation is useful:**

- **Fewer listeners** → less memory, better performance.
- **Works for dynamically added elements** — no need to re-bind when children change.

**Key point:** events capture down then bubble up through the DOM; delegation attaches a single listener to a common ancestor and uses `e.target`/`closest()` to handle events from many (including dynamically added) children — fewer listeners, better performance.
