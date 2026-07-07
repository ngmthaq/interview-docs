# 14. Structural typing (duck typing)? (Mid)

TypeScript is **structurally typed**: compatibility is decided by an object's **shape**, not by its declared name. "If it has the right members, it fits."

```ts
interface Point {
  x: number;
  y: number;
}
function log(p: Point) {}

const pt = { x: 1, y: 2, z: 3 };
log(pt); // ✅ has x & y — extra z is fine
```

This contrasts with **nominal** typing (Java, C#), where types must share a declared name/inheritance.

**Excess property check** — the leniency has one exception: **object literals** passed directly are checked strictly:

```ts
log({ x: 1, y: 2, z: 3 }); // ❌ 'z' not in Point (literal only)
```

**Simulating nominal typing** with a _brand_ when you need distinct types with the same shape:

```ts
type UserId = string & { readonly __brand: "UserId" };
type PostId = string & { readonly __brand: "PostId" };

function getUser(id: UserId) {}
const uid = "u1" as UserId;
getUser(uid); // ✅
getUser("p1" as PostId); // ❌ different brand
```

**Why it matters:** you can satisfy an interface without explicitly implementing it — flexible, but watch object-literal strictness.
