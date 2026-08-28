# Python Dictionaries — Interview Preparation

## 1. What Is a Dictionary in Python?

A **dictionary** is a mutable collection that stores data in **key-value pairs**.

```python
student = {
    "name": "Harsha",
    "age": 21,
    "course": "Data Engineering"
}

print(student)
```

Here:

```text
"name"  -> key
"Harsha" -> value

"age"   -> key
21      -> value
```

### Important Properties

A Python dictionary is:

- Mutable
- A mapping of keys to values
- Key-based rather than index-based
- Keys must be hashable
- Keys are unique
- Values can be duplicated
- Preserves insertion order in modern Python
- Provides average O(1) lookup by key

### Interview Answer

> A dictionary is a mutable mapping that stores data as key-value pairs. Keys must be hashable and unique, while values can be of any type. Dictionaries are useful when we need to efficiently access a value using a meaningful key.

---

# 2. Why Do We Use Dictionaries?

Dictionaries are useful when data has a **relationship between a key and a value**.

Instead of:

```python
student = ["Harsha", 21, "Data Engineering"]
```

we can write:

```python
student = {
    "name": "Harsha",
    "age": 21,
    "field": "Data Engineering"
}
```

Now the data is easier to understand and access:

```python
print(student["name"])
print(student["field"])
```

Output:

```text
Harsha
Data Engineering
```

### Real-World Example

An employee record can be represented as:

```python
employee = {
    "id": 101,
    "name": "Harsha",
    "department": "Data Engineering",
    "experience": 1
}
```

The keys describe what each value represents.

---

# 3. How Do You Create a Dictionary?

Using curly braces:

```python
student = {
    "name": "Harsha",
    "age": 21
}
```

You can also use `dict()`:

```python
student = dict(name="Harsha", age=21)

print(student)
```

---

# 4. How Do You Create an Empty Dictionary?

Use:

```python
data = {}
```

or:

```python
data = dict()
```

Both create an empty dictionary.

### Important Interview Trap

```python
data = {}
```

creates a dictionary, not a set.

To create an empty set:

```python
data = set()
```

---

# 5. Are Dictionary Keys Unique?

Yes.

If the same key is assigned multiple times, the latest value replaces the previous value.

```python
student = {
    "name": "Harsha",
    "name": "Rahul"
}

print(student)
```

Result:

```text
{'name': 'Rahul'}
```

### Interview Answer

> Dictionary keys must be unique. If the same key is assigned again, its previous value is overwritten.

---

# 6. Can Dictionary Values Be Duplicated?

Yes.

```python
data = {
    "a": 10,
    "b": 10,
    "c": 20
}

print(data)
```

The value `10` can appear multiple times.

### Important

```text
Keys   -> Unique
Values -> Can repeat
```

---

# 7. Are Dictionaries Ordered?

Modern Python dictionaries preserve **insertion order**.

```python
data = {}

data["a"] = 10
data["b"] = 20
data["c"] = 30

print(data)
```

The insertion order is preserved during iteration.

### Important Interview Point

Do not confuse:

> insertion order

with:

> sorting

A dictionary preserves insertion order, but it is not automatically sorted by key or value.

---

# 8. Can You Access Dictionary Elements Using an Index?

No.

A dictionary is accessed using keys.

```python
student = {
    "name": "Harsha",
    "age": 21
}

print(student["name"])
```

This is correct.

This is not:

```python
print(student[0])
```

unless `0` itself is a key.

### Interview Answer

> Dictionaries are key-based mappings, so we access values using keys rather than positional indexes.

---

# 9. How Do You Access a Dictionary Value?

Use the key:

```python
student = {
    "name": "Harsha",
    "age": 21
}

print(student["name"])
```

Output:

```text
Harsha
```

---

# 10. What Happens If You Access a Missing Key Using `[]`?

It raises a `KeyError`.

```python
student = {
    "name": "Harsha"
}

print(student["age"])
```

This raises:

```text
KeyError: 'age'
```

---

# 11. What Is the Difference Between `[]` and `get()`?

This is a very important interview question.

### Using `[]`

```python
student = {
    "name": "Harsha"
}

print(student["age"])
```

Raises:

```text
KeyError
```

### Using `get()`

```python
student = {
    "name": "Harsha"
}

print(student.get("age"))
```

Returns:

```text
None
```

You can also provide a default:

```python
print(student.get("age", 0))
```

Output:

```text
0
```

### Interview Answer

> `dict[key]` raises `KeyError` when the key does not exist, while `get()` returns `None` by default or a specified default value.

---

# 12. How Do You Add a New Key-Value Pair?

Assign a value to a new key.

```python
student = {
    "name": "Harsha"
}

student["age"] = 21

print(student)
```

Result:

```text
{'name': 'Harsha', 'age': 21}
```

---

# 13. How Do You Update an Existing Value?

Assign a new value to the existing key.

```python
student = {
    "name": "Harsha",
    "age": 21
}

student["age"] = 22

print(student)
```

Output:

```text
{'name': 'Harsha', 'age': 22}
```

---

# 14. How Do You Add Multiple Key-Value Pairs?

Use `update()`.

```python
student = {
    "name": "Harsha"
}

student.update({
    "age": 21,
    "course": "Data Engineering"
})

print(student)
```

---

# 15. What Does `update()` Do?

`update()` adds key-value pairs to the dictionary.

If a key already exists, its value is replaced.

```python
data = {
    "a": 10,
    "b": 20
}

data.update({
    "b": 200,
    "c": 30
})

print(data)
```

Result:

```text
{'a': 10, 'b': 200, 'c': 30}
```

---

# 16. How Do You Delete a Dictionary Element?

Use `del`.

```python
student = {
    "name": "Harsha",
    "age": 21
}

del student["age"]

print(student)
```

Result:

```text
{'name': 'Harsha'}
```

---

# 17. What Happens If `del` Is Used With a Missing Key?

It raises:

```text
KeyError
```

Example:

```python
student = {
    "name": "Harsha"
}

del student["age"]
```

---

# 18. What Does `pop()` Do in a Dictionary?

`pop()` removes a specified key and returns its value.

```python
student = {
    "name": "Harsha",
    "age": 21
}

age = student.pop("age")

print(age)
print(student)
```

Output:

```text
21
{'name': 'Harsha'}
```

---

# 19. What Happens If `pop()` Is Used With a Missing Key?

Normally it raises `KeyError`.

```python
student = {
    "name": "Harsha"
}

student.pop("age")
```

You can provide a default value:

```python
print(student.pop("age", None))
```

Output:

```text
None
```

---

# 20. What Does `popitem()` Do?

`popitem()` removes and returns the **last inserted key-value pair**.

```python
data = {
    "a": 10,
    "b": 20,
    "c": 30
}

item = data.popitem()

print(item)
print(data)
```

Output:

```text
('c', 30)
{'a': 10, 'b': 20}
```

### Interview Answer

> `popitem()` removes and returns the last inserted key-value pair in modern Python dictionaries.

---

# 21. What Does `clear()` Do?

It removes all key-value pairs.

```python
data = {
    "a": 10,
    "b": 20
}

data.clear()

print(data)
```

Output:

```text
{}
```

---

# 22. What Does `del data` Do?

It removes the dictionary variable itself.

```python
data = {
    "a": 10
}

del data
```

After this, `data` no longer exists.

This is different from:

```python
data.clear()
```

which leaves an empty dictionary.

---

# 23. How Do You Get All Dictionary Keys?

Use `keys()`.

```python
student = {
    "name": "Harsha",
    "age": 21,
    "course": "Data Engineering"
}

print(student.keys())
```

You can iterate over them:

```python
for key in student.keys():
    print(key)
```

---

# 24. How Do You Get All Dictionary Values?

Use `values()`.

```python
student = {
    "name": "Harsha",
    "age": 21
}

for value in student.values():
    print(value)
```

---

# 25. How Do You Get Both Keys and Values?

Use `items()`.

```python
student = {
    "name": "Harsha",
    "age": 21
}

for key, value in student.items():
    print(key, value)
```

Output:

```text
name Harsha
age 21
```

### Interview Answer

> `keys()` gives the keys, `values()` gives the values, and `items()` gives key-value pairs.

---

# 26. What Are `keys()`, `values()`, and `items()` Returning?

They return dynamic **view objects**.

```python
data = {
    "a": 10,
    "b": 20
}

print(type(data.keys()))
print(type(data.values()))
print(type(data.items()))
```

They are not ordinary lists.

If a list is required:

```python
keys = list(data.keys())
values = list(data.values())
items = list(data.items())
```

---

# 27. What Is Dictionary Membership Testing?

The `in` operator checks dictionary **keys** by default.

```python
student = {
    "name": "Harsha",
    "age": 21
}

print("name" in student)
print("Harsha" in student)
```

Output:

```text
True
False
```

### Important

This:

```python
"value" in dictionary
```

checks keys, not values.

To check values:

```python
print("Harsha" in student.values())
```

---

# 28. What Is the Average Time Complexity of Dictionary Lookup?

Dictionary lookup by key is:

```text
Average: O(1)
Worst case: O(n)
```

because dictionaries are hash-based.

```python
student = {
    "name": "Harsha",
    "age": 21
}

print(student["name"])
```

### Interview Answer

> Dictionary key lookup is O(1) on average because Python uses a hash-table-based implementation.

---

# 29. Why Are Dictionary Keys Required to Be Hashable?

Dictionaries use keys to locate values through hashing.

Therefore, keys must have a stable hash value.

Common hashable keys:

```text
int
float
str
bool
tuple containing hashable elements
```

Common unhashable objects:

```text
list
dict
set
```

---

# 30. Can a List Be a Dictionary Key?

No.

```python
data = {
    [1, 2]: "value"
}
```

This raises:

```text
TypeError: unhashable type: 'list'
```

---

# 31. Can a Tuple Be a Dictionary Key?

Yes, provided all elements inside the tuple are hashable.

```python
data = {
    (1, 2): "point"
}

print(data[(1, 2)])
```

Output:

```text
point
```

But:

```python
data = {
    ([1, 2], 3): "value"
}
```

is invalid because the tuple contains a list.

---

# 32. Can a Dictionary Be a Dictionary Key?

No.

```python
data = {
    {"a": 1}: "value"
}
```

This raises:

```text
TypeError: unhashable type: 'dict'
```

Dictionary keys must be hashable.

---

# 33. Can a Set Be a Dictionary Key?

No.

```python
data = {
    {1, 2}: "value"
}
```

This raises:

```text
TypeError: unhashable type: 'set'
```

A `frozenset` can be used:

```python
data = {
    frozenset([1, 2]): "value"
}
```

---

# 34. Can Dictionary Values Be Mutable Objects?

Yes.

Values can be lists, dictionaries, sets, objects, etc.

```python
student = {
    "name": "Harsha",
    "skills": ["Python", "SQL", "PySpark"]
}

print(student["skills"])
```

This is completely valid.

The hashability restriction applies to **keys**, not values.

---

# 35. Can Dictionary Values Be Dictionaries?

Yes.

This is common when representing nested data.

```python
employee = {
    "name": "Harsha",
    "address": {
        "city": "Hyderabad",
        "country": "India"
    }
}

print(employee["address"]["city"])
```

Output:

```text
Hyderabad
```

---

# 36. What Is a Nested Dictionary?

A dictionary containing another dictionary as a value is called a nested dictionary.

```python
employees = {
    101: {
        "name": "Harsha",
        "department": "Data Engineering"
    },
    102: {
        "name": "Rahul",
        "department": "Development"
    }
}
```

Access:

```python
print(employees[101]["name"])
```

Output:

```text
Harsha
```

---

# 37. How Do You Iterate Through a Dictionary?

Using keys:

```python
data = {
    "a": 10,
    "b": 20
}

for key in data:
    print(key)
```

Using key-value pairs:

```python
for key, value in data.items():
    print(key, value)
```

### Interview Tip

For most situations where you need both key and value, use:

```python
for key, value in data.items():
```

---

# 38. How Do You Sort a Dictionary?

Dictionaries themselves preserve insertion order, but you can create an ordered result based on keys or values.

### Sort by Keys

```python
data = {
    "c": 30,
    "a": 10,
    "b": 20
}

sorted_data = dict(sorted(data.items()))

print(sorted_data)
```

Result:

```text
{'a': 10, 'b': 20, 'c': 30}
```

### Sort by Values

```python
data = {
    "a": 30,
    "b": 10,
    "c": 20
}

sorted_data = dict(
    sorted(data.items(), key=lambda item: item[1])
)

print(sorted_data)
```

Result:

```text
{'b': 10, 'c': 20, 'a': 30}
```

### Interview Answer

> A dictionary maintains insertion order, but if I want the entries sorted by key or value, I can use `sorted()` on `items()` and create a new dictionary from the result.

---

# 39. What Is Dictionary Comprehension?

Dictionary comprehension is a concise way to create dictionaries.

### Example

```python
numbers = [1, 2, 3, 4]

squares = {
    number: number * number
    for number in numbers
}

print(squares)
```

Output:

```text
{
    1: 1,
    2: 4,
    3: 9,
    4: 16
}
```

### With Condition

```python
numbers = range(1, 6)

even_squares = {
    number: number * number
    for number in numbers
    if number % 2 == 0
}

print(even_squares)
```

Output:

```text
{
    2: 4,
    4: 16
}
```

---

# 40. What Happens If Dictionary Comprehension Generates Duplicate Keys?

The later value overwrites the earlier value.

```python
data = {
    x % 2: x
    for x in range(5)
}

print(data)
```

The possible keys are only:

```text
0
1
```

because dictionary keys must be unique.

---

# 41. How Do You Merge Two Dictionaries?

Using `update()`:

```python
a = {
    "name": "Harsha",
    "age": 21
}

b = {
    "course": "Data Engineering"
}

a.update(b)

print(a)
```

Or, in modern Python, using the merge operator:

```python
a = {
    "name": "Harsha"
}

b = {
    "course": "Data Engineering"
}

result = a | b

print(result)
```

`a | b` creates a new dictionary.

---

# 42. What Is the Difference Between `update()` and `|`?

### `update()`

Modifies the existing dictionary:

```python
a.update(b)
```

### `|`

Creates a new dictionary:

```python
c = a | b
```

The original dictionaries remain unchanged by the merge expression.

---

# 43. What Does the Dictionary Merge Assignment Operator `|=` Do?

It updates the existing dictionary.

```python
a = {
    "name": "Harsha"
}

b = {
    "age": 21
}

a |= b

print(a)
```

Output:

```text
{'name': 'Harsha', 'age': 21}
```

---

# 44. What Happens When Two Dictionaries Have the Same Key During Merge?

The value from the **right-hand dictionary** wins.

```python
a = {
    "name": "Harsha",
    "age": 21
}

b = {
    "age": 22,
    "city": "Hyderabad"
}

result = a | b

print(result)
```

Result:

```text
{
    "name": "Harsha",
    "age": 22,
    "city": "Hyderabad"
}
```

---

# 45. What Is `setdefault()`?

`setdefault()` returns the value for a key if it exists.

If the key does not exist, it inserts the key with the supplied default value and returns that value.

### Example

```python
data = {
    "name": "Harsha"
}

value = data.setdefault("age", 21)

print(value)
print(data)
```

Output:

```text
21
{'name': 'Harsha', 'age': 21}
```

If the key already exists:

```python
data = {
    "age": 21
}

value = data.setdefault("age", 30)

print(value)
print(data)
```

Output:

```text
21
{'age': 21}
```

The existing value is not replaced.

---

# 46. When Is `setdefault()` Useful?

It is useful when building grouped or categorized data.

### Example

```python
students = {}

students.setdefault("Python", []).append("Harsha")
students.setdefault("Python", []).append("Rahul")
students.setdefault("SQL", []).append("Anil")

print(students)
```

Result:

```text
{
    "Python": ["Harsha", "Rahul"],
    "SQL": ["Anil"]
}
```

This avoids manually checking whether each key already exists.

---

# 47. How Do You Count Frequencies Using a Dictionary?

This is one of the most common Python interview problems.

```python
numbers = [1, 2, 2, 3, 3, 3]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

print(frequency)
```

Output:

```text
{
    1: 1,
    2: 2,
    3: 3
}
```

### Interview Explanation

> I use each unique value as a dictionary key and its frequency as the value. `get()` allows me to start the count at zero when the key does not exist.

---

# 48. How Do You Count Character Frequencies?

```python
text = "banana"

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

print(frequency)
```

Result:

```text
{
    'b': 1,
    'a': 3,
    'n': 2
}
```

---

# 49. How Do You Find the First Non-Repeating Character?

A dictionary can be used to count frequencies first.

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

### Interview Explanation

> I first count the frequency of every character using a dictionary. Then I iterate through the original string and return the first character whose frequency is one.

---

# 50. How Do You Invert a Dictionary?

If values are unique:

```python
data = {
    "a": 1,
    "b": 2,
    "c": 3
}

inverted = {
    value: key
    for key, value in data.items()
}

print(inverted)
```

Output:

```text
{
    1: 'a',
    2: 'b',
    3: 'c'
}
```

### Important

If multiple keys have the same value, simply reversing the dictionary causes collisions.

```python
data = {
    "a": 1,
    "b": 1
}
```

You need a different structure if you want to preserve all original keys.

---

# 51. How Do You Find the Key With the Maximum Value?

Use `max()` with `key`.

```python
scores = {
    "Harsha": 85,
    "Rahul": 92,
    "Anil": 88
}

highest = max(scores, key=scores.get)

print(highest)
```

Output:

```text
Rahul
```

### Interview Explanation

> `max()` normally compares keys, but by passing `key=scores.get`, I tell Python to compare the corresponding dictionary values.

---

# 52. How Do You Find the Minimum Value Key?

```python
scores = {
    "Harsha": 85,
    "Rahul": 92,
    "Anil": 88
}

lowest = min(scores, key=scores.get)

print(lowest)
```

Output:

```text
Harsha
```

---

# 53. How Do You Check Whether a Key Exists?

Use:

```python
if "name" in student:
    print("Key exists")
```

Example:

```python
student = {
    "name": "Harsha",
    "age": 21
}

if "age" in student:
    print("Age is available")
```

This is preferable to manually iterating through all keys.

---

# 54. How Do You Check Whether a Value Exists?

Use:

```python
if 21 in student.values():
    print("Value exists")
```

Example:

```python
student = {
    "name": "Harsha",
    "age": 21
}

print(21 in student.values())
```

Output:

```text
True
```

---

# 55. What Is the Difference Between `in dictionary` and `in dictionary.values()`?

```python
"name" in student
```

checks keys.

```python
"Harsha" in student.values()
```

checks values.

### Interview Answer

> By default, membership testing on a dictionary checks keys. To search values, I explicitly use `dictionary.values()`.

---

# 56. What Is `dict.fromkeys()`?

`dict.fromkeys()` creates a dictionary using an iterable of keys.

```python
keys = ["name", "age", "city"]

data = dict.fromkeys(keys)

print(data)
```

Output:

```text
{
    "name": None,
    "age": None,
    "city": None
}
```

You can provide a default value:

```python
data = dict.fromkeys(keys, 0)

print(data)
```

Output:

```text
{
    "name": 0,
    "age": 0,
    "city": 0
}
```

---

# 57. What Is an Important Trap With `dict.fromkeys()` and Mutable Values?

Be careful when using a mutable object as the default value.

```python
data = dict.fromkeys(["a", "b"], [])

data["a"].append(10)

print(data)
```

Both keys reference the same list:

```text
{'a': [10], 'b': [10]}
```

### Better Approach

Use a dictionary comprehension:

```python
data = {
    key: []
    for key in ["a", "b"]
}

data["a"].append(10)

print(data)
```

Result:

```text
{
    "a": [10],
    "b": []
}
```

### Interview Answer

> `dict.fromkeys()` uses the same default object for all keys. Therefore, using a mutable object such as a list as the default value can cause multiple keys to reference the same object.

---

# 58. What Is the Difference Between a Dictionary and a Set?

Both use hashing, but their purposes are different.

### Set

Stores unique values:

```python
skills = {"Python", "SQL", "PySpark"}
```

### Dictionary

Stores key-value mappings:

```python
skills = {
    "primary": "Python",
    "database": "SQL"
}
```

### Interview Answer

> A set stores unique elements, while a dictionary stores mappings from unique keys to values.

---

# 59. What Is the Difference Between a Dictionary and a List?

| Dictionary | List |
|---|---|
| Key-value mapping | Ordered sequence |
| Accessed by key | Accessed by index |
| Keys must be hashable | Elements can be arbitrary objects |
| Average O(1) key lookup | Index lookup O(1) |
| Keys are unique | Duplicate elements allowed |
| Best for relationships/mappings | Best for ordered collections |

---

# 60. What Is the Difference Between Dictionary and Tuple?

| Dictionary | Tuple |
|---|---|
| Key-value mapping | Ordered sequence |
| Mutable | Immutable |
| Access by key | Access by index |
| Keys must be hashable | Tuple itself can be hashable |
| Keys are unique | Duplicate values allowed |

---

# 61. What Is the Difference Between Shallow Copy and Deep Copy of a Dictionary?

A shallow copy creates a new outer dictionary but nested mutable objects may still be shared.

```python
data = {
    "numbers": [1, 2, 3]
}

copy_data = data.copy()

copy_data["numbers"].append(4)

print(data)
print(copy_data)
```

The nested list is shared, so both dictionaries reflect the change.

### Deep Copy

```python
import copy

data = {
    "numbers": [1, 2, 3]
}

copy_data = copy.deepcopy(data)

copy_data["numbers"].append(4)

print(data)
print(copy_data)
```

Now the nested structures are independent.

### Interview Answer

> A shallow copy creates a new outer dictionary but does not recursively copy nested objects. A deep copy recursively copies nested objects, so modifications to nested mutable objects do not affect the original.

---

# 62. How Do You Copy a Dictionary?

Using `copy()`:

```python
data = {
    "a": 10,
    "b": 20
}

new_data = data.copy()
```

You can also use:

```python
new_data = dict(data)
```

For nested mutable structures where complete independence is required:

```python
import copy

new_data = copy.deepcopy(data)
```

---

# 63. What Is the Difference Between Assignment and Copy?

This is an important interview question.

### Assignment

```python
a = {
    "name": "Harsha"
}

b = a

b["name"] = "Rahul"

print(a)
```

Output:

```text
{'name': 'Rahul'}
```

Both variables refer to the same dictionary.

### Shallow Copy

```python
a = {
    "name": "Harsha"
}

b = a.copy()

b["name"] = "Rahul"

print(a)
print(b)
```

Output:

```text
{'name': 'Harsha'}
{'name': 'Rahul'}
```

The outer dictionaries are separate.

---

# 64. Can Dictionaries Contain Lists as Values?

Yes.

```python
data = {
    "skills": ["Python", "SQL", "PySpark"]
}
```

This is extremely common when representing structured data.

---

# 65. Can Dictionaries Be Nested Inside Lists?

Yes.

This is common when representing multiple records.

```python
employees = [
    {
        "id": 101,
        "name": "Harsha"
    },
    {
        "id": 102,
        "name": "Rahul"
    }
]
```

Access:

```python
print(employees[0]["name"])
```

Output:

```text
Harsha
```

This structure is similar to JSON data received from APIs.

---

# 66. Why Are Dictionaries Important in Data Engineering?

Dictionaries are heavily used when working with structured data.

Examples include:

- JSON data
- API responses
- Configuration
- Metadata
- Record representation
- Data transformation
- Frequency counting
- Lookup tables
- Mapping IDs to attributes

### Example — API/JSON-like Data

```python
record = {
    "customer_id": 101,
    "name": "Harsha",
    "orders": [
        {
            "order_id": 5001,
            "amount": 1200
        }
    ]
}
```

You can access:

```python
print(record["customer_id"])
print(record["orders"][0]["amount"])
```

Output:

```text
101
1200
```

### Interview Answer

> Dictionaries are important in data engineering because JSON and many API responses naturally map to Python dictionaries. They are also useful for configuration, record representation, lookup operations, grouping, and transformations.

---

# 67. Dictionary as a Lookup Table

Suppose we have employee IDs and names:

```python
employees = {
    101: "Harsha",
    102: "Rahul",
    103: "Anil"
}

employee_id = 102

print(employees[employee_id])
```

Output:

```text
Rahul
```

This is much more direct than searching through a list of records.

---

# 68. Real-World Data Engineering Example — Mapping IDs

Suppose a dataset contains department IDs:

```python
department_map = {
    10: "Data Engineering",
    20: "Development",
    30: "Testing"
}

records = [
    {"name": "Harsha", "department_id": 10},
    {"name": "Rahul", "department_id": 20}
]

for record in records:
    record["department"] = department_map.get(
        record["department_id"],
        "Unknown"
    )

print(records)
```

This creates a mapping from an ID to a meaningful department name.

### Interview Explanation

> A dictionary is useful as a lookup table. Instead of repeatedly searching for a department ID, I can map the ID directly to the department name using average O(1) dictionary lookup.

---

# 69. Real-World Example — Grouping Data

Suppose we have employees and their departments:

```python
employees = [
    ("Harsha", "Data Engineering"),
    ("Rahul", "Development"),
    ("Anil", "Data Engineering"),
    ("Kiran", "Testing")
]

grouped = {}

for name, department in employees:
    grouped.setdefault(department, []).append(name)

print(grouped)
```

Result:

```text
{
    "Data Engineering": ["Harsha", "Anil"],
    "Development": ["Rahul"],
    "Testing": ["Kiran"]
}
```

### Interview Explanation

> I can use a dictionary where each department is a key and the corresponding value is a list of employees. `setdefault()` makes it easy to initialize the list when the department appears for the first time.

---

# 70. Important Dictionary Output Questions

## Question 1

```python
data = {
    "a": 10,
    "b": 20
}

print(data["a"])
```

### Answer

```text
10
```

---

## Question 2

```python
data = {
    "a": 10
}

print(data.get("b"))
```

### Answer

```text
None
```

---

## Question 3

```python
data = {
    "a": 10
}

print(data["b"])
```

### Answer

```text
KeyError
```

---

## Question 4

```python
data = {
    "a": 10
}

data["a"] = 100

print(data)
```

### Answer

```text
{'a': 100}
```

The existing value is replaced.

---

## Question 5

```python
data = {
    "a": 10,
    "b": 20
}

data["c"] = 30

print(data)
```

### Answer

```text
{'a': 10, 'b': 20, 'c': 30}
```

---

## Question 6

```python
data = {
    "a": 10,
    "b": 20
}

print("a" in data)
print(10 in data)
```

### Answer

```text
True
False
```

Because dictionary membership checks keys.

---

## Question 7

```python
data = {
    "a": 10,
    "b": 20
}

print(10 in data.values())
```

### Answer

```text
True
```

---

## Question 8

```python
data = {
    "a": 10,
    "b": 20
}

value = data.pop("a")

print(value)
print(data)
```

### Answer

```text
10
{'b': 20}
```

---

## Question 9

```python
data = {
    "a": 10,
    "b": 20
}

print(data.popitem())
```

### Answer

It returns the last inserted key-value pair:

```text
('b', 20)
```

---

## Question 10

```python
data = {
    "a": 10,
    "b": 20
}

data.update({
    "b": 100,
    "c": 30
})

print(data)
```

### Answer

```text
{'a': 10, 'b': 100, 'c': 30}
```

---

## Question 11

```python
data = {
    "a": 10,
    "b": 20
}

print(list(data.keys()))
```

### Answer

```text
['a', 'b']
```

---

## Question 12

```python
data = {
    "a": 10,
    "b": 20
}

print(list(data.values()))
```

### Answer

```text
[10, 20]
```

---

## Question 13

```python
data = {
    "a": 10,
    "b": 20
}

print(list(data.items()))
```

### Answer

```text
[('a', 10), ('b', 20)]
```

---

## Question 14

```python
data = {
    "a": 10,
    "a": 20
}

print(data)
```

### Answer

```text
{'a': 20}
```

The later assignment replaces the earlier value.

---

## Question 15

```python
data = dict.fromkeys(["a", "b"], 0)

print(data)
```

### Answer

```text
{'a': 0, 'b': 0}
```

---

# 71. Common Dictionary Interview Traps

## Trap 1 — `{}`

```python
data = {}
```

This creates a dictionary.

Empty set:

```python
data = set()
```

---

## Trap 2 — Duplicate Keys

```python
data = {
    "a": 10,
    "a": 20
}
```

Only the latest value remains.

---

## Trap 3 — Missing Key

```python
data["x"]
```

raises `KeyError`.

But:

```python
data.get("x")
```

returns `None` by default.

---

## Trap 4 — Membership

```python
10 in data
```

checks keys, not values.

Use:

```python
10 in data.values()
```

to check values.

---

## Trap 5 — Mutable Key

```python
data = {
    [1, 2]: "value"
}
```

Invalid because lists are unhashable.

---

## Trap 6 — Tuple Key

```python
data = {
    (1, 2): "value"
}
```

Valid because the tuple contains hashable integers.

---

## Trap 7 — Mutable Tuple Element

```python
data = {
    ([1, 2], 3): "value"
}
```

Invalid because the tuple contains a list.

---

## Trap 8 — `dict.fromkeys()` With Lists

```python
data = dict.fromkeys(["a", "b"], [])
```

Both keys reference the same list.

---

## Trap 9 — Sorting

A dictionary preserves insertion order but is not automatically sorted.

---

## Trap 10 — `popitem()`

Modern Python dictionaries remove the last inserted item with `popitem()`.

---

# 72. Dictionary Time Complexities

For a normal Python dictionary, key-based operations are generally:

| Operation | Average | Worst Case |
|---|---:|---:|
| Lookup by key | O(1) | O(n) |
| Insert/update | O(1) | O(n) |
| Delete by key | O(1) | O(n) |
| Membership by key | O(1) | O(n) |

The O(1) average behavior comes from hashing.

### Interview Answer

> Dictionary operations such as lookup, insertion, update, deletion, and key membership are O(1) on average, although their theoretical worst case can be O(n).

---

# 73. Dictionary Comprehension Interview Example

### Question

Create a dictionary containing numbers and their cubes.

```python
numbers = [1, 2, 3, 4]

cubes = {
    number: number ** 3
    for number in numbers
}

print(cubes)
```

Output:

```text
{
    1: 1,
    2: 8,
    3: 27,
    4: 64
}
```

---

# 74. Frequency Counter Interview Example

### Question

Count the frequency of each word.

```python
words = ["python", "sql", "python", "spark", "sql"]

frequency = {}

for word in words:
    frequency[word] = frequency.get(word, 0) + 1

print(frequency)
```

Output:

```text
{
    "python": 2,
    "sql": 2,
    "spark": 1
}
```

### Interview Explanation

> I use each word as a key and its occurrence count as the value. `get(word, 0)` provides zero when the word is seen for the first time.

---

# 75. Find Duplicate Values Using a Dictionary

```python
numbers = [1, 2, 2, 3, 3, 3, 4]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

duplicates = {
    number
    for number, count in frequency.items()
    if count > 1
}

print(duplicates)
```

Output:

```text
{2, 3}
```

---

# 76. Find the Most Frequent Element

```python
numbers = [1, 2, 2, 3, 3, 3, 4]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

most_frequent = max(
    frequency,
    key=frequency.get
)

print(most_frequent)
```

Output:

```text
3
```

### Interview Explanation

> I first build a frequency dictionary and then use `max()` with `key=frequency.get` to find the key with the highest frequency.

---

# 77. Dictionary and JSON

A Python dictionary is often used to represent JSON-like data.

Example JSON-like structure:

```python
data = {
    "name": "Harsha",
    "skills": [
        "Python",
        "SQL",
        "PySpark"
    ]
}
```

Python provides the `json` module to convert between Python objects and JSON strings.

### Python Dictionary to JSON String

```python
import json

data = {
    "name": "Harsha",
    "age": 21
}

json_data = json.dumps(data)

print(json_data)
```

### JSON String to Python Dictionary

```python
json_string = '{"name": "Harsha", "age": 21}'

data = json.loads(json_string)

print(data)
print(data["name"])
```

### Interview Answer

> Dictionaries are commonly used to represent JSON objects in Python. The `json` module provides `dumps()` to serialize Python objects into JSON and `loads()` to parse JSON strings into Python objects.

---

# 78. Dictionary as Configuration

Dictionaries can store configuration values.

```python
config = {
    "environment": "production",
    "batch_size": 1000,
    "retry_count": 3
}

print(config["batch_size"])
```

This makes configuration easy to access using meaningful keys.

---

# 79. Dictionary as Metadata

In data processing, metadata can be represented using dictionaries.

```python
metadata = {
    "file_name": "customers.csv",
    "rows": 100000,
    "columns": 12,
    "source": "S3"
}
```

You can access:

```python
print(metadata["rows"])
```

Output:

```text
100000
```

---

# 80. Strong Interview Answer — Why Dictionary?

### Question

> Why would you choose a dictionary instead of a list?

### Strong Answer

> "I would choose a dictionary when I need to associate a value with a meaningful key and perform fast lookups. For example, if I have employee IDs and employee names, I can store the ID as the key and the name as the value. Dictionary key lookup is O(1) on average. If I mainly need an ordered sequence and positional access, I would choose a list instead."

---

# 81. Strong Interview Answer — Dictionary in Data Engineering

### Question

> How have you seen dictionaries being useful in data-related work?

### Strong Answer

> "Dictionaries are useful when working with structured and semi-structured data. For example, API and JSON responses can naturally be represented as dictionaries. They are also useful for lookup mappings, configuration, metadata, grouping, and frequency counting. A department ID-to-name mapping is a simple example where dictionary lookup can efficiently transform an ID into a meaningful value."

---

# 82. Strong Interview Answer — Hashing

### Question

> Why are dictionary lookups fast?

### Answer

> "Python dictionaries use hashing internally. A key is hashed and that hash helps determine where the corresponding entry is stored. This allows Python to locate values efficiently, giving average O(1) lookup time."

---

# 83. Strong Interview Answer — Hashable Keys

### Question

> Why can't we use a list as a dictionary key?

### Answer

> "Dictionary keys need to be hashable because the dictionary uses their hash values for lookup. Lists are mutable and therefore unhashable. Immutable objects such as strings and integers can be used as keys, and tuples can be keys when all their elements are hashable."

---

# 84. Strong Interview Answer — `get()` vs `[]`

### Question

> When would you use `get()` instead of square brackets?

### Answer

> "I use square brackets when the key is expected to exist and a missing key should be treated as an error. I use `get()` when the key may be absent and I want to safely return `None` or another default value instead of getting a `KeyError`."

---

# 85. Strong Interview Answer — Dictionary vs Set

### Question

> What is the difference between a dictionary and a set?

### Answer

> "A set stores unique values, whereas a dictionary stores key-value mappings. Both are hash-based and provide average O(1) membership or key lookup. I would use a set for uniqueness and membership testing, and a dictionary when I need to associate each key with a value."

---

# 86. Important Dictionary Interview Questions

1. What is a dictionary in Python?
2. What are the main properties of dictionaries?
3. Why are dictionaries useful?
4. How do you create a dictionary?
5. How do you create an empty dictionary?
6. How is an empty dictionary different from an empty set?
7. Are dictionary keys unique?
8. Can dictionary values be duplicated?
9. Are dictionaries ordered?
10. Does dictionary order mean sorted order?
11. Can dictionaries be accessed using indexes?
12. How do you access a dictionary value?
13. What happens when a key does not exist?
14. What is the difference between `[]` and `get()`?
15. How do you add a key-value pair?
16. How do you update a value?
17. What does `update()` do?
18. How do you delete a dictionary element?
19. What does `pop()` do?
20. What does `popitem()` do?
21. What does `clear()` do?
22. What is the difference between `del` and `clear()`?
23. What does `keys()` return?
24. What does `values()` return?
25. What does `items()` return?
26. What is dictionary membership testing?
27. Does `in` check keys or values?
28. How do you check whether a value exists?
29. What is the average complexity of dictionary lookup?
30. Why are dictionary lookups O(1) on average?
31. What is hashing?
32. What is hashability?
33. Why must dictionary keys be hashable?
34. Can a list be a dictionary key?
35. Can a tuple be a dictionary key?
36. When is a tuple hashable?
37. Can a set be a dictionary key?
38. Can a frozenset be a dictionary key?
39. Can a dictionary be a dictionary key?
40. Can dictionary values be mutable?
41. What is a nested dictionary?
42. How do you iterate over a dictionary?
43. What is dictionary comprehension?
44. How do you sort a dictionary by key?
45. How do you sort a dictionary by value?
46. How do you merge dictionaries?
47. What is the difference between `update()` and `|`?
48. What does `|=` do?
49. What happens when duplicate keys exist during a merge?
50. What is `setdefault()`?
51. When is `setdefault()` useful?
52. How do you count frequencies using a dictionary?
53. How do you count character frequencies?
54. How do you find the first non-repeating character?
55. How do you invert a dictionary?
56. What happens when inverted dictionary values are duplicated?
57. How do you find the key with the maximum value?
58. How do you check whether a key exists?
59. What is `dict.fromkeys()`?
60. What is the mutable-default trap with `dict.fromkeys()`?
61. What is the difference between a dictionary and a set?
62. What is the difference between a dictionary and a list?
63. What is the difference between a dictionary and a tuple?
64. What is shallow copy?
65. What is deep copy?
66. What is the difference between assignment and dictionary copy?
67. How do you copy a dictionary?
68. Can dictionaries contain lists as values?
69. Can dictionaries be nested inside lists?
70. Why are dictionaries useful in data engineering?
71. How can a dictionary act as a lookup table?
72. How can dictionaries be used for grouping?
73. How are dictionaries related to JSON?
74. What is `json.dumps()`?
75. What is `json.loads()`?
76. How can dictionaries be used for configuration?
77. How can dictionaries be used for metadata?
78. How do you find duplicate values using a dictionary?
79. How do you find the most frequent element?
80. How would you explain dictionaries in a real-world interview scenario?

---

# 87. Final Placement Focus

For Python interviews, make sure you deeply understand:

1. **Dictionary fundamentals**
2. **Key-value structure**
3. **Unique keys**
4. **Mutable values**
5. **Insertion order**
6. **Hashing**
7. **Hashability**
8. **Dictionary lookup complexity**
9. **`[]` vs `get()`**
10. **`add` does not exist for dictionaries**
11. **Assignment vs `update()`**
12. **`pop()`**
13. **`popitem()`**
14. **`clear()`**
15. **`del`**
16. **`keys()`**
17. **`values()`**
18. **`items()`**
19. **Membership testing**
20. **Nested dictionaries**
21. **Dictionary comprehension**
22. **Dictionary merging**
23. **`setdefault()`**
24. **Frequency counting**
25. **Finding maximum/minimum values**
26. **Hashable vs unhashable keys**
27. **Shallow vs deep copy**
28. **Dictionary vs list**
29. **Dictionary vs set**
30. **Dictionary vs tuple**
31. **JSON and dictionaries**
32. **Lookup-table use cases**
33. **Grouping use cases**
34. **Data-engineering applications**
35. **Common output-based traps**

The key idea to remember is:

> **A dictionary is a hash-based mapping from unique hashable keys to values, providing average O(1) key lookup and making it ideal for relationships, mappings, lookups, structured data, grouping, counting, configuration, and JSON-like data.**