# 3. Function vs class components? (Fresher)

Both produce UI; **function components + hooks** are the modern standard.

```tsx
// Function component (preferred)
function Hello({ name }: { name: string }) {
  const [count, setCount] = useState(0);
  return (
    <p>
      {name}: {count}
    </p>
  );
}

// Class component (legacy)
class Hello extends React.Component<{ name: string }, { count: number }> {
  state = { count: 0 };
  render() {
    return (
      <p>
        {this.props.name}: {this.state.count}
      </p>
    );
  }
}
```

|                | Function                  | Class                     |
| -------------- | ------------------------- | ------------------------- |
| State          | `useState` / `useReducer` | `this.state` / `setState` |
| Side effects   | `useEffect`               | lifecycle methods         |
| `this` binding | none                      | must bind handlers        |
| Boilerplate    | minimal                   | more                      |
| Logic reuse    | custom hooks              | HOCs / render props       |

**Why function components won:**

- **Hooks** allow state & side effects without classes.
- No confusing `this`.
- Easier to **extract and share logic** (custom hooks vs HOC wrapper hell).
- Less code.

**Rule:** write new components as functions. Classes are only for legacy code or the rare case that needs an error boundary (still class-only as of React 18).
