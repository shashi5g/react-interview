# React Interview Questions and Answers

## Beginner Level

### 1. What is React?
React is a JavaScript library used to build user interfaces. It helps developers create reusable UI components and efficiently update the UI when data changes.

### 2. What are React components?
Components are reusable building blocks of a React application. A component can represent a button, form, page, card, modal, or any UI section.

### 3. What is JSX?
JSX is a syntax extension for JavaScript that allows writing HTML-like code inside JavaScript. React converts JSX into regular JavaScript function calls.

### 4. What is the difference between props and state?
Props are read-only data passed from a parent component to a child component. State is data managed inside a component and can change over time.

### 5. What is a functional component?
A functional component is a JavaScript function that returns JSX. Modern React mainly uses functional components with hooks.

### 6. What is state in React?
State is component data that changes over time. When state changes, React re-renders the component.

### 7. What is useState?
useState is a React hook used to add state to functional components.

Example:
`const [count, setCount] = useState(0);`

### 8. Why should state not be mutated directly?
React relies on state references to detect changes. Direct mutation may not trigger re-rendering and can cause UI bugs.

### 9. What are props?
Props are inputs passed to a component. They allow components to be reusable and configurable.

### 10. What is conditional rendering?
Conditional rendering means showing different UI based on a condition, such as showing a dashboard when logged in and a login page when logged out.

### 11. How do you render a list in React?
Lists are rendered using the `map()` method. Each item should have a unique `key`.

### 12. Why are keys important in React?
Keys help React identify which list items changed, were added, or removed. They improve rendering performance and prevent incorrect UI updates.

### 13. What is an event handler in React?
An event handler is a function that runs when a user interacts with the UI, such as clicking a button or typing in an input.

### 14. What is a controlled component?
A controlled component is a form element whose value is controlled by React state.

### 15. What is an uncontrolled component?
An uncontrolled component manages its own value in the DOM. React can access the value using refs.

## Intermediate Level

### 16. What is useEffect?
useEffect is a hook used to run side effects in React components, such as API calls, subscriptions, timers, or DOM updates.

### 17. What is the dependency array in useEffect?
The dependency array controls when useEffect runs. An empty array runs once, dependencies run when values change, and no array runs after every render.

### 18. How do you clean up useEffect?
Return a cleanup function from useEffect. It is used to remove event listeners, clear timers, cancel subscriptions, or abort API requests.

### 19. What is prop drilling?
Prop drilling happens when data is passed through many components just to reach a deeply nested child component.

### 20. How can prop drilling be avoided?
Prop drilling can be avoided using Context API, component composition, custom hooks, or state management libraries.

### 21. What is Context API?
Context API allows sharing data across multiple components without manually passing props through every level.

### 22. What is useContext?
useContext is a hook used to read values from React context.

### 23. What is useRef?
useRef stores a mutable value that persists across renders without causing re-renders.

### 24. Difference between useRef and useState?
useState triggers a re-render when updated. useRef does not trigger a re-render when its value changes.

### 25. What is lifting state up?
Lifting state up means moving shared state to the nearest common parent component so multiple child components can use it.

### 26. What is component composition?
Component composition means building complex UI by combining smaller reusable components.

### 27. What are React fragments?
Fragments allow returning multiple elements without adding an extra DOM node.

### 28. What is reconciliation?
Reconciliation is React’s process of comparing the old virtual DOM with the new virtual DOM and updating only the changed parts of the real DOM.

### 29. What is the virtual DOM?
The virtual DOM is an in-memory representation of the UI. React uses it to calculate efficient updates to the real DOM.

### 30. What causes a React component to re-render?
A component re-renders when its state changes, props change, parent re-renders, or consumed context value changes.

## Advanced Level

### 31. What is React.memo?
React.memo is used to memoize a component. It prevents unnecessary re-renders when props have not changed.

### 32. What is useMemo?
useMemo memoizes a calculated value so it is recomputed only when dependencies change.

### 33. What is useCallback?
useCallback memoizes a function reference so the function is recreated only when dependencies change.

### 34. Difference between useMemo and useCallback?
useMemo memoizes a value. useCallback memoizes a function.

### 35. What is a custom hook?
A custom hook is a reusable function that uses React hooks to share stateful logic between components.

### 36. What are the rules of hooks?
Hooks must be called only at the top level of React components or custom hooks. They should not be called inside loops, conditions, or nested functions.

### 37. What is stale closure in React?
A stale closure happens when a function captures an old value from a previous render and continues using that outdated value.

### 38. How do you fix stale closure issues?
Use correct dependency arrays, functional state updates, or refs depending on the situation.

### 39. What is an error boundary?
An error boundary is a React component that catches rendering errors in child components and displays fallback UI.

### 40. What is code splitting?
Code splitting breaks the application bundle into smaller chunks that load only when needed.

### 41. What is React.lazy?
React.lazy allows loading a component dynamically using dynamic import.

### 42. What is Suspense?
Suspense allows showing fallback UI while waiting for lazy-loaded components or supported async operations.

### 43. What is a portal in React?
A portal renders a component outside its normal DOM hierarchy, commonly used for modals, dropdowns, and tooltips.

### 44. What is hydration?
Hydration is the process where React attaches event handlers and client-side behavior to server-rendered HTML.

### 45. Difference between client-side rendering and server-side rendering?
Client-side rendering builds the UI in the browser. Server-side rendering generates HTML on the server and sends it to the browser.

## Technical Specialist Level

### 46. How would you structure a scalable React application?
A scalable React app should be organized by features, use reusable components, shared hooks, typed API services, clear state boundaries, and consistent coding standards.

Example structure:
`components/`, `features/`, `hooks/`, `services/`, `types/`, `utils/`, `app/`.

### 47. How do you optimize performance in a large React application?
Use React.memo carefully, memoize expensive calculations, virtualize large lists, split code, lazy load heavy components, optimize context usage, and keep state close to where it is needed.

### 48. How do you manage forms at scale in React?
Use libraries such as React Hook Form with schema validation using Zod or Yup. Keep form logic reusable, accessible, and easy to validate on both client and server.

### 49. How do you handle authentication in React?
Authentication usually involves login, session/token handling, protected routes, refresh logic, logout, and permission checks. Secure apps often use HttpOnly cookies instead of storing long-lived tokens in localStorage.

### 50. How would you debug a complex React rendering issue?
Use React DevTools, inspect props and state, check dependency arrays, verify list keys, identify unnecessary re-renders, inspect context updates, and use the React Profiler to locate performance problems.

# React.js System Design Interview Questions and Answers

This README contains React.js system design interview questions from advanced frontend architecture to technical specialist level.

## React Frontend System Design Questions

### 1. How would you design a scalable React application architecture?
A scalable React application should be organized around business features rather than only technical file types.

Recommended structure:

```txt
src/
  app/
  features/
  components/
  hooks/
  services/
  stores/
  types/
  utils/
  styles/
```

Key points:
- Keep feature-specific logic inside `features/`
- Keep reusable UI inside `components/`
- Keep API calls inside `services/`
- Keep global state minimal
- Use TypeScript for maintainability
- Use clear boundaries between UI, data, and business logic

---

### 2. How would you design routing for a large React application?
Use route-based architecture with lazy loading.

Example:

```tsx
const Dashboard = lazy(() => import("./features/dashboard/Dashboard"));
const Settings = lazy(() => import("./features/settings/Settings"));
```

Good routing design includes:
- Public routes
- Protected routes
- Role-based routes
- Error routes
- Lazy-loaded route modules
- Layout-based routing

In large applications, routes should map closely to product areas.

---

### 3. How would you design authentication in React?
Authentication design should separate login state, session validation, token refresh, and route protection.

Recommended approach:
- Use HttpOnly secure cookies when possible
- Store user profile in memory or query cache
- Protect routes with an auth guard
- Refresh session automatically
- Handle logout globally
- Redirect unauthorized users safely

Avoid storing long-lived sensitive tokens in `localStorage`.

---

### 4. How would you design authorization in React?
Authorization controls what a user can access after authentication.

Common approaches:
- Role-based access control
- Permission-based access control
- Feature flags
- Route guards
- Component-level permission checks

Example:

```tsx
if (!user.permissions.includes("admin:read")) {
  return <AccessDenied />;
}
```

Authorization should also be enforced on the backend. Frontend checks are only for user experience.

---

### 5. How would you manage global state in a large React app?
Use global state only for data needed across many unrelated components.

Good candidates:
- Auth user
- Theme
- Language
- App preferences
- Feature flags

Avoid putting server data into global state manually. Use React Query, SWR, Apollo, or framework loaders for server state.

---

### 6. How would you decide between Context API and Redux/Zustand?
Use Context API for simple low-frequency global values like theme or auth.

Use Redux, Zustand, Jotai, or similar tools when:
- State changes frequently
- Many components consume different parts of state
- Debugging complex flows matters
- You need middleware
- You need predictable state transitions

Context is not always a full state management solution.

---

### 7. How would you design server state management?
Server state should be treated differently from client UI state.

Use tools like:
- React Query
- SWR
- Apollo Client
- Relay
- Next.js server actions/loaders

Server state includes:
- API data
- Cache
- Loading state
- Error state
- Refetching
- Pagination
- Optimistic updates

React Query is a strong default for REST APIs.

---

### 8. How would you design API integration in React?
Create a centralized API layer.

Example:

```txt
services/
  apiClient.ts
  userService.ts
  orderService.ts
```

Benefits:
- Consistent error handling
- Central auth handling
- Retry logic
- Request cancellation
- Typed responses
- Easier testing

Do not scatter `fetch()` calls randomly across components.

---

### 9. How would you handle API errors globally?
Use a centralized error handling strategy.

Handle:
- `400` validation errors
- `401` unauthorized
- `403` forbidden
- `404` not found
- `429` rate limit
- `500` server errors
- Network errors

Example behavior:
- Redirect on `401`
- Show access denied on `403`
- Show retry option on network errors
- Show form-level errors for validation failures

---

### 10. How would you design loading states in React?
Loading states should be designed at different levels.

Types:
- Page-level loading
- Section-level loading
- Button loading
- Skeleton UI
- Background refetch indicator
- Optimistic loading

Good UX avoids blocking the entire page when only one section is loading.

---

### 11. How would you design error boundaries?
Use error boundaries around major application sections.

Example boundaries:
- App-level boundary
- Route-level boundary
- Widget-level boundary
- Micro-frontend boundary

Error boundaries prevent one broken component from crashing the whole app.

They should:
- Show fallback UI
- Log errors
- Provide retry or navigation option
- Avoid exposing technical details to users

---

### 12. How would you design forms at scale?
Use a form library such as React Hook Form with schema validation.

Recommended stack:
- React Hook Form
- Zod or Yup
- Reusable input components
- Server-side validation mapping
- Accessible error messages

Forms should handle:
- Dirty state
- Touched state
- Validation state
- Submit state
- API errors
- Reset behavior

---

### 13. How would you design a multi-step form wizard?
A multi-step form should separate state, validation, and navigation.

Design considerations:
- Step-level validation
- Save progress
- Back/next navigation
- Draft persistence
- Final review page
- Server-side validation
- Resume later support

State can be stored in:
- Local component state
- Context
- Zustand
- URL/session storage
- Backend draft API

---

### 14. How would you design reusable UI components?
Reusable components should be generic, accessible, and style-consistent.

Examples:
- Button
- Input
- Modal
- Dropdown
- Tabs
- Table
- Card
- Toast

Good reusable components:
- Accept clear props
- Avoid business logic
- Support accessibility
- Support loading/disabled/error states
- Follow design system rules

---

### 15. How would you design a design system in React?
A React design system should include reusable components, design tokens, documentation, and usage rules.

Core parts:
- Colors
- Typography
- Spacing
- Icons
- Buttons
- Forms
- Modals
- Navigation
- Accessibility guidelines

Tools:
- Storybook
- Tailwind config
- CSS variables
- Figma tokens
- Component tests

---

### 16. How would you design theming in React?
Use CSS variables or a theme provider.

Recommended approach:

```css
:root {
  --color-bg: #ffffff;
  --color-text: #111827;
}

[data-theme="dark"] {
  --color-bg: #111827;
  --color-text: #ffffff;
}
```

Theme state can live in:
- Context
- Local storage
- User profile
- System preference

Avoid recalculating large style objects on every render.

---

### 17. How would you design dark mode?
Dark mode should support:
- System preference
- Manual override
- Persistence
- No flicker on load
- Accessible contrast
- Consistent design tokens

Use `prefers-color-scheme` and store user choice if they override it.

---

### 18. How would you design internationalization in React?
Internationalization should support translated text, dates, numbers, currencies, and pluralization.

Tools:
- react-i18next
- FormatJS
- next-intl

Design considerations:
- Lazy load language files
- Avoid hardcoded strings
- Support RTL languages if needed
- Format dates and currency by locale
- Keep translation keys organized

---

### 19. How would you design accessibility in a React application?
Accessibility should be part of component design from the start.

Key practices:
- Semantic HTML
- Keyboard navigation
- ARIA only when needed
- Visible focus states
- Proper labels
- Color contrast
- Screen reader testing
- Accessible modals and dropdowns

Accessibility should be tested with tools like axe, Lighthouse, and screen readers.

---

### 20. How would you design a modal system?
A modal system should support:
- Portal rendering
- Focus trapping
- Escape key close
- Backdrop click behavior
- Scroll locking
- Stacked modals if needed
- Accessible labels

Use React portals:

```tsx
createPortal(<Modal />, document.body);
```

Modals should not break keyboard navigation.

---

### 21. How would you design notifications or toast messages?
A toast system should support:
- Success, error, warning, info messages
- Auto-dismiss
- Manual dismiss
- Queueing
- Positioning
- Accessibility announcements

Global toast state can be managed with Context, Zustand, or a dedicated notification service.

---

### 22. How would you design a large data table in React?
Large tables require careful performance and UX design.

Features:
- Server-side pagination
- Sorting
- Filtering
- Column visibility
- Row selection
- Bulk actions
- Virtualization
- Sticky headers
- Loading and empty states

Avoid rendering thousands of rows directly. Use virtualization.

---

### 23. How would you design infinite scrolling?
Infinite scrolling should include:
- Cursor-based pagination
- Intersection Observer
- Loading indicator
- End-of-list state
- Error retry
- Scroll restoration
- Accessibility fallback

Cursor pagination is usually better than offset pagination for changing datasets.

---

### 24. How would you design pagination?
Pagination design depends on data size and user needs.

Options:
- Client-side pagination for small datasets
- Server-side pagination for large datasets
- Cursor-based pagination for feeds
- Offset pagination for admin tables

Include:
- Page size selection
- Total count if available
- Loading state
- Empty state
- URL query parameters

---

### 25. How would you design search in React?
Search design should consider performance and backend behavior.

Features:
- Debounced input
- Query parameters in URL
- Loading state
- Empty result state
- Recent searches
- Filter combinations
- Cancel previous requests

Use debounce to avoid calling APIs on every keystroke.

---

### 26. How would you design filtering and sorting?
Filtering and sorting should be reflected in the URL for shareability.

Example:

```txt
/products?category=books&sort=price_asc&page=2
```

Benefits:
- Bookmarkable
- Shareable
- Browser back button works
- Easier debugging
- Better page restoration

---

### 27. How would you design client-side caching?
Client-side caching should reduce unnecessary API calls and improve UX.

Strategies:
- Query cache
- Memory cache
- Local storage
- Session storage
- IndexedDB
- Service worker cache

Use React Query for most API cache use cases.

---

### 28. How would you design offline support?
Offline support requires a clear data strategy.

Options:
- Service workers
- IndexedDB
- Local queue for mutations
- Retry when online
- Conflict resolution
- Offline indicators

Best suited for apps like field service tools, note apps, dashboards, and mobile-first apps.

---

### 29. How would you design optimistic updates?
Optimistic updates immediately update UI before the server confirms.

Use cases:
- Likes
- Comments
- Toggles
- Small edits
- Task completion

Important parts:
- Update cache immediately
- Roll back on failure
- Show error message
- Avoid optimistic updates for high-risk financial actions

---

### 30. How would you design real-time updates in React?
Real-time updates can use:
- WebSockets
- Server-Sent Events
- Polling
- GraphQL subscriptions

Design considerations:
- Reconnect logic
- Heartbeats
- Backoff strategy
- Duplicate message handling
- Out-of-order events
- Connection status UI

---

### 31. How would you design a chat UI in React?
A chat UI should handle:
- Message list virtualization
- Real-time messages
- Optimistic sending
- Delivery status
- Read receipts
- Typing indicators
- Pagination for history
- Scroll-to-bottom behavior
- Offline retry

Avoid rendering the full message history at once.

---

### 32. How would you design a dashboard in React?
A dashboard should be modular and resilient.

Design:
- Independent widgets
- Widget-level loading
- Widget-level error states
- Refresh controls
- Role-based widgets
- Cached data
- Responsive layout

One failed widget should not crash the entire dashboard.

---

### 33. How would you design micro-frontends with React?
Micro-frontends split a large frontend into independently deployable applications.

Approaches:
- Module Federation
- Single-SPA
- iframe isolation
- Build-time integration

Challenges:
- Shared dependencies
- Styling conflicts
- Routing conflicts
- Authentication
- Versioning
- Performance overhead

Use micro-frontends only when team and deployment boundaries justify the complexity.

---

### 34. How would you design React with Module Federation?
Module Federation allows one app to load components from another app at runtime.

Use cases:
- Multiple teams own separate UI areas
- Independent deployments
- Shared shell application
- Plugin-based architecture

Important decisions:
- Shared React version
- Error boundaries
- Fallback loading
- Remote availability
- Contract testing

---

### 35. How would you design a plugin-based React application?
A plugin-based app allows features to be added dynamically.

Design:
- Plugin registry
- Defined extension points
- Permission model
- Lazy-loaded plugins
- Error isolation
- Version contracts

Example extension points:
- Sidebar item
- Dashboard widget
- Settings tab
- Form field
- Toolbar action

---

### 36. How would you design feature flags in React?
Feature flags allow enabling or disabling features without deployment.

Feature flags can control:
- Routes
- Buttons
- Experiments
- Beta features
- Role-based features

Best practices:
- Fetch flags early
- Cache flags
- Avoid deeply nested flag logic
- Remove old flags
- Never rely only on frontend flags for security

---

### 37. How would you design A/B testing in React?
A/B testing should assign users consistently to variants.

Design considerations:
- Stable user bucketing
- Analytics tracking
- Feature flag integration
- Avoid layout shift
- Measure conversion
- Respect privacy rules

The experiment assignment should usually come from the backend or experimentation platform.

---

### 38. How would you design analytics tracking in React?
Analytics should be centralized and consistent.

Track:
- Page views
- Button clicks
- Form submissions
- Errors
- Performance metrics
- Funnel events

Create an analytics service instead of calling analytics tools directly inside every component.

---

### 39. How would you design logging in React?
Frontend logging should capture useful debugging context.

Log:
- Runtime errors
- API failures
- Route changes
- User actions before error
- Browser/device details
- Correlation IDs

Tools:
- Sentry
- Datadog
- New Relic
- Azure Application Insights

Avoid logging sensitive data.

---

### 40. How would you design monitoring for React performance?
Monitor both technical and user-focused metrics.

Important metrics:
- Largest Contentful Paint
- Interaction to Next Paint
- Cumulative Layout Shift
- First Contentful Paint
- JavaScript bundle size
- Route load time
- API latency
- Error rate

Use real user monitoring in production.

---

### 41. How would you reduce React bundle size?
Bundle size can be reduced with:
- Code splitting
- Tree shaking
- Lazy loading
- Removing unused dependencies
- Using smaller libraries
- Dynamic imports
- Route-level splitting
- Bundle analyzer

Avoid importing entire libraries when only one function is needed.

---

### 42. How would you optimize rendering performance?
Rendering performance can be improved by:
- Splitting large components
- Keeping state local
- Using memoization carefully
- Avoiding inline object creation where it matters
- Virtualizing long lists
- Avoiding unnecessary context updates
- Using React Profiler

Do not blindly memoize everything. Measure first.

---

### 43. How would you design context to avoid unnecessary re-renders?
Context causes consumers to re-render when the provider value changes.

Better design:
- Split context by concern
- Memoize provider values
- Avoid putting frequently changing state in broad context
- Use selector-based stores if needed
- Keep context values small

Example:

```tsx
const value = useMemo(() => ({ user, logout }), [user, logout]);
```

---

### 44. How would you design a React app for SEO?
SEO depends on rendering strategy.

Use:
- Server-side rendering
- Static generation
- Metadata management
- Semantic HTML
- Structured data
- Fast page load
- Clean URLs
- Sitemap
- Open Graph tags

For SEO-heavy apps, frameworks like Next.js are often preferred.

---

### 45. How would you design SSR with React?
Server-side rendering sends HTML from the server before JavaScript loads.

Benefits:
- Better initial load
- Better SEO
- Better perceived performance

Challenges:
- Hydration errors
- Server/client mismatch
- More infrastructure complexity
- Data fetching coordination
- Caching strategy

Use SSR for public, SEO-sensitive, or performance-critical pages.

---

### 46. How would you prevent hydration mismatch?
Hydration mismatch happens when server-rendered HTML differs from client-rendered HTML.

Common causes:
- Using `Date.now()` during render
- Random values during render
- Browser-only APIs on server
- Different locale output
- Conditional rendering based on `window`

Fixes:
- Use client-only effects
- Use stable initial values
- Guard browser APIs
- Keep server/client render output consistent

---

### 47. How would you design file upload in React?
File upload design should support:
- File validation
- Size limits
- Type validation
- Progress indicator
- Cancel upload
- Retry failed upload
- Multiple files
- Drag and drop
- Direct upload to cloud storage

For large files, use chunked upload or signed URLs.

---

### 48. How would you design image-heavy React applications?
Image-heavy apps need performance-focused design.

Use:
- Lazy loading
- Responsive images
- Modern formats like WebP/AVIF
- CDN
- Placeholder blur
- Proper dimensions
- Infinite scroll with virtualization
- Avoid layout shift

Images should not block the main user interaction path.

---

### 49. How would you design a React application for multiple tenants?
Multi-tenant React apps should support tenant-specific configuration.

Tenant-specific items:
- Branding
- Theme
- Logo
- Permissions
- Feature flags
- Navigation
- API base URL
- Localization

Tenant config should usually be loaded before rendering the main app shell.

---

### 50. How would you design a React application for enterprise role-based dashboards?
Enterprise dashboards need modular, secure, and configurable architecture.

Design:
- Role-based navigation
- Permission-based widgets
- Configurable dashboard layout
- Server-driven data access
- Audit logging
- Export support
- Drill-down pages
- Real-time updates where needed
- Accessibility compliance
- Strong error handling

The frontend should hide unauthorized UI, but the backend must enforce all permissions.

---

### 51. How would you design route-level code splitting?
Route-level code splitting loads only the JavaScript needed for the current route.

Approach:
- Use `React.lazy`
- Wrap lazy components in `Suspense`
- Split by feature routes
- Preload high-probability next routes

This improves initial load performance for large applications.

---

### 52. How would you design state persistence in React?
State persistence depends on the type of state.

Options:
- URL params for shareable state
- Local storage for preferences
- Session storage for temporary session state
- IndexedDB for larger offline data
- Backend persistence for important business state

Avoid persisting sensitive data in browser storage.

---

### 53. How would you design browser back-button behavior for complex UI?
Important UI state should be reflected in the URL.

Examples:
- Search query
- Filters
- Selected tab
- Page number
- Modal route if needed

This makes navigation predictable and improves shareability.

---

### 54. How would you design request cancellation in React?
Request cancellation prevents race conditions and unnecessary work.

Use `AbortController` with `fetch`:

```tsx
useEffect(() => {
  const controller = new AbortController();

  fetch("/api/users", { signal: controller.signal });

  return () => controller.abort();
}, []);
```

It is useful for search, autocomplete, route changes, and component unmounts.

---

### 55. How would you design autocomplete in React?
Autocomplete should be fast, accessible, and resilient.

Design:
- Debounced input
- Request cancellation
- Keyboard navigation
- Highlighted option
- Empty state
- Loading state
- Error retry
- Cached recent results

Use ARIA combobox patterns for accessibility.

---

### 56. How would you design a reusable permission system?
Create a permission utility and wrapper components.

Example:

```tsx
function Can({ permission, children }) {
  const user = useAuthUser();
  return user.permissions.includes(permission) ? children : null;
}
```

Use it for UI visibility only. Backend APIs must still enforce permissions.

---

### 57. How would you design a frontend configuration system?
Frontend configuration can include API URLs, feature flags, branding, and environment-specific values.

Approaches:
- Build-time environment variables
- Runtime config endpoint
- Tenant config API
- Static JSON config file

Runtime config is better when the same build is deployed to multiple environments.

---

### 58. How would you design testing strategy for a large React app?
Use multiple levels of testing.

Recommended layers:
- Unit tests for utilities and hooks
- Component tests for UI behavior
- Integration tests for feature flows
- E2E tests for critical user journeys
- Visual regression tests for design system components

Test behavior, not implementation details.

---

### 59. How would you design CI/CD for React applications?
A React CI/CD pipeline should include:
- Install dependencies
- Type check
- Lint
- Unit tests
- Build
- Bundle size check
- Security audit
- E2E tests where appropriate
- Deploy to preview environment
- Promote to production

Preview deployments are useful for product and QA review.

---

### 60. How would you design a React app for long-term maintainability?
Long-term maintainability requires clear technical boundaries and conventions.

Important practices:
- Feature-based structure
- TypeScript
- Shared design system
- Consistent data-fetching pattern
- Clear naming conventions
- Automated tests
- Linting and formatting
- Documentation for complex decisions
- Regular dependency updates
- Removing unused code and stale feature flags

A maintainable React application should be easy for new developers to understand, change, test, and deploy.

