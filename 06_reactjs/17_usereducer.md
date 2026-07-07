# 17. `useReducer` — when over `useState`? (Mid)

`useReducer` manages state via a **reducer function** `(state, action) => newState` — the same pattern as Redux, built in.

```tsx
type State = { count: number };
type Action = { type: "inc" } | { type: "reset" };

function reducer(state: State, action: Action): State {
  switch (action.type) {
    case "inc":
      return { count: state.count + 1 };
    case "reset":
      return { count: 0 };
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  return <button onClick={() => dispatch({ type: "inc" })}>{state.count}</button>;
}
```

**Prefer `useReducer` when:**

- State has **multiple sub-values** that change together.
- **Next state depends on previous** in complex ways.
- Update logic is involved enough to **test in isolation** (the reducer is a pure function).
- Many handlers mutate the same state — `dispatch` centralizes the logic.

**`useState` vs `useReducer`:**

|             | `useState`          | `useReducer`                 |
| ----------- | ------------------- | ---------------------------- |
| Best for    | simple, independent | complex, related transitions |
| Logic       | inline in handlers  | centralized in reducer       |
| Testability | ad hoc              | reducer is pure & testable   |

**Bonus:** `dispatch` has a **stable identity**, so it's safe to pass down (via Context) without breaking memoized children.
