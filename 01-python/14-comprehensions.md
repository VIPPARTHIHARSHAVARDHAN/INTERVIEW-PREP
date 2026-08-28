# Python Comprehensions — Interview Preparation

## 1. What Are Comprehensions in Python?

Comprehensions provide a concise way to create collections such as:

- Lists
- Sets
- Dictionaries

They allow us to express a loop, transformation, and optionally a condition in a compact form.

The most commonly used types are:

```text
List Comprehension
Set Comprehension
Dictionary Comprehension
```

There is also a related concept called a **generator expression**, which creates values lazily instead of immediately creating a collection.

---

# 2. Why Are Comprehensions Important?

Comprehensions are frequently asked in Python interviews because they test whether you understand:

- `for` loops
- conditions
- expressions
- collection creation
- filtering
- transformation
- nested loops
- lazy evaluation through generator expressions

Example:

```python
numbers = [1, 2, 3, 4]

squares = [x * x for x in numbers]

print(squares)
```

Output:

```text
[1, 4, 9, 16]
```

The same operation using a normal loop:

```python
numbers = [1, 2, 3, 4]

squares = []

for x in numbers:
    squares.append(x * x)

print(squares)
```

Both produce:

```text
[1, 4, 9, 16]
```

---

# 3. What Is List Comprehension?

List comprehension is a concise way to create a list.

Basic syntax:

```python
[expression for item in iterable]
```

Example:

```python
numbers = [1, 2, 3, 4, 5]

squares = [x * x for x in numbers]

print(squares)
```

Output:

```text
[1, 4, 9, 16, 25]
```

---

# 4. How Does List Comprehension Work?

Consider:

```python
squares = [x * x for x in numbers]
```

Read it as:

```text
for every x in numbers
        ↓
calculate x * x
        ↓
put the result into a new list
```

For:

```python
numbers = [1, 2, 3]
```

the process is:

```text
1 → 1
2 → 4
3 → 9
```

Result:

```text
[1, 4, 9]
```

---

# 5. List Comprehension With a Condition

Syntax:

```python
[expression for item in iterable if condition]
```

Example:

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [x for x in numbers if x % 2 == 0]

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

The condition decides which elements are included.

---

# 6. List Comprehension With Transformation and Condition

```python
numbers = [1, 2, 3, 4, 5, 6]

squares = [x * x for x in numbers if x % 2 == 0]

print(squares)
```

Output:

```text
[4, 16, 36]
```

Process:

```text
Original:
[1, 2, 3, 4, 5, 6]

Keep even:
[2, 4, 6]

Square:
[4, 16, 36]
```

---

# 7. List Comprehension With an `if-else`

When `if-else` is used to choose the output value, the syntax changes.

Syntax:

```python
[expression_if_true if condition else expression_if_false for item in iterable]
```

Example:

```python
numbers = [1, 2, 3, 4, 5]

result = ["Even" if x % 2 == 0 else "Odd" for x in numbers]

print(result)
```

Output:

```text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

### Important Interview Point

Compare:

```python
[x for x in numbers if x % 2 == 0]
```

with:

```python
["Even" if x % 2 == 0 else "Odd" for x in numbers]
```

The first one **filters** elements.

The second one **chooses what value to produce** for every element.

---

# 8. Filtering vs Conditional Expression

### Filtering

```python
[x for x in numbers if x % 2 == 0]
```

Result:

```text
[2, 4]
```

Odd values are removed.

### `if-else`

```python
["Even" if x % 2 == 0 else "Odd" for x in numbers]
```

Result:

```text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

Every input produces an output.

---

# 9. Creating a List of Strings

```python
names = ["harsha", "ravi", "anu"]

upper_names = [name.upper() for name in names]

print(upper_names)
```

Output:

```text
['HARSHA', 'RAVI', 'ANU']
```

---

# 10. Converting Strings to Integers

```python
values = ["10", "20", "30", "40"]

numbers = [int(x) for x in values]

print(numbers)
```

Output:

```text
[10, 20, 30, 40]
```

This is a common data-processing operation.

---

# 11. Extracting Values From a List of Dictionaries

```python
employees = [
    {"name": "Harsha", "salary": 50000},
    {"name": "Ravi", "salary": 60000},
    {"name": "Anu", "salary": 70000}
]

salaries = [employee["salary"] for employee in employees]

print(salaries)
```

Output:

```text
[50000, 60000, 70000]
```

This pattern is useful when processing structured records.

---

# 12. Real-World Example — Filtering Employee Data

```python
employees = [
    {"name": "Harsha", "salary": 50000},
    {"name": "Ravi", "salary": 30000},
    {"name": "Anu", "salary": 70000}
]

high_salary = [
    employee
    for employee in employees
    if employee["salary"] > 40000
]

print(high_salary)
```

Output:

```text
[
    {'name': 'Harsha', 'salary': 50000},
    {'name': 'Anu', 'salary': 70000}
]
```

---

# 13. What Is Set Comprehension?

Set comprehension creates a set using comprehension syntax.

Syntax:

```python
{expression for item in iterable}
```

Example:

```python
numbers = [1, 2, 2, 3, 3, 4]

squares = {x * x for x in numbers}

print(squares)
```

Output:

```text
{1, 4, 9, 16}
```

Duplicate results are automatically removed because a set stores unique elements.

---

# 14. List Comprehension vs Set Comprehension

### List

```python
numbers = [1, 2, 2, 3]

result = [x for x in numbers]

print(result)
```

Output:

```text
[1, 2, 2, 3]
```

### Set

```python
result = {x for x in numbers}

print(result)
```

Output:

```text
{1, 2, 3}
```

The major difference is the resulting collection type and its behavior.

---

# 15. Set Comprehension With a Condition

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = {x for x in numbers if x % 2 == 0}

print(even_numbers)
```

Output:

```text
{2, 4, 6}
```

---

# 16. Creating Unique Characters Using Set Comprehension

```python
word = "programming"

unique = {char for char in word}

print(unique)
```

The exact display order of a set should not be relied upon.

The important result is that only unique characters are stored.

---

# 17. What Is Dictionary Comprehension?

Dictionary comprehension creates dictionaries using a concise syntax.

Syntax:

```python
{key_expression: value_expression for item in iterable}
```

Example:

```python
numbers = [1, 2, 3, 4]

squares = {x: x * x for x in numbers}

print(squares)
```

Output:

```text
{1: 1, 2: 4, 3: 9, 4: 16}
```

---

# 18. Dictionary Comprehension With a Condition

```python
numbers = [1, 2, 3, 4, 5, 6]

even_squares = {
    x: x * x
    for x in numbers
    if x % 2 == 0
}

print(even_squares)
```

Output:

```text
{2: 4, 4: 16, 6: 36}
```

---

# 19. Creating a Dictionary From Two Lists

```python
names = ["Harsha", "Ravi", "Anu"]
marks = [85, 75, 90]

result = {
    name: mark
    for name, mark in zip(names, marks)
}

print(result)
```

Output:

```text
{'Harsha': 85, 'Ravi': 75, 'Anu': 90}
```

---

# 20. Creating a Dictionary With Transformed Values

```python
prices = {
    "laptop": 50000,
    "phone": 30000,
    "tablet": 20000
}

discounted = {
    item: price * 0.9
    for item, price in prices.items()
}

print(discounted)
```

This creates a new dictionary with prices reduced by 10%.

---

# 21. Filtering a Dictionary

```python
prices = {
    "laptop": 50000,
    "phone": 30000,
    "tablet": 20000
}

expensive = {
    item: price
    for item, price in prices.items()
    if price > 30000
}

print(expensive)
```

Output:

```text
{'laptop': 50000}
```

---

# 22. Nested List Comprehension

A list comprehension can contain more than one `for`.

Example:

```python
result = [
    (x, y)
    for x in [1, 2]
    for y in [10, 20]
]

print(result)
```

Output:

```text
[(1, 10), (1, 20), (2, 10), (2, 20)]
```

This is equivalent to:

```python
result = []

for x in [1, 2]:
    for y in [10, 20]:
        result.append((x, y))

print(result)
```

---

# 23. How to Read Nested Comprehension

For:

```python
[
    (x, y)
    for x in [1, 2]
    for y in [10, 20]
]
```

read it as:

```text
for x in [1, 2]:
    for y in [10, 20]:
        create (x, y)
```

The order of the `for` clauses follows the same order as nested loops.

---

# 24. Nested List Comprehension With Condition

```python
result = [
    (x, y)
    for x in range(1, 4)
    for y in range(1, 4)
    if x != y
]

print(result)
```

Output:

```text
[(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
```

---

# 25. Flattening a Nested List

Suppose:

```python
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]
```

We can flatten it using:

```python
flat = [
    value
    for row in matrix
    for value in row
]

print(flat)
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

Equivalent loops:

```python
flat = []

for row in matrix:
    for value in row:
        flat.append(value)

print(flat)
```

---

# 26. Real-World Example — Flattening Data

Suppose an application receives batches of records:

```python
batches = [
    ["A", "B"],
    ["C", "D"],
    ["E", "F"]
]

records = [
    record
    for batch in batches
    for record in batch
]

print(records)
```

Output:

```text
['A', 'B', 'C', 'D', 'E', 'F']
```

This pattern is useful when processing nested collections.

---

# 27. Nested List Comprehension for a Matrix

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

result = [
    value
    for row in matrix
    for value in row
]

print(result)
```

Output:

```text
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

# 28. Matrix Transpose Using Comprehension

Given:

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]
```

Transpose:

```python
transposed = [
    [row[i] for row in matrix]
    for i in range(len(matrix[0]))
]

print(transposed)
```

Output:

```text
[[1, 4], [2, 5], [3, 6]]
```

For production code, `zip(*matrix)` is often a cleaner alternative:

```python
transposed = [list(row) for row in zip(*matrix)]
```

---

# 29. Can We Use Functions Inside Comprehensions?

Yes.

Example:

```python
def square(x):
    return x * x


numbers = [1, 2, 3, 4]

result = [square(x) for x in numbers]

print(result)
```

Output:

```text
[1, 4, 9, 16]
```

---

# 30. Comprehension vs `map()`

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

### Interview Answer

> Both can perform transformations. I often prefer list comprehensions when the transformation is simple because the syntax is concise and readable. `map()` is also useful when I already have a function that naturally describes the transformation.

---

# 31. Comprehension vs `filter()`

Using `filter()`:

```python
numbers = [1, 2, 3, 4, 5]

result = list(filter(lambda x: x % 2 == 0, numbers))
```

Using comprehension:

```python
result = [x for x in numbers if x % 2 == 0]
```

Both produce:

```text
[2, 4]
```

---

# 32. Comprehension vs Normal Loop

### Normal loop

```python
numbers = [1, 2, 3, 4]

squares = []

for x in numbers:
    squares.append(x * x)
```

### Comprehension

```python
squares = [x * x for x in numbers]
```

The comprehension is more compact.

### Interview Answer

> I use comprehensions for simple transformations and filtering. If the logic becomes complicated or contains multiple steps, I prefer a normal loop or a separate function because readability is more important than making the code shorter.

---

# 33. Are Comprehensions Always Better Than Loops?

No.

Example of a simple comprehension:

```python
squares = [x * x for x in numbers]
```

This is readable.

But if the logic becomes complicated:

```python
result = [
    ...
    for ...
    if ...
    for ...
    if ...
]
```

a normal loop may be easier to understand.

### Important Principle

> **Do not sacrifice readability just to make code shorter.**

---

# 34. What Is a Generator Expression?

A generator expression looks similar to a list comprehension but uses parentheses.

List comprehension:

```python
[x * x for x in numbers]
```

Generator expression:

```python
(x * x for x in numbers)
```

The important difference is that the list comprehension creates the list immediately, while the generator expression produces values lazily.

---

# 35. List Comprehension vs Generator Expression

### List comprehension

```python
numbers = [1, 2, 3, 4]

result = [x * x for x in numbers]

print(result)
```

Creates:

```text
[1, 4, 9, 16]
```

### Generator expression

```python
numbers = [1, 2, 3, 4]

result = (x * x for x in numbers)

print(result)
```

This creates a generator object.

Values are produced when iterated.

---

# 36. Why Use a Generator Expression?

Generator expressions are useful when:

- the complete collection is not needed at once
- data may be large
- we want lazy evaluation
- we want to process values one at a time

Example:

```python
numbers = range(1000000)

squares = (x * x for x in numbers)
```

The generator does not create a million-element list immediately.

---

# 37. Using a Generator Expression With `sum()`

```python
numbers = range(1, 6)

total = sum(x * x for x in numbers)

print(total)
```

Output:

```text
55
```

This is concise and avoids creating an intermediate list.

---

# 38. Important Interview Question — What Is the Difference Between List Comprehension and Generator Expression?

### List comprehension

```python
[x * 2 for x in numbers]
```

- creates a list
- values are materialized immediately
- supports indexing because the result is a list
- may require more memory for large results

### Generator expression

```python
(x * 2 for x in numbers)
```

- creates a generator
- values are produced lazily
- generally uses less memory for large sequences
- values are consumed as needed

### Strong Interview Answer

> A list comprehension immediately creates a list, whereas a generator expression creates a generator that produces values lazily. For small collections where I need the complete result, I use a list comprehension. For large or streaming-style processing where I only need values one at a time, a generator expression can be more memory-efficient.

---

# 39. Can We Use `if-else` in a Generator Expression?

Yes.

```python
numbers = [1, 2, 3, 4]

result = (
    "Even" if x % 2 == 0 else "Odd"
    for x in numbers
)

print(list(result))
```

Output:

```text
['Odd', 'Even', 'Odd', 'Even']
```

---

# 40. Can We Use Nested Loops in Comprehensions?

Yes.

Example:

```python
result = [
    x * y
    for x in [1, 2, 3]
    for y in [10, 20]
]

print(result)
```

Output:

```text
[10, 20, 20, 40, 30, 60]
```

Equivalent:

```python
result = []

for x in [1, 2, 3]:
    for y in [10, 20]:
        result.append(x * y)
```

---

# 41. Important Output Question

```python
numbers = [1, 2, 3, 4]

result = [x * 2 for x in numbers]

print(result)
```

Output:

```text
[2, 4, 6, 8]
```

---

# 42. Important Output Question

```python
numbers = [1, 2, 3, 4, 5]

result = [x for x in numbers if x > 3]

print(result)
```

Output:

```text
[4, 5]
```

---

# 43. Important Output Question

```python
numbers = [1, 2, 3, 4]

result = [x * x for x in numbers if x % 2 == 0]

print(result)
```

Output:

```text
[4, 16]
```

---

# 44. Important Output Question

```python
numbers = [1, 2, 3]

result = ["Even" if x % 2 == 0 else "Odd" for x in numbers]

print(result)
```

Output:

```text
['Odd', 'Even', 'Odd']
```

---

# 45. Important Output Question — Set Comprehension

```python
numbers = [1, 2, 2, 3, 3, 3]

result = {x for x in numbers}

print(result)
```

Output contains:

```text
{1, 2, 3}
```

The exact order should not be assumed.

---

# 46. Important Output Question — Dictionary Comprehension

```python
numbers = [1, 2, 3]

result = {x: x * x for x in numbers}

print(result)
```

Output:

```text
{1: 1, 2: 4, 3: 9}
```

---

# 47. Important Output Question — Nested Comprehension

```python
result = [
    (x, y)
    for x in [1, 2]
    for y in [3, 4]
]

print(result)
```

Output:

```text
[(1, 3), (1, 4), (2, 3), (2, 4)]
```

---

# 48. Important Output Question — Flattening

```python
matrix = [
    [1, 2],
    [3, 4]
]

result = [
    value
    for row in matrix
    for value in row
]

print(result)
```

Output:

```text
[1, 2, 3, 4]
```

---

# 49. Important Output Question — Conditional Expression

```python
numbers = [1, 2, 3, 4]

result = [
    x * 2 if x % 2 == 0 else x
    for x in numbers
]

print(result)
```

Output:

```text
[1, 4, 3, 8]
```

---

# 50. Important Output Question — Dictionary Filtering

```python
data = {
    "a": 10,
    "b": 20,
    "c": 30
}

result = {
    key: value
    for key, value in data.items()
    if value >= 20
}

print(result)
```

Output:

```text
{'b': 20, 'c': 30}
```

---

# 51. Important Interview Question — Can a Comprehension Contain Multiple Conditions?

Yes.

Example:

```python
numbers = range(1, 11)

result = [
    x
    for x in numbers
    if x % 2 == 0
    if x > 4
]

print(result)
```

Output:

```text
[6, 8, 10]
```

This is equivalent to:

```python
result = [
    x
    for x in numbers
    if x % 2 == 0 and x > 4
]
```

The second form is often clearer.

---

# 52. Multiple Conditions With `and`

```python
numbers = range(1, 11)

result = [
    x
    for x in numbers
    if x % 2 == 0 and x > 4
]

print(result)
```

Output:

```text
[6, 8, 10]
```

---

# 53. Multiple Conditions With `or`

```python
numbers = range(1, 11)

result = [
    x
    for x in numbers
    if x == 2 or x == 8
]

print(result)
```

Output:

```text
[2, 8]
```

---

# 54. Can Comprehensions Work With Strings?

Yes.

```python
word = "Python"

letters = [char.upper() for char in word]

print(letters)
```

Output:

```text
['P', 'Y', 'T', 'H', 'O', 'N']
```

---

# 55. Extracting Vowels From a String

```python
word = "programming"

vowels = [
    char
    for char in word
    if char in "aeiou"
]

print(vowels)
```

Output:

```text
['o', 'a', 'i']
```

---

# 56. Creating a Dictionary of Character Counts

A simple dictionary comprehension can create a mapping:

```python
word = "abc"

result = {
    char: word.count(char)
    for char in set(word)
}

print(result)
```

Possible output:

```text
{'a': 1, 'b': 1, 'c': 1}
```

Since a set is used, dictionary display order should not be relied upon for the conceptual result.

For large strings, repeatedly calling `count()` is inefficient; `collections.Counter` is the better tool.

---

# 57. Real-World Example — Data Transformation

Suppose raw data contains:

```python
raw_data = ["10", "20", "30", "40"]
```

Transform it:

```python
clean_data = [int(value) for value in raw_data]

print(clean_data)
```

Output:

```text
[10, 20, 30, 40]
```

This is a common transformation pattern in data processing.

---

# 58. Real-World Example — Filtering Valid Records

```python
records = [
    {"name": "Harsha", "age": 21},
    {"name": "Ravi", "age": 17},
    {"name": "Anu", "age": 25}
]

adults = [
    record
    for record in records
    if record["age"] >= 18
]

print(adults)
```

Output:

```text
[
    {'name': 'Harsha', 'age': 21},
    {'name': 'Anu', 'age': 25}
]
```

---

# 59. Real-World Example — Extracting Required Fields

```python
records = [
    {"name": "Harsha", "age": 21, "city": "Hyderabad"},
    {"name": "Ravi", "age": 22, "city": "Chennai"},
    {"name": "Anu", "age": 20, "city": "Bangalore"}
]

names = [record["name"] for record in records]

print(names)
```

Output:

```text
['Harsha', 'Ravi', 'Anu']
```

---

# 60. Real-World Example — Creating Lookup Data

```python
employees = [
    ("E101", "Harsha"),
    ("E102", "Ravi"),
    ("E103", "Anu")
]

employee_map = {
    employee_id: name
    for employee_id, name in employees
}

print(employee_map)
```

Output:

```text
{
    'E101': 'Harsha',
    'E102': 'Ravi',
    'E103': 'Anu'
}
```

This can be useful when transforming tabular records into lookup dictionaries.

---

# 61. Important Interview Question — What Is the Main Advantage of Comprehensions?

A strong answer:

> The main advantage is that comprehensions provide a concise and readable way to create collections from existing iterables, especially when the operation involves simple transformation or filtering.

Example:

```python
squares = [x * x for x in numbers if x % 2 == 0]
```

---

# 62. Important Interview Question — What Are the Disadvantages of Comprehensions?

Important points:

- Complex comprehensions can become difficult to read.
- They are not always the best replacement for normal loops.
- Nested comprehensions can become confusing.
- Large list comprehensions create the complete list in memory.
- Debugging complicated comprehension logic can be harder.

### Strong Interview Answer

> I use comprehensions when they make the logic clearer and shorter. For complex multi-step processing, I prefer normal loops or separate functions because maintainability and readability are more important than compact syntax.

---

# 63. Important Interview Question — Do List Comprehensions Always Improve Performance?

Not necessarily in a way that should be treated as the main reason to use them.

Comprehensions are implemented efficiently in Python and are often fast for straightforward operations, but performance depends on the actual operation.

The main reason to use them is:

```text
readability + concise collection creation
```

not blindly assuming they are always faster.

---

# 64. Important Interview Question — What Happens When a List Comprehension Is Assigned to a Variable?

Example:

```python
result = [x * 2 for x in [1, 2, 3]]

print(type(result))
```

Output indicates:

```text
<class 'list'>
```

The result is an actual list.

---

# 65. Important Interview Question — What Happens With a Set Comprehension?

```python
result = {x * 2 for x in [1, 2, 3]}

print(type(result))
```

The result is a:

```text
set
```

---

# 66. Important Interview Question — What Happens With a Dictionary Comprehension?

```python
result = {x: x * 2 for x in [1, 2, 3]}

print(type(result))
```

The result is a:

```text
dict
```

---

# 67. Important Interview Question — Can We Use `else` Without `if` in a Comprehension?

No.

This is invalid:

```python
[x else 0 for x in numbers]
```

If using `else`, it must be part of a conditional expression:

```python
[x if x > 0 else 0 for x in numbers]
```

---

# 68. Important Interview Question — Where Does `if` Go in a Comprehension?

For filtering:

```python
[expression for item in iterable if condition]
```

Example:

```python
[x for x in numbers if x > 5]
```

For choosing between two output values:

```python
[expression1 if condition else expression2 for item in iterable]
```

Example:

```python
[x if x > 5 else 0 for x in numbers]
```

This distinction is frequently tested in interviews.

---

# 69. Important Interview Question — Can We Use `break` or `continue` Inside a Comprehension?

No.

Comprehensions do not directly support statements such as:

```python
break
continue
```

If the processing requires `break` or `continue`, use a normal loop.

---

# 70. Important Interview Question — Can We Use Assignment Inside a Comprehension?

Python supports assignment expressions using the walrus operator `:=`, but they should be used carefully.

Example:

```python
numbers = [1, 2, 3, 4]

result = [
    doubled
    for x in numbers
    if (doubled := x * 2) > 4
]

print(result)
```

Output:

```text
[6, 8]
```

However, this is more advanced syntax and can reduce readability. Use it only when it genuinely makes the code clearer.

---

# 71. Important Interview Question — Are Comprehensions Scope-Isolated?

List comprehensions have their own comprehension scope in Python 3.

Example:

```python
x = 100

result = [x for x in range(3)]

print(x)
```

Output:

```text
100
```

The comprehension's loop variable `x` does not overwrite the outer `x`.

---

# 72. Important Interview Question — What Is the Scope of a Comprehension Variable?

In Python 3:

```python
result = [x for x in range(5)]
```

the `x` used as the comprehension variable does not leak into the surrounding scope.

This differs from the behavior of list comprehensions in Python 2.

---

# 73. Important Interview Question — Can a Comprehension Use a Function Defined Outside?

Yes.

```python
def square(x):
    return x * x


numbers = [1, 2, 3]

result = [square(x) for x in numbers]

print(result)
```

Output:

```text
[1, 4, 9]
```

---

# 74. Important Interview Question — Can Comprehensions Be Nested?

Yes.

Example:

```python
result = [
    [x * y for y in range(1, 4)]
    for x in range(1, 4)
]

print(result)
```

Output:

```text
[
    [1, 2, 3],
    [2, 4, 6],
    [3, 6, 9]
]
```

This creates a multiplication-table-like structure.

---

# 75. When Should You Avoid Nested Comprehensions?

Avoid them when they become difficult to read.

For example, a deeply nested comprehension with several conditions may be technically valid but difficult for another developer to maintain.

Prefer:

```python
for ...
    for ...
        if ...
```

when the logic is complex.

### Interview Answer

> Nested comprehensions are useful for simple nested transformations, but I avoid deeply nested comprehensions because readability and maintainability become worse.

---

# 76. Important Interview Question — What Is the Difference Between a List Comprehension and a Generator Expression?

Short interview answer:

> A list comprehension creates the complete list immediately, while a generator expression creates a generator and produces values lazily as they are requested. Therefore, generator expressions are often more memory-efficient for large sequences.

Example:

```python
list_result = [x * 2 for x in range(5)]

generator_result = (x * 2 for x in range(5))
```

---

# 77. Important Interview Question — What Is the Difference Between a Set Comprehension and Dictionary Comprehension?

### Set:

```python
{x * 2 for x in numbers}
```

Produces values:

```text
{2, 4, 6}
```

### Dictionary:

```python
{x: x * 2 for x in numbers}
```

Produces key-value pairs:

```text
{1: 2, 2: 4, 3: 6}
```

### Interview Answer

> Set comprehensions produce unique values, while dictionary comprehensions produce key-value pairs.

---

# 78. Common Interview Traps

### Trap 1 — Confusing filtering with `if-else`

Filtering:

```python
[x for x in numbers if x > 5]
```

Conditional output:

```python
[x if x > 5 else 0 for x in numbers]
```

### Trap 2 — Forgetting set uniqueness

```python
{x for x in [1, 1, 2, 2]}
```

produces:

```text
{1, 2}
```

### Trap 3 — Assuming generator expressions create lists

```python
(x * 2 for x in numbers)
```

creates a generator, not a list.

### Trap 4 — Making comprehensions unnecessarily complicated

Shorter code is not automatically better code.

---

# 79. Practical Decision Guide

When you see:

### "Create a transformed list"

Think:

```python
[x * 2 for x in numbers]
```

### "Create a filtered list"

Think:

```python
[x for x in numbers if condition]
```

### "Create a set of unique transformed values"

Think:

```python
{x * 2 for x in numbers}
```

### "Create key-value pairs"

Think:

```python
{key: value for item in items}
```

### "Process a large sequence lazily"

Think:

```python
(x * 2 for x in numbers)
```

### "Logic is complex"

Think:

```python
for
```

or a separate function.

---

# 80. Interview Revision Table

| Type | Syntax | Result |
|---|---|---|
| List comprehension | `[expr for x in iterable]` | List |
| Set comprehension | `{expr for x in iterable}` | Set |
| Dictionary comprehension | `{key: value for x in iterable}` | Dictionary |
| Generator expression | `(expr for x in iterable)` | Generator |

---

# 81. Final Interview Summary

```text
COMPREHENSIONS
      ↓
Concise way to create collections
      ↓
LIST
      ↓
[expression for item in iterable]
      ↓
SET
      ↓
{expression for item in iterable}
      ↓
DICTIONARY
      ↓
{key: value for item in iterable}
      ↓
GENERATOR EXPRESSION
      ↓
(expression for item in iterable)
      ↓
Lazy evaluation
```

## Most Important Patterns

```python
# Transformation
[x * 2 for x in numbers]

# Filtering
[x for x in numbers if x % 2 == 0]

# Transformation + filtering
[x * x for x in numbers if x % 2 == 0]

# Conditional output
["Even" if x % 2 == 0 else "Odd" for x in numbers]

# Set comprehension
{x * 2 for x in numbers}

# Dictionary comprehension
{x: x * x for x in numbers}

# Generator expression
(x * 2 for x in numbers)
```

## Final Interview-Level Takeaway

> **Comprehensions are a concise way to create collections using expressions, iteration, and optional conditions. List comprehensions create lists, set comprehensions create unique sets, dictionary comprehensions create key-value mappings, and generator expressions produce values lazily. I use comprehensions when they make simple transformations or filtering clearer, but for complex logic I prefer normal loops or functions because readability and maintainability are more important than compact syntax.**