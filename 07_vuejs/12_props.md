# 12. Props? (Fresher)

Props pass data **from parent to child** — one-way, top-down flow.

**Declaring props** with `<script setup>` and TypeScript:

```vue
<script setup lang="ts">
interface Props {
  title: string;
  count?: number; // optional
  tags?: string[];
}
const props = withDefaults(defineProps<Props>(), {
  count: 0,
  tags: () => [], // objects/arrays need a factory
});
</script>
```

**Passing props from the parent:**

```vue
<UserCard :title="user.name" :count="5" />
```

**Runtime declaration** (JS-style, with validation):

```ts
const props = defineProps({
  title: { type: String, required: true },
  count: { type: Number, default: 0 },
});
```

**One-way data flow:** props are **read-only** in the child. Mutating a prop is an anti-pattern and warns:

```ts
props.count++; // ❌ don't mutate props
```

To "change" a prop, either:

- **Emit an event** so the parent updates it, or
- Copy it into local state: `const local = ref(props.count)`.

**Naming:** declare in `camelCase`, pass in `kebab-case` in templates (`:user-name`).

**Boolean shorthand:** `<Modal open />` means `open = true`.
