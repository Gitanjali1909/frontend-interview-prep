# React.js Interview Q&A (Core Concepts)

---

## 1. What is React?

**Answer:**  
React is a **JavaScript library** for building **interactive UIs**.  
It uses a **component-based architecture** and **Virtual DOM** to efficiently update the view when data changes.

**Visual:**  
```
UI → Components → Virtual DOM → Real DOM
```

---

## 2. What are Components?

**Answer:**  
Components are **independent, reusable pieces of UI**.  
They can be functional or class-based.

```
function Greeting() {
  return <h1>Hello World</h1>;
}
```

**Visual:**  
```
App
 ├─ Header
 ├─ Body
 │   ├─ Sidebar
 │   └─ Content
 └─ Footer
```

---

## 3. What is JSX?

**Answer:**  
JSX (JavaScript XML) lets you **write HTML in JavaScript**.  
It’s converted into `React.createElement()` under the hood.

```
const element = <h1>Hello JSX</h1>;
```

**Visual:**  
```
JSX → React.createElement → Virtual DOM Object → Render to Real DOM
```

---

## 4. What is the Virtual DOM?

**Answer:**  
Virtual DOM is a lightweight in-memory tree representing the real DOM.  
React updates only the changed parts using **diffing**.

**Visual:**  
```
Virtual DOM
 ├─ Compare old vs new tree
 └─ Update changed nodes → Real DOM
```

---

## 5. Difference between Real DOM and Virtual DOM

| Real DOM | Virtual DOM |
|-----------|--------------|
| Directly updates browser DOM | Updates in memory |
| Slower | Faster |
| Repaints whole UI | Updates only diff |

---

## 6. What are Props?

**Answer:**  
Props are **inputs to components** that make them reusable. They are **immutable** inside the component.

```
function Welcome(props) {
  return <h2>Hello {props.name}</h2>;
}
```

**Visual:**  
```
Parent → (props) → Child
```

---

## 7. What is State?

**Answer:**  
State is **mutable data** managed within a component.  
Updating it triggers a re-render.

```
const [count, setCount] = useState(0);
```

**Visual:**  
```
User Action → setState() → Re-render → UI Updates
```

---

## 8. Difference between Props and State

| Props | State |
|--------|--------|
| Passed from parent | Managed inside component |
| Immutable | Mutable |
| External data | Internal data |

---

## 9. What is useState Hook?

**Answer:**  
`useState` allows function components to have local state.

```
const [name, setName] = useState("Alice");
```

---

## 10. What is useEffect Hook?

**Answer:**  
`useEffect` lets you run **side effects** (fetch, timers, DOM updates) after render.

```
useEffect(() => {
  console.log("Mounted");
}, []);
```

**Visual:**  
```
Render → useEffect() → Side Effects
```

---

## 11. What is useRef?

**Answer:**  
`useRef` gives direct access to DOM elements or stores mutable values without re-rendering.

```
const inputRef = useRef();
```

**Visual:**  
```
ref.current → DOM node reference
```

---

## 12. What is useMemo?

**Answer:**  
`useMemo` caches expensive computations to improve performance.

```
const result = useMemo(() => compute(a, b), [a, b]);
```

**Visual:**  
```
If dependencies same → use cached result
```

---

## 13. What is useCallback?

**Answer:**  
`useCallback` memoizes functions to prevent unnecessary re-creations.

```
const handleClick = useCallback(() => console.log("Click"), []);
```

---

## 14. What is useContext?

**Answer:**  
`useContext` allows components to **consume global data** without prop drilling.

```
const value = useContext(ThemeContext);
```

**Visual:**  
```
Provider → (Context) → Consumer
```

---

## 15. What are Controlled and Uncontrolled Components?

**Answer:**  
- **Controlled:** Form data handled by React state.  
- **Uncontrolled:** DOM manages its own state.

```
<input value={name} onChange={e => setName(e.target.value)} />
```

**Visual:**  
```
Controlled: React ↔ State ↔ Input
Uncontrolled: DOM ↔ Input Value
```

---

## 16. What is Conditional Rendering?

**Answer:**  
Show components based on conditions.

```
{isLoggedIn ? <Dashboard /> : <Login />}
```

---

## 17. What are Lists and Keys?

**Answer:**  
Keys help React identify which items change in a list.

```
{users.map(u => <li key={u.id}>{u.name}</li>)}
```

**Visual:**  
```
List diffing uses key to track updates
```

---

## 18. What is React Fragment?

**Answer:**  
`<React.Fragment>` groups multiple elements without extra DOM nodes.

```
<>
  <h1>Title</h1>
  <p>Text</p>
</>
```

---

## 19. What are Lifecycle Methods?

**Answer:**  
Phases: **Mounting → Updating → Unmounting**

**Class example:**
```
componentDidMount() { console.log("Mounted"); }
```

**Visual:**  
```
Mount → Render → Update → Unmount
```

---

## 20. Functional Lifecycle with useEffect

**Answer:**  
`useEffect` replaces lifecycle methods in functional components.

```
useEffect(() => { /* componentDidMount */ }, []);
```

---

## 21. What is Lifting State Up?

**Answer:**  
Move shared state to the nearest parent to sync data between children.

**Visual:**  
```
Parent
 ├─ ChildA (shares state)
 └─ ChildB (uses same data)
```

---

## 22. What is Context API?

**Answer:**  
Context provides **global data** access without prop drilling.

```
const ThemeContext = createContext();
```

---

## 23. What is Reconciliation?

**Answer:**  
React compares new Virtual DOM with previous to apply minimal changes.

**Visual:**  
```
Old VDOM ↔ Diff ↔ New VDOM → DOM Patch
```

---

## 24. What is React Fiber?

**Answer:**  
React Fiber is the **new reconciliation engine** that enables incremental rendering and pausing work.

**Visual:**  
```
Work Units → Pause/Resume → Commit Changes
```

---

## 25. What are Synthetic Events?

**Answer:**  
React’s wrapper around native events for cross-browser compatibility.

```
<button onClick={handleClick}>Click</button>
```

---

## 26. What are Pure Components?

**Answer:**  
Class components that only re-render if props/state change (shallow compare).

```
class MyComp extends React.PureComponent {}
```

---

## 27. What is React.memo?

**Answer:**  
Prevents re-render if props didn’t change (for functional components).

```
export default React.memo(MyComponent);
```

---

## 28. What are Higher-Order Components (HOC)?

**Answer:**  
Functions that wrap components to add extra behavior.

```
const withLogger = Comp => props => {
  console.log("Rendered");
  return <Comp {...props} />;
};
```

**Visual:**  
```
Input Component → HOC → Enhanced Component
```

---

## 29. What is Lazy Loading?

**Answer:**  
Load components only when needed.

```
const About = React.lazy(() => import('./About'));
```

---

## 30. What is Suspense?

**Answer:**  
Used with lazy components to show fallback during loading.

```
<Suspense fallback={<Loader />}>
  <About />
</Suspense>
```

---

## 31. What is Error Boundary?

**Answer:**  
Catches JS errors in child components.

```
componentDidCatch(error, info) { console.log(error); }
```

---

## 32. What is StrictMode?

**Answer:**  
Helps detect potential issues in development (doesn’t affect prod).

```
<React.StrictMode><App /></React.StrictMode>
```

---

## 33. What is Prop Drilling?

**Answer:**  
Passing props through multiple levels unnecessarily.  
Solved by Context or state managers.

---

## 34. What is Refs Forwarding?

**Answer:**  
Passing refs to child components using `forwardRef`.

```
const MyInput = forwardRef((props, ref) => <input ref={ref} />);
```

---

## 35. What is useReducer?

**Answer:**  
Alternative to useState for complex logic.

```
const [state, dispatch] = useReducer(reducer, initial);
```

**Visual:**  
```
Action → Reducer → State → UI
```

---

## 36. What is useLayoutEffect?

**Answer:**  
Runs **before** the browser paints — for layout measurement.

---

## 37. What is the difference between useEffect and useLayoutEffect?

| useEffect | useLayoutEffect |
|------------|-----------------|
| Runs after paint | Runs before paint |
| Non-blocking | Blocking |
| For async tasks | For layout reads |

---

## 38. What is Rendering in React?

**Answer:**  
Process of converting component JSX → Virtual DOM → Real DOM.

**Visual:**  
```
JSX → VDOM → Diff → Real DOM
```

---

## 39. What is Hydration?

**Answer:**  
Attaching React event handlers to server-rendered HTML (SSR).

---

## 40. What is Concurrent Mode?

**Answer:**  
Feature that allows React to interrupt rendering for higher-priority tasks, improving responsiveness.

---

## 41. What is React 18’s automatic batching?

**Answer:**  
Combines multiple state updates into a single re-render for efficiency.

---

## 42. What are Render Props?

**Answer:**  
A technique for sharing logic by passing a function as a prop.

```
<DataProvider render={data => <List data={data} />} />
```

---

## 43. What are Custom Hooks?

**Answer:**  
Functions that reuse hook logic.

```
function useFetch(url) {
  const [data, setData] = useState();
  useEffect(() => fetch(url).then(r=>r.json()).then(setData), [url]);
  return data;
}
```

---

## 44. What is Key Prop and Why is it Important?

**Answer:**  
Helps React identify which items changed or moved in lists.

---

## 45. What is a Pure Function in React?

**Answer:**  
Function with no side effects; same input → same output.  
Used in reducers and render logic.

---

## 46. What is ReactDOM?

**Answer:**  
Package that provides DOM-specific methods (like `createRoot`, `render`).

---

## 47. What is Re-rendering?

**Answer:**  
When state or props change, component runs render again.

**Visual:**  
```
State change → Virtual DOM diff → DOM update
```

---

## 48. What is the difference between Controlled and Uncontrolled Inputs?

| Controlled | Uncontrolled |
|-------------|--------------|
| Value in React state | Value in DOM |
| Updates via setState | Uses ref |

---

## 49. What is the importance of keys in React Lists?

**Answer:**  
Without keys, React reuses DOM nodes incorrectly, causing bugs.

---

## 50. What is Strict Mode double rendering?

**Answer:**  
React (in dev mode) renders components twice to detect side effects.

---

## 51. What are Side Effects?

**Answer:**  
Operations like fetching data, timers, logging — handled via `useEffect`.

---

## 52. What is React’s Diffing Algorithm?

**Answer:**  
Algorithm to efficiently compare Virtual DOM trees.

**Visual:**  
```
Old Tree
 ├─ A
 ├─ B
 └─ C

New Tree
 ├─ A
 ├─ B (changed)
 └─ D (added)
→ Only update B and D
```

---

## 53. What is useId?

**Answer:**  
Generates unique IDs that stay consistent between server and client renders.

```
const id = useId();
```

---

## 54. What is Profiler in React?

**Answer:**  
Tool to measure rendering performance and identify slow components.

---

## 55. What are controlled re-renders?

**Answer:**  
Optimizing re-renders with `React.memo`, `useMemo`, `useCallback`.

---

## 56. What is Reconciliation Phases?

**Answer:**  
- **Render phase:** Calculates what to change.  
- **Commit phase:** Applies changes to DOM.

**Visual:**  
```
Render (Virtual DOM) → Commit (Real DOM)
```

---

## 57. What is React DevTools?

**Answer:**  
Browser extension for inspecting React component trees, props, and performance.

---

## 58. What are children props?

**Answer:**  
Special prop for nested elements.

```
<Card>
  <Title />
</Card>
```

---

## 59. What is defaultProps?

**Answer:**  
Set default values for props when none are passed.

```
MyComp.defaultProps = { name: "Guest" };
```

---

## 60. What is PropTypes?

**Answer:**  
Typechecking props in components.

```
MyComp.propTypes = { name: PropTypes.string };
```

---

## 61. What is Rendering Optimization?

**Answer:**  
Avoiding unnecessary re-renders with:
- `React.memo`
- `useMemo`
- `useCallback`
- `key` usage

---

## 62. What is StrictMode’s purpose?

**Answer:**  
Detects unsafe lifecycle methods, side effects, legacy APIs in dev.

---

## 63. What is the difference between Mounting and Rendering?

**Answer:**  
Mounting → first insertion into DOM  
Rendering → every time the UI updates

---

## 64. What are SyntheticEvent differences?

**Answer:**  
React wraps native events into a single cross-browser object.

---

## 65. What is shallow rendering?

**Answer:**  
Testing technique rendering component without its children using Enzyme.

---

## 66. What are Portals?

**Answer:**  
Render children into a different DOM subtree.

```
ReactDOM.createPortal(<Modal />, root);
```

**Visual:**  
```
App
 └─ Portal → Renders to separate DOM node
```

---

## 67. What are concurrent features?

**Answer:**  
Features like transitions, streaming SSR, and Suspense for data fetching that improve responsiveness.

---

## 68. What is Transition API (useTransition)?

**Answer:**  
Lets you mark updates as non-urgent.

```
const [isPending, startTransition] = useTransition();
```

---

## 69. What is useDeferredValue?

**Answer:**  
Defers value updates to keep UI responsive.

---

## 70. How to improve performance in React?

**Answer:**  
- Memoization (useMemo, React.memo)  
- Lazy Loading  
- Code splitting  
- Avoid anonymous functions in render  
- Use keys properly

---

## 71. What is StrictMode double invoke behavior?

**Answer:**  
Used to detect side effects in dev, rendering components twice intentionally.

---

## 72. What are Controlled Components best practices?

**Answer:**  
Always sync state with input value and handle onChange properly.

---

## 73. What is difference between SPA and MPA?

| SPA | MPA |
|-----|-----|
| Loads one HTML file | Reloads pages |
| Fast navigation | Slower |
| Uses client-side routing | Uses server routing |

---

## 74. What is hydration warning?

**Answer:**  
Occurs when server-rendered HTML differs from client-rendered output.

---

## 75. What are stale closures?

**Answer:**  
When functions capture outdated state values — solved using dependencies in `useEffect`.

---

## 76. What are controlled side effects?

**Answer:**  
Side effects triggered by specific state changes via dependency arrays.

---

## 77. What is strict equality rendering?

**Answer:**  
React shallowly compares old vs new props/state to decide re-render.

---

## 78. What are React fibers and lanes?

**Answer:**  
Fibers are work units; lanes group priorities for better scheduling.

---

## 79. What is concurrent rendering?

**Answer:**  
React splits rendering into chunks so UI remains responsive during heavy updates.

---

## 80. What is suspense for data fetching?

**Answer:**  
Future feature allowing components to “wait” for data before rendering UI.
