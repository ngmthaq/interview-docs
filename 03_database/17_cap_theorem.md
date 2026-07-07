# 17. Explain the CAP theorem. (Senior)

In a **distributed** system you can guarantee only **two of three** properties during a network partition:

- **C**onsistency — every read sees the latest write.
- **A**vailability — every request gets a (non-error) response.
- **P**artition tolerance — the system keeps working despite dropped network messages between nodes.

```
Since network partitions WILL happen, P is mandatory.
So the real choice under a partition is: C or A.
```

| Choice | Behavior during a partition        | Examples                       |
| ------ | ---------------------------------- | ------------------------------ |
| **CP** | Reject requests to stay consistent | HBase, MongoDB (default), etcd |
| **AP** | Stay available, allow stale reads  | Cassandra, DynamoDB, Couchbase |

**Key point:** CAP is about the **partition scenario**. When the network is healthy you can have both C and A. The design question is: _when nodes can't talk, do you prefer to reject requests (CP) or serve possibly-stale data (AP)?_

**Related:** BASE (Basically Available, Soft state, Eventual consistency) is the AP-leaning philosophy behind many NoSQL stores.
