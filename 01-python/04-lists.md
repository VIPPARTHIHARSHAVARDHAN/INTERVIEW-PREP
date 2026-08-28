# Python Lists — Interview Preparation

## 1. What Is a List in Python?

A **list** is an ordered, mutable collection of elements.

A list can contain:

- Integers
- Strings
- Floats
- Booleans
- Other lists
- Tuples
- Dictionaries
- Objects
- Mixed data types

### Example

```python
numbers = [10, 20, 30, 40]

skills = ["Python", "SQL", "PySpark"]

mixed = [10, "Python", 3.14, True]

print(numbers)
print(skills)
print(mixed)
```

### Output

```text
[10, 20, 30, 40]
['Python', 'SQL', 'PySpark']
[10, 'Python', 3.14, True]
```

### Important Properties

A Python list is:

- **Ordered**
- **Mutable**
- **Indexed**
- **Allows duplicate values**
- **Allows different data types**
- **Dynamically sized**

### Real-World Example

In data processing, a list can temporarily hold records, column names, filenames, or transformed values.

```python
files = [
    "youtube_data.csv",
    "youtube_statistics.csv",
    "reference_data.json"
]
```

---

# 2. Why Is a List Called Mutable?

A list is mutable because its elements can be changed after the list is created.

### Example

```python
skills = ["Python", "SQL", "Java"]

skills[2] = "PySpark"

print(skills)
```

### Output

```text
['Python', 'SQL', 'PySpark']
```

The same list can be modified.

This is different from strings and tuples, which are immutable.

### Interview Answer

> A list is mutable because its elements can be modified, added, or removed after the list has been created.

---

# 3. How Do You Access Elements in a List?

Lists use zero-based indexing.

```python
skills = ["Python", "SQL", "PySpark"]

print(skills[0])
print(skills[1])
print(skills[2])
```

### Output

```text
Python
SQL
PySpark
```

---

# 4. What Is Negative Indexing in a List?

Negative indexes access elements from the end.

```python
skills = ["Python", "SQL", "PySpark"]

print(skills[-1])
print(skills[-2])
```

### Output

```text
PySpark
SQL
```

The indexes are:

```text
Python   SQL   PySpark
  0       1       2
 -3      -2      -1
```

---

# 5. What Happens If You Access an Invalid List Index?

Python raises an `IndexError`.

```python
skills = ["Python", "SQL"]

print(skills[5])
```

Output:

```text
IndexError: list index out of range
```

However, slicing beyond the list length does not produce the same error.

```python
skills = ["Python", "SQL"]

print(skills[1:10])
```

Output:

```text
['SQL']
```

---

# 6. What Is List Slicing?

List slicing extracts a portion of a list.

Syntax:

```python
list[start:stop:step]
```

The `stop` index is excluded.

### Example

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[1:4])
```

### Output

```text
[20, 30, 40]
```

---

# 7. How Do You Reverse a List Using Slicing?

Use:

```python
[::-1]
```

### Example

```python
numbers = [10, 20, 30, 40]

reversed_numbers = numbers[::-1]

print(reversed_numbers)
```

### Output

```text
[40, 30, 20, 10]
```

This creates a new list.

---

# 8. What Is the Difference Between `reverse()` and `[::-1]`?

This is an important interview question.

### `reverse()`

Modifies the existing list in place.

```python
numbers = [1, 2, 3, 4]

result = numbers.reverse()

print(numbers)
print(result)
```

Output:

```text
[4, 3, 2, 1]
None
```

### `[::-1]`

Creates a new reversed list.

```python
numbers = [1, 2, 3, 4]

result = numbers[::-1]

print(numbers)
print(result)
```

Output:

```text
[1, 2, 3, 4]
[4, 3, 2, 1]
```

### Interview Answer

> `reverse()` modifies the list in place and returns `None`, whereas `[::-1]` creates a new reversed list and leaves the original unchanged.

---

# 9. What Is the Difference Between `sort()` and `sorted()`?

This is one of the most important list interview questions.

### `sort()`

Sorts the list in place.

```python
numbers = [5, 2, 8, 1]

result = numbers.sort()

print(numbers)
print(result)
```

Output:

```text
[1, 2, 5, 8]
None
```

### `sorted()`

Returns a new sorted list.

```python
numbers = [5, 2, 8, 1]

result = sorted(numbers)

print(numbers)
print(result)
```

Output:

```text
[5, 2, 8, 1]
[1, 2, 5, 8]
```

### Interview Answer

> `list.sort()` sorts the existing list in place and returns `None`, while `sorted()` accepts an iterable and returns a new sorted list without modifying the original list.

---

# 10. Can `sorted()` Work With Other Iterables?

Yes.

`sorted()` accepts an iterable, not just a list.

### Example

```python
numbers = (5, 2, 8, 1)

result = sorted(numbers)

print(result)
```

Output:

```text
[1, 2, 5, 8]
```

The result is always a list.

---

# 11. How Do You Add an Element to a List?

Use `append()` to add one element at the end.

```python
skills = ["Python", "SQL"]

skills.append("PySpark")

print(skills)
```

Output:

```text
['Python', 'SQL', 'PySpark']
```

---

# 12. What Is the Difference Between `append()` and `extend()`?

This is a very common interview question.

### `append()`

Adds its argument as **one element**.

```python
numbers = [1, 2]

numbers.append([3, 4])

print(numbers)
```

Output:

```text
[1, 2, [3, 4]]
```

### `extend()`

Adds elements from an iterable individually.

```python
numbers = [1, 2]

numbers.extend([3, 4])

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

### Interview Answer

> `append()` adds its argument as a single element, whereas `extend()` iterates over the supplied iterable and adds its elements individually.

---

# 13. What Happens When You Use `append()` With a String?

A string is added as one element.

```python
items = [1, 2]

items.append("Python")

print(items)
```

Output:

```text
[1, 2, 'Python']
```

---

# 14. What Happens When You Use `extend()` With a String?

Because a string is iterable, `extend()` adds its characters individually.

```python
items = [1, 2]

items.extend("Python")

print(items)
```

Output:

```text
[1, 2, 'P', 'y', 't', 'h', 'o', 'n']
```

### Interview Trap

This is why you should understand that `extend()` works with an **iterable**, not specifically with lists.

---

# 15. How Do You Insert an Element at a Specific Position?

Use `insert(index, value)`.

### Example

```python
skills = ["Python", "PySpark"]

skills.insert(1, "SQL")

print(skills)
```

Output:

```text
['Python', 'SQL', 'PySpark']
```

---

# 16. What Happens If the `insert()` Index Is Too Large?

The element is added at the end.

```python
numbers = [1, 2, 3]

numbers.insert(100, 10)

print(numbers)
```

Output:

```text
[1, 2, 3, 10]
```

For a very negative index, it is inserted near the beginning according to Python's indexing rules.

---

# 17. How Do You Remove an Element From a List?

There are several methods, and they behave differently.

### `remove()`

Removes the first matching value.

```python
numbers = [10, 20, 30, 20]

numbers.remove(20)

print(numbers)
```

Output:

```text
[10, 30, 20]
```

---

# 18. What Is the Difference Between `remove()` and `pop()`?

### `remove(value)`

Removes by value.

```python
numbers = [10, 20, 30]

numbers.remove(20)

print(numbers)
```

Output:

```text
[10, 30]
```

### `pop(index)`

Removes by index and returns the removed element.

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

### Interview Answer

> `remove()` searches for and removes the first matching value, while `pop()` removes an element at a specified index and returns that removed element.

---

# 19. What Does `pop()` Do Without an Index?

It removes and returns the last element.

```python
numbers = [10, 20, 30]

value = numbers.pop()

print(value)
print(numbers)
```

Output:

```text
30
[10, 20]
```

---

# 20. What Is the Difference Between `del`, `remove()`, and `pop()`?

| Operation | Works by | Returns removed value? |
|---|---|---|
| `remove(value)` | Value | No |
| `pop(index)` | Index | Yes |
| `del list[index]` | Index | No |
| `del list[start:stop]` | Slice | No |

### Example

```python
numbers = [10, 20, 30, 40]

del numbers[1]

print(numbers)
```

Output:

```text
[10, 30, 40]
```

---

# 21. What Happens If `remove()` Cannot Find the Value?

It raises `ValueError`.

```python
numbers = [1, 2, 3]

numbers.remove(10)
```

Output:

```text
ValueError: list.remove(x): x not in list
```

---

# 22. What Happens If `pop()` Uses an Invalid Index?

It raises `IndexError`.

```python
numbers = [1, 2, 3]

numbers.pop(10)
```

Output:

```text
IndexError: pop index out of range
```

---

# 23. How Do You Find the Length of a List?

Use `len()`.

```python
skills = ["Python", "SQL", "PySpark"]

print(len(skills))
```

Output:

```text
3
```

---

# 24. How Do You Check Whether an Element Exists in a List?

Use the `in` operator.

```python
skills = ["Python", "SQL", "PySpark"]

print("Python" in skills)
print("Java" in skills)
```

Output:

```text
True
False
```

---

# 25. How Do You Find the Index of an Element?

Use `index()`.

```python
skills = ["Python", "SQL", "PySpark"]

print(skills.index("SQL"))
```

Output:

```text
1
```

If the value does not exist, `ValueError` is raised.

---

# 26. How Do You Count an Element in a List?

Use `count()`.

```python
numbers = [1, 2, 2, 3, 2]

print(numbers.count(2))
```

Output:

```text
3
```

---

# 27. How Do You Clear a List?

Use `clear()`.

```python
numbers = [1, 2, 3]

numbers.clear()

print(numbers)
```

Output:

```text
[]
```

`clear()` modifies the existing list.

---

# 28. What Is the Difference Between `clear()` and Reassignment?

### `clear()`

```python
numbers = [1, 2, 3]

numbers.clear()

print(numbers)
```

The same list object is emptied.

### Reassignment

```python
numbers = [1, 2, 3]

numbers = []

print(numbers)
```

The variable is assigned to a new list object.

This difference can matter when multiple variables refer to the same list.

---

# 29. What Is List Aliasing?

Aliasing occurs when two variables refer to the same list object.

### Example

```python
a = [1, 2, 3]

b = a

b.append(4)

print(a)
print(b)
```

Output:

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
```

Both variables refer to the same list.

### Interview Answer

> List aliasing occurs when multiple variables reference the same list object, so modifying the list through one variable is visible through the other.

---

# 30. How Do You Copy a List?

There are several common ways to create a shallow copy.

### Using `copy()`

```python
a = [1, 2, 3]

b = a.copy()

b.append(4)

print(a)
print(b)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

### Using slicing

```python
b = a[:]
```

### Using `list()`

```python
b = list(a)
```

All create a new outer list.

---

# 31. What Is the Difference Between Assignment and Copying?

### Assignment

```python
a = [1, 2, 3]

b = a
```

No new list is created.

### Copy

```python
a = [1, 2, 3]

b = a.copy()
```

A new outer list is created.

### Interview Answer

> Assignment makes another reference to the same list, while copying creates a separate outer list.

---

# 32. What Is a Shallow Copy of a List?

A shallow copy creates a new outer list, but nested objects inside it are still shared.

### Example

```python
a = [[1, 2], [3, 4]]

b = a.copy()

b[0].append(100)

print(a)
print(b)
```

Output:

```text
[[1, 2, 100], [3, 4]]
[[1, 2, 100], [3, 4]]
```

The outer lists are different, but the nested lists are shared.

---

# 33. What Is a Deep Copy?

A deep copy recursively copies nested objects as well.

Use the `copy` module.

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.deepcopy(a)

b[0].append(100)

print(a)
print(b)
```

Output:

```text
[[1, 2], [3, 4]]
[[1, 2, 100], [3, 4]]
```

### Interview Answer

> A shallow copy creates a new outer container while keeping references to nested objects, whereas a deep copy recursively creates independent copies of nested objects.

---

# 34. What Is a Nested List?

A list containing another list is called a nested list.

### Example

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[0])
print(matrix[1][2])
```

Output:

```text
[1, 2, 3]
6
```

### Real-World Example

Nested lists can represent simple tabular data:

```python
employees = [
    ["Harsha", "Python"],
    ["Rahul", "SQL"],
    ["Anita", "PySpark"]
]
```

For production data processing, specialized structures such as DataFrames are often more appropriate.

---

# 35. What Is List Comprehension?

List comprehension provides a concise way to create a list from an iterable.

### Normal Loop

```python
numbers = [1, 2, 3, 4, 5]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)
```

### List Comprehension

```python
numbers = [1, 2, 3, 4, 5]

squares = [number * number for number in numbers]

print(squares)
```

### Output

```text
[1, 4, 9, 16, 25]
```

### Interview Answer

> List comprehension is a concise way to create a new list by applying an expression to elements of an iterable, optionally with a condition.

---

# 36. How Do You Add a Condition in a List Comprehension?

### Example

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [number for number in numbers if number % 2 == 0]

print(even_numbers)
```

Output:

```text
[2, 4, 6]
```

---

# 37. Can List Comprehension Have an `if-else`?

Yes.

The syntax is different from filtering.

### Example

```python
numbers = [1, 2, 3, 4, 5]

result = [
    "Even" if number % 2 == 0 else "Odd"
    for number in numbers
]

print(result)
```

Output:

```text
['Odd', 'Even', 'Odd', 'Even', 'Odd']
```

### Important

Filtering:

```python
[number for number in numbers if condition]
```

Conditional expression:

```python
[value_if_true if condition else value_if_false for number in numbers]
```

---

# 38. What Is the Difference Between a List Comprehension and a Normal Loop?

Both can produce the same result.

### Loop

Usually more explicit and useful for complex logic.

### List Comprehension

Usually more concise for straightforward transformations and filtering.

### Interview Answer

> I prefer list comprehensions when the transformation is simple and readable. For complex logic or multiple side effects, a normal loop is often clearer.

---

# 39. What Is List Unpacking?

List unpacking assigns elements of a list to multiple variables.

### Example

```python
skills = ["Python", "SQL", "PySpark"]

a, b, c = skills

print(a)
print(b)
print(c)
```

Output:

```text
Python
SQL
PySpark
```

The number of variables normally needs to match the number of values.

---

# 40. What Is Extended Unpacking?

The `*` operator can collect multiple remaining values.

### Example

```python
numbers = [1, 2, 3, 4, 5]

first, *middle, last = numbers

print(first)
print(middle)
print(last)
```

Output:

```text
1
[2, 3, 4]
5
```

---

# 41. Can a List Contain Duplicate Values?

Yes.

```python
numbers = [1, 2, 2, 3, 3, 3]

print(numbers)
```

Output:

```text
[1, 2, 2, 3, 3, 3]
```

Lists preserve duplicates.

---

# 42. Can a List Contain Different Data Types?

Yes.

```python
data = [
    10,
    "Python",
    3.14,
    True,
    [1, 2]
]

print(data)
```

Output:

```text
[10, 'Python', 3.14, True, [1, 2]]
```

Python lists are heterogeneous.

---

# 43. What Is the Difference Between a List and a Tuple?

| List | Tuple |
|---|---|
| Mutable | Immutable |
| `[]` | `()` |
| Can be modified | Cannot be modified |
| Generally used for changing collections | Useful for fixed collections |
| Usually slightly more memory overhead | Often more memory-efficient |

### Example

```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)

my_list[0] = 100

print(my_list)
```

Output:

```text
[100, 2, 3]
```

Trying the same assignment on a tuple raises `TypeError`.

---

# 44. When Would You Use a List Instead of a Tuple?

Use a list when the collection needs to change.

### Example

```python
skills = ["Python", "SQL"]

skills.append("PySpark")
```

If the values should remain fixed:

```python
coordinates = (10, 20)
```

A tuple may be more appropriate.

### Interview Answer

> I use a list when I need a mutable collection and a tuple when the data should be immutable or represent a fixed grouping of values.

---

# 45. How Does Python List Sorting Work?

Python's list sorting uses **Timsort**, a hybrid sorting algorithm derived from merge sort and insertion sort.

### Example

```python
numbers = [5, 1, 4, 2, 3]

numbers.sort()

print(numbers)
```

Output:

```text
[1, 2, 3, 4, 5]
```

### Complexity

Python's sorting algorithm has worst-case time complexity of:

```text
O(n log n)
```

It can perform particularly well on partially ordered data.

---

# 46. How Do You Sort a List in Descending Order?

Use `reverse=True`.

```python
numbers = [5, 1, 4, 2, 3]

numbers.sort(reverse=True)

print(numbers)
```

Output:

```text
[5, 4, 3, 2, 1]
```

---

# 47. How Do You Sort a List Based on a Custom Key?

Use the `key` parameter.

### Example

```python
names = ["Harsha", "Raj", "Anita", "Christopher"]

names.sort(key=len)

print(names)
```

Output:

```text
['Raj', 'Anita', 'Harsha', 'Christopher']
```

The strings are sorted based on their length.

---

# 48. How Do You Sort a List of Dictionaries?

Use a key function.

### Example

```python
employees = [
    {"name": "Harsha", "salary": 60000},
    {"name": "Rahul", "salary": 50000},
    {"name": "Anita", "salary": 70000}
]

employees.sort(key=lambda employee: employee["salary"])

print(employees)
```

Output:

```text
[
    {'name': 'Rahul', 'salary': 50000},
    {'name': 'Harsha', 'salary': 60000},
    {'name': 'Anita', 'salary': 70000}
]
```

This pattern is useful when working with structured Python data.

---

# 49. Is Python List Sorting Stable?

Yes.

Python's sorting is stable.

If two elements have the same sorting key, their original relative order is preserved.

### Example

```python
students = [
    ("Harsha", 80),
    ("Rahul", 70),
    ("Anita", 80)
]

students.sort(key=lambda student: student[1])

print(students)
```

Output:

```text
[('Rahul', 70), ('Harsha', 80), ('Anita', 80)]
```

`Harsha` remains before `Anita` because they had equal keys and that was their original order.

---

# 50. What Is the Difference Between `copy()` and `deepcopy()`?

`copy()` creates a shallow copy.

`deepcopy()` recursively copies nested objects.

### Example

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

shallow[0].append(100)

print(original)
print(deep)
```

Output:

```text
[[1, 2, 100], [3, 4]]
[[1, 2], [3, 4]]
```

---

# 51. What Is the Difference Between `a = b` and `a = b.copy()`?

```python
a = [1, 2, 3]
b = a
```

Both refer to the same list.

But:

```python
a = [1, 2, 3]
b = a.copy()
```

creates a separate outer list.

### Verify With `is`

```python
a = [1, 2, 3]

b = a
c = a.copy()

print(a is b)
print(a is c)
```

Output:

```text
True
False
```

---

# 52. How Does List Membership Checking Work?

The `in` operator checks whether an element exists.

```python
numbers = [10, 20, 30, 40]

print(30 in numbers)
```

Output:

```text
True
```

For a normal list, membership checking generally requires scanning elements and has average/worst-case time complexity of `O(n)`.

If frequent membership checks are required, a set may be more appropriate because set membership is generally `O(1)` average case.

---

# 53. What Is the Time Complexity of Common List Operations?

A useful interview-level overview:

| Operation | Typical Complexity |
|---|---:|
| Access by index | O(1) |
| Assignment by index | O(1) |
| Append at end | O(1) amortized |
| Pop from end | O(1) |
| Insert at beginning | O(n) |
| Delete from beginning | O(n) |
| Search with `in` | O(n) |
| `remove()` | O(n) |
| `index()` | O(n) |
| `count()` | O(n) |
| Sort | O(n log n) |
| Reverse in place | O(n) |

### Important

`append()` is commonly described as **O(1) amortized**, not guaranteed O(1) for every individual operation, because the underlying dynamic array may occasionally need to resize.

---

# 54. Why Is Inserting at the Beginning of a List O(n)?

Python lists are implemented as dynamic arrays.

When inserting at the beginning, existing elements generally need to be shifted.

```python
numbers = [1, 2, 3, 4]

numbers.insert(0, 100)

print(numbers)
```

Conceptually:

```text
Before:
[1, 2, 3, 4]

After:
[100, 1, 2, 3, 4]
```

Multiple elements have to move, so the operation is generally `O(n)`.

If frequent insertion/removal from both ends is required, `collections.deque` is usually more appropriate.

---

# 55. Why Is `append()` Efficient?

Python lists are dynamic arrays.

When there is available capacity, an element can be added at the end without shifting existing elements.

Occasionally Python must allocate a larger internal array and copy references, but this is spread across many operations.

Therefore:

```text
append() → O(1) amortized
```

---

# 56. What Is List Capacity?

A Python list internally maintains storage for references to its elements.

It may allocate some extra capacity so that repeated appends do not require resizing on every operation.

This is one reason append is amortized O(1).

### Important Interview Point

Do not claim:

> Python lists are linked lists.

They are dynamic-array-like structures.

---

# 57. What Is the Difference Between a List and `deque`?

A `deque` from `collections` is designed for efficient insertion and removal from both ends.

### List

```python
numbers.append(10)
numbers.pop()
```

Efficient at the end.

### Deque

```python
from collections import deque

numbers = deque([1, 2, 3])

numbers.appendleft(0)
numbers.append(4)

print(numbers)
```

Output:

```text
deque([0, 1, 2, 3, 4])
```

### Interview Answer

> A list is generally better for random access and operations at the end, while `deque` is designed for efficient operations at both ends.

---

# 58. What Happens When You Multiply a List?

List multiplication repeats references to its elements.

### Example

```python
numbers = [1, 2, 3]

print(numbers * 2)
```

Output:

```text
[1, 2, 3, 1, 2, 3]
```

With immutable elements such as integers, this usually behaves as expected.

But nested mutable objects create an important trap.

---

# 59. What Is the Famous Nested List Multiplication Trap?

Consider:

```python
matrix = [[0] * 3] * 3

matrix[0][0] = 1

print(matrix)
```

Output:

```text
[[1, 0, 0], [1, 0, 0], [1, 0, 0]]
```

Why?

Because the multiplication duplicates references to the same inner list.

### Correct Approach

```python
matrix = [[0] * 3 for _ in range(3)]

matrix[0][0] = 1

print(matrix)
```

Output:

```text
[[1, 0, 0], [0, 0, 0], [0, 0, 0]]
```

### Interview Answer

> List multiplication repeats references to the same nested mutable object. A list comprehension creates a separate inner list for each row.

---

# 60. What Is the Difference Between `list.copy()` and Slicing?

Both create a shallow copy of the outer list.

```python
a = [1, 2, 3]

b = a.copy()
c = a[:]

print(b)
print(c)
```

Both produce:

```text
[1, 2, 3]
```

For nested objects, both are shallow copies.

---

# 61. Can a List Be a Dictionary Key?

Normally, no.

Lists are mutable and therefore unhashable.

```python
data = {
    [1, 2]: "value"
}
```

This raises:

```text
TypeError: unhashable type: 'list'
```

A tuple containing hashable elements can be used as a dictionary key.

```python
data = {
    (1, 2): "value"
}

print(data)
```

---

# 62. Can a List Contain Another List as an Element?

Yes.

```python
data = [1, 2, [3, 4]]

print(data)
print(data[2])
print(data[2][0])
```

Output:

```text
[1, 2, [3, 4]]
[3, 4]
3
```

---

# 63. How Do You Flatten a Simple Nested List?

For a simple two-level list:

```python
data = [[1, 2], [3, 4], [5, 6]]

result = [item for sublist in data for item in sublist]

print(result)
```

Output:

```text
[1, 2, 3, 4, 5, 6]
```

### Important

This approach is suitable for a known simple nesting level. Arbitrarily nested structures require a recursive or stack-based approach.

---

# 64. How Do You Remove Duplicates From a List?

If order does not matter:

```python
numbers = [1, 2, 2, 3, 3, 4]

result = list(set(numbers))

print(result)
```

However, this does not guarantee preserving the original order.

If order should be preserved:

```python
numbers = [1, 2, 2, 3, 3, 4]

result = list(dict.fromkeys(numbers))

print(result)
```

Output:

```text
[1, 2, 3, 4]
```

### Interview Answer

> If order does not matter, a set can remove duplicates. If I need to preserve insertion order, `dict.fromkeys()` is a simple option for hashable elements.

---

# 65. How Do You Find the Maximum and Minimum Values in a List?

Use `max()` and `min()`.

```python
numbers = [10, 5, 30, 20]

print(max(numbers))
print(min(numbers))
```

Output:

```text
30
5
```

---

# 66. How Do You Calculate the Sum of a List?

Use `sum()`.

```python
numbers = [10, 20, 30]

print(sum(numbers))
```

Output:

```text
60
```

---

# 67. What Happens If `sum()` Is Used With Strings?

It is not the correct tool for joining strings.

```python
words = ["Python", "SQL"]

print(sum(words))
```

This raises a `TypeError`.

Use:

```python
print(" ".join(words))
```

Output:

```text
Python SQL
```

---

# 68. How Do You Iterate Over a List?

The standard approach is a `for` loop.

```python
skills = ["Python", "SQL", "PySpark"]

for skill in skills:
    print(skill)
```

Output:

```text
Python
SQL
PySpark
```

---

# 69. How Do You Iterate With Both Index and Value?

Use `enumerate()`.

```python
skills = ["Python", "SQL", "PySpark"]

for index, skill in enumerate(skills):
    print(index, skill)
```

Output:

```text
0 Python
1 SQL
2 PySpark
```

This is usually cleaner than manually maintaining an index.

---

# 70. How Do You Iterate Over Two Lists Together?

Use `zip()`.

```python
names = ["Harsha", "Rahul", "Anita"]
roles = ["Data Engineer", "Developer", "Analyst"]

for name, role in zip(names, roles):
    print(name, role)
```

Output:

```text
Harsha Data Engineer
Rahul Developer
Anita Analyst
```

---

# 71. What Happens If Two Lists Have Different Lengths With `zip()`?

By default, `zip()` stops when the shortest iterable is exhausted.

```python
a = [1, 2, 3]
b = ["A", "B"]

print(list(zip(a, b)))
```

Output:

```text
[(1, 'A'), (2, 'B')]
```

---

# 72. How Do You Convert a List to a String?

If all elements are strings, use `join()`.

```python
words = ["Python", "is", "powerful"]

sentence = " ".join(words)

print(sentence)
```

Output:

```text
Python is powerful
```

For arbitrary objects, convert elements explicitly if needed:

```python
numbers = [1, 2, 3]

result = ",".join(map(str, numbers))

print(result)
```

Output:

```text
1,2,3
```

---

# 73. What Is List Comprehension With Nested Loops?

List comprehensions can contain nested iteration.

### Example

```python
matrix = [
    [1, 2],
    [3, 4]
]

result = [value for row in matrix for value in row]

print(result)
```

Output:

```text
[1, 2, 3, 4]
```

The order corresponds to:

```python
for row in matrix:
    for value in row:
        ...
```

---

# 74. What Are Common List Interview Traps?

## Trap 1 — `append()` vs `extend()`

```python
a = [1, 2]

a.append([3, 4])

print(a)
```

Output:

```text
[1, 2, [3, 4]]
```

Not:

```text
[1, 2, 3, 4]
```

---

## Trap 2 — `sort()` Returns `None`

```python
a = [3, 1, 2]

print(a.sort())
```

Output:

```text
None
```

The list itself is sorted.

---

## Trap 3 — `reverse()` Returns `None`

```python
a = [1, 2, 3]

print(a.reverse())
```

Output:

```text
None
```

---

## Trap 4 — Assignment Is Not Copying

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

---

## Trap 5 — Nested List Multiplication

```python
matrix = [[0] * 2] * 2

matrix[0][0] = 1

print(matrix)
```

Output:

```text
[[1, 0], [1, 0]]
```

---

# 75. Important List Output Questions

## Question 1

```python
numbers = [1, 2, 3]

numbers.append([4, 5])

print(numbers)
```

### Answer

```text
[1, 2, 3, [4, 5]]
```

---

## Question 2

```python
numbers = [1, 2, 3]

numbers.extend([4, 5])

print(numbers)
```

### Answer

```text
[1, 2, 3, 4, 5]
```

---

## Question 3

```python
numbers = [1, 2, 3]

result = numbers.reverse()

print(result)
print(numbers)
```

### Answer

```text
None
[3, 2, 1]
```

---

## Question 4

```python
numbers = [3, 1, 2]

result = sorted(numbers)

print(numbers)
print(result)
```

### Answer

```text
[3, 1, 2]
[1, 2, 3]
```

---

## Question 5

```python
numbers = [3, 1, 2]

result = numbers.sort()

print(numbers)
print(result)
```

### Answer

```text
[1, 2, 3]
None
```

---

## Question 6

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
print(b)
```

### Answer

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
```

---

## Question 7

```python
a = [1, 2, 3]
b = a.copy()

b.append(4)

print(a)
print(b)
```

### Answer

```text
[1, 2, 3]
[1, 2, 3, 4]
```

---

## Question 8

```python
matrix = [[0] * 2] * 2

matrix[0][0] = 1

print(matrix)
```

### Answer

```text
[[1, 0], [1, 0]]
```

---

## Question 9

```python
matrix = [[0] * 2 for _ in range(2)]

matrix[0][0] = 1

print(matrix)
```

### Answer

```text
[[1, 0], [0, 0]]
```

---

## Question 10

```python
numbers = [1, 2, 3, 4, 5]

print(numbers[1:4])
print(numbers[::-1])
```

### Answer

```text
[2, 3, 4]
[5, 4, 3, 2, 1]
```

---

# 76. Important List Interview Questions

1. What is a list in Python?
2. What are the properties of a Python list?
3. Why are lists mutable?
4. How does list indexing work?
5. What is negative indexing?
6. What is list slicing?
7. How do you reverse a list?
8. What is the difference between `reverse()` and `[::-1]`?
9. What is the difference between `sort()` and `sorted()`?
10. What does `sort()` return?
11. What does `reverse()` return?
12. What is the difference between `append()` and `extend()`?
13. What happens when `extend()` receives a string?
14. What does `insert()` do?
15. What is the difference between `remove()` and `pop()`?
16. What is the difference between `remove()`, `pop()`, and `del`?
17. What happens when `remove()` cannot find an element?
18. What happens when `pop()` receives an invalid index?
19. How do you clear a list?
20. What is list aliasing?
21. What is the difference between assignment and copying?
22. How do you make a shallow copy?
23. What is a deep copy?
24. What is the difference between shallow and deep copy?
25. What is a nested list?
26. What is list comprehension?
27. How do you add conditions to list comprehensions?
28. Can list comprehensions use `if-else`?
29. When should you avoid overly complex list comprehensions?
30. What is list unpacking?
31. What is extended unpacking?
32. Can lists contain duplicate values?
33. Can lists contain different data types?
34. What is the difference between a list and tuple?
35. Can a list be a dictionary key?
36. Why are lists unhashable?
37. How does Python sort lists?
38. What is Timsort?
39. What is the time complexity of sorting?
40. What does the `key` parameter do?
41. Is Python sorting stable?
42. What is the time complexity of list indexing?
43. What is the complexity of `append()`?
44. What is the complexity of inserting at the beginning?
45. What is the complexity of searching a list?
46. Why is `append()` O(1) amortized?
47. What is the difference between a list and `deque`?
48. What happens when you multiply a list?
49. Why is `[[0] * 3] * 3` dangerous for nested lists?
50. How do you remove duplicates from a list?
51. How do you preserve order while removing duplicates?
52. How do you flatten a nested list?
53. How do you find maximum and minimum values?
54. How do you calculate the sum?
55. How do you iterate over a list?
56. What is `enumerate()`?
57. What is `zip()`?
58. What happens when `zip()` receives lists of different lengths?
59. How do you convert a list into a string?
60. What are the most common list interview traps?

---

# 77. Strong Interview Answer Pattern

When an interviewer asks a list question, answer using:

**Definition → Behavior → Example → Practical use → Follow-up**

### Example: "What is the difference between `append()` and `extend()`?"

A strong answer:

> "`append()` adds its argument as a single element to the end of a list, while `extend()` iterates over the supplied iterable and adds its elements individually. For example, `append([3,4])` produces `[1,2,[3,4]]`, whereas `extend([3,4])` produces `[1,2,3,4]`. This distinction is important when combining collections or processing records."

---

# 78. Quick Revision

## List Properties

```text
Ordered
Mutable
Indexed
Allows duplicates
Allows heterogeneous elements
Dynamically sized
```

## Important Methods

```text
append()
extend()
insert()
remove()
pop()
clear()
index()
count()
sort()
reverse()
copy()
```

## Important Built-ins

```text
len()
sorted()
min()
max()
sum()
enumerate()
zip()
```

## Important Concepts

```text
List slicing
List comprehension
List unpacking
Aliasing
Shallow copy
Deep copy
Nested lists
List multiplication
List sorting
List complexity
```

## Most Important Interview Questions

```text
1. append() vs extend()
2. remove() vs pop() vs del
3. sort() vs sorted()
4. reverse() vs [::-1]
5. Assignment vs copy
6. Shallow copy vs deep copy
7. List comprehension
8. List vs tuple
9. List vs deque
10. Nested list multiplication trap
11. List mutability
12. List time complexities
13. List as dictionary key
14. Duplicate removal
15. Output-based list questions
```

## Final Placement Focus

For placement interviews, understand these deeply:

1. **Mutability**
2. **Indexing and slicing**
3. **`append()` vs `extend()`**
4. **`remove()` vs `pop()` vs `del`**
5. **`sort()` vs `sorted()`**
6. **`reverse()` vs `[::-1]`**
7. **Assignment vs shallow copy**
8. **Shallow copy vs deep copy**
9. **List comprehensions**
10. **Nested lists**
11. **List multiplication trap**
12. **List time complexity**
13. **List vs tuple**
14. **List vs deque**
15. **Common output-based questions**

The objective is not to memorize every list method. Focus on understanding **what each operation does, whether it modifies the original list, what it returns, its complexity, and the common traps an interviewer can use as follow-up questions**.