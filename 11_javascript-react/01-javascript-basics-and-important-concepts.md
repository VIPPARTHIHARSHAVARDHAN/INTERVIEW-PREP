# JavaScript Basics and Important Concepts

> Placement-focused JavaScript notes covering the **important fundamentals and interview concepts** required for fresher technical interviews, especially when JavaScript is used in React projects.

---

# 1. What is JavaScript?

JavaScript is a **high-level, dynamically typed programming language** mainly used to make web applications interactive and dynamic.

It can run:

- In web browsers
- On servers using environments such as Node.js
- In other JavaScript runtimes

### Example

```javascript
let name = "Harsha";

console.log("Hello " + name);
```

### Interview Answer

> "JavaScript is a dynamically typed programming language commonly used to build interactive web applications. It runs in browsers and can also be used on the server with runtimes such as Node.js."

---

# 2. JavaScript vs Java

JavaScript and Java are different programming languages.

| JavaScript | Java |
|---|---|
| Dynamically typed | Statically typed |
| Commonly used for web development | Commonly used for backend, enterprise, Android historically, etc. |
| Prototype-based object model | Class-based object model |
| Commonly runs in browsers | Runs on JVM |
| Uses JavaScript engines | Uses JVM |

### Interview Answer

> "Despite the similar name, JavaScript and Java are different languages with different type systems, runtime environments, and object models."

---

# 3. What are Variables in JavaScript?

Variables are used to store data.

JavaScript provides:

```javascript
var
let
const
```

Example:

```javascript
let age = 22;
const name = "Harsha";
```

---

# 4. `var` vs `let` vs `const`

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Scope | Function | Block | Block |
| Redeclaration in same scope | Allowed | Not allowed | Not allowed |
| Reassignment | Allowed | Allowed | Not allowed |
| Hoisted | Yes | Yes, but inaccessible before declaration | Yes, but inaccessible before declaration |

### Example

```javascript
let age = 20;
age = 21;
```

Valid.

```javascript
const age = 20;
age = 21;
```

Invalid because a `const` binding cannot be reassigned.

### Interview Answer

> "I prefer `let` when a variable needs reassignment and `const` when it does not. `var` is function-scoped and is generally avoided in modern JavaScript."

---

# 5. What is Scope?

Scope determines where a variable can be accessed.

Important types:

```text
Global Scope
Function Scope
Block Scope
```

### Example

```javascript
let x = 10;

if (true) {
    let y = 20;
    console.log(x); // accessible
    console.log(y); // accessible
}

console.log(x); // accessible
// console.log(y); // Error
```

`let` and `const` are block-scoped.

---

# 6. What is Block Scope?

A block is generally code inside `{ }`.

Variables declared with `let` and `const` are limited to the block.

```javascript
if (true) {
    let message = "Hello";
    console.log(message);
}

// console.log(message); // Error
```

---

# 7. What is Function Scope?

Variables declared using `var` are function-scoped.

```javascript
function test() {
    var x = 10;
    console.log(x);
}

test();

// console.log(x); // Error
```

---

# 8. What are Data Types in JavaScript?

JavaScript data types can broadly be divided into:

### Primitive Types

```text
string
number
bigint
boolean
undefined
null
symbol
```

### Non-Primitive / Object Type

```text
object
```

Arrays and functions are also objects in JavaScript's type system, with functions having callable behavior.

---

# 9. What is a Primitive Data Type?

Primitive values are basic values that are not objects.

Examples:

```javascript
let name = "Harsha";
let age = 22;
let isStudent = true;
let value = undefined;
let data = null;
```

Primitive types include:

```text
string
number
bigint
boolean
undefined
null
symbol
```

---

# 10. What is the `typeof` Operator?

`typeof` is used to determine the type of a value.

```javascript
typeof "Hello";     // "string"
typeof 10;          // "number"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
```

One important JavaScript quirk:

```javascript
typeof null;        // "object"
```

This is a historical behavior of JavaScript.

---

# 11. What is `null`?

`null` represents an intentional absence of a value.

```javascript
let user = null;
```

It means the variable currently has no object/value assigned intentionally.

---

# 12. What is `undefined`?

`undefined` generally means a value has not been assigned.

```javascript
let x;

console.log(x); // undefined
```

### `null` vs `undefined`

```text
null
→ Intentional absence of value.

undefined
→ Value is generally missing/not assigned.
```

---

# 13. What is Type Coercion?

Type coercion is the conversion of a value from one type to another, sometimes automatically.

Example:

```javascript
console.log("5" + 2);
```

Output:

```text
52
```

The number is converted to a string for the `+` operation.

Another example:

```javascript
console.log("5" - 2);
```

Output:

```text
3
```

Here JavaScript converts the string to a number.

---

# 14. `==` vs `===`

### `==`

Performs comparison with type coercion when necessary.

```javascript
5 == "5"; // true
```

### `===`

Performs strict equality comparison without converting the operands to make their types match.

```javascript
5 === "5"; // false
```

### Interview Answer

> "`==` allows type coercion, while `===` checks strict equality. In most application code, `===` is preferred because it avoids unexpected type conversion."

---

# 15. `!=` vs `!==`

```javascript
5 != "5";   // false
5 !== "5";  // true
```

`!=` allows type coercion.

`!==` performs strict inequality comparison.

---

# 16. What are Truthy and Falsy Values?

JavaScript converts values to boolean in conditions.

Common falsy values include:

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
if ("hello") {
    console.log("Truthy");
}
```

Output:

```text
Truthy
```

---

# 17. What is `NaN`?

`NaN` means **Not-a-Number**.

It represents an invalid numeric result.

Example:

```javascript
let result = Number("hello");

console.log(result); // NaN
```

Check it using:

```javascript
Number.isNaN(result);
```

---

# 18. What is a Function?

A function is a reusable block of code designed to perform a task.

```javascript
function add(a, b) {
    return a + b;
}

console.log(add(2, 3));
```

Output:

```text
5
```

---

# 19. What is an Arrow Function?

Arrow functions provide a shorter syntax for writing functions.

```javascript
const add = (a, b) => {
    return a + b;
};
```

For a single expression:

```javascript
const add = (a, b) => a + b;
```

Arrow functions are especially common in React code.

---

# 20. Regular Function vs Arrow Function

### Regular Function

```javascript
function greet() {
    console.log("Hello");
}
```

### Arrow Function

```javascript
const greet = () => {
    console.log("Hello");
};
```

One important difference is how `this` is handled.

Arrow functions **do not have their own `this`**; they capture `this` from the surrounding lexical scope.

---

# 21. What is a Callback Function?

A callback is a function passed to another function to be called later or as part of another operation.

```javascript
function greet(name, callback) {
    console.log("Hello " + name);
    callback();
}

function done() {
    console.log("Done");
}

greet("Harsha", done);
```

Callbacks are common in:

```text
Array methods
Event handling
Asynchronous programming
```

---

# 22. What is a Higher-Order Function?

A higher-order function is a function that:

- Takes another function as an argument, or
- Returns a function.

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

# 23. What is an Array?

An array is an ordered collection of values.

```javascript
const numbers = [10, 20, 30, 40];
```

Access an element:

```javascript
console.log(numbers[0]);
```

Output:

```text
10
```

---

# 24. Important Array Methods

Important methods for interviews and React projects:

```text
map()
filter()
reduce()
forEach()
find()
some()
every()
includes()
sort()
slice()
splice()
push()
pop()
shift()
unshift()
```

---

# 25. What is `map()`?

`map()` creates a new array by applying a function to every element.

```javascript
const numbers = [1, 2, 3];

const squares = numbers.map(num => num * num);

console.log(squares);
```

Output:

```text
[1, 4, 9]
```

### Important

`map()` returns a new array.

---

# 26. What is `filter()`?

`filter()` creates a new array containing elements that satisfy a condition.

```javascript
const numbers = [1, 2, 3, 4, 5];

const even = numbers.filter(num => num % 2 === 0);

console.log(even);
```

Output:

```text
[2, 4]
```

---

# 27. What is `reduce()`?

`reduce()` processes array elements and produces a single accumulated result.

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((total, num) => total + num, 0);

console.log(sum);
```

Output:

```text
10
```

Common uses:

```text
Sum
Product
Counting
Grouping
Building objects
```

---

# 28. `map()` vs `forEach()`

| `map()` | `forEach()` |
|---|---|
| Returns a new array | Returns `undefined` |
| Used to transform elements | Used to perform an action |
| Common for creating transformed arrays | Common for side effects |

Example:

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(x => x * 2);

console.log(result);
```

---

# 29. `filter()` vs `find()`

### `filter()`

Returns an array of all matching elements.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.filter(x => x > 2);

console.log(result);
```

Output:

```text
[3, 4]
```

### `find()`

Returns the first matching element.

```javascript
const result = numbers.find(x => x > 2);

console.log(result);
```

Output:

```text
3
```

---

# 30. What is an Object?

An object stores data in key-value pairs.

```javascript
const user = {
    name: "Harsha",
    age: 22,
    city: "Hyderabad"
};
```

Access values:

```javascript
console.log(user.name);
console.log(user["age"]);
```

---

# 31. Dot Notation vs Bracket Notation

### Dot notation

```javascript
user.name;
```

### Bracket notation

```javascript
user["name"];
```

Bracket notation is useful when the property name is stored in a variable.

```javascript
const key = "name";

console.log(user[key]);
```

---

# 32. What is Destructuring?

Destructuring allows values to be extracted from arrays or objects conveniently.

### Object Destructuring

```javascript
const user = {
    name: "Harsha",
    age: 22
};

const { name, age } = user;

console.log(name);
console.log(age);
```

### Array Destructuring

```javascript
const numbers = [10, 20];

const [a, b] = numbers;

console.log(a);
console.log(b);
```

Destructuring is frequently used in React.

---

# 33. What is the Spread Operator?

The spread operator `...` expands iterable values or object properties.

### Array Example

```javascript
const a = [1, 2];
const b = [3, 4];

const result = [...a, ...b];

console.log(result);
```

Output:

```text
[1, 2, 3, 4]
```

### Object Example

```javascript
const user = {
    name: "Harsha"
};

const updatedUser = {
    ...user,
    age: 22
};
```

Spread syntax is commonly used when creating updated state in React.

---

# 34. What is the Rest Parameter?

The rest parameter collects remaining arguments into an array.

```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4));
```

Output:

```text
10
```

### Spread vs Rest

```text
Spread
→ Expands values.

Rest
→ Collects values.
```

Both use:

```javascript
...
```

---

# 35. What is Hoisting?

Hoisting refers to JavaScript's handling of declarations before execution of the corresponding code.

Example:

```javascript
console.log(x);

var x = 10;
```

This behaves roughly as if the `var` declaration were processed before the assignment, so the result is:

```text
undefined
```

`let` and `const` are also hoisted in the language's execution model, but they cannot be accessed before their declaration because they are in the **Temporal Dead Zone (TDZ)**.

Example:

```javascript
console.log(x);

let x = 10;
```

This results in a `ReferenceError`.

---

# 36. What is the Temporal Dead Zone?

The Temporal Dead Zone is the period between entering a scope and the point where a `let`, `const`, or `class` declaration is initialized.

Example:

```javascript
console.log(x);

let x = 10;
```

Accessing `x` before its initialization causes a `ReferenceError`.

---

# 37. What is a Closure?

A closure occurs when a function remembers and can access variables from its surrounding lexical scope even after the outer function has finished executing.

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

The inner function retains access to `count`.

### Interview Answer

> "A closure is a function together with access to variables from its surrounding lexical scope. It allows an inner function to remember variables even after the outer function has finished."

---

# 38. Why are Closures useful?

Closures are useful for:

```text
Data privacy
State preservation
Callbacks
Event handlers
Function factories
Timers
```

They are also important for understanding React and JavaScript behavior.

---

# 39. What is Lexical Scope?

Lexical scope means that the scope of a variable is determined by where the code is written.

Example:

```javascript
function outer() {
    let message = "Hello";

    function inner() {
        console.log(message);
    }

    inner();
}
```

`inner()` can access `message` because it is defined inside the lexical scope of `outer()`.

---

# 40. What is `this` in JavaScript?

`this` refers to a value determined by how a function is called.

In object method calls:

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

The exact behavior of `this` depends on the calling context.

---

# 41. How is `this` different in Arrow Functions?

Arrow functions do not create their own `this`.

They capture `this` from the surrounding lexical scope.

Example:

```javascript
const obj = {
    name: "Harsha",

    greet: () => {
        console.log(this.name);
    }
};
```

Using an arrow function as an object method generally does **not** make `this` refer to `obj`.

### Interview Point

> "Arrow functions have lexical `this`, while regular functions determine `this` based on how they are called."

---

# 42. What is a Promise?

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

# 43. What is `async/await`?

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

# 44. Promise vs `async/await`

Both are used for asynchronous programming.

```text
Promise
→ Uses .then() / .catch()

async/await
→ Provides syntax that makes asynchronous code easier to read.
```

Example using Promise methods:

```javascript
fetch("/api/users")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

Using `async/await`:

```javascript
async function getUsers() {
    try {
        const response = await fetch("/api/users");
        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

---

# 45. What is `try...catch`?

`try...catch` is used to handle runtime errors.

```javascript
try {
    const result = riskyOperation();
    console.log(result);
} catch (error) {
    console.log(error);
}
```

It helps prevent an error from terminating the current execution flow without being handled.

---

# 46. What is the Event Loop?

JavaScript execution is based on an event-driven model.

The event loop coordinates:

```text
Call Stack
Web/Runtime APIs
Task Queues
Microtask Queue
```

It allows asynchronous operations to be handled while JavaScript executes code on its main thread.

Example:

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

The callback from `setTimeout` does not execute immediately after being registered.

---

# 47. What is the Call Stack?

The call stack keeps track of function calls currently being executed.

Example:

```javascript
function one() {
    two();
}

function two() {
    console.log("Hello");
}

one();
```

Conceptually:

```text
one()
  ↓
two()
  ↓
console.log()
```

Functions are added to and removed from the stack as they execute.

---

# 48. What is Asynchronous JavaScript?

Asynchronous JavaScript allows operations that may take time to complete to be handled without blocking normal JavaScript execution.

Common examples:

```text
API requests
Timers
File operations in server environments
User events
```

Common tools:

```text
Callbacks
Promises
async/await
```

---

# 49. What is the DOM?

DOM stands for **Document Object Model**.

The browser represents an HTML document as a tree of objects.

Example:

```text
Document
   ↓
HTML
   ├── Head
   └── Body
        ├── H1
        └── Button
```

JavaScript can interact with the DOM to:

```text
Find elements
Change content
Change attributes
Handle events
Create/remove elements
```

---

# 50. How do you select an element from the DOM?

Common methods:

```javascript
document.getElementById("title");

document.querySelector(".title");

document.querySelectorAll(".item");
```

`querySelector()` returns the first matching element.

`querySelectorAll()` returns a collection of all matching elements.

---

# 51. What is Event Handling?

Event handling means responding to events such as:

```text
Click
Input
Submit
Mouse movement
Keyboard events
```

Example:

```javascript
const button = document.querySelector("#btn");

button.addEventListener("click", () => {
    console.log("Button clicked");
});
```

---

# 52. What is Event Bubbling?

Event bubbling means an event generally propagates from the target element upward through its ancestors.

Example:

```text
Button
  ↓
Div
  ↓
Body
  ↓
Document
```

An event triggered on the button can also reach parent elements unless propagation is stopped.

---

# 53. What is Event Capturing?

Event capturing is the phase where an event travels from an outer ancestor toward the target element.

Conceptually:

```text
Document
   ↓
Body
   ↓
Div
   ↓
Button
```

Event propagation commonly consists of:

```text
Capturing phase
Target phase
Bubbling phase
```

---

# 54. What is JSON?

JSON stands for **JavaScript Object Notation**.

It is a text-based format commonly used for exchanging structured data between applications.

Example:

```json
{
    "name": "Harsha",
    "age": 22
}
```

Convert JSON string to JavaScript object:

```javascript
const user = JSON.parse(jsonString);
```

Convert JavaScript object to JSON string:

```javascript
const jsonString = JSON.stringify(user);
```

---

# 55. What is the difference between `JSON.parse()` and `JSON.stringify()`?

```text
JSON.parse()
→ JSON string → JavaScript value/object

JSON.stringify()
→ JavaScript value/object → JSON string
```

Example:

```javascript
const json = '{"name":"Harsha"}';

const obj = JSON.parse(json);

const text = JSON.stringify(obj);
```

---

# 56. What is an API call in JavaScript?

An API call is a request made by the application to a server to exchange data.

A common approach is `fetch()`.

```javascript
fetch("/api/users")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

In React applications, API calls are commonly performed when data needs to be loaded or updated.

---

# 57. What is `fetch()`?

`fetch()` is a browser API used to make network requests.

Example:

```javascript
fetch("https://example.com/api/users")
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

`fetch()` returns a Promise.

---

# 58. What are ES6 features?

ES6, also called ECMAScript 2015, introduced many important JavaScript features.

Important examples:

```text
let
const
Arrow Functions
Template Literals
Destructuring
Spread Operator
Rest Parameters
Classes
Modules
Promises
Default Parameters
```

---

# 59. What are Template Literals?

Template literals use backticks and allow string interpolation.

```javascript
const name = "Harsha";
const age = 22;

console.log(`My name is ${name} and I am ${age} years old.`);
```

They are easier to use than repeated string concatenation.

---

# 60. What are Default Parameters?

Default parameters provide a default value when an argument is not supplied.

```javascript
function greet(name = "User") {
    console.log(`Hello ${name}`);
}

greet();
```

Output:

```text
Hello User
```

---

# 61. What are JavaScript Modules?

Modules allow code to be separated into reusable files.

### Export

```javascript
export const add = (a, b) => a + b;
```

### Import

```javascript
import { add } from "./math.js";
```

Modules help organize larger applications.

React projects commonly use modules.

---

# 62. What is `export default`?

A default export provides the primary exported value from a module.

```javascript
export default function App() {
    console.log("App");
}
```

It can be imported without curly braces:

```javascript
import App from "./App";
```

Named exports use curly braces:

```javascript
export const add = () => {};

import { add } from "./math";
```

---

# 63. Named Export vs Default Export

| Named Export | Default Export |
|---|---|
| Can have multiple per module | One default export per module |
| Imported using `{}` | Imported without `{}` |
| Import name generally matches exported name | Import name can be chosen |

Example:

```javascript
export const add = () => {};
export const subtract = () => {};
```

```javascript
import { add, subtract } from "./math";
```

Default:

```javascript
export default App;
```

```javascript
import App from "./App";
```

---

# 64. What is Immutability?

Immutability means avoiding direct modification of an existing value and instead creating a new value when an update is required.

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

This pattern is especially important in React state updates.

---

# 65. Shallow Copy vs Deep Copy

### Shallow Copy

Copies the top-level structure but nested objects can still be shared.

Example:

```javascript
const copy = { ...original };
```

### Deep Copy

Creates independent copies of nested data as well.

One modern approach for supported data is:

```javascript
const copy = structuredClone(original);
```

### Interview Point

> "Spread syntax creates a shallow copy, not a deep copy."

---

# 66. What is Optional Chaining?

Optional chaining `?.` allows safe access to potentially missing properties.

```javascript
const user = {};

console.log(user.address?.city);
```

Instead of throwing an error because `address` is undefined, the expression evaluates to `undefined`.

---

# 67. What is Nullish Coalescing?

The nullish coalescing operator `??` provides a fallback when the left side is `null` or `undefined`.

```javascript
const name = null;

const result = name ?? "Guest";

console.log(result);
```

Output:

```text
Guest
```

Unlike `||`, `??` does not treat values such as `0` or `""` as nullish.

---

# 68. `||` vs `??`

```javascript
const a = 0 || 10;
console.log(a);
```

Output:

```text
10
```

But:

```javascript
const b = 0 ?? 10;
console.log(b);
```

Output:

```text
0
```

### Reason

```text
|| 
→ Uses truthiness.

??
→ Uses only null and undefined.
```

---

# 69. What is an IIFE?

IIFE stands for **Immediately Invoked Function Expression**.

It is a function expression that is executed immediately after creation.

```javascript
(function () {
    console.log("Hello");
})();
```

IIFEs were historically used to create private scopes before modern modules and block scoping became common.

### Placement Priority

Know the definition, but it is **not a high-priority modern JavaScript topic** compared with closures, promises, async/await, arrays, objects, and scope.

---

# 70. What is the difference between `slice()` and `splice()`?

### `slice()`

Returns a portion of an array without modifying the original array.

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.slice(1, 3);

console.log(result);
```

Output:

```text
[2, 3]
```

### `splice()`

Can add, remove, or replace elements and modifies the original array.

```javascript
const numbers = [1, 2, 3, 4];

numbers.splice(1, 2);

console.log(numbers);
```

Output:

```text
[1, 4]
```

---

# 71. What is the difference between `push()` and `concat()`?

### `push()`

Adds elements to an array and modifies the original array.

```javascript
const arr = [1, 2];

arr.push(3);

console.log(arr);
```

### `concat()`

Creates a new array.

```javascript
const arr = [1, 2];

const result = arr.concat(3);

console.log(result);
```

---

# 72. What is a Set?

A `Set` is a collection that stores unique values.

```javascript
const numbers = new Set([1, 2, 2, 3]);

console.log(numbers);
```

The duplicate `2` is stored only once.

Convert it to an array:

```javascript
const unique = [...new Set([1, 2, 2, 3])];

console.log(unique);
```

Output:

```text
[1, 2, 3]
```

---

# 73. What is a Map?

A `Map` stores key-value pairs.

```javascript
const map = new Map();

map.set("name", "Harsha");
map.set("age", 22);

console.log(map.get("name"));
```

Output:

```text
Harsha
```

A `Map` can use values of different types as keys.

---

# 74. Object vs Map

| Object | Map |
|---|---|
| Key-value structure | Key-value structure |
| Common for structured records | Designed specifically for key-value collections |
| Keys are primarily strings/symbols | Keys can be values of many types |
| Convenient object syntax | Provides methods such as `set`, `get`, `has` |

For normal application data, objects are extremely common. `Map` is useful when its specific collection behavior is needed.

---

# 75. What is Garbage Collection?

JavaScript automatically manages memory.

When objects are no longer reachable by the program, the JavaScript engine can eventually reclaim their memory through garbage collection.

Developers generally do not manually free memory as they would in languages with manual memory management.

---

# 76. What is Pass by Value in JavaScript?

JavaScript passes arguments by value.

For primitive values, the value itself is copied.

```javascript
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

For objects, the copied value is a reference to the same object.

---

# 77. How are Objects Passed to Functions?

When an object is passed to a function, the value passed is a reference to the object.

Example:

```javascript
function update(user) {
    user.name = "Updated";
}

const user = {
    name: "Harsha"
};

update(user);

console.log(user.name);
```

Output:

```text
Updated
```

Both the caller and function can refer to the same object.

### Interview Answer

> "JavaScript passes arguments by value. For objects, the value being passed is a reference to the same object, so mutations to that object can be visible to the caller."

---

# 78. What is Strict Mode?

Strict mode enables stricter JavaScript behavior.

```javascript
"use strict";
```

It helps detect certain mistakes and prevents some problematic behaviors.

Modules are automatically strict mode.

---

# 79. What is the Difference Between Synchronous and Asynchronous Code?

### Synchronous

Code executes sequentially and the next operation waits for the current operation.

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

Some operations can complete later while other JavaScript execution continues.

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 1000);

console.log("C");
```

Output:

```text
A
C
B
```

---

# 80. Important JavaScript Concepts for React

Because React projects use JavaScript heavily, these concepts are especially important:

```text
let / const
Arrow Functions
Objects
Arrays
map()
filter()
reduce()
Destructuring
Spread Operator
Rest Parameters
Modules
Promises
async/await
Closures
Scope
this
Events
JSON
API calls
Immutability
Optional Chaining
Nullish Coalescing
```

You should be able to explain these before going deep into React.

---

# 81. Common JavaScript Output Questions

## Question 1

```javascript
console.log(2 + "2");
```

### Answer

```text
22
```

Because `+` performs string concatenation when one operand becomes a string.

---

## Question 2

```javascript
console.log("5" - 2);
```

### Answer

```text
3
```

The string is converted to a number for the subtraction operation.

---

## Question 3

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

## Question 4

```javascript
console.log(typeof null);
```

### Answer

```text
object
```

This is a historical JavaScript behavior.

---

## Question 5

```javascript
let x;

console.log(x);
```

### Answer

```text
undefined
```

---

## Question 6

```javascript
console.log(Boolean(""));
console.log(Boolean("Hello"));
```

### Answer

```text
false
true
```

---

## Question 7

```javascript
console.log([1, 2, 3].map(x => x * 2));
```

### Answer

```text
[2, 4, 6]
```

---

## Question 8

```javascript
console.log([1, 2, 3, 4].filter(x => x % 2 === 0));
```

### Answer

```text
[2, 4]
```

---

## Question 9

```javascript
console.log([1, 2, 3].reduce((sum, x) => sum + x, 0));
```

### Answer

```text
6
```

---

## Question 10

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

# 82. Most Important JavaScript Interview Questions

## Q1. What is JavaScript?

**Answer:** JavaScript is a dynamically typed programming language widely used for interactive web applications and also available in server-side runtimes.

## Q2. What is the difference between `var`, `let`, and `const`?

**Answer:** `var` is function-scoped, while `let` and `const` are block-scoped. `let` allows reassignment, while `const` does not allow reassignment of its binding.

## Q3. What is the difference between `==` and `===`?

**Answer:** `==` allows type coercion, while `===` performs strict equality comparison.

## Q4. What is hoisting?

**Answer:** Hoisting describes how JavaScript handles declarations during execution setup. `var` can be accessed before its declaration as `undefined`, while `let` and `const` cannot be accessed before initialization because of the Temporal Dead Zone.

## Q5. What is a closure?

**Answer:** A closure is a function that retains access to variables from its surrounding lexical scope.

## Q6. What is an arrow function?

**Answer:** An arrow function is a shorter function syntax and has lexical `this`.

## Q7. What is a callback?

**Answer:** A callback is a function passed to another function to be invoked later or during an operation.

## Q8. What is a Promise?

**Answer:** A Promise represents the eventual success or failure of an asynchronous operation.

## Q9. What is `async/await`?

**Answer:** `async/await` is syntax for working with Promises in a more readable sequential style.

## Q10. What is the event loop?

**Answer:** The event loop coordinates asynchronous callbacks and other queued work with JavaScript execution.

## Q11. What is the DOM?

**Answer:** The DOM is an object representation of an HTML document that JavaScript can interact with.

## Q12. What is JSON?

**Answer:** JSON is a text-based format commonly used for exchanging structured data.

## Q13. What is destructuring?

**Answer:** Destructuring extracts values from arrays or properties from objects into variables.

## Q14. What is the spread operator?

**Answer:** Spread syntax expands elements of an iterable or properties of an object.

## Q15. What is the rest parameter?

**Answer:** Rest syntax collects remaining function arguments into an array.

## Q16. What is `map()`?

**Answer:** `map()` creates a new array by transforming each element.

## Q17. What is `filter()`?

**Answer:** `filter()` creates a new array containing elements that satisfy a condition.

## Q18. What is `reduce()`?

**Answer:** `reduce()` combines array elements into a single accumulated result.

## Q19. What is the difference between `map()` and `forEach()`?

**Answer:** `map()` returns a new array, while `forEach()` is generally used to perform an action on each element and returns `undefined`.

## Q20. What is the difference between `slice()` and `splice()`?

**Answer:** `slice()` returns a portion without modifying the original array, while `splice()` can modify the original array by adding, removing, or replacing elements.

## Q21. What is `this`?

**Answer:** `this` is determined by the function's calling context, while arrow functions capture it lexically.

## Q22. What is type coercion?

**Answer:** Type coercion is the conversion of values from one type to another, sometimes automatically.

## Q23. What are truthy and falsy values?

**Answer:** They are values that JavaScript converts to `true` or `false` in boolean contexts. Values such as `false`, `0`, `""`, `null`, `undefined`, and `NaN` are falsy.

## Q24. What is the difference between `null` and `undefined`?

**Answer:** `null` generally represents an intentional absence of a value, while `undefined` generally means a value has not been assigned.

## Q25. What is immutability?

**Answer:** Immutability means avoiding direct modification of existing data and creating a new value when an update is needed.

---

# 83. JavaScript Topics You Must Be Able to Explain Without Notes

Before an interview, make sure you can explain these naturally:

```text
1. var vs let vs const
2. Scope
3. Hoisting
4. Temporal Dead Zone
5. == vs ===
6. Primitive data types
7. Truthy and falsy values
8. Functions
9. Arrow functions
10. Callbacks
11. Higher-order functions
12. Arrays
13. map()
14. filter()
15. reduce()
16. Objects
17. Destructuring
18. Spread and Rest
19. Closures
20. this
21. Promises
22. async/await
23. Event Loop
24. Synchronous vs asynchronous
25. DOM
26. Event handling
27. JSON
28. fetch()
29. Modules
30. Immutability
31. Optional chaining
32. Nullish coalescing
```

---

# 84. Final Interview Revision

## Highest Priority

```text
★★★★★ var vs let vs const
★★★★★ == vs ===
★★★★★ Scope
★★★★★ Hoisting
★★★★★ Closures
★★★★★ Functions
★★★★★ Arrow Functions
★★★★★ Arrays
★★★★★ map/filter/reduce
★★★★★ Objects
★★★★★ Destructuring
★★★★★ Spread/Rest
★★★★★ Promises
★★★★★ async/await
★★★★★ Event Loop
★★★★★ JSON
★★★★★ API / fetch
★★★★★ Immutability
```

## Medium Priority

```text
★★★★ this
★★★★ DOM
★★★★ Event Bubbling
★★★★ Event Capturing
★★★★ Modules
★★★★ Optional Chaining
★★★★ Nullish Coalescing
★★★★ Set
★★★★ Map
★★★★ slice vs splice
★★★★ Shallow vs Deep Copy
```

## Lower Priority for Fresher Placements

```text
★★ IIFE
★★ Advanced prototype internals
★★ Complex metaprogramming
★★ Advanced JavaScript engine internals
```

> **Placement Focus:** Do not try to become a JavaScript expert before your interview. Since JavaScript is being used in your React projects, focus on being able to explain the important fundamentals above and, most importantly, explain **how you used JavaScript in your own project**.