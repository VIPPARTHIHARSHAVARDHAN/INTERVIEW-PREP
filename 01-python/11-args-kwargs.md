# Python `*args` and `**kwargs` — Interview Preparation

## 1. What Are `*args` and `**kwargs`?

`*args` and `**kwargs` are used when a function needs to accept a variable number of arguments.

- `*args` → variable number of **positional arguments**
- `**kwargs` → variable number of **keyword arguments**

```python
def show(*args, **kwargs):
    print(args)
    print(kwargs)

show(10, 20, 30, name="Harsha", age=21)
```

Output:

```text
(10, 20, 30)
{'name': 'Harsha', 'age': 21}
```

### Interview Answer

> `*args` allows a function to accept any number of positional arguments, which are collected into a tuple. `**kwargs` allows a function to accept any number of keyword arguments, which are collected into a dictionary.

---

# 2. What Does `*` Mean in `*args`?

The `*` tells Python to collect multiple positional arguments into one variable.

```python
def add(*args):
    print(args)

add(10, 20, 30, 40)
```

Output:

```text
(10, 20, 30, 40)
```

The name `args` is only a convention. We can use another valid variable name:

```python
def add(*numbers):
    print(numbers)

add(10, 20, 30)
```

Output:

```text
(10, 20, 30)
```

The important part is `*`, not the name `args`.

---

# 3. What Does `**` Mean in `**kwargs`?

The `**` tells Python to collect multiple keyword arguments into a dictionary.

```python
def show(**data):
    print(data)

show(name="Harsha", age=21, city="Hyderabad")
```

Output:

```text
{'name': 'Harsha', 'age': 21, 'city': 'Hyderabad'}
```

Again, `kwargs` is only a conventional name.

This is also valid:

```python
def show(**data):
    print(data)
```

---

# 4. Why Do We Use `*args`?

Use `*args` when the number of positional arguments is not known beforehand.

Without `*args`:

```python
def add(a, b):
    return a + b
```

This only accepts two arguments.

With `*args`:

```python
def add(*args):
    return sum(args)

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

### Interview Answer

> I use `*args` when a function needs to support a variable number of positional inputs without defining every parameter individually.

---

# 5. What Type Is `args` Inside the Function?

`args` is a tuple.

```python
def show(*args):
    print(type(args))

show(10, 20, 30)
```

Output:

```text
<class 'tuple'>
```

Therefore:

```python
args[0]
args[1]
```

can be used to access individual arguments.

---

# 6. What Type Is `kwargs` Inside the Function?

`kwargs` is a dictionary.

```python
def show(**kwargs):
    print(type(kwargs))

show(name="Harsha", age=21)
```

Output:

```text
<class 'dict'>
```

Therefore, we can use dictionary operations:

```python
def show(**kwargs):
    print(kwargs["name"])

show(name="Harsha")
```

Output:

```text
Harsha
```

---

# 7. What Is the Difference Between `*args` and `**kwargs`?

| Feature | `*args` | `**kwargs` |
|---|---|---|
| Purpose | Variable positional arguments | Variable keyword arguments |
| Internal type | Tuple | Dictionary |
| Syntax | `*args` | `**kwargs` |
| Example | `func(10, 20)` | `func(name="Harsha")` |

Example:

```python
def test(*args, **kwargs):
    print("args:", args)
    print("kwargs:", kwargs)

test(10, 20, name="Harsha", age=21)
```

Output:

```text
args: (10, 20)
kwargs: {'name': 'Harsha', 'age': 21}
```

### Interview Answer

> `*args` collects extra positional arguments into a tuple, while `**kwargs` collects extra keyword arguments into a dictionary.

---

# 8. Can We Use `*args` and `**kwargs` Together?

Yes.

```python
def display(*args, **kwargs):
    print("Positional:", args)
    print("Keyword:", kwargs)

display(10, 20, 30, name="Harsha", city="Hyderabad")
```

Output:

```text
Positional: (10, 20, 30)
Keyword: {'name': 'Harsha', 'city': 'Hyderabad'}
```

This is very common when writing flexible functions and wrappers.

---

# 9. What Is the Correct Order of Parameters?

A function can contain different kinds of parameters, but their ordering rules must be respected.

A common structure is:

```python
def function(positional, default=10, *args, keyword_only=True, **kwargs):
    pass
```

Example:

```python
def test(a, b=10, *args, c=20, **kwargs):
    print(a)
    print(b)
    print(args)
    print(c)
    print(kwargs)

test(1, 2, 3, 4, c=50, name="Harsha")
```

Output:

```text
1
2
(3, 4)
50
{'name': 'Harsha'}
```

---

# 10. What Happens to Arguments After `*args`?

Arguments that are not assigned to earlier positional parameters are collected into `args`.

```python
def test(a, *args):
    print("a:", a)
    print("args:", args)

test(10, 20, 30, 40)
```

Output:

```text
a: 10
args: (20, 30, 40)
```

---

# 11. What Happens to Keyword Arguments in `**kwargs`?

Keyword arguments that are not matched by explicitly named parameters are collected into `kwargs`.

```python
def test(name, **kwargs):
    print("name:", name)
    print("kwargs:", kwargs)

test("Harsha", age=21, city="Hyderabad")
```

Output:

```text
name: Harsha
kwargs: {'age': 21, 'city': 'Hyderabad'}
```

---

# 12. Can `*args` Be Empty?

Yes.

```python
def test(*args):
    print(args)

test()
```

Output:

```text
()
```

An empty tuple is created.

---

# 13. Can `**kwargs` Be Empty?

Yes.

```python
def test(**kwargs):
    print(kwargs)

test()
```

Output:

```text
{}
```

An empty dictionary is created.

---

# 14. Can a Function Have Only `*args`?

Yes.

```python
def test(*args):
    print(args)

test(1, 2, 3)
```

Output:

```text
(1, 2, 3)
```

---

# 15. Can a Function Have Only `**kwargs`?

Yes.

```python
def test(**kwargs):
    print(kwargs)

test(name="Harsha", age=21)
```

Output:

```text
{'name': 'Harsha', 'age': 21}
```

---

# 16. Can We Rename `args` and `kwargs`?

Yes.

The names are conventions.

```python
def test(*numbers, **details):
    print(numbers)
    print(details)

test(10, 20, name="Harsha")
```

Output:

```text
(10, 20)
{'name': 'Harsha'}
```

### Interview Point

> The special behavior comes from `*` and `**`; `args` and `kwargs` are conventional names that make the code easier for other developers to understand.

---

# 17. What Is Argument Unpacking?

Argument unpacking means taking elements from an iterable or dictionary and passing them as separate arguments.

For positional arguments, use `*`.

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

The list is unpacked as:

```python
add(10, 20, 30)
```

---

# 18. What Is Keyword Argument Unpacking?

Use `**` to unpack a dictionary into keyword arguments.

```python
def introduce(name, age):
    print(name, age)

person = {
    "name": "Harsha",
    "age": 21
}

introduce(**person)
```

This is equivalent to:

```python
introduce(name="Harsha", age=21)
```

Output:

```text
Harsha 21
```

---

# 19. Difference Between Packing and Unpacking

### Packing

Collecting multiple values into one variable.

```python
def test(*args):
    print(args)

test(10, 20, 30)
```

Here the arguments are packed into:

```python
(10, 20, 30)
```

### Unpacking

Taking values from a collection and passing them separately.

```python
numbers = [10, 20, 30]

def test(a, b, c):
    print(a, b, c)

test(*numbers)
```

### Interview Answer

> Packing collects multiple arguments into a tuple or dictionary, while unpacking expands an iterable or dictionary into individual function arguments.

---

# 20. `*args` Packing Example

```python
def show(*args):
    print(args)

show("Python", "SQL", "PySpark")
```

Output:

```text
('Python', 'SQL', 'PySpark')
```

---

# 21. `*` Unpacking Example

```python
skills = ["Python", "SQL", "PySpark"]

def show(a, b, c):
    print(a)
    print(b)
    print(c)

show(*skills)
```

Output:

```text
Python
SQL
PySpark
```

---

# 22. `**kwargs` Packing Example

```python
def show(**kwargs):
    print(kwargs)

show(language="Python", database="SQL")
```

Output:

```text
{'language': 'Python', 'database': 'SQL'}
```

---

# 23. `**` Unpacking Example

```python
data = {
    "language": "Python",
    "database": "SQL"
}

def show(language, database):
    print(language)
    print(database)

show(**data)
```

Output:

```text
Python
SQL
```

---

# 24. What Happens If We Pass Too Many Positional Arguments Without `*args`?

```python
def add(a, b):
    return a + b

add(10, 20, 30)
```

Python raises a `TypeError` because the function accepts only two positional arguments.

Using `*args` avoids this restriction:

```python
def add(*args):
    return sum(args)

print(add(10, 20, 30))
```

Output:

```text
60
```

---

# 25. What Happens If We Pass Unexpected Keyword Arguments Without `**kwargs`?

```python
def introduce(name):
    print(name)

introduce(name="Harsha", age=21)
```

This raises a `TypeError` because `age` is not an accepted parameter.

With `**kwargs`:

```python
def introduce(name, **kwargs):
    print(name)
    print(kwargs)

introduce(name="Harsha", age=21)
```

Output:

```text
Harsha
{'age': 21}
```

---

# 26. How Can `*args` Be Used to Calculate a Sum?

```python
def calculate_sum(*numbers):
    return sum(numbers)

print(calculate_sum(10, 20))
print(calculate_sum(10, 20, 30))
print(calculate_sum(1, 2, 3, 4, 5))
```

Output:

```text
30
60
15
```

---

# 27. How Can `*args` Be Used With a Loop?

```python
def display(*args):
    for value in args:
        print(value)

display("Python", "SQL", "AWS")
```

Output:

```text
Python
SQL
AWS
```

---

# 28. How Can `**kwargs` Be Used With a Loop?

```python
def display(**kwargs):
    for key, value in kwargs.items():
        print(key, ":", value)

display(
    name="Harsha",
    role="Data Engineer",
    skill="Python"
)
```

Output:

```text
name : Harsha
role : Data Engineer
skill : Python
```

---

# 29. How Can We Combine Normal Parameters With `*args`?

```python
def greet(name, *skills):
    print("Name:", name)
    print("Skills:", skills)

greet("Harsha", "Python", "SQL", "PySpark")
```

Output:

```text
Name: Harsha
Skills: ('Python', 'SQL', 'PySpark')
```

The first argument is assigned to `name`, and remaining positional arguments go into `skills`.

---

# 30. How Can We Combine Normal Parameters With `**kwargs`?

```python
def profile(name, **details):
    print("Name:", name)
    print("Details:", details)

profile(
    "Harsha",
    age=21,
    city="Hyderabad",
    skill="Python"
)
```

Output:

```text
Name: Harsha
Details: {'age': 21, 'city': 'Hyderabad', 'skill': 'Python'}
```

---

# 31. What Is a Keyword-Only Argument Using `*`?

A bare `*` can force parameters after it to be keyword-only.

```python
def introduce(name, *, age, city):
    print(name, age, city)
```

Correct:

```python
introduce("Harsha", age=21, city="Hyderabad")
```

Incorrect:

```python
introduce("Harsha", 21, "Hyderabad")
```

### Interview Answer

> A bare `*` in a function signature marks the parameters after it as keyword-only parameters.

---

# 32. What Is the Difference Between `*args` and a Bare `*`?

### `*args`

Collects extra positional arguments.

```python
def test(*args):
    print(args)
```

### Bare `*`

Does not collect arguments. It marks subsequent parameters as keyword-only.

```python
def test(*, name, age):
    print(name, age)
```

---

# 33. Can `*args` Come Before `**kwargs`?

Yes.

```python
def test(*args, **kwargs):
    print(args)
    print(kwargs)
```

This is the standard arrangement when accepting both variable positional and variable keyword arguments.

---

# 34. Can `**kwargs` Come Before `*args`?

No.

This is invalid:

```python
def test(**kwargs, *args):
    pass
```

The variable positional argument collection must come before `**kwargs`.

---

# 35. Can We Pass a List to a Function With `*args` Without `*`?

Consider:

```python
def add(*args):
    print(args)

numbers = [10, 20, 30]

add(numbers)
```

Output:

```text
([10, 20, 30],)
```

The entire list becomes one positional argument.

If we use:

```python
add(*numbers)
```

Output:

```text
(10, 20, 30)
```

The list is unpacked into separate arguments.

---

# 36. Can We Pass a Dictionary to `**kwargs` Without `**`?

Consider:

```python
def show(**kwargs):
    print(kwargs)

data = {
    "name": "Harsha",
    "age": 21
}

show(data)
```

This raises a `TypeError` because `data` is passed as a positional argument.

Correct:

```python
show(**data)
```

Output:

```text
{'name': 'Harsha', 'age': 21}
```

---

# 37. Can We Use a Tuple With `*`?

Yes.

```python
def add(a, b, c):
    return a + b + c

numbers = (10, 20, 30)

print(add(*numbers))
```

Output:

```text
60
```

Any suitable iterable can be unpacked with `*`.

---

# 38. Can We Use a String With `*`?

Yes, although it should be used carefully.

```python
def show(a, b, c):
    print(a, b, c)

show(*"ABC")
```

Output:

```text
A B C
```

The string is iterable, so its characters are unpacked.

---

# 39. Can We Use a Dictionary With `*`?

Yes, but `*dictionary` iterates over its keys.

```python
def show(a, b):
    print(a, b)

data = {
    "a": 10,
    "b": 20
}

show(*data)
```

Output:

```text
a b
```

For keyword arguments, use:

```python
show(**data)
```

which produces:

```text
10 20
```

---

# 40. What Happens When We Use `*` on a Dictionary?

`*dictionary` unpacks the dictionary's keys.

```python
data = {
    "name": "Harsha",
    "age": 21
}

print(*data)
```

Output:

```text
name age
```

---

# 41. What Happens When We Use `**` on a Dictionary?

`**` unpacks dictionary keys as keyword names and their values as corresponding arguments.

```python
def show(name, age):
    print(name, age)

data = {
    "name": "Harsha",
    "age": 21
}

show(**data)
```

Output:

```text
Harsha 21
```

---

# 42. What Happens If Dictionary Keys Do Not Match Parameter Names?

```python
def show(name, age):
    print(name, age)

data = {
    "username": "Harsha",
    "age": 21
}

show(**data)
```

This raises a `TypeError` because `username` does not match the parameter `name`.

---

# 43. What Happens If a Dictionary Has Extra Keys?

```python
def show(name, **kwargs):
    print(name)
    print(kwargs)

data = {
    "name": "Harsha",
    "age": 21,
    "city": "Hyderabad"
}

show(**data)
```

Output:

```text
Harsha
{'age': 21, 'city': 'Hyderabad'}
```

The unmatched keys are collected by `kwargs`.

---

# 44. What Happens If We Pass Duplicate Values?

Example:

```python
def show(name):
    print(name)

show("Harsha", name="Ravi")
```

This causes a `TypeError` because `name` receives two values.

The same issue can happen when combining explicit keyword arguments with `**kwargs`.

---

# 45. How Does `**kwargs` Help With Flexible APIs?

Suppose a function accepts optional configuration values.

```python
def create_user(name, **options):
    print("Name:", name)

    if "age" in options:
        print("Age:", options["age"])

    if "city" in options:
        print("City:", options["city"])

create_user(
    "Harsha",
    age=21,
    city="Hyderabad"
)
```

This allows the function to accept additional optional settings without explicitly defining every possible option.

---

# 46. Real-World Example — API Function

In backend development, a helper function may accept optional parameters:

```python
def create_request(endpoint, **options):
    print("Endpoint:", endpoint)
    print("Options:", options)

create_request(
    "/users",
    timeout=10,
    retries=3,
    headers={"Authorization": "token"}
)
```

Output:

```text
Endpoint: /users
Options: {'timeout': 10, 'retries': 3, 'headers': {'Authorization': 'token'}}
```

### Interview Explanation

> `**kwargs` can be useful when a function supports optional configuration values, but I would still prefer explicit parameters for important, well-defined inputs because they provide better readability and validation.

---

# 47. Real-World Example — Data Processing

Suppose a data-processing function accepts optional processing settings.

```python
def process_data(data, **options):
    if options.get("remove_duplicates"):
        data = list(set(data))

    if options.get("sort"):
        data.sort()

    return data

data = [3, 1, 2, 3]

print(
    process_data(
        data,
        remove_duplicates=True,
        sort=True
    )
)
```

Output:

```text
[1, 2, 3]
```

### Interview Explanation

> Variable keyword arguments can be useful for optional configuration, but for production systems I would keep the accepted options controlled and documented rather than allowing arbitrary parameters without validation.

---

# 48. Real-World Example — Wrapper Function

`*args` and `**kwargs` are especially important when creating wrappers around other functions.

```python
def wrapper(func, *args, **kwargs):
    print("Before function call")

    result = func(*args, **kwargs)

    print("After function call")

    return result


def add(a, b):
    return a + b


result = wrapper(add, 10, 20)

print(result)
```

Output:

```text
Before function call
After function call
30
```

The wrapper can forward any positional and keyword arguments.

---

# 49. Why Are `*args` and `**kwargs` Important in Decorators?

A decorator often needs to work with functions having different parameter lists.

Example:

```python
from functools import wraps

def log_call(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Calling:", func.__name__)

        result = func(*args, **kwargs)

        return result

    return wrapper


@log_call
def add(a, b):
    return a + b


@log_call
def greet(name):
    return f"Hello {name}"


print(add(10, 20))
print(greet("Harsha"))
```

Output:

```text
Calling: add
30
Calling: greet
Hello Harsha
```

### Interview Answer

> `*args` and `**kwargs` allow a decorator wrapper to accept and forward different combinations of positional and keyword arguments without knowing the decorated function's exact signature.

---

# 50. Important Interview Question — Explain This Code

```python
def test(a, *args, **kwargs):
    print(a)
    print(args)
    print(kwargs)

test(10, 20, 30, name="Harsha", age=21)
```

### Answer

```text
10
(20, 30)
{'name': 'Harsha', 'age': 21}
```

Explanation:

- `10` → assigned to `a`
- `20, 30` → collected into `args`
- `name` and `age` → collected into `kwargs`

---

# 51. Important Output Question

```python
def test(*args):
    print(type(args))
    print(args)

test(1, 2, 3)
```

### Answer

```text
<class 'tuple'>
(1, 2, 3)
```

---

# 52. Important Output Question

```python
def test(**kwargs):
    print(type(kwargs))
    print(kwargs)

test(a=10, b=20)
```

### Answer

```text
<class 'dict'>
{'a': 10, 'b': 20}
```

---

# 53. Important Output Question

```python
def test(*args):
    print(len(args))

test()
test(1, 2, 3)
```

### Answer

```text
0
3
```

---

# 54. Important Output Question

```python
def test(**kwargs):
    print(len(kwargs))

test()
test(a=10, b=20, c=30)
```

### Answer

```text
0
3
```

---

# 55. Important Output Question

```python
def test(a, *args):
    print(a)
    print(args)

test(10, 20, 30)
```

### Answer

```text
10
(20, 30)
```

---

# 56. Important Output Question

```python
def test(a, **kwargs):
    print(a)
    print(kwargs)

test(10, x=20, y=30)
```

### Answer

```text
10
{'x': 20, 'y': 30}
```

---

# 57. Important Output Question — Unpacking

```python
def add(a, b, c):
    return a + b + c

values = [10, 20, 30]

print(add(*values))
```

### Answer

```text
60
```

---

# 58. Important Output Question — Dictionary Unpacking

```python
def show(name, age):
    print(name, age)

data = {
    "name": "Harsha",
    "age": 21
}

show(**data)
```

### Answer

```text
Harsha 21
```

---

# 59. Important Output Question — Dictionary With `*`

```python
data = {
    "name": "Harsha",
    "age": 21
}

print(*data)
```

### Answer

```text
name age
```

Because `*` iterates over dictionary keys.

---

# 60. Important Output Question — Combined

```python
def test(a, b=20, *args, **kwargs):
    print(a)
    print(b)
    print(args)
    print(kwargs)

test(10, 30, 40, 50, x=60, y=70)
```

### Answer

```text
10
30
(40, 50)
{'x': 60, 'y': 70}
```

---

# 61. Important Output Question — Keyword-Only

```python
def test(a, *, b):
    print(a, b)

test(10, b=20)
```

### Answer

```text
10 20
```

`b` must be supplied as a keyword argument.

---

# 62. Important Output Question — `*args` and Keyword-Only Parameter

```python
def test(a, *args, b=10):
    print(a)
    print(args)
    print(b)

test(1, 2, 3, 4, b=20)
```

### Answer

```text
1
(2, 3, 4)
20
```

---

# 63. Important Output Question — Forwarding Arguments

```python
def add(a, b):
    return a + b

def wrapper(*args, **kwargs):
    return add(*args, **kwargs)

print(wrapper(10, 20))
```

### Answer

```text
30
```

The wrapper receives the arguments and forwards them to `add()`.

---

# 64. Common Mistake — Thinking `args` Is a List

```python
def test(*args):
    print(type(args))
```

The answer is:

```text
<class 'tuple'>
```

Not:

```text
<class 'list'>
```

---

# 65. Common Mistake — Thinking `kwargs` Is a Tuple

```python
def test(**kwargs):
    print(type(kwargs))
```

The answer is:

```text
<class 'dict'>
```

Not a tuple.

---

# 66. Common Mistake — Thinking `args` and `kwargs` Are Keywords

They are not Python keywords.

This works:

```python
def test(*values, **details):
    print(values)
    print(details)
```

The special syntax is:

```text
*
**
```

The names are chosen by the programmer.

---

# 67. Common Mistake — Using `*args` When Explicit Parameters Are Better

This:

```python
def create_user(*args):
    pass
```

may be less readable if the function always requires:

```text
name
age
email
```

A clearer design may be:

```python
def create_user(name, age, email):
    pass
```

### Interview Point

> I would use `*args` and `**kwargs when flexibility is genuinely required. I would not use them everywhere because explicit parameters provide better readability, documentation, and validation.

---

# 68. Common Mistake — Using `**kwargs` for Everything

This:

```python
def process(**kwargs):
    pass
```

can hide the function's expected interface.

If important parameters are known, explicit parameters are usually clearer:

```python
def process(name, age, city):
    pass
```

`**kwargs` is most useful for optional or extensible configuration.

---

# 69. `*args` vs List Parameter

These are not exactly the same.

### List parameter

```python
def test(numbers):
    print(numbers)

test([10, 20, 30])
```

The caller must provide one list.

### `*args`

```python
def test(*numbers):
    print(numbers)

test(10, 20, 30)
```

The function accepts separate positional arguments and packs them into a tuple.

---

# 70. `**kwargs` vs Dictionary Parameter

### Dictionary parameter

```python
def test(data):
    print(data)

test({
    "name": "Harsha",
    "age": 21
})
```

The caller provides one dictionary.

### `**kwargs`

```python
def test(**data):
    print(data)

test(name="Harsha", age=21)
```

The keyword arguments are automatically collected into a dictionary.

---

# 71. When Should You Use `*args`?

Good use cases include:

- Variable number of values
- Utility functions
- Wrappers
- Decorators
- Functions forwarding positional arguments
- APIs where positional inputs are intentionally flexible

Example:

```python
def total(*numbers):
    return sum(numbers)
```

---

# 72. When Should You Use `**kwargs`?

Good use cases include:

- Optional configuration
- Wrappers
- Decorators
- Forwarding keyword arguments
- Extensible APIs
- Functions that intentionally support additional named options

Example:

```python
def configure(**settings):
    print(settings)
```

---

# 73. When Should You Avoid `*args` and `**kwargs`?

Avoid them when the function has a small, known, meaningful set of parameters.

Instead of:

```python
def calculate(*args):
    pass
```

prefer:

```python
def calculate(price, quantity, discount):
    pass
```

when those inputs are always required.

### Interview Answer

> Flexibility should not come at the cost of clarity. If the expected inputs are known, I prefer explicit parameters.

---

# 74. How Are `*args` and `**kwargs` Used in Decorators?

Typical decorator pattern:

```python
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function:", func.__name__)
        print("Arguments:", args)
        print("Keyword arguments:", kwargs)

        return func(*args, **kwargs)

    return wrapper


@logger
def add(a, b):
    return a + b


print(add(10, 20))
```

Output:

```text
Function: add
Arguments: (10, 20)
Keyword arguments: {}
30
```

---

# 75. How Are `*args` and `**kwargs` Used in Inheritance or `super()`?

They can be used when forwarding flexible arguments to another method.

Example:

```python
class Parent:
    def show(self, *args, **kwargs):
        print("Parent:", args, kwargs)


class Child(Parent):
    def show(self, *args, **kwargs):
        print("Child:", args, kwargs)
        super().show(*args, **kwargs)


obj = Child()

obj.show(10, 20, name="Harsha")
```

Output:

```text
Child: (10, 20) {'name': 'Harsha'}
Parent: (10, 20) {'name': 'Harsha'}
```

This concept connects `*args` and `**kwargs` with OOP and method overriding.

---

# 76. How Would You Explain `*args` and `**kwargs` in an Interview?

A strong concise answer:

> `*args` and `**kwargs` are used when we want a function to accept a variable number of arguments. `*args` collects positional arguments into a tuple, while `**kwargs` collects keyword arguments into a dictionary. They are especially useful in wrappers, decorators, flexible utility functions, and forwarding arguments. However, I prefer explicit parameters when the function's inputs are known because they make the interface clearer.

---

# 77. Placement Interview Questions — Must Know

You should be able to answer these without hesitation:

1. What are `*args` and `**kwargs`?
2. Why do we use `*args`?
3. Why do we use `**kwargs`?
4. What type is `args`?
5. What type is `kwargs`?
6. Difference between `*args` and `**kwargs`.
7. Can they be used together?
8. Can `args` and `kwargs` be renamed?
9. What does `*` mean in a function definition?
10. What does `**` mean in a function definition?
11. What is argument packing?
12. What is argument unpacking?
13. Difference between packing and unpacking.
14. How do you unpack a list into function arguments?
15. How do you unpack a dictionary into keyword arguments?
16. What happens when `*` is used with a dictionary?
17. What happens when `**` is used with a dictionary?
18. Can `*args` be empty?
19. Can `**kwargs` be empty?
20. Can a function have only `*args`?
21. Can a function have only `**kwargs`?
22. Can normal parameters be used with `*args`?
23. Can normal parameters be used with `**kwargs`?
24. What is a keyword-only argument?
25. Difference between `*args` and a bare `*`.
26. What is the correct order of parameters?
27. Can `**kwargs` appear before `*args`?
28. What happens when too many positional arguments are passed?
29. What happens when unexpected keyword arguments are passed?
30. What happens if a list is passed without `*`?
31. What happens if a dictionary is passed without `**`?
32. How can `*args` be used in a decorator?
33. How can `**kwargs` be used in a decorator?
34. Why are `*args` and `**kwargs` useful in wrappers?
35. Difference between `*args` and a list parameter.
36. Difference between `**kwargs` and a dictionary parameter.
37. When should `*args` be avoided?
38. When should `**kwargs` be avoided?
39. Explain a real-world use case of `*args`.
40. Explain a real-world use case of `**kwargs`.
41. Predict output involving `*args`.
42. Predict output involving `**kwargs`.
43. Predict output involving argument unpacking.
44. Explain how `*args` and `**kwargs` forward arguments.
45. Explain how they are used in decorators.

---

# 78. Final Quick Revision

```text
*args
    -> Variable positional arguments
    -> Stored as tuple
    -> Example: func(10, 20, 30)

**kwargs
    -> Variable keyword arguments
    -> Stored as dictionary
    -> Example: func(name="Harsha", age=21)

Packing
    -> Collect arguments
    -> *args / **kwargs

Unpacking
    -> Expand collections
    -> *list / *tuple
    -> **dictionary

* in function signature
    -> Can collect positional arguments when followed by a name
    -> Can mark following parameters as keyword-only when used alone

*args + **kwargs
    -> Useful for flexible functions
    -> Very common in decorators and wrappers

args
    -> tuple

kwargs
    -> dict

Important principle
    -> Use flexibility when needed
    -> Prefer explicit parameters when inputs are known
```

# Interview-Level Takeaway

> **The most important thing is not just memorizing the syntax. Understand what happens during packing and unpacking. `*args` receives multiple positional arguments as a tuple, while `**kwargs` receives multiple keyword arguments as a dictionary. The same `*` and `**` syntax can also be used for unpacking when calling a function. These concepts become particularly important when working with decorators, wrappers, APIs, configurable functions, and reusable Python utilities.**