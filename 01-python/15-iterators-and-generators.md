# Python Iterators and Generators — Interview Preparation

# 1. What Are Iterators and Generators?

Iterators and generators are important Python concepts used to process data **one item at a time**.

They are especially useful when:

- working with large datasets
- processing files
- handling streams of data
- avoiding unnecessary memory usage
- building pipelines of operations

The main ideas to understand are:

```text
Iterable
   ↓
Iterator
   ↓
__iter__()
   ↓
__next__()
   ↓
One value at a time
```

Generators provide a simpler way to create iterators using the `yield` keyword.

---

# 2. What Is an Iterable?

An **iterable** is an object that can be iterated over.

Common examples:

```python
list
tuple
string
set
dictionary
range
```

Example:

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Output:

```text
10
20
30
```

A `for` loop can iterate over the list because a list is iterable.

---

# 3. What Is an Iterator?

An **iterator** is an object that produces values one at a time when requested.

An iterator implements:

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

---

# 4. Iterable vs Iterator

This is one of the most important interview questions.

### Iterable

An iterable is an object from which we can obtain an iterator.

Example:

```python
numbers = [10, 20, 30]

iterator = iter(numbers)
```

### Iterator

The iterator is the object that actually keeps track of the current position and provides the next value.

```python
iterator = iter(numbers)

print(next(iterator))
```

### Strong Interview Answer

> An iterable is an object that can be iterated over and can provide an iterator. An iterator is an object that produces values one at a time using `__next__()` and maintains its iteration state.

---

# 5. Is Every Iterable an Iterator?

No.

For example:

```python
numbers = [1, 2, 3]
```

A list is iterable, but it is not itself an iterator.

We can create an iterator from it:

```python
iterator = iter(numbers)
```

Now:

```python
print(next(iterator))
```

works.

But:

```python
print(next(numbers))
```

raises an error because the list itself is not an iterator.

---

# 6. What Does `iter()` Do?

The built-in `iter()` function obtains an iterator from an iterable.

Example:

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(iterator)
```

Now the iterator can be consumed using `next()`:

```python
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

---

# 7. What Does `next()` Do?

`next()` retrieves the next item from an iterator.

Example:

```python
numbers = [10, 20, 30]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
```

Output:

```text
10
20
```

The iterator remembers its current position.

The next call continues from where it stopped.

```python
print(next(iterator))
```

Output:

```text
30
```

---

# 8. What Happens When the Iterator Is Exhausted?

When there are no more values, `next()` raises:

```python
StopIteration
```

Example:

```python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
print(next(iterator))
```

The third `next()` raises:

```text
StopIteration
```

This exception tells Python that the iterator has no more values.

---

# 9. Why Doesn't a `for` Loop Usually Show `StopIteration`?

A `for` loop internally handles `StopIteration`.

Conceptually:

```python
for value in iterable:
    print(value)
```

works roughly like:

```python
iterator = iter(iterable)

while True:
    try:
        value = next(iterator)
        print(value)
    except StopIteration:
        break
```

This is a simplified conceptual explanation of how iteration works.

---

# 10. How Does a `for` Loop Work Internally?

Consider:

```python
numbers = [1, 2, 3]

for number in numbers:
    print(number)
```

Conceptually:

```python
iterator = iter(numbers)

while True:
    try:
        number = next(iterator)
        print(number)
    except StopIteration:
        break
```

Important flow:

```text
Iterable
   ↓
iter()
   ↓
Iterator
   ↓
next()
   ↓
value
   ↓
next()
   ↓
value
   ↓
StopIteration
   ↓
loop ends
```

---

# 11. What Is the Iterator Protocol?

Python's iterator protocol is mainly based on two methods:

```python
__iter__()
__next__()
```

### `__iter__()`

Returns an iterator.

### `__next__()`

Returns the next value.

When there are no more values:

```python
StopIteration
```

is raised.

---

# 12. How Do You Create a Custom Iterator?

We can create a class that implements `__iter__()` and `__next__()`.

Example:

```python
class CountUp:
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


counter = CountUp(3)

for value in counter:
    print(value)
```

Output:

```text
1
2
3
```

---

# 13. How Does the Custom Iterator Work?

Initially:

```python
self.current = 1
```

For each `next()` call:

```text
current = 1 → return 1
current = 2 → return 2
current = 3 → return 3
current = 4 → StopIteration
```

The iterator maintains its state through:

```python
self.current
```

---

# 14. Why Does `__iter__()` Return `self` in a Custom Iterator?

For an iterator object, `__iter__()` normally returns itself.

Example:

```python
def __iter__(self):
    return self
```

This is because the object itself is the iterator.

### Interview Answer

> An iterator implements both `__iter__()` and `__next__()`. Since the object itself represents the iterator, its `__iter__()` method returns `self`.

---

# 15. Iterable and Iterator Example

```python
numbers = [1, 2, 3]

print(hasattr(numbers, "__iter__"))
print(hasattr(numbers, "__next__"))
```

Conceptually:

```text
True
False
```

Now:

```python
iterator = iter(numbers)

print(hasattr(iterator, "__iter__"))
print(hasattr(iterator, "__next__"))
```

Conceptually:

```text
True
True
```

This is a useful way to demonstrate the difference.

---

# 16. What Is a Generator?

A **generator** is a convenient way to create an iterator.

Generators use the:

```python
yield
```

keyword.

Example:

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

---

# 17. What Does `yield` Do?

`yield` produces a value from a generator and pauses its execution.

Example:

```python
def numbers():
    yield 1
    yield 2
    yield 3
```

When the generator is iterated:

```text
yield 1
pause
resume
yield 2
pause
resume
yield 3
pause
finish
```

The function does not execute completely at once.

---

# 18. `return` vs `yield`

This is an important interview question.

### `return`

```python
def example():
    return 10
```

The function returns and finishes immediately.

### `yield`

```python
def example():
    yield 10
```

The function becomes a generator and can pause and resume.

### Strong Interview Answer

> `return` terminates a function and gives back a final result, while `yield` produces a value from a generator and pauses its execution so it can resume later.

---

# 19. What Happens When a Function Contains `yield`?

Example:

```python
def test():
    yield 10
```

Calling:

```python
result = test()
```

does not immediately execute the body in the same way as a normal function call.

Instead, it returns a generator object.

```python
print(type(result))
```

Output is conceptually:

```text
<class 'generator'>
```

The generator begins producing values when requested.

---

# 20. Calling `next()` on a Generator

```python
def numbers():
    yield 10
    yield 20
    yield 30


gen = numbers()

print(next(gen))
print(next(gen))
print(next(gen))
```

Output:

```text
10
20
30
```

The fourth call:

```python
next(gen)
```

raises:

```text
StopIteration
```

---

# 21. Generator Execution Flow

Consider:

```python
def numbers():
    print("Start")
    yield 10
    print("Middle")
    yield 20
    print("End")
```

Now:

```python
gen = numbers()
```

The generator is created.

Then:

```python
print(next(gen))
```

Output:

```text
Start
10
```

Next:

```python
print(next(gen))
```

Output:

```text
Middle
20
```

Next:

```python
next(gen)
```

Output:

```text
End
```

and then the generator finishes.

The important idea is that execution resumes from the point where it previously paused.

---

# 22. Why Are Generators Memory Efficient?

Consider:

```python
numbers = [x for x in range(1000000)]
```

This creates a large list in memory.

A generator:

```python
numbers = (x for x in range(1000000))
```

produces values lazily.

It does not need to materialize all one million values at once.

### Strong Interview Answer

> Generators are memory-efficient because they produce values lazily, one at a time, instead of creating the complete collection in memory.

---

# 23. List vs Generator

### List

```python
numbers = [x for x in range(10)]
```

The values are stored in the list.

### Generator

```python
numbers = (x for x in range(10))
```

The values are generated when requested.

### Comparison

| Feature | List | Generator |
|---|---|---|
| Evaluation | Immediate | Lazy |
| Memory | Stores values | Produces values as needed |
| Indexing | Supported | Not directly supported |
| Reusable | Yes | Usually one-time consumption |
| Large data | Can use more memory | More memory-efficient |
| Creation | List comprehension | Generator expression / function |

---

# 24. Generator Function vs Generator Expression

### Generator function

Uses `yield`:

```python
def numbers():
    for x in range(5):
        yield x
```

### Generator expression

Uses parentheses:

```python
numbers = (x for x in range(5))
```

Both produce generators.

---

# 25. Generator Function Example

```python
def squares(n):
    for x in range(1, n + 1):
        yield x * x


gen = squares(5)

for value in gen:
    print(value)
```

Output:

```text
1
4
9
16
25
```

---

# 26. Generator Expression Example

```python
numbers = range(1, 6)

squares = (x * x for x in numbers)

for value in squares:
    print(value)
```

Output:

```text
1
4
9
16
25
```

---

# 27. Generator vs Iterator

A generator is a convenient way of creating an iterator.

### Custom iterator

You may need:

```python
class MyIterator:
    def __iter__(self):
        return self

    def __next__(self):
        ...
```

### Generator

You can often write:

```python
def my_generator():
    yield ...
```

### Strong Interview Answer

> A generator is a special type of iterator that can be created using a generator function or generator expression. Generators automatically handle much of the iterator machinery, so we usually don't need to manually implement `__iter__()` and `__next__()`.

---

# 28. Is a Generator an Iterator?

Yes.

A generator object follows the iterator protocol.

Example:

```python
def numbers():
    yield 1
    yield 2


gen = numbers()

print(iter(gen) is gen)
```

Output:

```text
True
```

This demonstrates that the generator itself is an iterator.

---

# 29. Is a List an Iterator?

No.

A list is iterable but is not itself an iterator.

```python
numbers = [1, 2, 3]

# This works:
iterator = iter(numbers)

# This does not:
# next(numbers)
```

---

# 30. Can We Iterate Over a Generator More Than Once?

Usually, no.

Generators are generally **single-use iterators**.

Example:

```python
def numbers():
    yield 1
    yield 2
    yield 3


gen = numbers()

print(list(gen))
print(list(gen))
```

Output:

```text
[1, 2, 3]
[]
```

After the first iteration, the generator is exhausted.

If we need to iterate again, create a new generator.

```python
gen = numbers()
```

---

# 31. Can a List Be Iterated Multiple Times?

Yes.

```python
numbers = [1, 2, 3]

print(list(numbers))
print(list(numbers))
```

Both produce:

```text
[1, 2, 3]
```

This is an important difference between reusable iterables such as lists and one-shot iterators such as generators.

---

# 32. What Is Lazy Evaluation?

Lazy evaluation means that a value is calculated only when it is needed.

Generator example:

```python
def numbers():
    for i in range(5):
        print("Generating", i)
        yield i


gen = numbers()
```

At this point, values have not all been generated.

When we call:

```python
print(next(gen))
```

the generator produces the next value.

---

# 33. Real-World Example — Reading a Large File

Suppose a file contains millions of lines.

A normal approach might load everything:

```python
with open("large_file.txt") as file:
    data = file.readlines()
```

This can require significant memory.

A better approach is to process lines one at a time:

```python
with open("large_file.txt") as file:
    for line in file:
        process(line)
```

File objects are iterable and support iteration over lines.

This is a practical example of Python's iterator model.

---

# 34. Real-World Example — Generator for Large Data

```python
def read_records(records):
    for record in records:
        if record["active"]:
            yield record
```

Usage:

```python
records = [
    {"name": "Harsha", "active": True},
    {"name": "Ravi", "active": False},
    {"name": "Anu", "active": True}
]

active_records = read_records(records)

for record in active_records:
    print(record)
```

Output:

```text
{'name': 'Harsha', 'active': True}
{'name': 'Anu', 'active': True}
```

The generator yields records one at a time.

---

# 35. Real-World Example — Data Engineering Pipeline

Generators can be useful when processing data in stages.

Conceptually:

```text
Raw Data
   ↓
Read records
   ↓
Filter records
   ↓
Transform records
   ↓
Write records
```

Example:

```python
def filter_valid(records):
    for record in records:
        if record["valid"]:
            yield record


def transform(records):
    for record in records:
        record["name"] = record["name"].upper()
        yield record


records = [
    {"name": "harsha", "valid": True},
    {"name": "ravi", "valid": False},
    {"name": "anu", "valid": True}
]

pipeline = transform(filter_valid(records))

for record in pipeline:
    print(record)
```

Output:

```text
{'name': 'HARSHA', 'valid': True}
{'name': 'ANU', 'valid': True}
```

The stages can process data progressively instead of requiring every intermediate result to be stored as a separate list.

---

# 36. Real-World Example — Infinite Generator

Generators can represent sequences that conceptually never end.

```python
def counter():
    number = 1

    while True:
        yield number
        number += 1
```

Usage:

```python
gen = counter()

print(next(gen))
print(next(gen))
print(next(gen))
```

Output:

```text
1
2
3
```

The generator can continue producing values indefinitely.

---

# 37. How Do You Stop an Infinite Generator?

Use a condition in the consumer.

Example:

```python
def counter():
    number = 1

    while True:
        yield number
        number += 1


gen = counter()

for value in gen:
    if value > 5:
        break
    print(value)
```

Output:

```text
1
2
3
4
5
```

---

# 38. Generator With `send()`

Generators can also receive values using:

```python
send()
```

Example:

```python
def receiver():
    while True:
        value = yield
        print("Received:", value)


gen = receiver()

next(gen)

gen.send(10)
gen.send(20)
```

Output:

```text
Received: 10
Received: 20
```

`next(gen)` initially advances the generator to the `yield` expression so that it is ready to receive a value.

This is an advanced generator feature.

---

# 39. What Does `yield` Return?

When a generator pauses at:

```python
value = yield
```

a value can be sent into the generator using:

```python
generator.send(value)
```

Example:

```python
def receiver():
    value = yield
    print(value)


gen = receiver()

next(gen)
gen.send(100)
```

Output:

```text
100
```

---

# 40. Can a Generator Have `return`?

Yes.

Example:

```python
def numbers():
    yield 1
    yield 2
    return "Finished"
```

The `return` value becomes part of the `StopIteration` exception when the generator finishes.

Normally, a `for` loop does not expose this return value.

---

# 41. What Happens When a Generator Returns?

Example:

```python
def test():
    yield 1
    return "Done"


gen = test()

print(next(gen))

try:
    next(gen)
except StopIteration as e:
    print(e.value)
```

Output:

```text
1
Done
```

The generator's `return` value is stored in the `StopIteration` exception.

---

# 42. What Is `yield from`?

`yield from` allows one generator to delegate iteration to another iterable or generator.

Example:

```python
def numbers():
    yield from [1, 2, 3]


for value in numbers():
    print(value)
```

Output:

```text
1
2
3
```

It is useful for composing generators.

---

# 43. `yield from` With Another Generator

```python
def first():
    yield 1
    yield 2


def second():
    yield 3
    yield 4


def combined():
    yield from first()
    yield from second()


for value in combined():
    print(value)
```

Output:

```text
1
2
3
4
```

---

# 44. Why Is `yield from` Useful?

It makes generator composition easier.

Instead of:

```python
def combined():
    for value in first():
        yield value

    for value in second():
        yield value
```

we can write:

```python
def combined():
    yield from first()
    yield from second()
```

This is especially useful when building generator pipelines.

---

# 45. What Is Generator State?

A generator remembers where it stopped.

Example:

```python
def numbers():
    yield 10
    yield 20
    yield 30
```

After:

```python
gen = numbers()

next(gen)
```

the generator pauses after yielding `10`.

The next:

```python
next(gen)
```

continues from where it stopped and yields `20`.

This preserved execution state is one of the most important properties of generators.

---

# 46. Does a Generator Execute Immediately?

No.

Consider:

```python
def test():
    print("Hello")
    yield 10


gen = test()
```

At this point, `"Hello"` has not been printed.

When:

```python
next(gen)
```

is called, execution starts and prints:

```text
Hello
```

followed by:

```text
10
```

---

# 47. Important Output Question

```python
def test():
    print("A")
    yield 1
    print("B")
    yield 2


gen = test()

print("C")
print(next(gen))
print("D")
print(next(gen))
```

Output:

```text
C
A
1
D
B
2
```

### Why?

Generator execution starts only when `next()` is called.

---

# 48. Important Output Question

```python
def numbers():
    yield 1
    yield 2
    yield 3


gen = numbers()

print(next(gen))
print(next(gen))
```

Output:

```text
1
2
```

The generator is paused at the second `yield`.

---

# 49. Important Output Question

```python
def numbers():
    yield 1
    yield 2


gen = numbers()

print(list(gen))
print(list(gen))
```

Output:

```text
[1, 2]
[]
```

The generator is exhausted after the first conversion to a list.

---

# 50. Important Output Question

```python
numbers = [1, 2, 3]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))
```

Output:

```text
1
2
```

The iterator remembers its position.

---

# 51. Important Output Question — `iter()` and `next()`

```python
numbers = [10, 20]

iterator = iter(numbers)

print(next(iterator))
print(next(iterator))

try:
    print(next(iterator))
except StopIteration:
    print("Finished")
```

Output:

```text
10
20
Finished
```

---

# 52. Important Interview Question — Why Are Generators Useful for Large Data?

Strong answer:

> Generators are useful for large datasets because they use lazy evaluation. Instead of creating and storing the complete result in memory, they produce one value at a time. This can significantly reduce memory usage when the complete dataset does not need to be stored at once.

---

# 53. Important Interview Question — Where Would You Use Generators in Real Projects?

Good examples include:

- reading large files
- processing large datasets
- streaming records
- data transformation pipelines
- pagination
- generating sequences
- processing logs
- handling large API responses incrementally

### Strong Interview Answer

> I would use generators when data can be processed incrementally. For example, while processing a large file or dataset, I can yield one record at a time, transform it, and send it to the next stage without storing the entire intermediate result in memory.

---

# 54. Important Interview Question — What Is the Difference Between `iter()` and `next()`?

### `iter()`

Gets an iterator from an iterable.

```python
iterator = iter(numbers)
```

### `next()`

Gets the next value from an iterator.

```python
value = next(iterator)
```

### Short Answer

> `iter()` obtains an iterator, while `next()` retrieves the next item from that iterator.

---

# 55. Important Interview Question — What Is `StopIteration`?

`StopIteration` is an exception used by the iterator protocol to indicate that there are no more values.

Example:

```python
iterator = iter([1])

print(next(iterator))

try:
    print(next(iterator))
except StopIteration:
    print("No more values")
```

Output:

```text
1
No more values
```

A `for` loop automatically handles this internally.

---

# 56. Important Interview Question — Why Does a Generator Save Memory?

A generator does not need to store every generated result.

Example:

```python
def numbers():
    for i in range(1000000):
        yield i
```

The generator produces:

```text
0
1
2
3
...
```

as requested.

It does not create a million-element result list.

---

# 57. Important Interview Question — Is `range()` a Generator?

No.

`range` is an iterable sequence type, not a generator.

Example:

```python
numbers = range(5)

print(type(numbers))
```

It is a `range` object.

It supports iteration and is memory-efficient because it represents the range compactly, but it is not itself a generator.

---

# 58. Important Interview Question — Is a String an Iterator?

A string is iterable but is not itself an iterator.

```python
text = "ABC"
```

You can do:

```python
iterator = iter(text)

print(next(iterator))
```

Output:

```text
A
```

But:

```python
next(text)
```

does not work because the string itself is not an iterator.

---

# 59. Important Interview Question — Is a Dictionary Iterable?

Yes.

Iterating directly over a dictionary produces its keys.

```python
data = {
    "name": "Harsha",
    "age": 21
}

for key in data:
    print(key)
```

Output:

```text
name
age
```

The dictionary is iterable.

---

# 60. Important Interview Question — How Do You Iterate Over Dictionary Values?

```python
data = {
    "name": "Harsha",
    "age": 21
}

for value in data.values():
    print(value)
```

Output:

```text
Harsha
21
```

For key-value pairs:

```python
for key, value in data.items():
    print(key, value)
```

---

# 61. Iterator vs Generator vs Iterable

| Concept | Meaning |
|---|---|
| Iterable | Object that can provide an iterator |
| Iterator | Object that provides values using `next()` |
| Generator | Convenient iterator created using `yield` or generator expression |

Example:

```text
list
 ↓
iter(list)
 ↓
iterator
 ↓
next()
 ↓
value
```

Generator:

```text
generator function
       ↓
      yield
       ↓
generator object
       ↓
     next()
       ↓
     value
```

---

# 62. Important Interview Question — What Is the Difference Between an Iterable and an Iterator?

Strong answer:

> An iterable is an object that can return an iterator, usually through `iter()`. An iterator is the object that maintains iteration state and returns the next value through `next()`. For example, a list is iterable, while `iter(list)` returns an iterator.

---

# 63. Important Interview Question — What Is the Difference Between an Iterator and a Generator?

Strong answer:

> An iterator is any object that follows Python's iterator protocol by implementing `__iter__()` and `__next__()`. A generator is a convenient kind of iterator created using `yield` or a generator expression. Generators automatically maintain their execution state, so they are usually simpler to write.

---

# 64. Important Interview Question — Which One Is More Memory Efficient?

For equivalent processing:

```text
Generator → generally more memory-efficient
List → stores the complete result
```

But the correct answer depends on what the application needs.

If random access and repeated iteration are required, a list may be more appropriate.

If values can be processed sequentially, a generator can be better.

---

# 65. Important Interview Question — Can an Iterator Be Reused?

It depends on the iterator.

Most iterators are consumed as they are advanced.

Example:

```python
iterator = iter([1, 2, 3])

print(list(iterator))
print(list(iterator))
```

Output:

```text
[1, 2, 3]
[]
```

Once consumed, the iterator has no values left.

---

# 66. Important Interview Question — Why Does `list(iterator)` Consume the Iterator?

`list()` iterates through the iterator until it is exhausted.

Example:

```python
iterator = iter([1, 2, 3])

result = list(iterator)
```

The iterator is advanced through:

```text
1
2
3
StopIteration
```

Therefore, there are no remaining values for a second iteration.

---

# 67. Important Interview Question — Can We Use `for` on an Iterator?

Yes.

```python
iterator = iter([1, 2, 3])

for value in iterator:
    print(value)
```

Output:

```text
1
2
3
```

The `for` loop consumes the iterator.

---

# 68. Important Interview Question — Can We Use `for` on a Generator?

Yes.

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

---

# 69. Important Interview Question — What Happens to the Generator After a `for` Loop?

It becomes exhausted.

```python
def numbers():
    yield 1
    yield 2


gen = numbers()

for value in gen:
    print(value)

print(list(gen))
```

Output:

```text
1
2
[]
```

---

# 70. Important Interview Question — Why Would You Choose a Generator Over a List?

A good answer:

> I would choose a generator when I only need sequential access to the results and especially when the dataset may be large. It allows lazy processing and reduces memory usage. I would choose a list when I need random access, repeated iteration, or the complete result available immediately.

---

# 71. Common Interview Mistakes

### Mistake 1

Calling a list an iterator.

Incorrect:

> A list is an iterator.

Correct:

> A list is iterable, but it is not an iterator.

### Mistake 2

Saying `yield` returns all values.

Incorrect:

> `yield` returns the complete collection.

Correct:

> `yield` produces one value and pauses the generator.

### Mistake 3

Saying generators always make programs faster.

Generators primarily provide:

```text
lazy evaluation
memory efficiency
incremental processing
```

They do not automatically make every program faster.

### Mistake 4

Assuming generators can always be restarted.

A generator is normally consumed once.

---

# 72. Common Coding Question — Create a Generator for Even Numbers

```python
def even_numbers(n):
    for number in range(1, n + 1):
        if number % 2 == 0:
            yield number


for value in even_numbers(10):
    print(value)
```

Output:

```text
2
4
6
8
10
```

---

# 73. Common Coding Question — Create a Generator for Squares

```python
def squares(n):
    for number in range(1, n + 1):
        yield number * number


for value in squares(5):
    print(value)
```

Output:

```text
1
4
9
16
25
```

---

# 74. Common Coding Question — Create a Generator for Fibonacci Numbers

```python
def fibonacci(n):
    a = 0
    b = 1

    for _ in range(n):
        yield a
        a, b = b, a + b


for value in fibonacci(10):
    print(value)
```

Output:

```text
0
1
1
2
3
5
8
13
21
34
```

---

# 75. Common Coding Question — Create an Infinite Counter

```python
def counter():
    number = 1

    while True:
        yield number
        number += 1


gen = counter()

for _ in range(5):
    print(next(gen))
```

Output:

```text
1
2
3
4
5
```

---

# 76. Common Coding Question — Generator to Read Lines

```python
def read_lines(filename):
    with open(filename, "r") as file:
        for line in file:
            yield line.strip()
```

Usage:

```python
for line in read_lines("data.txt"):
    print(line)
```

This processes one line at a time.

---

# 77. Common Coding Question — Generator Pipeline

```python
def numbers():
    for number in range(1, 11):
        yield number


def even_numbers(numbers):
    for number in numbers:
        if number % 2 == 0:
            yield number


def squares(numbers):
    for number in numbers:
        yield number * number


pipeline = squares(even_numbers(numbers()))

for value in pipeline:
    print(value)
```

Output:

```text
4
16
36
64
100
```

This demonstrates how generators can be chained into a processing pipeline.

---

# 78. Generator Pipeline Concept

The previous example works like:

```text
numbers()
    ↓
1 2 3 4 5 6 7 8 9 10
    ↓
even_numbers()
    ↓
2 4 6 8 10
    ↓
squares()
    ↓
4 16 36 64 100
```

The data can flow through the pipeline incrementally.

This pattern is particularly useful in data processing.

---

# 79. Important Interview Question — Are Generators Suitable for Data Engineering?

Yes, especially for certain processing patterns.

A strong answer:

> Generators can be useful in data engineering when records can be processed incrementally. For example, a generator can read records from a large file or source, yield one record at a time, and pass those records through filtering and transformation stages without creating large intermediate lists in memory.

However, generators are not a replacement for distributed processing frameworks such as Spark when the dataset and computation require distributed execution.

---

# 80. Important Interview Question — Generator vs PySpark?

These concepts solve different problems.

### Python generator

Useful for:

```text
single-process
incremental processing
lazy evaluation
memory-efficient iteration
```

### PySpark

Designed for:

```text
distributed processing
large-scale datasets
parallel computation
cluster execution
```

### Strong Interview Answer

> A Python generator is mainly a language-level mechanism for lazy, sequential iteration within a Python process. PySpark is a distributed data-processing framework designed to process large datasets across multiple machines. A generator can help with memory-efficient local processing, while PySpark is appropriate when distributed computation is required.

---

# 81. Important Interview Question — Why Not Always Use Generators?

Generators have trade-offs.

They are not ideal when:

- you need random access
- you need repeated iteration
- you need the complete result immediately
- you need to inspect previous elements frequently

Example:

```python
numbers = [10, 20, 30]

print(numbers[1])
```

A list supports indexing.

A generator does not provide direct indexing like:

```python
generator[1]
```

---

# 82. Important Interview Question — What Happens If We Call `next()` After a Generator Is Exhausted?

Example:

```python
def numbers():
    yield 1


gen = numbers()

print(next(gen))

try:
    print(next(gen))
except StopIteration:
    print("Generator exhausted")
```

Output:

```text
1
Generator exhausted
```

Once exhausted, the generator does not restart automatically.

---

# 83. Important Interview Question — Can `iter()` Be Called on an Iterator?

Yes.

For an iterator:

```python
iterator = iter([1, 2, 3])

print(iter(iterator) is iterator)
```

Output:

```text
True
```

An iterator's `__iter__()` returns itself.

---

# 84. Important Interview Question — What Is the Relationship Between `for`, `iter()`, and `next()`?

A `for` loop obtains an iterator from the iterable and repeatedly requests the next value until `StopIteration`.

Conceptually:

```python
iterator = iter(iterable)

while True:
    try:
        value = next(iterator)
    except StopIteration:
        break
```

This is one of the most important internal concepts to understand.

---

# 85. Interview Cheat Sheet

```text
ITERABLE
↓
Can be iterated over
↓
iter(iterable)
↓
ITERATOR
↓
next(iterator)
↓
next value
↓
next(iterator)
↓
next value
↓
StopIteration
```

Generator:

```text
def function():
    yield value
        ↓
generator object
        ↓
iterator
        ↓
next()
        ↓
value
```

---

# 86. Most Important Questions to Prepare First

If interview preparation time is limited, prioritize these:

1. What is an iterable?
2. What is an iterator?
3. Iterable vs iterator?
4. What does `iter()` do?
5. What does `next()` do?
6. What is `StopIteration`?
7. How does a `for` loop work internally?
8. What is the iterator protocol?
9. How do you create a custom iterator?
10. Why does `__iter__()` return `self`?
11. What is a generator?
12. What is `yield`?
13. `return` vs `yield`?
14. What happens when a function contains `yield`?
15. Why are generators memory-efficient?
16. Generator vs list?
17. Generator vs iterator?
18. Generator function vs generator expression?
19. Can generators be reused?
20. What is lazy evaluation?
21. What is generator state?
22. What is `yield from`?
23. What is `send()`?
24. Real-world use cases of generators?
25. How can generators help in data processing?
26. Generator vs PySpark?

---

# 87. Final Interview Answer — Iterators

> An iterator is an object that allows us to access elements one at a time. It follows Python's iterator protocol by implementing `__iter__()` and `__next__()`. The `__next__()` method returns the next value and raises `StopIteration` when there are no more values.

---

# 88. Final Interview Answer — Generators

> A generator is a convenient way to create an iterator using the `yield` keyword or a generator expression. It produces values lazily, one at a time, and maintains its execution state between iterations. This makes generators useful for memory-efficient processing of large or streaming data.

---

# 89. Final Interview Answer — Iterable vs Iterator

> An iterable is an object that can provide an iterator, while an iterator is the object that actually produces values one at a time and maintains the current iteration state. For example, a list is iterable, and `iter(list)` gives us an iterator.

---

# 90. Final Interview Answer — Why Generators?

> I use generators when I want to process data incrementally instead of loading the complete result into memory. They are particularly useful for large files, streams, and data-processing pipelines where records can be handled one at a time.

---

# 91. Final Interview Answer — Real-World Example

> One practical example is processing a large file. Instead of reading all lines into a list, I can iterate over the file or use a generator to yield one line or record at a time. This allows the application to process large amounts of data with much lower memory usage.

---

# 92. Final Revision

Remember these four concepts clearly:

```text
Iterable
    ↓
Can provide an iterator

Iterator
    ↓
Uses __iter__() and __next__()

Generator
    ↓
A convenient way to create an iterator

yield
    ↓
Produces one value
    ↓
Pauses execution
    ↓
Resumes later
```

The most important relationship is:

```text
Iterable
   ↓ iter()
Iterator
   ↓ next()
Value
   ↓ next()
Value
   ↓
StopIteration
```

And for generators:

```text
Generator Function
       ↓
     yield
       ↓
Generator Object
       ↓
     next()
       ↓
Value
       ↓
Pause
       ↓
     next()
       ↓
Next Value
```

## Core Interview Takeaway

> **An iterable is something we can iterate over, an iterator is an object that produces the next value using `__next__()`, and a generator is a convenient way to create an iterator using `yield`. The biggest advantage of generators is lazy evaluation, which allows values to be processed one at a time and can significantly reduce memory usage for large sequential workloads.**