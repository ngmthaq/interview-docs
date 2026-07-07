# 1. What is React and the Virtual DOM? (Fresher)

React is a **declarative, component-based** library for building UIs. You describe **what** the UI should look like for a given state, and React figures out **how** to update the DOM.

**Virtual DOM** — a lightweight JavaScript representation of the real DOM. On each state change React:

1. Builds a new virtual DOM tree.
2. **Diffs** it against the previous one (reconciliation).
3. Applies the **minimal set** of real DOM mutations.

```tsx
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

You never call `document.getElementById` or manually patch nodes — you change state, React re-renders.

**Why it matters:**

- **Declarative** — UI is a function of state; easier to reason about than imperative DOM code.
- **Efficient** — batched, minimal DOM updates.
- **Composable** — build complex UIs from small, reusable components.

**Note:** the real DOM is slow to mutate; diffing in JS memory first and batching the writes is what makes React fast.
