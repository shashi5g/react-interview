# Nx Monorepo Micro-Frontend Interview Questions and Answers

This README contains interview questions and answers focused on Nx monorepos, micro-frontends, Module Federation, architecture, CI/CD, deployment, and senior-level frontend system design.

## Beginner Level

### 1. What is Nx?
Nx is a build system and monorepo toolkit for managing multiple applications and libraries in one workspace.

It provides:
- Monorepo structure
- Code generation
- Dependency graph
- Affected builds and tests
- Caching
- Task orchestration
- Plugin support for frameworks like React, Angular, Next.js, Node.js, and more

Nx is commonly used in large frontend and full-stack enterprise applications.

---

### 2. What is a monorepo?
A monorepo is a single repository that contains multiple applications and libraries.

Example:

```txt
apps/
  shell/
  admin/
  dashboard/
libs/
  ui/
  auth/
  data-access/
  shared-utils/
```

Benefits:
- Shared code is easier to manage
- Consistent tooling
- Easier refactoring across projects
- Better dependency visibility
- Centralized CI/CD workflows

---

### 3. What is the difference between monorepo and polyrepo?
A monorepo stores multiple projects in one repository.

A polyrepo stores each project in a separate repository.

Monorepo benefits:
- Easier code sharing
- Atomic commits across apps/libs
- Unified tooling
- Central dependency management

Polyrepo benefits:
- Stronger repository isolation
- Smaller repository size
- Independent access control
- Simpler ownership for small teams

Nx helps solve many monorepo scaling problems using caching and affected commands.

---

### 4. What is a micro-frontend?
A micro-frontend is an architectural pattern where a frontend application is split into independently owned and deployable frontend modules.

Example:
- Shell app owns navigation and layout
- Product team owns product app
- Checkout team owns checkout app
- Profile team owns user profile app

Micro-frontends are useful when multiple teams need independent delivery.

---

### 5. Why use Nx for micro-frontends?
Nx is useful for micro-frontends because it provides:
- Workspace structure
- Code sharing through libraries
- Module Federation support
- Dependency graph visualization
- Affected builds and tests
- Local development orchestration
- Consistent linting, testing, and build commands

Nx reduces the operational complexity of managing multiple frontend applications.

---

### 6. What is Module Federation?
Module Federation is a Webpack feature that allows one application to load code from another application at runtime.

In micro-frontends:
- Host or shell loads remote applications
- Remote apps expose modules or routes
- Shared dependencies can be configured

Example:

```txt
shell -> loads remote dashboard
shell -> loads remote admin
shell -> loads remote profile
```

---

### 7. What is a host application in micro-frontends?
A host application, often called a shell, is the main application that loads remote micro-frontends.

Responsibilities:
- Global layout
- Navigation
- Authentication shell
- Routing composition
- Loading remote apps
- Shared global providers
- Error boundaries around remotes

The host coordinates the user experience across micro-frontends.

---

### 8. What is a remote application?
A remote application is a separately built micro-frontend that exposes components, routes, or modules to a host application.

Example:
- `dashboard` remote exposes dashboard routes
- `admin` remote exposes admin panel routes
- `profile` remote exposes user profile components

Remote apps can often run independently during local development.

---

### 9. What is an Nx library?
An Nx library is a reusable package inside the workspace.

Examples:

```txt
libs/ui
libs/auth
libs/api-client
libs/shared-types
libs/util-formatting
```

Libraries help share code across applications while keeping clear boundaries.

---

### 10. What is the Nx dependency graph?
The Nx dependency graph visually shows relationships between apps and libraries.

It helps answer:
- Which apps depend on this library?
- What is affected by a change?
- Are there circular dependencies?
- Are architectural boundaries being followed?

Command:

```bash
nx graph
```

---

## Intermediate Level

### 11. How would you structure an Nx workspace for micro-frontends?
A common structure is:

```txt
apps/
  shell/
  dashboard/
  admin/
  profile/
libs/
  ui/
  auth/
  data-access/
  shared-types/
  shared-utils/
```

Guidelines:
- Apps contain deployable units
- Libraries contain shared logic
- Feature-specific libraries stay close to domain ownership
- Shared UI goes into a design system library
- Shared API clients go into data-access libraries

---

### 12. How do you decide what should be an app vs a library in Nx?
Use an app when it is deployable or runnable independently.

Use a library when it is reusable code consumed by apps or other libraries.

App examples:
- Shell app
- Dashboard remote
- Admin remote

Library examples:
- Button components
- Auth utilities
- API client
- Validation schemas
- Shared TypeScript types

---

### 13. What are affected commands in Nx?
Affected commands run tasks only for projects impacted by a change.

Examples:

```bash
nx affected:test
nx affected:build
nx affected:lint
```

Benefits:
- Faster CI
- Avoids rebuilding everything
- Scales better in large monorepos
- Uses dependency graph to determine impact

---

### 14. What is Nx caching?
Nx caching stores task outputs so repeated tasks can be skipped if inputs have not changed.

Cached tasks can include:
- Builds
- Tests
- Linting
- Type checks

Benefits:
- Faster local development
- Faster CI pipelines
- Reduced compute cost

Nx can use local cache and remote cache.

---

### 15. What is remote caching in Nx?
Remote caching allows teams and CI pipelines to share cached task results.

If one developer or CI job builds a project, another developer or CI job can reuse that result.

Benefits:
- Faster CI
- Faster onboarding
- Less duplicate work
- Better scalability for large teams

Nx Cloud is commonly used for remote caching.

---

### 16. What is distributed task execution in Nx?
Distributed task execution splits tasks across multiple machines.

Useful when:
- Many apps/libs exist
- CI is slow
- Large test suites exist
- Multiple builds can run in parallel

It helps large monorepos keep CI times manageable.

---

### 17. How does Nx help enforce architecture boundaries?
Nx can enforce module boundaries using lint rules and project tags.

Example tags:

```json
{
  "tags": ["scope:auth", "type:data-access"]
}
```

Rules can prevent:
- Feature libraries importing unrelated features
- UI libraries importing data-access libraries
- Circular dependencies
- Apps depending on forbidden internal libraries

---

### 18. What are project tags in Nx?
Project tags are metadata labels used to describe project type, scope, or ownership.

Examples:
- `type:ui`
- `type:feature`
- `type:data-access`
- `scope:admin`
- `scope:shared`

Tags are often used with dependency constraints to enforce clean architecture.

---

### 19. What is the difference between build-time and runtime integration?
Build-time integration means shared code is compiled together before deployment.

Example:
- Shell imports `libs/ui` at build time

Runtime integration means one app loads another app while running.

Example:
- Shell loads dashboard remote through Module Federation

Micro-frontends usually use runtime integration for independently deployed apps.

---

### 20. What are the benefits of Module Federation in Nx?
Benefits:
- Independent deployment of remotes
- Runtime loading of features
- Better team autonomy
- Smaller ownership boundaries
- Shared dependencies
- Shell-driven composition

Nx simplifies configuration and local development for Module Federation setups.

---

## Advanced Level

### 21. How would you design routing in an Nx micro-frontend architecture?
The shell should own top-level routing and delegate route segments to remotes.

Example:

```txt
/              -> shell home
/dashboard     -> dashboard remote
/admin         -> admin remote
/profile       -> profile remote
```

Design considerations:
- Shell owns global navigation
- Remote owns internal child routes
- Route contracts should be documented
- Unauthorized routes should be protected
- Lazy loading should happen at route boundaries

---

### 22. How would you handle authentication across micro-frontends?
Authentication should be centralized and consistent.

Recommended approach:
- Shell validates session
- Shared auth library provides auth utilities
- Token/session handling is not duplicated in every remote
- Backend still enforces authorization
- Remotes receive user context through shared providers or APIs

Avoid each remote implementing separate login behavior.

---

### 23. How would you handle authorization across remotes?
Authorization should be enforced both in the frontend and backend.

Frontend responsibilities:
- Hide unauthorized navigation
- Hide unauthorized actions
- Show access denied pages

Backend responsibilities:
- Enforce API permissions
- Validate tenant/user access
- Prevent data leakage

Use a shared permissions library to keep checks consistent.

---

### 24. How would you share UI components across micro-frontends?
Create a shared design system library.

Example:

```txt
libs/ui/button
libs/ui/modal
libs/ui/table
libs/ui/forms
```

Benefits:
- Consistent user experience
- Less duplication
- Central accessibility fixes
- Common styling standards

Versioning and breaking changes should be handled carefully because many remotes may depend on shared UI.

---

### 25. How would you share TypeScript types across apps?
Create a shared types library.

Example:

```txt
libs/shared-types
```

Use it for:
- API response types
- Domain models
- Permission models
- Shared enums
- Event contracts

Be careful not to create a giant shared library that couples all teams together.

---

### 26. How would you avoid tight coupling in a monorepo?
Avoid tight coupling by:
- Using clear library boundaries
- Enforcing dependency constraints
- Avoiding large shared utility libraries
- Keeping domain logic inside domain libraries
- Using contracts between remotes
- Avoiding direct imports from another team's internal code

Shared code should be intentional, stable, and well-owned.

---

### 27. How would you handle version conflicts in Module Federation?
Version conflicts can happen when host and remotes use different dependency versions.

Strategies:
- Share critical dependencies like React as singletons
- Align major versions across workspace
- Use strict version checks where appropriate
- Test remotes with host before deployment
- Avoid sharing unstable dependencies globally

Example shared config:

```js
shared: {
  react: { singleton: true, strictVersion: true },
  "react-dom": { singleton: true, strictVersion: true }
}
```

---

### 28. How would you handle failure of a remote micro-frontend?
Remote failure should not crash the whole app.

Use:
- Error boundaries around remote apps
- Fallback UI
- Retry option
- Remote availability monitoring
- Graceful degradation
- Logging and alerting

The shell should remain usable even if one remote is unavailable.

---

### 29. How would you handle loading states for remotes?
Use Suspense or route-level loading UI.

Good loading design:
- Show skeleton or section loader
- Avoid blank page
- Keep shell navigation available
- Handle slow networks
- Show retry on failure

Remote loading should feel like part of the same product, not a separate app booting awkwardly.

---

### 30. How would you handle shared global state across micro-frontends?
Keep shared global state minimal.

Good shared state candidates:
- Auth user
- Theme
- Locale
- Feature flags

Avoid sharing large business state globally. Each remote should own its domain state where possible.

Options:
- Shared provider in shell
- Shared state library
- URL state
- Backend/state synchronization
- Event bus for limited communication

---

### 31. How would remotes communicate with each other?
Prefer loose coupling.

Options:
- URL parameters
- Shared backend APIs
- Browser custom events
- Shared event bus
- Shell-mediated communication
- Shared state for small global concerns

Avoid direct imports between remotes because it breaks independence.

---

### 32. How would you design an event bus for micro-frontends?
An event bus can help remotes communicate without direct dependency.

Design considerations:
- Typed event contracts
- Clear event ownership
- Avoid excessive global events
- Support unsubscribe
- Log important events
- Prevent memory leaks

Example events:
- `cart:item-added`
- `auth:user-updated`
- `notification:show`

Use event bus carefully. Too many events can make the system hard to debug.

---

### 33. How would you handle styling across micro-frontends?
Styling should avoid conflicts between remotes.

Options:
- Shared design system
- CSS Modules
- Tailwind with shared config
- CSS-in-JS with scoped styles
- Shadow DOM for strong isolation

Risks:
- Global CSS conflicts
- Different design tokens
- Duplicate styles
- Inconsistent spacing and typography

A shared design system helps maintain consistency.

---

### 34. How would you handle environment configuration?
Each app may need environment-specific configuration.

Examples:
- API URLs
- Remote URLs
- Feature flags
- Auth settings
- Analytics keys

Approaches:
- Build-time environment variables
- Runtime config endpoint
- Static config JSON
- Deployment-specific remote manifest

Runtime configuration is useful when the same build must run in multiple environments.

---

### 35. How would you manage remote URLs in production?
Remote URLs should be configurable per environment.

Example:

```txt
DEV: https://dev-dashboard.example.com/remoteEntry.js
QA: https://qa-dashboard.example.com/remoteEntry.js
PROD: https://dashboard.example.com/remoteEntry.js
```

A remote manifest can help the shell discover remote URLs dynamically.

---

### 36. How would you deploy Nx micro-frontends?
Deployment options:
- Deploy shell and remotes independently
- Deploy all apps together from one pipeline
- Use affected deployment to deploy only changed apps
- Use containers or static hosting depending on framework

A common senior-level approach is independent deployment with integration checks.

---

### 37. What is affected deployment?
Affected deployment means only deploying applications impacted by a change.

Nx can determine affected apps from the dependency graph.

Example:
- Change in `libs/ui` affects shell, dashboard, and admin
- Change in `apps/profile` affects only profile remote

This reduces deployment time and risk.

---

### 38. How would you design CI/CD for an Nx monorepo?
A strong Nx CI/CD pipeline includes:
- Install dependencies
- Format check
- Lint affected projects
- Test affected projects
- Build affected projects
- Run E2E tests for critical flows
- Use remote caching
- Deploy affected apps
- Publish artifacts

CI should use Nx affected commands to avoid unnecessary work.

---

### 39. How would you test Nx micro-frontends?
Testing should happen at multiple levels.

Test types:
- Unit tests for utilities
- Component tests for UI libraries
- Integration tests for feature libraries
- Contract tests between shell and remotes
- E2E tests for full user flows
- Visual regression tests for design system

Test both remotes independently and inside the shell.

---

### 40. What are contract tests in micro-frontends?
Contract tests verify that remotes expose what the host expects.

Examples:
- Remote exposes correct module name
- Route export exists
- Component props are compatible
- Shared event contracts are valid
- Required permissions metadata exists

Contract tests reduce runtime integration failures.

---

## Senior System Design Level

### 41. How would you design a shell application for enterprise micro-frontends?
A shell should own cross-cutting concerns.

Responsibilities:
- Global layout
- Top-level routing
- Navigation
- Authentication context
- Theme and locale providers
- Feature flag provider
- Remote loading
- Remote error boundaries
- Observability setup

The shell should not contain every domain's business logic.

---

### 42. How would you decide whether micro-frontends are necessary?
Use micro-frontends when organizational scale justifies the complexity.

Good reasons:
- Multiple teams need independent deployment
- Different domains have separate ownership
- Release cycles differ significantly
- Large frontend is becoming hard to coordinate

Bad reasons:
- It sounds modern
- Small team with one app
- Avoiding normal modular architecture
- No real independent deployment need

Micro-frontends add complexity, so they should solve a real team or scaling problem.

---

### 43. What are the trade-offs of Nx monorepo micro-frontends?
Benefits:
- Shared tooling
- Code reuse
- Dependency graph
- Affected builds
- Better consistency
- Easier cross-project refactoring

Trade-offs:
- Repository can become large
- Ownership boundaries must be enforced
- Shared libraries can create coupling
- CI/CD needs careful design
- Module Federation adds runtime complexity

Senior engineers should understand both benefits and costs.

---

### 44. How would you prevent a shared library from becoming a dumping ground?
Use clear ownership and purpose.

Rules:
- Every shared library has an owner
- Avoid generic `shared-utils` growth
- Split libraries by domain or purpose
- Enforce dependency constraints
- Review shared API changes carefully
- Remove unused exports

A bad shared library creates hidden coupling across the monorepo.

---

### 45. How would you handle breaking changes in shared libraries?
Strategies:
- Use semantic versioning if libraries are published
- Use migration generators
- Update affected apps in the same PR when possible
- Communicate breaking changes
- Add compatibility wrappers temporarily
- Use tests to identify affected consumers

In a monorepo, atomic commits make breaking changes easier to coordinate.

---

### 46. How would you design observability for micro-frontends?
Observability should work across shell and remotes.

Track:
- Remote load failures
- JavaScript runtime errors
- Route transition performance
- API latency
- User actions
- Web vitals
- Correlation IDs
- Remote version loaded

Tools:
- Sentry
- Datadog
- New Relic
- Azure Application Insights
- OpenTelemetry

Include app and remote name in logs.

---

### 47. How would you handle feature flags across Nx micro-frontends?
Feature flags should be consistent across host and remotes.

Design:
- Shell loads flags early
- Shared feature flag library exposes access methods
- Remotes consume the same flag context
- Backend still enforces protected features
- Old flags are removed regularly

Avoid each remote calling a different flag service independently unless there is a strong reason.

---

### 48. How would you handle performance optimization in Nx micro-frontends?
Performance strategies:
- Lazy load remotes
- Share React as singleton
- Avoid duplicate dependencies
- Use route-level code splitting
- Use Nx affected builds
- Analyze bundles per remote
- Preload important remotes
- Cache remote assets with correct headers
- Monitor real user performance

A micro-frontend architecture should not make users download unnecessary code.

---

### 49. How would you secure a micro-frontend architecture?
Security considerations:
- Enforce auth on backend APIs
- Validate remote URLs
- Use HTTPS
- Set Content Security Policy
- Avoid exposing secrets in frontend builds
- Limit cross-origin risks
- Protect against dependency supply-chain issues
- Scan dependencies
- Restrict who can deploy remotes

Frontend authorization improves UX, but backend authorization provides real security.

---

### 50. What are common mistakes in Nx micro-frontend projects?
Common mistakes:
- Using micro-frontends without team-scale need
- Sharing too much state globally
- Allowing remotes to directly depend on each other
- No contract testing
- No remote failure fallback
- Duplicating React in bundles
- No clear ownership of shared libraries
- Ignoring dependency boundaries
- Slow CI from not using affected commands
- Using one giant shared utility library
- Deploying remotes independently without integration checks

A strong Nx micro-frontend architecture balances team autonomy with system consistency.
