# Python Functions — Interview Preparation

## 1. What Is a Function in Python?

A function is a reusable block of code designed to perform a specific task.

Instead of writing the same logic multiple times, we can define it once and call it whenever required.

### Example

```python
def greet():
    print("Hello, Harsha")

greet()
```

Output:

```text
Hello, Harsha
```

### Interview Answer

> A function is a reusable block of code that performs a specific task. Functions improve code reusability, readability, maintainability, and reduce duplicate code.

### Real-World Example

In a data-processing application, instead of writing validation logic repeatedly for different datasets, we can create a function such as:

```python
def validate_record(record):
    # validation logic
    return True
```

and reuse it wherever required.

---

# 2. Why Do We Use Functions?

Functions provide several advantages:

- Code reusability
- Better readability
- Easier debugging
- Easier testing
- Better maintainability
- Separation of responsibilities
- Reduced code duplication

### Example Without a Function

```python
a = 10
b = 20
print(a + b)

x = 30
y = 40
print(x + y)
```

### Using a Function

```python
def add(a, b):
    return a + b

print(add(10, 20))
print(add(30, 40))
```

The logic is written only once.

---

# 3. How Do You Define a Function?

Use the `def` keyword.

```python
def function_name():
    # function body
    pass
```

Example:

```python
def greet():
    print("Hello")
```

The function does not execute merely because it is defined.

It executes when called:

```python
greet()
```

---

# 4. What Is Function Calling?

Calling a function means executing the function by using its name followed by parentheses.

```python
def greet():
    print("Hello")

greet()
```

Here:

```python
greet()
```

is the function call.

---

# 5. What Are Parameters and Arguments?

A **parameter** is a variable defined in the function definition.

An **argument** is the actual value passed to the function when calling it.

```python
def add(a, b):
    return a + b
```

Here:

```text
a and b -> parameters
```

When we call:

```python
add(10, 20)
```

```text
10 and 20 -> arguments
```

### Interview Answer

> Parameters are variables specified in the function definition, while arguments are the actual values supplied when the function is called.

---

# 6. What Is a Return Statement?

`return` sends a value back from a function to its caller.

```python
def add(a, b):
    return a + b

result = add(10, 20)

print(result)
```

Output:

```text
30
```

### Important Point

`return` also terminates the current function execution.

```python
def test():
    return 10
    print("Hello")

print(test())
```

Output:

```text
10
```

The `print("Hello")` is never reached.

---

# 7. What Happens If a Function Has No `return` Statement?

Python implicitly returns `None`.

```python
def greet():
    print("Hello")

result = greet()

print(result)
```

Output:

```text
Hello
None
```

### Interview Answer

> If a function does not explicitly return a value, Python returns `None`.

---

# 8. Difference Between `print()` and `return`

This is a very common interview question.

### `print()`

Displays a value on the screen.

```python
def add(a, b):
    print(a + b)

result = add(10, 20)

print(result)
```

Output:

```text
30
None
```

### `return`

Sends the value back to the caller.

```python
def add(a, b):
    return a + b

result = add(10, 20)

print(result)
```

Output:

```text
30
```

### Interview Answer

> `print()` displays a value, whereas `return` sends a value back to the caller and allows the returned value to be stored, reused, or passed to another function.

---

# 9. Can a Function Return Multiple Values?

Yes.

Python allows a function to return multiple values.

```python
def calculate(a, b):
    return a + b, a - b, a * b

result = calculate(10, 5)

print(result)
```

Output:

```text
(15, 5, 50)
```

The values are returned as a tuple.

We can unpack them:

```python
addition, subtraction, multiplication = calculate(10, 5)

print(addition)
print(subtraction)
print(multiplication)
```

---

# 10. Can a Function Return a List, Dictionary, or Object?

Yes.

```python
def get_data():
    return {
        "name": "Harsha",
        "age": 21
    }

data = get_data()

print(data)
```

Functions can return almost any Python object.

---

# 11. What Are Default Arguments?

A default argument is a parameter that has a predefined value.

```python
def greet(name="Guest"):
    print("Hello", name)

greet()
greet("Harsha")
```

Output:

```text
Hello Guest
Hello Harsha
```

If no argument is provided, the default value is used.

---

# 12. What Are Positional Arguments?

Arguments passed according to the position of parameters are positional arguments.

```python
def introduce(name, age):
    print(name, age)

introduce("Harsha", 21)
```

Here:

```text
"Harsha" -> name
21 -> age
```

The order matters.

---

# 13. What Are Keyword Arguments?

Arguments can be passed by explicitly specifying parameter names.

```python
def introduce(name, age):
    print(name, age)

introduce(age=21, name="Harsha")
```

The order does not matter when using keyword arguments.

---

# 14. Difference Between Positional and Keyword Arguments

### Positional

```python
introduce("Harsha", 21)
```

Values are assigned based on position.

### Keyword

```python
introduce(name="Harsha", age=21)
```

Values are assigned based on parameter name.

### Interview Answer

> Positional arguments are matched based on their position, while keyword arguments are matched explicitly using parameter names.

---

# 15. Can We Mix Positional and Keyword Arguments?

Yes, but positional arguments must come before keyword arguments.

Correct:

```python
def introduce(name, age, city):
    print(name, age, city)

introduce("Harsha", age=21, city="Hyderabad")
```

Incorrect:

```python
introduce(name="Harsha", 21, city="Hyderabad")
```

A positional argument cannot follow a keyword argument in a function call.

---

# 16. What Are `*args`?

`*args` allows a function to accept a variable number of positional arguments.

```python
def add(*args):
    total = 0

    for value in args:
        total += value

    return total

print(add(10, 20))
print(add(10, 20, 30))
print(add(1, 2, 3, 4, 5))
```

Output:

```text
30
60
15
```

Inside the function, `args` is a tuple.

---

# 17. Why Do We Use `*args`?

When we don't know beforehand how many positional arguments the caller will provide.

```python
def show(*args):
    print(args)

show(10, 20, 30)
```

Output:

```text
(10, 20, 30)
```

### Interview Answer

> `*args` allows a function to accept a variable number of positional arguments. Inside the function, those arguments are available as a tuple.

---

# 18. What Are `**kwargs`?

`**kwargs` allows a function to accept a variable number of keyword arguments.

```python
def show(**kwargs):
    print(kwargs)

show(name="Harsha", age=21, city="Hyderabad")
```

Output:

```text
{'name': 'Harsha', 'age': 21, 'city': 'Hyderabad'}
```

Inside the function, `kwargs` is a dictionary.

---

# 19. Difference Between `*args` and `**kwargs`

| `*args` | `**kwargs` |
|---|---|
| Variable positional arguments | Variable keyword arguments |
| Stored as tuple | Stored as dictionary |
| Uses `*` | Uses `**` |

Example:

```python
def test(*args, **kwargs):
    print(args)
    print(kwargs)

test(10, 20, name="Harsha", age=21)
```

Output:

```text
(10, 20)
{'name': 'Harsha', 'age': 21}
```

---

# 20. Can We Use `*args` and `**kwargs` Together?

Yes.

```python
def display(*args, **kwargs):
    print("Arguments:", args)
    print("Keyword arguments:", kwargs)

display(10, 20, name="Harsha", age=21)
```

Output:

```text
Arguments: (10, 20)
Keyword arguments: {'name': 'Harsha', 'age': 21}
```

---

# 21. What Is Argument Unpacking?

Argument unpacking allows an iterable or dictionary to provide arguments to a function.

### List/Tuple With `*`

```python
def add(a, b, c):
    return a + b + c

numbers = [10, 20, 30]

print(add(*numbers))
```

Output:

```text
60
```

### Dictionary With `**`

```python
def introduce(name, age):
    print(name, age)

data = {
    "name": "Harsha",
    "age": 21
}

introduce(**data)
```

---

# 22. What Is a Positional-Only Parameter?

Python allows parameters to be specified as positional-only using `/`.

```python
def add(a, b, /):
    return a + b
```

This is valid:

```python
add(10, 20)
```

But this is not:

```python
add(a=10, b=20)
```

The `/` indicates that parameters before it must be passed positionally.

---

# 23. What Is a Keyword-Only Parameter?

Parameters after `*` can be made keyword-only.

```python
def introduce(name, *, age):
    print(name, age)
```

Valid:

```python
introduce("Harsha", age=21)
```

Invalid:

```python
introduce("Harsha", 21)
```

### Interview Point

This can make function calls clearer and prevent accidental positional usage.

---

# 24. What Is a Lambda Function?

A lambda is a small anonymous function written using the `lambda` keyword.

```python
square = lambda x: x * x

print(square(5))
```

Output:

```text
25
```

### Syntax

```python
lambda arguments: expression
```

### Interview Answer

> A lambda is a small anonymous function that contains a single expression. It is commonly used for short operations, especially with functions such as `sorted()`, `map()`, and `filter()`.

---

# 25. Can a Lambda Contain Multiple Statements?

A lambda is designed for a single expression, not a normal multi-statement function body.

For complex logic, a regular `def` function is more readable.

---

# 26. What Is a Higher-Order Function?

A higher-order function is a function that:

- Accepts another function as an argument, or
- Returns another function.

Example:

```python
def apply_operation(func, value):
    return func(value)

def square(x):
    return x * x

print(apply_operation(square, 5))
```

Output:

```text
25
```

---

# 27. What Is `map()`?

`map()` applies a function to each item of an iterable.

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x * 2, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6, 8]
```

### Interview Answer

> `map()` applies a function to each element of an iterable and returns an iterator containing the transformed results.

---

# 28. What Is `filter()`?

`filter()` selects elements for which a condition is true.

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda x: x % 2 == 0, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6]
```

### Interview Answer

> `filter()` returns an iterator containing elements for which the supplied function returns a truthy value.

---

# 29. What Is `reduce()`?

`reduce()` repeatedly applies a function to elements of an iterable to produce a single accumulated result.

It is available from `functools`.

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda x, y: x + y, numbers)

print(result)
```

Output:

```text
10
```

### Interview Point

For simple sums, Python's built-in `sum()` is generally clearer:

```python
sum(numbers)
```

---

# 30. Difference Between `map()`, `filter()`, and `reduce()`

| Function | Purpose |
|---|---|
| `map()` | Transform each element |
| `filter()` | Select elements |
| `reduce()` | Combine elements into one result |

Example:

```python
numbers = [1, 2, 3, 4]
```

Transform:

```python
map(lambda x: x * 2, numbers)
```

Filter:

```python
filter(lambda x: x % 2 == 0, numbers)
```

Reduce:

```python
reduce(lambda x, y: x + y, numbers)
```

---

# 31. What Is a Recursive Function?

A recursive function is a function that calls itself.

A recursive function needs a **base case** to stop recursion.

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)

print(factorial(5))
```

Output:

```text
120
```

---

# 32. What Is the Base Case in Recursion?

The base case is the condition that stops recursive calls.

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)
```

Here:

```python
if n == 0:
    return 1
```

is the base case.

Without a suitable base case, recursion can continue until Python raises a recursion-related error.

---

# 33. Recursion vs Iteration

### Recursion

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

### Iteration

```python
def factorial(n):
    result = 1

    for i in range(1, n + 1):
        result *= i

    return result
```

### Interview Answer

> Recursion solves a problem by calling the same function on smaller subproblems, while iteration uses loops. Recursion can make some problems easier to express, but it introduces function-call overhead and uses the call stack.

For simple repetitive tasks, iteration is often preferable in Python.

---

# 34. What Is Variable Scope?

Scope determines where a variable can be accessed.

The commonly discussed Python scopes are:

- Local
- Enclosing
- Global
- Built-in

This is often remembered as the **LEGB rule**.

---

# 35. What Is a Local Variable?

A variable created inside a function is generally local to that function.

```python
def test():
    x = 10
    print(x)

test()
```

`x` is local to `test()`.

Trying to access it outside:

```python
print(x)
```

causes an error because `x` is not defined in that outer scope.

---

# 36. What Is a Global Variable?

A variable defined outside functions is generally global within that module.

```python
x = 10

def test():
    print(x)

test()
```

Output:

```text
10
```

The function can read the global variable.

---

# 37. Can a Function Modify a Global Variable?

To reassign a global variable from inside a function, use the `global` keyword.

```python
x = 10

def update():
    global x
    x = 20

update()

print(x)
```

Output:

```text
20
```

### Important Point

Using global state unnecessarily can make programs harder to understand and test. Passing values through function parameters and returning results is often cleaner.

---

# 38. What Is the `global` Keyword?

`global` tells Python that a variable inside a function refers to a global variable rather than creating a local binding for assignment.

```python
count = 0

def increment():
    global count
    count += 1
```

---

# 39. What Is the `nonlocal` Keyword?

`nonlocal` is used inside a nested function to refer to a variable in the nearest enclosing function scope.

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 1

    inner()

    print(x)

outer()
```

Output:

```text
11
```

### Interview Answer

> `nonlocal` allows a nested function to modify a variable belonging to an enclosing function scope.

---

# 40. What Is the LEGB Rule?

Python searches for names in this order:

```text
L -> Local
E -> Enclosing
G -> Global
B -> Built-in
```

Example:

```python
x = "global"

def outer():
    x = "enclosing"

    def inner():
        x = "local"
        print(x)

    inner()

outer()
```

Output:

```text
local
```

Python first checks the local scope.

---

# 41. What Is a Nested Function?

A function defined inside another function is called a nested function.

```python
def outer():
    def inner():
        print("Inside inner")

    inner()

outer()
```

Nested functions are useful for keeping helper logic close to the function that uses it.

---

# 42. What Is a Closure?

A closure occurs when an inner function remembers and accesses variables from its enclosing function even after the enclosing function has finished executing.

```python
def multiplier(factor):
    def multiply(number):
        return number * factor

    return multiply

double = multiplier(2)

print(double(5))
```

Output:

```text
10
```

The inner function remembers `factor`.

### Interview Answer

> A closure is a function that retains access to variables from its enclosing scope even after the enclosing function has returned.

---

# 43. What Are First-Class Functions?

In Python, functions are first-class objects.

This means functions can be:

- Assigned to variables
- Passed as arguments
- Returned from functions
- Stored in collections

Example:

```python
def greet():
    return "Hello"

message = greet

print(message())
```

Output:

```text
Hello
```

---

# 44. Can a Function Be Stored in a List?

Yes.

```python
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

operations = [add, multiply]

print(operations[0](10, 5))
print(operations[1](10, 5))
```

Output:

```text
15
50
```

---

# 45. What Are Function Annotations?

Function annotations allow us to provide metadata about parameters and return values.

```python
def add(a: int, b: int) -> int:
    return a + b
```

The annotations can improve readability and tooling, but Python does not automatically enforce them as runtime type checks.

### Interview Answer

> Function annotations provide information about expected parameter and return types. They are mainly useful for readability, documentation, IDE support, and static type checking.

---

# 46. What Is a Docstring?

A docstring is a string used to document a function, class, or module.

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

It can be accessed using:

```python
print(add.__doc__)
```

Output:

```text
Return the sum of two numbers.
```

---

# 47. Why Are Docstrings Useful?

They help explain:

- What a function does
- Parameters
- Return value
- Expected behavior
- Important assumptions

This is especially useful in team projects and production code.

---

# 48. What Is a Pure Function?

A pure function generally:

1. Produces the same output for the same input.
2. Does not cause observable side effects.

Example:

```python
def add(a, b):
    return a + b
```

For the same inputs:

```python
add(10, 20)
```

always produces:

```text
30
```

A function that modifies global state or performs external I/O is not purely functional.

---

# 49. What Are Side Effects?

A side effect is an observable change outside the function's returned result.

Examples:

- Modifying a global variable
- Writing to a file
- Updating a database
- Printing to the console
- Making an API request

Example:

```python
def write_data():
    with open("data.txt", "w") as file:
        file.write("Hello")
```

The function changes external state by writing to a file.

---

# 50. What Is Mutable Default Argument Behavior?

This is a very important Python interview question.

Consider:

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(1))
print(add_item(2))
```

Output:

```text
[1]
[1, 2]
```

The default list is created once when the function is defined, not once per function call.

### Safer Approach

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items

print(add_item(1))
print(add_item(2))
```

Output:

```text
[1]
[2]
```

### Interview Answer

> Mutable default arguments such as lists are evaluated once when the function is defined. Therefore, the same object can be reused across calls. Using `None` as the default and creating a new object inside the function avoids this issue.

---

# 51. Are Function Arguments Passed by Value or Reference?

Python's behavior is best described as **call by sharing** or **object reference passing**.

The function receives a reference to the object.

For immutable objects:

```python
def change(x):
    x = x + 1

n = 10

change(n)

print(n)
```

Output:

```text
10
```

The integer object cannot be modified in place.

For mutable objects:

```python
def change(numbers):
    numbers.append(4)

values = [1, 2, 3]

change(values)

print(values)
```

Output:

```text
[1, 2, 3, 4]
```

The function modified the existing list object.

### Interview Answer

> Python uses object-reference semantics, often described as call by sharing. The function receives a reference to the object. Mutating a mutable object can be visible to the caller, while rebinding the local parameter does not rebind the caller's variable.

---

# 52. What Happens When We Reassign a List Parameter?

Consider:

```python
def change(numbers):
    numbers = [100, 200]

values = [1, 2, 3]

change(values)

print(values)
```

Output:

```text
[1, 2, 3]
```

The local parameter is simply rebound to a different list. The caller's variable still refers to the original list.

---

# 53. What Happens When We Mutate a List Parameter?

```python
def change(numbers):
    numbers.append(4)

values = [1, 2, 3]

change(values)

print(values)
```

Output:

```text
[1, 2, 3, 4]
```

The same list object was modified.

---

# 54. What Is Function Overloading in Python?

Python does not support traditional compile-time method/function overloading like some statically typed languages.

You cannot define multiple functions with the same name and expect Python to choose one based on argument types.

```python
def add(a, b):
    return a + b

def add(a, b, c):
    return a + b + c
```

The second definition replaces the first one.

### Common Python Approach

Use default arguments or `*args`.

```python
def add(*args):
    return sum(args)

print(add(10, 20))
print(add(10, 20, 30))
```

---

# 55. What Is Function Overriding?

Function or method overriding is mainly discussed in object-oriented programming.

A child class can provide its own implementation of a method inherited from a parent class.

```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def show(self):
        print("Child")

obj = Child()
obj.show()
```

Output:

```text
Child
```

This topic is more closely related to OOP and should be studied in the OOP section as well.

---

# 56. What Is a Decorator?

A decorator is a function that modifies or extends the behavior of another function without changing its source code.

Basic example:

```python
def decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")

    return wrapper

@decorator
def greet():
    print("Hello")

greet()
```

Output:

```text
Before function
Hello
After function
```

### Interview Answer

> A decorator is a callable that takes another function and returns a modified or enhanced callable. It is commonly used for logging, authentication, timing, validation, and other cross-cutting concerns.

---

# 57. What Does `@decorator` Mean?

This:

```python
@decorator
def greet():
    print("Hello")
```

is essentially equivalent to:

```python
def greet():
    print("Hello")

greet = decorator(greet)
```

The decorator replaces the original function reference with the returned wrapper or callable.

---

# 58. Why Is `functools.wraps` Used in Decorators?

Consider:

```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

`wraps` preserves important metadata of the original function, such as its name and docstring.

Without it, introspection may show the wrapper's metadata instead.

---

# 59. How Do You Create a Decorator That Accepts Arguments?

A decorator with arguments generally needs another level of nesting.

```python
from functools import wraps

def repeat(times):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result

        return wrapper

    return decorator

@repeat(3)
def greet():
    print("Hello")

greet()
```

Output:

```text
Hello
Hello
Hello
```

---

# 60. Real-World Example of a Decorator

Suppose an API application needs logging.

Instead of writing logging code inside every endpoint, a decorator can be used.

```python
from functools import wraps

def log_call(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Calling:", func.__name__)
        result = func(*args, **kwargs)
        print("Completed:", func.__name__)
        return result

    return wrapper

@log_call
def process_data():
    return "Data processed"

print(process_data())
```

### Interview Explanation

> A decorator is useful when the same additional behavior needs to be applied to multiple functions, such as logging, authentication, timing, validation, or error handling.

---

# 61. What Is a Function That Takes Another Function as an Argument?

Example:

```python
def execute(func, value):
    return func(value)

def square(x):
    return x * x

print(execute(square, 5))
```

Output:

```text
25
```

Here `execute()` is a higher-order function because it accepts another function.

---

# 62. What Is a Function That Returns Another Function?

```python
def multiplier(factor):
    def multiply(number):
        return number * factor

    return multiply

double = multiplier(2)

print(double(10))
```

Output:

```text
20
```

This is also related to closures.

---

# 63. What Is a Nested Scope?

A nested scope occurs when functions are defined inside other functions.

```python
def outer():
    x = 10

    def inner():
        print(x)

    inner()

outer()
```

The inner function can access `x` from the enclosing function scope.

---

# 64. What Is the Difference Between Local and Global Variables?

```python
x = 100

def test():
    x = 10
    print(x)

test()

print(x)
```

Output:

```text
10
100
```

The local `x` does not change the global `x`.

---

# 65. Can a Function Call Another Function?

Yes.

```python
def square(x):
    return x * x

def calculate(x):
    return square(x) + 10

print(calculate(5))
```

Output:

```text
35
```

Functions can be composed to build larger operations from smaller reusable pieces.

---

# 66. Can a Function Call Itself?

Yes. This is recursion.

```python
def countdown(n):
    if n == 0:
        return

    print(n)
    countdown(n - 1)

countdown(3)
```

Output:

```text
3
2
1
```

---

# 67. What Is the Function Call Stack?

When a function is called, Python keeps track of the active function call and its local state.

For recursive calls, multiple function-call frames can accumulate.

Example:

```python
def countdown(n):
    if n == 0:
        return

    countdown(n - 1)
```

For:

```python
countdown(3)
```

conceptually:

```text
countdown(3)
    -> countdown(2)
        -> countdown(1)
            -> countdown(0)
```

After reaching the base case, the calls return back up.

---

# 68. What Is Recursion Depth?

Python limits recursion depth to prevent uncontrolled growth of the call stack.

Deep recursion can result in:

```text
RecursionError
```

For many straightforward repetitive operations, an iterative solution may be more appropriate.

---

# 69. What Is the Difference Between a Function and a Method?

A function is a callable defined independently.

```python
def greet():
    print("Hello")
```

A method is a function associated with an object or class.

```python
class Person:
    def greet(self):
        print("Hello")
```

Then:

```python
person = Person()
person.greet()
```

### Interview Answer

> A function can exist independently, while a method is a function associated with an object or class and is typically called through that object or class.

---

# 70. What Is a Built-in Function?

Python provides many functions that are available without defining them ourselves.

Examples:

```python
len()
print()
type()
sum()
max()
min()
range()
enumerate()
zip()
```

Example:

```python
numbers = [10, 20, 30]

print(len(numbers))
print(sum(numbers))
```

Output:

```text
3
60
```

---

# 71. What Is a User-Defined Function?

A function created by the programmer is called a user-defined function.

```python
def calculate_total(price, quantity):
    return price * quantity
```

This is a user-defined function.

---

# 72. What Are Anonymous Functions?

An anonymous function is a function without a conventional name.

Python commonly creates anonymous functions using `lambda`.

```python
square = lambda x: x * x
```

---

# 73. What Is the Difference Between `lambda` and `def`?

| `lambda` | `def` |
|---|---|
| Usually anonymous | Named function |
| Single expression | Can contain multiple statements |
| Useful for short operations | Better for complex logic |
| Often used inline | Better for reusable functions |

Example:

```python
square = lambda x: x * x
```

Equivalent regular function:

```python
def square(x):
    return x * x
```

For complex code, `def` is generally clearer.

---

# 74. What Is a Function Signature?

A function signature describes the parameters accepted by a function.

Example:

```python
def add(a, b=0, *args, **kwargs):
    pass
```

The signature includes the parameter structure and their kinds.

Python's `inspect` module can be used to inspect signatures:

```python
import inspect

def add(a, b=0):
    return a + b

print(inspect.signature(add))
```

---

# 75. What Is Argument Validation?

Argument validation means checking whether input values satisfy expected requirements.

```python
def divide(a, b):
    if b == 0:
        raise ValueError("b cannot be zero")

    return a / b

print(divide(10, 2))
```

If:

```python
divide(10, 0)
```

is called, the function raises an appropriate error instead of performing invalid division.

---

# 76. What Is Exception Handling Inside a Function?

A function can catch exceptions or allow them to propagate to the caller.

```python
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return None

print(divide(10, 0))
```

Output:

```text
None
```

In larger applications, whether the function should handle or propagate an exception depends on where the error can be meaningfully handled.

---

# 77. Should Every Function Handle Its Own Exceptions?

No.

It depends on the responsibility of the function.

If a lower-level function cannot meaningfully recover from an error, it may be better to let the exception propagate to a higher-level layer that can handle it appropriately.

### Interview Answer

> I don't catch every exception blindly. I handle an exception at the layer where I can take meaningful action, and otherwise allow it to propagate so that higher-level code can handle it.

---

# 78. How Can Functions Improve Code Design?

A good function should ideally have a clear responsibility.

Instead of:

```python
def process_everything():
    # read data
    # validate data
    # transform data
    # save data
    # send email
```

we can separate responsibilities:

```python
def read_data():
    pass

def validate_data(data):
    pass

def transform_data(data):
    pass

def save_data(data):
    pass
```

This makes the code easier to test and maintain.

---

# 79. Real-World Data Engineering Example

A simplified ETL pipeline can be separated into functions:

```python
def extract_data():
    return [
        {"name": "Harsha", "amount": 1000},
        {"name": "Ravi", "amount": 2000}
    ]


def transform_data(records):
    transformed = []

    for record in records:
        transformed.append({
            "name": record["name"],
            "amount": record["amount"] * 1.18
        })

    return transformed


def load_data(records):
    print("Loading:", records)


data = extract_data()
transformed_data = transform_data(data)
load_data(transformed_data)
```

### Interview Explanation

> Functions help separate the extract, transform, and load responsibilities. This makes each stage easier to understand, test, modify, and reuse.

---

# 80. Real-World Full-Stack Example

In a backend application, functions can separate responsibilities such as:

```python
def validate_user(data):
    pass


def create_user(data):
    pass


def save_user(user):
    pass


def get_user(user_id):
    pass
```

This keeps validation, business logic, persistence, and retrieval separate rather than putting everything inside one large function.

---

# 81. What Makes a Good Function?

A good function generally has:

- Clear purpose
- Meaningful name
- Appropriate parameters
- Clear return behavior
- Limited responsibility
- Minimal unnecessary side effects
- Good error handling
- Useful documentation when needed

### Interview Answer

> I try to design functions with a clear responsibility, meaningful names, predictable inputs and outputs, and minimal unnecessary side effects. This makes them easier to test and maintain.

---

# 82. Should a Function Always Return Something?

No.

Some functions intentionally perform an action and do not need to return a meaningful value.

```python
def log_message(message):
    print(message)
```

It implicitly returns `None`.

Other functions should return values when the caller needs their result.

```python
def calculate_total(price, quantity):
    return price * quantity
```

---

# 83. What Is a Function With Side Effects?

Example:

```python
total = 0

def add(value):
    global total
    total += value
```

The function changes external state.

Another example:

```python
def save_data(data):
    with open("data.txt", "w") as file:
        file.write(data)
```

It changes the file system.

---

# 84. What Is Function Composition?

Function composition means using the output of one function as the input of another.

```python
def square(x):
    return x * x

def add_ten(x):
    return x + 10

result = add_ten(square(5))

print(result)
```

Output:

```text
35
```

First:

```text
square(5) -> 25
```

Then:

```text
add_ten(25) -> 35
```

---

# 85. Important Output Question

```python
def test():
    print("Hello")

result = test()

print(result)
```

### Answer

```text
Hello
None
```

The function prints `"Hello"` but does not return a value.

---

# 86. Important Output Question

```python
def test():
    return 10
    print("Hello")

print(test())
```

### Answer

```text
10
```

The statement after `return` is not executed.

---

# 87. Important Output Question

```python
def add(a, b=10):
    return a + b

print(add(5))
print(add(5, 20))
```

### Answer

```text
15
25
```

---

# 88. Important Output Question

```python
def test(*args):
    print(args)

test(1, 2, 3)
```

### Answer

```text
(1, 2, 3)
```

`args` is a tuple.

---

# 89. Important Output Question

```python
def test(**kwargs):
    print(kwargs)

test(name="Harsha", age=21)
```

### Answer

```text
{'name': 'Harsha', 'age': 21}
```

`kwargs` is a dictionary.

---

# 90. Important Output Question

```python
x = 10

def test():
    x = 20
    print(x)

test()
print(x)
```

### Answer

```text
20
10
```

The local variable does not change the global variable.

---

# 91. Important Output Question

```python
x = 10

def test():
    global x
    x = 20

test()

print(x)
```

### Answer

```text
20
```

The `global` keyword allows the function to reassign the global variable.

---

# 92. Important Output Question

```python
def outer():
    x = 10

    def inner():
        print(x)

    inner()

outer()
```

### Answer

```text
10
```

The inner function can access the enclosing function's variable.

---

# 93. Important Output Question

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 5

    inner()

    print(x)

outer()
```

### Answer

```text
15
```

`nonlocal` allows the nested function to modify the enclosing function's variable.

---

# 94. Important Output Question

```python
def add(a, b):
    return a + b

operation = add

print(operation(10, 20))
```

### Answer

```text
30
```

Functions are first-class objects and can be assigned to variables.

---

# 95. Important Output Question

```python
def calculate(func, value):
    return func(value)

def square(x):
    return x * x

print(calculate(square, 5))
```

### Answer

```text
25
```

The function `square` is passed as an argument.

---

# 96. Important Output Question

```python
square = lambda x: x * x

print(square(4))
```

### Answer

```text
16
```

---

# 97. Important Output Question

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(list(result))
```

### Answer

```text
[2, 4, 6]
```

---

# 98. Important Output Question

```python
numbers = [1, 2, 3, 4]

result = filter(lambda x: x % 2 == 0, numbers)

print(list(result))
```

### Answer

```text
[2, 4]
```

---

# 99. Important Output Question

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n - 1)

print(factorial(4))
```

### Answer

```text
24
```

---

# 100. Important Output Question — Mutable Default Argument

```python
def add_item(item, items=[]):
    items.append(item)
    return items

print(add_item(1))
print(add_item(2))
```

### Answer

```text
[1]
[1, 2]
```

The same default list is reused.

---

# 101. Important Output Question — Mutation vs Reassignment

```python
def change(data):
    data.append(4)

numbers = [1, 2, 3]

change(numbers)

print(numbers)
```

### Answer

```text
[1, 2, 3, 4]
```

The original list was mutated.

---

# 102. Important Output Question — Reassignment

```python
def change(data):
    data = [100, 200]

numbers = [1, 2, 3]

change(numbers)

print(numbers)
```

### Answer

```text
[1, 2, 3]
```

The local parameter was rebound; the caller's variable still refers to the original list.

---

# 103. Important Interview Questions to Master

Before a Python placement interview, make sure you can confidently answer:

1. What is a function?
2. Why do we use functions?
3. How do you define a function?
4. How do you call a function?
5. What are parameters?
6. What are arguments?
7. Difference between parameters and arguments.
8. What is `return`?
9. What happens if a function has no return?
10. Difference between `print()` and `return`.
11. Can a function return multiple values?
12. Can a function return a list or dictionary?
13. What are default arguments?
14. What are positional arguments?
15. What are keyword arguments?
16. Difference between positional and keyword arguments.
17. Can positional and keyword arguments be mixed?
18. What are `*args`?
19. What are `**kwargs`?
20. Difference between `*args` and `**kwargs`.
21. What is argument unpacking?
22. What does `*` do during function calls?
23. What does `**` do during function calls?
24. What are positional-only parameters?
25. What are keyword-only parameters?
26. What is a lambda function?
27. Difference between `lambda` and `def`.
28. What is a higher-order function?
29. What is `map()`?
30. What is `filter()`?
31. What is `reduce()`?
32. Difference between `map()`, `filter()`, and `reduce()`.
33. What is recursion?
34. What is a base case?
35. Recursion vs iteration.
36. What is local scope?
37. What is global scope?
38. What is the `global` keyword?
39. What is the `nonlocal` keyword?
40. What is the LEGB rule?
41. What is a nested function?
42. What is a closure?
43. What are first-class functions?
44. Can functions be stored in variables?
45. Can functions be passed as arguments?
46. Can functions return functions?
47. What are function annotations?
48. What is a docstring?
49. What is a pure function?
50. What are side effects?
51. What is a mutable default argument problem?
52. How do you avoid mutable default arguments?
53. How are arguments passed in Python?
54. Difference between mutation and reassignment.
55. What is function overloading?
56. Does Python support traditional function overloading?
57. What is function/method overriding?
58. What is a decorator?
59. What does `@decorator` mean?
60. Why use `functools.wraps`?
61. What is a decorator with arguments?
62. What is a function signature?
63. What is argument validation?
64. How should exceptions be handled inside functions?
65. What makes a function well designed?
66. Difference between a function and a method.
67. What is a built-in function?
68. What is a user-defined function?
69. What is function composition?
70. How are functions useful in ETL pipelines?
71. How are functions useful in backend development?
72. How do functions improve testing and maintainability?
73. Predict the output of functions using local/global variables.
74. Predict the output of `*args` and `**kwargs`.
75. Predict the output of recursive functions.
76. Predict the output of mutable default arguments.
77. Predict the output of `map()` and `filter()`.
78. Predict the output of closures.
79. Explain a decorator with a practical example.
80. Explain how you would divide a real-world project into reusable functions.

---

# 104. Final Quick Revision

```text
def
    -> Defines a function

()
    -> Calls a function

parameter
    -> Variable in function definition

argument
    -> Actual value passed to a function

return
    -> Sends a result back to the caller

*args
    -> Variable positional arguments
    -> Tuple inside the function

**kwargs
    -> Variable keyword arguments
    -> Dictionary inside the function

lambda
    -> Small anonymous function

map()
    -> Transform elements

filter()
    -> Select elements

reduce()
    -> Combine elements into one result

recursion
    -> Function calls itself

global
    -> Refers to a global variable

nonlocal
    -> Refers to an enclosing function variable

LEGB
    -> Local -> Enclosing -> Global -> Built-in

closure
    -> Inner function remembers enclosing scope

decorator
    -> Extends/modifies function behavior

docstring
    -> Documents a function

generator
    -> Produces values lazily

mutable default argument
    -> Default object is reused across calls
```

# Final Interview-Level Understanding

> **A strong understanding of Python functions means knowing much more than how to write `def`. You should understand parameters and arguments, positional and keyword arguments, default arguments, `*args` and `**kwargs`, return values, scope and LEGB, closures, recursion, lambda functions, higher-order functions, `map()`, `filter()`, `reduce()`, decorators, function annotations, docstrings, mutable default arguments, argument passing, mutation vs reassignment, and function design. For placement interviews, you should also be able to explain how functions help separate responsibilities in real-world applications such as ETL pipelines, APIs, backend applications, validation, logging, and data processing.**