# 19 — Decorators

## 1. What Is a Decorator?

A **decorator** is a function that modifies or extends the behavior of another function or class **without changing its original source code**.

A decorator takes a function, adds some behavior around it, and returns a new function.

The basic idea is:

```text
Original Function
       ↓
   Decorator
       ↓
Enhanced Function
```

Decorators are commonly used for:

- logging
- authentication
- authorization
- timing
- validation
- caching
- access control
- transaction handling
- debugging

---

# 2. Why Do We Need Decorators?

Suppose we have several functions:

```python
def add(a, b):
    print("Function started")
    return a + b

def subtract(a, b):
    print("Function started")
    return a - b
```

If many functions need the same additional behavior, repeating the code is not ideal.

Instead, we can create one decorator:

```python
def log_call(func):
    def wrapper(*args, **kwargs):
        print("Function started")
        return func(*args, **kwargs)

    return wrapper
```

Then:

```python
@log_call
def add(a, b):
    return a + b
```

Now the logging behavior is added without modifying the actual `add()` implementation.

---

# 3. Basic Decorator Syntax

```python
def decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")

    return wrapper
```

Apply it:

```python
@decorator
def greet():
    print("Hello")
```

Call:

```python
greet()
```

Output:

```text
Before function
Hello
After function
```

---

# 4. What Does `@decorator` Mean?

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

This is one of the most important decorator concepts for interviews.

### Interview Answer

> The `@decorator` syntax is syntactic sugar for passing the function to the decorator and assigning the returned function back to the original function name.

---

# 5. How Does a Decorator Work?

Consider:

```python
def decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")

    return wrapper
```

and:

```python
@decorator
def greet():
    print("Hello")
```

The process is conceptually:

```text
greet function created
        ↓
decorator(greet)
        ↓
wrapper returned
        ↓
greet now refers to wrapper
        ↓
greet()
        ↓
wrapper executes
        ↓
original greet executes
```

---

# 6. Simple Decorator Example

```python
def my_decorator(func):
    def wrapper():
        print("Starting function")
        func()
        print("Function completed")

    return wrapper


@my_decorator
def greet():
    print("Hello, Harsha")


greet()
```

Output:

```text
Starting function
Hello, Harsha
Function completed
```

---

# 7. Decorator With Function Arguments

A decorator should often work with functions that accept arguments.

Example:

```python
def decorator(func):
    def wrapper(a, b):
        print("Before")
        result = func(a, b)
        print("After")
        return result

    return wrapper


@decorator
def add(a, b):
    return a + b


print(add(10, 20))
```

Output:

```text
Before
After
30
```

---

# 8. Why Do We Use `*args` and `**kwargs` in Decorators?

A general-purpose decorator should be able to wrap functions with different argument patterns.

For example:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function")

        result = func(*args, **kwargs)

        print("After function")

        return result

    return wrapper
```

Now it can work with:

```python
@decorator
def greet(name):
    return f"Hello {name}"
```

and:

```python
@decorator
def add(a, b):
    return a + b
```

and functions using keyword arguments.

### Interview Answer

> `*args` and `**kwargs` make a decorator flexible because the wrapper can accept arbitrary positional and keyword arguments and pass them to the original function.

---

# 9. General-Purpose Decorator

```python
def log_function(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")

        result = func(*args, **kwargs)

        print(f"Finished {func.__name__}")

        return result

    return wrapper
```

Usage:

```python
@log_function
def add(a, b):
    return a + b


@log_function
def greet(name):
    return f"Hello {name}"


print(add(10, 20))
print(greet("Harsha"))
```

---

# 10. Why Should a Decorator Return the Function Result?

Consider:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        func(*args, **kwargs)

    return wrapper
```

If the original function returns something:

```python
@decorator
def add(a, b):
    return a + b
```

then:

```python
print(add(10, 20))
```

would print:

```text
None
```

because the wrapper did not return the original result.

Correct:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result

    return wrapper
```

Or simply:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

---

# 11. What Is a Wrapper Function?

The inner function inside a decorator is commonly called a **wrapper**.

Example:

```python
def decorator(func):

    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result

    return wrapper
```

Here:

```text
decorator → receives original function
wrapper   → adds behavior
func      → original function
```

---

# 12. Decorator for Execution Time

A common real-world use case is measuring how long a function takes.

```python
import time


def timer(func):
    def wrapper(*args, **kwargs):
        start = time.perf_counter()

        result = func(*args, **kwargs)

        end = time.perf_counter()

        print("Execution time:", end - start)

        return result

    return wrapper
```

Usage:

```python
@timer
def calculate():
    total = 0

    for i in range(1000000):
        total += i

    return total


print(calculate())
```

The decorator adds timing behavior without changing `calculate()`.

---

# 13. Decorator for Logging

```python
def log_call(func):
    def wrapper(*args, **kwargs):
        print("Calling:", func.__name__)

        result = func(*args, **kwargs)

        print("Returned:", result)

        return result

    return wrapper
```

Usage:

```python
@log_call
def multiply(a, b):
    return a * b


print(multiply(5, 4))
```

Output:

```text
Calling: multiply
Returned: 20
20
```

---

# 14. Decorator for Authentication

Decorators are very common in web applications.

Conceptually:

```python
def login_required(func):
    def wrapper(user, *args, **kwargs):

        if not user.is_authenticated:
            return "Access denied"

        return func(user, *args, **kwargs)

    return wrapper
```

Usage:

```python
@login_required
def dashboard(user):
    return "Welcome to dashboard"
```

The decorator can check authentication before allowing the function to execute.

This pattern is common in web frameworks.

---

# 15. Decorator for Authorization

Authentication asks:

```text
Who are you?
```

Authorization asks:

```text
Are you allowed to perform this action?
```

Example:

```python
def admin_required(func):
    def wrapper(user, *args, **kwargs):

        if user.role != "admin":
            return "Permission denied"

        return func(user, *args, **kwargs)

    return wrapper
```

Usage:

```python
@admin_required
def delete_user(user, user_id):
    return f"User {user_id} deleted"
```

---

# 16. Decorator for Validation

A decorator can validate input before calling a function.

```python
def positive_only(func):
    def wrapper(n):
        if n <= 0:
            raise ValueError("Number must be positive")

        return func(n)

    return wrapper
```

Usage:

```python
@positive_only
def square(n):
    return n * n


print(square(5))
```

Output:

```text
25
```

But:

```python
square(-5)
```

raises:

```text
ValueError
```

---

# 17. Decorator for Caching

Caching is another important use case.

Python provides:

```python
from functools import lru_cache
```

Example:

```python
from functools import lru_cache


@lru_cache
def expensive_operation(n):
    print("Calculating...")
    return n * n


print(expensive_operation(10))
print(expensive_operation(10))
```

The second call can reuse the cached result instead of recalculating it.

---

# 18. What Is `functools.wraps`?

When a decorator wraps a function, the wrapper can replace important metadata of the original function.

Example:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

Then:

```python
@decorator
def greet():
    """Greets the user."""
    print("Hello")
```

Without preserving metadata:

```python
print(greet.__name__)
```

may give:

```text
wrapper
```

instead of:

```text
greet
```

We can use:

```python
from functools import wraps
```

---

# 19. Using `functools.wraps`

```python
from functools import wraps


def decorator(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

Now:

```python
@decorator
def greet():
    """Greets the user."""
    print("Hello")


print(greet.__name__)
print(greet.__doc__)
```

Output:

```text
greet
Greets the user.
```

### Interview Answer

> `functools.wraps` preserves important metadata of the original function, such as its name and docstring, when it is wrapped by a decorator.

---

# 20. Why Is `functools.wraps` Important?

Without:

```python
@wraps(func)
```

the wrapper can make debugging and introspection confusing because:

```python
function.__name__
function.__doc__
```

may describe the wrapper rather than the original function.

Using `wraps` preserves the original function's metadata.

---

# 21. Decorator With Arguments

Sometimes we want to configure a decorator.

For example:

```python
@repeat(3)
def greet():
    print("Hello")
```

Here:

```python
repeat(3)
```

is not directly receiving the function.

It first receives the decorator configuration.

Example:

```python
def repeat(times):

    def decorator(func):

        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator
```

Usage:

```python
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

# 22. Structure of a Decorator With Arguments

There are three levels:

```text
repeat(times)
      ↓
decorator(func)
      ↓
wrapper(*args, **kwargs)
```

Example:

```python
def repeat(times):

    def decorator(func):

        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator
```

This is an important interview coding pattern.

---

# 23. Multiple Decorators

Python allows multiple decorators:

```python
@decorator1
@decorator2
def greet():
    print("Hello")
```

This is conceptually equivalent to:

```python
greet = decorator1(decorator2(greet))
```

So the decorator closest to the function is applied first.

---

# 24. Example of Multiple Decorators

```python
def decorator1(func):
    def wrapper():
        print("Decorator 1 before")
        func()
        print("Decorator 1 after")

    return wrapper


def decorator2(func):
    def wrapper():
        print("Decorator 2 before")
        func()
        print("Decorator 2 after")

    return wrapper


@decorator1
@decorator2
def greet():
    print("Hello")


greet()
```

Conceptually:

```text
decorator2(greet)
        ↓
decorator1(result)
        ↓
final greet
```

---

# 25. Decorators and Closures

Decorators commonly rely on **closures**.

Example:

```python
def decorator(func):

    def wrapper():
        print("Before")
        func()
        print("After")

    return wrapper
```

The `wrapper()` function remembers the `func` variable from the enclosing `decorator()` function.

This is possible because of Python's closure behavior.

### Interview Connection

If an interviewer asks:

> How does the wrapper remember the original function?

A strong answer is:

> The wrapper forms a closure over the `func` variable from the enclosing decorator function, so it can access the original function even after the outer decorator function has returned.

---

# 26. Decorators Are Possible Because Functions Are First-Class Objects

Python functions can be:

- assigned to variables
- passed as arguments
- returned from functions
- stored in data structures

Example:

```python
def greet():
    print("Hello")


x = greet

x()
```

Output:

```text
Hello
```

Because functions can be passed around, decorators can receive a function and return another function.

---

# 27. Passing a Function to Another Function

```python
def greet():
    print("Hello")


def execute(func):
    func()


execute(greet)
```

Output:

```text
Hello
```

This concept is fundamental to understanding decorators.

---

# 28. Returning a Function

```python
def outer():

    def inner():
        print("Hello")

    return inner


func = outer()

func()
```

Output:

```text
Hello
```

Decorators combine these ideas:

```text
receive function
      ↓
create wrapper
      ↓
return wrapper
```

---

# 29. Function Decorator vs Class Decorator

A decorator can be implemented using:

- a function
- a class

Most simple decorators use functions.

Example function decorator:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        return func(*args, **kwargs)

    return wrapper
```

A class can also implement decorator behavior using `__call__`.

Example:

```python
class Decorator:

    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("Before")
        return self.func(*args, **kwargs)
```

Usage:

```python
@Decorator
def greet():
    print("Hello")


greet()
```

---

# 30. What Is a Callable?

An object is **callable** if it can be invoked using:

```python
()
```

Functions are callable.

Classes are callable.

Objects can also be made callable by implementing:

```python
__call__
```

Example:

```python
class Greeter:

    def __call__(self):
        print("Hello")


g = Greeter()

g()
```

Output:

```text
Hello
```

This is why class-based decorators can work.

---

# 31. Built-in Decorators

Python provides several important decorators.

Examples:

```python
@property
@staticmethod
@classmethod
```

These are frequently asked in Python interviews.

---

# 32. `@staticmethod`

A static method does not receive an automatic instance (`self`) or class (`cls`) argument.

Example:

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

Output:

```text
30
```

Use it when the method logically belongs to the class but does not need instance or class state.

---

# 33. `@classmethod`

A class method receives the class as the first argument, conventionally called:

```python
cls
```

Example:

```python
class Student:

    school = "ABC School"

    @classmethod
    def get_school(cls):
        return cls.school


print(Student.get_school())
```

Output:

```text
ABC School
```

---

# 34. `@property`

`@property` allows a method to be accessed like an attribute.

Example:

```python
class Person:

    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name


person = Person("Harsha")

print(person.name)
```

Notice that we use:

```python
person.name
```

rather than:

```python
person.name()
```

---

# 35. Why Is `@property` Useful?

It allows us to provide method logic while keeping attribute-like syntax.

For example:

```python
class Rectangle:

    def __init__(self, width, height):
        self.width = width
        self.height = height

    @property
    def area(self):
        return self.width * self.height


r = Rectangle(10, 5)

print(r.area)
```

Output:

```text
50
```

---

# 36. `@property` With Setter

```python
class Person:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")

        self._age = value


person = Person(20)

print(person.age)

person.age = 25

print(person.age)
```

Output:

```text
20
25
```

The setter allows validation when assigning the property.

---

# 37. Important Difference Between `staticmethod` and `classmethod`

| `staticmethod` | `classmethod` |
|---|---|
| Does not receive `self` or `cls` automatically | Receives `cls` automatically |
| Cannot directly access instance state through `self` | Can access class state through `cls` |
| Useful for utility behavior related to the class | Useful for class-level behavior |
| Called using class or instance | Commonly called using class |

Example:

```python
class Example:

    @staticmethod
    def add(a, b):
        return a + b

    @classmethod
    def create(cls):
        return cls()
```

---

# 38. Important Interview Question — Are Decorators Only Used With Functions?

No.

Decorators can also be used with classes.

Example:

```python
def add_feature(cls):
    cls.category = "Python"
    return cls


@add_feature
class Student:
    pass


print(Student.category)
```

Output:

```text
Python
```

---

# 39. Class Decorator Example

```python
def add_greeting(cls):

    def greet(self):
        return "Hello"

    cls.greet = greet

    return cls


@add_greeting
class Person:
    pass


p = Person()

print(p.greet())
```

Output:

```text
Hello
```

A class decorator receives the class object and can modify or replace it.

---

# 40. Decorator Execution vs Function Execution

Consider:

```python
def decorator(func):
    print("Decorator executed")

    def wrapper():
        print("Wrapper executed")
        func()

    return wrapper


@decorator
def greet():
    print("Hello")


print("Before calling")
greet()
```

Output:

```text
Decorator executed
Before calling
Wrapper executed
Hello
```

Important:

```text
Decorator execution
```

happens when the function is defined/decorated, while:

```text
Wrapper execution
```

happens when the decorated function is called.

---

# 41. Important Interview Question — When Does a Decorator Execute?

A strong answer:

> The decorator expression is applied when the decorated function or class is created, while the wrapper's runtime behavior occurs when the decorated object is called.

Example:

```python
@decorator
def greet():
    pass
```

The decorator is applied during definition/import time, not each time `greet()` is called.

---

# 42. Decorators Can Modify Return Values

```python
def double_result(func):

    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result * 2

    return wrapper


@double_result
def add(a, b):
    return a + b


print(add(5, 10))
```

Output:

```text
30
```

The original function returns:

```text
15
```

The decorator changes the returned result to:

```text
30
```

---

# 43. Decorators Can Prevent Function Execution

```python
def block(func):

    def wrapper(*args, **kwargs):
        print("Function blocked")

    return wrapper


@block
def delete_data():
    print("Deleting data")


delete_data()
```

Output:

```text
Function blocked
```

The original function is never called.

---

# 44. Decorators Can Handle Exceptions

A decorator can provide common exception handling.

```python
def handle_errors(func):

    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except Exception as e:
            print("Error:", e)
            return None

    return wrapper
```

Usage:

```python
@handle_errors
def divide(a, b):
    return a / b


print(divide(10, 0))
```

Output:

```text
Error: division by zero
None
```

In production code, exception handling should be specific and should not blindly hide unexpected failures.

---

# 45. Decorators and Separation of Concerns

One of the biggest advantages of decorators is **separation of concerns**.

Suppose a function handles business logic:

```python
def process_payment():
    ...
```

We may separately need:

```text
logging
authentication
authorization
timing
error handling
```

Instead of mixing all these concerns into the business logic, decorators can handle cross-cutting behavior.

Conceptually:

```text
Authentication
      ↓
Logging
      ↓
Timing
      ↓
Business Logic
```

---

# 46. Real-World Example — API Authentication

In a backend application, we may have:

```python
@authenticate
def get_user_profile(user):
    ...
```

The authentication decorator can check whether the user is logged in before allowing the endpoint logic to run.

The function itself can focus on:

```text
Get user profile
```

instead of repeatedly implementing authentication checks.

---

# 47. Real-World Example — Logging

Suppose an application has:

```python
create_user()
update_user()
delete_user()
```

Instead of writing logging code inside every function:

```python
@log_call
def create_user():
    ...


@log_call
def update_user():
    ...


@log_call
def delete_user():
    ...
```

The common logging behavior is centralized.

---

# 48. Real-World Example — Performance Monitoring

Suppose a data-processing function is slow:

```python
@timer
def process_large_dataset(data):
    ...
```

The decorator can measure execution time without modifying the processing logic.

This is useful when debugging or monitoring performance.

---

# 49. Real-World Example — Data Engineering

Suppose an ETL pipeline has:

```python
@log_call
def extract():
    ...


@timer
def transform(data):
    ...


@validate_output
def load(data):
    ...
```

Decorators can keep cross-cutting concerns such as:

```text
logging
timing
validation
```

separate from the main ETL logic.

---

# 50. Decorator vs Normal Function

A normal function:

```python
def add(a, b):
    return a + b
```

A decorator:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        return func(*args, **kwargs)

    return wrapper
```

A decorator is specifically designed to accept a callable and modify/extend its behavior.

---

# 51. Important Interview Question — What Are the Advantages of Decorators?

### Strong Answer

> Decorators allow us to add reusable behavior without modifying the original function. They reduce code duplication and help separate cross-cutting concerns such as logging, authentication, authorization, timing, caching, and validation from the core business logic.

---

# 52. Important Interview Question — What Are the Disadvantages of Decorators?

Decorators are powerful, but overusing them can make code harder to understand.

Possible disadvantages:

- debugging can become harder
- multiple decorators can make execution flow less obvious
- poorly written decorators can hide function metadata
- complex decorators can be difficult to maintain
- decorator ordering can affect behavior

### Interview Answer

> Decorators improve reuse and separation of concerns, but excessive or complex use can make the execution flow harder to understand and debug.

---

# 53. Important Interview Question — What Is the Difference Between a Decorator and a Wrapper?

A **decorator** is the function that receives the original function and returns an enhanced callable.

A **wrapper** is usually the inner function that actually surrounds the original function call.

Example:

```python
def decorator(func):          # decorator

    def wrapper(*args):       # wrapper
        print("Before")
        return func(*args)

    return wrapper
```

---

# 54. Important Interview Question — Why Are `*args` and `**kwargs` Used?

### Strong Answer

> They allow the wrapper to accept arbitrary positional and keyword arguments, making the decorator reusable with functions that have different signatures.

Example:

```python
def decorator(func):

    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper
```

---

# 55. Important Interview Question — Why Use `functools.wraps`?

### Strong Answer

> `functools.wraps` preserves metadata of the original function, such as its name and docstring, when it is wrapped. Without it, tools such as debugging and introspection may see the wrapper's metadata instead.

---

# 56. Important Interview Question — What Is a Decorator With Arguments?

A decorator with arguments is a decorator factory.

Example:

```python
def repeat(times):

    def decorator(func):

        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)

        return wrapper

    return decorator
```

Usage:

```python
@repeat(3)
def greet():
    print("Hello")
```

There are three nested levels because:

```text
repeat()
   ↓
decorator()
   ↓
wrapper()
```

---

# 57. Important Interview Question — What Happens With Multiple Decorators?

Example:

```python
@A
@B
def func():
    pass
```

is equivalent to:

```python
func = A(B(func))
```

Therefore, `B` is applied to `func` first, and then `A` is applied to the result.

---

# 58. Important Interview Question — Can a Decorator Change Function Behavior?

Yes.

A decorator can:

- execute code before the function
- execute code after the function
- modify arguments
- modify return values
- prevent execution
- catch exceptions
- add logging
- enforce permissions
- cache results

Example:

```python
def double_result(func):

    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) * 2

    return wrapper
```

---

# 59. Important Interview Question — Can Decorators Be Used on Classes?

Yes.

Example:

```python
def add_attribute(cls):
    cls.category = "Python"
    return cls


@add_attribute
class Student:
    pass


print(Student.category)
```

Output:

```text
Python
```

---

# 60. Important Interview Question — Why Are Functions Called First-Class Objects?

Functions are first-class objects because they can be:

```text
assigned to variables
passed as arguments
returned from functions
stored in collections
```

Example:

```python
def greet():
    return "Hello"


func = greet

print(func())
```

This behavior makes decorators possible.

---

# 61. Coding Interview Question — Write a Logging Decorator

### Question

Write a decorator that prints the function name before executing it.

### Answer

```python
from functools import wraps


def log_function(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Calling:", func.__name__)
        return func(*args, **kwargs)

    return wrapper


@log_function
def add(a, b):
    return a + b


print(add(10, 20))
```

Output:

```text
Calling: add
30
```

---

# 62. Coding Interview Question — Write a Timing Decorator

### Question

Write a decorator that measures function execution time.

### Answer

```python
import time
from functools import wraps


def timer(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()

        result = func(*args, **kwargs)

        end = time.perf_counter()

        print("Execution time:", end - start)

        return result

    return wrapper
```

---

# 63. Coding Interview Question — Write a Decorator That Allows Only Positive Numbers

### Answer

```python
from functools import wraps


def positive_only(func):

    @wraps(func)
    def wrapper(n):
        if n <= 0:
            raise ValueError("Number must be positive")

        return func(n)

    return wrapper


@positive_only
def square(n):
    return n * n


print(square(5))
```

---

# 64. Coding Interview Question — Write a Decorator That Runs a Function Three Times

### Answer

```python
from functools import wraps


def repeat_three(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        for _ in range(3):
            func(*args, **kwargs)

    return wrapper


@repeat_three
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

# 65. Coding Interview Question — Write a Decorator With a Configurable Number of Repetitions

### Answer

```python
from functools import wraps


def repeat(times):

    def decorator(func):

        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)

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

# 66. Coding Interview Question — Create Two Decorators

### Answer

```python
def first(func):

    def wrapper():
        print("First")
        func()

    return wrapper


def second(func):

    def wrapper():
        print("Second")
        func()

    return wrapper


@first
@second
def greet():
    print("Hello")


greet()
```

Output:

```text
First
Second
Hello
```

---

# 67. Coding Interview Question — Preserve Function Metadata

### Answer

```python
from functools import wraps


def decorator(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)

    return wrapper


@decorator
def greet():
    """Greets the user."""
    print("Hello")


print(greet.__name__)
print(greet.__doc__)
```

Output:

```text
greet
Greets the user.
```

---

# 68. Coding Interview Question — Create a Decorator That Measures and Returns the Result

### Answer

```python
import time
from functools import wraps


def measure_time(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()

        result = func(*args, **kwargs)

        elapsed = time.perf_counter() - start

        print("Time:", elapsed)

        return result

    return wrapper


@measure_time
def add(a, b):
    return a + b


result = add(10, 20)

print("Result:", result)
```

---

# 69. Coding Interview Question — Create a Decorator That Blocks a Function

### Answer

```python
from functools import wraps


def block_function(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Access denied")

    return wrapper


@block_function
def delete_account():
    print("Account deleted")


delete_account()
```

Output:

```text
Access denied
```

---

# 70. Coding Interview Question — Create a Decorator for Role Checking

### Answer

```python
from functools import wraps


def admin_only(func):

    @wraps(func)
    def wrapper(user, *args, **kwargs):

        if user["role"] != "admin":
            return "Access denied"

        return func(user, *args, **kwargs)

    return wrapper


@admin_only
def delete_user(user, user_id):
    return f"User {user_id} deleted"


admin = {"role": "admin"}

print(delete_user(admin, 10))
```

Output:

```text
User 10 deleted
```

---

# 71. Common Tricky Question — Why Is the Wrapper Usually Defined Inside the Decorator?

Because the wrapper needs access to the original function.

Example:

```python
def decorator(func):

    def wrapper():
        return func()

    return wrapper
```

The wrapper closes over:

```python
func
```

This creates a closure.

---

# 72. Common Tricky Question — What Happens to the Original Function Name?

Consider:

```python
@decorator
def greet():
    print("Hello")
```

After decoration, conceptually:

```python
greet = decorator(greet)
```

Therefore, `greet` now refers to the object returned by the decorator, usually the wrapper.

Using:

```python
@wraps(func)
```

helps preserve the original function's metadata even though the name points to the wrapper.

---

# 73. Common Tricky Question — Does the Decorator Run Every Time the Function Is Called?

The decorator itself is applied when the function is defined/decorated.

The wrapper code runs each time the decorated function is called.

For example:

```python
@decorator
def greet():
    pass
```

The decorator is applied once during definition/import.

Then:

```python
greet()
greet()
greet()
```

executes the wrapper three times.

---

# 74. Common Tricky Question — Can We Have a Decorator Without a Wrapper?

Yes.

A decorator does not technically have to contain a nested function named `wrapper`.

The essential requirement is that it accepts an object and returns an appropriate replacement/transformed object.

For example:

```python
def decorator(func):
    return func
```

This is technically a decorator, although it does not add behavior.

The nested wrapper pattern is simply the most common form.

---

# 75. Common Tricky Question — Can One Decorator Accept Both Functions and Arguments?

It is possible, but the implementation becomes more complex because the decorator must distinguish whether it received a function directly or configuration arguments.

For normal interview and production code, it is usually clearer to keep:

```python
@decorator
```

and:

```python
@decorator(...)
```

as separate patterns when appropriate.

---

# 76. Common Tricky Question — What Happens If a Decorator Does Not Return Anything?

Example:

```python
def decorator(func):
    print("Decorator applied")
```

Then:

```python
@decorator
def greet():
    print("Hello")
```

Since the decorator returns `None`, conceptually:

```python
greet = None
```

Then:

```python
greet()
```

causes a `TypeError`.

Therefore, a function decorator normally needs to return a callable replacement.

---

# 77. Common Tricky Question — Can Decorators Be Stacked?

Yes.

```python
@authentication
@logging
@timer
def process():
    pass
```

Conceptually:

```python
process = authentication(
    logging(
        timer(process)
    )
)
```

The order matters because each decorator wraps the result of the decorator below it.

---

# 78. Important Mental Model

Remember decorators using this simple pattern:

```text
def decorator(func):
    def wrapper(*args, **kwargs):

        # before

        result = func(*args, **kwargs)

        # after

        return result

    return wrapper
```

Then:

```python
@decorator
def function(...):
    ...
```

means:

```python
function = decorator(function)
```

This mental model is enough to understand most decorator interview questions.

---

# 79. Interview Revision Table

| Concept | Key Point |
|---|---|
| Decorator | Modifies/enhances callable behavior |
| `@decorator` | Syntactic sugar for reassignment |
| Wrapper | Inner function around original function |
| `*args` | Arbitrary positional arguments |
| `**kwargs` | Arbitrary keyword arguments |
| `wraps` | Preserves function metadata |
| Decorator arguments | Usually require an additional nesting level |
| Multiple decorators | Applied from bottom to top |
| Function decorator | Decorates a function/method |
| Class decorator | Decorates a class |
| Closure | Helps wrapper retain access to original function |
| `staticmethod` | No automatic `self` or `cls` |
| `classmethod` | Receives `cls` |
| `property` | Method accessed using attribute syntax |

---

# 80. Must-Know Interview Questions

Before an interview, make sure you can answer these without memorizing word-for-word:

1. What is a decorator in Python?
2. Why do we use decorators?
3. What does `@decorator` mean?
4. How does a decorator work internally?
5. What is a wrapper function?
6. Why are `*args` and `**kwargs` commonly used?
7. Why should a wrapper return the original function's result?
8. What is `functools.wraps`?
9. Why is `functools.wraps` important?
10. What is a decorator with arguments?
11. Why does a decorator with arguments require three nested functions?
12. Can we have multiple decorators on one function?
13. What is the execution order of multiple decorators?
14. Can decorators modify return values?
15. Can decorators modify arguments?
16. Can decorators prevent function execution?
17. Can decorators handle exceptions?
18. Can decorators be used on classes?
19. What is a class decorator?
20. What is a closure?
21. How are decorators related to closures?
22. Why do first-class functions make decorators possible?
23. What is the difference between a decorator and a wrapper?
24. When is a decorator applied?
25. Does the decorator execute every time the function is called?
26. What happens to the original function name after decoration?
27. What happens if a decorator does not return a function?
28. What is `@staticmethod`?
29. What is `@classmethod`?
30. What is `@property`?
31. Difference between `staticmethod` and `classmethod`.
32. What are real-world uses of decorators?
33. How can decorators be used for authentication?
34. How can decorators be used for logging?
35. How can decorators be used for performance monitoring?
36. How can decorators be used in data engineering?
37. What are the advantages of decorators?
38. What are the disadvantages of decorators?
39. Write a logging decorator.
40. Write a timing decorator.
41. Write a decorator that validates input.
42. Write a decorator that repeats a function.
43. Write a decorator with configurable repetitions.
44. Write two stacked decorators.
45. Write a decorator that preserves function metadata.

---

# 81. Final Interview Answer

> A decorator is a Python feature that allows us to extend or modify the behavior of a function or class without changing its original implementation. A decorator usually receives the original function, defines a wrapper around it, and returns that wrapper. The `@decorator` syntax is syntactic sugar for applying the decorator to the function. Decorators are useful for cross-cutting concerns such as logging, authentication, authorization, validation, caching, and performance monitoring. For reusable decorators, I commonly use `*args`, `**kwargs`, and `functools.wraps` so that different function signatures are supported and the original function's metadata is preserved.