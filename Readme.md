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
