# 10. What are Streams in Node.js? (Junior)

**Streams** process data **in chunks** instead of loading it all into memory — essential for large files and network data.

**Four types:**

- **Readable** — source you read from (`fs.createReadStream`, HTTP request).
- **Writable** — destination you write to (`fs.createWriteStream`, HTTP response).
- **Duplex** — both (TCP socket).
- **Transform** — duplex that modifies data (gzip, encryption).

```js
const fs = require("fs");
const { pipeline } = require("stream/promises");
const zlib = require("zlib");

// Stream + compress a large file without loading it fully into memory
await pipeline(
  fs.createReadStream("big.log"),
  zlib.createGzip(),
  fs.createWriteStream("big.log.gz")
);
```

**Why streams matter:** reading a 2 GB file with `fs.readFile` buffers all 2 GB in RAM; a stream handles it a chunk at a time with backpressure (auto-pausing when the consumer is slow).

**Key point:** streams handle data incrementally with built-in backpressure — use `pipeline`/`pipe` for memory-efficient file, compression, and network processing.
