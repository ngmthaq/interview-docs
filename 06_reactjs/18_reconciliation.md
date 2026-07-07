# 18. Reconciliation and the diffing algorithm? (Senior)

**Reconciliation** is how React decides what DOM to change when state updates. It diffs the new element tree against the previous one and applies the minimum mutations.

A naive tree diff is O(n³). React uses **heuristics** to get O(n):

**1. Different element types → replace the whole subtree.**

```tsx
<div><Counter /></div>   →   <span><Counter /></span>
// div → span: React destroys the old tree (Counter unmounts) and rebuilds
```

**2. Same type → keep the node, update changed props**, then recurse into children.

**3. Lists are matched by `key`** — keys let React detect moves/inserts/removes instead of re-creating rows (see keys question).

**Fiber architecture (React 16+):** the reconciler was rewritten to be **incremental**. Work is split into units that can be **paused, resumed, and prioritized**, so rendering doesn't block the main thread. This enables **concurrent features** (transitions, `useDeferredValue`, Suspense).

**Two phases:**

- **Render/reconcile** — build the work-in-progress fiber tree, compute diffs. Interruptible, no DOM changes.
- **Commit** — apply the diffs to the DOM. Synchronous, not interruptible.

**Practical implications:**

- Stable **keys** and stable **component types** = efficient diffing.
- Changing a component's position/type unnecessarily throws away its state.
- Purity in render matters — React may call render multiple times or discard results.
