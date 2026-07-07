# 11. What is a Buffer? (Junior)

A **`Buffer`** is a fixed-length chunk of **raw binary data** outside V8's heap — Node's way of handling bytes (files, network packets, images) before they're strings.

```js
// From a string (default UTF-8)
const buf = Buffer.from("Hi ✓");
console.log(buf); // <Buffer 48 69 20 e2 9c 93>
console.log(buf.length); // 6 bytes (✓ takes 3 bytes, not 1)

// Allocate zero-filled 4 bytes
const empty = Buffer.alloc(4);

// Convert back
console.log(buf.toString("utf8")); // "Hi ✓"
console.log(buf.toString("hex")); // "486920e29c93"
```

**Key points about Buffers:**

- Length is in **bytes**, not characters — multibyte chars (emoji, accents) take several bytes.
- Use **`Buffer.alloc(n)`** (safe, zero-filled), not `allocUnsafe` unless you immediately overwrite it.
- Streams emit Buffers by default; call `.toString(encoding)` to decode.

**Key point:** Buffers represent raw bytes for binary I/O; remember `.length` counts bytes and encodings (utf8/hex/base64) govern conversion to/from strings.
