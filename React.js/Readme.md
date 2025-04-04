## **4. React.js**

---

### **Beginner:**

**1. What is React, and why is it used?**  
React is a JavaScript library developed by Meta (Facebook) for building fast and interactive user interfaces. It is used for:
- Component-based architecture
- Efficient DOM updates via Virtual DOM
- Fast rendering and great performance
- Reusable components

---

**2. What are components in React?**  
Components are independent, reusable pieces of UI. They can be functional or class-based and manage their own state and logic.

---

**3. Explain the difference between functional and class components.**  
- **Functional Components:** Simple JavaScript functions. Use Hooks for state and side effects.  
- **Class Components:** ES6 classes that extend `React.Component` with lifecycle methods and `this.state`.

---

**4. What is JSX, and how does it differ from regular JavaScript?**  
JSX is a syntax extension that allows writing HTML inside JavaScript:

```jsx
const element = <h1>Hello, World!</h1>;
```

It’s transpiled to `React.createElement()` and allows for more readable UI code.

---

**5. How do you pass data between React components?**  
- **Parent to child:** via **props**  
- **Child to parent:** via **callback functions passed as props**  
- **Across many components:** via **Context API** or state management libraries

---

**6. What are React props, and how do they work?**  
Props (short for "properties") are read-only values passed from a parent component to a child component.

```jsx
<Greeting name="John" />
```

---

**7. What is state in React? How do you use `useState()`?**  
State is used to store local data within a component.  
`useState()` is a Hook used to declare state in functional components.

```jsx
const [count, setCount] = useState(0);
```

---

**8. What is the virtual DOM, and how does it improve performance?**  
The Virtual DOM is a lightweight copy of the real DOM. React uses it to:
- Batch updates
- Compare changes using **diffing**
- Apply minimal DOM manipulations

---

**9. What are controlled and uncontrolled components?**  
- **Controlled Component:** Form element controlled by React state  
- **Uncontrolled Component:** Uses refs to access form values directly from the DOM

---

**10. What are React fragments, and why are they useful?**  
Fragments allow grouping elements without adding extra nodes to the DOM.

```jsx
<>
  <h1>Title</h1>
  <p>Text</p>
</>
```

---

### **Mid-Level:**

**1. What is React’s reconciliation process?**  
Reconciliation is the process React uses to compare the new Virtual DOM with the old one and update only what's changed using the diffing algorithm.

---

**2. How does React’s `useEffect()` work? Provide examples.**  
`useEffect()` lets you run side effects like fetching data, subscriptions, etc.

```jsx
useEffect(() => {
  fetchData();
}, []); // empty array means run once on mount
```

---

**3. What is context API in React, and how does it work?**  
It provides a way to pass data through the component tree without passing props manually at every level.

```jsx
const MyContext = React.createContext();

<MyContext.Provider value={data}>
  <Child />
</MyContext.Provider>
```

---

**4. Explain React hooks: `useState`, `useEffect`, `useContext`, and `useReducer`.**
- `useState`: For local state  
- `useEffect`: For side effects  
- `useContext`: Consume context values  
- `useReducer`: State management with a reducer function, like Redux

---

**5. What are higher-order components (HOCs)?**  
A HOC is a function that takes a component and returns a new component with added functionality.

```jsx
const withLogger = (Component) => (props) => {
  console.log('Rendering');
  return <Component {...props} />;
};
```

---

**6. How do you optimize React performance?**  
- Use `React.memo()` to prevent unnecessary re-renders  
- Use `useCallback()` and `useMemo()`  
- Lazy load components  
- Use efficient data structures  
- Avoid inline functions and props chaining

---

**7. What is the difference between React Router and Next.js routing?**  
- **React Router:** Client-side routing, manual setup  
- **Next.js routing:** File-based, automatic SSR, built-in API routes

---

**8. What is the `useMemo()` hook, and when should you use it?**  
It memoizes expensive calculations to prevent recalculation on every render.

```jsx
const result = useMemo(() => expensiveFunction(a, b), [a, b]);
```

---

**9. What is the `useCallback()` hook, and how does it work?**  
It memoizes functions so they don’t change reference unless dependencies change.

```jsx
const handleClick = useCallback(() => {
  doSomething();
}, []);
```

---

**10. How do you handle forms and form validation in React?**  
- Controlled inputs with `useState()`  
- Form validation with libraries like `Formik`, `Yup`, or `React Hook Form`  
- Manual validation using custom logic in `onChange` or `onSubmit`

---

### **Senior-Level:**

**1. How does React’s rendering process work?**  
- Renders Virtual DOM  
- Diffs previous and new Virtual DOM  
- Uses Fiber architecture to schedule and batch updates  
- Commits the minimal updates to the real DOM

---

**2. What are React Suspense and React Lazy?**  
They allow lazy loading components:

```jsx
const LazyComp = React.lazy(() => import('./LazyComp'));

<Suspense fallback={<Loading />}>
  <LazyComp />
</Suspense>
```

---

**3. Explain the benefits of server-side rendering (SSR) in React.**  
- Faster first load and SEO friendly  
- Pre-renders HTML on server  
- Better for static content  
Next.js provides built-in SSR with `getServerSideProps`.

---

**4. How does React Fiber work?**  
Fiber is a new reconciliation engine that enables incremental rendering, improves scheduling, and enhances responsiveness by breaking tasks into units of work.

---

**5. How would you handle state management in a large React application?**  
- Use Context API for global state  
- Use `useReducer()` for complex state  
- Integrate libraries like Redux, Zustand, Recoil, or Jotai  
- Use code splitting for performance

---

**6. What is React concurrent mode, and why is it important?**  
A feature to make rendering interruptible. It allows React to:
- Pause rendering  
- Prioritize urgent updates  
- Avoid blocking UI  
Still experimental, used internally with `startTransition()`.

---

**7. How would you design a reusable React component library?**  
- Use TypeScript for typings  
- Keep components isolated  
- Write Storybook docs  
- Use props and slots  
- Publish with tools like Rollup/Vite  
- Version and test with CI/CD

---

**8. What is hydration in React, and how does it work?**  
Hydration is when React attaches event handlers to existing SSR-rendered HTML. It reconciles the static HTML with the Virtual DOM without re-rendering everything.

---

**9. How does React handle accessibility (a11y)?**  
- Semantic HTML (`<button>`, `<label>`)  
- ARIA attributes  
- Keyboard navigation support  
- Focus management using `useRef()`  
- Tools like `eslint-plugin-jsx-a11y`

---

**10. How do you implement a micro-frontend architecture in React?**  
- Split app into independent React apps/modules  
- Use module federation (Webpack 5)  
- Share components via npm or monorepos  
- Communicate using custom events, Redux store, or pub/sub  
- Deploy each part independently
