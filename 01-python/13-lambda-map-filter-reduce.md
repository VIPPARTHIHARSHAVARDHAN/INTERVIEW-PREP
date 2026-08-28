# Lambda, Map, Filter and Reduce — Python Interview Preparation

## 1. What Are Lambda, `map()`, `filter()` and `reduce()`?

These are important Python concepts used for **functional-style programming**.

- **Lambda** → creates a small anonymous function.
- **`map()`** → applies a function to every item.
- **`filter()`** → selects items based on a condition.
- **`reduce()`** → combines multiple items into a single result.

Example:

```python
numbers = [1, 2, 3, 4, 5]

squares = list(map(lambda x: x * x, numbers))

print(squares)
```

Output:

```text
[1, 4, 9, 16, 25]
```

---

# 2. What Is a Lambda Function?

A lambda function is a small **anonymous function** created using the `lambda` keyword.

Syntax:

```python
lambda arguments: expression
```

Example:

```python
square = lambda x: x * x

print(square(5))
```

Output:

```text
25
```

Equivalent normal function:

```python
def square(x):
    return x * x
```

### Interview Answer

> A lambda function is an anonymous function used mainly for short operations where defining a separate function using `def` would be unnecessary.

---

# 3. Why Is It Called an Anonymous Function?

Normally, a function is defined with a name:

```python
def add(a, b):
    return a + b
```

A lambda can be created without explicitly defining a function name:

```python
lambda a, b: a + b
```

Example:

```python
result = (lambda a, b: a + b)(10, 20)

print(result)
```

Output:

```text
30
```

The lambda itself has no explicitly assigned function name.

---

# 4. Basic Lambda Example

```python
add = lambda a, b: a + b

print(add(10, 20))
```

Output:

```text
30
```

Here:

```text
lambda a, b: a + b
```

means:

```text
take a and b
↓
add them
↓
return the result
```

---

# 5. Lambda With One Argument

```python
cube = lambda x: x ** 3

print(cube(3))
```

Output:

```text
27
```

---

# 6. Lambda With Multiple Arguments

```python
multiply = lambda a, b: a * b

print(multiply(5, 4))
```

Output:

```text
20
```

Lambda functions can accept multiple arguments.

---

# 7. Can a Lambda Have Multiple Expressions?

A lambda is restricted to **one expression**.

This is valid:

```python
square = lambda x: x * x
```

This is not valid:

```python
lambda x:
    y = x * 2
    return y
```

If the logic becomes complicated, use a normal function with `def`.

### Interview Answer

> A lambda can contain only one expression. For complex multi-step logic, a normal function is more readable and appropriate.

---

# 8. Does a Lambda Have an Implicit Return?

Yes.

The expression in a lambda is automatically returned.

```python
square = lambda x: x * x

print(square(5))
```

There is no need to write:

```python
return
```

---

# 9. Lambda With Conditional Expression

A conditional expression can be used inside a lambda.

```python
check = lambda x: "Even" if x % 2 == 0 else "Odd"

print(check(10))
print(check(7))
```

Output:

```text
Even
Odd
```

---

# 10. Lambda With `sorted()`

Lambda functions are commonly used as sorting keys.

```python
students = [
    ("Harsha", 85),
    ("Ravi", 70),
    ("Anu", 95)
]

students.sort(key=lambda student: student[1])

print(students)
```

Output:

```text
[('Ravi', 70), ('Harsha', 85), ('Anu', 95)]
```

Here:

```python
key=lambda student: student[1]
```

tells Python to sort based on the marks.

---

# 11. Real-World Example — Sorting Records

Suppose we have employee records:

```python
employees = [
    {"name": "Harsha", "salary": 50000},
    {"name": "Ravi", "salary": 70000},
    {"name": "Anu", "salary": 60000}
]

employees.sort(key=lambda employee: employee["salary"])

print(employees)
```

The lambda extracts the salary used for sorting.

This pattern is common when working with structured data.

---

# 12. What Is `map()`?

`map()` applies a function to every item in an iterable.

Syntax:

```python
map(function, iterable)
```

Example:

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x * 2, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6, 8]
```

---

# 13. Why Do We Usually Use `list()` With `map()`?

In Python 3, `map()` returns a **map iterator**, not a list.

Example:

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(result)
```

You get a map object representation rather than the actual list of results.

To materialize the results:

```python
print(list(result))
```

Output:

```text
[2, 4, 6]
```

---

# 14. How Does `map()` Work?

Example:

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x * x, numbers)

print(list(result))
```

Conceptually:

```text
1 → 1
2 → 4
3 → 9
4 → 16
```

Final result:

```text
[1, 4, 9, 16]
```

---

# 15. `map()` With a Normal Function

`map()` does not require lambda.

```python
def square(x):
    return x * x


numbers = [1, 2, 3, 4]

result = map(square, numbers)

print(list(result))
```

Output:

```text
[1, 4, 9, 16]
```

---

# 16. Lambda vs `def`

### Lambda

```python
square = lambda x: x * x
```

### Normal function

```python
def square(x):
    return x * x
```

Use lambda when:

- operation is short
- function is needed temporarily
- commonly used as an argument to functions such as `map()`, `filter()`, or `sorted()`

Use `def` when:

- logic is complex
- function is reused
- readability matters
- multiple statements are required

---

# 17. What Is `filter()`?

`filter()` selects elements from an iterable based on a condition.

Syntax:

```python
filter(function, iterable)
```

The function should return a truthy or falsy value.

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda x: x % 2 == 0, numbers)

print(list(result))
```

Output:

```text
[2, 4, 6]
```

---

# 18. How Does `filter()` Work?

Given:

```python
numbers = [1, 2, 3, 4, 5]
```

Condition:

```python
lambda x: x % 2 == 0
```

Python checks:

```text
1 → False
2 → True
3 → False
4 → True
5 → False
```

Only values returning `True` are included.

Result:

```text
[2, 4]
```

---

# 19. `filter()` With a Normal Function

```python
def is_even(x):
    return x % 2 == 0


numbers = [1, 2, 3, 4, 5]

result = filter(is_even, numbers)

print(list(result))
```

Output:

```text
[2, 4]
```

---

# 20. `filter()` With Strings

```python
names = ["Harsha", "", "Ravi", "", "Anu"]

result = filter(lambda name: name != "", names)

print(list(result))
```

Output:

```text
['Harsha', 'Ravi', 'Anu']
```

---

# 21. Filtering Based on String Length

```python
names = ["Ram", "Harsha", "Anu", "Krishna"]

result = filter(lambda name: len(name) > 3, names)

print(list(result))
```

Output:

```text
['Harsha', 'Krishna']
```

---

# 22. What Is `reduce()`?

`reduce()` repeatedly applies a function to elements of an iterable and produces a single result.

It is available in:

```python
functools
```

Example:

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

Conceptually:

```text
1 + 2 = 3
3 + 3 = 6
6 + 4 = 10
```

---

# 23. Why Is `reduce()` Imported From `functools`?

In Python 3, `reduce()` was moved from the built-in namespace to the `functools` module.

Therefore:

```python
from functools import reduce
```

is required before using it.

---

# 24. How Does `reduce()` Work?

Example:

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

Step by step:

```text
a = 1, b = 2 → 3
a = 3, b = 3 → 6
a = 6, b = 4 → 10
```

Final result:

```text
10
```

---

# 25. `reduce()` With Multiplication

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

result = reduce(lambda a, b: a * b, numbers)

print(result)
```

Output:

```text
120
```

This can be used to calculate a product of values.

---

# 26. What Is the Initial Value in `reduce()`?

`reduce()` can accept an optional initializer.

Syntax:

```python
reduce(function, iterable, initializer)
```

Example:

```python
from functools import reduce

numbers = [1, 2, 3]

result = reduce(lambda a, b: a + b, numbers, 10)

print(result)
```

Output:

```text
16
```

Calculation:

```text
10 + 1 = 11
11 + 2 = 13
13 + 3 = 16
```

---

# 27. What Happens When `reduce()` Gets an Empty Iterable?

Without an initializer:

```python
from functools import reduce

numbers = []

result = reduce(lambda a, b: a + b, numbers)
```

This raises:

```text
TypeError
```

With an initializer:

```python
from functools import reduce

numbers = []

result = reduce(lambda a, b: a + b, numbers, 0)

print(result)
```

Output:

```text
0
```

---

# 28. Difference Between `map()`, `filter()` and `reduce()`

| Function | Purpose | Result |
|---|---|---|
| `map()` | Transform every item | Iterator |
| `filter()` | Select matching items | Iterator |
| `reduce()` | Combine items | Single value |

Example:

```python
numbers = [1, 2, 3, 4, 5]
```

### `map()`

```python
[2, 4, 6, 8, 10]
```

### `filter()`

```python
[2, 4]
```

### `reduce()`

```text
15
```

---

# 29. `map()` vs `filter()`

### `map()`

Changes/transforms every item.

```python
numbers = [1, 2, 3]

print(list(map(lambda x: x * 2, numbers)))
```

Output:

```text
[2, 4, 6]
```

### `filter()`

Keeps only items satisfying a condition.

```python
numbers = [1, 2, 3]

print(list(filter(lambda x: x > 1, numbers)))
```

Output:

```text
[2, 3]
```

### Interview Answer

> `map()` is mainly used for transformation, while `filter()` is used for selection based on a condition.

---

# 30. `map()` vs `reduce()`

### `map()`

Produces one transformed output for each input.

```python
numbers = [1, 2, 3]

result = list(map(lambda x: x * 2, numbers))

print(result)
```

Output:

```text
[2, 4, 6]
```

### `reduce()`

Combines values into one final result.

```python
from functools import reduce

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

Output:

```text
6
```

---

# 31. `filter()` vs `reduce()`

### `filter()`

Returns selected elements.

```python
numbers = [1, 2, 3, 4]

result = list(filter(lambda x: x % 2 == 0, numbers))

print(result)
```

Output:

```text
[2, 4]
```

### `reduce()`

Combines elements into one result.

```python
from functools import reduce

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

Output:

```text
10
```

---

# 32. Can `map()` Take Multiple Iterables?

Yes.

Example:

```python
numbers1 = [1, 2, 3]
numbers2 = [10, 20, 30]

result = map(lambda a, b: a + b, numbers1, numbers2)

print(list(result))
```

Output:

```text
[11, 22, 33]
```

Python passes corresponding elements to the function.

---

# 33. What Happens If Multiple Iterables Have Different Lengths in `map()`?

`map()` stops when the **shortest iterable is exhausted**.

Example:

```python
a = [1, 2, 3]
b = [10, 20]

result = map(lambda x, y: x + y, a, b)

print(list(result))
```

Output:

```text
[11, 22]
```

The third element of `a` has no corresponding element in `b`.

---

# 34. Can `filter()` Take Multiple Iterables?

No.

`filter()` accepts one iterable:

```python
filter(function, iterable)
```

If you need multiple iterables, other approaches such as `zip()` can be used first.

Example:

```python
a = [1, 2, 3]
b = [10, 20, 30]

result = filter(
    lambda pair: pair[0] + pair[1] > 20,
    zip(a, b)
)

print(list(result))
```

Output:

```text
[(2, 20), (3, 30)]
```

---

# 35. Can `reduce()` Work With Different Data Types?

Yes, as long as the function can combine the values correctly.

Example:

```python
from functools import reduce

words = ["Python", "is", "easy"]

result = reduce(lambda a, b: a + " " + b, words)

print(result)
```

Output:

```text
Python is easy
```

---

# 36. Lambda With `map()`

This is one of the most common combinations.

```python
numbers = [1, 2, 3, 4]

squares = list(map(lambda x: x ** 2, numbers))

print(squares)
```

Output:

```text
[1, 4, 9, 16]
```

---

# 37. Lambda With `filter()`

Another common combination:

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = list(
    filter(lambda x: x % 2 == 0, numbers)
)

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

---

# 38. Lambda With `reduce()`

```python
from functools import reduce

numbers = [1, 2, 3, 4]

total = reduce(lambda a, b: a + b, numbers)

print(total)
```

Output:

```text
10
```

---

# 39. Combining `filter()` and `map()`

These functions can be chained.

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]

result = list(
    map(
        lambda x: x * x,
        filter(lambda x: x % 2 == 0, numbers)
    )
)

print(result)
```

Output:

```text
[4, 16, 36]
```

Process:

```text
Original
[1, 2, 3, 4, 5, 6]

filter even
[2, 4, 6]

map square
[4, 16, 36]
```

---

# 40. Combining `filter()`, `map()` and `reduce()`

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5, 6]

result = reduce(
    lambda a, b: a + b,
    map(
        lambda x: x * x,
        filter(lambda x: x % 2 == 0, numbers)
    )
)

print(result)
```

Output:

```text
56
```

Process:

```text
Original
[1, 2, 3, 4, 5, 6]

filter even
[2, 4, 6]

square
[4, 16, 36]

reduce sum
4 + 16 + 36 = 56
```

---

# 41. Can We Replace `map()` With a List Comprehension?

Yes.

Using `map()`:

```python
numbers = [1, 2, 3, 4]

result = list(map(lambda x: x * 2, numbers))
```

Using list comprehension:

```python
result = [x * 2 for x in numbers]
```

Both produce:

```text
[2, 4, 6, 8]
```

---

# 42. Can We Replace `filter()` With a List Comprehension?

Yes.

Using `filter()`:

```python
numbers = [1, 2, 3, 4, 5]

result = list(filter(lambda x: x % 2 == 0, numbers))
```

Using list comprehension:

```python
result = [x for x in numbers if x % 2 == 0]
```

Both produce:

```text
[2, 4]
```

---

# 43. Which Is More Readable: `filter()` or List Comprehension?

It depends on the operation, but list comprehensions are often easier to read for simple filtering and transformation.

Example:

```python
even_numbers = [x for x in numbers if x % 2 == 0]
```

is often more immediately readable than:

```python
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
```

### Interview Answer

> I would choose based on readability and context. List comprehensions are often concise and readable for simple transformations or filtering, while `map()` and `filter()` can be useful when working naturally with existing functions or functional-style pipelines.

---

# 44. Is `reduce()` Always Better Than a Loop?

No.

For simple operations such as summing values, built-in functions are usually clearer:

```python
numbers = [1, 2, 3, 4]

total = sum(numbers)
```

rather than:

```python
from functools import reduce

total = reduce(lambda a, b: a + b, numbers)
```

### Interview Answer

> `reduce()` is useful when we genuinely need repeated pairwise accumulation, but I prefer specialized built-ins such as `sum()` when they express the operation more clearly.

---

# 45. What Is the Advantage of `map()`?

`map()` can express a transformation clearly and returns an iterator, allowing lazy processing.

Example:

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x * 10, numbers)

print(list(result))
```

Output:

```text
[10, 20, 30, 40]
```

---

# 46. What Is the Advantage of `filter()`?

`filter()` expresses selection logic and returns an iterator.

Example:

```python
numbers = [1, 2, 3, 4, 5]

result = filter(lambda x: x > 3, numbers)

print(list(result))
```

Output:

```text
[4, 5]
```

---

# 47. Are `map()` and `filter()` Eager or Lazy?

In Python 3, both return iterators and are **lazy**.

Example:

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(result)
```

The transformation is not materialized into a list immediately.

When iterated:

```python
print(list(result))
```

the values are produced.

---

# 48. Why Is Laziness Useful?

It can reduce unnecessary memory usage because the complete result does not have to be stored immediately.

Example:

```python
numbers = range(1000000)

result = map(lambda x: x * 2, numbers)
```

`result` is an iterator rather than a million-element list.

If we do:

```python
result = list(map(lambda x: x * 2, numbers))
```

the results are materialized into a list, requiring memory for that list.

---

# 49. Important Interview Question — Can We Iterate Over a `map` Object Twice?

Not after it has been exhausted.

Example:

```python
numbers = [1, 2, 3]

result = map(lambda x: x * 2, numbers)

print(list(result))
print(list(result))
```

Output:

```text
[2, 4, 6]
[]
```

The map object is an iterator and has already been consumed.

---

# 50. Same Concept With `filter()`

```python
numbers = [1, 2, 3, 4]

result = filter(lambda x: x % 2 == 0, numbers)

print(list(result))
print(list(result))
```

Output:

```text
[2, 4]
[]
```

The iterator is exhausted after the first conversion to a list.

---

# 51. Important Interview Question — What Does `map()` Return?

In Python 3:

```python
map()
```

returns a **map iterator**.

Example:

```python
result = map(lambda x: x * 2, [1, 2, 3])

print(type(result))
```

It is a map object implementing iterator behavior.

---

# 52. What Does `filter()` Return?

In Python 3, `filter()` returns a **filter iterator**.

Example:

```python
result = filter(lambda x: x > 1, [1, 2, 3])

print(type(result))
```

It returns a filter object.

---

# 53. Important Interview Question — What Does `reduce()` Return?

Unlike `map()` and `filter()`, `reduce()` produces a single accumulated result.

Example:

```python
from functools import reduce

result = reduce(lambda a, b: a + b, [1, 2, 3])

print(result)
```

Output:

```text
6
```

---

# 54. Important Output Question

```python
numbers = [1, 2, 3, 4]

result = map(lambda x: x + 1, numbers)

print(list(result))
```

Output:

```text
[2, 3, 4, 5]
```

---

# 55. Important Output Question

```python
numbers = [1, 2, 3, 4]

result = filter(lambda x: x > 2, numbers)

print(list(result))
```

Output:

```text
[3, 4]
```

---

# 56. Important Output Question

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda a, b: a * b, numbers)

print(result)
```

Output:

```text
24
```

---

# 57. Important Output Question

```python
numbers = [1, 2, 3]

result = list(map(lambda x: x * 2, numbers))

print(result)
```

Output:

```text
[2, 4, 6]
```

---

# 58. Important Output Question

```python
numbers = [1, 2, 3, 4, 5]

result = list(filter(lambda x: x % 2 != 0, numbers))

print(result)
```

Output:

```text
[1, 3, 5]
```

---

# 59. Important Output Question

```python
from functools import reduce

numbers = [10, 20, 30]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

Output:

```text
60
```

---

# 60. Important Output Question — `map()` With Two Lists

```python
a = [1, 2, 3]
b = [10, 20, 30]

result = list(map(lambda x, y: x + y, a, b))

print(result)
```

Output:

```text
[11, 22, 33]
```

---

# 61. Important Output Question — Filter After Map

```python
numbers = [1, 2, 3, 4]

result = filter(
    lambda x: x > 5,
    map(lambda x: x * 2, numbers)
)

print(list(result))
```

First:

```text
[2, 4, 6, 8]
```

Then filter:

```text
[6, 8]
```

Output:

```text
[6, 8]
```

---

# 62. Important Output Question — Map After Filter

```python
numbers = [1, 2, 3, 4, 5]

result = map(
    lambda x: x * 10,
    filter(lambda x: x % 2 == 0, numbers)
)

print(list(result))
```

First:

```text
[2, 4]
```

Then:

```text
[20, 40]
```

Output:

```text
[20, 40]
```

---

# 63. Important Output Question — Reduce With Initializer

```python
from functools import reduce

numbers = [1, 2, 3]

result = reduce(lambda a, b: a + b, numbers, 10)

print(result)
```

Output:

```text
16
```

---

# 64. Important Output Question — Empty Reduce

```python
from functools import reduce

numbers = []

result = reduce(lambda a, b: a + b, numbers, 100)

print(result)
```

Output:

```text
100
```

The initializer becomes the result when there are no iterable elements to process.

---

# 65. Important Output Question — Lambda Conditional

```python
check = lambda x: "Positive" if x > 0 else "Non-positive"

print(check(10))
print(check(-2))
```

Output:

```text
Positive
Non-positive
```

---

# 66. Important Output Question — Lambda Sorting

```python
numbers = [5, 2, 9, 1]

numbers.sort(key=lambda x: x)

print(numbers)
```

Output:

```text
[1, 2, 5, 9]
```

The lambda returns the value used as the sorting key.

---

# 67. Important Output Question — Sorting Tuples

```python
students = [
    ("A", 80),
    ("B", 60),
    ("C", 90)
]

result = sorted(students, key=lambda x: x[1])

print(result)
```

Output:

```text
[('B', 60), ('A', 80), ('C', 90)]
```

---

# 68. Important Interview Question — What Is the Difference Between `sorted()` and `sort()` When Using Lambda?

Both can use:

```python
key=lambda ...
```

Example:

```python
numbers = [3, 1, 2]

result = sorted(numbers, key=lambda x: x)

print(result)
```

`sorted()` returns a new list.

```python
numbers.sort(key=lambda x: x)
```

`sort()` modifies the existing list in place.

---

# 69. Important Interview Question — Can Lambda Be Used With Dictionaries?

Yes.

Example:

```python
employees = {
    "Harsha": 50000,
    "Ravi": 70000,
    "Anu": 60000
}

result = sorted(
    employees.items(),
    key=lambda item: item[1]
)

print(result)
```

Output:

```text
[('Harsha', 50000), ('Anu', 60000), ('Ravi', 70000)]
```

---

# 70. Real-World Example — Processing Employee Salaries

Suppose an application receives salaries:

```python
salaries = [30000, 45000, 60000, 25000]
```

Increase each salary by 10%:

```python
updated = list(
    map(lambda salary: salary * 1.10, salaries)
)

print(updated)
```

Output:

```text
[33000.0, 49500.0, 66000.0, 27500.000000000004]
```

In production code, monetary values should normally be handled carefully rather than relying on binary floating-point arithmetic.

---

# 71. Real-World Example — Filtering Employees

```python
employees = [
    {"name": "Harsha", "salary": 50000},
    {"name": "Ravi", "salary": 30000},
    {"name": "Anu", "salary": 70000}
]

high_salary = list(
    filter(
        lambda employee: employee["salary"] > 40000,
        employees
    )
)

print(high_salary)
```

This selects employees whose salary is greater than `40000`.

---

# 72. Real-World Example — Data Transformation

Suppose a data pipeline receives:

```python
raw_values = ["10", "20", "30", "40"]
```

Convert strings to integers:

```python
numbers = list(map(int, raw_values))

print(numbers)
```

Output:

```text
[10, 20, 30, 40]
```

Notice that lambda is not necessary because `int` itself can be passed to `map()`.

This is often cleaner:

```python
map(int, raw_values)
```

than:

```python
map(lambda x: int(x), raw_values)
```

---

# 73. Real-World Example — Data Cleaning

Suppose we have:

```python
values = ["10", "", "20", "", "30"]
```

Filter out empty values:

```python
cleaned = list(
    filter(lambda x: x != "", values)
)

print(cleaned)
```

Output:

```text
['10', '20', '30']
```

Then convert them:

```python
numbers = list(map(int, cleaned))

print(numbers)
```

Output:

```text
[10, 20, 30]
```

This pattern is useful in ETL/data-processing scenarios.

---

# 74. Real-World Example — Combining Filter and Map

```python
values = ["10", "20", "", "30", ""]

numbers = list(
    map(
        int,
        filter(lambda x: x != "", values)
    )
)

print(numbers)
```

Output:

```text
[10, 20, 30]
```

Process:

```text
Raw data
↓
Remove empty values
↓
Convert strings to integers
↓
Clean numeric data
```

---

# 75. Real-World Example — Total From Filtered Data

```python
from functools import reduce

numbers = [10, 20, 30, 40, 50]

large_numbers = filter(lambda x: x >= 30, numbers)

total = reduce(lambda a, b: a + b, large_numbers)

print(total)
```

Output:

```text
120
```

Because:

```text
30 + 40 + 50 = 120
```

In this particular case, `sum()` would be clearer:

```python
total = sum(x for x in numbers if x >= 30)
```

---

# 76. Interview Question — Why Not Use Lambda Everywhere?

Strong answer:

> Lambda functions are useful for short, simple operations, especially when a function is needed temporarily. I would not use them for complex logic because named functions with `def` are usually easier to read, test, debug, and maintain.

---

# 77. Interview Question — Is Lambda Faster Than a Normal Function?

You should not claim that lambda is inherently faster.

Example:

```python
lambda x: x * 2
```

and:

```python
def double(x):
    return x * 2
```

both create callable functions.

The main difference is syntax and intended use, not that lambda automatically provides a performance advantage.

### Interview Answer

> Lambda is primarily a concise syntax for creating a function expression; I would not choose it simply for performance reasons.

---

# 78. Interview Question — What Are the Limitations of Lambda?

Important limitations:

1. Only one expression.
2. Cannot contain normal statements such as assignments in the lambda body.
3. Usually less readable for complex logic.
4. No explicit `return` statement.
5. Poor choice for large reusable functions.

Example:

```python
square = lambda x: x * x
```

Good use.

For complex processing:

```python
def process_data(data):
    # multiple steps
    ...
```

is preferable.

---

# 79. Interview Question — Can Lambda Accept Default Arguments?

Yes.

```python
greet = lambda name="Harsha": "Hello " + name

print(greet())
print(greet("Ravi"))
```

Output:

```text
Hello Harsha
Hello Ravi
```

---

# 80. Interview Question — Can Lambda Accept `*args`?

Yes.

```python
total = lambda *args: sum(args)

print(total(1, 2, 3, 4))
```

Output:

```text
10
```

Although possible, if the logic becomes complex, a normal function is usually more readable.

---

# 81. Interview Question — Can Lambda Accept `**kwargs`?

Yes.

```python
show = lambda **kwargs: kwargs

print(show(name="Harsha", age=21))
```

Output:

```text
{'name': 'Harsha', 'age': 21}
```

---

# 82. Interview Question — Can a Lambda Return Another Lambda?

Yes.

Example:

```python
multiply = lambda x: lambda y: x * y

double = multiply(2)

print(double(5))
```

Output:

```text
10
```

This demonstrates that functions can be treated as first-class objects.

---

# 83. What Does "Functions Are First-Class Objects" Mean?

It means functions can be:

- assigned to variables
- passed as arguments
- returned from functions
- stored in collections

Example:

```python
def square(x):
    return x * x


operation = square

print(operation(5))
```

Output:

```text
25
```

This is why functions can be passed to:

```python
map()
filter()
sorted()
```

---

# 84. Important Interview Question — Can `map()` Accept a Named Function?

Yes.

```python
def double(x):
    return x * 2


numbers = [1, 2, 3]

result = list(map(double, numbers))

print(result)
```

Output:

```text
[2, 4, 6]
```

---

# 85. Important Interview Question — Can `filter()` Accept a Named Function?

Yes.

```python
def positive(x):
    return x > 0


numbers = [-2, 0, 3, 5]

result = list(filter(positive, numbers))

print(result)
```

Output:

```text
[3, 5]
```

---

# 86. Important Interview Question — Can `reduce()` Accept a Named Function?

Yes.

```python
from functools import reduce


def add(a, b):
    return a + b


numbers = [1, 2, 3, 4]

result = reduce(add, numbers)

print(result)
```

Output:

```text
10
```

---

# 87. `map()` With `None`

`map()` requires a callable as its first argument.

Unlike some languages' mapping functions, Python's `map()` does not use `None` as a special identity-function mode.

For example, this is not a valid way to simply combine two iterables:

```python
map(None, [1, 2], [3, 4])
```

If you want paired values, use:

```python
list(zip([1, 2], [3, 4]))
```

Output:

```text
[(1, 3), (2, 4)]
```

---

# 88. `filter()` With `None`

`filter(None, iterable)` is valid.

It keeps elements that are truthy.

Example:

```python
values = [0, 1, "", "Hello", None, 5]

result = filter(None, values)

print(list(result))
```

Output:

```text
[1, 'Hello', 5]
```

Falsy values such as:

```text
0
""
None
```

are removed.

---

# 89. Important Interview Question — What Does `filter(None, iterable)` Do?

It returns an iterator containing only the truthy elements.

Example:

```python
values = [0, 1, False, True, "", "Python"]

print(list(filter(None, values)))
```

Output:

```text
[1, True, 'Python']
```

---

# 90. `map()` and `filter()` With `None` Values

Example:

```python
values = [1, None, 3]

result = list(
    map(lambda x: x * 2, values)
)
```

This raises an error when the lambda tries to multiply `None`.

A safer pipeline could first filter valid values:

```python
result = list(
    map(
        lambda x: x * 2,
        filter(lambda x: x is not None, values)
    )
)

print(result)
```

Output:

```text
[2, 6]
```

---

# 91. Which Should You Learn First?

A good learning order is:

```text
1. Lambda
      ↓
2. map()
      ↓
3. filter()
      ↓
4. reduce()
      ↓
5. Combining them
      ↓
6. List comprehensions vs map/filter
      ↓
7. Iterators and lazy evaluation
```

---

# 92. Common Interview Mistakes

### Mistake 1 — Forgetting `list()`

```python
result = map(lambda x: x * 2, [1, 2, 3])

print(result)
```

Remember that Python 3 returns an iterator.

Use:

```python
print(list(result))
```

when you need the materialized values.

### Mistake 2 — Forgetting `reduce` import

Wrong:

```python
reduce(lambda a, b: a + b, [1, 2, 3])
```

Correct:

```python
from functools import reduce
```

### Mistake 3 — Using lambda for complicated logic

Prefer:

```python
def process_data(data):
    ...
```

when the logic needs multiple steps.

### Mistake 4 — Using `reduce()` when a built-in is clearer

Prefer:

```python
sum(numbers)
```

over:

```python
reduce(lambda a, b: a + b, numbers)
```

when calculating a simple sum.

---

# 93. Interview Comparison Table

| Concept | Main Purpose | Input | Output |
|---|---|---|---|
| Lambda | Short anonymous function | Arguments | One expression result |
| `map()` | Transform elements | Function + iterable(s) | Iterator |
| `filter()` | Select elements | Function + iterable | Iterator |
| `reduce()` | Accumulate elements | Function + iterable | Single result |

---

# 94. Quick Decision Guide

If interviewer gives you a problem:

### "Apply something to every element"

Think:

```python
map()
```

### "Keep only elements satisfying a condition"

Think:

```python
filter()
```

### "Combine all elements into one result"

Think:

```python
reduce()
```

### "Need a tiny temporary function"

Think:

```python
lambda
```

### "Need complex reusable logic"

Think:

```python
def
```

---

# 95. Strong Interview Answer — Explain Lambda

> Lambda is a concise way of creating an anonymous function. It is useful for small operations where I need a function temporarily, especially with functions such as `map()`, `filter()`, or `sorted()`. Since a lambda is limited to a single expression, I prefer a normal `def` function when the logic becomes complex.

---

# 96. Strong Interview Answer — Explain `map()`

> `map()` applies a function to every element of an iterable and returns a lazy iterator in Python 3. It is mainly useful for transformations. For example, I can use `map()` to convert strings to integers or calculate the square of every number.

Example:

```python
numbers = [1, 2, 3]

result = list(map(lambda x: x * x, numbers))

print(result)
```

---

# 97. Strong Interview Answer — Explain `filter()`

> `filter()` is used to select elements from an iterable based on a condition. It returns a lazy iterator in Python 3. The function supplied to `filter()` determines whether each element should be included.

Example:

```python
numbers = [1, 2, 3, 4]

result = list(filter(lambda x: x % 2 == 0, numbers))

print(result)
```

---

# 98. Strong Interview Answer — Explain `reduce()`

> `reduce()` repeatedly applies a function to pairs of elements and reduces the iterable to a single accumulated result. It is available from the `functools` module. I would use it when pairwise accumulation is appropriate, but for common operations like summing values I would usually prefer a built-in such as `sum()` because it is clearer.

Example:

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda a, b: a + b, numbers)

print(result)
```

---

# 99. Strong Interview Answer — Explain All Four Together

> Lambda is used to create a short anonymous function, `map()` is used mainly to transform every element, `filter()` is used to select elements based on a condition, and `reduce()` combines elements into a single result. In Python 3, `map()` and `filter()` return lazy iterators, while `reduce()` returns the accumulated result.

---

# 100. Final Revision

```text
LAMBDA
↓
Small anonymous function
↓
lambda x: x * 2

MAP
↓
Transform every element
↓
map(function, iterable)
↓
Returns iterator

FILTER
↓
Select elements
↓
filter(function, iterable)
↓
Returns iterator

REDUCE
↓
Combine elements
↓
reduce(function, iterable)
↓
Returns one accumulated result

IMPORTANT
↓
reduce comes from functools

MAP/FILTER
↓
Lazy in Python 3

LAMBDA
↓
One expression

PRACTICAL CHOICE
↓
Use list comprehensions when they are clearer
Use built-ins such as sum() when they directly express the operation
Use def for complex/reusable logic
```

# Interview-Level Takeaway

> **The most important thing is not just memorizing the syntax. Be able to identify the operation the interviewer is asking for: transformation → `map()`, selection → `filter()`, accumulation → `reduce()`, and a short temporary function → `lambda`. Also understand that `map()` and `filter()` are lazy iterators in Python 3, while `reduce()` produces one accumulated result.**