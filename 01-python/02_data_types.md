# Python Data Types — Interview Preparation

## 1. What Are Data Types in Python?

A **data type** defines what kind of value a variable contains and what operations can be performed on that value.

Python is **dynamically typed**, which means we do not have to explicitly declare the type of a variable. Python determines the type at runtime.

### Example

```python
name = "Harsha"
age = 22
salary = 45000.50
is_placed = False

print(type(name))
print(type(age))
print(type(salary))
print(type(is_placed))
```

### Output

```text
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

### Real-World Example

In a data engineering application, different types of information naturally have different data types:

```python
employee_id = 101
employee_name = "Harsha"
salary = 55000.75
is_active = True
skills = ["Python", "SQL", "PySpark"]
```

Here:

- `employee_id` → `int`
- `employee_name` → `str`
- `salary` → `float`
- `is_active` → `bool`
- `skills` → `list`

Understanding data types is important because the operations available depend on the type of data.

---

# 2. What Are the Main Built-in Data Types in Python?

Python provides several built-in data types.

| Category | Data Types |
|---|---|
| Numeric | `int`, `float`, `complex` |
| Boolean | `bool` |
| Text | `str` |
| Sequence | `list`, `tuple`, `range` |
| Set | `set`, `frozenset` |
| Mapping | `dict` |
| Binary | `bytes`, `bytearray`, `memoryview` |
| None | `NoneType` |

### Example

```python
age = 22                    # int
price = 99.99               # float
number = 2 + 3j             # complex
is_valid = True             # bool
name = "Harsha"             # str
numbers = [1, 2, 3]         # list
coordinates = (10, 20)      # tuple
values = range(5)           # range
unique = {1, 2, 3}           # set
data = {"name": "Harsha"}   # dict
value = None                # NoneType
```

---

# 3. How Do You Check the Data Type of a Variable?

We can use the built-in `type()` function.

### Example

```python
name = "Harsha"
age = 22

print(type(name))
print(type(age))
```

### Output

```text
<class 'str'>
<class 'int'>
```

### Interview Tip

A common interview follow-up is:

> What is the difference between `type()` and `isinstance()`?

`type()` checks the exact type of an object, while `isinstance()` checks whether an object belongs to a specified class or its subclasses.

### Example

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()

print(type(dog) == Dog)
print(isinstance(dog, Dog))
print(isinstance(dog, Animal))
```

### Output

```text
True
True
True
```

`isinstance()` is generally preferred when checking whether an object is an instance of a class hierarchy.

---

# 4. What Is Dynamic Typing in Python?

Python is dynamically typed because the type of a variable is determined during runtime.

We don't have to specify the type when creating a variable.

### Example

```python
x = 10
print(type(x))

x = "Hello"
print(type(x))

x = [1, 2, 3]
print(type(x))
```

### Output

```text
<class 'int'>
<class 'str'>
<class 'list'>
```

The same variable name can refer to objects of different types at different times.

### Interview Answer

> Python is dynamically typed because variable types are determined at runtime rather than being explicitly declared by the programmer. A variable can also refer to objects of different types during its lifetime.

### Important

Dynamic typing does **not** mean Python has no types.

Python is strongly typed as well as dynamically typed.

---

# 5. What Is Strong Typing in Python?

Python generally does not automatically perform arbitrary conversions between incompatible types.

For example:

```python
age = 22
name = "Harsha"

print(age + name)
```

This produces:

```text
TypeError
```

Python does not automatically convert the integer `22` into a string.

We need explicit conversion:

```python
age = 22
name = "Harsha"

print(str(age) + name)
```

### Output

```text
22Harsha
```

### Interview Answer

> Python is strongly typed because incompatible types generally cannot be combined implicitly. When conversion is required, we usually perform explicit type conversion.

---

# 6. What Is the Difference Between Dynamic Typing and Strong Typing?

These concepts describe different things.

| Concept | Meaning |
|---|---|
| Dynamic typing | Type checking happens at runtime and variables don't require explicit type declarations |
| Strong typing | Python does not freely combine incompatible types through implicit conversion |

### Example

```python
x = 10
x = "Python"
```

This demonstrates **dynamic typing**.

But:

```python
print(10 + "Python")
```

causes a `TypeError`, demonstrating Python's **strong typing**.

### Interview Answer

> Dynamic typing is about when the type is determined, while strong typing is about how strictly different types are treated during operations.

---

# 7. What Is an Integer (`int`)?

An `int` represents whole numbers without a decimal component.

### Examples

```python
age = 22
count = 100
temperature = -5

print(type(age))
```

### Output

```text
<class 'int'>
```

Python integers can represent arbitrarily large integers, limited primarily by available memory.

### Example

```python
number = 10 ** 100
print(number)
```

Python can handle this large integer without overflowing like a fixed-width integer type would.

---

# 8. What Is a Float (`float`)?

A `float` represents numbers with a decimal component.

### Example

```python
price = 99.99
temperature = 36.5
percentage = 85.75

print(type(price))
```

### Output

```text
<class 'float'>
```

### Important Interview Point

Floating-point numbers use binary floating-point representation, so some decimal values cannot be represented exactly.

### Example

```python
print(0.1 + 0.2)
```

Typical output:

```text
0.30000000000000004
```

This does not mean Python's arithmetic is broken. It is a consequence of how floating-point numbers are represented in binary.

### Interview Answer

> Floats are approximate binary floating-point values, so some decimal numbers cannot be represented exactly. That's why calculations such as `0.1 + 0.2` can produce a result slightly different from `0.3`.

---

# 9. What Is a Complex Number in Python?

A complex number contains a real part and an imaginary part.

Python uses `j` to represent the imaginary component.

### Example

```python
number = 3 + 4j

print(number)
print(number.real)
print(number.imag)
```

### Output

```text
(3+4j)
3.0
4.0
```

### Real-World Usage

Complex numbers are useful in mathematical, scientific, engineering, and signal-processing applications.

---

# 10. What Is a Boolean (`bool`)?

A Boolean represents one of two values:

```text
True
False
```

### Example

```python
is_logged_in = True
is_admin = False

print(type(is_logged_in))
```

### Output

```text
<class 'bool'>
```

Boolean values are commonly produced by comparisons.

```python
age = 22

print(age >= 18)
print(age < 18)
```

### Output

```text
True
False
```

---

# 11. Is `bool` an `int` in Python?

Yes. In Python, `bool` is a subclass of `int`.

```python
print(isinstance(True, int))
print(isinstance(False, int))
```

### Output

```text
True
True
```

Boolean values behave numerically in some contexts:

```python
print(True + True)
print(True + False)
```

### Output

```text
2
1
```

Because:

```text
True  → 1
False → 0
```

### Interview Answer

> In Python, `bool` is a subclass of `int`. Therefore, `True` behaves like `1` and `False` behaves like `0` in numeric contexts.

---

# 12. What Is a String (`str`)?

A string is a sequence of Unicode characters.

Strings can be created using single, double, or triple quotes.

### Example

```python
name = "Harsha"
message = 'Hello Python'
description = """Python is widely used in data engineering."""

print(name)
print(type(name))
```

### Output

```text
Harsha
<class 'str'>
```

### Important Point

Strings are **immutable**.

This means that once a string object is created, its contents cannot be changed directly.

---

# 13. Why Are Strings Immutable?

Consider:

```python
name = "Harsha"

name[0] = "X"
```

This produces:

```text
TypeError
```

Instead, we create a new string:

```python
name = "Harsha"
name = "X" + name[1:]

print(name)
```

### Output

```text
Xarsha
```

The original string wasn't modified. A new string was created.

### Interview Answer

> Strings are immutable, meaning their existing characters cannot be modified in place. Operations that appear to modify a string generally create a new string object.

---

# 14. What Is a List?

A list is an ordered, mutable collection that can contain multiple values.

### Example

```python
skills = ["Python", "SQL", "PySpark"]

print(skills)
print(skills[0])
```

### Output

```text
['Python', 'SQL', 'PySpark']
Python
```

Lists can contain different data types:

```python
data = [101, "Harsha", 85.5, True]

print(data)
```

### Important Properties

- Ordered
- Mutable
- Allows duplicate values
- Can contain different data types
- Supports indexing and slicing

---

# 15. What Is a Tuple?

A tuple is an ordered and immutable collection.

### Example

```python
coordinates = (10, 20)

print(coordinates)
print(coordinates[0])
```

### Output

```text
(10, 20)
10
```

Trying to modify it:

```python
coordinates[0] = 100
```

causes:

```text
TypeError
```

### Real-World Example

A tuple can represent fixed information:

```python
location = (17.3850, 78.4867)
```

The latitude and longitude can conceptually be treated as a fixed pair.

---

# 16. What Is a Set?

A set is an unordered collection of unique elements.

### Example

```python
numbers = {1, 2, 3, 2, 1}

print(numbers)
```

### Output

```text
{1, 2, 3}
```

Duplicate values are automatically removed.

### Real-World Example

Suppose a dataset contains repeated skills:

```python
skills = ["Python", "SQL", "Python", "Spark", "SQL"]

unique_skills = set(skills)

print(unique_skills)
```

The set gives the unique values.

### Important Properties

- Unique elements
- Mutable
- No indexing
- Useful for membership testing and set operations

---

# 17. What Is a Dictionary?

A dictionary stores data as **key-value pairs**.

### Example

```python
employee = {
    "id": 101,
    "name": "Harsha",
    "role": "Data Engineer"
}

print(employee["name"])
```

### Output

```text
Harsha
```

### Real-World Example

A dictionary can represent a record:

```python
employee = {
    "employee_id": 101,
    "name": "Harsha",
    "department": "Data Engineering",
    "skills": ["Python", "SQL", "PySpark"]
}
```

This structure is commonly useful when representing JSON-like data.

### Important Properties

- Mutable
- Stores key-value pairs
- Keys must be hashable
- Keys are unique
- Values can be of different types

---

# 18. What Is `None` in Python?

`None` represents the absence of a value.

Its type is `NoneType`.

### Example

```python
result = None

print(result)
print(type(result))
```

### Output

```text
None
<class 'NoneType'>
```

### Real-World Example

Suppose an employee does not currently have a manager:

```python
manager = None
```

This means there is currently no value assigned to `manager`.

### Important

`None` is different from:

```text
0
""
False
[]
```

Those are different values.

---

# 19. What Are Mutable and Immutable Data Types?

This is one of the most important Python interview concepts.

### Mutable

An object is mutable if its contents can be changed after creation.

Common mutable types:

- `list`
- `dict`
- `set`
- `bytearray`

### Immutable

An object is immutable if its contents cannot be changed after creation.

Common immutable types:

- `int`
- `float`
- `complex`
- `bool`
- `str`
- `tuple`
- `frozenset`
- `bytes`

### Example

List:

```python
numbers = [1, 2, 3]

numbers[0] = 100

print(numbers)
```

Output:

```text
[100, 2, 3]
```

String:

```python
name = "Harsha"

# name[0] = "X"
```

This would raise:

```text
TypeError
```

### Interview Answer

> Mutable objects can be changed after they are created, while immutable objects cannot be modified in place. Lists, dictionaries, and sets are examples of mutable types, while strings, integers, tuples, and booleans are immutable.

---

# 20. Why Does Mutability Matter in Python?

Mutability matters because multiple variables can refer to the same object.

### Example

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
print(b)
```

### Output

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
```

Both variables refer to the same list object.

### Interview Follow-Up

**Question:** How can we create an independent copy?

```python
a = [1, 2, 3]
b = a.copy()

b.append(4)

print(a)
print(b)
```

### Output

```text
[1, 2, 3]
[1, 2, 3, 4]
```

The deeper topic of shallow and deep copying will be covered separately.

---

# 21. What Is Type Conversion?

Type conversion means converting a value from one data type to another.

Python provides functions such as:

```text
int()
float()
str()
bool()
list()
tuple()
set()
dict()
```

### Example

```python
age = "22"

age = int(age)

print(age)
print(type(age))
```

### Output

```text
22
<class 'int'>
```

---

# 22. What Is Explicit Type Conversion?

Explicit conversion happens when the programmer manually converts a value.

### Example

```python
price = "99.50"

price = float(price)

print(price)
print(type(price))
```

### Output

```text
99.5
<class 'float'>
```

### Interview Answer

> Explicit type conversion occurs when the programmer intentionally converts a value from one type to another using functions such as `int()`, `float()`, or `str()`.

---

# 23. Does Python Support Implicit Type Conversion?

Yes, Python performs some implicit conversions when they are safe and well-defined.

### Example

```python
x = 10
y = 2.5

result = x + y

print(result)
print(type(result))
```

### Output

```text
12.5
<class 'float'>
```

Here, the integer participates in the operation with the float and the result is a float.

However, Python does not perform arbitrary conversions.

```python
print(10 + "5")
```

produces:

```text
TypeError
```

---

# 24. What Happens When You Convert a Float to an Integer?

When converting a float to an integer using `int()`, the decimal portion is discarded.

### Example

```python
x = 9.8

print(int(x))
```

### Output

```text
9
```

For negative values:

```python
print(int(-9.8))
```

### Output

```text
-9
```

It truncates toward zero; it does not perform mathematical floor rounding.

---

# 25. What Happens When You Convert a String to an Integer?

If the string represents a valid integer, conversion works.

```python
number = "100"

number = int(number)

print(number)
```

Output:

```text
100
```

But:

```python
number = "100.5"
print(int(number))
```

raises:

```text
ValueError
```

because `"100.5"` is not a valid integer literal for `int()` directly.

We can instead do:

```python
number = int(float("100.5"))

print(number)
```

Output:

```text
100
```

---

# 26. What Is Truthy and Falsy in Python?

Python allows many objects to be evaluated in a Boolean context.

Values that evaluate to `False` are called **falsy**.

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
if []:
    print("True")
else:
    print("False")
```

### Output

```text
False
```

Another example:

```python
if [1, 2, 3]:
    print("True")
```

### Output

```text
True
```

### Real-World Example

```python
records = []

if records:
    print("Records available")
else:
    print("No records available")
```

This is a common and readable way to check whether a collection contains values.

---

# 27. What Is the Difference Between `None`, `0`, `False`, and an Empty String?

They are different values even though several of them are falsy.

```python
print(None == 0)
print(False == 0)
print("" == False)
```

### Output

```text
False
True
False
```

`None` specifically represents the absence of a value.

`0` is a numeric value.

`False` is a Boolean value.

`""` is an empty string.

### Important Interview Point

When checking for `None`, prefer:

```python
if value is None:
    ...
```

rather than relying on general truthiness.

---

# 28. What Is Hashability?

An object is hashable if it has a hash value that remains unchanged during its lifetime and can therefore be used as a dictionary key or set element.

Common hashable types include:

- `int`
- `float`
- `str`
- `bool`
- tuples containing only hashable elements
- `frozenset`

### Example

```python
data = {
    "name": "Harsha",
    101: "Employee"
}

print(data)
```

Strings and integers can be dictionary keys.

### Unhashable Example

A list cannot be used as a dictionary key:

```python
data = {
    [1, 2, 3]: "value"
}
```

This produces:

```text
TypeError: unhashable type: 'list'
```

### Interview Answer

> Hashable objects have a stable hash value and can be used as dictionary keys or set elements. Mutable types such as lists and dictionaries are generally unhashable.

---

# 29. Can a Tuple Contain a List?

Yes.

A tuple itself is immutable, but it can contain a mutable object.

### Example

```python
data = (1, 2, [3, 4])

data[2].append(5)

print(data)
```

### Output

```text
(1, 2, [3, 4, 5])
```

The tuple's references cannot be replaced, but the list object inside the tuple can be modified.

### Important Interview Point

This is why saying:

> "A tuple can never change."

is an oversimplification.

The tuple structure is immutable, but objects referenced by it may themselves be mutable.

---

# 30. What Is the Difference Between List, Tuple, Set, and Dictionary?

| Feature | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Syntax | `[]` | `()` | `{}` | `{key: value}` |
| Ordered | Yes | Yes | No indexing/order should not be relied on for interview purposes | Yes |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: No |
| Indexing | Yes | Yes | No | By key |
| Main use | Collection of items | Fixed collection | Unique values | Key-value data |

### Example

```python
my_list = [1, 2, 2]
my_tuple = (1, 2, 2)
my_set = {1, 2, 2}
my_dict = {"id": 101, "name": "Harsha"}
```

---

# 31. Which Python Data Types Are Ordered?

Common ordered built-in collection types include:

- `list`
- `tuple`
- `str`
- `range`
- `dict` — dictionaries preserve insertion order in modern Python versions

Sets do not provide indexing and should not be treated as ordered sequences.

### Example

```python
data = {"name": "Harsha", "age": 22, "role": "Developer"}

print(data)
```

The dictionary preserves insertion order.

### Interview Tip

Do not simply say:

> "Dictionaries are unordered."

That is outdated for modern Python. Modern Python dictionaries preserve insertion order as a language guarantee.

---

# 32. What Is the Difference Between `is` and `==`?

This is an important interview question related to objects and values.

`==` checks whether two objects are equal in value.

`is` checks whether two references point to the same object.

### Example

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

### Output

```text
True
False
```

The lists contain the same values, but they are separate objects.

### Another Example

```python
a = [1, 2, 3]
b = a

print(a == b)
print(a is b)
```

### Output

```text
True
True
```

### Interview Answer

> `==` compares values for equality, while `is` checks object identity. We normally use `is` when checking identity, especially for singleton values such as `None`.

Correct:

```python
if value is None:
    print("No value")
```

---

# 33. What Is Object Identity?

Every Python object has an identity during its lifetime.

The `id()` function can be used to obtain an identity value for an object.

### Example

```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(id(a))
print(id(b))
print(id(c))
```

`a` and `b` refer to the same object, so their IDs are the same.

`c` is a separate list, so its ID is different.

### Important

Do not use `id()` values as persistent identifiers in an application. They represent object identity during the object's lifetime.

---

# 34. What Happens When Two Variables Have the Same Value?

Consider:

```python
a = [1, 2, 3]
b = [1, 2, 3]
```

Both variables contain equal values:

```python
print(a == b)
```

Output:

```text
True
```

But they are separate objects:

```python
print(a is b)
```

Output:

```text
False
```

This demonstrates the difference between **equality** and **identity**.

---

# 35. What Are Sequence Data Types?

A sequence is an ordered collection that supports operations such as indexing and often slicing.

Common Python sequence types include:

- `str`
- `list`
- `tuple`
- `range`

### Example

```python
name = "Harsha"

print(name[0])
print(name[1:4])
```

### Output

```text
H
ars
```

Lists and tuples also support indexing:

```python
numbers = [10, 20, 30]

print(numbers[0])
print(numbers[-1])
```

Output:

```text
10
30
```

---

# 36. What Is Indexing?

Indexing is accessing an individual element using its position.

Python uses **zero-based indexing**.

### Example

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

Negative indexing starts from the end:

```python
print(skills[-1])
```

Output:

```text
PySpark
```

---

# 37. What Is Slicing?

Slicing extracts a portion of a sequence.

Syntax:

```python
sequence[start:stop:step]
```

The `stop` index is excluded.

### Example

```python
numbers = [0, 1, 2, 3, 4, 5]

print(numbers[1:4])
```

### Output

```text
[1, 2, 3]
```

### With Step

```python
print(numbers[0:6:2])
```

Output:

```text
[0, 2, 4]
```

### Reverse

```python
print(numbers[::-1])
```

Output:

```text
[5, 4, 3, 2, 1, 0]
```

---

# 38. What Is the `range` Data Type?

`range` represents an immutable sequence of numbers commonly used for iteration.

### Example

```python
numbers = range(5)

print(list(numbers))
```

### Output

```text
[0, 1, 2, 3, 4]
```

The stop value is excluded.

### Example

```python
numbers = range(1, 10, 2)

print(list(numbers))
```

Output:

```text
[1, 3, 5, 7, 9]
```

### Interview Point

`range()` is useful because it represents the sequence without necessarily storing every number as a separate list element.

---

# 39. What Is the Difference Between `range()` and a List?

A list stores its elements, while a range represents a sequence defined by start, stop, and step.

### Example

```python
numbers = range(1000000)

print(type(numbers))
```

Output:

```text
<class 'range'>
```

If we create:

```python
numbers = list(range(1000000))
```

we actually create a list containing one million integer objects.

### Interview Answer

> `range` is an immutable sequence representation commonly used for iteration, whereas a list is a mutable collection that stores its elements. `range` is generally more memory-efficient when we only need to iterate over a numeric sequence.

---

# 40. What Are Binary Data Types?

Python provides data types for handling binary data:

- `bytes`
- `bytearray`
- `memoryview`

### Example

```python
data = b"Python"

print(data)
print(type(data))
```

Output:

```text
b'Python'
<class 'bytes'>
```

`bytes` is immutable.

`bytearray` is mutable.

### Example

```python
data = bytearray(b"Python")

data[0] = 74

print(data)
```

Output:

```text
bytearray(b'Jython')
```

Binary types are useful when working with files, network communication, protocols, and raw binary data.

---

# 41. What Is `bytes`?

`bytes` represents an immutable sequence of bytes.

### Example

```python
data = b"Hello"

print(data)
print(type(data))
```

### Output

```text
b'Hello'
<class 'bytes'>
```

You cannot modify individual bytes:

```python
data[0] = 72
```

This raises a `TypeError`.

---

# 42. What Is `bytearray`?

`bytearray` is similar to `bytes`, but it is mutable.

### Example

```python
data = bytearray(b"Hello")

data[0] = 74

print(data)
```

### Output

```text
bytearray(b'Jello')
```

### Interview Answer

> `bytes` is immutable binary data, while `bytearray` provides a mutable binary sequence.

---

# 43. What Is `frozenset`?

`frozenset` is an immutable version of a set.

### Example

```python
numbers = frozenset([1, 2, 3])

print(numbers)
print(type(numbers))
```

Output:

```text
frozenset({1, 2, 3})
<class 'frozenset'>
```

You cannot add or remove elements.

### Important Difference

A normal set is mutable:

```python
numbers = {1, 2, 3}
numbers.add(4)
```

A frozenset is immutable:

```python
numbers = frozenset([1, 2, 3])
```

### Real-World Use

Because a `frozenset` is immutable and hashable, it can be used as a dictionary key or as an element of another set.

---

# 44. Can a Dictionary Have Duplicate Keys?

No. Dictionary keys must be unique.

### Example

```python
data = {
    "name": "Harsha",
    "name": "Developer"
}

print(data)
```

### Output

```text
{'name': 'Developer'}
```

The later assignment replaces the earlier value for the same key.

### Interview Answer

> Dictionary keys are unique. If the same key appears multiple times, the later value replaces the previous value.

---

# 45. Can Dictionary Values Be Duplicated?

Yes.

```python
data = {
    "employee1": "Python",
    "employee2": "Python",
    "employee3": "SQL"
}

print(data)
```

Multiple keys can have the same value.

The uniqueness requirement applies to **keys**, not values.

---

# 46. Can Dictionary Keys Be Lists?

No.

```python
data = {
    [1, 2, 3]: "value"
}
```

This raises:

```text
TypeError: unhashable type: 'list'
```

A tuple containing only hashable elements can be a key:

```python
data = {
    (1, 2): "value"
}

print(data)
```

This works because the tuple is hashable.

---

# 47. What Happens When You Assign One Variable to Another?

Python variables hold references to objects.

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

`b = a` does not create a new list. Both names refer to the same list object.

### Interview Answer

> Assignment generally binds another variable name to the same object rather than automatically creating a copy.

---

# 48. What Is Variable Reassignment?

A variable can be reassigned to another object.

```python
x = 10
print(type(x))

x = "Python"
print(type(x))
```

Output:

```text
<class 'int'>
<class 'str'>
```

The variable name `x` first refers to an integer object and later refers to a string object.

This is another example of dynamic typing.

---

# 49. Can Different Data Types Be Stored in the Same List?

Yes.

Python lists can contain objects of different types.

### Example

```python
data = [
    101,
    "Harsha",
    85.5,
    True,
    None
]

print(data)
```

Output:

```text
[101, 'Harsha', 85.5, True, None]
```

This is possible because Python lists store references to objects rather than requiring every element to have the same type.

### Interview Follow-Up

Although this is allowed, in real-world applications we generally prefer collections with logically related data because consistent data makes processing easier.

---

# 50. How Can You Find the Length of Different Data Types?

The `len()` function works with objects that define a length.

### Example

```python
name = "Harsha"
numbers = [1, 2, 3]
data = {"id": 101, "name": "Harsha"}

print(len(name))
print(len(numbers))
print(len(data))
```

### Output

```text
6
3
2
```

For a dictionary, `len()` returns the number of key-value pairs.

### Important

Not every object supports `len()`.

```python
number = 100

print(len(number))
```

This raises:

```text
TypeError
```

---

# 51. What Is the Difference Between `str()` and `repr()`?

Both can produce string representations, but they serve different purposes.

`str()` is generally intended to provide a user-friendly representation.

`repr()` aims to provide an unambiguous representation useful for debugging and development.

### Example

```python
name = "Harsha"

print(str(name))
print(repr(name))
```

Output:

```text
Harsha
'Harsha'
```

### Interview Answer

> `str()` is intended for a readable representation of an object, while `repr()` is intended to provide a more developer-oriented representation that can help with debugging.

---

# 52. What Is the Difference Between `int`, `float`, and `str`?

| Type | Example | Purpose |
|---|---|---|
| `int` | `10` | Whole numbers |
| `float` | `10.5` | Decimal/floating-point values |
| `str` | `"10"` | Text |

These are different types even if they appear similar.

```python
a = 10
b = 10.0
c = "10"

print(type(a))
print(type(b))
print(type(c))
```

Output:

```text
<class 'int'>
<class 'float'>
<class 'str'>
```

---

# 53. What Is the Difference Between `10` and `"10"`?

`10` is an integer.

`"10"` is a string.

```python
a = 10
b = "10"

print(a + 5)
print(b + "5")
```

Output:

```text
15
105
```

The first performs numeric addition.

The second performs string concatenation.

Trying:

```python
print(b + 5)
```

produces:

```text
TypeError
```

---

# 54. What Is Type Inference in Python?

Python determines the type of an object from the value assigned to a variable.

```python
x = 10
```

Python knows that `x` refers to an integer object.

```python
x = "Python"
```

Now `x` refers to a string object.

The programmer doesn't need to declare:

```python
int x
```

as would be required in some statically typed languages.

---

# 55. Is Python Statically Typed or Dynamically Typed?

Python is **dynamically typed**.

Example:

```python
x = 10
x = "Python"
x = [1, 2, 3]
```

The variable can refer to objects of different types at runtime.

### Important Interview Answer

> Python is dynamically typed because types are associated with objects and checked at runtime rather than requiring explicit variable type declarations.

---

# 56. Is Python Strongly Typed or Weakly Typed?

Python is generally considered **strongly typed**.

For example:

```python
print("10" + 5)
```

produces a `TypeError`.

Python doesn't silently treat `"10"` as the integer `10` for this operation.

You need:

```python
print(int("10") + 5)
```

Output:

```text
15
```

---

# 57. What Is a Nested Data Structure?

A nested data structure is a data structure containing another data structure.

### Example

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

print(employees[0]["name"])
```

### Output

```text
Harsha
```

### Real-World Usage

Nested dictionaries and lists are common when working with JSON and API responses.

For example, an API might return:

```python
response = {
    "status": "success",
    "data": [
        {"id": 1, "name": "Harsha"},
        {"id": 2, "name": "Rahul"}
    ]
}
```

This is particularly relevant when working with REST APIs and data engineering pipelines.

---

# 58. What Is a JSON-Like Python Structure?

JSON data commonly maps to Python structures as follows:

| JSON | Python |
|---|---|
| object | `dict` |
| array | `list` |
| string | `str` |
| number | `int` / `float` |
| true | `True` |
| false | `False` |
| null | `None` |

### Example

JSON-like data:

```json
{
    "name": "Harsha",
    "age": 22,
    "skills": ["Python", "SQL"],
    "active": true
}
```

Equivalent Python representation:

```python
data = {
    "name": "Harsha",
    "age": 22,
    "skills": ["Python", "SQL"],
    "active": True
}
```

This mapping is important when working with APIs and data pipelines.

---

# 59. What Data Type Should You Use for Unique Values?

A `set` is generally appropriate when the primary requirement is to store unique values.

### Example

```python
skills = ["Python", "SQL", "Python", "SQL", "PySpark"]

unique_skills = set(skills)

print(unique_skills)
```

The duplicates are removed.

### Interview Follow-Up

If you need to preserve the original order while removing duplicates, a common approach is:

```python
skills = ["Python", "SQL", "Python", "PySpark", "SQL"]

unique_skills = list(dict.fromkeys(skills))

print(unique_skills)
```

Output:

```text
['Python', 'SQL', 'PySpark']
```

---

# 60. Which Data Type Should You Use for Key-Value Data?

Use a dictionary.

### Example

```python
employee = {
    "id": 101,
    "name": "Harsha",
    "department": "Data Engineering"
}
```

Accessing the value:

```python
print(employee["department"])
```

Output:

```text
Data Engineering
```

Dictionaries are especially useful when data naturally has named fields.

---

# 61. Which Data Type Should You Use for Fixed Data?

A tuple is often suitable when you want an ordered collection that should not be modified.

### Example

```python
rgb = (255, 255, 255)
```

The tuple structure cannot be changed.

However, the choice should depend on the requirements. Immutability is the key advantage rather than simply assuming tuples are always better than lists.

---

# 62. Why Might You Choose a Tuple Instead of a List?

Common reasons include:

1. The collection represents fixed data.
2. You want immutability.
3. The tuple can be used as a dictionary key if all its elements are hashable.
4. It can communicate that the values should not be modified.

### Example

```python
database_config = ("localhost", 5432, "company_db")
```

This can conceptually represent a fixed configuration tuple.

---

# 63. Why Might You Choose a Set Instead of a List?

Use a set when uniqueness and membership testing are important.

### Example

```python
allowed_roles = {"admin", "developer", "manager"}

if "developer" in allowed_roles:
    print("Role allowed")
```

### Output

```text
Role allowed
```

A set is generally designed for efficient membership testing and mathematical set operations.

---

# 64. Why Might You Choose a Dictionary Instead of a List?

A dictionary is useful when values need to be accessed using meaningful keys.

Instead of:

```python
employee = [101, "Harsha", "Data Engineer"]
```

we can use:

```python
employee = {
    "id": 101,
    "name": "Harsha",
    "role": "Data Engineer"
}
```

This makes the code more readable because each value has a meaningful name.

---

# 65. Interview Trap: Is Everything in Python an Object?

In Python's object model, essentially everything you manipulate is an object, including numbers, strings, functions, classes, and modules.

### Example

```python
x = 10

print(type(x))
print(type(print))
```

Output will show that both are objects with their respective types.

### Interview Answer

> Python follows an object-oriented object model in which values such as integers, strings, functions, and classes are represented as objects.

---

# 66. Interview Trap: Are Variables Objects in Python?

A more accurate explanation is that variables are **names bound to objects**.

For example:

```python
x = 10
```

Here:

- `10` is an object.
- `x` is a name referring to that object.

This distinction becomes important when explaining assignment, mutability, identity, and copying.

---

# 67. Interview Trap: Are Lists Stored Directly Inside Variables?

Conceptually, a variable name refers to a list object.

```python
numbers = [1, 2, 3]
```

The name `numbers` refers to the list object.

If we do:

```python
another = numbers
```

both names refer to the same object.

```python
another.append(4)

print(numbers)
```

Output:

```text
[1, 2, 3, 4]
```

This is why understanding references and mutability is important.

---

# 68. Common Data Type Interview Questions — Quick Revision

### Q1. Is Python dynamically typed?

**Answer:** Yes. Variable names do not require explicit type declarations, and the type of the referenced object is determined at runtime.

### Q2. Is Python strongly typed?

**Answer:** Yes, generally. Python does not freely combine incompatible types through implicit conversion.

### Q3. Which types are mutable?

**Answer:** Common examples are `list`, `dict`, `set`, and `bytearray`.

### Q4. Which types are immutable?

**Answer:** Common examples are `int`, `float`, `complex`, `bool`, `str`, `tuple`, `frozenset`, and `bytes`.

### Q5. What is the difference between `is` and `==`?

**Answer:** `==` checks equality of values, while `is` checks whether two references point to the same object.

### Q6. Why is `None` special?

**Answer:** `None` represents the absence of a value and is the sole instance of `NoneType`.

### Q7. Can a list contain different data types?

**Answer:** Yes.

### Q8. Can a tuple contain a list?

**Answer:** Yes. The tuple is immutable, but the list inside it can still be mutable.

### Q9. Can a list be a dictionary key?

**Answer:** No, because lists are unhashable.

### Q10. Can a tuple be a dictionary key?

**Answer:** Yes, if all elements inside the tuple are hashable.

### Q11. Does a set allow duplicates?

**Answer:** No.

### Q12. Does a dictionary allow duplicate keys?

**Answer:** No. A later value replaces the previous value for the same key.

### Q13. What does `type()` do?

**Answer:** It returns the type of an object.

### Q14. What does `isinstance()` do?

**Answer:** It checks whether an object is an instance of a specified class or its subclasses.

### Q15. What is type conversion?

**Answer:** Converting a value from one data type to another using functions such as `int()`, `float()`, `str()`, `list()`, or `tuple()`.

---

# 69. Practical Interview Examples

## Example 1 — Employee Record

```python
employee = {
    "id": 101,
    "name": "Harsha",
    "age": 22,
    "skills": ["Python", "SQL", "PySpark"],
    "active": True
}

print(employee["name"])
print(employee["skills"])
```

This demonstrates:

- Dictionary
- Integer
- String
- List
- Boolean

---

## Example 2 — Removing Duplicate Data

```python
skills = ["Python", "SQL", "Python", "PySpark", "SQL"]

unique_skills = set(skills)

print(unique_skills)
```

This demonstrates why sets are useful for unique values.

---

## Example 3 — Fixed Configuration

```python
database = ("localhost", 5432, "company_db")

host = database[0]
port = database[1]
name = database[2]

print(host)
print(port)
print(name)
```

This demonstrates tuple usage for a fixed ordered collection.

---

## Example 4 — API-Like Data

```python
response = {
    "status": "success",
    "users": [
        {"id": 101, "name": "Harsha"},
        {"id": 102, "name": "Rahul"}
    ]
}

print(response["users"][0]["name"])
```

### Output

```text
Harsha
```

This demonstrates nested dictionaries and lists, which are common when processing API/JSON data.

---

# 70. Mini Practice Questions

Try answering these without looking at the answers above.

1. What is dynamic typing in Python?
2. What is strong typing?
3. What is the difference between mutable and immutable objects?
4. Give five examples of immutable types.
5. Give four examples of mutable types.
6. Why are strings immutable?
7. What is the difference between a list and tuple?
8. What is the difference between a set and a list?
9. What is the difference between a dictionary and a list?
10. Why can't a list be a dictionary key?
11. Can a tuple contain a mutable object?
12. What is the difference between `is` and `==`?
13. What is `None`?
14. What is the difference between `None` and `False`?
15. What is type conversion?
16. What happens when `int(9.8)` is executed?
17. What are truthy and falsy values?
18. What is hashability?
19. What is the difference between `bytes` and `bytearray`?
20. What is `frozenset`?
21. What does `range()` return?
22. Why is `range()` memory-efficient compared with creating a large list?
23. What is the difference between `type()` and `isinstance()`?
24. Can a dictionary have duplicate values?
25. Can a dictionary have duplicate keys?
26. Can different data types exist in the same list?
27. What is object identity?
28. What does `id()` return?
29. What happens when `b = a` for a list?
30. Why is understanding mutability important in Python?

---

# 71. Quick Interview Revision Sheet

## Python Data Types

```text
int          → Whole numbers
float        → Decimal/floating-point numbers
complex      → Real + imaginary numbers
bool         → True / False
str          → Text
list         → Ordered + mutable collection
tuple        → Ordered + immutable collection
set          → Unique collection
frozenset    → Immutable set
dict         → Key-value collection
range        → Immutable numeric sequence
bytes        → Immutable binary data
bytearray    → Mutable binary data
memoryview   → View over binary data
NoneType     → Type of None
```

## Mutable

```text
list
dict
set
bytearray
```

## Immutable

```text
int
float
complex
bool
str
tuple
frozenset
bytes
```

## Most Important Interview Concepts

```text
Dynamic typing
Strong typing
Mutable vs immutable
Identity vs equality
Hashability
Truthy vs falsy
Type conversion
Object references
Indexing
Slicing
Nested data structures
```

## Interview Rule

When explaining a Python data type in an interview, don't stop at its definition.

A strong answer should usually cover:

**Definition → Properties → Example → Code → Real-world use → Important limitation → Possible follow-up**

For example:

> "A list is an ordered and mutable collection. It allows duplicate values and can contain different data types. I would use a list when I need an ordered collection that may change during execution. For example, I could store the skills associated with an employee in a list. If the interviewer asks about its limitations, I would mention that lists are mutable and are not suitable as dictionary keys because they are unhashable."

This style demonstrates not only that you know the definition, but that you understand **when and why to use the data type**.