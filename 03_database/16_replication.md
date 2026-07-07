# 16. What is database replication? (Senior)

**Replication** keeps copies of the database on multiple servers. The common setup is **primary-replica** (master-slave).

```
        writes          reads
Client ───────▶ Primary ─────────▶ Replica 1
                   │  \            └▶ Replica 2
                   │   └─ replicates changes ─┘
```

- **Primary** handles writes.
- **Replicas** receive a stream of changes and serve **read** queries.

**Benefits:**

- **Read scaling** — spread read load across replicas.
- **High availability** — promote a replica if the primary fails (failover).
- **Geo-locality** — replicas close to users.

**Trade-off — replication lag:**

- Replicas may be **slightly behind** the primary → a read right after a write might return stale data (eventual consistency).
- Fix: read critical-after-write data from the primary, or use synchronous replication (slower writes).

**Sync vs async:** synchronous = no data loss but slower; asynchronous = fast but possible loss on failover.
