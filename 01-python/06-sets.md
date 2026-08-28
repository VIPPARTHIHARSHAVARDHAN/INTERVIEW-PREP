# Python Sets — Interview Preparation

## 1. What Is a Set in Python?

A **set** is a mutable collection of **unique, hashable elements**.

A set is mainly used when we need to:

- Remove duplicates
- Perform mathematical set operations
- Check membership efficiently
- Find common or different elements between collections

### Example

```python
numbers = {10, 20, 30, 40}

print(numbers)
```

A set does not support positional indexing like a list or tuple.

### Important Properties

A Python set is:

- Mutable
- Unordered for indexing purposes
- Does not allow duplicate elements
- Contains only hashable elements
- Supports fast membership testing on average
- Supports union, intersection, difference, and symmetric difference
- Does not support indexing or slicing

### Interview Answer

> A set is a mutable collection of unique hashable elements. It is mainly useful for removing duplicates, performing set operations, and efficient membership testing.

---

# 2. Does a Set Allow Duplicate Values?

No.

If duplicate values are provided, only one copy is stored.

```python
numbers = {10, 20, 20, 30, 30}

print(numbers)
```

Output will contain each value only once:

```text
{10, 20, 30}
```

### Important

A set automatically removes duplicates.

---

# 3. Why Does a Set Not Contain Duplicates?

Set elements are stored based on **hashing and equality**.

If two values are considered equal, the set keeps only one element.

```python
numbers = {1, 1, 2, 2, 3}

print(numbers)
```

Output:

```text
{1, 2, 3}
```

### Interview Answer

> Sets use hashing to organize unique elements. If another element compares equal to an existing element, it is not stored as a separate element.

---

# 4. How Do You Create a Set?

You can use curly braces:

```python
numbers = {1, 2, 3}
```

Or the `set()` constructor:

```python
numbers = set([1, 2, 3])
```

Both create a set.

---

# 5. How Do You Create an Empty Set?

This is a very common interview question.

You must use:

```python
my_set = set()
```

Do **not** use:

```python
my_set = {}
```

because `{}` creates an empty dictionary.

### Example

```python
a = set()
b = {}

print(type(a))
print(type(b))
```

Output:

```text
<class 'set'>
<class 'dict'>
```

### Interview Answer

> `set()` creates an empty set, while `{}` creates an empty dictionary.

---

# 6. What Is the Difference Between a Set and a List?

| Set | List |
|---|---|
| Stores unique elements | Allows duplicates |
| Does not support indexing | Supports indexing |
| Mutable | Mutable |
| Optimized for membership testing | Membership generally requires sequential search |
| Supports mathematical set operations | Does not directly provide set operations |
| Elements must be hashable | Elements can be any objects |
| No positional ordering should be relied upon | Ordered sequence |

### Example

```python
my_list = [1, 2, 2, 3]
my_set = {1, 2, 2, 3}

print(my_list)
print(my_set)
```

Output:

```text
[1, 2, 2, 3]
{1, 2, 3}
```

---

# 7. What Is the Difference Between a Set and a Tuple?

| Set | Tuple |
|---|---|
| Mutable | Immutable |
| Unique elements | Allows duplicates |
| No indexing | Supports indexing |
| Elements must be hashable | Elements themselves can include mutable objects |
| Used for uniqueness and set operations | Used for fixed ordered data |

### Example

```python
my_set = {1, 2, 3}
my_tuple = (1, 2, 2, 3)

print(my_set)
print(my_tuple)
```

Output:

```text
{1, 2, 3}
(1, 2, 2, 3)
```

---

# 8. Are Sets Ordered or Unordered?

For interview purposes, do not treat a set as an indexed or position-based collection.

You should not rely on the order in which set elements are displayed or iterated.

```python
numbers = {10, 20, 30, 40}

for number in numbers:
    print(number)
```

The important point is:

> A set is not a sequence and does not support positional access.

### Avoid Saying

> "A set always prints in random order."

That is an oversimplification.

### Better Interview Answer

> A set is not an ordered sequence, so I should not depend on element positions or displayed iteration order.

---

# 9. Can You Access a Set Using an Index?

No.

```python
numbers = {10, 20, 30}

print(numbers[0])
```

This raises:

```text
TypeError: 'set' object is not subscriptable
```

### Why?

A set is not a positional collection.

If you need indexing, convert it to a list:

```python
numbers = {10, 20, 30}

numbers_list = list(numbers)

print(numbers_list[0])
```

However, the resulting position should not be treated as a meaningful original set order.

---

# 10. Can You Slice a Set?

No.

Sets do not support slicing.

```python
numbers = {1, 2, 3, 4}

print(numbers[1:3])
```

This raises:

```text
TypeError: 'set' object is not subscriptable
```

---

# 11. What Is Hashability?

Hashability is an important concept for sets.

A set element must be **hashable**.

Hashable objects have a hash value that remains stable during their lifetime and can be compared for equality.

Common hashable objects include:

```text
int
float
str
bool
tuple (when its elements are hashable)
```

Common unhashable objects include:

```text
list
dict
set
```

---

# 12. Can a List Be an Element of a Set?

No.

```python
numbers = {[1, 2], [3, 4]}
```

This raises:

```text
TypeError: unhashable type: 'list'
```

### Why?

Lists are mutable and therefore unhashable.

---

# 13. Can a Tuple Be an Element of a Set?

Yes, if all elements inside the tuple are hashable.

```python
data = {(1, 2), (3, 4)}

print(data)
```

This works.

But:

```python
data = {([1, 2], 3)}
```

raises:

```text
TypeError: unhashable type: 'list'
```

because the tuple contains a list.

### Interview Answer

> A tuple can be stored in a set if all of its elements are hashable.

---

# 14. What Is Membership Testing in a Set?

Membership testing checks whether an element exists.

Use:

```python
in
```

### Example

```python
skills = {"Python", "SQL", "PySpark"}

print("Python" in skills)
print("Java" in skills)
```

Output:

```text
True
False
```

Sets are designed to make membership testing efficient on average.

---

# 15. What Is the Average Time Complexity of Set Membership?

For a normal hash set, membership testing is generally:

```text
Average: O(1)
Worst case: O(n)
```

Example:

```python
numbers = {10, 20, 30, 40}

print(30 in numbers)
```

### Interview Answer

> Set membership is O(1) on average because Python uses hashing, although the theoretical worst case can be O(n).

---

# 16. How Do You Add an Element to a Set?

Use `add()`.

```python
numbers = {1, 2, 3}

numbers.add(4)

print(numbers)
```

The set now contains:

```text
{1, 2, 3, 4}
```

---

# 17. What Happens If You Add a Duplicate Element?

Nothing changes.

```python
numbers = {1, 2, 3}

numbers.add(2)

print(numbers)
```

Output still contains:

```text
{1, 2, 3}
```

`add()` does not create duplicates.

---

# 18. What Is the Difference Between `add()` and `update()`?

`add()` adds **one element**.

```python
numbers = {1, 2}

numbers.add(3)

print(numbers)
```

`update()` adds elements from an iterable.

```python
numbers = {1, 2}

numbers.update([3, 4, 5])

print(numbers)
```

Result:

```text
{1, 2, 3, 4, 5}
```

### Important Interview Trap

```python
numbers.add([3, 4])
```

raises an error because the list is unhashable.

But:

```python
numbers.update([3, 4])
```

works because the list is used as an iterable and its individual elements are added.

---

# 19. What Does `set.update()` Accept?

`update()` accepts an iterable.

Examples:

```python
numbers = {1, 2}

numbers.update([3, 4])
numbers.update((5, 6))
numbers.update({7, 8})

print(numbers)
```

The elements from each iterable are added.

---

# 20. What Happens With `update()` on a String?

A string is iterable, so its characters are added individually.

```python
letters = {"a", "b"}

letters.update("python")

print(letters)
```

The characters from `"python"` are added individually.

### Important

This:

```python
letters.add("python")
```

adds `"python"` as **one element**.

But:

```python
letters.update("python")
```

adds the individual characters.

---

# 21. How Do You Remove an Element Using `remove()`?

Use:

```python
remove()
```

### Example

```python
numbers = {1, 2, 3}

numbers.remove(2)

print(numbers)
```

Result:

```text
{1, 3}
```

---

# 22. What Happens If `remove()` Cannot Find the Element?

It raises `KeyError`.

```python
numbers = {1, 2, 3}

numbers.remove(10)
```

Output:

```text
KeyError: 10
```

---

# 23. What Is the Difference Between `remove()` and `discard()`?

This is an important interview question.

### `remove()`

Raises `KeyError` if the element does not exist.

```python
numbers = {1, 2, 3}

numbers.remove(10)
```

### `discard()`

Does nothing if the element does not exist.

```python
numbers = {1, 2, 3}

numbers.discard(10)

print(numbers)
```

No error occurs.

### Interview Answer

> `remove()` raises `KeyError` when the element is absent, while `discard()` silently does nothing.

---

# 24. What Does `pop()` Do on a Set?

`pop()` removes and returns an element from the set.

```python
numbers = {10, 20, 30}

value = numbers.pop()

print(value)
print(numbers)
```

The removed element should not be assumed to be a specific value.

### Important

Unlike a list, you cannot specify an index:

```python
numbers.pop(0)
```

is invalid.

### Interview Answer

> Set `pop()` removes and returns an arbitrary element. I should not depend on which particular element it removes.

---

# 25. What Does `clear()` Do?

It removes all elements from the set.

```python
numbers = {1, 2, 3}

numbers.clear()

print(numbers)
```

Output:

```text
set()
```

The set object still exists, but it is empty.

---

# 26. What Does `del` Do With a Set?

`del` removes the variable binding.

```python
numbers = {1, 2, 3}

del numbers
```

After that, accessing `numbers` produces a `NameError`.

This is different from:

```python
numbers.clear()
```

which keeps the variable pointing to an empty set.

---

# 27. What Is Set Union?

Union combines all unique elements from two sets.

Mathematically:

```text
A ∪ B
```

Python operator:

```python
|
```

### Example

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)
```

Output:

```text
{1, 2, 3, 4, 5}
```

You can also use:

```python
a.union(b)
```

---

# 28. What Is Set Intersection?

Intersection returns elements common to both sets.

Mathematically:

```text
A ∩ B
```

Python operator:

```python
&
```

### Example

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a & b)
```

Output:

```text
{2, 3}
```

You can also use:

```python
a.intersection(b)
```

---

# 29. What Is Set Difference?

Difference returns elements that exist in the first set but not in the second.

Mathematically:

```text
A - B
```

### Example

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a - b)
print(b - a)
```

Output:

```text
{1}
{4}
```

### Important

Set difference is **directional**.

`A - B` is not necessarily equal to `B - A`.

---

# 30. What Is Symmetric Difference?

Symmetric difference returns elements that belong to either set but not both.

Mathematically:

```text
A △ B
```

Python operator:

```python
^
```

### Example

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a ^ b)
```

Output:

```text
{1, 4}
```

---

# 31. What Is the Difference Between Difference and Symmetric Difference?

### Difference

```python
a - b
```

Returns:

```text
elements only in a
```

### Symmetric difference

```python
a ^ b
```

Returns:

```text
elements only in a + elements only in b
```

### Example

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a - b)
print(a ^ b)
```

Output:

```text
{1}
{1, 4}
```

---

# 32. Can Set Operations Be Performed Using Methods?

Yes.

```python
a = {1, 2, 3}
b = {2, 3, 4}

print(a.union(b))
print(a.intersection(b))
print(a.difference(b))
print(a.symmetric_difference(b))
```

Equivalent operators are:

```text
union                  |
intersection           &
difference             -
symmetric difference   ^
```

---

# 33. What Is an In-Place Set Operation?

Some set methods modify the existing set.

Examples:

```python
update()
intersection_update()
difference_update()
symmetric_difference_update()
```

### Example

```python
a = {1, 2, 3}

a.update({4, 5})

print(a)
```

Output:

```text
{1, 2, 3, 4, 5}
```

The original set was modified.

---

# 34. What Is the Difference Between `union()` and `update()`?

This is an important distinction.

### `union()`

Creates and returns a new set.

```python
a = {1, 2}
b = {2, 3}

result = a.union(b)

print(a)
print(result)
```

`a` remains unchanged.

### `update()`

Modifies the original set.

```python
a = {1, 2}
b = {2, 3}

a.update(b)

print(a)
```

Output:

```text
{1, 2, 3}
```

### Interview Answer

> `union()` returns a new set without modifying the original set, while `update()` adds elements to the existing set.

---

# 35. What Is `intersection_update()`?

It keeps only elements that are common to both sets.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.intersection_update(b)

print(a)
```

Output:

```text
{2, 3}
```

The original `a` is modified.

---

# 36. What Is `difference_update()`?

It removes elements from the first set that are present in another set.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.difference_update(b)

print(a)
```

Output:

```text
{1}
```

---

# 37. What Is `symmetric_difference_update()`?

It replaces the set with its symmetric difference.

```python
a = {1, 2, 3}
b = {2, 3, 4}

a.symmetric_difference_update(b)

print(a)
```

Output:

```text
{1, 4}
```

---

# 38. What Is a Subset?

Set `A` is a subset of set `B` if every element of `A` is also present in `B`.

Mathematically:

```text
A ⊆ B
```

Python:

```python
A.issubset(B)
```

### Example

```python
a = {1, 2}
b = {1, 2, 3, 4}

print(a.issubset(b))
```

Output:

```text
True
```

You can also use:

```python
print(a <= b)
```

---

# 39. What Is a Proper Subset?

A proper subset is a subset that is not equal to the other set.

Python uses:

```python
<
```

### Example

```python
a = {1, 2}
b = {1, 2, 3}

print(a < b)
```

Output:

```text
True
```

But:

```python
a = {1, 2}
b = {1, 2}

print(a < b)
```

Output:

```text
False
```

because they are equal.

---

# 40. What Is a Superset?

Set `A` is a superset of `B` if `A` contains every element of `B`.

Python:

```python
A.issuperset(B)
```

### Example

```python
a = {1, 2, 3, 4}
b = {1, 2}

print(a.issuperset(b))
```

Output:

```text
True
```

You can also use:

```python
print(a >= b)
```

---

# 41. What Is a Proper Superset?

A proper superset contains all elements of another set and has additional elements.

Python uses:

```python
>
```

### Example

```python
a = {1, 2, 3}
b = {1, 2}

print(a > b)
```

Output:

```text
True
```

---

# 42. What Does `isdisjoint()` Do?

It checks whether two sets have no common elements.

```python
a = {1, 2}
b = {3, 4}

print(a.isdisjoint(b))
```

Output:

```text
True
```

If they share an element:

```python
a = {1, 2}
b = {2, 3}

print(a.isdisjoint(b))
```

Output:

```text
False
```

---

# 43. What Is a Frozen Set?

A **frozenset** is an immutable version of a set.

```python
numbers = frozenset([1, 2, 3])

print(numbers)
```

You cannot modify it using:

```python
add()
remove()
discard()
```

### Example

```python
numbers = frozenset([1, 2, 3])

numbers.add(4)
```

This raises:

```text
AttributeError
```

---

# 44. Why Would You Use a Frozenset?

A frozenset is useful when you need set behavior but the collection itself must be immutable and hashable.

For example:

```python
permissions = frozenset(["read", "write"])

roles = {
    permissions: "editor"
}
```

A normal mutable set cannot be used as a dictionary key.

### Interview Answer

> A frozenset is an immutable and hashable set-like object. It is useful when I need unique elements and set operations but also need the collection itself to be immutable or usable as a dictionary key.

---

# 45. What Is the Difference Between `set` and `frozenset`?

| Set | Frozenset |
|---|---|
| Mutable | Immutable |
| Not hashable | Hashable |
| Cannot be a dictionary key | Can be a dictionary key |
| Supports `add()` | Does not support `add()` |
| Supports `remove()` | Does not support `remove()` |
| Supports set operations | Supports set operations |

---

# 46. Can a Set Be Used as a Dictionary Key?

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

Use a `frozenset` instead:

```python
data = {
    frozenset([1, 2]): "value"
}

print(data)
```

---

# 47. Can a Set Contain Another Set?

A normal set cannot contain a mutable set.

```python
data = {{1, 2}, {3, 4}}
```

This raises:

```text
TypeError: unhashable type: 'set'
```

Use `frozenset`:

```python
data = {
    frozenset([1, 2]),
    frozenset([3, 4])
}

print(data)
```

This works.

---

# 48. How Do You Remove Duplicates From a List Using a Set?

This is one of the most common practical interview questions.

```python
numbers = [1, 2, 2, 3, 3, 4]

unique_numbers = set(numbers)

print(unique_numbers)
```

Output contains:

```text
{1, 2, 3, 4}
```

### Important Interview Point

If the original order must be preserved, blindly converting to a set is not the right approach.

For example:

```python
numbers = [3, 1, 3, 2, 1]

unique_numbers = list(dict.fromkeys(numbers))

print(unique_numbers)
```

Output:

```text
[3, 1, 2]
```

This preserves first occurrence order.

### Interview Answer

> If order does not matter, I can use `set()` to remove duplicates. If order matters, I would use an order-preserving approach such as `dict.fromkeys()` or a loop with a seen set.

---

# 49. How Would You Find Common Elements Between Two Lists?

Convert them to sets and use intersection.

```python
a = [1, 2, 3, 4]
b = [3, 4, 5, 6]

common = set(a) & set(b)

print(common)
```

Output:

```text
{3, 4}
```

### Real-World Example

Suppose two systems provide lists of customer IDs:

```python
system_a = [101, 102, 103, 104]
system_b = [103, 104, 105]

common_customers = set(system_a) & set(system_b)

print(common_customers)
```

The intersection gives IDs present in both systems.

---

# 50. How Would You Find Elements Present in One List but Not Another?

Use set difference.

```python
a = [1, 2, 3, 4]
b = [3, 4, 5]

result = set(a) - set(b)

print(result)
```

Output:

```text
{1, 2}
```

---

# 51. How Would You Find Elements Unique to Both Lists?

Use symmetric difference.

```python
a = [1, 2, 3]
b = [3, 4, 5]

result = set(a) ^ set(b)

print(result)
```

Output:

```text
{1, 2, 4, 5}
```

---

# 52. How Do You Find the Number of Unique Elements?

Use `len()` on a set.

```python
numbers = [1, 2, 2, 3, 3, 4]

unique_count = len(set(numbers))

print(unique_count)
```

Output:

```text
4
```

---

# 53. How Do You Find Duplicate Values in a List?

One approach is to use a set.

```python
numbers = [1, 2, 2, 3, 3, 4, 5, 5]

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
{2, 3, 5}
```

### Interview Explanation

> I maintain a `seen` set. If an element is already in `seen`, I add it to a `duplicates` set. This gives average O(n) time because set membership is O(1) on average.

---

# 54. What Is the Time Complexity of Adding to a Set?

Average:

```text
O(1)
```

Worst case:

```text
O(n)
```

because set operations are hash-table based.

---

# 55. What Is the Time Complexity of Removing From a Set?

For normal hashable elements:

```text
Average: O(1)
Worst case: O(n)
```

---

# 56. What Is the Time Complexity of Set Union?

If the sets contain `n` and `m` elements, union is generally proportional to the total number of elements:

```text
O(n + m)
```

---

# 57. What Is the Time Complexity of Set Intersection?

The exact implementation details matter, but conceptually intersection is based on membership checks and is generally proportional to the size of the smaller set plus membership-test costs.

For interview purposes, a common answer is:

```text
O(min(n, m))
```

assuming average O(1) membership checks.

---

# 58. What Is the Difference Between `in` on a List and `in` on a Set?

### List

```python
value in my_list
```

Average/worst-case search is generally:

```text
O(n)
```

### Set

```python
value in my_set
```

Average:

```text
O(1)
```

### Interview Answer

> A list generally performs membership testing through sequential search, while a set uses hashing and therefore provides average O(1) membership testing.

---

# 59. What Happens When You Iterate Over a Set?

You can iterate through its elements:

```python
numbers = {10, 20, 30}

for number in numbers:
    print(number)
```

But you should not write code that depends on a particular positional order.

---

# 60. Can You Change a Set While Iterating Over It?

You should not structurally modify a set while directly iterating over it.

For example:

```python
numbers = {1, 2, 3, 4}

for number in numbers:
    numbers.remove(number)
```

This can raise:

```text
RuntimeError: Set changed size during iteration
```

A safe approach is to iterate over a copy:

```python
numbers = {1, 2, 3, 4}

for number in numbers.copy():
    if number % 2 == 0:
        numbers.remove(number)

print(numbers)
```

Output:

```text
{1, 3}
```

---

# 61. Can Set Operations Work With Other Iterables?

Some set methods accept iterable arguments.

For example:

```python
a = {1, 2, 3}

print(a.union([3, 4, 5]))
```

This works.

But set operators such as:

```python
a | [3, 4]
```

require set-like operands of the appropriate type rather than arbitrary iterables.

### Interview Tip

If you want to be safe and clear:

```python
a.union(set(b))
```

or use the appropriate set method.

---

# 62. What Happens With `set("hello")`?

Each character becomes an element and duplicates are removed.

```python
letters = set("hello")

print(letters)
```

The result contains:

```text
h
e
l
o
```

There are four unique characters.

### Important

Do not rely on the displayed order.

---

# 63. How Do You Find Unique Characters in a String?

Use a set.

```python
text = "programming"

unique_characters = set(text)

print(unique_characters)
```

This gives the unique characters.

To count them:

```python
print(len(set(text)))
```

---

# 64. How Can Sets Be Useful in Data Engineering?

Sets are useful for operations such as:

- Finding unique IDs
- Comparing datasets
- Checking whether values already exist
- Detecting duplicates
- Comparing records from two sources
- Finding missing values between datasets

### Example

Suppose two data sources contain customer IDs:

```python
source_a = {101, 102, 103, 104}
source_b = {103, 104, 105}

common_ids = source_a & source_b
only_in_a = source_a - source_b
only_in_b = source_b - source_a

print(common_ids)
print(only_in_a)
print(only_in_b)
```

Conceptually:

```text
Common IDs  -> 103, 104
Only in A   -> 101, 102
Only in B   -> 105
```

### Interview Answer

> In data processing, sets are useful for uniqueness and comparing collections. For example, I can use intersections to find IDs present in two datasets and differences to identify IDs missing from one source.

---

# 65. Set Comprehension

Python supports set comprehensions.

### Example

```python
numbers = {1, 2, 3, 4, 5}

squares = {number * number for number in numbers}

print(squares)
```

Output:

```text
{1, 4, 9, 16, 25}
```

### With Condition

```python
numbers = range(10)

even_numbers = {
    number
    for number in numbers
    if number % 2 == 0
}

print(even_numbers)
```

Output:

```text
{0, 2, 4, 6, 8}
```

---

# 66. Difference Between List, Set, Tuple, and Dictionary

| Feature | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Syntax | `[]` | `()` | `{}` | `{key: value}` |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: No |
| Indexing | Yes | Yes | No | By key |
| Main purpose | Ordered collection | Fixed collection | Unique elements | Key-value mapping |
| Hash-based | No | Can be hashable | Yes | Yes |
| Membership | O(n) typical | O(n) typical | O(1) average | O(1) average for keys |

### Interview Summary

> I use lists for mutable ordered collections, tuples for fixed ordered data, sets for unique elements and fast membership testing, and dictionaries for key-value relationships.

---

# 67. Common Set Interview Traps

## Trap 1 — Empty Set

```python
a = {}
```

This is a dictionary.

Correct:

```python
a = set()
```

---

## Trap 2 — Indexing

```python
a = {1, 2, 3}

print(a[0])
```

Invalid because sets do not support indexing.

---

## Trap 3 — Duplicates

```python
a = {1, 1, 2, 2, 3}

print(a)
```

Duplicates are removed.

---

## Trap 4 — List as Set Element

```python
a = {[1, 2]}
```

Invalid because lists are unhashable.

---

## Trap 5 — `remove()` vs `discard()`

```python
a.remove(10)
```

can raise `KeyError`.

```python
a.discard(10)
```

does not raise an error if `10` is absent.

---

## Trap 6 — `pop()`

```python
a.pop()
```

removes an arbitrary element.

Do not assume it removes the first or last element.

---

## Trap 7 — `add()` vs `update()`

```python
a.add("Python")
```

adds one element.

```python
a.update("Python")
```

adds individual characters.

---

## Trap 8 — `set()` on a String

```python
set("hello")
```

creates a set of unique characters, not one `"hello"` element.

---

# 68. Important Set Output Questions

## Question 1

```python
a = {1, 2, 2, 3, 3}

print(a)
```

### Answer

The set contains only unique values:

```text
{1, 2, 3}
```

Do not rely on a particular display order.

---

## Question 2

```python
a = {}
print(type(a))
```

### Answer

```text
<class 'dict'>
```

---

## Question 3

```python
a = set()
print(type(a))
```

### Answer

```text
<class 'set'>
```

---

## Question 4

```python
a = {1, 2, 3}

print(2 in a)
print(5 in a)
```

### Answer

```text
True
False
```

---

## Question 5

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a & b)
```

### Answer

```text
{3}
```

---

## Question 6

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)
```

### Answer

The result contains all unique elements:

```text
{1, 2, 3, 4, 5}
```

---

## Question 7

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a - b)
```

### Answer

```text
{1, 2}
```

---

## Question 8

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a ^ b)
```

### Answer

```text
{1, 2, 4, 5}
```

---

## Question 9

```python
a = {1, 2}

a.add(3)
a.add(3)

print(a)
```

### Answer

The value `3` appears only once.

```text
{1, 2, 3}
```

---

## Question 10

```python
a = {1, 2}

a.update([3, 4])

print(a)
```

### Answer

```text
{1, 2, 3, 4}
```

---

## Question 11

```python
a = {"Python", "SQL"}

a.update("AI")

print(a)
```

### Answer

`A` and `I` are added as separate elements.

Do not rely on the displayed order.

---

## Question 12

```python
a = {1, 2, 3}

a.discard(10)

print(a)
```

### Answer

No error occurs and the set remains unchanged:

```text
{1, 2, 3}
```

---

## Question 13

```python
a = {1, 2, 3}

a.remove(10)
```

### Answer

Raises:

```text
KeyError
```

---

## Question 14

```python
a = {1, 2, 3}

print(len(a))
```

### Answer

```text
3
```

---

## Question 15

```python
a = set("hello")

print(len(a))
```

### Answer

```text
4
```

The unique characters are:

```text
h, e, l, o
```

---

# 69. Important Set Interview Questions

1. What is a set in Python?
2. What are the main properties of a set?
3. Why does a set not allow duplicates?
4. How does hashing help sets?
5. How do you create a set?
6. How do you create an empty set?
7. Why does `{}` create a dictionary instead of a set?
8. Are sets ordered?
9. Can you access a set using an index?
10. Can you slice a set?
11. Why can't sets support indexing?
12. What is hashability?
13. Which objects can be elements of a set?
14. Can a list be a set element?
15. Can a tuple be a set element?
16. When is a tuple hashable?
17. What is membership testing?
18. What is the average complexity of set membership?
19. How do you add an element to a set?
20. What happens when you add a duplicate?
21. What is the difference between `add()` and `update()`?
22. What does `update()` accept?
23. What happens when `update()` receives a string?
24. What does `remove()` do?
25. What happens when `remove()` cannot find an element?
26. What is the difference between `remove()` and `discard()`?
27. What does `pop()` do on a set?
28. Can you specify an index to set `pop()`?
29. What does `clear()` do?
30. What is set union?
31. What is set intersection?
32. What is set difference?
33. Why is set difference directional?
34. What is symmetric difference?
35. What is the difference between difference and symmetric difference?
36. What operators represent set operations?
37. What is the difference between `union()` and `update()`?
38. What are in-place set operations?
39. What is a subset?
40. What is a proper subset?
41. What is a superset?
42. What is a proper superset?
43. What does `isdisjoint()` do?
44. What is a frozenset?
45. Why would you use a frozenset?
46. What is the difference between set and frozenset?
47. Can a set be used as a dictionary key?
48. Can a frozenset be used as a dictionary key?
49. Can a set contain another set?
50. How do you remove duplicates from a list?
51. How do you preserve order while removing duplicates?
52. How do you find common elements between two lists?
53. How do you find elements present in one list but not another?
54. How do you find unique elements across two lists?
55. How do you count unique values?
56. How do you find duplicate values using sets?
57. What is the time complexity of adding to a set?
58. What is the time complexity of removing from a set?
59. What is the complexity of set membership?
60. What is the complexity of union?
61. What is the complexity of intersection?
62. What is the difference between list membership and set membership?
63. Can you modify a set while iterating over it?
64. What is set comprehension?
65. How are sets useful in data engineering?
66. What are the differences between list, tuple, set, and dictionary?

---

# 70. Strong Interview Answer Pattern

### Question: Why would you use a set instead of a list?

A strong answer:

> "I would use a set when uniqueness and fast membership checking are important. For example, if I receive customer IDs from two data sources and want to find common IDs, I can convert them to sets and use intersection. Set membership is O(1) on average, whereas list membership is generally O(n). However, if I need duplicate values, indexing, or meaningful positional order, I would use a list instead."

### Question: How do you remove duplicates from a list?

> "If the order does not matter, I can simply use `set()`. If the original order needs to be preserved, I would use an order-preserving approach such as `dict.fromkeys()` or maintain a `seen` set while iterating."

### Question: Why can't a list be stored inside a set?

> "Set elements must be hashable. A list is mutable and therefore unhashable, so Python does not allow a list to be a set element. A tuple can be used if all of its elements are hashable."

---

# 71. Real-World Example — Comparing Two Data Sources

Suppose two systems provide customer IDs.

```python
crm_ids = {101, 102, 103, 104, 105}
billing_ids = {103, 104, 105, 106, 107}

common = crm_ids & billing_ids
missing_from_billing = crm_ids - billing_ids
new_in_billing = billing_ids - crm_ids

print("Common:", common)
print("Missing from billing:", missing_from_billing)
print("New in billing:", new_in_billing)
```

Conceptually:

```text
Common:
103, 104, 105

Missing from billing:
101, 102

New in billing:
106, 107
```

### Interview Explanation

> "This is a simple example of how sets can help compare two datasets. I can use intersection to find common records and difference to identify records that exist in one source but not the other."

This connects Python set knowledge to practical data engineering work.

---

# 72. Real-World Example — Duplicate Detection

Suppose a pipeline receives customer IDs:

```python
customer_ids = [
    101,
    102,
    103,
    102,
    104,
    101
]

seen = set()
duplicates = set()

for customer_id in customer_ids:
    if customer_id in seen:
        duplicates.add(customer_id)
    else:
        seen.add(customer_id)

print("Duplicates:", duplicates)
```

Result:

```text
Duplicates: {101, 102}
```

### Interview Explanation

> "I can use a set as a fast lookup structure while processing records. If an ID has already been seen, I know it is duplicated."

---

# 73. Set vs Dictionary — Important Interview Distinction

Both sets and dictionaries use hash-based structures, but their purposes are different.

### Set

Stores unique values:

```python
skills = {"Python", "SQL", "PySpark"}
```

### Dictionary

Stores key-value pairs:

```python
employee = {
    "name": "Harsha",
    "role": "Data Engineer"
}
```

### Interview Answer

> A set stores unique values, while a dictionary stores mappings between keys and values. Both provide efficient average-case key or membership lookup using hashing.

---

# 74. Quick Revision

## Set Properties

```text
Mutable
Unique elements
Hash-based
No positional indexing
No slicing
Elements must be hashable
Fast membership on average
Supports mathematical set operations
```

## Important Methods

```text
add()
update()
remove()
discard()
pop()
clear()

union()
intersection()
difference()
symmetric_difference()

intersection_update()
difference_update()
symmetric_difference_update()

issubset()
issuperset()
isdisjoint()
```

## Important Operators

```text
A | B    -> Union
A & B    -> Intersection
A - B    -> Difference
A ^ B    -> Symmetric Difference
A <= B   -> Subset
A < B    -> Proper Subset
A >= B   -> Superset
A > B    -> Proper Superset
```

## Important Concepts

```text
Hashability
Membership testing
Uniqueness
Set operations
Frozenset
Set comprehension
Duplicate detection
Dataset comparison
```

---

# 75. Final Placement Focus

For placement interviews, understand these concepts deeply:

1. **What a set is**
2. **Why sets contain only unique elements**
3. **Hashing and hashability**
4. **Why lists cannot be set elements**
5. **Why tuples can sometimes be set elements**
6. **Set vs list**
7. **Set vs tuple**
8. **Set vs dictionary**
9. **Empty set vs empty dictionary**
10. **Membership complexity**
11. **`add()` vs `update()`**
12. **`remove()` vs `discard()`**
13. **`pop()` behavior**
14. **Union**
15. **Intersection**
16. **Difference**
17. **Symmetric difference**
18. **Subset and superset**
19. **Frozenset**
20. **Removing duplicates**
21. **Finding duplicates**
22. **Comparing two datasets**
23. **Set comprehension**
24. **Set time complexity**
25. **Common output-based traps**

The most important thing is not memorizing every method. Be able to clearly explain **why sets are useful, how hashing provides efficient membership testing, why elements must be hashable, how set operations work, and when you would choose a set over a list or tuple in a real-world problem.**