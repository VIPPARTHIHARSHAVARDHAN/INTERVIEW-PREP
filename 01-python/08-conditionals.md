# Python Conditionals — Interview Preparation

## 1. What Are Conditional Statements in Python?

Conditional statements allow a program to **make decisions based on whether a condition is true or false**.

The main conditional statements in Python are:

- `if`
- `if-else`
- `if-elif-else`
- Nested `if`
- Conditional expression (ternary operator)

### Basic Example

```python
age = 21

if age >= 18:
    print("Eligible to vote")
```

Output:

```text
Eligible to vote
```

### Interview Answer

> Conditional statements are used to control the flow of a program based on conditions. Python mainly provides `if`, `elif`, and `else` for decision-making.

---

# 2. What Is an `if` Statement?

The `if` statement executes a block of code only when its condition evaluates to `True`.

```python
age = 20

if age >= 18:
    print("Adult")
```

If the condition is false, the block is skipped.

```python
age = 15

if age >= 18:
    print("Adult")
```

No output is produced.

### Syntax

```python
if condition:
    statement
```

---

# 3. Why Is Indentation Important in Python Conditionals?

Python uses **indentation to define code blocks**.

```python
age = 20

if age >= 18:
    print("Adult")
    print("Eligible")
```

Both `print()` statements belong to the `if` block.

Incorrect indentation can result in an `IndentationError` or change the logic of the program.

### Interview Answer

> Unlike languages that use braces to define blocks, Python uses indentation. Therefore, proper indentation is required to define which statements belong to a conditional block.

---

# 4. What Is `if-else`?

`if-else` provides two possible paths.

```python
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

Output:

```text
Minor
```

If the condition is true, the `if` block executes. Otherwise, the `else` block executes.

---

# 5. What Is `if-elif-else`?

It is used when there are **multiple conditions**.

```python
marks = 75

if marks >= 90:
    print("A")
elif marks >= 75:
    print("B")
elif marks >= 50:
    print("C")
else:
    print("Fail")
```

Output:

```text
B
```

Python checks the conditions from top to bottom and executes the first matching branch.

---

# 6. How Does Python Execute an `if-elif-else` Chain?

Consider:

```python
marks = 85

if marks >= 90:
    print("A")
elif marks >= 75:
    print("B")
elif marks >= 50:
    print("C")
else:
    print("Fail")
```

Execution:

1. Check `marks >= 90` → `False`
2. Check `marks >= 75` → `True`
3. Execute `"B"`
4. Stop checking the remaining conditions

Output:

```text
B
```

### Important Interview Point

Only **one branch** of an `if-elif-else` chain executes.

---

# 7. Can Multiple Conditions Be True in an `if-elif` Chain?

Yes, multiple conditions may technically be true, but only the **first true condition** executes.

```python
x = 10

if x > 0:
    print("Positive")
elif x > 5:
    print("Greater than 5")
```

Output:

```text
Positive
```

Although both conditions are true, the `elif` is not checked after the first `if` succeeds.

### Important

Compare this with separate `if` statements:

```python
x = 10

if x > 0:
    print("Positive")

if x > 5:
    print("Greater than 5")
```

Output:

```text
Positive
Greater than 5
```

---

# 8. Difference Between Multiple `if` Statements and `if-elif-else`

### Multiple `if`

Every condition is evaluated independently.

```python
x = 10

if x > 0:
    print("Positive")

if x > 5:
    print("Greater than 5")
```

Output:

```text
Positive
Greater than 5
```

### `if-elif-else`

Only the first matching condition executes.

```python
x = 10

if x > 0:
    print("Positive")
elif x > 5:
    print("Greater than 5")
```

Output:

```text
Positive
```

### Interview Answer

> Separate `if` statements are independent, so multiple blocks can execute. In an `if-elif-else` chain, Python stops after the first condition that evaluates to true.

---

# 9. What Is a Nested `if` Statement?

An `if` statement inside another `if` statement is called a nested `if`.

```python
age = 22
has_id = True

if age >= 18:
    if has_id:
        print("Entry allowed")
```

Output:

```text
Entry allowed
```

### Real-World Example

```python
username = "harsha"
password = "1234"

if username == "harsha":
    if password == "1234":
        print("Login successful")
```

Nested conditions can be useful, but excessive nesting can make code harder to read.

---

# 10. What Are Logical Operators in Conditions?

Python provides:

- `and`
- `or`
- `not`

### `and`

Both conditions must be true.

```python
age = 21
has_id = True

if age >= 18 and has_id:
    print("Allowed")
```

### `or`

At least one condition must be true.

```python
is_admin = False
is_manager = True

if is_admin or is_manager:
    print("Access granted")
```

### `not`

Reverses the Boolean result.

```python
logged_in = False

if not logged_in:
    print("Please login")
```

---

# 11. What Is the Difference Between `and` and `or`?

### `and`

Returns a truthy result only when both operands are truthy.

```python
True and True
```

Result:

```text
True
```

But:

```python
True and False
```

Result:

```text
False
```

### `or`

Returns a truthy result when at least one operand is truthy.

```python
True or False
```

Result:

```text
True
```

---

# 12. What Does `not` Do?

`not` reverses the truth value.

```python
print(not True)
print(not False)
```

Output:

```text
False
True
```

Example:

```python
is_logged_in = False

if not is_logged_in:
    print("Login required")
```

---

# 13. What Are Comparison Operators?

Comparison operators are frequently used in conditions.

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

Example:

```python
a = 10
b = 20

print(a == b)
print(a != b)
print(a < b)
print(a > b)
```

Output:

```text
False
True
True
False
```

---

# 14. What Is the Difference Between `=` and `==`?

This is a very common interview question.

### `=`

Assignment operator.

```python
x = 10
```

It assigns `10` to `x`.

### `==`

Equality comparison.

```python
x == 10
```

It checks whether `x` is equal to `10`.

### Interview Answer

> `=` assigns a value to a variable, whereas `==` compares two values for equality.

---

# 15. What Is the Difference Between `==` and `is`?

`==` compares **values**.

`is` compares **object identity**.

```python
a = [1, 2]
b = [1, 2]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

The lists contain equal values but are different objects.

### Interview Answer

> `==` checks whether two objects have equal values, while `is` checks whether both references point to the same object.

---

# 16. When Should `is` Commonly Be Used?

A common use is checking against `None`.

```python
value = None

if value is None:
    print("No value")
```

Prefer:

```python
if value is None:
```

instead of:

```python
if value == None:
```

### Interview Answer

> `is` is commonly used for identity checks, especially checking whether a variable is `None`.

---

# 17. What Is Truthiness in Python?

Python allows many objects to be evaluated directly in a condition.

Some values are considered **falsy**:

```text
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

Most other objects are truthy.

Example:

```python
data = []

if data:
    print("Data exists")
else:
    print("Data is empty")
```

Output:

```text
Data is empty
```

---

# 18. Why Can We Write `if list:` Instead of `if len(list) > 0`?

Python collections have a truth value.

```python
numbers = [1, 2, 3]

if numbers:
    print("List is not empty")
```

This is cleaner than:

```python
if len(numbers) > 0:
    print("List is not empty")
```

### Interview Answer

> Empty collections are falsy and non-empty collections are truthy, so Python allows direct truth-value testing of collections.

---

# 19. What Is a Truthy Value?

An object is truthy when its Boolean evaluation is `True`.

```python
print(bool(10))
print(bool("Python"))
print(bool([1, 2]))
```

Output:

```text
True
True
True
```

---

# 20. What Is a Falsy Value?

An object is falsy when its Boolean evaluation is `False`.

```python
print(bool(0))
print(bool(""))
print(bool([]))
print(bool(None))
```

Output:

```text
False
False
False
False
```

---

# 21. What Does `bool()` Do?

`bool()` converts a value into its Boolean truth value.

```python
print(bool(1))
print(bool(0))
print(bool("hello"))
print(bool(""))
```

Output:

```text
True
False
True
False
```

---

# 22. What Happens If `if` Receives a Non-Boolean Value?

Python evaluates the object's **truth value**.

```python
value = 10

if value:
    print("Truthy")
```

Output:

```text
Truthy
```

It is not necessary for the condition to literally be `True` or `False`.

---

# 23. Can Strings Be Used Directly in Conditions?

Yes.

Non-empty strings are truthy.

```python
name = "Harsha"

if name:
    print("Name is available")
```

Output:

```text
Name is available
```

An empty string is falsy:

```python
name = ""

if not name:
    print("Name is empty")
```

---

# 24. Can Numbers Be Used Directly in Conditions?

Yes.

`0` is falsy and non-zero numbers are truthy.

```python
number = 10

if number:
    print("Non-zero")
```

Output:

```text
Non-zero
```

---

# 25. What Is a Conditional Expression?

A conditional expression is Python's one-line form of `if-else`.

It is commonly called a **ternary expression**.

### Normal

```python
age = 20

if age >= 18:
    result = "Adult"
else:
    result = "Minor"
```

### Conditional Expression

```python
age = 20

result = "Adult" if age >= 18 else "Minor"

print(result)
```

Output:

```text
Adult
```

### Syntax

```python
value_if_true if condition else value_if_false
```

---

# 26. When Should You Use a Conditional Expression?

Use it when the logic is simple and readable.

```python
status = "Pass" if marks >= 40 else "Fail"
```

Avoid putting complicated logic into a single line.

Instead of:

```python
result = "A" if marks >= 90 else "B" if marks >= 75 else "C"
```

a normal `if-elif-else` structure may be clearer.

---

# 27. Can We Have Nested Ternary Expressions?

Yes.

```python
marks = 85

result = (
    "A" if marks >= 90
    else "B" if marks >= 75
    else "C"
)

print(result)
```

Output:

```text
B
```

However, too many nested ternary expressions reduce readability.

---

# 28. What Is Short-Circuit Evaluation?

Python may stop evaluating a logical expression as soon as the result is known.

This happens with:

- `and`
- `or`

### `and`

If the first operand is falsy, Python does not need to evaluate the second operand.

```python
x = 0

if x and 10 / x:
    print("True")
```

No division-by-zero error occurs because `x` is falsy and the second expression is not evaluated.

### `or`

If the first operand is truthy, Python does not need to evaluate the second operand.

```python
x = 10

result = x or 20

print(result)
```

Output:

```text
10
```

### Interview Answer

> Short-circuit evaluation means Python stops evaluating a logical expression as soon as the final result is already determined.

---

# 29. What Is the Short-Circuit Behavior of `and`?

For:

```python
A and B
```

if `A` is falsy, Python returns `A` without evaluating `B`.

Example:

```python
x = 0

result = x and 10

print(result)
```

Output:

```text
0
```

---

# 30. What Is the Short-Circuit Behavior of `or`?

For:

```python
A or B
```

if `A` is truthy, Python returns `A` without evaluating `B`.

```python
x = 10

result = x or 20

print(result)
```

Output:

```text
10
```

---

# 31. Do `and` and `or` Always Return `True` or `False`?

No.

This is an important Python interview question.

They return one of their operands.

```python
print(10 and 20)
print(0 and 20)

print(10 or 20)
print(0 or 20)
```

Output:

```text
20
0
10
20
```

### Interview Answer

> `and` and `or` are logical operators, but they return operands rather than necessarily returning Boolean values. Their behavior is based on truthiness and short-circuit evaluation.

---

# 32. What Is the Order of Evaluation of Logical Operators?

The general precedence is:

```text
not
and
or
```

So:

```python
a or b and c
```

is evaluated as:

```python
a or (b and c)
```

not:

```python
(a or b) and c
```

### Best Practice

Use parentheses when the logic could be unclear:

```python
if (age >= 18 and has_id) or is_admin:
    print("Allowed")
```

---

# 33. What Is Operator Precedence in Conditions?

Python follows operator precedence rules.

For common conditional expressions:

1. Arithmetic operators
2. Comparison operators
3. `not`
4. `and`
5. `or`

Example:

```python
x = 10

if x > 5 and x < 20:
    print("Valid")
```

Python evaluates the comparisons before `and`.

---

# 34. What Is Chained Comparison?

Python allows multiple comparisons in a single expression.

```python
x = 10

if 5 < x < 20:
    print("x is between 5 and 20")
```

This is equivalent in meaning to:

```python
if x > 5 and x < 20:
    print("x is between 5 and 20")
```

### Interview Answer

> Python supports chained comparisons, which allow multiple comparisons to be written in a readable form such as `5 < x < 20`.

---

# 35. Can We Chain Equality Comparisons?

Yes.

```python
x = 10

if x == 10 == 10:
    print("True")
```

Python evaluates chained comparisons according to its comparison chaining rules.

---

# 36. How Do You Check Whether a Number Is Within a Range?

Use chained comparison:

```python
age = 21

if 18 <= age <= 60:
    print("Eligible")
```

This is concise and readable.

---

# 37. What Is the Difference Between `if x == True` and `if x`?

Consider:

```python
x = 1

if x:
    print("Truthy")
```

This executes because `1` is truthy.

But:

```python
if x == True:
    print("Equal to True")
```

has different semantics.

For clean Boolean checks, prefer:

```python
if x:
```

when you want truthiness.

For actual Boolean variables:

```python
is_active = True

if is_active:
    print("Active")
```

---

# 38. How Do You Check Multiple Possible Values?

Use `in`.

Instead of:

```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("Weekend")
```

you can write:

```python
if day in ("Saturday", "Sunday"):
    print("Weekend")
```

For membership checks, this is usually cleaner.

---

# 39. How Do You Check Multiple Invalid Values?

Use `not in`.

```python
role = "guest"

if role not in ("admin", "manager"):
    print("Limited access")
```

---

# 40. What Is the Difference Between `in` and `==` in Conditions?

`==` checks equality between two values.

```python
if role == "admin":
    print("Admin")
```

`in` checks membership in a collection.

```python
if role in ("admin", "manager"):
    print("Authorized")
```

---

# 41. What Happens If No Condition Matches and There Is No `else`?

Nothing happens.

```python
age = 15

if age >= 18:
    print("Adult")
```

No output is produced.

An `else` is optional.

---

# 42. Is `else` Mandatory With `if`?

No.

```python
if condition:
    statement
```

is valid.

Likewise:

```python
if condition:
    statement
elif another_condition:
    statement
```

is also valid without an `else`.

---

# 43. Can `elif` Exist Without `if`?

No.

`elif` must belong to an `if` statement.

This is invalid:

```python
elif x > 10:
    print(x)
```

---

# 44. Can We Have Multiple `elif` Statements?

Yes.

```python
marks = 65

if marks >= 90:
    print("A")
elif marks >= 80:
    print("B")
elif marks >= 70:
    print("C")
elif marks >= 60:
    print("D")
else:
    print("Fail")
```

Python checks them from top to bottom.

---

# 45. Can We Have Multiple `else` Blocks for One `if`?

No.

This is invalid:

```python
if x > 0:
    print("Positive")
else:
    print("Not positive")
else:
    print("Another")
```

An `if` statement can have at most one `else`.

---

# 46. Can We Have Multiple `if` Blocks Inside an `else`?

Yes.

```python
age = 15

if age >= 18:
    print("Adult")
else:
    if age >= 13:
        print("Teenager")
    else:
        print("Child")
```

However, if the logic becomes complex, `elif` is often clearer.

---

# 47. How Do You Rewrite Nested `if` Using Logical Operators?

Instead of:

```python
if age >= 18:
    if has_id:
        print("Allowed")
```

you can write:

```python
if age >= 18 and has_id:
    print("Allowed")
```

This is often simpler.

---

# 48. What Is the Difference Between Nested `if` and `and`?

Both can express dependent conditions, but they have different readability and control-flow characteristics.

### Nested

```python
if user_exists:
    if password_correct:
        print("Login")
```

### Combined

```python
if user_exists and password_correct:
    print("Login")
```

The combined form is concise when both conditions are simple.

Nested logic can be useful when the second check should only happen after the first condition or when each level has its own logic.

---

# 49. What Happens With `None` in a Condition?

`None` is falsy.

```python
value = None

if value:
    print("Available")
else:
    print("No value")
```

Output:

```text
No value
```

To specifically check for `None`:

```python
if value is None:
    print("No value")
```

---

# 50. What Happens With an Empty Dictionary in a Condition?

An empty dictionary is falsy.

```python
data = {}

if data:
    print("Dictionary has data")
else:
    print("Dictionary is empty")
```

Output:

```text
Dictionary is empty
```

A non-empty dictionary is truthy.

---

# 51. What Happens With an Empty Set?

An empty set is falsy.

```python
data = set()

if data:
    print("Set has elements")
else:
    print("Set is empty")
```

Output:

```text
Set is empty
```

---

# 52. What Happens With an Empty Tuple?

An empty tuple is falsy.

```python
data = ()

if data:
    print("Tuple has elements")
else:
    print("Tuple is empty")
```

Output:

```text
Tuple is empty
```

---

# 53. What Happens With an Empty String?

An empty string is falsy.

```python
name = ""

if name:
    print("Name available")
else:
    print("Name missing")
```

Output:

```text
Name missing
```

---

# 54. What Happens With Negative Numbers in Conditions?

Negative non-zero numbers are truthy.

```python
x = -10

if x:
    print("Truthy")
```

Output:

```text
Truthy
```

Only zero is falsy among ordinary numeric values.

---

# 55. What Is the Difference Between `if not value` and `if value is None`?

They are not equivalent.

### `if not value`

Checks whether the value is falsy.

This includes:

```text
None
0
""
[]
{}
()
set()
```

### `if value is None`

Checks specifically whether the object is `None`.

Example:

```python
value = 0

if not value:
    print("Falsy")

if value is None:
    print("None")
```

Only `"Falsy"` is printed.

### Interview Answer

> `if not value` checks general truthiness, while `if value is None` specifically checks object identity with `None`.

---

# 56. How Can Conditions Be Used to Validate Input?

Example:

```python
age = int(input("Enter age: "))

if age < 0:
    print("Invalid age")
elif age < 18:
    print("Minor")
else:
    print("Adult")
```

The conditional structure validates the input and chooses the appropriate result.

---

# 57. Real-World Example — Login Validation

```python
username = "harsha"
password = "python123"

if username == "harsha" and password == "python123":
    print("Login successful")
else:
    print("Invalid credentials")
```

### Interview Explanation

> Conditional statements allow the application to compare the provided credentials with the expected values and choose the appropriate flow.

---

# 58. Real-World Example — Data Validation

Suppose a data pipeline receives a record:

```python
record = {
    "name": "Harsha",
    "age": 21
}

if record.get("name") and record.get("age") is not None:
    print("Valid record")
else:
    print("Invalid record")
```

This checks whether required fields are available.

### Data Engineering Connection

Conditions are commonly used for:

- Validating records
- Handling missing values
- Filtering data
- Applying business rules
- Classifying records
- Controlling ETL logic

---

# 59. Real-World Example — Data Classification

```python
amount = 15000

if amount >= 10000:
    category = "High"
elif amount >= 5000:
    category = "Medium"
else:
    category = "Low"

print(category)
```

Output:

```text
High
```

This kind of conditional classification can be used when applying business rules to data.

---

# 60. Real-World Example — File Processing

```python
file_type = "csv"

if file_type == "csv":
    print("Process CSV file")
elif file_type == "json":
    print("Process JSON file")
else:
    print("Unsupported file type")
```

This is a simple example of selecting processing logic based on input type.

---

# 61. Important Output-Based Interview Questions

## Question 1

```python
x = 10

if x > 5:
    print("A")
else:
    print("B")
```

### Answer

```text
A
```

---

## Question 2

```python
x = 3

if x > 5:
    print("A")
elif x > 2:
    print("B")
else:
    print("C")
```

### Answer

```text
B
```

---

## Question 3

```python
x = 10

if x > 0:
    print("Positive")

if x > 5:
    print("Greater")
```

### Answer

```text
Positive
Greater
```

Both `if` statements are independent.

---

## Question 4

```python
x = 10

if x > 0:
    print("Positive")
elif x > 5:
    print("Greater")
```

### Answer

```text
Positive
```

The `elif` is skipped.

---

## Question 5

```python
x = 0

if x:
    print("A")
else:
    print("B")
```

### Answer

```text
B
```

`0` is falsy.

---

## Question 6

```python
x = []

if x:
    print("A")
else:
    print("B")
```

### Answer

```text
B
```

An empty list is falsy.

---

## Question 7

```python
x = [1]

if x:
    print("A")
else:
    print("B")
```

### Answer

```text
A
```

A non-empty list is truthy.

---

## Question 8

```python
x = 10

if x > 5 and x < 20:
    print("A")
```

### Answer

```text
A
```

Both conditions are true.

---

## Question 9

```python
x = 10

if x < 5 or x > 8:
    print("A")
```

### Answer

```text
A
```

The second condition is true.

---

## Question 10

```python
x = False

if not x:
    print("A")
```

### Answer

```text
A
```

`not False` is `True`.

---

# 62. Important `and` / `or` Output Questions

## Question 1

```python
print(True and True)
```

### Answer

```text
True
```

---

## Question 2

```python
print(True and False)
```

### Answer

```text
False
```

---

## Question 3

```python
print(False or True)
```

### Answer

```text
True
```

---

## Question 4

```python
print(10 and 20)
```

### Answer

```text
20
```

---

## Question 5

```python
print(0 and 20)
```

### Answer

```text
0
```

---

## Question 6

```python
print(10 or 20)
```

### Answer

```text
10
```

---

## Question 7

```python
print(0 or 20)
```

### Answer

```text
20
```

---

## Question 8

```python
print("" or "Python")
```

### Answer

```text
Python
```

---

## Question 9

```python
print("Python" and "SQL")
```

### Answer

```text
SQL
```

---

## Question 10

```python
print([] or [1, 2])
```

### Answer

```text
[1, 2]
```

---

# 63. Important `is` vs `==` Interview Question

```python
a = [1, 2]
b = [1, 2]

print(a == b)
print(a is b)
```

### Answer

```text
True
False
```

### Explanation

The values are equal, but the two lists are separate objects.

---

# 64. Important Truthiness Interview Question

```python
values = [
    False,
    None,
    0,
    "",
    [],
    (),
    {},
    set()
]

for value in values:
    print(bool(value))
```

### Answer

All evaluate to:

```text
False
```

---

# 65. What Is a Common Mistake With `if` Conditions?

Using assignment instead of comparison.

Incorrect:

```python
if x = 10:
    print("Ten")
```

This is invalid syntax.

Correct:

```python
if x == 10:
    print("Ten")
```

---

# 66. What Is a Common Mistake With `is`?

Using `is` when value equality is intended.

Instead of:

```python
if name is "Harsha":
```

use:

```python
if name == "Harsha":
```

Use `is` for identity checks.

For example:

```python
if value is None:
```

---

# 67. What Is a Common Mistake With `elif` Ordering?

Conditions should generally be ordered from the most specific or restrictive case to the broader case.

Incorrect:

```python
marks = 95

if marks >= 40:
    print("Pass")
elif marks >= 90:
    print("A")
```

Output:

```text
Pass
```

The `elif` can never be reached for marks `90+`.

Better:

```python
if marks >= 90:
    print("A")
elif marks >= 40:
    print("Pass")
else:
    print("Fail")
```

Output:

```text
A
```

### Interview Insight

> In an `if-elif` chain, the order of conditions matters because Python executes the first matching branch.

---

# 68. How Do You Write a Grade Program Using Conditions?

```python
marks = 82

if marks >= 90:
    grade = "A"
elif marks >= 80:
    grade = "B"
elif marks >= 70:
    grade = "C"
elif marks >= 60:
    grade = "D"
else:
    grade = "F"

print(grade)
```

Output:

```text
B
```

---

# 69. How Do You Check Whether a Number Is Even or Odd?

```python
number = 10

if number % 2 == 0:
    print("Even")
else:
    print("Odd")
```

Output:

```text
Even
```

### Interview Explanation

> I use the modulus operator to check the remainder after division by 2. If the remainder is zero, the number is even; otherwise, it is odd.

---

# 70. How Do You Find the Largest of Two Numbers?

```python
a = 10
b = 20

if a > b:
    print(a)
else:
    print(b)
```

Output:

```text
20
```

---

# 71. How Do You Find the Largest of Three Numbers?

```python
a = 10
b = 25
c = 15

if a >= b and a >= c:
    largest = a
elif b >= a and b >= c:
    largest = b
else:
    largest = c

print(largest)
```

Output:

```text
25
```

---

# 72. How Do You Check Whether a Character Is a Vowel?

```python
char = "a"

if char.lower() in "aeiou":
    print("Vowel")
else:
    print("Consonant")
```

Output:

```text
Vowel
```

---

# 73. How Do You Check Whether a Year Is a Leap Year?

A year is a leap year when:

- It is divisible by 400, or
- It is divisible by 4 but not by 100.

```python
year = 2024

if year % 400 == 0 or (
    year % 4 == 0 and year % 100 != 0
):
    print("Leap year")
else:
    print("Not a leap year")
```

Output:

```text
Leap year
```

### Interview Explanation

> The condition handles the special century-year rule. Years divisible by 400 are leap years, while years divisible by 100 but not 400 are not.

---

# 74. How Do You Check Whether a Number Is Positive, Negative, or Zero?

```python
number = -10

if number > 0:
    print("Positive")
elif number < 0:
    print("Negative")
else:
    print("Zero")
```

Output:

```text
Negative
```

---

# 75. How Do You Validate a Range?

```python
age = 25

if 18 <= age <= 60:
    print("Within range")
else:
    print("Outside range")
```

Output:

```text
Within range
```

---

# 76. How Do You Combine Multiple Conditions Clearly?

Use parentheses when they improve readability.

```python
age = 25
has_id = True
is_member = False

if (age >= 18 and has_id) or is_member:
    print("Allowed")
else:
    print("Not allowed")
```

### Interview Tip

Even when Python's precedence rules make parentheses optional, using them can make business logic easier to understand.

---

# 77. How Are Conditions Used in ETL/Data Pipelines?

Conditions are commonly used to determine how data should be processed.

Example:

```python
record = {
    "amount": 15000,
    "status": "completed"
}

if record["status"] == "completed":
    if record["amount"] >= 10000:
        category = "high_value"
    else:
        category = "normal"
else:
    category = "ignore"

print(category)
```

Output:

```text
high_value
```

### Interview Answer

> In data processing, conditions are useful for validation, filtering, classification, handling missing values, and applying business rules before or during transformations.

---

# 78. Strong Interview Answer — What Are Conditional Statements?

### Question

> What are conditional statements in Python?

### Answer

> "Conditional statements allow us to control program flow based on conditions. Python provides `if`, `elif`, and `else` for decision-making. The condition is evaluated using Python's truth-value rules, and the appropriate block is executed based on the result."

---

# 79. Strong Interview Answer — `if` vs `if-elif`

### Question

> What is the difference between multiple `if` statements and an `if-elif` chain?

### Answer

> "Multiple `if` statements are independent, so more than one block can execute if multiple conditions are true. In an `if-elif-else` chain, Python checks the conditions from top to bottom and executes only the first matching branch."

---

# 80. Strong Interview Answer — Truthiness

### Question

> What does truthy and falsy mean in Python?

### Answer

> "Python allows objects to be used directly in conditions. Values such as `0`, `None`, empty strings, and empty collections are falsy, while most non-empty and non-zero values are truthy. Python uses this truth value to decide whether a conditional block should execute."

---

# 81. Strong Interview Answer — Short-Circuiting

### Question

> What is short-circuit evaluation?

### Answer

> "Short-circuit evaluation means Python stops evaluating a logical expression once its final result is already known. With `and`, a falsy left operand is enough to determine the result. With `or`, a truthy left operand is enough."

---

# 82. Strong Interview Answer — `==` vs `is`

### Question

> What is the difference between `==` and `is`?

### Answer

> "`==` checks value equality, whereas `is` checks object identity. For example, two separate lists can have the same contents and therefore be equal using `==`, but they are not necessarily the same object. I commonly use `is` when checking for `None`."

---

# 83. Strong Interview Answer — Ternary Expression

### Question

> Does Python have a ternary operator?

### Answer

> "Python provides a conditional expression rather than the traditional ternary syntax used in some other languages. The syntax is `value_if_true if condition else value_if_false`. I use it for simple conditions where it improves readability."

---

# 84. Strong Interview Answer — Why Conditions Matter in Data Engineering

### Question

> Why are conditional statements important for a data engineer?

### Answer

> "Conditions are important because data processing often involves business rules and validation. For example, I may need to check whether a record contains required fields, classify records based on values, handle missing data, or choose different processing logic depending on the input. Conditional statements provide the control flow for these decisions."

---

# 85. Placement-Focused Questions to Master

These are the questions that should be understood deeply for Python interviews:

1. What are conditional statements in Python?
2. What is an `if` statement?
3. What is `if-else`?
4. What is `if-elif-else`?
5. How does an `if-elif-else` chain execute?
6. Can multiple conditions be true in an `if-elif` chain?
7. What is the difference between multiple `if` statements and `if-elif`?
8. What is nested `if`?
9. What are logical operators?
10. Difference between `and`, `or`, and `not`.
11. What are comparison operators?
12. Difference between `=` and `==`.
13. Difference between `==` and `is`.
14. What is truthiness?
15. What are truthy values?
16. What are falsy values?
17. What does `bool()` do?
18. Why can collections be directly used in conditions?
19. What is a conditional expression?
20. What is a ternary expression?
21. When should a ternary expression be avoided?
22. What is short-circuit evaluation?
23. How does `and` short-circuit?
24. How does `or` short-circuit?
25. Do `and` and `or` return Boolean values?
26. What is logical operator precedence?
27. What are chained comparisons?
28. How do you check whether a value is in a range?
29. Difference between `if value` and `if value is None`.
30. How do you check multiple possible values?
31. Difference between `in` and `==`.
32. Is `else` mandatory?
33. Can `elif` exist without `if`?
34. Can there be multiple `elif` statements?
35. Can there be multiple `else` blocks?
36. How do you simplify nested conditions?
37. How do you validate user input using conditions?
38. How do you classify data using conditions?
39. How are conditions used in ETL pipelines?
40. How are conditions used in real-world applications?
41. What happens when no condition matches?
42. Why does condition order matter?
43. What is the difference between equality and identity?
44. Why should `is` commonly be used with `None`?
45. What happens when `0` is used as a condition?
46. What happens when an empty list is used as a condition?
47. What happens when an empty dictionary is used as a condition?
48. What happens when an empty string is used as a condition?
49. What happens when a negative number is used as a condition?
50. Predict the output of complex `and`/`or` expressions.

---

# 86. Final Quick Revision

Remember these core points before an interview:

```text
if
    -> Executes when condition is truthy

if-else
    -> Chooses between two paths

if-elif-else
    -> Chooses the first matching path

nested if
    -> if inside another conditional block

and
    -> Requires both operands to be truthy

or
    -> Requires at least one operand to be truthy

not
    -> Reverses truth value

==
    -> Value equality

is
    -> Object identity

in
    -> Membership testing

not in
    -> Negative membership testing

bool()
    -> Converts value to Boolean truth value

truthy
    -> Evaluates to True

falsy
    -> Evaluates to False

and/or
    -> Use short-circuit evaluation

ternary expression
    -> value_if_true if condition else value_if_false

chained comparison
    -> 18 <= age <= 60
```

## Final Interview-Level Understanding

> **Python conditionals are not only about `if` and `else`. A strong understanding includes Boolean logic, truthiness, comparison operators, identity versus equality, membership testing, short-circuit evaluation, operator precedence, chained comparisons, conditional expressions, and the way these concepts are applied to real-world validation and data-processing logic.**