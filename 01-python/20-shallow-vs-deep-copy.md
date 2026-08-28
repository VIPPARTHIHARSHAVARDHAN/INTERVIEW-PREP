# 20 — Shallow Copy vs Deep Copy

## 1. What Is Copying in Python?

Copying means creating another object based on an existing object.

For example:

```python
a = [1, 2, 3]

b = a
```

This does **not** create a new list.

Both variables refer to the same list:

```text
a ─────┐
       ↓
    [1, 2, 3]
       ↑
       └───── b
```

Therefore:

```python
b.append(4)

print(a)
print(b)
```

Output:

```text
[1, 2, 3, 4]
[1, 2, 3, 4]
```

This is an important distinction between **assignment** and **copying**.

---

# 2. Assignment vs Copy

## Assignment

```python
a = [1, 2, 3]
b = a
```

Here:

```python
a is b
```

is:

```text
True
```

Both variables point to the same object.

---

## Copy

```python
a = [1, 2, 3]
b = a.copy()
```

Now:

```python
a is b
```

is:

```text
False
```

They are separate list objects.

---

# 3. What Is a Shallow Copy?

A **shallow copy** creates a new outer object but does not recursively copy objects contained inside it.

For nested mutable objects, the inner objects are still shared.

Example:

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
```

Now:

```text
original ──→ [ ──→ [1, 2]
              └──→ [3, 4] ]

shallow  ──→ [ ──→ [1, 2]
              └──→ [3, 4] ]
```

The outer lists are different, but the inner lists are shared.

---

# 4. How to Create a Shallow Copy

Several common ways can create shallow copies.

### Using `copy.copy()`

```python
import copy

b = copy.copy(a)
```

### Using list slicing

```python
b = a[:]
```

### Using `list()`

```python
b = list(a)
```

### Using `.copy()`

```python
b = a.copy()
```

For a list, these create a shallow copy.

---

# 5. Basic Shallow Copy Example

```python
import copy

original = [1, 2, 3]

shallow = copy.copy(original)

shallow.append(4)

print(original)
print(shallow)
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

Because the list itself was copied, modifying the outer list does not affect the original.

---

# 6. Shallow Copy With Nested Lists

This is where shallow copying becomes important.

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)

shallow[0].append(100)

print(original)
print(shallow)
```

Output:

```text
[[1, 2, 100], [3, 4]]
[[1, 2, 100], [3, 4]]
```

Why?

Because:

```python
original[0]
```

and:

```python
shallow[0]
```

refer to the same inner list.

---

# 7. Visual Representation of Shallow Copy

```text
             ┌───────────────┐
original ───→│ outer list    │
             └───────┬───────┘
                     │
                     ↓
                  [inner list]
                     ↑
                     │
             ┌───────┴───────┐
shallow ────→│ outer list    │
             └───────────────┘
```

The important point is:

```text
Outer object → copied
Nested objects → shared
```

---

# 8. What Is a Deep Copy?

A **deep copy** creates a new outer object and recursively creates copies of nested objects as well.

Example:

```python
import copy

original = [[1, 2], [3, 4]]

deep = copy.deepcopy(original)
```

Conceptually:

```text
original ──→ [ ──→ [1, 2]
              └──→ [3, 4] ]

deep     ──→ [ ──→ [1, 2]
              └──→ [3, 4] ]
```

The inner lists are also separate objects.

---

# 9. Basic Deep Copy Example

```python
import copy

original = [[1, 2], [3, 4]]

deep = copy.deepcopy(original)

deep[0].append(100)

print(original)
print(deep)
```

Output:

```text
[[1, 2], [3, 4]]
[[1, 2, 100], [3, 4]]
```

The original is not affected because the nested list was also copied.

---

# 10. How to Create a Deep Copy

Use:

```python
import copy

deep_copy = copy.deepcopy(original)
```

The main difference is:

```python
copy.copy()
```

creates a shallow copy.

```python
copy.deepcopy()
```

creates a deep copy.

---

# 11. Shallow Copy vs Deep Copy

| Feature | Shallow Copy | Deep Copy |
|---|---|---|
| Creates new outer object | Yes | Yes |
| Copies nested objects recursively | No | Yes |
| Nested mutable objects shared | Usually yes | No |
| Function | `copy.copy()` | `copy.deepcopy()` |
| Usually faster | Yes | No |
| Uses more memory | Usually less | Usually more |

---

# 12. Most Important Interview Example

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

shallow[0].append(10)
deep[1].append(20)

print("Original:", original)
print("Shallow:", shallow)
print("Deep:", deep)
```

Output:

```text
Original: [[1, 2, 10], [3, 4]]
Shallow: [[1, 2, 10], [3, 4]]
Deep: [[1, 2], [3, 4, 20]]
```

The shallow copy shares the inner list with the original.

The deep copy has its own inner lists.

---

# 13. Why Does Shallow Copy Behave This Way?

Consider:

```python
original = [[1, 2], [3, 4]]

shallow = original.copy()
```

The outer list is copied.

But the elements inside the outer list are references to the existing inner lists.

Conceptually:

```text
original
   ↓
outer list
   ├──→ inner list A
   └──→ inner list B

shallow
   ↓
new outer list
   ├──→ inner list A
   └──→ inner list B
```

So:

```text
Outer list → different
Inner lists → same
```

---

# 14. Why Does Deep Copy Behave Differently?

With:

```python
deep = copy.deepcopy(original)
```

Python recursively copies the nested objects.

Conceptually:

```text
original
   ↓
outer list
   ├──→ inner list A
   └──→ inner list B

deep
   ↓
new outer list
   ├──→ new inner list A
   └──→ new inner list B
```

Therefore:

```text
Outer object → different
Nested objects → different
```

---

# 15. Checking Object Identity With `is`

The `is` operator checks whether two variables refer to the same object.

Example:

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

print(original is shallow)
print(original is deep)
```

Output:

```text
False
False
```

The outer objects are different.

---

# 16. Checking Inner Object Identity

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

print(original[0] is shallow[0])
print(original[0] is deep[0])
```

Output:

```text
True
False
```

This is one of the best examples to understand shallow vs deep copy.

---

# 17. `==` vs `is` in Copying

Consider:

```python
import copy

a = [[1, 2]]

b = copy.copy(a)
c = copy.deepcopy(a)
```

Then:

```python
print(a == b)
print(a == c)
```

Output:

```text
True
True
```

Because their contents are equal.

But:

```python
print(a is b)
print(a is c)
```

Output:

```text
False
False
```

Because they are different outer objects.

---

# 18. Important Interview Question — What Is the Difference Between `is` and `==`?

`==` checks **value/content equality**.

`is` checks **object identity**.

Example:

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

---

# 19. Shallow Copy of a List With Immutable Elements

Consider:

```python
import copy

original = [1, 2, 3]

shallow = copy.copy(original)

shallow[0] = 100

print(original)
print(shallow)
```

Output:

```text
[1, 2, 3]
[100, 2, 3]
```

There is no visible shared-mutation issue here because integers are immutable.

The important difference becomes visible when nested mutable objects are involved.

---

# 20. Mutable Objects and Shallow Copy

Common mutable objects include:

```text
list
dict
set
user-defined mutable objects
```

If a shallow copy contains references to mutable nested objects, modifications to those nested objects can affect the original.

Example:

```python
original = [[1, 2]]

shallow = original.copy()

shallow[0].append(3)

print(original)
```

Output:

```text
[[1, 2, 3]]
```

---

# 21. Immutable Objects and Copying

Common immutable objects include:

```text
int
float
str
tuple (when its contents are immutable)
bool
frozenset
```

You generally don't need a deep copy to protect an immutable object from mutation because it cannot be modified in place.

---

# 22. Important Point About Tuples

A tuple itself is immutable, but it can contain mutable objects.

Example:

```python
original = ([1, 2], [3, 4])
```

The tuple cannot be modified structurally:

```python
original[0] = [10, 20]
```

would raise an error.

But the inner list can be modified:

```python
original[0].append(5)
```

So when thinking about copying, always consider the mutability of the nested objects, not just the outer container.

---

# 23. Shallow Copy of a Dictionary

```python
import copy

original = {
    "name": "Harsha",
    "skills": ["Python", "SQL"]
}

shallow = copy.copy(original)

shallow["skills"].append("PySpark")

print(original)
print(shallow)
```

Output:

```text
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'PySpark']}
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'PySpark']}
```

The nested list is shared.

---

# 24. Deep Copy of a Dictionary

```python
import copy

original = {
    "name": "Harsha",
    "skills": ["Python", "SQL"]
}

deep = copy.deepcopy(original)

deep["skills"].append("PySpark")

print(original)
print(deep)
```

Output:

```text
{'name': 'Harsha', 'skills': ['Python', 'SQL']}
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'PySpark']}
```

The nested list is independently copied.

---

# 25. Common Ways to Create Shallow Copies

### List

```python
a = [1, 2, 3]

b = a.copy()
```

or:

```python
b = a[:]
```

or:

```python
b = list(a)
```

or:

```python
import copy

b = copy.copy(a)
```

### Dictionary

```python
b = a.copy()
```

or:

```python
b = dict(a)
```

or:

```python
import copy

b = copy.copy(a)
```

All of these are shallow-copy approaches.

---

# 26. Is `b = a` a Shallow Copy?

**No.**

This:

```python
b = a
```

is assignment.

It does not create another container object.

Example:

```python
a = [1, 2, 3]
b = a

print(a is b)
```

Output:

```text
True
```

For a shallow copy:

```python
b = a.copy()

print(a is b)
```

Output:

```text
False
```

---

# 27. Important Interview Question — What Is the Difference Between Assignment and Shallow Copy?

### Assignment

```python
b = a
```

Both names refer to the same object.

### Shallow copy

```python
b = copy.copy(a)
```

A new outer object is created, but nested objects can still be shared.

### Deep copy

```python
b = copy.deepcopy(a)
```

A new outer object and recursively copied nested objects are created.

---

# 28. Important Interview Question — Which Is Faster?

Generally:

```text
Shallow copy → faster
Deep copy → slower
```

because deep copy recursively copies nested objects.

However, the actual performance depends on the structure and contents of the object.

---

# 29. Important Interview Question — Which Uses More Memory?

Generally:

```text
Shallow copy → less additional memory
Deep copy → more additional memory
```

because deep copy creates additional copies of nested objects.

---

# 30. When Should We Use Shallow Copy?

Use a shallow copy when:

- you need a separate outer container
- nested objects can safely be shared
- you don't need independent nested mutable objects
- performance and memory efficiency matter

Example:

```python
original = [1, 2, 3]

copy_list = original.copy()
```

---

# 31. When Should We Use Deep Copy?

Use deep copy when:

- the object contains nested mutable objects
- the copied structure must be completely independent
- changes to nested objects should not affect the original

Example:

```python
import copy

configuration = {
    "database": {
        "host": "localhost",
        "port": 5432
    }
}

new_configuration = copy.deepcopy(configuration)
```

Now nested modifications are independent.

---

# 32. Real-World Example — Configuration

Suppose an application has a base configuration:

```python
base_config = {
    "database": {
        "host": "localhost",
        "port": 5432
    },
    "logging": {
        "level": "INFO"
    }
}
```

Suppose we need a separate configuration for testing.

A shallow copy:

```python
test_config = base_config.copy()
```

still shares the nested dictionaries.

A deep copy:

```python
import copy

test_config = copy.deepcopy(base_config)
```

allows us to modify the test configuration independently.

---

# 33. Real-World Example — Data Processing

Suppose a data-processing application maintains nested configuration or metadata:

```python
pipeline_config = {
    "source": {
        "type": "S3",
        "path": "raw/data"
    },
    "transform": {
        "format": "parquet"
    }
}
```

If a separate pipeline needs to modify nested configuration without affecting the original, a deep copy can be appropriate:

```python
import copy

new_config = copy.deepcopy(pipeline_config)

new_config["source"]["path"] = "test/data"
```

The original configuration remains unchanged.

---

# 34. Real-World Example — API Request Templates

Suppose we have:

```python
base_request = {
    "headers": {
        "Content-Type": "application/json"
    },
    "body": {
        "user": {
            "name": "Harsha"
        }
    }
}
```

If we create multiple independent request configurations, deep copying can prevent nested modifications from affecting the base template.

```python
import copy

request1 = copy.deepcopy(base_request)
request2 = copy.deepcopy(base_request)

request1["body"]["user"]["name"] = "A"

print(request2["body"]["user"]["name"])
```

Output:

```text
Harsha
```

---

# 35. How Does `copy.deepcopy()` Handle Recursive Objects?

A complex object can contain references back to itself.

Example:

```python
a = []
a.append(a)
```

Now:

```text
a → list
     ↓
     refers to itself
```

A naive recursive copy could continue forever.

Python's `deepcopy()` uses internal mechanisms to handle objects that have already been copied and can therefore handle recursive structures in many cases.

Example:

```python
import copy

a = []
a.append(a)

b = copy.deepcopy(a)

print(b is b[0])
```

Output:

```text
True
```

The recursive relationship is preserved in the copied structure.

---

# 36. What Is the `copy` Module?

Python provides the built-in:

```python
import copy
```

module for copying objects.

Important functions include:

```python
copy.copy()
copy.deepcopy()
```

Example:

```python
import copy

shallow = copy.copy(original)
deep = copy.deepcopy(original)
```

---

# 37. Does `deepcopy()` Always Create Completely New Objects?

Not necessarily every object in every situation.

Python's copying machinery handles objects according to their types and may reuse or specially handle objects that should not or cannot be meaningfully copied.

For normal interview examples involving nested lists and dictionaries, the practical rule is:

```text
shallow copy → nested references shared
deep copy → nested mutable structures copied recursively
```

---

# 38. Important Interview Question — Does Deep Copy Copy Immutable Objects?

Deep copying focuses on recursively copying objects where necessary.

Immutable objects such as integers and strings do not need an independent mutable copy.

For interview purposes, remember:

> Deep copy recursively copies nested objects when required, while immutable objects can safely be shared because they cannot be changed in place.

---

# 39. Common Mistake

Do not say:

> Shallow copy means only the reference is copied.

That description is incomplete.

Correct:

> A shallow copy creates a new outer object, but references to nested objects are copied rather than recursively creating new nested objects.

---

# 40. Common Mistake

Do not say:

> Deep copy means everything is always duplicated.

A better answer is:

> Deep copy recursively creates independent copies of nested objects when appropriate, while handling immutable and special objects according to Python's copying rules.

---

# 41. Common Interview Output Question

### Question

What is the output?

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.copy(a)

b[0].append(5)

print(a)
print(b)
```

### Answer

```text
[[1, 2, 5], [3, 4]]
[[1, 2, 5], [3, 4]]
```

### Why?

Because:

```python
a[0] is b[0]
```

is:

```text
True
```

---

# 42. Common Interview Output Question

### Question

What is the output?

```python
import copy

a = [[1, 2], [3, 4]]

b = copy.deepcopy(a)

b[0].append(5)

print(a)
print(b)
```

### Answer

```text
[[1, 2], [3, 4]]
[[1, 2, 5], [3, 4]]
```

Because the nested list was independently copied.

---

# 43. Common Interview Output Question

### Question

What is the output?

```python
a = [1, 2, 3]
b = a

b.append(4)

print(a)
```

### Answer

```text
[1, 2, 3, 4]
```

Because `a` and `b` refer to the same list.

---

# 44. Common Interview Output Question

### Question

What is the output?

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

Because `b` is a separate outer list.

---

# 45. Coding Interview Question — Demonstrate Shallow and Deep Copy

### Answer

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

shallow[0].append(10)
deep[1].append(20)

print("Original:", original)
print("Shallow:", shallow)
print("Deep:", deep)
```

Output:

```text
Original: [[1, 2, 10], [3, 4]]
Shallow: [[1, 2, 10], [3, 4]]
Deep: [[1, 2], [3, 4, 20]]
```

---

# 46. Coding Interview Question — Check Which Objects Are Shared

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
deep = copy.deepcopy(original)

print("Outer shallow:", original is shallow)
print("Inner shallow:", original[0] is shallow[0])

print("Outer deep:", original is deep)
print("Inner deep:", original[0] is deep[0])
```

Output:

```text
Outer shallow: False
Inner shallow: True
Outer deep: False
Inner deep: False
```

---

# 47. Interview Question — Is `list.copy()` Deep or Shallow?

### Answer

`list.copy()` creates a **shallow copy**.

Example:

```python
a = [[1, 2]]

b = a.copy()

print(a is b)
print(a[0] is b[0])
```

Output:

```text
False
True
```

---

# 48. Interview Question — Is Dictionary `.copy()` Deep or Shallow?

`dict.copy()` creates a **shallow copy**.

Example:

```python
a = {
    "skills": ["Python", "SQL"]
}

b = a.copy()

print(a is b)
print(a["skills"] is b["skills"])
```

Output:

```text
False
True
```

---

# 49. Interview Question — Is List Slicing a Deep Copy?

No.

List slicing creates a **shallow copy**.

```python
a = [[1, 2]]

b = a[:]

b[0].append(3)

print(a)
```

Output:

```text
[[1, 2, 3]]
```

The inner list is shared.

---

# 50. Interview Question — What Is the Simplest Way to Deep Copy a Nested List?

Use:

```python
import copy

b = copy.deepcopy(a)
```

Example:

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

# 51. Interview Question — Why Not Always Use Deep Copy?

Deep copy can be more expensive in terms of:

- execution time
- memory
- complexity

If nested objects do not need to be independent, a shallow copy is often sufficient.

### Strong Answer

> I would not use deep copy by default because it can recursively copy a large object graph and consume additional time and memory. I would choose it when independent nested mutable objects are actually required.

---

# 52. Interview Question — Can Shallow Copy Be Useful?

Yes.

For example:

```python
users = ["A", "B", "C"]

new_users = users.copy()

new_users.append("D")
```

If the list contains immutable values, a shallow copy is sufficient for independently modifying the outer list.

---

# 53. Interview Question — What Is the Main Difference in One Sentence?

### Best Short Answer

> A shallow copy creates a new outer object but shares nested object references, whereas a deep copy recursively creates independent copies of nested objects.

---

# 54. Interview Question — Explain With a Real Example

### Strong Interview Answer

> Suppose I have a nested configuration dictionary and I want to create another configuration from it. With a shallow copy, the outer dictionary is separate but nested dictionaries or lists can still be shared, so modifying them can affect the original. With a deep copy, the nested structure is recursively copied, so I can modify the new configuration independently.

---

# 55. Interview Question — What Would You Choose in a Real Project?

The answer depends on the requirement.

### If only the outer container needs to be independent:

```python
copy.copy()
```

or:

```python
list.copy()
```

### If nested mutable objects must also be independent:

```python
copy.deepcopy()
```

The important point is not to blindly choose deep copy; choose based on whether nested state needs to be isolated.

---

# 56. Quick Comparison Example

```python
import copy

original = {
    "name": "Harsha",
    "skills": ["Python", "SQL"]
}

shallow = copy.copy(original)
deep = copy.deepcopy(original)

shallow["skills"].append("AWS")
deep["skills"].append("PySpark")

print(original)
print(shallow)
print(deep)
```

Output:

```text
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'AWS']}
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'AWS']}
{'name': 'Harsha', 'skills': ['Python', 'SQL', 'PySpark']}
```

This example clearly demonstrates the difference.

---

# 57. Interview Revision Cheat Sheet

```text
b = a
    ↓
Assignment
Same object

b = copy.copy(a)
    ↓
Shallow copy
New outer object
Nested references can be shared

b = copy.deepcopy(a)
    ↓
Deep copy
New outer object
Nested objects recursively copied
```

Remember:

```text
Assignment:
same object

Shallow:
new outer + shared nested references

Deep:
new outer + independent nested structure
```

---

# 58. Must-Know Interview Questions

1. What is copying in Python?
2. What is the difference between assignment and copying?
3. What is a shallow copy?
4. What is a deep copy?
5. How do you create a shallow copy?
6. How do you create a deep copy?
7. What is the difference between `copy.copy()` and `copy.deepcopy()`?
8. Is `list.copy()` shallow or deep?
9. Is `dict.copy()` shallow or deep?
10. Is list slicing a shallow or deep copy?
11. Why does modifying a nested list affect the original after a shallow copy?
12. Why does deep copy avoid this problem?
13. What is the difference between `is` and `==`?
14. What happens with `b = a`?
15. Which is faster, shallow copy or deep copy?
16. Which uses more memory?
17. When should you use shallow copy?
18. When should you use deep copy?
19. What happens when immutable objects are involved?
20. Can a tuple contain mutable objects?
21. How does shallow copying work with dictionaries?
22. How does deep copying work with dictionaries?
23. Can `deepcopy()` handle recursive objects?
24. Why shouldn't we always use deep copy?
25. Write code demonstrating shallow vs deep copy.
26. Predict the output of a shallow-copy program.
27. Predict the output of a deep-copy program.
28. How can you check whether nested objects are shared?
29. What does `original[0] is copied[0]` tell you?
30. Explain shallow vs deep copy using a real-world example.

---

# 59. Final Interview Answer

> In Python, a shallow copy creates a new outer object but keeps references to the nested objects, so nested mutable objects can still be shared between the original and the copy. A deep copy creates a new outer object and recursively copies nested objects, making the copied structure independent. Python provides `copy.copy()` for shallow copying and `copy.deepcopy()` for deep copying. I would use shallow copy when sharing nested objects is acceptable and deep copy when I need complete independence of nested mutable state.