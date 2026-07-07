# 3. Arrays vs linked lists. (Fresher)

Both store sequences, but with different memory layouts and performance.

**Array** — contiguous memory, indexed:

- **Access by index: O(1)** — direct address calculation.
- **Insert/delete in the middle: O(n)** — must shift elements.
- Cache-friendly (elements adjacent in memory).

**Linked list** — nodes each pointing to the next:

- **Access by index: O(n)** — must traverse from the head.
- **Insert/delete at a known node: O(1)** — just repoint pointers.
- Extra memory per node (the pointer); not cache-friendly.

```ts
// Singly linked list node
class ListNode {
  value: number;
  next: ListNode | null = null;
  constructor(value: number) {
    this.value = value;
  }
}
```

| Operation              | Array | Linked list    |
| ---------------------- | ----- | -------------- |
| Access by index        | O(1)  | O(n)           |
| Insert/delete at front | O(n)  | O(1)           |
| Insert/delete at end   | O(1)* | O(1) with tail |
| Search                 | O(n)  | O(n)           |

*Amortized for dynamic arrays.

**Key point:** arrays give O(1) indexed access but O(n) middle insertions; linked lists give O(1) insert/delete at a known node but O(n) access — choose arrays for random access and iteration, linked lists for frequent front/middle insertions.
