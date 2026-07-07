# 27. `nextTick` and async DOM updates? (Mid)

Vue updates the DOM **asynchronously**. When you change reactive state, the DOM is **not** updated immediately — Vue **batches** all changes in the same tick and flushes them together for efficiency.

```ts
count.value = 1;
// DOM still shows the old value here
console.log(el.textContent); // old
```

**`nextTick`** waits for the DOM to finish updating:

```ts
import { nextTick } from "vue";

count.value = 1;
await nextTick();
// now the DOM reflects the change
console.log(el.textContent); // new
```

**Why batching?** If you change state 100 times synchronously, Vue re-renders **once**, not 100 times — a major performance win. The trade-off is that DOM reads right after a state change see stale content.

**Common use cases:**

```ts
// 1. Access updated DOM after adding an item
messages.value.push(newMsg);
await nextTick();
scrollToBottom(); // list is now rendered

// 2. Focus an element that just became visible
showInput.value = true;
await nextTick();
inputRef.value?.focus();
```

**Two forms:**

```ts
await nextTick(); // promise
nextTick(() => {}); // callback
```

**Key insight:** the async update queue is what makes Vue efficient. Reach for `nextTick` whenever you must read or act on the DOM **immediately after** a reactive change.
