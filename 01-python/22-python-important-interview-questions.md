# 22 - Python Important Interview Questions

> **Purpose:** This is the main Python interview revision file.  
> Prepare this file more deeply than the individual topic files. It combines the most important and frequently asked Core Python concepts, explanations, examples, output-based questions, small coding questions, and common follow-up questions.
>
> **Interview strategy:** For every question, try to understand the explanation, remember the example, and be able to write the small code yourself. You do not need to memorize the wording exactly.

---

# 1. Python Fundamentals

## Q1. What is Python?

### Answer

Python is a **high-level, interpreted, general-purpose programming language** known for its simple and readable syntax.

It supports multiple programming styles, including:

- Procedural programming
- Object-oriented programming
- Functional programming

Python is widely used in:

- Web development
- Data Engineering
- Data Science
- Machine Learning
- Automation
- Scripting
- API development

### Example

```python
name = "Harsha"
print("Hello", name)
```

### Interview Point

A good short answer is:

> "Python is a high-level, interpreted, general-purpose programming language known for its readability and large ecosystem. It is widely used for web development, automation, data engineering, data science, and many other applications."

---

## Q2. Why is Python called an interpreted language?

### Answer

Python is commonly described as an interpreted language because Python programs are executed by the Python interpreter rather than being directly compiled into native machine code before execution in the traditional sense.

In CPython, the source code is first converted into **bytecode**, which is then executed by the Python Virtual Machine.

### Simple flow

```text
Python Source Code
        ↓
     Bytecode
        ↓
Python Virtual Machine
        ↓
     Execution
```

### Important

Do not simply say:

> "Python is 100% interpreted and never compiled."

That is an oversimplification because CPython does compile source code to bytecode.

---

## Q3. What are the main features of Python?

### Answer

Important features include:

- Simple and readable syntax
- High-level language
- Dynamically typed
- Object-oriented
- Interpreted execution model
- Large standard library
- Large third-party ecosystem
- Cross-platform
- Supports multiple programming paradigms
- Automatic memory management
- Exception handling
- Easy integration with other technologies

---

## Q4. What does dynamically typed mean in Python?

### Answer

Python is dynamically typed because the type of a variable is determined at **runtime**, and we do not have to explicitly declare the variable's type.

```python
x = 10
print(type(x))

x = "Hello"
print(type(x))
```

Here, `x` first refers to an integer and later refers to a string.

### Important distinction

Dynamic typing does **not** mean Python has no types.

Python is strongly typed and dynamically typed.

---

## Q5. Is Python strongly typed or weakly typed?

### Answer

Python is generally considered **strongly typed**.

Python does not automatically perform arbitrary incompatible type conversions.

```python
a = 10
b = "20"

print(a + b)
```

This produces a `TypeError`.

We need explicit conversion:

```python
print(a + int(b))
```

---

## Q6. What is the difference between syntax error and runtime error?

### Answer

A **syntax error** occurs when Python cannot understand the structure of the code.

```python
if True
    print("Hello")
```

A **runtime error** occurs while the program is executing.

```python
x = 10 / 0
```

This produces:

```text
ZeroDivisionError
```

### Simple difference

| Error | When it occurs |
|---|---|
| Syntax Error | Code structure is invalid |
| Runtime Error | Error occurs during execution |

---

# 2. Python Data Types

## Q7. What are Python's built-in data types?

### Answer

Important built-in types include:

### Numeric

```python
int
float
complex
```

### Boolean

```python
bool
```

### Sequence

```python
str
list
tuple
range
```

### Set

```python
set
frozenset
```

### Mapping

```python
dict
```

### Binary

```python
bytes
bytearray
memoryview
```

### Special

```python
NoneType
```

---

## Q8. What is the difference between mutable and immutable objects?

### Answer

A **mutable object** can be changed after creation.

Examples:

```python
list
set
dict
bytearray
```

An **immutable object** cannot be changed after creation.

Examples:

```python
int
float
bool
str
tuple
frozenset
bytes
```

### Example

```python
numbers = [1, 2, 3]
numbers.append(4)

print(numbers)
```

The list itself was modified.

For strings:

```python
name = "Harsha"
name = name + " Kumar"
```

A new string object is created rather than modifying the original string.

---

## Q9. What is the difference between `is` and `==`?

### Answer

`==` checks whether two objects have equal values.

`is` checks whether two variables refer to the **same object**.

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

The lists contain the same values but are different objects.

### Interview rule

Use:

```python
==
```

for value comparison.

Use:

```python
is
```

when checking object identity, especially:

```python
x is None
```

---

## Q10. What is `None` in Python?

### Answer

`None` represents the absence of a value.

```python
result = None
```

It is an object of type:

```python
NoneType
```

Example:

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

A function without an explicit `return` returns `None`.

---

## Q11. What are truthy and falsy values?

### Answer

Python evaluates some values as `False` in Boolean contexts.

Common falsy values include:

```python
False
None
0
0.0
""
[]
()
{}
set()
```

Most other values are truthy.

### Example

```python
items = []

if items:
    print("Not empty")
else:
    print("Empty")
```

Output:

```text
Empty
```

---

# 3. Strings

## Q12. Are strings mutable in Python?

### Answer

No. Strings are **immutable**.

```python
name = "Python"
```

We cannot directly modify an individual character:

```python
name[0] = "J"
```

This produces:

```text
TypeError
```

Instead, we create a new string:

```python
name = "J" + name[1:]
print(name)
```

---

## Q13. What are common string methods?

### Answer

Frequently used methods include:

```python
upper()
lower()
strip()
replace()
split()
join()
find()
startswith()
endswith()
count()
```

### Example

```python
text = "  Python Programming  "

print(text.strip())
print(text.lower())
print(text.upper())
print(text.replace("Python", "Java"))
```

---

## Q14. What is the difference between `split()` and `join()`?

### Answer

`split()` converts a string into a list.

```python
text = "Python SQL AWS"

result = text.split()

print(result)
```

Output:

```text
['Python', 'SQL', 'AWS']
```

`join()` combines multiple strings into one string.

```python
words = ["Python", "SQL", "AWS"]

result = " ".join(words)

print(result)
```

Output:

```text
Python SQL AWS
```

---

## Q15. What is string slicing?

### Answer

Slicing extracts a portion of a sequence.

Syntax:

```python
string[start:stop:step]
```

Example:

```python
text = "Python"

print(text[0:3])
print(text[:3])
print(text[2:])
print(text[::-1])
```

Output:

```text
Pyt
Pyt
thon
nohtyP
```

---

# 4. Lists

## Q16. What is a list?

### Answer

A list is an **ordered, mutable collection** that can contain multiple values.

```python
numbers = [10, 20, 30, 40]
```

Lists can contain different data types:

```python
data = [10, "Python", 3.14, True]
```

---

## Q17. What are common list methods?

### Answer

Important methods include:

```python
append()
extend()
insert()
remove()
pop()
clear()
sort()
reverse()
index()
count()
```

### Example

```python
numbers = [3, 1, 2]

numbers.append(4)
numbers.sort()

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

---

## Q18. What is the difference between `append()` and `extend()`?

### Answer

`append()` adds the entire object as one element.

```python
a = [1, 2]
a.append([3, 4])

print(a)
```

Output:

```text
[1, 2, [3, 4]]
```

`extend()` adds each element separately.

```python
a = [1, 2]
a.extend([3, 4])

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

---

## Q19. What is the difference between `remove()` and `pop()`?

### Answer

`remove()` removes an element based on its value.

```python
numbers = [10, 20, 30]

numbers.remove(20)

print(numbers)
```

`pop()` removes an element based on its index and returns the removed value.

```python
numbers = [10, 20, 30]

value = numbers.pop(1)

print(value)
print(numbers)
```

Output:

```text
20
[10, 30]
```

---

# 5. Tuples

## Q20. What is a tuple?

### Answer

A tuple is an **ordered and immutable collection**.

```python
numbers = (10, 20, 30)
```

Once created, its elements cannot normally be changed.

### Example

```python
point = (10, 20)

print(point[0])
```

---

## Q21. Why would you use a tuple instead of a list?

### Answer

A tuple is useful when the collection should not be modified.

For example:

```python
coordinates = (17.38, 78.48)
```

Tuples can also be used as dictionary keys when their elements are hashable.

```python
locations = {
    (17.38, 78.48): "Hyderabad"
}
```

---

## Q22. Can a tuple contain mutable objects?

### Answer

Yes.

```python
data = ([1, 2], 10)

data[0].append(3)

print(data)
```

Output:

```text
([1, 2, 3], 10)
```

The tuple itself is immutable, but the list inside it is mutable.

---

# 6. Sets

## Q23. What is a set?

### Answer

A set is an **unordered collection of unique elements**.

```python
numbers = {1, 2, 3, 3}

print(numbers)
```

The duplicate is removed.

Output:

```text
{1, 2, 3}
```

Sets are useful for:

- Removing duplicates
- Membership testing
- Mathematical set operations

---

## Q24. What are common set operations?

### Answer

Important operations include:

```python
union
intersection
difference
symmetric difference
```

Example:

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)
print(a & b)
print(a - b)
print(a ^ b)
```

Output:

```text
{1, 2, 3, 4, 5}
{3}
{1, 2}
{1, 2, 4, 5}
```

---

## Q25. Can a set contain a list?

### Answer

No.

A set requires its elements to be hashable, and lists are mutable and unhashable.

```python
s = {[1, 2]}
```

This produces:

```text
TypeError: unhashable type: 'list'
```

A tuple containing hashable elements can be placed in a set:

```python
s = {(1, 2)}
```

---

# 7. Dictionaries

## Q26. What is a dictionary?

### Answer

A dictionary stores data as **key-value pairs**.

```python
student = {
    "name": "Harsha",
    "age": 22,
    "course": "Python"
}
```

We access values using keys:

```python
print(student["name"])
```

---

## Q27. Can dictionary keys be lists?

### Answer

No.

Dictionary keys must be hashable.

This is invalid:

```python
data = {
    [1, 2]: "value"
}
```

But a tuple can be a key if its elements are hashable:

```python
data = {
    (1, 2): "value"
}
```

---

## Q28. What is the difference between `dict[key]` and `dict.get(key)`?

### Answer

If the key doesn't exist:

```python
data = {"name": "Harsha"}

print(data["age"])
```

This raises:

```text
KeyError
```

But:

```python
print(data.get("age"))
```

returns:

```text
None
```

We can provide a default:

```python
print(data.get("age", 0))
```

Output:

```text
0
```

---

## Q29. How do you iterate over a dictionary?

### Answer

```python
student = {
    "name": "Harsha",
    "age": 22
}

for key, value in student.items():
    print(key, value)
```

Useful methods:

```python
keys()
values()
items()
```

---

# 8. Conditionals

## Q30. What is the purpose of `if`, `elif`, and `else`?

### Answer

They are used for conditional execution.

```python
marks = 75

if marks >= 90:
    print("Excellent")
elif marks >= 60:
    print("Good")
else:
    print("Needs improvement")
```

Only the appropriate branch is executed.

---

## Q31. What is the difference between `if` and multiple `if` statements?

### Answer

With separate `if` statements, multiple conditions can execute.

```python
x = 10

if x > 5:
    print("A")

if x > 8:
    print("B")
```

Output:

```text
A
B
```

With `if` / `elif`, once a matching condition is found, the remaining conditions are skipped.

---

# 9. Loops

## Q32. What is the difference between `for` and `while` loops?

### Answer

A `for` loop is commonly used when iterating over a sequence or iterable.

```python
for i in range(5):
    print(i)
```

A `while` loop continues while a condition remains true.

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

---

## Q33. What is the difference between `break`, `continue`, and `pass`?

### Answer

### `break`

Terminates the loop.

```python
for i in range(5):
    if i == 3:
        break
    print(i)
```

### `continue`

Skips the current iteration.

```python
for i in range(5):
    if i == 3:
        continue
    print(i)
```

### `pass`

Does nothing. It is used as a placeholder.

```python
if True:
    pass
```

---

## Q34. What is `range()`?

### Answer

`range()` produces a sequence of numbers commonly used with loops.

```python
range(stop)
range(start, stop)
range(start, stop, step)
```

Example:

```python
for i in range(1, 6):
    print(i)
```

Output:

```text
1
2
3
4
5
```

The stop value is excluded.

---

# 10. Functions

## Q35. What is a function?

### Answer

A function is a reusable block of code designed to perform a particular task.

```python
def add(a, b):
    return a + b

result = add(10, 20)

print(result)
```

Functions improve:

- Code reuse
- Readability
- Maintainability
- Testing

---

## Q36. What is the difference between a parameter and an argument?

### Answer

A **parameter** is a variable defined in the function declaration.

```python
def greet(name):
    print(name)
```

Here, `name` is a parameter.

An **argument** is the actual value passed when calling the function.

```python
greet("Harsha")
```

`"Harsha"` is the argument.

---

## Q37. What is the difference between `return` and `print()`?

### Answer

`print()` displays a value.

`return` sends a value back to the caller.

```python
def add(a, b):
    print(a + b)

result = add(2, 3)
print(result)
```

Output:

```text
5
None
```

With `return`:

```python
def add(a, b):
    return a + b

result = add(2, 3)

print(result)
```

Output:

```text
5
```

---

## Q38. Can a function return multiple values?

### Answer

Yes. Python packages multiple returned values into a tuple.

```python
def calculate(a, b):
    return a + b, a - b

result = calculate(10, 5)

print(result)
```

Output:

```text
(15, 5)
```

We can unpack it:

```python
add, subtract = calculate(10, 5)
```

---

## Q39. What are default arguments?

### Answer

A default argument has a value that is used when the caller doesn't provide one.

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

---

# 11. `*args` and `**kwargs`

## Q40. What is `*args`?

### Answer

`*args` allows a function to accept a variable number of positional arguments.

```python
def add(*args):
    return sum(args)

print(add(1, 2))
print(add(1, 2, 3, 4))
```

Inside the function, `args` is a tuple.

---

## Q41. What is `**kwargs`?

### Answer

`**kwargs` allows a function to accept a variable number of keyword arguments.

```python
def display(**kwargs):
    print(kwargs)

display(name="Harsha", age=22)
```

Inside the function, `kwargs` is a dictionary.

---

## Q42. What is the difference between `*args` and `**kwargs`?

| Feature | `*args` | `**kwargs` |
|---|---|---|
| Arguments | Positional | Keyword |
| Internal type | Tuple | Dictionary |
| Example | `func(1, 2)` | `func(a=1, b=2)` |

---

# 12. Scope and Namespaces

## Q43. What is variable scope?

### Answer

Scope determines where a variable can be accessed.

Common scopes are:

- Local
- Enclosing
- Global
- Built-in

This is commonly remembered as **LEGB**.

```text
Local
Enclosing
Global
Built-in
```

---

## Q44. What is a local variable?

### Answer

A variable created inside a function is generally local to that function.

```python
def test():
    x = 10
    print(x)

test()
```

`x` cannot normally be accessed outside the function.

---

## Q45. What is a global variable?

### Answer

A variable defined outside functions is global within the module.

```python
x = 10

def test():
    print(x)

test()
```

The function can read the global variable.

---

## Q46. What are `global` and `nonlocal`?

### Answer

`global` allows a function to modify a global variable.

```python
x = 10

def change():
    global x
    x = 20

change()

print(x)
```

`nonlocal` is used inside a nested function to modify a variable from the enclosing function scope.

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

---

# 13. Lambda, Map, Filter, Reduce

## Q47. What is a lambda function?

### Answer

A lambda is a small anonymous function.

```python
square = lambda x: x * x

print(square(5))
```

Output:

```text
25
```

Lambda functions are useful when a small function is required temporarily.

---

## Q48. What is `map()`?

### Answer

`map()` applies a function to every item in an iterable.

```python
numbers = [1, 2, 3, 4]

result = list(map(lambda x: x * 2, numbers))

print(result)
```

Output:

```text
[2, 4, 6, 8]
```

---

## Q49. What is `filter()`?

### Answer

`filter()` selects elements for which a condition is true.

```python
numbers = [1, 2, 3, 4, 5]

result = list(filter(lambda x: x % 2 == 0, numbers))

print(result)
```

Output:

```text
[2, 4]
```

---

## Q50. What is `reduce()`?

### Answer

`reduce()` repeatedly applies a function to combine elements into a single result.

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

Output:

```text
10
```

---

# 14. Comprehensions

## Q51. What is list comprehension?

### Answer

List comprehension provides a concise way to create a list.

Normal approach:

```python
squares = []

for x in range(5):
    squares.append(x * x)

print(squares)
```

Using comprehension:

```python
squares = [x * x for x in range(5)]

print(squares)
```

Output:

```text
[0, 1, 4, 9, 16]
```

---

## Q52. Can we use conditions in list comprehension?

### Answer

Yes.

```python
even = [x for x in range(10) if x % 2 == 0]

print(even)
```

Output:

```text
[0, 2, 4, 6, 8]
```

---

## Q53. What other comprehensions exist in Python?

### Answer

Python supports:

- List comprehension
- Set comprehension
- Dictionary comprehension
- Generator expressions

### Examples

```python
squares = [x * x for x in range(5)]

unique = {x % 3 for x in range(10)}

data = {x: x * x for x in range(5)}

gen = (x * x for x in range(5))
```

---

# 15. Iterators and Generators

## Q54. What is an iterable?

### Answer

An iterable is an object that can return its elements one at a time.

Examples:

```python
list
tuple
string
set
dictionary
```

We can use them in a `for` loop.

```python
for item in [1, 2, 3]:
    print(item)
```

---

## Q55. What is an iterator?

### Answer

An iterator is an object that keeps track of its current position and provides elements one at a time using:

```python
__iter__()
__next__()
```

Example:

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

Output:

```text
10
20
30
```

After all elements are consumed, `next()` raises `StopIteration`.

---

## Q56. Write a custom iterator.

### Answer

```python
class Count:
    def __init__(self, limit):
        self.current = 1
        self.limit = limit

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= self.limit:
            value = self.current
            self.current += 1
            return value
        raise StopIteration


obj = Count(3)

for value in obj:
    print(value)
```

Output:

```text
1
2
3
```

### Interview explanation

> "An iterator implements `__iter__()` and `__next__()`. `__next__()` returns the next value and raises `StopIteration` when there are no more values."

---

## Q57. What is a generator?

### Answer

A generator is a convenient way to create an iterator using the `yield` keyword.

```python
def numbers():
    yield 1
    yield 2
    yield 3

for value in numbers():
    print(value)
```

Output:

```text
1
2
3
```

Generators produce values lazily instead of storing all values in memory at once.

---

## Q58. What is the difference between `return` and `yield`?

### Answer

`return` terminates the function and returns a value.

`yield` pauses the function and produces a value. The function can continue from where it stopped when requested again.

```python
def test():
    yield 1
    yield 2
```

This creates a generator.

### Important interview point

Generators are useful when dealing with:

- Large datasets
- Large files
- Streaming data
- Memory-sensitive processing

---

# 16. Exception Handling

## Q59. What is exception handling?

### Answer

Exception handling allows us to handle runtime errors without unnecessarily terminating the entire program.

Main keywords:

```python
try
except
else
finally
raise
```

Example:

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

---

## Q60. What is the purpose of `finally`?

### Answer

`finally` executes whether an exception occurs or not.

```python
try:
    print("Working")
except Exception:
    print("Error")
finally:
    print("Cleanup")
```

It is commonly useful for cleanup operations such as closing resources.

---

## Q61. What is the difference between `except` and `finally`?

### Answer

`except` handles an exception.

`finally` executes regardless of whether an exception occurred.

---

## Q62. What is `raise`?

### Answer

`raise` is used to explicitly raise an exception.

```python
age = -1

if age < 0:
    raise ValueError("Age cannot be negative")
```

---

## Q63. Can we have multiple `except` blocks?

### Answer

Yes.

```python
try:
    x = int(input("Enter number: "))
    result = 10 / x

except ValueError:
    print("Invalid number")

except ZeroDivisionError:
    print("Cannot divide by zero")
```

It is generally better to catch specific exceptions rather than using a broad `except` unnecessarily.

---

# 17. File Handling

## Q64. How do you open a file in Python?

### Answer

Use `open()`.

```python
file = open("data.txt", "r")
```

Common modes:

| Mode | Meaning |
|---|---|
| `r` | Read |
| `w` | Write |
| `a` | Append |
| `x` | Create |
| `b` | Binary |
| `t` | Text |

---

## Q65. Why is `with open()` preferred?

### Answer

A `with` statement automatically handles closing the file.

```python
with open("data.txt", "r") as file:
    content = file.read()

print(content)
```

This is safer and cleaner because the file is properly closed after the block.

---

## Q66. What is the difference between `read()`, `readline()`, and `readlines()`?

### Answer

`read()` reads the entire content.

```python
file.read()
```

`readline()` reads one line.

```python
file.readline()
```

`readlines()` reads lines and returns them as a list.

```python
file.readlines()
```

---

# 18. Modules and Packages

## Q67. What is a module?

### Answer

A module is a Python file containing code such as:

- Functions
- Classes
- Variables
- Statements

For example:

```text
math_utils.py
```

can contain:

```python
def add(a, b):
    return a + b
```

Then another file can import it:

```python
import math_utils

print(math_utils.add(10, 20))
```

---

## Q68. What is a package?

### Answer

A package is a way of organizing related Python modules into a directory structure.

Example:

```text
project/
    main.py
    utilities/
        module1.py
        module2.py
```

Packages help organize larger applications.

---

## Q69. What is the purpose of `if __name__ == "__main__"`?

### Answer

It allows code to run only when the file is executed directly, rather than when it is imported.

```python
def greet():
    print("Hello")


if __name__ == "__main__":
    greet()
```

If the file is run directly, `greet()` executes.

If it is imported into another module, the guarded code does not execute automatically.

---

# 19. Decorators

## Q70. What is a decorator?

### Answer

A decorator is a function that modifies or extends the behavior of another function without changing its original code.

Example:

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

---

## Q71. Why are decorators useful?

### Answer

Decorators are commonly used for:

- Logging
- Authentication
- Authorization
- Timing
- Validation
- Caching
- Access control

They are especially common in web frameworks.

---

## Q72. What does `@decorator` mean?

### Answer

This:

```python
@decorator
def greet():
    pass
```

is essentially equivalent to:

```python
def greet():
    pass

greet = decorator(greet)
```

---

# 20. Shallow Copy and Deep Copy

## Q73. What is the difference between assignment and copying?

### Answer

Assignment creates another reference to the same object.

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
```

Output:

```text
[1, 2, 3, 4]
```

Both variables refer to the same list.

---

## Q74. What is a shallow copy?

### Answer

A shallow copy creates a new outer object, but nested objects may still be shared.

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.copy(a)

b[0].append(5)

print(a)
print(b)
```

The nested list is shared.

---

## Q75. What is a deep copy?

### Answer

A deep copy recursively copies nested objects.

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.deepcopy(a)

b[0].append(5)

print(a)
print(b)
```

Output:

```text
[[1, 2], [3, 4]]
[[1, 2, 5], [3, 4]]
```

---

# 21. Object-Oriented Programming

## Q76. What is OOP?

### Answer

Object-oriented programming is a programming paradigm based on objects and classes.

The four commonly discussed pillars are:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

---

## Q77. What is a class?

### Answer

A class is a blueprint for creating objects.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student = Student("Harsha")

student.display()
```

---

## Q78. What is an object?

### Answer

An object is an instance of a class.

```python
class Student:
    pass


student1 = Student()
student2 = Student()
```

Here, `student1` and `student2` are objects of the `Student` class.

---

## Q79. What is `self`?

### Answer

`self` refers to the current object instance.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)
```

`self.name` refers to the `name` belonging to that particular object.

---

## Q80. What is `__init__()`?

### Answer

`__init__()` is an initializer method that runs when an object is created.

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Harsha")
```

It is commonly used to initialize instance attributes.

---

## Q81. What is inheritance?

### Answer

Inheritance allows one class to reuse or extend the functionality of another class.

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    def bark(self):
        print("Dog barking")


dog = Dog()

dog.speak()
dog.bark()
```

---

## Q82. What is method overriding?

### Answer

Method overriding occurs when a child class provides its own implementation of a method defined in the parent class.

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    def speak(self):
        print("Bark")


dog = Dog()
dog.speak()
```

Output:

```text
Bark
```

---

## Q83. What is polymorphism?

### Answer

Polymorphism means the same interface or method name can behave differently depending on the object.

```python
class Dog:
    def speak(self):
        print("Bark")


class Cat:
    def speak(self):
        print("Meow")


for animal in [Dog(), Cat()]:
    animal.speak()
```

Output:

```text
Bark
Meow
```

---

## Q84. What is encapsulation?

### Answer

Encapsulation means keeping data and related behavior together and controlling how internal data is accessed.

Python commonly uses naming conventions such as:

```python
_name
__name
```

Example:

```python
class Account:
    def __init__(self):
        self.__balance = 1000

    def get_balance(self):
        return self.__balance
```

---

## Q85. What is abstraction?

### Answer

Abstraction means exposing essential functionality while hiding implementation details.

Python can implement abstraction using the `abc` module.

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def speak(self):
        pass


class Dog(Animal):

    def speak(self):
        print("Bark")
```

---

## Q86. What is the difference between instance, class, and static methods?

### Answer

### Instance method

Uses `self`.

```python
class Student:

    def display(self):
        print("Instance method")
```

### Class method

Uses `cls` and is declared using `@classmethod`.

```python
class Student:

    school = "ABC"

    @classmethod
    def show_school(cls):
        print(cls.school)
```

### Static method

Does not require `self` or `cls`.

```python
class Math:

    @staticmethod
    def add(a, b):
        return a + b
```

---

# 22. Python Coding Questions — Core Concepts

## Q87. Write a program to reverse a string.

### Answer

```python
text = "Python"

print(text[::-1])
```

Output:

```text
nohtyP
```

### Without slicing

```python
text = "Python"

result = ""

for char in text:
    result = char + result

print(result)
```

---

## Q88. Check whether a string is a palindrome.

### Answer

```python
text = "madam"

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not palindrome")
```

---

## Q89. Count the frequency of characters in a string.

### Answer

```python
text = "python"

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

print(frequency)
```

Output:

```text
{'p': 1, 'y': 1, 't': 1, 'h': 1, 'o': 1, 'n': 1}
```

### Important concept tested

This question tests:

- Strings
- Loops
- Dictionaries
- `get()`

---

## Q90. Remove duplicates from a list.

### Simple solution

```python
numbers = [1, 2, 2, 3, 3, 4]

result = list(set(numbers))

print(result)
```

### Important note

Using a set does not preserve the original ordering as a general guarantee in the way a list does.

If preserving order matters:

```python
numbers = [1, 2, 2, 3, 3, 4]

result = list(dict.fromkeys(numbers))

print(result)
```

Output:

```text
[1, 2, 3, 4]
```

---

## Q91. Find the largest element in a list without using `max()`.

### Answer

```python
numbers = [10, 5, 30, 20]

largest = numbers[0]

for number in numbers:
    if number > largest:
        largest = number

print(largest)
```

Output:

```text
30
```

---

## Q92. Count even and odd numbers in a list.

### Answer

```python
numbers = [1, 2, 3, 4, 5, 6]

even = 0
odd = 0

for number in numbers:
    if number % 2 == 0:
        even += 1
    else:
        odd += 1

print("Even:", even)
print("Odd:", odd)
```

---

## Q93. Find the sum of elements in a list without using `sum()`.

### Answer

```python
numbers = [1, 2, 3, 4]

total = 0

for number in numbers:
    total += number

print(total)
```

Output:

```text
10
```

---

## Q94. Find the second largest number in a list.

### Answer

```python
numbers = [10, 20, 5, 30, 25]

unique_numbers = list(set(numbers))
unique_numbers.sort()

print(unique_numbers[-2])
```

Output:

```text
25
```

### Interview follow-up

The interviewer may ask:

> "Can you do it without sorting?"

Be prepared to explain a one-pass approach using two variables such as `largest` and `second_largest`.

---

## Q95. Swap two variables without using a temporary variable.

### Answer

```python
a = 10
b = 20

a, b = b, a

print(a, b)
```

Output:

```text
20 10
```

Python supports tuple unpacking for this.

---

## Q96. Count the digits of a number.

### Answer

```python
n = 9474

count = 0

while n > 0:
    n = n // 10
    count += 1

print(count)
```

Output:

```text
4
```

### Interview follow-up

The interviewer may ask:

> "Is `lastdigit = n % 10` necessary?"

No. If we only need the number of digits, it is unnecessary.

We only need:

```python
n = n // 10
```

because each integer division by `10` removes one digit.

---

## Q97. Reverse a number.

### Answer

```python
n = 1234

reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n = n // 10

print(reverse)
```

Output:

```text
4321
```

---

## Q98. Check whether a number is a palindrome.

### Answer

```python
n = 121

original = n
reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n = n // 10

if original == reverse:
    print("Palindrome")
else:
    print("Not palindrome")
```

---

## Q99. Check whether a number is an Armstrong number.

### Answer

An Armstrong number is a number equal to the sum of its digits raised to the power of the number of digits.

For example:

```text
153 = 1³ + 5³ + 3³
```

Code:

```python
n = 153

original = n
digits = len(str(n))
total = 0

while n > 0:
    digit = n % 10
    total += digit ** digits
    n //= 10

if total == original:
    print("Armstrong number")
else:
    print("Not Armstrong number")
```

---

# 23. Output-Based Python Questions

## Q100. What is the output?

```python
x = [1, 2, 3]
y = x

y.append(4)

print(x)
```

### Answer

```text
[1, 2, 3, 4]
```

### Why?

`x` and `y` refer to the same list object.

---

## Q101. What is the output?

```python
x = [1, 2, 3]
y = x.copy()

y.append(4)

print(x)
print(y)
```

### Answer

```text
[1, 2, 3]
[1, 2, 3, 4]
```

`copy()` creates a new outer list.

---

## Q102. What is the output?

```python
a = 10

def test():
    a = 20
    print(a)

test()
print(a)
```

### Answer

```text
20
10
```

The `a` inside the function is local.

---

## Q103. What is the output?

```python
x = [1, 2, 3]

print(x[-1])
print(x[::-1])
```

### Answer

```text
3
[3, 2, 1]
```

---

## Q104. What is the output?

```python
numbers = [1, 2, 3, 4, 5]

result = [x * 2 for x in numbers if x % 2 == 0]

print(result)
```

### Answer

```text
[4, 8]
```

Only even numbers are selected, then multiplied by `2`.

---

## Q105. What is the output?

```python
a = "Python"
b = "Python"

print(a == b)
print(a is b)
```

### Answer

The first output is:

```text
True
```

The result of `is` should not be relied upon for string value comparison because object interning/identity behavior can vary with context.

The correct interview point is:

> Use `==` to compare string values, not `is`.

---

## Q106. What is the output?

```python
x = (1, 2, 3)

a, b, c = x

print(a)
print(b)
print(c)
```

### Answer

```text
1
2
3
```

This is tuple unpacking.

---

## Q107. What is the output?

```python
x = [1, 2, 3]

print(x.append(4))
```

### Answer

```text
None
```

`append()` modifies the list in place and returns `None`.

The list becomes:

```python
[1, 2, 3, 4]
```

---

## Q108. What is the output?

```python
x = [1, 2, 3]

print(x.pop())
print(x)
```

### Answer

```text
3
[1, 2]
```

`pop()` removes and returns the last element by default.

---

# 24. Important Python Internals — Interview-Level Only

> **Do not spend significant preparation time on deep Python internals.**  
> Know these basic explanations because an interviewer may ask them as follow-ups.

## Q109. What is a namespace?

### Answer

A namespace is a mapping between names and objects.

Examples include:

- Local namespace
- Global namespace
- Built-in namespace

Python uses namespaces to avoid naming conflicts.

---

## Q110. What is LEGB?

### Answer

LEGB describes the order Python uses when looking for a name:

```text
L → Local
E → Enclosing
G → Global
B → Built-in
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

Python finds the local `x` first.

---

## Q111. What is garbage collection?

### Answer

Python automatically manages memory and can remove objects that are no longer reachable.

CPython primarily uses **reference counting**, along with a cyclic garbage collector to handle reference cycles.

For an interview, the safe explanation is:

> "Python provides automatic memory management. CPython uses reference counting and garbage collection to reclaim memory from objects that are no longer needed."

---

## Q112. What is reference counting?

### Answer

Reference counting keeps track of how many references point to an object.

When an object's reference count reaches zero, CPython can generally reclaim that object's memory.

You do not normally need to manually manage this.

---

# 25. Python Memory and Object Behavior

## Q113. How are variables stored in Python?

### Answer

Python variables are names that refer to objects.

```python
x = 10
```

Conceptually:

```text
x ─────→ 10
```

If we do:

```python
y = x
```

then both names can refer to the same object:

```text
x ─────→ 10
y ─────→ 10
```

This is important when understanding mutable objects.

---

## Q114. Why can changing one list change another variable's list?

### Answer

Because both variables may refer to the same mutable object.

```python
a = [1, 2]
b = a

b.append(3)

print(a)
```

Output:

```text
[1, 2, 3]
```

To create a separate outer list:

```python
b = a.copy()
```

---

# 26. Important Tricky Questions

## Q115. What is the difference between `sort()` and `sorted()`?

### Answer

`sort()` modifies the list in place and returns `None`.

```python
numbers = [3, 1, 2]

numbers.sort()

print(numbers)
```

`sorted()` returns a new sorted list.

```python
numbers = [3, 1, 2]

result = sorted(numbers)

print(numbers)
print(result)
```

Output:

```text
[3, 1, 2]
[1, 2, 3]
```

---

## Q116. What is the difference between `remove()`, `pop()`, and `del`?

### Answer

### `remove()`

Removes by value.

```python
numbers.remove(20)
```

### `pop()`

Removes by index and returns the element.

```python
value = numbers.pop(1)
```

### `del`

Deletes an element, slice, or variable.

```python
del numbers[1]
```

---

## Q117. What is the difference between `copy()` and `deepcopy()`?

### Answer

`copy()` creates a shallow copy.

`deepcopy()` recursively copies nested objects.

```python
import copy

a = [[1, 2]]

b = copy.copy(a)
c = copy.deepcopy(a)
```

For nested mutable structures, `deepcopy()` provides independent nested objects.

---

## Q118. What is the mutable default argument problem?

### Answer

Using a mutable object such as a list as a default argument can cause values to persist between function calls.

Avoid:

```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

A safer approach is:

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items
```

### Interview point

Default arguments are evaluated when the function is defined, not each time the function is called.

---

## Q119. What is duck typing?

### Answer

Duck typing means Python generally focuses on whether an object supports the required behavior rather than requiring a specific class type.

For example:

```python
class Dog:
    def speak(self):
        print("Bark")


class Person:
    def speak(self):
        print("Hello")


def make_speak(obj):
    obj.speak()


make_speak(Dog())
make_speak(Person())
```

Both objects work because they provide the required `speak()` method.

---

# 27. Python Functions — Advanced Interview Questions

## Q120. Are functions first-class objects in Python?

### Answer

Yes.

Functions can be:

- Assigned to variables
- Passed as arguments
- Returned from functions
- Stored in collections

Example:

```python
def greet():
    return "Hello"


func = greet

print(func())
```

Output:

```text
Hello
```

This concept is important for understanding decorators, callbacks, and functional programming.

---

## Q121. What is a closure?

### Answer

A closure occurs when an inner function remembers variables from its enclosing function even after the enclosing function has finished executing.

```python
def outer(message):

    def inner():
        print(message)

    return inner


func = outer("Hello")

func()
```

Output:

```text
Hello
```

The inner function retains access to `message`.

---

## Q122. What is recursion?

### Answer

Recursion is when a function calls itself.

Example:

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

A recursive function needs a proper base condition to stop.

---

# 28. Python Modules and Imports

## Q123. What is the difference between `import module` and `from module import function`?

### Answer

Using:

```python
import math

print(math.sqrt(16))
```

imports the module and accesses the function through the module.

Using:

```python
from math import sqrt

print(sqrt(16))
```

imports the specific function directly.

---

## Q124. What is an alias in imports?

### Answer

An alias gives another name to an imported module or function.

```python
import pandas as pd
```

Here, `pd` is an alias for `pandas`.

Another example:

```python
import numpy as np
```

---

# 29. Python Exception Questions

## Q125. Why should we avoid using a bare `except` everywhere?

### Answer

A broad exception handler can hide unexpected problems.

Instead of:

```python
try:
    risky_operation()
except:
    pass
```

prefer specific handling:

```python
try:
    risky_operation()
except ValueError:
    print("Invalid value")
```

This makes debugging and maintenance easier.

---

## Q126. Can we use `else` with `try-except`?

### Answer

Yes.

The `else` block executes when no exception occurs.

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print("Success:", result)
finally:
    print("Done")
```

Output:

```text
Success: 5.0
Done
```

---

# 30. Common Python Interview Coding Questions

## Q127. Find the frequency of elements in a list.

### Answer

```python
numbers = [1, 2, 2, 3, 3, 3]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

print(frequency)
```

Output:

```text
{1: 1, 2: 2, 3: 3}
```

---

## Q128. Find duplicate elements in a list.

### Answer

```python
numbers = [1, 2, 3, 2, 4, 3]

seen = set()
duplicates = set()

for number in numbers:
    if number in seen:
        duplicates.add(number)
    else:
        seen.add(number)

print(duplicates)
```

Output:

```text
{2, 3}
```

---

## Q129. Find common elements between two lists.

### Answer

```python
a = [1, 2, 3, 4]
b = [3, 4, 5, 6]

common = list(set(a) & set(b))

print(common)
```

Output:

```text
[3, 4]
```

---

## Q130. Count vowels in a string.

### Answer

```python
text = "python programming"

vowels = "aeiou"
count = 0

for char in text.lower():
    if char in vowels:
        count += 1

print(count)
```

---

## Q131. Find the first non-repeating character.

### Answer

```python
text = "swiss"

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

for char in text:
    if frequency[char] == 1:
        print(char)
        break
```

Output:

```text
w
```

### Concepts tested

- Dictionary
- String iteration
- Frequency counting
- `break`

---

## Q132. Find the longest word in a sentence.

### Answer

```python
sentence = "Python is easy to learn"

words = sentence.split()

longest = ""

for word in words:
    if len(word) > len(longest):
        longest = word

print(longest)
```

Output:

```text
Python
```

---

## Q133. Check whether two strings are anagrams.

### Answer

```python
a = "listen"
b = "silent"

if sorted(a) == sorted(b):
    print("Anagrams")
else:
    print("Not anagrams")
```

Output:

```text
Anagrams
```

---

# 31. Python Concepts Interviewers Commonly Combine

## Q134. How would you process a large file without loading everything into memory?

### Answer

Use iteration or a generator so that data can be processed incrementally.

```python
with open("large_file.txt", "r") as file:
    for line in file:
        process(line)
```

This is more memory-efficient than:

```python
data = file.read()
```

for a very large file.

### Real-world relevance

This concept is especially useful in **Data Engineering**, where files can be very large.

---

## Q135. Why are generators useful in data processing?

### Answer

Generators produce values lazily.

Instead of creating a huge list:

```python
numbers = [x * 2 for x in range(1000000)]
```

we can use:

```python
numbers = (x * 2 for x in range(1000000))
```

Values are generated as needed.

### Interview answer

> "Generators are useful for memory-efficient processing because they produce one value at a time instead of storing the complete result in memory."

---

## Q136. How would you remove duplicates while preserving order?

### Answer

A simple Python approach is:

```python
numbers = [3, 1, 3, 2, 1, 4]

result = list(dict.fromkeys(numbers))

print(result)
```

Output:

```text
[3, 1, 2, 4]
```

---

# 32. Python for Data Engineering Interviews

## Q137. Why is Python widely used in Data Engineering?

### Answer

Python has a large ecosystem for data processing and integration.

Common tools include:

```text
PySpark
Pandas
NumPy
SQLAlchemy
Requests
Airflow
AWS SDKs
```

Python is useful for:

- Data ingestion
- ETL pipelines
- Transformation
- API integration
- Automation
- Data validation
- Cloud workflows

---

## Q138. What is ETL?

### Answer

ETL stands for:

```text
Extract → Transform → Load
```

### Extract

Get data from sources such as:

- APIs
- CSV files
- Databases
- Cloud storage

### Transform

Clean or modify the data.

Examples:

- Remove duplicates
- Handle missing values
- Change data types
- Filter records
- Join datasets

### Load

Store the transformed data in a destination such as:

- Database
- Data warehouse
- S3
- Other storage systems

---

## Q139. What is the difference between a list and a generator when processing data?

### Answer

A list stores all elements in memory.

A generator produces elements one at a time.

```python
numbers_list = [x for x in range(1000000)]

numbers_generator = (x for x in range(1000000))
```

For large datasets, generators can reduce memory usage.

---

# 33. Practical Interview Questions

## Q140. How would you handle invalid data in a Python program?

### Answer

I would validate the data and handle expected exceptions explicitly.

For example:

```python
def convert_age(value):
    try:
        age = int(value)

        if age < 0:
            raise ValueError("Age cannot be negative")

        return age

    except ValueError as e:
        print("Invalid age:", e)
```

In a real application, I would also decide whether the invalid record should be:

- Rejected
- Logged
- Corrected
- Sent to a separate error location

---

## Q141. How do you make Python code more readable?

### Answer

I would focus on:

- Meaningful variable names
- Small functions
- Proper indentation
- Avoiding unnecessary duplication
- Appropriate comments
- Following PEP 8
- Using clear data structures
- Handling exceptions properly
- Keeping functions focused on one responsibility

Example:

```python
def calculate_total_price(price, tax):
    return price + (price * tax)
```

is easier to understand than putting the entire calculation into one large block.

---

## Q142. How do you debug a Python program?

### Answer

My usual approach would be:

1. Reproduce the problem.
2. Read the error message and traceback.
3. Identify the line causing the issue.
4. Check variable values and assumptions.
5. Use debugging tools or controlled print statements when appropriate.
6. Fix the root cause.
7. Test the affected case and related cases.

For larger applications, logging and a debugger are preferable to relying only on `print()`.

---

# 34. Rapid-Fire Questions

## Q143. What is PEP 8?

### Answer

PEP 8 is the main style guide for Python code. It provides recommendations for writing readable and consistent Python code.

---

## Q144. What is indentation used for in Python?

### Answer

Indentation defines code blocks.

```python
if True:
    print("Hello")
```

Unlike languages that commonly use braces, Python uses indentation to define blocks.

---

## Q145. What is a docstring?

### Answer

A docstring is a string used to document a module, class, or function.

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

---

## Q146. What is unpacking?

### Answer

Unpacking assigns elements from an iterable to multiple variables.

```python
numbers = [10, 20, 30]

a, b, c = numbers

print(a, b, c)
```

Output:

```text
10 20 30
```

Extended unpacking:

```python
a, *middle, b = [1, 2, 3, 4, 5]

print(a)
print(middle)
print(b)
```

Output:

```text
1
[2, 3, 4]
5
```

---

## Q147. What is the walrus operator?

### Answer

The `:=` operator allows an expression to assign a value to a variable.

Example:

```python
if (length := len("Python")) > 5:
    print(length)
```

Output:

```text
6
```

It should be used only when it makes the code clearer.

---

## Q148. What is the difference between `range` and `list(range())`?

### Answer

`range()` represents a range object and generates values as needed.

```python
r = range(5)
```

`list(range(5))` creates an actual list containing the values.

```python
numbers = list(range(5))
```

Output:

```text
[0, 1, 2, 3, 4]
```

---

# 35. Most Important Follow-Up Questions

These are questions an interviewer can ask immediately after your first answer.

## Q149. You said Python is dynamically typed. Can you explain with an example?

### Answer

```python
x = 10
print(type(x))

x = "Python"
print(type(x))
```

The same variable name can refer to objects of different types at runtime.

---

## Q150. You said lists are mutable. Show me.

### Answer

```python
numbers = [1, 2, 3]

numbers.append(4)

print(numbers)
```

The existing list is modified.

---

## Q151. You said tuples are immutable. Show me.

### Answer

```python
numbers = (1, 2, 3)

numbers[0] = 10
```

This raises:

```text
TypeError
```

---

## Q152. You said dictionaries use key-value pairs. What happens if a key doesn't exist?

### Answer

Using:

```python
data["missing"]
```

raises `KeyError`.

Using:

```python
data.get("missing")
```

returns `None` unless another default is provided.

---

## Q153. You said generators save memory. Why?

### Answer

A generator does not create the entire result at once. It produces values lazily as they are requested.

```python
def numbers():
    for i in range(1000000):
        yield i
```

Only the required values are produced during iteration.

---

## Q154. You said decorators modify functions. Can you write one?

### Answer

```python
def logger(func):

    def wrapper():
        print("Function started")
        func()
        print("Function finished")

    return wrapper


@logger
def greet():
    print("Hello")


greet()
```

---

## Q155. You said Python supports OOP. What are the four pillars?

### Answer

The commonly discussed four pillars are:

```text
Encapsulation
Inheritance
Polymorphism
Abstraction
```

---

# 36. Questions You Should Be Able to Code Without Help

Before an interview, make sure you can write these without looking at the answer.

### Strings

1. Reverse a string.
2. Check palindrome.
3. Count vowels.
4. Count character frequency.
5. Find first non-repeating character.
6. Check anagrams.
7. Find longest word.

### Lists

8. Find largest number.
9. Find smallest number.
10. Find second largest.
11. Remove duplicates.
12. Count duplicates.
13. Find common elements.
14. Reverse a list.
15. Sum list elements.
16. Count even and odd numbers.

### Numbers

17. Count digits.
18. Reverse a number.
19. Check palindrome number.
20. Check Armstrong number.
21. Find factorial.
22. Check prime number.
23. Generate Fibonacci series.

### Dictionaries/Sets

24. Character frequency.
25. Element frequency.
26. Remove duplicates.
27. Find common elements.
28. Group/count values using a dictionary.

### Core Python

29. Write a custom iterator.
30. Write a generator.
31. Write a decorator.
32. Demonstrate shallow vs deep copy.
33. Demonstrate inheritance.
34. Demonstrate polymorphism.
35. Demonstrate exception handling.
36. Read and process a file line by line.

---

# 37. Essential Coding Examples

## Factorial

```python
n = 5

factorial = 1

for i in range(1, n + 1):
    factorial *= i

print(factorial)
```

Output:

```text
120
```

---

## Prime Number

```python
n = 17

if n < 2:
    print("Not prime")
else:
    is_prime = True

    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime")
    else:
        print("Not prime")
```

---

## Fibonacci Series

```python
n = 7

a = 0
b = 1

for _ in range(n):
    print(a, end=" ")
    a, b = b, a + b
```

Output:

```text
0 1 1 2 3 5 8
```

---

# 38. Final Interview Priority

## 🔥 Tier 1 — Prepare Very Well

These should be your strongest areas:

- Python basics
- Data types
- Mutable vs immutable
- List
- Tuple
- Set
- Dictionary
- Strings
- Conditions
- Loops
- Functions
- Parameters vs arguments
- `return` vs `print`
- `*args` and `**kwargs`
- Scope / LEGB
- Lambda
- List comprehensions
- Exception handling
- File handling
- OOP
- Inheritance
- Polymorphism
- Encapsulation
- Abstraction
- `is` vs `==`
- Shallow vs deep copy
- Core Python coding questions
- Output-based questions

---

## 🟡 Tier 2 — Know and Practice

- Iterators
- Generators
- Decorators
- `map()`
- `filter()`
- `reduce()`
- Modules
- Packages
- Closures
- Recursion
- Context managers
- `__name__ == "__main__"`
- `sort()` vs `sorted()`
- Mutable default arguments

---

## 🟢 Tier 3 — Quick Revision Only

Do not spend excessive time here:

- Reference counting details
- Garbage collector internals
- Bytecode internals
- CPython implementation details
- Python interpreter internals
- Very obscure language behavior

Know the basic explanation, but prioritize practical Python.

---

# 39. Last-Minute Revision Checklist

Before entering a Python interview, make sure you can confidently answer:

- What is Python?
- Why is Python popular?
- Is Python interpreted or compiled?
- What does dynamically typed mean?
- Is Python strongly typed?
- What are Python's data types?
- Mutable vs immutable?
- List vs tuple?
- List vs set?
- Set vs dictionary?
- `is` vs `==`?
- `append()` vs `extend()`?
- `remove()` vs `pop()`?
- `sort()` vs `sorted()`?
- `dict[key]` vs `dict.get()`?
- What is `None`?
- What are truthy/falsy values?
- What is a function?
- Parameter vs argument?
- `return` vs `print()`?
- Default arguments?
- `*args` vs `**kwargs`?
- What is scope?
- What is LEGB?
- `global` vs `nonlocal`?
- What is lambda?
- `map()`?
- `filter()`?
- `reduce()`?
- List comprehension?
- Dictionary comprehension?
- Iterable vs iterator?
- Write a custom iterator?
- What is a generator?
- `yield` vs `return`?
- What is exception handling?
- `try`, `except`, `else`, `finally`?
- What is `raise`?
- How do you read a file?
- Why use `with open()`?
- What is a module?
- What is a package?
- What is `__name__ == "__main__"`?
- What is a decorator?
- Write a decorator?
- Shallow copy vs deep copy?
- Assignment vs copy?
- What is OOP?
- What is a class?
- What is an object?
- What is `self`?
- What is `__init__()`?
- What is inheritance?
- What is polymorphism?
- What is encapsulation?
- What is abstraction?
- Instance vs class vs static method?
- What is a closure?
- What is recursion?
- What is garbage collection?
- How does Python manage memory?
- Reverse a string?
- Palindrome?
- Character frequency?
- Remove duplicates?
- Find largest/second-largest?
- Count digits?
- Reverse a number?
- Armstrong number?
- Prime number?
- Fibonacci?
- Factorial?
- Write a custom iterator?
- Write a generator?
- Write a decorator?
- Process a large file efficiently?

---

# 40. Final Preparation Rule

You **do not need to memorize all 150+ questions word-for-word**.

The purpose of this file is to make sure that the important interview areas are covered.

Your preparation should be:

```text
Understand the concept
        ↓
See the example
        ↓
Write the code yourself
        ↓
Explain it in simple English
        ↓
Prepare for the follow-up question
```

For example, don't only memorize:

> "A generator uses yield."

Be able to explain:

> "A generator is a function that produces values one at a time using `yield`. It pauses its execution and resumes when the next value is requested. This makes it useful for memory-efficient processing of large data."

And be able to write:

```python
def numbers():
    for i in range(5):
        yield i


for number in numbers():
    print(number)
```

This is the level of preparation that is most useful in an interview.

---

# 41. The Most Important Principle

For a Python interview, focus on **understanding rather than memorizing definitions**.

If an interviewer asks:

> "What is a list?"

You should be able to continue naturally if they ask:

> "Is it mutable?"

Then:

> "What is the difference between a list and tuple?"

Then:

> "What happens when you assign one list to another variable?"

Then:

> "How would you make a copy?"

Then:

> "What is shallow copy?"

Then:

> "What about nested lists?"

This is how interviewers often test whether you genuinely understand Python.

Therefore, your main preparation target should be:

**Concept → Example → Code → Output → Follow-up → Real-world use**

---

# 42. Final High-Value Real-World Connections

## Lists

Useful when working with an ordered collection of items.

```python
records = ["record1", "record2", "record3"]
```

## Dictionaries

Useful for structured key-value data.

```python
user = {
    "name": "Harsha",
    "role": "Developer"
}
```

## Sets

Useful for uniqueness and membership testing.

```python
unique_ids = {101, 102, 103}
```

## Generators

Useful for processing large amounts of data incrementally.

```python
def read_records():
    for record in records:
        yield record
```

## Exception Handling

Useful when external operations can fail.

```python
try:
    process_data()
except ValueError:
    handle_invalid_data()
```

## Decorators

Useful for cross-cutting behavior such as logging or authentication.

```python
@authenticate
def get_data():
    pass
```

## OOP

Useful for structuring larger applications around related data and behavior.

```python
class Employee:
    def __init__(self, name):
        self.name = name
```

---

# 43. One-Minute Python Revision

If you have only a few minutes before an interview, remember:

```text
Python
├── Dynamically typed
├── Strongly typed
├── High-level
├── Multi-paradigm
└── Automatic memory management

Collections
├── List → ordered, mutable
├── Tuple → ordered, immutable
├── Set → unique elements
└── Dict → key-value pairs

Functions
├── parameters / arguments
├── return
├── default arguments
├── *args
├── **kwargs
├── lambda
└── scope / LEGB

Advanced Core
├── comprehensions
├── iterators
├── generators
├── decorators
├── exceptions
├── modules
├── packages
└── copy

OOP
├── class
├── object
├── inheritance
├── polymorphism
├── encapsulation
└── abstraction

Coding
├── strings
├── lists
├── dictionaries
├── numbers
├── loops
└── small core-Python programs
```

---

# 44. Final Interview Mindset

If you don't know an advanced question, don't try to invent an answer.

A professional response is:

> "I haven't worked deeply with that concept yet, but I understand the basic idea. I would be happy to learn and explore it further."

For concepts you **do** know, explain them using:

```text
Definition
+
Simple example
+
Small code
+
Practical use
```

That is much stronger than giving a memorized one-line definition.

**This file should be your main Python interview revision file. The individual topic files are reference material; this file is where you should put the majority of your preparation effort.**