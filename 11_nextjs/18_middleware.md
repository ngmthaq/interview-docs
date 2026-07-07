# 18. What is Next.js Middleware? (Mid)

**Middleware** runs **before a request is completed**, at the **edge** — letting you rewrite, redirect, or modify requests/responses globally (auth checks, geolocation, A/B testing, i18n).

```ts
// middleware.ts (project root)
import { NextRequest, NextResponse } from "next/server";

export function middleware(request: NextRequest) {
  const token = request.cookies.get("token");

  // Protect /dashboard routes
  if (request.nextUrl.pathname.startsWith("/dashboard") && !token) {
    return NextResponse.redirect(new URL("/login", request.url));
  }

  return NextResponse.next(); // continue
}

// Limit which paths it runs on
export const config = {
  matcher: ["/dashboard/:path*", "/profile/:path*"],
};
```

**Key facts:**

- Runs on the **Edge Runtime** — fast, but a limited API (no Node.js-specific modules by default).
- Common uses: **auth gating**, redirects/rewrites, setting headers/cookies, localization, bot protection.
- Use the **`matcher`** config to scope it and avoid running on every request (including static assets).

**Key point:** Middleware (`middleware.ts`) runs at the edge before requests resolve, enabling global redirects, rewrites, auth gating, and header/cookie manipulation — scope it with `matcher` and remember it uses the limited Edge Runtime.
