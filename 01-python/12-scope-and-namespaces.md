# Python Scope and Namespaces — Interview Preparation

## 1. What Is a Namespace?

A **namespace** is a mapping between names and the objects they refer to.

In simple words:

> A namespace is like a container where Python keeps track of names such as variables, functions, classes, and objects.

Example:

```python
name = "Harsha"
age = 21

print(name)
print(age)
```

Here:

```text
name → "Harsha"
age  → 21
```

Python uses a namespace to know which object a particular name refers to.

---

# 2. Why Are Namespaces Needed?

Namespaces prevent naming conflicts.

For example, two different functions can have variables with the same name:

```python
def student():
    name = "Harsha"
    print(name)


def employee():
    name = "Ravi"
    print(name)


student()
employee()
```

Output:

```text
Harsha
Ravi
```

Both functions have a variable called `name`, but they belong to different local namespaces.

### Interview Answer

> Namespaces help Python organize names and avoid naming conflicts by keeping names in different scopes or contexts.

---

# 3. What Is Scope?

**Scope** is the region of a Python program where a particular name can be accessed directly.

Example:

```python
def greet():
    message = "Hello"
    print(message)

greet()
```

`message` is available inside `greet()` because it is defined in that function's local scope.

Trying to access it outside:

```python
def greet():
    message = "Hello"

greet()

print(message)
```

results in:

```text
NameError
```

because `message` exists only in the local scope of `greet()`.

---

# 4. Difference Between Namespace and Scope

These two concepts are related but not the same.

### Namespace

Answers:

> Where is the name stored or associated with an object?

### Scope

Answers:

> Where can that name be accessed directly?

Example:

```python
x = 10

def test():
    y = 20
    print(x)
    print(y)
```

Here:

- `x` belongs to the global namespace.
- `y` belongs to the local namespace of `test()`.
- The scope determines where these names can be accessed.

### Interview Answer

> A namespace is a mapping of names to objects, while scope defines the region of the program where a name can be accessed.

---

# 5. What Are the Different Types of Namespaces in Python?

The important namespaces are:

1. **Built-in namespace**
2. **Global namespace**
3. **Local namespace**
4. **Enclosing namespace**

Example:

```python
x = "global"

def outer():
    y = "enclosing"

    def inner():
        z = "local"

        print(x)
        print(y)
        print(z)

    inner()

outer()
```

The lookup can involve:

```text
Local
Enclosing
Global
Built-in
```

This is known as the **LEGB rule**.

---

# 6. What Is the Built-in Namespace?

The built-in namespace contains names provided by Python itself.

Examples:

```python
print()
len()
sum()
max()
min()
type()
range()
```

Example:

```python
numbers = [10, 20, 30]

print(len(numbers))
```

Here `len` is available because it belongs to Python's built-in namespace.

---

# 7. What Is the Global Namespace?

The global namespace contains names defined at the module/program level.

Example:

```python
name = "Harsha"
age = 21

def greet():
    print(name)

greet()
```

Here:

```text
name
age
greet
```

are defined in the global namespace.

---

# 8. What Is the Local Namespace?

The local namespace contains names created inside a function.

```python
def calculate():
    price = 100
    quantity = 2

    total = price * quantity

    print(total)

calculate()
```

The variables:

```text
price
quantity
total
```

belong to the local namespace of `calculate()`.

They are normally not directly accessible outside the function.

---

# 9. What Is an Enclosing Namespace?

An enclosing namespace occurs when one function is nested inside another function.

Example:

```python
def outer():
    message = "Hello"

    def inner():
        print(message)

    inner()

outer()
```

`message` belongs to the enclosing scope of `inner()`.

The inner function can access it because Python searches the enclosing scope after checking its local scope.

---

# 10. What Is the LEGB Rule?

**LEGB** describes Python's name lookup order:

```text
L → Local
E → Enclosing
G → Global
B → Built-in
```

When Python encounters a name, it searches in this order.

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

Python finds `x` in the local scope first.

---

# 11. Explain LEGB With an Example

```python
x = "Global"

def outer():
    x = "Enclosing"

    def inner():
        x = "Local"
        print(x)

    inner()

outer()
```

Output:

```text
Local
```

Why?

Python searches:

```text
Local → Enclosing → Global → Built-in
```

It finds `x` in the local scope, so it stops searching.

---

# 12. What Happens If the Local Variable Does Not Exist?

```python
x = "Global"

def outer():
    x = "Enclosing"

    def inner():
        print(x)

    inner()

outer()
```

Output:

```text
Enclosing
```

`inner()` does not have a local `x`, so Python searches the enclosing scope.

---

# 13. What Happens If Local and Enclosing Variables Do Not Exist?

```python
x = "Global"

def outer():

    def inner():
        print(x)

    inner()

outer()
```

Output:

```text
Global
```

Python searches:

```text
Local → Enclosing → Global
```

and finds `x` in the global namespace.

---

# 14. What Happens If the Name Is Not Found Anywhere?

```python
def test():
    print(x)

test()
```

Python raises:

```text
NameError
```

because `x` cannot be found in:

```text
Local
Enclosing
Global
Built-in
```

---

# 15. What Is a Local Variable?

A variable created inside a function is generally local to that function.

```python
def test():
    x = 10
    print(x)

test()
```

`x` is a local variable.

---

# 16. What Is a Global Variable?

A variable defined outside functions at the module level is generally considered global within that module.

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

# 17. Can a Function Access a Global Variable?

Yes.

```python
name = "Harsha"

def greet():
    print(name)

greet()
```

Output:

```text
Harsha
```

The function does not have a local `name`, so Python searches the global scope.

---

# 18. Can a Function Modify a Global Variable?

Not directly through assignment.

Consider:

```python
count = 10

def update():
    count = 20

update()

print(count)
```

Output:

```text
10
```

The `count = 20` creates/assigns a local variable inside `update()` rather than changing the global `count`.

---

# 19. What Is the `global` Keyword?

The `global` keyword tells Python that a name inside a function refers to the global variable rather than creating a local variable.

Example:

```python
count = 10

def update():
    global count
    count = 20

update()

print(count)
```

Output:

```text
20
```

### Interview Answer

> The `global` keyword allows a function to assign to a variable defined in the global scope.

---

# 20. Why Do We Need the `global` Keyword?

Consider:

```python
count = 10

def update():
    count = count + 1
```

This causes:

```text
UnboundLocalError
```

because Python treats `count` as local due to the assignment.

Correct:

```python
count = 10

def update():
    global count
    count = count + 1

update()

print(count)
```

Output:

```text
11
```

---

# 21. Important Interview Question — Reading vs Modifying Global Variables

A function can read a global variable without `global`:

```python
x = 10

def test():
    print(x)

test()
```

But assignment to the global variable requires `global`:

```python
x = 10

def test():
    global x
    x = 20

test()

print(x)
```

Output:

```text
20
```

### Interview Answer

> Reading a global variable does not require the `global` keyword, but assigning to it from inside a function requires `global`.

---

# 22. What Is the `nonlocal` Keyword?

`nonlocal` is used in nested functions when we want to modify a variable belonging to an enclosing function.

Example:

```python
def outer():
    count = 10

    def inner():
        nonlocal count
        count += 1

    inner()

    print(count)

outer()
```

Output:

```text
11
```

---

# 23. Difference Between `global` and `nonlocal`

| `global` | `nonlocal` |
|---|---|
| Refers to global scope | Refers to enclosing function scope |
| Used for module-level variables | Used in nested functions |
| Can modify global variable | Can modify enclosing variable |

Example:

```python
x = 10

def outer():
    y = 20

    def inner():
        global x
        nonlocal y

        x += 1
        y += 1

    inner()

outer()

print(x)
```

---

# 24. Why Does `nonlocal` Exist?

Consider:

```python
def counter():
    count = 0

    def increment():
        count += 1

    increment()
```

This causes an error because `count += 1` makes `count` local to `increment()`.

Using `nonlocal`:

```python
def counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    print(increment())
    print(increment())

counter()
```

Output:

```text
1
2
```

---

# 25. What Is the Difference Between `global` and `nonlocal` in One Example?

```python
x = 10

def outer():
    y = 20

    def inner():
        global x
        nonlocal y

        x += 1
        y += 1

    inner()

    print("y:", y)

outer()

print("x:", x)
```

Output:

```text
y: 21
x: 11
```

`global` modifies `x` from the global scope.

`nonlocal` modifies `y` from the enclosing function scope.

---

# 26. What Is Variable Shadowing?

Variable shadowing occurs when a variable in a more specific scope has the same name as a variable in an outer scope.

Example:

```python
x = "Global"

def test():
    x = "Local"
    print(x)

test()
print(x)
```

Output:

```text
Local
Global
```

The local `x` shadows the global `x` inside the function.

---

# 27. Does a Local Variable Change the Global Variable?

No, simply using the same name does not change the global variable.

```python
x = 100

def test():
    x = 200
    print("Inside:", x)

test()

print("Outside:", x)
```

Output:

```text
Inside: 200
Outside: 100
```

---

# 28. What Is Name Resolution?

Name resolution is the process Python uses to determine which object a name refers to.

Example:

```python
x = "global"

def test():
    x = "local"
    print(x)

test()
```

Python resolves `x` to the local variable because local scope has higher priority than global scope.

---

# 29. Can a Local Variable Have the Same Name as a Global Variable?

Yes.

```python
name = "Harsha"

def test():
    name = "Ravi"
    print(name)

test()
print(name)
```

Output:

```text
Ravi
Harsha
```

This is an example of variable shadowing.

---

# 30. What Is the Built-in Namespace Used for?

It provides commonly used Python names such as:

```python
print
len
sum
range
type
int
str
list
dict
```

Example:

```python
numbers = [10, 20, 30]

print(len(numbers))
```

Python finds `len` in the built-in namespace if it is not found in local, enclosing, or global scope.

---

# 31. Can We Shadow a Built-in Name?

Yes, but it is generally a bad practice.

Example:

```python
len = 100

print(len)
```

Now `len` refers to `100` in the current namespace.

This can cause problems:

```python
len = 100

numbers = [1, 2, 3]

print(len(numbers))
```

This produces an error because `len` no longer refers to the built-in function.

### Interview Point

> We can technically shadow built-in names, but it should be avoided because it can make built-in functionality unavailable or confusing.

---

# 32. What Is `locals()`?

`locals()` returns a dictionary representing the current local namespace.

Example:

```python
def test():
    x = 10
    y = 20

    print(locals())

test()
```

Output will contain entries similar to:

```text
{'x': 10, 'y': 20}
```

The exact representation can vary depending on the context.

---

# 33. What Is `globals()`?

`globals()` returns a dictionary representing the current global namespace.

Example:

```python
x = 10

print(globals()["x"])
```

Output:

```text
10
```

It provides access to the global namespace dictionary.

---

# 34. Difference Between `locals()` and `globals()`

| `locals()` | `globals()` |
|---|---|
| Current local namespace | Current global namespace |
| Returns a dictionary-like mapping | Returns the global namespace dictionary |
| Commonly used inside functions | Refers to module/global scope |

Example:

```python
x = 10

def test():
    y = 20

    print("Local:", locals())
    print("Global x:", globals()["x"])

test()
```

---

# 35. Can We Use `globals()` to Modify a Global Variable?

Yes.

Example:

```python
x = 10

globals()["x"] = 20

print(x)
```

Output:

```text
20
```

However, directly modifying the global namespace through `globals()` is generally less readable than normal assignment or using a clearly designed interface.

---

# 36. What Is the Scope of a Variable Inside a Function?

Normally, a variable assigned inside a function belongs to that function's local scope.

```python
def test():
    x = 10

    print(x)

test()
```

`x` is local to `test()`.

---

# 37. What Is the Scope of a Variable Defined at Module Level?

A module-level variable belongs to the module's global namespace.

```python
x = 10

def test():
    print(x)
```

Functions in the same module can access it through global name lookup.

---

# 38. How Does Scope Work With Nested Functions?

Example:

```python
def outer():
    x = 10

    def inner():
        print(x)

    inner()

outer()
```

`inner()` does not have a local `x`, so Python looks in the enclosing scope and finds `x`.

---

# 39. What Is a Closure and How Is It Related to Scope?

A closure occurs when an inner function remembers and can access variables from its enclosing scope even after the outer function has finished executing.

Example:

```python
def outer(message):
    def inner():
        print(message)

    return inner


greet = outer("Hello")

greet()
```

Output:

```text
Hello
```

The inner function retains access to `message`.

### Interview Answer

> A closure is created when an inner function retains access to variables from its enclosing scope. It is closely related to the enclosing scope and lexical scoping.

---

# 40. Real-World Example — Counter Using Closure

```python
def create_counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment


counter = create_counter()

print(counter())
print(counter())
print(counter())
```

Output:

```text
1
2
3
```

Here:

- `count` belongs to `create_counter()`
- `increment()` accesses it through the enclosing scope
- `nonlocal` allows `increment()` to modify it
- The returned function remembers `count`

---

# 41. What Happens When a Function Is Called Multiple Times?

Each function call creates its own local execution context.

Example:

```python
def test():
    x = 10
    print(x)

test()
test()
```

Each call gets its own local variable `x`.

---

# 42. Are Local Variables Shared Between Function Calls?

Normally, no.

```python
def test():
    x = 0
    x += 1
    print(x)

test()
test()
```

Output:

```text
1
1
```

Each invocation starts with a new local `x`.

---

# 43. What Is the Relationship Between Scope and Function Calls?

A function creates a local scope when it executes.

Example:

```python
def calculate():
    result = 100
    print(result)

calculate()
```

`result` belongs to the function's local namespace during execution.

---

# 44. What Happens to Local Variables After a Function Returns?

Local names associated only with that function's execution context are no longer directly accessible after the function returns.

Example:

```python
def test():
    x = 10
    return x

result = test()

print(result)
```

The value can be returned and stored elsewhere, but:

```python
print(x)
```

outside the function raises:

```text
NameError
```

---

# 45. Does Scope Depend on Where a Variable Is Used or Where It Is Defined?

Python uses **lexical/static scoping**.

The scope of a name is determined by the structure of the code rather than by which function happens to call another function.

Example:

```python
x = "global"

def outer():
    x = "outer"

    def inner():
        print(x)

    inner()

outer()
```

`inner()` finds `x` in its lexical enclosing scope.

---

# 46. Important Interview Question — Explain This Output

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

The local `x` shadows the global `x`; it does not modify it.

---

# 47. Important Interview Question — Explain This Output

```python
x = 10

def test():
    print(x)

test()
```

### Answer

```text
10
```

There is no local `x`, so Python searches the global scope.

---

# 48. Important Interview Question — Explain This Error

```python
x = 10

def test():
    x = x + 1

test()
```

### Answer

This raises:

```text
UnboundLocalError
```

because Python sees the assignment:

```python
x = ...
```

and therefore treats `x` as a local variable inside `test()`. The right-hand side tries to read that local `x` before it has been assigned.

Correct version:

```python
x = 10

def test():
    global x
    x = x + 1

test()

print(x)
```

Output:

```text
11
```

---

# 49. Important Interview Question — Explain `nonlocal`

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

`nonlocal` tells `inner()` to use the `x` belonging to `outer()` rather than creating a new local `x`.

---

# 50. Important Output Question

```python
x = "A"

def outer():
    x = "B"

    def inner():
        x = "C"
        print(x)

    inner()

outer()
```

Output:

```text
C
```

The local scope of `inner()` has the highest priority.

---

# 51. Important Output Question

```python
x = "A"

def outer():
    x = "B"

    def inner():
        print(x)

    inner()

outer()
```

Output:

```text
B
```

`inner()` finds `x` in the enclosing scope.

---

# 52. Important Output Question

```python
x = "A"

def outer():

    def inner():
        print(x)

    inner()

outer()
```

Output:

```text
A
```

The name is found in the global scope.

---

# 53. Important Output Question

```python
x = "global"

def test():
    global x
    x = "local-looking"

test()

print(x)
```

Output:

```text
local-looking
```

The `global` keyword makes the assignment modify the global `x`.

---

# 54. Important Output Question

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x = 20

    inner()

    print(x)

outer()
```

Output:

```text
20
```

---

# 55. Important Output Question

```python
x = 10

def test():
    x = 20

test()

print(x)
```

Output:

```text
10
```

The assignment creates a local `x`.

---

# 56. Important Interview Question — Why Is This `UnboundLocalError`?

```python
x = 10

def test():
    print(x)
    x = 20

test()
```

### Answer

This raises:

```text
UnboundLocalError
```

because Python determines that `x` is local to `test()` due to the assignment:

```python
x = 20
```

Therefore the earlier:

```python
print(x)
```

tries to access the local `x` before it has a value.

---

# 57. Difference Between `NameError` and `UnboundLocalError`

### `NameError`

Usually occurs when a name cannot be found.

```python
def test():
    print(x)

test()
```

If `x` is nowhere available, Python raises `NameError`.

### `UnboundLocalError`

Occurs when Python treats a variable as local but it is accessed before being assigned.

```python
x = 10

def test():
    print(x)
    x = 20

test()
```

### Interview Answer

> `NameError` means Python cannot resolve the name, while `UnboundLocalError` is a specific case where a local variable is referenced before it has been assigned a value.

---

# 58. Can `global` Be Used Inside a Nested Function?

Yes.

```python
x = 10

def outer():

    def inner():
        global x
        x = 20

    inner()

outer()

print(x)
```

Output:

```text
20
```

`global` always refers to the module/global scope, not the nearest enclosing function.

---

# 59. Can `nonlocal` Be Used at the Top Level?

No.

`nonlocal` requires an enclosing function scope.

Incorrect:

```python
x = 10

nonlocal x
```

This produces a syntax error.

---

# 60. Can `nonlocal` Refer to a Global Variable?

No.

`nonlocal` must refer to an existing variable in an enclosing function scope.

For a global variable, use:

```python
global x
```

---

# 61. `global` vs `nonlocal` — Easy Memory Trick

```text
global
    ↓
module/global level

nonlocal
    ↓
nearest enclosing function
```

Example:

```python
x = 10

def outer():
    y = 20

    def inner():
        global x
        nonlocal y
```

Here:

```text
x → global
y → enclosing
```

---

# 62. Scope in `if` Blocks

Unlike functions, an `if` block does not create a separate local scope.

```python
if True:
    x = 10

print(x)
```

Output:

```text
10
```

This is different from a function:

```python
def test():
    x = 10

test()

print(x)
```

The second example raises `NameError`.

---

# 63. Scope in `for` Loops

A normal `for` loop does not create a separate scope.

```python
for i in range(3):
    x = i

print(x)
```

Output:

```text
2
```

The variable remains accessible after the loop in the same scope.

---

# 64. Do List Comprehensions Have Their Own Scope?

In Python 3, the comprehension variable has its own scope.

Example:

```python
x = 10

result = [x for x in range(3)]

print(x)
```

Output:

```text
10
```

The `x` used by the comprehension does not overwrite the outer `x`.

This is an important difference from ordinary `for` loops.

---

# 65. Scope of Function Parameters

Function parameters are local variables.

```python
def greet(name):
    print(name)

greet("Harsha")
```

`name` belongs to the local scope of `greet()`.

---

# 66. Scope of Imported Names

Imported names generally become names in the module's namespace.

Example:

```python
import math

print(math.sqrt(25))
```

`math` becomes available in the module namespace.

---

# 67. What Is a Module Namespace?

Each Python module has its own namespace.

Example:

```python
# module_a.py

x = 10
```

Another module can access it through:

```python
import module_a

print(module_a.x)
```

Using module namespaces helps prevent naming conflicts.

---

# 68. Why Are Modules Useful for Namespaces?

Suppose two modules both define:

```python
value = 100
```

We can access them separately:

```python
import module_a
import module_b

print(module_a.value)
print(module_b.value)
```

The module name provides a namespace boundary.

---

# 69. What Is `__name__`?

`__name__` is a special built-in/module-level name that tells us the name under which a module is being used.

When a Python file is run directly:

```python
print(__name__)
```

the value is typically:

```text
__main__
```

When imported as a module, `__name__` is generally the module's name.

---

# 70. Why Do We Use `if __name__ == "__main__"`?

It allows code to run only when the file is executed directly, not when it is imported.

Example:

```python
def greet():
    print("Hello")


if __name__ == "__main__":
    greet()
```

If the file is executed directly:

```text
Hello
```

If imported from another module, the guarded code does not execute automatically.

### Interview Answer

> `if __name__ == "__main__"` is used to distinguish direct execution from importing a module and to prevent execution of script-specific code during import.

---

# 71. Namespace Example With a Module

Suppose:

```python
# calculator.py

x = 10

def add(a, b):
    return a + b
```

Another file:

```python
import calculator

print(calculator.x)
print(calculator.add(10, 20))
```

Output:

```text
10
30
```

Here `calculator` acts as a namespace containing:

```text
x
add
```

---

# 72. Real-World Example — Large Application

In a large application, many files may contain names such as:

```text
config
logger
process
data
```

Using modules/packages creates separate namespaces:

```python
user_service.process()
payment_service.process()
```

Even though both modules have a function called `process`, the module namespace keeps them distinct.

### Interview Explanation

> Namespaces become especially useful in larger applications because different modules can contain similarly named functions or variables without directly conflicting with each other.

---

# 73. Real-World Example — Data Engineering

In a data pipeline, different modules might contain functions such as:

```python
extract_data()
transform_data()
load_data()
```

A project could organize them as:

```text
pipeline/
    ingestion.py
    transformation.py
    loading.py
```

Then we can use:

```python
from pipeline import ingestion
from pipeline import transformation

ingestion.extract_data()
transformation.transform_data()
```

The module structure keeps related names organized and reduces naming conflicts.

---

# 74. Should We Use Many Global Variables?

Generally, no.

Although global variables are supported, excessive use can make programs:

- harder to understand
- harder to test
- harder to maintain
- more dependent on shared mutable state

Prefer passing values explicitly when practical.

Instead of:

```python
total = 0

def calculate():
    global total
    total += 100
```

prefer:

```python
def calculate(total):
    return total + 100

total = calculate(0)
```

This makes the dependency explicit.

---

# 75. Why Should `global` Be Used Carefully?

`global` can make functions modify state outside their local scope.

Example:

```python
count = 0

def increment():
    global count
    count += 1
```

This works, but the function now depends on shared global state.

For larger applications, returning values or encapsulating state in an object is often easier to reason about.

### Interview Answer

> `global` is useful when genuinely required, but I avoid unnecessary global state because it increases coupling and can make testing and maintenance harder.

---

# 76. Scope and Mutable Objects

Scope controls the name, not whether the referenced object itself is mutable.

Example:

```python
numbers = [1, 2, 3]

def add_value():
    numbers.append(4)

add_value()

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

The function can mutate the global list without using `global` because it is not assigning a new object to the name `numbers`.

---

# 77. Why Does `global` Not Need to Be Used for `append()`?

Consider:

```python
numbers = [1, 2, 3]

def add():
    numbers.append(4)

add()

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

The function is modifying the existing list object.

It is not doing:

```python
numbers = another_list
```

Therefore, `global` is not required.

---

# 78. Important Difference — Mutation vs Reassignment

### Mutation

```python
numbers.append(4)
```

Changes the existing object.

### Reassignment

```python
numbers = [1, 2, 3, 4]
```

Makes the name refer to another object.

This distinction is important when discussing global variables and scope.

---

# 79. Important Output Question — Mutable Global

```python
numbers = [1, 2]

def test():
    numbers.append(3)

test()

print(numbers)
```

Output:

```text
[1, 2, 3]
```

No `global` keyword is needed because there is no reassignment of the name.

---

# 80. Important Output Question — Reassignment

```python
numbers = [1, 2]

def test():
    numbers = [3, 4]

test()

print(numbers)
```

Output:

```text
[1, 2]
```

The assignment creates a local `numbers`.

---

# 81. Important Interview Question — Explain the LEGB Rule in One Minute

A strong answer:

> LEGB stands for Local, Enclosing, Global, and Built-in. When Python needs to resolve a name, it first checks the current local scope, then any enclosing function scopes, then the global module scope, and finally the built-in namespace. Python stops when it finds the name. If it cannot find the name anywhere, it raises a `NameError`.

---

# 82. Important Interview Question — Difference Between Scope and Lifetime

These concepts are different.

### Scope

Where a name can be accessed.

### Lifetime

How long an object exists in memory.

For example:

```python
def test():
    x = [1, 2, 3]
    return x

data = test()
```

The local name `x` belongs to the function's local scope, but the list object can continue to exist because it is returned and referenced by `data`.

### Interview Answer

> Scope concerns where a name is accessible, while lifetime concerns how long the referenced object exists.

---

# 83. Important Interview Question — What Is LEGB Lookup Order?

Remember:

```text
L → Local
E → Enclosing
G → Global
B → Built-in
```

Example:

```python
x = "Global"

def outer():
    x = "Enclosing"

    def inner():
        x = "Local"
        print(x)

    inner()

outer()
```

Output:

```text
Local
```

---

# 84. Important Interview Question — What Is the Difference Between `global` and `nonlocal`?

Strong answer:

> `global` tells Python that an assignment should target a variable in the module-level global scope. `nonlocal` is used inside nested functions and tells Python to use a variable from an enclosing function scope. So `global` moves outward to the module scope, while `nonlocal` refers to the nearest suitable enclosing function scope.

---

# 85. Important Interview Question — Why Does Python Have Separate Namespaces?

Strong answer:

> Separate namespaces help organize names and avoid conflicts. For example, different functions can have local variables with the same name, and different modules can define functions with the same name. Python can distinguish them based on their namespace and scope.

---

# 86. Important Interview Question — Can Two Functions Have the Same Local Variable Name?

Yes.

```python
def first():
    value = 10
    print(value)


def second():
    value = 20
    print(value)


first()
second()
```

Output:

```text
10
20
```

Each function has its own local namespace.

---

# 87. Important Interview Question — What Happens If a Local and Global Variable Have the Same Name?

The local variable takes priority inside the function.

```python
x = 10

def test():
    x = 20
    print(x)

test()
```

Output:

```text
20
```

The global value remains unchanged.

---

# 88. Important Interview Question — How Can You Inspect Namespaces?

Useful built-in functions include:

```python
locals()
globals()
```

Example:

```python
x = 10

def test():
    y = 20

    print(locals())
    print(globals()["x"])

test()
```

These can be useful for debugging and understanding name resolution, although they should not normally replace clean program design.

---

# 89. Important Interview Question — What Is Shadowing?

Strong answer:

> Shadowing happens when a name in an inner or more specific scope has the same name as one in an outer scope. The inner name takes precedence during lookup within that scope.

Example:

```python
x = "global"

def test():
    x = "local"
    print(x)

test()
```

Output:

```text
local
```

---

# 90. Important Interview Question — Can a Function Access a Variable From an Enclosing Function?

Yes.

```python
def outer():
    message = "Hello"

    def inner():
        print(message)

    inner()

outer()
```

Output:

```text
Hello
```

This is an example of enclosing-scope lookup.

---

# 91. Important Interview Question — Why Is `nonlocal` Useful in Closures?

Example:

```python
def counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment
```

`nonlocal` allows the inner function to maintain and update state belonging to the enclosing function.

This is useful for creating stateful closures.

---

# 92. Interview Trap — Does an `if` Block Create a New Scope?

No, not in the same way a function does.

```python
if True:
    x = 10

print(x)
```

Output:

```text
10
```

Functions create local scopes; ordinary `if` and `for` blocks do not create separate function-like scopes.

---

# 93. Interview Trap — Does a `for` Loop Create a New Scope?

A normal `for` loop does not create a separate scope.

```python
for i in range(3):
    value = i

print(value)
```

Output:

```text
2
```

---

# 94. Interview Trap — Are Comprehension Variables the Same as Normal Loop Variables?

In Python 3, comprehension variables have their own comprehension scope.

```python
x = 100

result = [x for x in range(3)]

print(x)
```

Output:

```text
100
```

---

# 95. Interview Trap — Does `global` Make a Variable Global Everywhere?

No.

`global` affects name resolution within the current function and refers to the module-level global namespace.

It does not magically make a variable globally available across every module in an application.

---

# 96. Interview Trap — Is `global` Required to Read a Global List?

No.

```python
numbers = [1, 2, 3]

def test():
    print(numbers)

test()
```

Reading it works without `global`.

Even mutation works:

```python
def test():
    numbers.append(4)
```

`global` is required when assigning to the global name itself.

---

# 97. Interview Trap — Is `global` Required for Every Global Variable?

No.

Only assignment/rebinding from inside a function requires it.

Reading:

```python
print(x)
```

does not require `global`.

Mutation of a mutable object:

```python
items.append(10)
```

does not require `global`.

Reassignment:

```python
items = []
```

does require `global` if the intention is to change the module-level binding.

---

# 98. Important Practical Example

Consider a data-processing application:

```python
pipeline_name = "YouTube Data Pipeline"

def process_data(records):
    processed_count = len(records)

    def report():
        print(pipeline_name)
        print(processed_count)

    report()


records = [1, 2, 3, 4]

process_data(records)
```

Output:

```text
YouTube Data Pipeline
4
```

Name lookup works through:

```text
report local scope
↓
process_data enclosing scope
↓
module/global scope
↓
built-in scope
```

This is a useful way to connect scope concepts with real applications.

---

# 99. Interview Checklist

Before moving to the next Python topic, you should be comfortable explaining:

- What is a namespace?
- What is scope?
- Difference between namespace and scope
- Local namespace
- Global namespace
- Enclosing namespace
- Built-in namespace
- LEGB rule
- Name resolution
- Local variables
- Global variables
- Enclosing variables
- `global`
- `nonlocal`
- Variable shadowing
- `locals()`
- `globals()`
- Function scope
- Module scope
- Nested function scope
- Closures
- Scope of `if`
- Scope of `for`
- Comprehension scope
- Function parameter scope
- Module namespaces
- `__name__`
- `if __name__ == "__main__"`
- Mutation vs reassignment
- `NameError`
- `UnboundLocalError`
- Global state and its drawbacks

---

# 100. Final Quick Revision

```text
NAMESPACE
    ↓
Mapping of names → objects

SCOPE
    ↓
Where a name can be accessed

LEGB
    ↓
L = Local
E = Enclosing
G = Global
B = Built-in

LOCAL
    ↓
Inside current function

ENCLOSING
    ↓
Outer/nested function scope

GLOBAL
    ↓
Module-level scope

BUILT-IN
    ↓
print, len, sum, range, type, etc.

global
    ↓
Modify/rebind a module-level variable from a function

nonlocal
    ↓
Modify/rebind a variable from an enclosing function

SHADOWING
    ↓
Inner name hides outer name

locals()
    ↓
Current local namespace

globals()
    ↓
Global namespace

CLOSURE
    ↓
Inner function retains access to enclosing variables

MUTATION
    ↓
Modify existing object

REASSIGNMENT
    ↓
Make a name refer to another object

IMPORTANT
    ↓
Prefer clear local state and explicit parameters
Avoid unnecessary global state
```

# Interview-Level Takeaway

> **The core idea is name resolution. Python organizes names into namespaces, and scope determines where those names can be accessed. When Python encounters a name, it follows the LEGB order: Local, Enclosing, Global, and Built-in. Understanding `global`, `nonlocal`, shadowing, closures, and the difference between mutation and reassignment is important because many Python interview questions test these concepts through short code snippets and output-based questions.**