# JavaScript + React Important Interview Questions

> Placement-focused interview questions and answers for **JavaScript and React**. These questions cover the fundamentals, common practical questions, output-based concepts, and project-based questions most useful for fresher technical interviews.

---

# Part 1: JavaScript Interview Questions

## 1. What is JavaScript?

### Answer

JavaScript is a dynamically typed programming language mainly used to build interactive and dynamic web applications.

It is commonly used with HTML and CSS on the frontend and can also be used on the backend with runtimes such as Node.js.

---

## 2. What is the difference between `var`, `let`, and `const`?

### Answer

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function | Block | Block |
| Redeclaration | Allowed | Not allowed in same scope | Not allowed in same scope |
| Reassignment | Allowed | Allowed | Not allowed |
| Modern usage | Generally avoided | Common | Common |

Example:

```javascript
let age = 22;
age = 23;

const name = "Harsha";
// name = "John"; // Error
```

---

## 3. What is the difference between `==` and `===`?

### Answer

`==` performs comparison with type coercion.

`===` performs strict equality comparison without coercing the operands to match types.

```javascript
5 == "5";   // true
5 === "5";  // false
```

### Interview Answer

> "I generally prefer `===` because it avoids unexpected type coercion."

---

## 4. What is hoisting?

### Answer

Hoisting describes how JavaScript handles declarations during execution setup.

For example:

```javascript
console.log(x);

var x = 10;
```

The `var` declaration is available before its assignment, so the output is:

```text
undefined
```

For `let` and `const`, accessing the variable before initialization causes a `ReferenceError` because of the Temporal Dead Zone.

---

## 5. What is the Temporal Dead Zone?

### Answer

The Temporal Dead Zone is the period between entering a scope and the point where a `let`, `const`, or `class` declaration is initialized.

Example:

```javascript
console.log(x);

let x = 10;
```

This results in:

```text
ReferenceError
```

---

## 6. What is scope in JavaScript?

### Answer

Scope determines where a variable can be accessed.

Important types include:

```text
Global Scope
Function Scope
Block Scope
```

`let` and `const` are block-scoped.

`var` is function-scoped.

---

## 7. What is a closure?

### Answer

A closure is created when a function retains access to variables from its surrounding lexical scope even after the outer function has finished executing.

Example:

```javascript
function outer() {
    let count = 0;

    return function inner() {
        count++;
        return count;
    };
}

const counter = outer();

console.log(counter());
console.log(counter());
```

Output:

```text
1
2
```

### Interview Answer

> "A closure allows an inner function to remember and access variables from its surrounding lexical scope even after the outer function has completed."

---

## 8. What is an arrow function?

### Answer

An arrow function is a shorter syntax for writing functions.

```javascript
const add = (a, b) => a + b;
```

Arrow functions are commonly used in React.

One important difference is that arrow functions do not have their own `this`; they capture `this` from the surrounding lexical scope.

---

## 9. What is a callback function?

### Answer

A callback is a function passed to another function to be invoked later or as part of an operation.

Example:

```javascript
function processUser(name, callback) {
    console.log(name);
    callback();
}

processUser("Harsha", () => {
    console.log("Done");
});
```

Callbacks are commonly used in:

```text
Array methods
Event handling
Asynchronous operations
```

---

## 10. What is a higher-order function?

### Answer

A higher-order function is a function that takes another function as an argument or returns a function.

Example:

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

const add = (x, y) => x + y;

console.log(calculate(5, 3, add));
```

Output:

```text
8
```

---

## 11. What is the difference between `map()`, `filter()`, and `reduce()`?

### Answer

```text
map()
→ Transforms every element.

filter()
→ Selects elements that satisfy a condition.

reduce()
→ Combines elements into an accumulated result.
```

Example:

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(x => x * 2);

const even = numbers.filter(x => x % 2 === 0);

const sum = numbers.reduce((total, x) => total + x, 0);
```

Results:

```text
doubled → [2, 4, 6, 8]
even    → [2, 4]
sum     → 10
```

---

## 12. What is the difference between `map()` and `forEach()`?

### Answer

`map()` returns a new array.

`forEach()` is generally used to perform an action for each element and returns `undefined`.

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(x => x * 2);

console.log(result);
```

Output:

```text
[2, 4, 6]
```

---

## 13. What is the difference between `filter()` and `find()`?

### Answer

`filter()` returns an array containing all matching elements.

`find()` returns the first matching element.

```javascript
const numbers = [1, 2, 3, 4];

console.log(numbers.filter(x => x > 2));
console.log(numbers.find(x => x > 2));
```

Output:

```text
[3, 4]
3
```

---

## 14. What is destructuring?

### Answer

Destructuring allows values to be extracted from arrays or objects.

### Object

```javascript
const user = {
    name: "Harsha",
    age: 22
};

const { name, age } = user;
```

### Array

```javascript
const numbers = [10, 20];

const [a, b] = numbers;
```

Destructuring is frequently used in React components.

---

## 15. What is the spread operator?

### Answer

The spread operator `...` expands elements or object properties.

```javascript
const a = [1, 2];
const b = [3, 4];

const result = [...a, ...b];
```

Result:

```text
[1, 2, 3, 4]
```

It is also commonly used when creating updated objects or arrays in React.

---

## 16. What is the rest parameter?

### Answer

The rest parameter collects remaining arguments into an array.

```javascript
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(1, 2, 3));
```

Output:

```text
6
```

### Spread vs Rest

```text
Spread → Expands values.
Rest   → Collects values.
```

---

## 17. What is the difference between `null` and `undefined`?

### Answer

```text
null
→ Usually represents an intentional absence of a value.

undefined
→ Usually indicates that a value has not been assigned.
```

Example:

```javascript
let a;
let b = null;
```

Here:

```text
a → undefined
b → null
```

---

## 18. What are primitive data types in JavaScript?

### Answer

The primitive types are:

```text
string
number
bigint
boolean
undefined
null
symbol
```

Objects are non-primitive values.

---

## 19. What are truthy and falsy values?

### Answer

Falsy values include:

```text
false
0
-0
0n
""
null
undefined
NaN
```

Most other values are truthy.

Example:

```javascript
if ("Hello") {
    console.log("Truthy");
}
```

---

## 20. What is `NaN`?

### Answer

`NaN` means **Not-a-Number**.

It represents an invalid numeric result.

```javascript
const value = Number("hello");

console.log(value);
```

Output:

```text
NaN
```

Check it using:

```javascript
Number.isNaN(value);
```

---

## 21. What is `this` in JavaScript?

### Answer

`this` refers to a value determined by how a function is called.

Example:

```javascript
const user = {
    name: "Harsha",

    greet() {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
Harsha
```

Arrow functions handle `this` differently because they capture it lexically.

---

## 22. What is a Promise?

### Answer

A Promise represents the eventual completion or failure of an asynchronous operation.

It has three states:

```text
Pending
Fulfilled
Rejected
```

Example:

```javascript
const promise = new Promise((resolve, reject) => {
    resolve("Success");
});

promise.then(result => {
    console.log(result);
});
```

---

## 23. What is `async/await`?

### Answer

`async/await` provides a cleaner syntax for working with Promises.

Example:

```javascript
async function getData() {
    const response = await fetch("/api/users");
    const data = await response.json();

    console.log(data);
}
```

An `async` function always returns a Promise.

---

## 24. What is the difference between synchronous and asynchronous JavaScript?

### Answer

### Synchronous

Operations execute sequentially.

```javascript
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

### Asynchronous

Some operations complete later while other JavaScript execution continues.

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

console.log("C");
```

Output:

```text
A
C
B
```

---

## 25. What is the Event Loop?

### Answer

The event loop coordinates JavaScript execution with asynchronous callbacks and queued work.

A simplified model contains:

```text
Call Stack
    ↓
Runtime APIs
    ↓
Queues
    ↓
Event Loop
    ↓
Call Stack
```

This allows JavaScript to handle asynchronous operations without blocking normal execution.

---

## 26. What is the DOM?

### Answer

DOM stands for **Document Object Model**.

It represents an HTML document as a tree of objects that JavaScript can interact with.

JavaScript can use the DOM to:

```text
Find elements
Change content
Change attributes
Handle events
Create/remove elements
```

---

## 27. What is JSON?

### Answer

JSON stands for **JavaScript Object Notation**.

It is a text-based format commonly used to exchange structured data between frontend and backend applications.

Example:

```json
{
    "name": "Harsha",
    "age": 22
}
```

---

## 28. What is the difference between `JSON.parse()` and `JSON.stringify()`?

### Answer

```text
JSON.parse()
→ JSON string → JavaScript value

JSON.stringify()
→ JavaScript value → JSON string
```

Example:

```javascript
const text = '{"name":"Harsha"}';

const user = JSON.parse(text);

const json = JSON.stringify(user);
```

---

## 29. What is `fetch()`?

### Answer

`fetch()` is a browser API used to make HTTP requests.

It returns a Promise.

Example:

```javascript
fetch("/api/users")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

---

## 30. What is immutability?

### Answer

Immutability means avoiding direct modification of existing data and instead creating a new value when an update is required.

Example:

```javascript
const user = {
    name: "Harsha",
    age: 22
};

const updatedUser = {
    ...user,
    age: 23
};
```

Immutability is especially important when working with React state.

---

# Part 2: React Interview Questions

## 31. What is React?

### Answer

React is a JavaScript library for building user interfaces using reusable components.

It is especially useful for dynamic and component-based web applications.

---

## 32. Why did you use React in your project?

### Answer

> "I used React because my project has a dynamic user interface with multiple reusable sections. React's component-based architecture helped me divide the UI into reusable components, manage changing data using state, handle user interactions, and update the UI when data changed."

Always modify this answer according to your actual project.

---

## 33. What is a component in React?

### Answer

A component is a reusable piece of UI and its associated logic.

Example:

```jsx
function Welcome() {
    return <h1>Welcome</h1>;
}
```

Large applications can be divided into many smaller components.

---

## 34. What is a functional component?

### Answer

A functional component is a JavaScript function that returns JSX.

```jsx
function App() {
    return <h1>Hello</h1>;
}
```

Modern React applications primarily use functional components with Hooks.

---

## 35. What is JSX?

### Answer

JSX is syntax that allows HTML-like markup to be written within JavaScript.

Example:

```jsx
const element = <h1>Hello World</h1>;
```

JSX is transformed into JavaScript by the application's build tooling.

---

## 36. What are props in React?

### Answer

Props are values passed from a parent component to a child component.

Example:

```jsx
function User({ name }) {
    return <h1>Hello {name}</h1>;
}

function App() {
    return <User name="Harsha" />;
}
```

Here `name` is a prop.

---

## 37. Can a child component modify props?

### Answer

A child component should treat props as read-only.

If a value needs to change, the component that owns the state should update it and pass the new value down.

---

## 38. What is state in React?

### Answer

State is data managed by a component that can change over time.

When relevant state changes, React can render the component again with the new state.

Example:

```jsx
const [count, setCount] = useState(0);
```

---

## 39. What is the difference between props and state?

### Answer

| Props | State |
|---|---|
| Passed into a component | Managed by a state owner |
| Read-only to receiving component | Updated through state update mechanisms |
| Used to pass data/configuration | Used for changing data |
| Parent commonly controls it | Component or another owner manages it |

---

## 40. What is `useState()`?

### Answer

`useState()` is a Hook used to add state to a functional component.

```jsx
const [count, setCount] = useState(0);
```

It returns:

```text
Current state
State setter
```

---

## 41. Why should we not directly modify React state?

### Answer

Instead of directly modifying state:

```jsx
count = count + 1;
```

use the state setter:

```jsx
setCount(count + 1);
```

The setter tells React that the state has changed and allows React to schedule the necessary update.

---

## 42. What is a functional state update?

### Answer

When the next state depends on the previous state, use the updater function.

```jsx
setCount(prevCount => prevCount + 1);
```

This ensures the update is calculated from the latest state value available to the update.

---

## 43. What is `useEffect()`?

### Answer

`useEffect()` is a React Hook used to synchronize a component with external systems and perform side-effect logic.

Common examples:

```text
API requests
Timers
Event listeners
Subscriptions
Browser APIs
```

Example:

```jsx
useEffect(() => {
    console.log("Effect executed");
}, []);
```

---

## 44. What is the dependency array in `useEffect()`?

### Answer

The dependency array determines when an effect should be re-run.

Example:

```jsx
useEffect(() => {
    console.log("Runs when count changes");
}, [count]);
```

With an empty dependency array:

```jsx
useEffect(() => {
    console.log("Effect");
}, []);
```

The effect runs after the component is initially committed and does not re-run because of ordinary prop/state changes.

Without a dependency array:

```jsx
useEffect(() => {
    console.log("Effect");
});
```

The effect runs after every completed render.

---

## 45. What is cleanup in `useEffect()`?

### Answer

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

Cleanup is useful for:

```text
Clearing timers
Removing event listeners
Unsubscribing
Cleaning up external resources
```

---

## 46. What is `useRef()`?

### Answer

`useRef()` creates a mutable ref object whose value persists between renders.

Changing `.current` does not itself cause a re-render.

Example:

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

Then:

```jsx
inputRef.current.focus();
```

can access the DOM element.

---

## 47. `useState()` vs `useRef()`

### Answer

```text
useState()
→ Stores state.
→ State updates can trigger a re-render.

useRef()
→ Stores a mutable reference.
→ Changing .current does not trigger a re-render.
```

---

## 48. What is conditional rendering?

### Answer

Conditional rendering means displaying different UI based on a condition.

Example:

```jsx
function App({ isLoggedIn }) {
    return (
        <div>
            {isLoggedIn ? (
                <h1>Welcome</h1>
            ) : (
                <h1>Please Login</h1>
            )}
        </div>
    );
}
```

---

## 49. How do you render a list in React?

### Answer

JavaScript's `map()` method is commonly used.

```jsx
const users = [
    { id: 1, name: "A" },
    { id: 2, name: "B" }
];

function App() {
    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>
                    {user.name}
                </li>
            ))}
        </ul>
    );
}
```

---

## 50. What are keys in React?

### Answer

Keys provide stable identity to list elements so React can correctly match items between renders.

Example:

```jsx
users.map(user => (
    <li key={user.id}>
        {user.name}
    </li>
))
```

Keys should generally be stable and unique among siblings.

---

## 51. Why should we avoid array indexes as keys?

### Answer

Array indexes can be problematic when items are inserted, removed, or reordered because the same index can represent a different item.

A stable identifier is generally better.

Example:

```jsx
<li key={user.id}>{user.name}</li>
```

is generally preferable to:

```jsx
<li key={index}>{user.name}</li>
```

when `user.id` is available.

---

## 52. What is event handling in React?

### Answer

React uses event handlers to respond to user interactions.

Example:

```jsx
function App() {
    const handleClick = () => {
        console.log("Clicked");
    };

    return (
        <button onClick={handleClick}>
            Click
        </button>
    );
}
```

---

## 53. What is a controlled component?

### Answer

A controlled form element gets its value from React state.

Example:

```jsx
const [name, setName] = useState("");

<input
    value={name}
    onChange={e => setName(e.target.value)}
/>
```

React state acts as the source of truth for the input value.

---

## 54. What is an uncontrolled component?

### Answer

An uncontrolled component allows the DOM to maintain the form value.

A ref can be used to access the value.

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

---

## 55. Controlled vs uncontrolled components

### Answer

| Controlled | Uncontrolled |
|---|---|
| Value managed by React state | Value managed by DOM |
| Uses `value` and `onChange` | Often uses refs |
| Easy to validate/control during changes | Can be simpler for some cases |
| Common in React forms | Useful in specific situations |

---

## 56. What is prop drilling?

### Answer

Prop drilling occurs when data is passed through several intermediate components just to reach a deeply nested component.

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

If A and B do not need the data but only pass it to C, this is prop drilling.

---

## 57. How can prop drilling be avoided?

### Answer

Depending on the application, you can use:

```text
Component composition
Context
State management solutions
```

Do not use Context or a state management library automatically; choose based on the application's requirements.

---

## 58. What is Context API?

### Answer

Context allows data to be shared with components deeper in the component tree without passing props through every intermediate component.

Common examples:

```text
Theme
Authentication information
Language
Shared configuration
```

---

## 59. What is `useContext()`?

### Answer

`useContext()` reads the current value from a React Context.

Example:

```jsx
const theme = useContext(ThemeContext);

console.log(theme);
```

---

## 60. What is lifting state up?

### Answer

Lifting state up means moving shared state to the closest common parent of the components that need it.

Example:

```text
       Parent
       /    \
   Child A  Child B
```

If both children need the same state:

```text
          Parent
          State
         /     \
    Child A   Child B
```

---

## 61. What is component composition?

### Answer

Component composition means building larger UI pieces by combining smaller reusable components.

Example:

```jsx
function Card({ children }) {
    return <div className="card">{children}</div>;
}
```

Usage:

```jsx
<Card>
    <h2>Hello</h2>
    <p>Welcome</p>
</Card>
```

---

## 62. What is the `children` prop?

### Answer

`children` represents the content placed inside a component's opening and closing tags.

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

---

## 63. What is the Virtual DOM?

### Answer

The Virtual DOM is a conceptual in-memory representation of the UI that React uses to determine what changes are needed.

When state or props change, React calculates the next UI and commits the required changes to the actual DOM.

---

## 64. What is reconciliation?

### Answer

Reconciliation is the process React uses to determine how the rendered UI should change when the component output changes.

Keys are especially important when reconciling lists.

---

## 65. What causes a React component to re-render?

### Answer

A component may re-render when:

```text
Its state changes
Its props change
A relevant context value changes
Its parent re-renders
```

A re-render does not mean that every DOM element is recreated.

---

## 66. What are React Hooks?

### Answer

Hooks are functions that allow functional components to use React features such as state, context, and other capabilities.

Important Hooks include:

```text
useState
useEffect
useRef
useContext
useMemo
useCallback
```

---

## 67. What are the Rules of Hooks?

### Answer

Important rules:

```text
1. Call Hooks at the top level.
2. Do not call Hooks inside loops or conditions.
3. Call Hooks from React function components or custom Hooks.
```

Correct:

```jsx
function App() {
    const [count, setCount] = useState(0);

    return <h1>{count}</h1>;
}
```

---

## 68. What is a custom Hook?

### Answer

A custom Hook is a reusable function that uses React Hooks to share stateful logic.

Example:

```jsx
function useCounter() {
    const [count, setCount] = useState(0);

    const increment = () => {
        setCount(prev => prev + 1);
    };

    return {
        count,
        increment
    };
}
```

Custom Hooks share logic, not UI.

---

## 69. What is React Router?

### Answer

React Router is commonly used to implement client-side routing in React applications.

Example:

```jsx
<Route
    path="/about"
    element={<About />}
/>
```

It allows different UI components to be associated with different URL paths.

---

## 70. What is client-side routing?

### Answer

Client-side routing allows a web application to display different UI based on the URL without requiring a full page reload for every route transition.

It is commonly used in single-page applications.

---

# Part 3: JavaScript + React Practical Questions

## 71. Why is `map()` commonly used in React?

### Answer

`map()` is commonly used to transform an array of data into an array of React elements.

Example:

```jsx
const users = ["A", "B", "C"];

return (
    <ul>
        {users.map(user => (
            <li key={user}>
                {user}
            </li>
        ))}
    </ul>
);
```

---

## 72. Why is immutability important in React?

### Answer

React applications commonly update state by creating new arrays or objects instead of directly mutating existing state.

Example:

```jsx
setUser(prev => ({
    ...prev,
    name: "Updated"
}));
```

This makes state updates predictable and works well with React's rendering model.

---

## 73. How do you update an array in React state?

### Answer

Create a new array instead of directly modifying the existing state.

Example:

```jsx
const [users, setUsers] = useState([]);

setUsers(prev => [
    ...prev,
    newUser
]);
```

---

## 74. How do you remove an item from an array in React state?

### Answer

Use `filter()` to create a new array.

```jsx
setUsers(prev =>
    prev.filter(user => user.id !== id)
);
```

---

## 75. How do you update an object in React state?

### Answer

Use the spread operator to create a new object.

```jsx
setUser(prev => ({
    ...prev,
    age: 23
}));
```

---

## 76. How do you fetch API data in React?

### Answer

A common approach is to use `useEffect()` with `fetch()`.

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

In real applications, loading and error states should also be handled.

---

## 77. How do you handle loading and error states?

### Answer

Maintain separate state values.

```jsx
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
const [users, setUsers] = useState([]);
```

Typical flow:

```text
Start request
    ↓
loading = true
    ↓
API response
    ↓
Success → store data
Error   → store error
    ↓
loading = false
```

---

## 78. How does React communicate with a backend?

### Answer

React communicates with the backend through HTTP requests.

Typical architecture:

```text
React Frontend
      ↓
HTTP Request
      ↓
Backend API
      ↓
Database
      ↓
JSON Response
      ↓
React
      ↓
Update State
      ↓
UI
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

## 79. What happens when you click a button that updates state?

### Answer

A simplified flow is:

```text
User clicks button
       ↓
Event handler executes
       ↓
State setter is called
       ↓
React schedules an update
       ↓
Component renders again
       ↓
React determines required UI changes
       ↓
Changes are committed
```

---

## 80. What is the difference between state and a normal JavaScript variable?

### Answer

A normal local variable does not provide React with a mechanism to trigger a UI update when it changes.

React state is managed by React, and updating it can cause the component to render again.

Example:

```jsx
let count = 0;
```

versus:

```jsx
const [count, setCount] = useState(0);
```

For values that affect rendered UI, React state is generally appropriate.

---

# Part 4: Project-Based Interview Questions

## 81. Explain your React project.

### Answer Structure

Use this structure:

```text
1. What the project does
2. Why you built it
3. Technologies used
4. How React was used
5. Important components
6. Backend/API communication
7. Database if applicable
8. Your specific contribution
9. Challenges faced
10. Result
```

### Example

> "My project is a web application built using React for the frontend. I divided the UI into reusable components and used React state to manage changing data. I used API calls to communicate with the backend and displayed the returned data dynamically. I also handled user interactions, forms, loading states, and errors. My main contribution was developing the frontend components and integrating them with the backend APIs."

Replace the generic parts with your actual project details.

---

## 82. Why did you choose React for your project?

### Answer

> "I chose React because the project required a dynamic user interface with reusable components. React allowed me to break the application into smaller components, manage state, handle user interactions, and update the UI based on changing data."

---

## 83. Which React components did you create?

### Answer

Be prepared to name your actual components.

For example:

```text
Navbar
Login
Dashboard
ProductList
ProductCard
Profile
Footer
```

Then explain:

> "I separated the application into components based on their responsibilities. Components that were reused across multiple pages were kept reusable."

Do not claim components that you did not actually build.

---

## 84. Where did you use state in your project?

### Answer

Mention actual examples from your project.

Possible examples:

```text
Login form values
User information
API response data
Search input
Selected filters
Modal visibility
Loading state
Error state
```

Example answer:

> "I used state for values that change during user interaction, such as form inputs, API response data, and loading/error states."

---

## 85. Where did you use `useEffect()`?

### Answer

If your project uses API calls:

> "I used `useEffect()` to perform side-effect logic such as loading data from the backend when the component was initialized or when specific dependencies changed."

Always explain your actual usage.

---

## 86. How did you handle API errors?

### Answer

A good approach is:

```text
try
 ↓
API request
 ↓
Check response
 ↓
Success → update state
Error → set error state
 ↓
finally
 ↓
stop loading
```

Example:

```jsx
try {
    const response = await fetch("/api/users");

    if (!response.ok) {
        throw new Error("Request failed");
    }

    const data = await response.json();
    setUsers(data);
} catch (error) {
    setError(error.message);
} finally {
    setLoading(false);
}
```

---

## 87. How did you make your React components reusable?

### Answer

> "I created components that accept data and behavior through props instead of hardcoding the same UI multiple times. This allowed the same component to be reused with different data."

Example:

```jsx
function UserCard({ name, email }) {
    return (
        <div>
            <h2>{name}</h2>
            <p>{email}</p>
        </div>
    );
}
```

---

## 88. What was the most difficult part of your React project?

### Answer

Do not give a fake generic answer.

Use this structure:

```text
Problem
↓
Why it was difficult
↓
What you tried
↓
Solution
↓
Result
```

Example:

> "The difficult part was integrating the frontend with the backend because the API response structure initially did not match what the UI expected. I inspected the response, adjusted the data mapping, added loading and error handling, and then tested the different states."

---

## 89. What would you improve in your project?

### Answer

Mention realistic improvements.

Examples:

```text
Better error handling
Improved form validation
Better component reuse
Improved accessibility
Better loading states
Pagination
Better performance
Testing
Improved responsive design
```

---

## 90. What happens from frontend to database when a user submits a form?

### Answer

A typical full-stack flow is:

```text
User submits form
        ↓
React event handler
        ↓
Validate input
        ↓
HTTP POST request
        ↓
Backend API
        ↓
Backend validation
        ↓
Database operation
        ↓
Backend response
        ↓
React receives response
        ↓
Update state
        ↓
UI changes
```

Be able to explain this using your actual project's architecture.

---

# Part 5: Important Output-Based Questions

## 91. What is the output?

```javascript
console.log(2 + "2");
```

### Answer

```text
22
```

The `+` operator performs string concatenation when one operand is a string.

---

## 92. What is the output?

```javascript
console.log("5" - 2);
```

### Answer

```text
3
```

The string is converted to a number for subtraction.

---

## 93. What is the output?

```javascript
console.log(5 == "5");
console.log(5 === "5");
```

### Answer

```text
true
false
```

---

## 94. What is the output?

```javascript
console.log(typeof null);
```

### Answer

```text
object
```

This is a historical JavaScript behavior.

---

## 95. What is the output?

```javascript
let x;

console.log(x);
```

### Answer

```text
undefined
```

---

## 96. What is the output?

```javascript
console.log([1, 2, 3].map(x => x * 2));
```

### Answer

```text
[2, 4, 6]
```

---

## 97. What is the output?

```javascript
console.log([1, 2, 3, 4].filter(x => x % 2 === 0));
```

### Answer

```text
[2, 4]
```

---

## 98. What is the output?

```javascript
console.log(
    [1, 2, 3].reduce((sum, x) => sum + x, 0)
);
```

### Answer

```text
6
```

---

## 99. What is the output?

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

console.log("C");
```

### Answer

```text
A
C
B
```

---

## 100. What is the output?

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(x => x + 1);

console.log(numbers);
console.log(result);
```

### Answer

```text
[1, 2, 3]
[2, 3, 4]
```

`map()` creates a new array and does not modify the original array.

---

# Part 6: Rapid-Fire Questions

## JavaScript

### Q101. Is JavaScript statically or dynamically typed?

**Answer:** JavaScript is dynamically typed.

### Q102. Is JavaScript single-threaded?

**Answer:** JavaScript execution is generally single-threaded per execution context, while the runtime can provide mechanisms for asynchronous operations and additional threads.

### Q103. What does `typeof` do?

**Answer:** It returns a string indicating the type of a value.

### Q104. What is `typeof null`?

**Answer:** `"object"`.

### Q105. What is `NaN`?

**Answer:** A special numeric value representing an invalid numeric result.

### Q106. What is a closure?

**Answer:** A function retaining access to variables from its surrounding lexical scope.

### Q107. What is a Promise?

**Answer:** An object representing the eventual result of an asynchronous operation.

### Q108. What does `async` do?

**Answer:** It makes a function return a Promise.

### Q109. What does `await` do?

**Answer:** It pauses execution within an async function until the awaited Promise settles, allowing the resolved value to be used in sequential-looking code.

### Q110. What is JSON?

**Answer:** A text-based format commonly used for structured data exchange.

### Q111. What does `map()` return?

**Answer:** A new array.

### Q112. What does `filter()` return?

**Answer:** A new array containing elements that satisfy the condition.

### Q113. What does `reduce()` return?

**Answer:** A single accumulated result, which can be of any type.

### Q114. What is destructuring?

**Answer:** A convenient syntax for extracting values from arrays or properties from objects.

### Q115. What is the spread operator?

**Answer:** Syntax that expands iterable elements or object properties.

---

# Part 7: React Rapid-Fire Questions

### Q116. What is React?

**Answer:** A JavaScript library for building user interfaces.

### Q117. What is JSX?

**Answer:** Syntax that allows HTML-like markup to be written in JavaScript.

### Q118. What is a component?

**Answer:** A reusable piece of UI and its associated logic.

### Q119. What are props?

**Answer:** Inputs passed from a parent component to a child component.

### Q120. What is state?

**Answer:** Data managed by a component or other state owner that can change over time.

### Q121. What is `useState()`?

**Answer:** A Hook used to manage state in a functional component.

### Q122. What is `useEffect()`?

**Answer:** A Hook used to synchronize a component with external systems and perform side-effect logic.

### Q123. What is `useRef()`?

**Answer:** A Hook that provides a persistent mutable reference whose `.current` changes do not themselves trigger re-renders.

### Q124. What are keys?

**Answer:** Stable identities for list elements that help React reconcile list changes.

### Q125. What is prop drilling?

**Answer:** Passing props through intermediate components just to reach a deeper component.

### Q126. What is Context?

**Answer:** A mechanism for making values available to components deeper in the tree without explicitly passing props through every intermediate component.

### Q127. What is lifting state up?

**Answer:** Moving shared state to the closest common parent of components that need it.

### Q128. What is a controlled component?

**Answer:** A form element whose value is controlled by React state.

### Q129. What is a custom Hook?

**Answer:** A reusable function that uses React Hooks to share stateful logic.

### Q130. What is React Router?

**Answer:** A commonly used library for implementing client-side routing in React applications.

---

# Part 8: Scenario-Based Questions

## 131. A list item is not updating correctly. What would you check?

### Answer

I would check:

```text
1. Whether state is being updated correctly.
2. Whether the array/object is being mutated directly.
3. Whether the list has stable keys.
4. Whether the new state actually differs as expected.
5. Whether the component receives the correct props.
```

---

## 132. Your API data is not appearing on the page. What would you check?

### Answer

I would check:

```text
1. Whether the API request is being executed.
2. Network response status.
3. Response structure.
4. Whether JSON parsing succeeds.
5. Whether state is updated.
6. Whether the component renders the correct state.
7. Console errors.
8. Loading and error handling.
```

---

## 133. The API is slow. What should the UI do?

### Answer

The UI should provide a loading state instead of appearing frozen.

Example:

```text
Request starts
     ↓
Show loading indicator
     ↓
Request succeeds
     ↓
Show data
```

If the request fails:

```text
Request fails
     ↓
Show meaningful error message
```

---

## 134. A child component needs to update data owned by the parent. How can you handle it?

### Answer

The parent can pass a callback function to the child through props.

Example:

```jsx
function Parent() {
    const handleUpdate = value => {
        console.log(value);
    };

    return <Child onUpdate={handleUpdate} />;
}
```

The child can call:

```jsx
onUpdate(newValue);
```

This follows React's common one-way data flow.

---

## 135. Multiple components need the same data. What can you do?

### Answer

Depending on the situation:

```text
Lift state to a common parent
        ↓
Pass props
```

If many distant components need the same data:

```text
Context
or
State management solution
```

should be considered.

---

## 136. How would you improve a slow React component?

### Answer

First identify the actual bottleneck.

Possible approaches include:

```text
Avoid unnecessary state
Avoid unnecessary renders
Use stable keys
Memoize expensive calculations when justified
Use React.memo when appropriate
Use useCallback when function identity matters
Lazy-load large components
Optimize API/data fetching
```

Do not blindly add memoization everywhere.

---

# Part 9: Final Interview Checklist

Before the interview, make sure you can answer these without reading notes:

## JavaScript

```text
[ ] What is JavaScript?
[ ] var vs let vs const
[ ] Scope
[ ] Hoisting
[ ] Temporal Dead Zone
[ ] == vs ===
[ ] Primitive data types
[ ] Truthy and falsy
[ ] Functions
[ ] Arrow functions
[ ] Callbacks
[ ] Higher-order functions
[ ] map()
[ ] filter()
[ ] reduce()
[ ] Objects
[ ] Destructuring
[ ] Spread
[ ] Rest
[ ] Closures
[ ] this
[ ] Promises
[ ] async/await
[ ] Event Loop
[ ] Synchronous vs asynchronous
[ ] DOM
[ ] Events
[ ] JSON
[ ] fetch()
[ ] Modules
[ ] Immutability
```

## React

```text
[ ] What is React?
[ ] Why React?
[ ] Components
[ ] Functional components
[ ] JSX
[ ] Props
[ ] State
[ ] Props vs State
[ ] useState
[ ] useEffect
[ ] useRef
[ ] useContext
[ ] Conditional rendering
[ ] List rendering
[ ] Keys
[ ] Event handling
[ ] Forms
[ ] Controlled components
[ ] Uncontrolled components
[ ] Prop drilling
[ ] Context
[ ] Lifting state up
[ ] Component composition
[ ] children
[ ] Custom Hooks
[ ] React Router
[ ] API integration
[ ] Loading/error states
[ ] Virtual DOM
[ ] Reconciliation
[ ] Re-rendering
[ ] useMemo
[ ] useCallback
[ ] React.memo
```

## Project

```text
[ ] Explain your project in 1–2 minutes
[ ] Explain why you chose React
[ ] Explain your components
[ ] Explain your state management
[ ] Explain your API integration
[ ] Explain your useEffect usage
[ ] Explain your forms
[ ] Explain loading/error handling
[ ] Explain routing
[ ] Explain your hardest problem
[ ] Explain your personal contribution
[ ] Explain what you would improve
```

---

# Final Preparation Strategy

For campus placements, do not try to become an advanced JavaScript or React developer just for the interview.

Your priority should be:

```text
JavaScript Fundamentals
        ↓
React Fundamentals
        ↓
Important Interview Questions
        ↓
Output/Scenario Questions
        ↓
Your Actual Project
        ↓
Mock Technical Interviews
```

The most important rule is:

> **If JavaScript or React is written on your resume, be prepared to explain anything you actually used in your project.**

Knowing definitions is useful, but being able to explain **where, why, and how you used the technology in your project** is what makes your preparation interview-ready.