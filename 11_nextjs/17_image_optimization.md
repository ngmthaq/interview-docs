# 17. How does next/image optimize images? (Mid)

The **`next/image`** component automatically optimizes images — a major performance and Core Web Vitals win over a raw `<img>`.

```tsx
import Image from "next/image";

export default function Hero() {
  return (
    <Image
      src="/hero.jpg"
      alt="Hero"
      width={1200}
      height={600}
      priority // preload above-the-fold images
      placeholder="blur"
    />
  );
}
```

**What it does automatically:**

- **Resizing & responsive** `srcset` — serves the right size per device.
- **Modern formats** — converts to WebP/AVIF when supported.
- **Lazy loading** by default (except `priority` images).
- **Prevents layout shift (CLS)** — reserves space via `width`/`height` (or `fill`).
- **On-demand optimization** — images processed and cached at request time.

**Notes:**

- Remote images need their domain allow-listed in `next.config.js` (`images.remotePatterns`).
- Use `fill` + a sized parent for unknown dimensions; always provide `alt`.

**Key point:** `next/image` auto-resizes, converts to modern formats (WebP/AVIF), lazy-loads, and reserves layout space to prevent CLS — set `width`/`height` (or `fill`), mark above-the-fold images `priority`, and allow-list remote domains.
