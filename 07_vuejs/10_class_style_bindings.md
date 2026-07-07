# 10. Class and style bindings? (Fresher)

`v-bind` on `class` and `style` has special enhancements — you can pass objects and arrays, not just strings.

**Class — object syntax** (toggle classes by boolean):

```vue
<div :class="{ active: isActive, 'text-danger': hasError }"></div>
```

**Class — array syntax:**

```vue
<div :class="[baseClass, isActive ? 'active' : '']"></div>
<div :class="[{ active: isActive }, extraClass]"></div>
```

You can combine with a static `class` — they merge:

```vue
<div class="card" :class="{ selected }"></div>
```

**Style — object syntax** (camelCase or kebab-case keys):

```vue
<div :style="{ color: activeColor, fontSize: size + 'px' }"></div>
```

**Style — array of objects** (merged):

```vue
<div :style="[baseStyles, overrideStyles]"></div>
```

**Binding a computed** keeps templates clean:

```ts
const classes = computed(() => ({
  active: isActive.value,
  disabled: !isEnabled.value,
}));
```

```vue
<div :class="classes"></div>
```

**On components:** class/style bound on a component are automatically applied to its **root element** (attribute fallthrough).

**Vue-specific niceties:** auto-prefixing for vendor styles, and array values for a property with fallbacks (`:style="{ display: ['flex', '-webkit-box'] }"`).
