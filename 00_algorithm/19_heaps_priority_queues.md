# 19. What are heaps and priority queues? (Senior)

A **heap** is a complete binary tree satisfying the **heap property**: in a **min-heap**, every parent ≤ its children (the min is at the root); in a **max-heap**, every parent ≥ its children. It's the standard implementation of a **priority queue**.

**Operations** (heap stored in an array):

- **Peek** (min/max) — **O(1)** (the root).
- **Insert** — **O(log n)** (add at end, "bubble up").
- **Extract** min/max — **O(log n)** (swap root with last, "sift down").
- **Build heap** from n items — **O(n)**.

```ts
// Min-heap sketch — array where children of i are 2i+1, 2i+2
class MinHeap {
  private h: number[] = [];
  peek() {
    return this.h[0];
  }
  push(v: number) {
    this.h.push(v);
    let i = this.h.length - 1;
    while (i > 0) {
      const p = (i - 1) >> 1;
      if (this.h[p] <= this.h[i]) break;
      [this.h[p], this.h[i]] = [this.h[i], this.h[p]]; // bubble up
      i = p;
    }
  }
  // pop(): swap root with last, sift down — O(log n)
}
```

**Use cases:** priority queues, **Dijkstra's / Prim's** algorithms, **top-K** elements, merging k sorted lists, median of a stream (two heaps), heap sort, task scheduling.

**Key point:** a heap keeps the min/max at the root via the heap property, giving O(1) peek and O(log n) insert/extract in an array — it's how priority queues are built, powering Dijkstra, top-K, k-way merge, and streaming-median problems.
