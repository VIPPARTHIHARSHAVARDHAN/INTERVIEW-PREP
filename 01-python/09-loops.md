# Python Loops — Interview Preparation

## 1. What Are Loops in Python?

Loops are used to **execute a block of code repeatedly** until a particular condition is satisfied or until all items in an iterable have been processed.

Python mainly provides two types of loops:

- `for` loop
- `while` loop

Python also provides loop-control statements:

- `break`
- `continue`
- `pass`

### Basic Example

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

### Interview Answer

> A loop is used to repeatedly execute a block of code. In Python, `for` is commonly used to iterate over an iterable, while `while` is used when repetition depends on a condition.

---

# 2. What Is a `for` Loop?

A `for` loop iterates over the elements of an iterable such as:

- List
- Tuple
- String
- Set
- Dictionary
- Range
- File
- Other iterable objects

### Example

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

The loop takes each element from the iterable one by one.

---

# 3. What Is the Syntax of a `for` Loop?

```python
for variable in iterable:
    statements
```

Example:

```python
names = ["Harsha", "Rahul", "Ravi"]

for name in names:
    print(name)
```

---

# 4. What Is an Iterable?

An iterable is an object whose elements can be accessed one at a time during iteration.

Common iterables include:

```python
numbers = [1, 2, 3]
name = "Python"
data = (10, 20, 30)
items = {1, 2, 3}
```

All of these can be used with a `for` loop.

```python
for x in numbers:
    print(x)
```

### Interview Answer

> An iterable is an object that can provide its elements one by one during iteration. Lists, tuples, strings, sets, dictionaries, and ranges are common examples.

---

# 5. What Is an Iterator?

An iterator is an object that produces values one at a time using the `__next__()` method.

An iterator can be created using `iter()`.

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

After all elements are consumed:

```python
next(iterator)
```

raises:

```text
StopIteration
```

### Interview Answer

> An iterator is an object that keeps track of its current position and returns the next value when `next()` is called. Iterators implement `__iter__()` and `__next__()`.

---

# 6. Difference Between Iterable and Iterator

| Iterable | Iterator |
|---|---|
| Can be iterated over | Produces values one at a time |
| Can be passed to `iter()` | Supports `next()` |
| Example: list | Example: `iter(list)` |
| Does not necessarily maintain iteration state | Maintains current iteration state |

Example:

```python
numbers = [1, 2, 3]

iterator = iter(numbers)

print(next(iterator))
```

Output:

```text
1
```

---

# 7. How Does a `for` Loop Work Internally?

Conceptually, Python obtains an iterator from the iterable and repeatedly calls `next()` until `StopIteration` occurs.

For example:

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

Conceptually behaves like:

```python
iterator = iter(numbers)

while True:
    try:
        number = next(iterator)
        print(number)
    except StopIteration:
        break
```

### Interview Answer

> A `for` loop works through the iterator protocol. Python obtains an iterator from the iterable, repeatedly gets the next element, and stops when `StopIteration` is raised.

---

# 8. What Is the `while` Loop?

A `while` loop repeatedly executes code **as long as its condition is truthy**.

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

Output:

```text
1
2
3
4
5
```

### Syntax

```python
while condition:
    statements
```

---

# 9. Difference Between `for` and `while` Loops

| `for` | `while` |
|---|---|
| Commonly used for iterating over an iterable | Commonly used when repetition depends on a condition |
| Iteration is naturally controlled by the iterable | Programmer usually controls the condition |
| Useful for known collections | Useful when the number of iterations may depend on runtime conditions |
| Example: iterate over a list | Example: continue until user enters a valid value |

### Example

```python
for number in [1, 2, 3]:
    print(number)
```

```python
count = 1

while count <= 3:
    print(count)
    count += 1
```

### Interview Answer

> I generally use a `for` loop when I want to iterate through an iterable, and a `while` loop when the repetition should continue based on a condition.

---

# 10. What Happens If the `while` Condition Is Initially False?

The loop body does not execute even once.

```python
x = 10

while x < 5:
    print(x)
```

There is no output.

---

# 11. What Is an Infinite Loop?

An infinite loop is a loop that never reaches a terminating condition.

Example:

```python
x = 1

while x <= 5:
    print(x)
```

Here `x` never changes, so the condition remains true.

### Correct Version

```python
x = 1

while x <= 5:
    print(x)
    x += 1
```

### Interview Answer

> An infinite loop occurs when the loop's termination condition is never reached. In a `while` loop, this commonly happens when the variable controlling the condition is never updated.

---

# 12. How Can You Intentionally Create an Infinite Loop?

You can use:

```python
while True:
    print("Running")
```

This continues until something exits the loop, such as `break`, an exception, or external interruption.

Example:

```python
while True:
    value = input("Enter q to quit: ")

    if value == "q":
        break
```

This pattern is useful when the termination condition is determined from inside the loop.

---

# 13. What Is `break`?

`break` immediately terminates the nearest enclosing loop.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

Output:

```text
0
1
2
3
4
```

When `i` becomes `5`, the loop stops.

---

# 14. What Is `continue`?

`continue` skips the remaining statements in the current iteration and moves to the next iteration.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

Output:

```text
0
1
3
4
```

The value `2` is skipped.

---

# 15. Difference Between `break` and `continue`

### `break`

Stops the entire loop.

```python
for i in range(5):
    if i == 2:
        break
    print(i)
```

Output:

```text
0
1
```

### `continue`

Skips only the current iteration.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

Output:

```text
0
1
3
4
```

### Interview Answer

> `break` terminates the loop completely, while `continue` skips the current iteration and allows the loop to continue with the next iteration.

---

# 16. What Is `pass`?

`pass` is a null statement. It does nothing when executed.

```python
for i in range(5):
    if i == 2:
        pass
    print(i)
```

Output:

```text
0
1
2
3
4
```

### Why Is It Used?

It can be used when Python requires a statement syntactically but you do not want to perform any action yet.

```python
def process_data():
    pass
```

---

# 17. Difference Between `pass`, `continue`, and `break`

| Statement | Behavior |
|---|---|
| `pass` | Does nothing |
| `continue` | Skips current iteration |
| `break` | Terminates loop |

Example:

```python
for i in range(5):
    if i == 1:
        pass
    elif i == 2:
        continue
    elif i == 4:
        break

    print(i)
```

Output:

```text
0
1
3
```

---

# 18. What Is `range()`?

`range()` generates a sequence of numbers that is commonly used with `for` loops.

```python
for i in range(5):
    print(i)
```

Output:

```text
0
1
2
3
4
```

The ending value `5` is excluded.

---

# 19. What Are the Different Forms of `range()`?

### One argument

```python
range(stop)
```

Example:

```python
range(5)
```

Produces:

```text
0 1 2 3 4
```

### Two arguments

```python
range(start, stop)
```

Example:

```python
range(2, 6)
```

Produces:

```text
2 3 4 5
```

### Three arguments

```python
range(start, stop, step)
```

Example:

```python
range(2, 10, 2)
```

Produces:

```text
2 4 6 8
```

---

# 20. Is the Stop Value Included in `range()`?

No.

```python
for i in range(1, 5):
    print(i)
```

Output:

```text
1
2
3
4
```

The value `5` is excluded.

---

# 21. Can `range()` Use a Negative Step?

Yes.

```python
for i in range(5, 0, -1):
    print(i)
```

Output:

```text
5
4
3
2
1
```

---

# 22. What Happens With `range(5, 1)`?

The default step is positive `1`.

```python
range(5, 1)
```

produces no values because Python would need to move upward from `5` toward `1`.

To count downward:

```python
range(5, 1, -1)
```

produces:

```text
5
4
3
2
```

---

# 23. Is `range()` a List?

No.

In Python 3, `range` is a range object rather than a list.

```python
r = range(5)

print(type(r))
```

It produces a range type.

If a list is required:

```python
print(list(range(5)))
```

Output:

```text
[0, 1, 2, 3, 4]
```

### Interview Answer

> `range()` returns a range object representing an arithmetic sequence. It does not create a complete list of values in memory like `list(range(...))` does.

---

# 24. Why Is `range()` Memory Efficient?

A range object represents the sequence using its parameters such as:

- start
- stop
- step

It does not need to store every generated number as a list.

For example:

```python
r = range(1000000000)
```

does not create a billion-element list in memory.

### Interview Answer

> `range` is memory efficient because it represents the sequence rather than storing every number as a list.

---

# 25. Can We Iterate Over a String?

Yes.

```python
name = "Python"

for char in name:
    print(char)
```

Output:

```text
P
y
t
h
o
n
```

---

# 26. Can We Iterate Over a List?

Yes.

```python
numbers = [10, 20, 30]

for number in numbers:
    print(number)
```

---

# 27. Can We Iterate Over a Tuple?

Yes.

```python
data = (10, 20, 30)

for value in data:
    print(value)
```

---

# 28. Can We Iterate Over a Set?

Yes.

```python
numbers = {10, 20, 30}

for number in numbers:
    print(number)
```

The order should not be relied upon as a meaningful ordering of a set.

---

# 29. How Does a `for` Loop Work With a Dictionary?

By default, iterating over a dictionary gives its keys.

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

---

# 30. How Do You Iterate Over Dictionary Values?

Use `.values()`.

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

---

# 31. How Do You Iterate Over Dictionary Keys and Values?

Use `.items()`.

```python
data = {
    "name": "Harsha",
    "age": 21
}

for key, value in data.items():
    print(key, value)
```

Output:

```text
name Harsha
age 21
```

### Interview Answer

> By default, iterating over a dictionary gives keys. I can use `.values()` for values and `.items()` when I need both keys and values.

---

# 32. What Is `enumerate()`?

`enumerate()` allows us to iterate over an iterable while getting both the index and the value.

```python
names = ["Harsha", "Rahul", "Ravi"]

for index, name in enumerate(names):
    print(index, name)
```

Output:

```text
0 Harsha
1 Rahul
2 Ravi
```

---

# 33. How Can You Change the Starting Index in `enumerate()`?

Use the `start` argument.

```python
names = ["Harsha", "Rahul", "Ravi"]

for index, name in enumerate(names, start=1):
    print(index, name)
```

Output:

```text
1 Harsha
2 Rahul
3 Ravi
```

### Interview Answer

> `enumerate()` is useful when I need both the index and the element while iterating. The optional `start` argument allows me to choose the starting index.

---

# 34. What Is `zip()`?

`zip()` combines elements from multiple iterables position by position.

```python
names = ["Harsha", "Rahul", "Ravi"]
scores = [90, 80, 70]

for name, score in zip(names, scores):
    print(name, score)
```

Output:

```text
Harsha 90
Rahul 80
Ravi 70
```

---

# 35. What Happens When Iterables Given to `zip()` Have Different Lengths?

Normally, `zip()` stops when the shortest iterable is exhausted.

```python
names = ["Harsha", "Rahul", "Ravi"]
scores = [90, 80]

for name, score in zip(names, scores):
    print(name, score)
```

Output:

```text
Harsha 90
Rahul 80
```

`Ravi` has no corresponding score, so it is not included.

---

# 36. What Is a Nested Loop?

A loop inside another loop is called a nested loop.

```python
for i in range(3):
    for j in range(2):
        print(i, j)
```

Output:

```text
0 0
0 1
1 0
1 1
2 0
2 1
```

For each iteration of the outer loop, the inner loop completes all its iterations.

---

# 37. How Many Times Does a Nested Loop Execute?

If the outer loop executes `m` times and the inner loop executes `n` times for every outer iteration, the inner statement executes approximately:

```text
m × n
```

times.

Example:

```python
for i in range(3):
    for j in range(4):
        print(i, j)
```

The `print()` executes:

```text
3 × 4 = 12
```

times.

---

# 38. What Is the Time Complexity of a Nested Loop?

If both loops independently run `n` times:

```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

the time complexity is:

```text
O(n²)
```

This is important for understanding performance.

---

# 39. Can Loops Be Nested With Different Types?

Yes.

A `for` loop can contain a `while` loop and vice versa.

```python
for i in range(3):
    j = 0

    while j < 2:
        print(i, j)
        j += 1
```

---

# 40. What Happens When `break` Is Used Inside Nested Loops?

`break` terminates the **nearest enclosing loop**.

```python
for i in range(3):
    for j in range(3):
        if j == 1:
            break
        print(i, j)
```

Output:

```text
0 0
1 0
2 0
```

The inner loop stops, but the outer loop continues.

---

# 41. What Happens When `continue` Is Used Inside Nested Loops?

It affects the nearest enclosing loop.

```python
for i in range(2):
    for j in range(3):
        if j == 1:
            continue
        print(i, j)
```

Output:

```text
0 0
0 2
1 0
1 2
```

Only the current inner-loop iteration is skipped.

---

# 42. Can `break` Exit Multiple Nested Loops?

A normal `break` exits only the nearest loop.

```python
for i in range(3):
    for j in range(3):
        if i == 1 and j == 1:
            break
```

The outer loop still continues.

To exit multiple levels, you generally need another control mechanism, such as:

- A flag
- Returning from a function
- Raising an exception in appropriate cases

Example using a flag:

```python
found = False

for i in range(3):
    for j in range(3):
        if i == 1 and j == 1:
            found = True
            break

    if found:
        break
```

---

# 43. What Is the `else` Clause With a Loop?

Python allows `else` with both `for` and `while`.

The loop's `else` block executes when the loop finishes **normally**, meaning it was not terminated by `break`.

### Example

```python
for i in range(5):
    print(i)
else:
    print("Loop completed")
```

Output:

```text
0
1
2
3
4
Loop completed
```

---

# 44. When Does Loop `else` Not Execute?

If the loop terminates using `break`, the `else` block does not execute.

```python
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("Loop completed")
```

Output:

```text
0
1
2
```

The `else` is skipped because `break` terminated the loop.

### Interview Answer

> The `else` associated with a loop executes when the loop completes normally. If the loop is terminated using `break`, the loop's `else` block is skipped.

---

# 45. What Is a Practical Use of Loop `else`?

A common use is searching for an item.

```python
numbers = [10, 20, 30, 40]
target = 25

for number in numbers:
    if number == target:
        print("Found")
        break
else:
    print("Not found")
```

Output:

```text
Not found
```

This avoids using a separate flag in simple search logic.

---

# 46. What Happens With `continue` and Loop `else`?

`continue` does not prevent the loop from completing normally.

Therefore, the `else` block can still execute.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
else:
    print("Completed")
```

Output:

```text
0
1
3
4
Completed
```

---

# 47. What Happens With `pass` and Loop `else`?

`pass` does not terminate the loop, so the loop can complete normally and its `else` can execute.

```python
for i in range(3):
    pass
else:
    print("Completed")
```

Output:

```text
Completed
```

---

# 48. What Is a Loop Variable?

The variable that receives each value during iteration is commonly called the loop variable.

```python
for number in [10, 20, 30]:
    print(number)
```

Here:

```text
number
```

is the loop variable.

Its value changes on each iteration.

---

# 49. Can We Use `_` as a Loop Variable?

Yes.

When the actual value is not needed, `_` is commonly used by convention.

```python
for _ in range(3):
    print("Hello")
```

Output:

```text
Hello
Hello
Hello
```

### Interview Point

`_` is still a normal variable name; Python does not make it magically unused. It is simply a common convention indicating that the value is intentionally ignored.

---

# 50. Can We Modify a List While Iterating Over It?

It is generally risky to modify the structure of a list while directly iterating over it because elements can be skipped or processed unexpectedly.

Problematic example:

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers:
    if number % 2 == 0:
        numbers.remove(number)

print(numbers)
```

This can produce surprising results because the list changes while the loop is traversing it.

A safer approach is to create a new list:

```python
numbers = [1, 2, 3, 4, 5]

numbers = [number for number in numbers if number % 2 != 0]

print(numbers)
```

Output:

```text
[1, 3, 5]
```

---

# 51. How Do You Iterate Over a Copy of a List?

If modification is necessary, one option is to iterate over a copy.

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers[:]:
    if number % 2 == 0:
        numbers.remove(number)

print(numbers)
```

Output:

```text
[1, 3, 5]
```

The loop iterates over the copy while modifying the original list.

---

# 52. How Do You Reverse a Loop?

Use a negative step with `range()`.

```python
for i in range(5, 0, -1):
    print(i)
```

Output:

```text
5
4
3
2
1
```

---

# 53. How Do You Loop Through a List in Reverse?

Use `reversed()`.

```python
numbers = [1, 2, 3, 4]

for number in reversed(numbers):
    print(number)
```

Output:

```text
4
3
2
1
```

---

# 54. Difference Between `reversed()` and `reverse()`

`reverse()` is a list method that modifies the list in place.

```python
numbers = [1, 2, 3]

numbers.reverse()

print(numbers)
```

Output:

```text
[3, 2, 1]
```

`reversed()` returns an iterator that iterates over the sequence in reverse.

```python
numbers = [1, 2, 3]

for number in reversed(numbers):
    print(number)
```

The original list is not modified.

---

# 55. How Do You Skip Even Numbers in a Loop?

```python
for number in range(1, 11):
    if number % 2 == 0:
        continue
    print(number)
```

Output:

```text
1
3
5
7
9
```

---

# 56. How Do You Stop When a Particular Value Is Found?

```python
numbers = [10, 20, 30, 40]

for number in numbers:
    if number == 30:
        break
    print(number)
```

Output:

```text
10
20
```

---

# 57. How Do You Find the Sum of Numbers Using a Loop?

```python
numbers = [10, 20, 30, 40]

total = 0

for number in numbers:
    total += number

print(total)
```

Output:

```text
100
```

---

# 58. How Do You Count Elements Using a Loop?

```python
numbers = [10, 20, 30, 40]

count = 0

for number in numbers:
    count += 1

print(count)
```

Output:

```text
4
```

In real Python code, `len(numbers)` is usually simpler when the goal is simply to get the collection's length.

---

# 59. How Do You Find the Maximum Value Using a Loop?

```python
numbers = [10, 25, 15, 40, 5]

maximum = numbers[0]

for number in numbers[1:]:
    if number > maximum:
        maximum = number

print(maximum)
```

Output:

```text
40
```

### Interview Explanation

> I initialize the maximum with the first element and then compare every remaining element against it. Whenever I find a larger value, I update the maximum.

---

# 60. How Do You Find the Minimum Value Using a Loop?

```python
numbers = [10, 25, 15, 40, 5]

minimum = numbers[0]

for number in numbers[1:]:
    if number < minimum:
        minimum = number

print(minimum)
```

Output:

```text
5
```

---

# 61. How Do You Count Vowels in a String Using a Loop?

```python
text = "python programming"

count = 0

for char in text.lower():
    if char in "aeiou":
        count += 1

print(count)
```

Output:

```text
4
```

---

# 62. How Do You Reverse a String Using a Loop?

```python
text = "Python"

reversed_text = ""

for char in text:
    reversed_text = char + reversed_text

print(reversed_text)
```

Output:

```text
nohtyP
```

For normal Python code, slicing is simpler:

```python
reversed_text = text[::-1]
```

---

# 63. How Do You Check Whether a String Is a Palindrome Using a Loop?

```python
text = "madam"

reversed_text = ""

for char in text:
    reversed_text = char + reversed_text

if text == reversed_text:
    print("Palindrome")
else:
    print("Not palindrome")
```

Output:

```text
Palindrome
```

---

# 64. How Do You Print a Multiplication Table?

```python
number = 5

for i in range(1, 11):
    print(number, "*", i, "=", number * i)
```

Output:

```text
5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
5 * 4 = 20
5 * 5 = 25
5 * 6 = 30
5 * 7 = 35
5 * 8 = 40
5 * 9 = 45
5 * 10 = 50
```

---

# 65. How Do You Calculate Factorial Using a Loop?

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

# 66. How Do You Generate Fibonacci Numbers Using a Loop?

```python
n = 7

a = 0
b = 1

for _ in range(n):
    print(a)
    a, b = b, a + b
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
```

---

# 67. How Do You Check Whether a Number Is Prime Using a Loop?

```python
number = 29

if number < 2:
    print("Not prime")
else:
    is_prime = True

    for i in range(2, int(number ** 0.5) + 1):
        if number % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime")
    else:
        print("Not prime")
```

Output:

```text
Prime
```

### Interview Explanation

> I only need to check possible divisors up to the square root of the number. If a number has a factor greater than its square root, the corresponding factor must be smaller than the square root.

---

# 68. Why Is `break` Useful in Searching?

Once the required value is found, continuing to scan the remaining elements is unnecessary.

```python
numbers = [10, 20, 30, 40, 50]

target = 30

for number in numbers:
    if number == target:
        print("Found")
        break
```

This can avoid unnecessary iterations.

---

# 69. What Is the Difference Between `for` and `while` in Terms of Infinite Loops?

A `while` loop can easily become infinite if its condition never becomes false.

```python
x = 1

while x > 0:
    print(x)
```

A `for` loop over a finite iterable naturally terminates when the iterable is exhausted.

```python
for x in [1, 2, 3]:
    print(x)
```

However, a `for` loop can also be infinite if its underlying iterator produces values indefinitely.

---

# 70. Can a `for` Loop Have an `else`?

Yes.

```python
for i in range(3):
    print(i)
else:
    print("Done")
```

Output:

```text
0
1
2
Done
```

---

# 71. Can a `while` Loop Have an `else`?

Yes.

```python
i = 0

while i < 3:
    print(i)
    i += 1
else:
    print("Done")
```

Output:

```text
0
1
2
Done
```

---

# 72. What Happens If a Loop `else` Contains a `break`?

The `break` inside the loop determines whether the loop's `else` runs.

```python
for i in range(5):
    if i == 2:
        break
else:
    print("Completed")
```

Nothing is printed from the `else`.

---

# 73. What Happens If a Loop `else` Contains a `continue`?

The `continue` only affects the current iteration.

```python
for i in range(3):
    if i == 1:
        continue
    print(i)
else:
    print("Completed")
```

Output:

```text
0
2
Completed
```

---

# 74. What Is a Common Mistake in a `while` Loop?

Forgetting to update the loop-control variable.

Incorrect:

```python
i = 1

while i <= 5:
    print(i)
```

The condition never becomes false.

Correct:

```python
i = 1

while i <= 5:
    print(i)
    i += 1
```

---

# 75. What Is a Common Off-by-One Error?

An off-by-one error happens when the loop executes one time too many or one time too few.

Example:

```python
for i in range(1, 5):
    print(i)
```

Output:

```text
1
2
3
4
```

If you want to include `5`:

```python
for i in range(1, 6):
    print(i)
```

### Interview Tip

Remember:

> `range(start, stop)` excludes `stop`.

---

# 76. What Happens If `range()` Has a Step of Zero?

This is invalid.

```python
range(1, 5, 0)
```

It raises:

```text
ValueError
```

A step must not be zero because Python would have no way to progress through the sequence.

---

# 77. Can We Use Expressions in `range()`?

Yes.

```python
n = 5

for i in range(1, n + 1):
    print(i)
```

This is common when you want to include `n`.

---

# 78. What Is Loop Control Flow?

Loop control flow determines whether the loop:

- Continues normally
- Skips an iteration
- Terminates
- Completes and executes `else`

The important statements are:

```text
break
continue
pass
```

---

# 79. Real-World Example — Processing Records

Suppose a list contains customer records:

```python
records = [
    {"name": "A", "status": "valid"},
    {"name": "B", "status": "invalid"},
    {"name": "C", "status": "valid"}
]

for record in records:
    if record["status"] == "invalid":
        continue

    print("Processing:", record["name"])
```

Output:

```text
Processing: A
Processing: C
```

### Data Engineering Connection

`continue` can be useful when invalid records should be skipped while processing the remaining records.

---

# 80. Real-World Example — Stop Processing After a Condition

```python
records = [
    {"id": 1, "status": "completed"},
    {"id": 2, "status": "completed"},
    {"id": 3, "status": "failed"},
    {"id": 4, "status": "completed"}
]

for record in records:
    if record["status"] == "failed":
        print("Failure found")
        break

    print("Processing:", record["id"])
```

Output:

```text
Processing: 1
Processing: 2
Failure found
```

---

# 81. Real-World Example — Processing Data From a File

```python
with open("data.txt") as file:
    for line in file:
        line = line.strip()

        if not line:
            continue

        print(line)
```

Here the loop processes the file line by line and skips empty lines.

### Interview Explanation

> Iterating over a file is useful because the file can be processed incrementally instead of manually loading every line into a list first.

---

# 82. Real-World Example — Data Validation

```python
records = [
    {"name": "Harsha", "age": 21},
    {"name": "", "age": 20},
    {"name": "Ravi", "age": None}
]

for record in records:
    if not record["name"] or record["age"] is None:
        continue

    print("Valid:", record)
```

Output:

```text
Valid: {'name': 'Harsha', 'age': 21}
```

This demonstrates how loops and conditions can work together for validation.

---

# 83. Real-World Example — ETL Processing

A simplified ETL-style example:

```python
records = [
    {"amount": 1000, "status": "completed"},
    {"amount": 5000, "status": "failed"},
    {"amount": 3000, "status": "completed"}
]

processed = []

for record in records:
    if record["status"] != "completed":
        continue

    transformed_amount = record["amount"] * 1.18

    processed.append({
        "amount": transformed_amount
    })

print(processed)
```

Output:

```text
[
    {'amount': 1180.0},
    {'amount': 3540.0}
]
```

### Interview Explanation

> This is a simplified example of a transformation step where I iterate through records, filter out invalid or failed records, transform the required data, and store the processed result.

---

# 84. How Do Loops Relate to Data Engineering?

Loops are useful for:

- Processing records
- Reading files
- Validating data
- Applying business rules
- Iterating through API responses
- Processing configuration items
- Automating repetitive tasks

However, when working with large datasets using tools such as Spark, repeatedly processing individual records in Python may not be the most efficient approach.

### Important Data Engineering Interview Point

> In distributed data processing, I would generally prefer Spark transformations and built-in functions instead of Python-level loops over large datasets because Spark can optimize and distribute the work.

---

# 85. Why Should We Avoid Python Loops for Large DataFrames in PySpark?

Suppose we have a large Spark DataFrame.

A Python loop over individual records can introduce unnecessary driver-side processing and reduce the benefits of distributed execution.

Instead of thinking:

```python
for row in large_dataframe:
    # process row
```

prefer Spark-native transformations such as:

```python
from pyspark.sql.functions import col, when

result = df.withColumn(
    "category",
    when(col("amount") >= 10000, "high")
    .otherwise("normal")
)
```

### Interview Answer

> For large Spark datasets, I prefer Spark-native transformations and functions because they are designed for distributed processing. Python-level iteration can move the work toward the driver and lose Spark's distributed execution advantages.

---

# 86. What Is a Generator and How Is It Related to Loops?

A generator produces values lazily, usually using `yield`.

```python
def numbers():
    for i in range(3):
        yield i

for number in numbers():
    print(number)
```

Output:

```text
0
1
2
```

The generator produces values one at a time instead of creating the entire result at once.

### Interview Connection

Generators are useful when working with large or streaming data because they can reduce memory usage.

---

# 87. Difference Between Returning a List and Using a Generator

### List

```python
def get_numbers():
    return [1, 2, 3, 4, 5]
```

The complete list is created.

### Generator

```python
def get_numbers():
    for i in range(1, 6):
        yield i
```

Values are produced one at a time.

### Interview Answer

> A list stores the complete collection in memory, while a generator produces values lazily as they are requested. Generators are useful when the complete result does not need to be held in memory at once.

---

# 88. Important Output-Based Question

```python
for i in range(5):
    if i == 2:
        break
    print(i)
```

### Answer

```text
0
1
```

---

# 89. Important Output-Based Question

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

### Answer

```text
0
1
3
4
```

---

# 90. Important Output-Based Question

```python
for i in range(3):
    print(i)
else:
    print("Done")
```

### Answer

```text
0
1
2
Done
```

---

# 91. Important Output-Based Question

```python
for i in range(3):
    if i == 1:
        break
    print(i)
else:
    print("Done")
```

### Answer

```text
0
```

The `else` does not execute because the loop was terminated by `break`.

---

# 92. Important Output-Based Question

```python
for i in range(3):
    if i == 1:
        continue
    print(i)
else:
    print("Done")
```

### Answer

```text
0
2
Done
```

`continue` does not count as terminating the loop.

---

# 93. Important Output-Based Question

```python
x = 0

while x < 3:
    print(x)
    x += 1
```

### Answer

```text
0
1
2
```

---

# 94. Important Output-Based Question

```python
x = 5

while x > 0:
    print(x)
    x -= 2
```

### Answer

```text
5
3
1
```

---

# 95. Important Output-Based Question

```python
for i in range(2):
    for j in range(3):
        print(i, j)
```

### Answer

```text
0 0
0 1
0 2
1 0
1 1
1 2
```

---

# 96. Important Output-Based Question

```python
numbers = [1, 2, 3]

for index, value in enumerate(numbers):
    print(index, value)
```

### Answer

```text
0 1
1 2
2 3
```

---

# 97. Important Output-Based Question

```python
a = [1, 2, 3]
b = ["a", "b", "c"]

for x, y in zip(a, b):
    print(x, y)
```

### Answer

```text
1 a
2 b
3 c
```

---

# 98. Important Output-Based Question

```python
for i in range(5, 0, -1):
    print(i)
```

### Answer

```text
5
4
3
2
1
```

---

# 99. Important Output-Based Question

```python
for i in range(2, 10, 2):
    print(i)
```

### Answer

```text
2
4
6
8
```

---

# 100. Important Output-Based Question

```python
x = 10

while x:
    print(x)
    x -= 3
```

### Answer

```text
10
7
4
1
```

After `x` becomes `-2`, the condition is still truthy, so this actually continues:

```text
10
7
4
1
-2
-5
...
```

### Important Interview Point

A negative non-zero integer is truthy. Therefore, this loop does **not** terminate merely because `x` becomes negative.

A correct terminating version would be:

```python
x = 10

while x > 0:
    print(x)
    x -= 3
```

Output:

```text
10
7
4
1
```

---

# 101. Important Output-Based Question

```python
numbers = [1, 2, 3, 4]

for number in numbers:
    if number % 2 == 0:
        continue

    print(number)
```

### Answer

```text
1
3
```

---

# 102. Important Output-Based Question

```python
numbers = [1, 2, 3, 4, 5]

for number in numbers:
    if number == 4:
        break

    print(number)
```

### Answer

```text
1
2
3
```

---

# 103. Important Output-Based Question

```python
for i in range(3):
    pass

print("Finished")
```

### Answer

```text
Finished
```

`pass` does nothing and does not stop the loop.

---

# 104. Important Output-Based Question

```python
print(list(range(2, 10, 2)))
```

### Answer

```text
[2, 4, 6, 8]
```

---

# 105. Important Output-Based Question

```python
print(list(range(5, 0, -1)))
```

### Answer

```text
[5, 4, 3, 2, 1]
```

---

# 106. Important Interview Questions to Master

Before a Python placement interview, make sure you can confidently answer:

1. What is a loop?
2. What are the different types of loops in Python?
3. Difference between `for` and `while`.
4. What is an iterable?
5. What is an iterator?
6. Difference between iterable and iterator.
7. How does a `for` loop work internally?
8. What is `iter()`?
9. What is `next()`?
10. What is `StopIteration`?
11. What is `range()`?
12. Is `range()` a list?
13. Why is `range()` memory efficient?
14. How does `range(start, stop, step)` work?
15. Is the stop value included?
16. How do you iterate backward?
17. What is an infinite loop?
18. How can a `while` loop become infinite?
19. What is `break`?
20. What is `continue`?
21. What is `pass`?
22. Difference between `break`, `continue`, and `pass`.
23. What is nested looping?
24. What is the complexity of nested loops?
25. How does `break` behave in nested loops?
26. How does `continue` behave in nested loops?
27. What is loop `else`?
28. When does loop `else` execute?
29. When does loop `else` not execute?
30. Can both `for` and `while` have `else`?
31. What is `enumerate()`?
32. Why use `enumerate()`?
33. What is `zip()`?
34. What happens when `zip()` receives different-length iterables?
35. How do you iterate over dictionary keys?
36. How do you iterate over dictionary values?
37. How do you iterate over dictionary key-value pairs?
38. How do you iterate over a string?
39. How do you iterate over a file?
40. Why can modifying a list while iterating be dangerous?
41. How can you safely filter a list?
42. What is an off-by-one error?
43. Why does `range()` exclude the stop value?
44. What happens if range step is zero?
45. How do you reverse a list during iteration?
46. Difference between `reverse()` and `reversed()`.
47. What is a generator?
48. How does `yield` relate to loops?
49. Difference between a generator and a list.
50. How are loops used in data processing?
51. Why should Python loops generally be avoided for large PySpark DataFrames?
52. What are Spark-native transformations?
53. How would you use `break` when searching?
54. How would you use `continue` for invalid records?
55. How would you process records using a loop?
56. How would you calculate sum using a loop?
57. How would you find maximum/minimum using a loop?
58. How would you count vowels?
59. How would you reverse a string?
60. How would you check a palindrome?
61. How would you calculate factorial?
62. How would you generate Fibonacci numbers?
63. How would you check whether a number is prime?
64. Predict the output of nested loops.
65. Predict the output of `break`.
66. Predict the output of `continue`.
67. Predict the output of loop `else`.
68. Predict the output of `range()`.
69. Predict the output of `enumerate()`.
70. Predict the output of `zip()`.

---

# 107. Final Quick Revision

```text
for
    -> Iterates over an iterable

while
    -> Repeats while a condition is truthy

break
    -> Terminates the nearest loop

continue
    -> Skips the current iteration

pass
    -> Does nothing

range()
    -> Represents an arithmetic sequence

iter()
    -> Creates/obtains an iterator

next()
    -> Gets the next item from an iterator

StopIteration
    -> Signals that an iterator is exhausted

enumerate()
    -> Gives index + value

zip()
    -> Combines iterables position by position

nested loop
    -> Loop inside another loop

loop else
    -> Runs when loop finishes without break

generator
    -> Produces values lazily using yield
```

## Final Interview-Level Understanding

> **A strong understanding of Python loops goes beyond knowing `for` and `while`. You should understand the iterable and iterator protocols, `range()`, `break`, `continue`, `pass`, nested loops, loop `else`, `enumerate()`, `zip()`, generators, common loop patterns, output-based questions, and the performance implications of loops. For data engineering interviews, you should also understand when Python loops are appropriate and why Spark-native transformations are preferred for large distributed datasets.**