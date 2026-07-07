# 22. How do you implement authentication in Next.js? (Senior)

A typical stack uses a library (**NextAuth/Auth.js**, Clerk, Lucia) plus **middleware** for route protection and **cookies** for sessions.

```ts
// middleware.ts — gate protected routes at the edge
export function middleware(req: NextRequest) {
  const session = req.cookies.get("session");
  if (req.nextUrl.pathname.startsWith("/dashboard") && !session) {
    return NextResponse.redirect(new URL("/login", req.url));
  }
}
export const config = { matcher: ["/dashboard/:path*"] };
```

**Reading the user server-side:**

```tsx
// Server Component — read session directly, no client fetch
import { auth } from "@/auth";

export default async function Dashboard() {
  const session = await auth();
  if (!session) redirect("/login");
  return <p>Hello {session.user.name}</p>;
}
```

**Key considerations:**

- Store sessions in **httpOnly cookies** (not `localStorage`) to resist XSS.
- Use **middleware** for coarse gating and **per-page/Server Action checks** for real authorization (middleware alone isn't a security boundary).
- Validate/authorize inside **Server Actions and Route Handlers** — they're public entry points.

**Key point:** combine an auth library (Auth.js/Clerk) with middleware for route gating and httpOnly-cookie sessions; read the session directly in Server Components, but enforce real authorization in each Server Action/Route Handler, not middleware alone.
