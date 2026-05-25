# Next.js Interview Questions and Answers

This README contains the top 50 Next.js interview questions and answers, arranged from beginner level to senior and advanced system design level.

## Beginner Level

### 1. What is Next.js?
Next.js is a React framework used to build production-ready web applications. It provides routing, rendering strategies, API routes, server components, image optimization, metadata handling, and deployment-friendly features out of the box.

Key features:
- File-based routing
- Server-side rendering
- Static site generation
- API routes
- React Server Components
- Image optimization
- Built-in performance optimizations
- Full-stack application support

---

### 2. How is Next.js different from React?
React is a UI library. Next.js is a framework built on top of React.

React provides:
- Components
- Hooks
- State management patterns
- UI rendering

Next.js adds:
- Routing
- Server-side rendering
- Static generation
- API endpoints
- Server Components
- Build optimization
- Deployment structure

In simple terms, React builds UI, while Next.js provides the application architecture around React.

---

### 3. What are the main benefits of using Next.js?
Main benefits:
- Better SEO through server rendering
- Faster initial page load
- File-based routing
- Built-in image optimization
- API routes for backend logic
- Static generation for fast pages
- Server Components for reduced client JavaScript
- Good developer experience
- Easy deployment on platforms like Vercel, Azure, AWS, or Docker

---

### 4. What is file-based routing in Next.js?
File-based routing means routes are created based on the folder and file structure.

In the App Router:

```txt
app/
  page.tsx              -> /
  about/page.tsx        -> /about
  products/page.tsx     -> /products
  products/[id]/page.tsx -> /products/:id
```

You do not need to manually configure routes like in traditional React Router applications.

---

### 5. What is the difference between App Router and Pages Router?
Pages Router is the older routing system using the `pages/` directory.

App Router is the newer routing system using the `app/` directory.

Pages Router features:
- `pages/index.tsx`
- `getServerSideProps`
- `getStaticProps`
- API routes under `pages/api`

App Router features:
- `app/page.tsx`
- Layouts
- Server Components
- Loading UI
- Error boundaries
- Route handlers
- Server Actions
- Streaming support

For new projects, App Router is generally recommended.

---

### 6. What is a page in Next.js?
A page is a React component that maps to a route.

Example:

```tsx
export default function HomePage() {
  return <h1>Home Page</h1>;
}
```

In App Router, a page file must be named `page.tsx`.

---

### 7. What is a layout in Next.js?
A layout is shared UI that wraps pages and child routes.

Example:

```tsx
export default function DashboardLayout({ children }) {
  return (
    <div>
      <Sidebar />
      <main>{children}</main>
    </div>
  );
}
```

Layouts preserve state across navigation and are useful for dashboards, navigation shells, and common page structure.

---

### 8. What is the purpose of `next/link`?
`next/link` enables client-side navigation between routes.

Example:

```tsx
import Link from "next/link";

<Link href="/dashboard">Dashboard</Link>
```

It improves performance by avoiding full page reloads and can prefetch routes automatically.

---

### 9. What is the purpose of `next/image`?
`next/image` optimizes images automatically.

Benefits:
- Lazy loading
- Responsive sizes
- Modern formats
- Prevents layout shift
- Optimized delivery

Example:

```tsx
import Image from "next/image";

<Image src="/profile.png" alt="Profile" width={200} height={200} />
```

---

### 10. What is the difference between static and dynamic routes?
Static routes have fixed paths.

Example:

```txt
app/about/page.tsx -> /about
```

Dynamic routes use parameters.

Example:

```txt
app/products/[id]/page.tsx -> /products/123
```

Dynamic routes are useful for product pages, user profiles, blog posts, and detail pages.

---

## Intermediate Level

### 11. What is Server-Side Rendering in Next.js?
Server-Side Rendering means HTML is generated on the server for each request.

Benefits:
- Better SEO
- Fresh data on every request
- Faster first meaningful paint for dynamic pages

Use SSR for:
- Personalized dashboards
- Frequently changing data
- Authenticated pages
- Request-specific content

Trade-off:
- More server work compared to static generation

---

### 12. What is Static Site Generation in Next.js?
Static Site Generation means HTML is generated at build time.

Benefits:
- Very fast page load
- CDN-friendly
- Lower server cost
- Good for SEO

Use SSG for:
- Blog posts
- Marketing pages
- Documentation
- Product landing pages
- Mostly unchanged content

---

### 13. What is Incremental Static Regeneration?
Incremental Static Regeneration allows static pages to be regenerated after deployment.

It gives the performance of static pages while allowing content updates.

Example:

```tsx
await fetch("https://api.example.com/products", {
  next: { revalidate: 60 }
});
```

This means the cached data can be refreshed every 60 seconds.

---

### 14. What are React Server Components in Next.js?
React Server Components render on the server and do not send their JavaScript to the browser.

Benefits:
- Smaller client bundle
- Direct server-side data access
- Better performance
- Improved security for server-only logic

By default, components in the App Router are Server Components unless marked with `"use client"`.

---

### 15. What is a Client Component in Next.js?
A Client Component runs in the browser and can use browser-only features.

Use Client Components for:
- `useState`
- `useEffect`
- Event handlers
- Browser APIs
- Interactive UI

Example:

```tsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

---

### 16. When should you use `"use client"`?
Use `"use client"` only when a component needs client-side interactivity.

Use it for:
- State
- Effects
- Event handlers
- Browser APIs
- Client-only libraries

Avoid marking large page components as client components unnecessarily. Doing so increases JavaScript sent to the browser.

---

### 17. Can Server Components import Client Components?
Yes. Server Components can import and render Client Components.

This is common when a mostly server-rendered page needs a small interactive section.

Example:

```tsx
export default async function ProductPage() {
  const product = await getProduct();

  return (
    <div>
      <ProductDetails product={product} />
      <AddToCartButton productId={product.id} />
    </div>
  );
}
```

`AddToCartButton` can be a Client Component.

---

### 18. Can Client Components import Server Components?
No. Client Components cannot directly import Server Components.

Reason:
- Client Components run in the browser
- Server Components may use server-only code, databases, secrets, or file system APIs

Instead, pass Server Components as children or fetch data through an API or server action.

---

### 19. What are route handlers in Next.js?
Route handlers define backend endpoints inside the App Router.

Example:

```txt
app/api/users/route.ts
```

```tsx
export async function GET() {
  return Response.json({ users: [] });
}
```

Route handlers can handle `GET`, `POST`, `PUT`, `PATCH`, and `DELETE` requests.

---

### 20. What are API routes in Next.js?
API routes are backend endpoints inside a Next.js application.

In Pages Router:

```txt
pages/api/users.ts
```

In App Router, route handlers are preferred:

```txt
app/api/users/route.ts
```

They are useful for:
- Form submissions
- Authentication callbacks
- Webhooks
- Proxying backend services
- Lightweight backend logic

---

### 21. What is middleware in Next.js?
Middleware runs before a request is completed.

Use cases:
- Authentication checks
- Redirects
- Rewrites
- Locale detection
- A/B testing
- Request filtering

Example:

```tsx
import { NextResponse } from "next/server";

export function middleware(request) {
  const token = request.cookies.get("token");

  if (!token) {
    return NextResponse.redirect(new URL("/login", request.url));
  }

  return NextResponse.next();
}
```

Middleware should be lightweight because it can run frequently.

---

### 22. What is dynamic rendering in Next.js?
Dynamic rendering means a route is rendered at request time instead of build time.

A route becomes dynamic when it uses:
- Cookies
- Headers
- Search params
- No-store fetch
- Request-specific data

Dynamic rendering is useful when content depends on the current user or request.

---

### 23. What is caching in Next.js?
Next.js has multiple caching layers.

Common caches:
- Request memoization
- Data cache
- Full route cache
- Router cache

Caching improves performance but requires careful invalidation when data changes.

---

### 24. How does `fetch` caching work in Next.js?
Next.js extends the native `fetch` API with caching behavior.

Static cached fetch:

```tsx
await fetch("https://api.example.com/products");
```

No cache:

```tsx
await fetch("https://api.example.com/products", {
  cache: "no-store"
});
```

Revalidation:

```tsx
await fetch("https://api.example.com/products", {
  next: { revalidate: 60 }
});
```

---

### 25. What is `generateStaticParams`?
`generateStaticParams` tells Next.js which dynamic routes should be statically generated at build time.

Example:

```tsx
export async function generateStaticParams() {
  const posts = await getPosts();

  return posts.map((post) => ({
    slug: post.slug
  }));
}
```

Useful for blogs, product pages, and documentation pages.

---

## Advanced Level

### 26. What is metadata handling in Next.js?
Next.js provides a Metadata API for managing SEO metadata.

Static metadata:

```tsx
export const metadata = {
  title: "Products",
  description: "Browse products"
};
```

Dynamic metadata:

```tsx
export async function generateMetadata({ params }) {
  const product = await getProduct(params.id);

  return {
    title: product.name,
    description: product.summary
  };
}
```

---

### 27. What is streaming in Next.js?
Streaming allows the server to send parts of the UI as they become ready.

Benefits:
- Faster perceived loading
- Better user experience
- Independent loading sections
- Works well with Suspense

Use `loading.tsx` for route-level loading UI.

---

### 28. What is `loading.tsx`?
`loading.tsx` defines loading UI for a route segment.

Example:

```txt
app/dashboard/loading.tsx
```

```tsx
export default function Loading() {
  return <DashboardSkeleton />;
}
```

It works with React Suspense and streaming.

---

### 29. What is `error.tsx`?
`error.tsx` defines an error boundary for a route segment.

Example:

```tsx
"use client";

export default function Error({ error, reset }) {
  return (
    <div>
      <p>Something went wrong</p>
      <button onClick={reset}>Try again</button>
    </div>
  );
}
```

It must be a Client Component.

---

### 30. What is `not-found.tsx`?
`not-found.tsx` defines UI for a 404 state.

Example:

```tsx
export default function NotFound() {
  return <h1>Page not found</h1>;
}
```

You can trigger it using:

```tsx
import { notFound } from "next/navigation";

if (!product) {
  notFound();
}
```

---

### 31. What are Server Actions in Next.js?
Server Actions allow running server-side logic directly from components, usually for mutations.

Example:

```tsx
"use server";

export async function createPost(formData: FormData) {
  await db.post.create({
    data: {
      title: formData.get("title") as string
    }
  });
}
```

They are useful for forms, mutations, and reducing separate API route boilerplate.

---

### 32. How would you handle forms in Next.js?
Options:
- Client-side form with API route
- Server Action form
- React Hook Form with validation
- Zod schema validation

For simple server mutations, Server Actions are clean. For complex interactive forms, React Hook Form is often better.

Important form concerns:
- Client validation
- Server validation
- Error states
- Pending state
- Revalidation after submit
- Security checks

---

### 33. How do you revalidate data after a mutation?
Use `revalidatePath` or `revalidateTag`.

Example:

```tsx
import { revalidatePath } from "next/cache";

export async function createProduct() {
  await saveProduct();
  revalidatePath("/products");
}
```

Use tags when multiple pages depend on the same data.

---

### 34. What is the difference between `revalidatePath` and `revalidateTag`?
`revalidatePath` invalidates cache for a specific route path.

`revalidateTag` invalidates cached data associated with a tag.

Example:

```tsx
await fetch("https://api.example.com/products", {
  next: { tags: ["products"] }
});
```

Then:

```tsx
revalidateTag("products");
```

Use tags for shared data used by multiple routes.

---

### 35. How do you handle authentication in Next.js?
Authentication can be handled using:
- NextAuth/Auth.js
- Custom cookie-based sessions
- JWT tokens
- External identity providers
- Middleware route protection

Senior-level recommendation:
- Prefer secure HttpOnly cookies
- Validate sessions on the server
- Avoid trusting only client-side auth state
- Protect backend routes as well as pages
- Keep authorization checks close to sensitive data access

---

### 36. Where should authentication checks happen in Next.js?
Authentication checks can happen in multiple places:
- Middleware for broad route protection
- Server Components for page-level user loading
- Route handlers for API protection
- Server Actions for mutation protection
- Backend services for final enforcement

Middleware is useful for redirects, but sensitive authorization should still be checked on the server where data is accessed.

---

### 37. How do you protect routes in Next.js?
Common approach:
- Use middleware for protected route groups
- Check session cookie
- Redirect unauthenticated users to login
- Use role checks for protected pages

Example protected paths:

```tsx
export const config = {
  matcher: ["/dashboard/:path*", "/settings/:path*"]
};
```

Do not rely only on hiding links in the UI.

---

### 38. How do you handle role-based access in Next.js?
Role-based access should be checked on the server.

Example:

```tsx
const user = await getCurrentUser();

if (user.role !== "admin") {
  redirect("/unauthorized");
}
```

Use frontend checks only to improve UX. Backend and server-side checks are mandatory for security.

---

### 39. How do you handle environment variables in Next.js?
Next.js supports environment variables through `.env` files.

Server-only variable:

```txt
DATABASE_URL=postgres://...
```

Client-exposed variable:

```txt
NEXT_PUBLIC_API_URL=https://api.example.com
```

Only variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.

Never expose secrets using `NEXT_PUBLIC_`.

---

### 40. How do you optimize images in Next.js?
Use `next/image`.

Optimization techniques:
- Set width and height
- Use responsive sizes
- Use priority for above-the-fold images
- Use CDN/image loader if needed
- Avoid layout shift
- Use meaningful alt text

Example:

```tsx
<Image
  src="/hero.jpg"
  alt="Product dashboard"
  width={1200}
  height={600}
  priority
/>
```

---

## Senior and System Design Level

### 41. How would you design a large enterprise dashboard in Next.js?
Recommended design:
- App Router with nested layouts
- Server Components for initial data loading
- Client Components for interactive widgets
- React Query for client-side server state where needed
- Route-level loading and error boundaries
- Role-based navigation
- Widget-level authorization
- Cached APIs with revalidation
- Observability and analytics

Architecture example:

```txt
app/
  (dashboard)/
    layout.tsx
    dashboard/page.tsx
    reports/page.tsx
    settings/page.tsx
features/
  reports/
  users/
  billing/
components/
  ui/
services/
  api/
```

---

### 42. How would you decide between SSR, SSG, ISR, and CSR?
Choose based on data freshness, SEO, personalization, and performance.

Use SSR when:
- Data changes per request
- Page is personalized
- SEO matters

Use SSG when:
- Content is mostly static
- Maximum performance is needed

Use ISR when:
- Static performance is desired
- Content updates periodically

Use CSR when:
- SEO is not important
- UI is highly interactive
- Data depends heavily on browser state

---

### 43. How would you reduce JavaScript bundle size in Next.js?
Strategies:
- Prefer Server Components
- Use route-level code splitting
- Dynamically import heavy Client Components
- Avoid unnecessary `"use client"`
- Analyze bundle with bundle analyzer
- Remove unused dependencies
- Import only needed functions
- Replace heavy libraries with lighter alternatives

Server Components are one of the strongest tools for reducing client JavaScript.

---

### 44. How would you debug hydration errors?
Hydration errors happen when server-rendered HTML differs from client-rendered HTML.

Common causes:
- `Date.now()` during render
- `Math.random()` during render
- Browser-only APIs like `window`
- Different server/client locale output
- Conditional UI based on client-only data
- Invalid HTML nesting

Fixes:
- Move client-only logic into `useEffect`
- Use stable values for initial render
- Use dynamic imports with SSR disabled when necessary
- Validate HTML structure
- Keep server and client output consistent

---

### 45. How would you design data fetching in a Next.js App Router project?
Recommended approach:
- Fetch initial page data in Server Components
- Use cached fetch for stable data
- Use `cache: "no-store"` for request-specific data
- Use React Query/SWR for client-side interactions
- Use Server Actions or route handlers for mutations
- Use revalidation after mutations

Avoid duplicating the same data-fetching logic across many components.

---

### 46. How would you handle real-time data in Next.js?
Options:
- WebSockets
- Server-Sent Events
- Polling
- Third-party real-time services

Recommended design:
- Use Server Components for initial load
- Use Client Components for live updates
- Keep WebSocket logic isolated in hooks/services
- Handle reconnects and backoff
- Prevent duplicate events
- Sync real-time updates with query cache

---

### 47. How would you design multi-tenant Next.js applications?
A multi-tenant app should load tenant configuration early.

Tenant-specific data:
- Theme
- Logo
- Domain
- Permissions
- Feature flags
- Navigation
- Localization
- API routing rules

Implementation options:
- Middleware detects tenant from hostname
- Server Component loads tenant config
- Layout applies branding
- Authorization checks include tenant context
- Cache keys include tenant ID

Be careful not to leak data across tenants.

---

### 48. How would you design observability for a Next.js app?
Observability should cover frontend and backend behavior.

Track:
- Client-side errors
- Server-side errors
- Route handler failures
- Server Action failures
- Web vitals
- API latency
- Cache hit/miss behavior
- User flows
- Correlation IDs

Tools:
- Sentry
- Datadog
- Azure Application Insights
- OpenTelemetry
- Vercel Analytics

Avoid logging secrets or personal data unnecessarily.

---

### 49. How would you deploy a Next.js application in production?
Deployment options:
- Vercel
- Azure App Service
- Azure Static Web Apps for static output
- Docker container
- Kubernetes
- AWS Amplify
- Netlify

Production checklist:
- Environment variables configured
- Build succeeds
- Image optimization supported
- Logging configured
- Error monitoring enabled
- Security headers configured
- CDN/cache strategy defined
- Health checks configured if using containers

---

### 50. What are common mistakes in large Next.js applications?
Common mistakes:
- Adding `"use client"` too high in the tree
- Fetching all data on the client unnecessarily
- Ignoring caching behavior
- Not handling loading and error states
- Exposing secrets with `NEXT_PUBLIC_`
- Relying only on frontend authorization
- Creating hydration mismatches
- Overusing middleware for heavy logic
- Not revalidating cache after mutations
- Shipping large client bundles
- Not monitoring production errors

A senior developer should understand not only how to build features, but also how rendering, caching, security, and deployment choices affect the whole system.
