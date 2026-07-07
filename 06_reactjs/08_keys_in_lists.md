# 8. Why are `key`s needed in lists? (Fresher)

When rendering a list, React uses `key` to **identify which items changed, were added, or removed** during reconciliation. Keys let React match old and new elements instead of rebuilding everything.

```tsx
{
  users.map((u) => <li key={u.id}>{u.name}</li>);
}
```

**Keys must be:**

- **Stable** — same item → same key across renders.
- **Unique** among siblings.
- Ideally a **domain id**, not derived from render order.

**Why not the array index?** Index keys break when the list is reordered, filtered, or items are inserted — React reuses the wrong DOM node, causing bugs with input state and animations:

```tsx
{
  items.map((it, i) => <Input key={i} />);
} // ❌ breaks on reorder/insert
{
  items.map((it) => <Input key={it.id} />);
} // ✅ stable identity
```

**Index is acceptable only if** the list is static, never reordered, and items have no state/id.

**What goes wrong without keys:** React falls back to index matching and may preserve state on the wrong row — e.g. a typed value "jumps" to a different item after a delete.

**Note:** `key` is a special React prop — it is not passed to the component as a prop.
