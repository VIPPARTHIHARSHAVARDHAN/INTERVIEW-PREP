# React Basics and Important Concepts

> Placement-focused React notes covering the important fundamentals and interview concepts required for fresher technical interviews, especially when React is used in projects.

---

# 1. What is React?

React is a **JavaScript library for building user interfaces**, especially component-based web applications.

It was developed by Meta.

React applications are built using reusable components.

### Interview Answer

> "React is a JavaScript library used to build user interfaces using reusable, component-based architecture. It helps developers efficiently build dynamic web applications."

---

# 2. Why is React Used?

React is commonly used because it provides:

- Reusable components
- Component-based architecture
- Efficient UI updates
- Declarative programming
- State management
- Large ecosystem
- Good support for building dynamic applications

---

# 3. What is a Component?

A component is an independent, reusable piece of UI.

Example:

```jsx
function Welcome() {
    return <h1>Hello World</h1>;
}
```

The component can be reused wherever needed.

A React application is generally composed of many components.

```text
App
├── Navbar
├── Sidebar
├── ProductList
│   └── ProductCard
└── Footer
```

---

# 4. What is a Functional Component?

A functional component is a JavaScript function that returns JSX.

```jsx
function Welcome() {
    return <h1>Welcome</h1>;
}
```

Modern React primarily uses functional components with Hooks.

---

# 5. What is JSX?

JSX stands for **JavaScript XML**.

It allows HTML-like syntax to be written inside JavaScript.

Example:

```jsx
const element = <h1>Hello World</h1>;
```

JSX is transformed into JavaScript by the build tooling.

### Important

JSX is **not HTML**. It is syntax that gets transformed into JavaScript.

---

# 6. JSX Example

```jsx
function App() {
    const name = "Harsha";

    return (
        <div>
            <h1>Hello {name}</h1>
        </div>
    );
}
```

JavaScript expressions can be embedded inside JSX using:

```text
{ }
```

---

# 7. JSX Rules

Some important JSX rules:

### Use `className`

```jsx
<div className="container">
    Hello
</div>
```

Instead of:

```jsx
<div class="container">
```

### Close elements

```jsx
<img src="image.jpg" alt="Example" />
```

### Return one enclosing structure

```jsx
return (
    <div>
        <h1>Hello</h1>
        <p>Welcome</p>
    </div>
);
```

A Fragment can also be used:

```jsx
return (
    <>
        <h1>Hello</h1>
        <p>Welcome</p>
    </>
);
```

---

# 8. What are Props?

Props are values passed from a parent component to a child component.

Example:

```jsx
function User({ name }) {
    return <h2>Hello {name}</h2>;
}

function App() {
    return <User name="Harsha" />;
}
```

Here:

```text
App
 ↓
User
 ↓
name prop
```

### Interview Answer

> "Props are inputs passed from a parent component to a child component. They are used to pass data and configuration between components."

---

# 9. Are Props Mutable?

Props should be treated as **read-only** by the receiving component.

A child component should not directly modify the props it receives.

If the value needs to change, the parent should generally manage the state and pass the updated value down.

---

# 10. What is State?

State is data managed by a component that can change over time.

Example:

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            {count}
        </button>
    );
}
```

When state changes, React can re-render the component.

---

# 11. Props vs State

| Props | State |
|---|---|
| Passed from parent | Managed by component |
| Read-only to receiving component | Updated using state setters |
| Used to pass data | Used to manage changing data |
| Controlled by parent | Usually controlled by component |

### Simple Example

```text
Props
Parent → Child

State
Component → manages its own changing data
```

---

# 12. What is `useState()`?

`useState()` is a React Hook used to add state to a functional component.

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            {count}
        </button>
    );
}
```

It returns:

```text
Current state
State update function
```

---

# 13. Why Should We Not Directly Modify State?

Incorrect:

```jsx
count = count + 1;
```

Instead:

```jsx
setCount(count + 1);
```

React needs the state update mechanism to know that the component's state has changed and should be rendered again.

---

# 14. Functional State Update

When the next state depends on the previous state, use the updater form.

```jsx
setCount(prevCount => prevCount + 1);
```

This is particularly useful when multiple updates may be queued.

Example:

```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

---

# 15. What is `useEffect()`?

`useEffect()` is a React Hook used to synchronize a component with external systems or perform side-effect logic.

Common examples include:

```text
Fetching data
Subscriptions
Timers
Event listeners
Synchronizing with browser APIs
```

Example:

```jsx
import { useEffect } from "react";

useEffect(() => {
    console.log("Component rendered");
}, []);
```

---

# 16. `useEffect()` Dependency Array

The dependency array controls when an effect is re-run.

### Empty dependency array

```jsx
useEffect(() => {
    console.log("Effect");
}, []);
```

The effect runs after the component is initially committed, and does not re-run due to ordinary prop/state changes.

### Dependency

```jsx
useEffect(() => {
    console.log(count);
}, [count]);
```

The effect re-runs when `count` changes.

### No dependency array

```jsx
useEffect(() => {
    console.log("Effect");
});
```

The effect runs after every completed render.

---

# 17. Cleanup Function in `useEffect()`

An effect can return a cleanup function.

```jsx
useEffect(() => {
    const timer = setInterval(() => {
        console.log("Running");
    }, 1000);

    return () => {
        clearInterval(timer);
    };
}, []);
```

Cleanup is useful for things such as:

```text
Removing event listeners
Clearing timers
Unsubscribing from subscriptions
Canceling/ignoring stale asynchronous work
```

---

# 18. What is `useRef()`?

`useRef()` creates a mutable ref object whose `.current` value persists between renders without causing a re-render when changed.

Example:

```jsx
import { useRef } from "react";

function App() {
    const inputRef = useRef(null);

    return (
        <>
            <input ref={inputRef} />
            <button onClick={() => inputRef.current.focus()}>
                Focus
            </button>
        </>
    );
}
```

Common uses:

```text
Accessing DOM elements
Storing mutable values
Keeping a value between renders
```

---

# 19. `useState()` vs `useRef()`

| `useState()` | `useRef()` |
|---|---|
| Stores state | Stores a mutable reference |
| Updating state causes a re-render | Changing `.current` does not cause a re-render |
| Used for UI-related changing data | Often used for DOM references or persistent mutable values |

---

# 20. What is Conditional Rendering?

Conditional rendering means displaying UI based on a condition.

Example:

```jsx
function App({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? <h1>Welcome</h1> : <h1>Please Login</h1>}
        </div>
    );
}
```

---

# 21. Conditional Rendering Using `&&`

```jsx
function App({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn && <h1>Welcome</h1>}
        </div>
    );
}
```

If `isLoggedIn` is truthy, the element is rendered.

---

# 22. What is List Rendering?

React can render lists using JavaScript array methods such as `map()`.

```jsx
const users = ["A", "B", "C"];

function App() {
    return (
        <ul>
            {users.map(user => (
                <li key={user}>{user}</li>
            ))}
        </ul>
    );
}
```

---

# 23. What are Keys in React?

Keys help React identify list items between renders.

Example:

```jsx
users.map(user => (
    <li key={user.id}>
        {user.name}
    </li>
))
```

Keys should generally be:

- Unique among siblings
- Stable
- Associated with the identity of the item

Avoid using array indexes as keys when the list can be reordered, inserted into, or deleted from in ways that would change item positions.

---

# 24. Why are Keys Important?

Keys help React determine which list items:

```text
Changed
Added
Removed
Moved
```

This helps React update the UI correctly and efficiently.

### Interview Answer

> "Keys give list elements a stable identity so React can correctly match items between renders."

---

# 25. What is Event Handling in React?

React uses event handlers to respond to user actions.

Example:

```jsx
function App() {
    const handleClick = () => {
        console.log("Clicked");
    };

    return (
        <button onClick={handleClick}>
            Click Me
        </button>
    );
}
```

---

# 26. React Event vs HTML Event

In React, event handlers are typically written using camelCase.

```jsx
<button onClick={handleClick}>
    Click
</button>
```

Instead of HTML-style:

```html
<button onclick="handleClick()">
```

---

# 27. What are Forms in React?

Forms are commonly controlled using component state.

Example:

```jsx
import { useState } from "react";

function Form() {
    const [name, setName] = useState("");

    return (
        <input
            value={name}
            onChange={e => setName(e.target.value)}
        />
    );
}
```

Here:

```text
Input value
     ↓
React state
     ↓
onChange
     ↓
Updated state
```

---

# 28. What is a Controlled Component?

A controlled form element has its value controlled by React state.

Example:

```jsx
const [name, setName] = useState("");

<input
    value={name}
    onChange={e => setName(e.target.value)}
/>
```

React state is the source of truth for the input value.

---

# 29. What is an Uncontrolled Component?

An uncontrolled component lets the DOM maintain the form value rather than React state.

A ref can be used to access its value.

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

### Interview Priority

For fresher interviews, know the difference between controlled and uncontrolled inputs and understand why controlled inputs are commonly used.

---

# 30. What is Component Composition?

Component composition means building larger components by combining smaller components.

Example:

```jsx
function Card({ children }) {
    return <div className="card">{children}</div>;
}

function App() {
    return (
        <Card>
            <h2>Hello</h2>
            <p>Welcome</p>
        </Card>
    );
}
```

Composition improves reusability.

---

# 31. What is the `children` Prop?

`children` represents content placed between a component's opening and closing tags.

Example:

```jsx
function Box({ children }) {
    return <div>{children}</div>;
}
```

Usage:

```jsx
<Box>
    <h1>Hello</h1>
</Box>
```

The `<h1>` becomes the `children` value.

---

# 32. What is Prop Drilling?

Prop drilling occurs when data is passed through multiple intermediate components that do not directly need the data, simply to reach a deeply nested component.

Example:

```text
App
 ↓
Component A
 ↓
Component B
 ↓
Component C
```

If data is passed through A and B only to reach C, this can be called prop drilling.

Possible solutions include:

```text
Component composition
Context
State management libraries
```

---

# 33. What is Context API?

React Context allows data to be made available to components deeper in the component tree without passing props through every intermediate component.

Example:

```jsx
import { createContext } from "react";

const ThemeContext = createContext("light");
```

A provider can supply a value:

```jsx
<ThemeContext.Provider value="dark">
    <App />
</ThemeContext.Provider>
```

Components can consume the context using an appropriate API such as `useContext()`.

---

# 34. What is `useContext()`?

`useContext()` reads the current value of a React Context.

Example:

```jsx
const theme = useContext(ThemeContext);

console.log(theme);
```

It is useful for values that need to be shared across many components.

Common examples:

```text
Theme
Authentication information
Language
Shared configuration
```

---

# 35. What is the Virtual DOM?

The Virtual DOM is a conceptual in-memory representation used by React to determine what UI changes are needed.

When state or props change, React calculates the necessary updates and commits changes to the actual DOM.

### Interview Answer

> "React uses an in-memory representation of the UI to determine the necessary DOM updates. It compares the new and previous rendered trees and commits the required changes."

---

# 36. What is Reconciliation?

Reconciliation is the process React uses to determine how the rendered UI should be updated when the component output changes.

React compares the previous and next element trees and determines the necessary updates.

Keys are especially important when reconciling lists.

---

# 37. What Causes a React Component to Re-render?

A component can re-render when relevant:

```text
State changes
Props change
Context value changes
Its parent re-renders
```

A re-render means React runs the component function again to determine the next UI representation.

A re-render does not necessarily mean every DOM node is recreated.

---

# 38. What is React Strict Mode?

`StrictMode` is a development-only feature that helps identify potential problems in a React application.

Example:

```jsx
import { StrictMode } from "react";

<StrictMode>
    <App />
</StrictMode>
```

It can intentionally invoke certain functions or lifecycle-related behavior more than once in development to help detect unsafe patterns.

This does not mean production rendering behaves identically.

---

# 39. What are Hooks?

Hooks are functions that allow functional components to use React features such as state and context.

Common Hooks:

```text
useState
useEffect
useRef
useContext
useMemo
useCallback
```

For fresher interviews, the most important are:

```text
useState
useEffect
useRef
useContext
```

---

# 40. Rules of Hooks

Important rules:

### 1. Call Hooks at the top level

Don't call Hooks inside:

```text
Loops
Conditions
Nested functions
```

### 2. Call Hooks from React functions

Hooks should generally be called from:

```text
React function components
Custom Hooks
```

Example:

```jsx
function App() {
    const [count, setCount] = useState(0);

    return <h1>{count}</h1>;
}
```

---

# 41. What is a Custom Hook?

A custom Hook is a reusable function that uses React Hooks to share stateful logic.

It generally starts with:

```text
use
```

Example:

```jsx
function useCounter() {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount(prev => prev + 1);
    };

    return { count, increment };
}
```

Then:

```jsx
function App() {
    const { count, increment } = useCounter();

    return (
        <button onClick={increment}>
            {count}
        </button>
    );
}
```

Custom Hooks help reuse **logic**, not UI.

---

# 42. What is React Router?

React Router is commonly used to handle client-side routing in React applications.

It allows different UI components to be rendered for different URL paths.

Example:

```jsx
<Route path="/about" element={<About />} />
```

Typical routes:

```text
/
 /about
 /products
 /contact
```

---

# 43. What is Client-Side Routing?

Client-side routing allows a web application to change the displayed UI based on the URL without requiring a full page reload for every route transition.

This is commonly used in single-page applications.

---

# 44. How do React Applications Call APIs?

React applications can use JavaScript APIs such as `fetch()` or libraries such as Axios.

Example:

```jsx
useEffect(() => {
    async function loadUsers() {
        const response = await fetch("/api/users");
        const data = await response.json();

        setUsers(data);
    }

    loadUsers();
}, []);
```

Typical flow:

```text
React Component
      ↓
API Request
      ↓
Backend
      ↓
Response
      ↓
Update State
      ↓
UI Re-renders
```

---

# 45. How Does React Communicate With a Backend?

React acts as the frontend.

It sends HTTP requests to a backend API.

Example:

```text
React
  ↓
GET /api/users
  ↓
Backend
  ↓
Database
  ↓
JSON Response
  ↓
React
  ↓
Display Data
```

Common HTTP methods:

```text
GET
POST
PUT
PATCH
DELETE
```

---

# 46. What is Loading and Error State?

When fetching data, a UI commonly maintains states such as:

```text
Loading
Success
Error
```

Example:

```jsx
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
const [users, setUsers] = useState([]);
```

This allows the UI to show appropriate feedback.

---

# 47. Basic API Example in React

```jsx
import { useEffect, useState } from "react";

function Users() {
    const [users, setUsers] = useState([]);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        async function fetchUsers() {
            try {
                const response = await fetch("/api/users");

                if (!response.ok) {
                    throw new Error("Failed to fetch users");
                }

                const data = await response.json();
                setUsers(data);
            } catch (err) {
                setError(err.message);
            } finally {
                setLoading(false);
            }
        }

        fetchUsers();
    }, []);

    if (loading) {
        return <p>Loading...</p>;
    }

    if (error) {
        return <p>{error}</p>;
    }

    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>{user.name}</li>
            ))}
        </ul>
    );
}

export default Users;
```

---

# 48. What is `useMemo()`?

`useMemo()` memoizes the result of a calculation between renders until its dependencies change.

Example:

```jsx
const expensiveValue = useMemo(() => {
    return calculateValue(data);
}, [data]);
```

It can help avoid unnecessary expensive recalculations.

### Important

Do not use `useMemo()` everywhere. It is a performance optimization and should be used when there is a meaningful reason.

---

# 49. What is `useCallback()`?

`useCallback()` memoizes a function reference between renders until its dependencies change.

Example:

```jsx
const handleClick = useCallback(() => {
    console.log("Clicked");
}, []);
```

It can be useful when function identity matters, such as when passing callbacks to memoized child components.

---

# 50. `useMemo()` vs `useCallback()`

```text
useMemo()
→ Memoizes a calculated value.

useCallback()
→ Memoizes a function reference.
```

Example:

```jsx
const value = useMemo(() => calculate(), [data]);

const handleClick = useCallback(() => {
    doSomething();
}, []);
```

These are optimization tools, not replacements for correct application design.

---

# 51. What is `React.memo()`?

`React.memo()` can memoize a functional component so React can skip rendering it when its props have not changed according to the memoization comparison.

Example:

```jsx
const User = React.memo(function User({ name }) {
    return <h1>{name}</h1>;
});
```

It can help in specific performance-sensitive situations.

---

# 52. What is Lazy Loading?

Lazy loading means loading code or resources only when needed.

React supports component-level code splitting with mechanisms such as:

```jsx
const Dashboard = lazy(() => import("./Dashboard"));
```

Usually used together with `Suspense`:

```jsx
<Suspense fallback={<p>Loading...</p>}>
    <Dashboard />
</Suspense>
```

This can reduce the initial JavaScript bundle size.

---

# 53. What is Component Lifecycle?

A component goes through stages such as:

```text
Mount
Update
Unmount
```

### Mount

Component is added to the UI.

### Update

Component output may be recalculated because relevant data changed.

### Unmount

Component is removed from the UI.

In modern React, `useEffect()` cleanup is commonly used for cleanup related to effects.

---

# 54. What is Lifting State Up?

When multiple components need to share the same state, the state can be moved to their closest common parent.

Example:

```text
       Parent
       /    \
   Child A  Child B
```

If both children need the same data:

```text
State
 ↓
Parent
 ↙   ↘
A     B
```

This is called **lifting state up**.

---

# 55. What is One-Way Data Flow?

React generally follows one-way data flow.

Data commonly moves:

```text
Parent
  ↓
Child
```

through props.

A child can communicate an event or requested change back to the parent through a callback passed as a prop.

Example:

```jsx
function Parent() {
    const handleMessage = message => {
        console.log(message);
    };

    return <Child onMessage={handleMessage} />;
}
```

---

# 56. What is a Fragment?

A Fragment lets a component return multiple elements without adding an unnecessary DOM element.

```jsx
<>
    <h1>Hello</h1>
    <p>Welcome</p>
</>
```

It is equivalent to using:

```jsx
<React.Fragment>
    <h1>Hello</h1>
    <p>Welcome</p>
</React.Fragment>
```

---

# 57. Why Should We Avoid Unnecessary State?

Not every value needs to be stored in state.

If a value can be calculated from existing props or state, it may be better to derive it.

Instead of:

```jsx
const [fullName, setFullName] = useState("");

```

when it can be derived:

```jsx
const fullName = `${firstName} ${lastName}`;
```

Avoiding unnecessary state can make components simpler and prevent synchronization problems.

---

# 58. What is Derived State?

Derived state is a value that can be calculated from existing props or state.

Example:

```jsx
const total = price * quantity;
```

There may be no need to maintain `total` separately in state if it can always be calculated from `price` and `quantity`.

---

# 59. Common React Project Structure

A simple React project may contain:

```text
src/
├── components/
├── pages/
├── hooks/
├── services/
├── assets/
├── App.jsx
└── main.jsx
```

Possible purpose:

```text
components/
→ Reusable UI components

pages/
→ Page-level components

hooks/
→ Custom Hooks

services/
→ API-related logic

assets/
→ Images, styles, etc.

App.jsx
→ Main application component

main.jsx
→ Application entry point
```

The exact structure depends on the project.

---

# 60. How to Explain React in Your Project

If the interviewer asks:

> "Why did you use React in your project?"

A good answer:

> "I used React because the project contains a dynamic user interface with multiple reusable sections. React's component-based architecture allowed me to break the UI into reusable components, manage changing data with state, handle user interactions, and update the UI when the data changed."

---

# 61. How to Explain Components Used in Your Project

Be ready to explain:

```text
What components did you create?
Why did you divide the UI that way?
Which components were reusable?
Where did you use props?
Where did you use state?
Where did you make API calls?
How did you handle loading and errors?
How did you handle forms?
How did you implement routing?
```

Do not memorize a generic answer.

Explain the actual components you built.

---

# 62. Important React Interview Questions

## Q1. What is React?

**Answer:** React is a JavaScript library for building user interfaces using reusable components.

## Q2. What is a component?

**Answer:** A component is a reusable piece of UI and its associated logic.

## Q3. What is JSX?

**Answer:** JSX is syntax that allows HTML-like UI markup to be written within JavaScript. It is transformed into JavaScript by tooling.

## Q4. What are props?

**Answer:** Props are values passed from a parent component to a child component.

## Q5. What is state?

**Answer:** State is data managed by a component that can change over time and trigger an update to the rendered UI.

## Q6. Props vs state?

**Answer:** Props are passed into a component, while state is managed by the component or a state owner.

## Q7. What is `useState()`?

**Answer:** `useState()` is a Hook that lets a functional component manage state.

## Q8. What is `useEffect()`?

**Answer:** `useEffect()` is used to synchronize a component with external systems and perform side-effect logic.

## Q9. What is `useRef()`?

**Answer:** `useRef()` stores a mutable reference whose value persists between renders without causing a re-render when `.current` changes.

## Q10. What are keys?

**Answer:** Keys provide stable identity for elements in a list so React can correctly reconcile list changes.

## Q11. What is the Virtual DOM?

**Answer:** It is an in-memory representation of UI used by React to determine the necessary DOM updates.

## Q12. What is reconciliation?

**Answer:** Reconciliation is the process React uses to determine the changes needed when the rendered element tree changes.

## Q13. What is prop drilling?

**Answer:** Prop drilling is passing data through intermediate components that do not need the data themselves just to reach a deeper component.

## Q14. How can prop drilling be reduced?

**Answer:** Depending on the situation, component composition, Context, or a state management solution can be used.

## Q15. What is Context?

**Answer:** Context allows values to be shared with components deeper in the tree without explicitly passing props through every intermediate component.

## Q16. What is conditional rendering?

**Answer:** Conditional rendering means displaying different UI depending on a condition.

## Q17. What is a controlled component?

**Answer:** A controlled form element gets its value from React state and updates that state through event handlers.

## Q18. What is lifting state up?

**Answer:** Lifting state up means moving shared state to the closest common parent of the components that need it.

## Q19. What is a custom Hook?

**Answer:** A custom Hook is a reusable function that uses React Hooks to share stateful logic between components.

## Q20. What is React Router?

**Answer:** React Router is commonly used to implement client-side routing in React applications.

---

# 63. Most Important React Concepts for Placements

Prioritize these first:

```text
★★★★★ React basics
★★★★★ Components
★★★★★ JSX
★★★★★ Props
★★★★★ State
★★★★★ Props vs State
★★★★★ useState
★★★★★ useEffect
★★★★★ Event handling
★★★★★ Conditional rendering
★★★★★ Lists and keys
★★★★★ Forms
★★★★★ API calls
★★★★★ Component communication
★★★★★ Lifting state up
★★★★★ Context
★★★★★ useRef
```

Then learn:

```text
★★★★ Custom Hooks
★★★★ useMemo
★★★★ useCallback
★★★★ React.memo
★★★★ React Router
★★★★ Lazy loading
★★★★ Reconciliation
★★★★ Virtual DOM
```

Lower priority for basic fresher interviews:

```text
★★ Advanced rendering internals
★★ Complex state management internals
★★ Advanced performance optimization
★★ Deep React framework internals
```

---

# 64. React Interview Preparation Checklist

Before attending an interview, make sure you can explain:

```text
[ ] What is React?
[ ] Why React?
[ ] What is a component?
[ ] What is JSX?
[ ] What are props?
[ ] What is state?
[ ] Props vs state
[ ] useState
[ ] useEffect
[ ] useRef
[ ] useContext
[ ] Conditional rendering
[ ] List rendering
[ ] Keys
[ ] Event handling
[ ] Controlled components
[ ] Uncontrolled components
[ ] Prop drilling
[ ] Lifting state up
[ ] Component composition
[ ] children
[ ] Context API
[ ] API calls
[ ] Loading/error handling
[ ] React Router basics
[ ] Custom Hooks
[ ] Virtual DOM
[ ] Reconciliation
[ ] useMemo
[ ] useCallback
[ ] React.memo
```

---

# 65. Most Important: Know Your Own React Project

If React appears on your resume, the interviewer can ask project-specific questions.

You should be able to explain:

```text
1. Why did you choose React?
2. What components did you create?
3. How did you structure the project?
4. Where did you use props?
5. Where did you use state?
6. Which Hooks did you use?
7. Why did you use useEffect?
8. How did you call your backend APIs?
9. How did you handle loading?
10. How did you handle API errors?
11. How did you implement forms?
12. How did you validate input?
13. How did you implement routing?
14. How did components communicate?
15. Where did you use reusable components?
16. What was the most difficult part?
17. What problem did React solve in your project?
18. What would you improve if you rebuilt it?
```

### Final Placement Focus

You do **not** need to become an advanced React developer just for a fresher technical interview.

Your target should be:

```text
JavaScript Fundamentals
        +
React Fundamentals
        +
React Interview Questions
        +
Your Actual Project
```

If you can confidently explain the concepts above **and connect them to your own project**, you will be well prepared for most basic React questions you are likely to encounter in a fresher interview.