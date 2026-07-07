# 11. What are Route Handlers (API routes)? (Junior)

**Route Handlers** let you build **API endpoints** inside the App Router using a `route.ts` file that exports functions named after HTTP methods.

```ts
// app/api/users/route.ts  →  /api/users
import { NextRequest, NextResponse } from "next/server";

export async function GET(request: NextRequest) {
  const users = await db.users.findMany();
  return NextResponse.json(users);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await db.users.create(body);
  return NextResponse.json(user, { status: 201 });
}
```

**Dynamic API routes:**

```ts
// app/api/users/[id]/route.ts
export async function GET(req: NextRequest, { params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  return NextResponse.json(await db.users.findById(id));
}
```

**Notes:**

- Export `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, etc.
- Use `NextResponse` for JSON/redirects/headers; read input via `request.json()` / `request.nextUrl.searchParams`.
- The Pages Router equivalent lives in `pages/api/`.

**Key point:** Route Handlers (`app/api/.../route.ts`) build backend endpoints by exporting HTTP-method functions using `NextRequest`/`NextResponse` — the App Router's way to add an API layer alongside your pages.
