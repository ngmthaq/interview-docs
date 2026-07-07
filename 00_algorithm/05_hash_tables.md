# 5. How do hash tables work? (Junior)

A **hash table** (hash map) stores key/value pairs, using a **hash function** to map a key to a bucket index — giving **average O(1)** insert, lookup, and delete.

```ts
// JS Map / object are hash tables
const map = new Map<string, number>();
map.set("apple", 3); // hash("apple") → bucket
map.get("apple"); // O(1) average
map.has("apple"); // O(1) average
```

**How it works:**

1. **Hash** the key to a number.
2. **Modulo** by the array size to get a bucket index.
3. Store the entry there.

**Collisions** (two keys → same bucket) are resolved by:

- **Chaining** — each bucket holds a linked list/array of entries.
- **Open addressing** — probe for the next empty slot.

**Complexity:**

- **Average: O(1)** for get/set/delete.
- **Worst: O(n)** — many collisions degrade to a linear scan (mitigated by a good hash + **resizing** when the load factor gets high).

**Common uses:** deduplication, frequency counting, caching/memoization, fast lookups (turning O(n²) into O(n)).

**Key point:** hash tables map keys to buckets via a hash function for average O(1) operations; collisions are handled by chaining or open addressing, and worst case is O(n) — they're the go-to structure for fast lookups, counting, and deduplication.
