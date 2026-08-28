# 16 — Exception Handling

## 1. What Is Exception Handling?

Exception handling is a mechanism in Python used to handle **runtime errors** without abruptly terminating the program.

For example:

```python
a = 10
b = 0

print(a / b)
```

This produces:

```text
ZeroDivisionError
```

If we handle the exception:

```python
a = 10
b = 0

try:
    print(a / b)
except ZeroDivisionError:
    print("Cannot divide by zero")
```

Output:

```text
Cannot divide by zero
```

The program can continue executing after handling the error.

---

# 2. Error vs Exception

These terms are related but should not be treated as exactly the same.

### Error

An error is a problem that prevents the program from working correctly.

Examples:

```text
SyntaxError
IndentationError
NameError
TypeError
ValueError
```

### Exception

An exception is an event that occurs during program execution and can generally be handled using `try`/`except`.

Example:

```python
try:
    number = int("abc")
except ValueError:
    print("Invalid number")
```

---

# 3. What Is an Exception?

An exception is an object representing an abnormal condition that occurs while the program is running.

Example:

```python
number = int("abc")
```

Python raises:

```text
ValueError
```

Instead of allowing the program to terminate, we can handle it:

```python
try:
    number = int("abc")
except ValueError:
    print("Please enter a valid number")
```

---

# 4. Why Do We Need Exception Handling?

Exception handling helps us:

- prevent unexpected program termination
- handle expected runtime problems
- provide meaningful error messages
- clean up resources
- separate normal program logic from error-handling logic
- make applications more robust

### Real-World Example

Suppose an application reads data from a file:

```python
try:
    with open("data.txt") as file:
        data = file.read()
except FileNotFoundError:
    print("The file does not exist")
```

Instead of crashing, the application can respond appropriately.

---

# 5. Basic `try` and `except`

The basic structure is:

```python
try:
    # code that may raise an exception
except:
    # code that handles the exception
```

Example:

```python
try:
    number = int(input("Enter a number: "))
    print(number)
except:
    print("Invalid input")
```

However, using a bare `except` is generally not recommended because it catches almost everything.

It is better to catch the specific exception:

```python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Please enter a valid number")
```

---

# 6. What Is the Purpose of `try`?

The `try` block contains code that may raise an exception.

Example:

```python
try:
    result = 10 / 0
```

Python detects the exception and looks for an appropriate `except` block.

---

# 7. What Is the Purpose of `except`?

The `except` block contains the code that handles an exception.

Example:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Division by zero is not allowed")
```

Output:

```text
Division by zero is not allowed
```

---

# 8. What Is `finally`?

The `finally` block executes whether an exception occurs or not.

Example:

```python
try:
    number = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
finally:
    print("Execution completed")
```

Output:

```text
5.0
Execution completed
```

If an exception occurs:

```python
try:
    number = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
finally:
    print("Execution completed")
```

Output:

```text
Cannot divide by zero
Execution completed
```

---

# 9. Why Is `finally` Useful?

`finally` is commonly used for cleanup operations.

Examples:

- closing resources
- releasing connections
- cleaning temporary resources
- closing files
- releasing locks

Example:

```python
file = None

try:
    file = open("data.txt", "r")
    data = file.read()
except FileNotFoundError:
    print("File not found")
finally:
    if file:
        file.close()
```

In modern Python, `with open(...)` is generally preferred for file handling because it manages closing automatically.

---

# 10. What Is `else` in Exception Handling?

The `else` block executes **only when no exception occurs in the `try` block**.

Example:

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("Result:", result)
```

Output:

```text
Result: 5.0
```

If an exception occurs, the `else` block is skipped.

---

# 11. `try-except-else-finally`

Python allows all four blocks:

```python
try:
    # risky code
except SomeException:
    # handle exception
else:
    # executes if no exception
finally:
    # executes regardless
```

Example:

```python
try:
    number = int("10")
except ValueError:
    print("Invalid number")
else:
    print("Valid number:", number)
finally:
    print("Finished")
```

Output:

```text
Valid number: 10
Finished
```

---

# 12. Execution Flow of Exception Handling

The flow is:

```text
try
 ↓
Exception?
 ├── Yes → matching except
 │
 └── No  → else
            ↓
         finally
```

Important:

```text
finally
```

is normally executed regardless of whether an exception occurred.

---

# 13. Common Built-in Exceptions

Some important Python exceptions are:

| Exception | Common cause |
|---|---|
| `ValueError` | Invalid value |
| `TypeError` | Invalid operation/type |
| `NameError` | Variable/name not defined |
| `IndexError` | Invalid list/sequence index |
| `KeyError` | Missing dictionary key |
| `ZeroDivisionError` | Division by zero |
| `FileNotFoundError` | File does not exist |
| `AttributeError` | Invalid attribute |
| `ImportError` | Import problem |
| `ModuleNotFoundError` | Module cannot be found |
| `TypeError` | Incompatible types |
| `OverflowError` | Numeric result too large |
| `RuntimeError` | Generic runtime problem |

---

# 14. `ValueError`

A `ValueError` occurs when the type is appropriate but the value is invalid.

Example:

```python
number = int("abc")
```

Handle it:

```python
try:
    number = int("abc")
except ValueError:
    print("Invalid numeric value")
```

Output:

```text
Invalid numeric value
```

---

# 15. `TypeError`

A `TypeError` occurs when an operation is applied to an inappropriate type.

Example:

```python
result = "10" + 5
```

Handle it:

```python
try:
    result = "10" + 5
except TypeError:
    print("Incompatible types")
```

---

# 16. `IndexError`

An `IndexError` occurs when an index is outside the valid range.

Example:

```python
numbers = [10, 20, 30]

print(numbers[5])
```

Handle it:

```python
try:
    print(numbers[5])
except IndexError:
    print("Index is out of range")
```

---

# 17. `KeyError`

A `KeyError` occurs when trying to access a dictionary key that does not exist.

Example:

```python
data = {
    "name": "Harsha"
}

print(data["age"])
```

Handle it:

```python
try:
    print(data["age"])
except KeyError:
    print("Key does not exist")
```

---

# 18. `NameError`

A `NameError` occurs when Python cannot find a variable or name.

Example:

```python
print(age)
```

If `age` was never defined, Python raises:

```text
NameError
```

---

# 19. `ZeroDivisionError`

Example:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

Output:

```text
Cannot divide by zero
```

---

# 20. `FileNotFoundError`

Example:

```python
try:
    with open("missing.txt", "r") as file:
        data = file.read()
except FileNotFoundError:
    print("File not found")
```

This is a practical exception when working with files.

---

# 21. Handling Multiple Exceptions

We can use multiple `except` blocks.

```python
try:
    number = int(input("Enter number: "))
    result = 10 / number
except ValueError:
    print("Invalid input")
except ZeroDivisionError:
    print("Cannot divide by zero")
```

Each exception can have its own handling logic.

---

# 22. Can One `except` Handle Multiple Exceptions?

Yes.

```python
try:
    number = int(input("Enter number: "))
    result = 10 / number
except (ValueError, ZeroDivisionError):
    print("Invalid operation")
```

This is useful when different exceptions require the same handling.

---

# 23. How Do You Get the Exception Message?

We can use:

```python
as
```

Example:

```python
try:
    number = int("abc")
except ValueError as e:
    print(e)
```

Output:

```text
invalid literal for int() with base 10: 'abc'
```

The variable `e` contains the exception object.

---

# 24. What Is the Difference Between `except Exception` and Bare `except`?

A bare:

```python
except:
```

catches almost all exceptions, including exceptions such as `KeyboardInterrupt` and `SystemExit`.

Using:

```python
except Exception:
```

catches exceptions derived from the normal `Exception` hierarchy.

Generally, this is safer than a bare `except`, but catching the **specific expected exception** is usually better.

Example:

```python
try:
    number = int("abc")
except ValueError:
    print("Invalid number")
```

This makes the intention clear.

---

# 25. Why Should We Avoid Bare `except`?

Consider:

```python
try:
    risky_operation()
except:
    print("Something went wrong")
```

The problem is that it may hide unexpected problems and make debugging difficult.

Prefer:

```python
try:
    risky_operation()
except ValueError:
    print("Invalid value")
```

Or, when a broader boundary is genuinely required:

```python
try:
    risky_operation()
except Exception as e:
    print("Unexpected application error:", e)
```

---

# 26. What Is Exception Propagation?

If an exception is not handled in the current function, it can propagate to the caller.

Example:

```python
def divide():
    return 10 / 0


def calculate():
    return divide()


try:
    calculate()
except ZeroDivisionError:
    print("Handled in caller")
```

Output:

```text
Handled in caller
```

The exception propagated from:

```text
divide()
   ↓
calculate()
   ↓
try/except
```

---

# 27. What Is `raise`?

The `raise` statement is used to explicitly raise an exception.

Example:

```python
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")
```

Output:

```text
ValueError: Age cannot be negative
```

---

# 28. Why Use `raise`?

We use `raise` when we want to explicitly signal that something is invalid.

Example:

```python
def withdraw(balance, amount):
    if amount > balance:
        raise ValueError("Insufficient balance")

    return balance - amount
```

The function clearly communicates that the input is invalid for the operation.

---

# 29. Raising a Specific Exception

```python
def set_age(age):
    if age < 0:
        raise ValueError("Age must be positive")

    return age
```

Usage:

```python
try:
    set_age(-10)
except ValueError as e:
    print(e)
```

Output:

```text
Age must be positive
```

---

# 30. What Is a Custom Exception?

A custom exception is an exception class created by the programmer for application-specific problems.

Example:

```python
class InsufficientBalanceError(Exception):
    pass
```

Use it:

```python
balance = 100

if balance < 500:
    raise InsufficientBalanceError("Insufficient balance")
```

---

# 31. Custom Exception With a Function

```python
class InsufficientBalanceError(Exception):
    pass


def withdraw(balance, amount):
    if amount > balance:
        raise InsufficientBalanceError("Insufficient balance")

    return balance - amount


try:
    print(withdraw(100, 500))
except InsufficientBalanceError as e:
    print(e)
```

Output:

```text
Insufficient balance
```

---

# 32. Why Use Custom Exceptions?

Custom exceptions make application-specific errors clearer.

For example, instead of:

```python
raise Exception("Problem")
```

we can use:

```python
raise InsufficientBalanceError("Insufficient balance")
```

This allows the calling code to handle that specific condition.

---

# 33. Exception Hierarchy

Python exceptions follow a class hierarchy.

A simplified structure is:

```text
BaseException
│
├── KeyboardInterrupt
├── SystemExit
├── GeneratorExit
│
└── Exception
    ├── ArithmeticError
    │   ├── ZeroDivisionError
    │   └── OverflowError
    │
    ├── LookupError
    │   ├── IndexError
    │   └── KeyError
    │
    ├── ValueError
    ├── TypeError
    ├── OSError
    │   ├── FileNotFoundError
    │   └── PermissionError
    └── ...
```

Understanding the hierarchy helps when deciding what exception to catch.

---

# 34. Why Does the Order of `except` Blocks Matter?

More specific exceptions should generally be handled before broader exceptions.

Incorrect ordering:

```python
try:
    number = int("abc")
except Exception:
    print("General exception")
except ValueError:
    print("Value error")
```

The `ValueError` block will never be reached because `Exception` catches it first.

Better:

```python
try:
    number = int("abc")
except ValueError:
    print("Value error")
except Exception:
    print("Other exception")
```

---

# 35. What Is Exception Chaining?

Python can preserve the relationship between one exception and another when an exception is raised while handling a previous exception.

Example:

```python
try:
    number = int("abc")
except ValueError as e:
    raise RuntimeError("Unable to process input") from e
```

The `from e` explicitly records the original exception as the cause.

This is useful when converting low-level errors into application-level errors while preserving the original cause for debugging.

---

# 36. What Is `raise` Without an Exception?

Inside an `except` block, we can use:

```python
raise
```

to re-raise the currently handled exception.

Example:

```python
try:
    number = int("abc")
except ValueError:
    print("Logging error")
    raise
```

The exception is logged and then propagated to the caller.

---

# 37. Why Is Re-Raising Useful?

Suppose a lower-level function needs to log an error but should not completely handle it.

```python
def process():
    try:
        number = int("abc")
    except ValueError:
        print("Logging error")
        raise
```

The caller can then decide how to handle the exception.

This separates:

```text
logging
```

from:

```text
final error handling
```

---

# 38. What Happens If an Exception Occurs in `else`?

The `else` block only means that the `try` block completed successfully.

If the `else` block itself raises an exception, that exception is not handled by the preceding `except` blocks.

Example:

```python
try:
    value = 10
except ValueError:
    print("Value error")
else:
    print(10 / 0)
```

The `ZeroDivisionError` occurs in `else` and is not caught by the `ValueError` handler.

---

# 39. What Happens If an Exception Occurs in `finally`?

An exception raised in `finally` can override an exception that was already being propagated.

Example:

```python
try:
    raise ValueError("Original error")
finally:
    raise RuntimeError("Finally error")
```

The `RuntimeError` becomes the exception that propagates.

Therefore, `finally` should normally be used for cleanup and should not unnecessarily raise new exceptions.

---

# 40. What Happens If `return` Is Used in `finally`?

This is an important interview edge case.

Example:

```python
def test():
    try:
        return 10
    finally:
        return 20


print(test())
```

Output:

```text
20
```

The `return` in `finally` overrides the earlier return.

Because this can make control flow confusing, returning from `finally` is generally discouraged.

---

# 41. `finally` With `return`

Example:

```python
def test():
    try:
        return "try"
    finally:
        print("finally")


print(test())
```

Output:

```text
finally
try
```

The `finally` block executes before the function actually returns.

---

# 42. Exception Handling With File Operations

A practical example:

```python
try:
    with open("data.txt", "r") as file:
        data = file.read()
        print(data)

except FileNotFoundError:
    print("The file was not found")

except PermissionError:
    print("Permission denied")
```

This handles two common file-related problems.

The `with` statement also manages the file resource automatically.

---

# 43. Exception Handling With User Input

```python
try:
    age = int(input("Enter your age: "))
    print("Age:", age)

except ValueError:
    print("Please enter a valid integer")
```

This prevents invalid input from crashing the application.

---

# 44. Exception Handling in a Data Processing Scenario

Suppose records contain values that need conversion:

```python
records = ["10", "20", "abc", "40"]

for record in records:
    try:
        number = int(record)
        print(number * 2)
    except ValueError:
        print("Skipping invalid record:", record)
```

Output:

```text
20
40
Skipping invalid record: abc
80
```

This is a practical example of handling bad records without stopping the entire processing loop.

---

# 45. Exception Handling in Data Engineering

In data processing, individual records may sometimes contain invalid data.

For example:

```python
records = [
    {"amount": "100"},
    {"amount": "200"},
    {"amount": "invalid"},
    {"amount": "300"}
]

for record in records:
    try:
        amount = float(record["amount"])
        print(amount)
    except (ValueError, KeyError) as e:
        print("Invalid record:", record)
```

Possible output:

```text
100.0
200.0
Invalid record: {'amount': 'invalid'}
300.0
```

A robust pipeline may log the invalid record, send it to a rejected/error dataset, and continue processing valid records depending on the business requirements.

---

# 46. Should We Catch Every Exception in a Data Pipeline?

No.

A good design is to catch exceptions that we can meaningfully handle.

For example:

```python
try:
    amount = float(record["amount"])
except (ValueError, KeyError):
    # Handle known bad data
    ...
```

But blindly doing:

```python
except Exception:
    pass
```

can hide serious programming or infrastructure problems.

---

# 47. What Is `pass` in Exception Handling?

Sometimes we intentionally do nothing.

```python
try:
    number = int("abc")
except ValueError:
    pass
```

However, silently ignoring exceptions is usually not a good production practice unless the exception is genuinely expected and irrelevant.

Better:

```python
try:
    number = int("abc")
except ValueError:
    number = 0
```

or log/handle the condition appropriately.

---

# 48. Exception Handling vs Validation

These are related but different.

### Validation

Checks whether input is acceptable.

```python
if age < 0:
    print("Invalid age")
```

### Exception handling

Handles an exceptional condition raised during execution.

```python
try:
    age = int(user_input)
except ValueError:
    print("Invalid integer")
```

Validation and exceptions can work together.

---

# 49. When Should You Raise an Exception Instead of Returning `None`?

It depends on the contract of the function.

If invalid input represents an error that the caller must handle, raising a meaningful exception can be appropriate.

Example:

```python
def divide(a, b):
    if b == 0:
        raise ValueError("Denominator cannot be zero")

    return a / b
```

The caller can decide how to handle it.

---

# 50. Exception Handling Best Practices

### 1. Catch specific exceptions

Prefer:

```python
except ValueError:
```

over:

```python
except:
```

### 2. Don't silently ignore errors

Avoid:

```python
except Exception:
    pass
```

unless there is a clear reason.

### 3. Keep `try` blocks focused

Instead of:

```python
try:
    # 30 lines of unrelated code
```

keep the risky operation relatively small.

### 4. Use meaningful custom exceptions

For application-specific failures:

```python
class PaymentError(Exception):
    pass
```

### 5. Use `finally` or context managers for cleanup

For example:

```python
with open("data.txt") as file:
    ...
```

### 6. Preserve useful context

When translating exceptions, exception chaining can help:

```python
raise ApplicationError("Processing failed") from e
```

---

# 51. Common Interview Question — What Is the Difference Between `try`, `except`, `else`, and `finally`?

### `try`

Contains code that may raise an exception.

### `except`

Handles a matching exception.

### `else`

Runs when the `try` block completes without an exception.

### `finally`

Runs regardless of whether an exception occurred.

### Strong Interview Answer

> `try` contains potentially risky code, `except` handles matching exceptions, `else` runs when no exception occurs in the `try` block, and `finally` is used for cleanup that should happen regardless of the result.

---

# 52. Common Interview Question — What Is the Difference Between `raise` and `except`?

`except` is used to **handle** an exception.

```python
try:
    ...
except ValueError:
    ...
```

`raise` is used to **create or propagate** an exception.

```python
raise ValueError("Invalid value")
```

### Strong Answer

> `except` handles an exception, while `raise` explicitly raises an exception or re-raises the current exception.

---

# 53. Common Interview Question — What Is the Difference Between `raise` and `raise e`?

Inside an exception handler:

```python
except Exception:
    raise
```

re-raises the current exception.

```python
except Exception as e:
    raise e
```

raises the exception object explicitly.

For simply propagating the currently handled exception, the bare:

```python
raise
```

is generally preferred because it preserves the original traceback more directly.

---

# 54. Common Interview Question — Can We Have `try` Without `except`?

Yes, if it has `finally`.

Example:

```python
try:
    print("Hello")
finally:
    print("Cleanup")
```

Output:

```text
Hello
Cleanup
```

A `try` statement must have at least one of:

```text
except
else
finally
```

and `else` cannot appear without an `except`.

---

# 55. Common Interview Question — Can We Have Multiple `except` Blocks?

Yes.

```python
try:
    number = int(input())
    result = 10 / number

except ValueError:
    print("Invalid input")

except ZeroDivisionError:
    print("Cannot divide by zero")
```

Python checks the exception handlers for a matching exception.

---

# 56. Common Interview Question — Can We Have Multiple Exceptions in One `except`?

Yes.

```python
try:
    ...
except (ValueError, TypeError):
    print("Invalid operation")
```

This is useful when the handling logic is identical.

---

# 57. Common Interview Question — What Is a Custom Exception?

Strong answer:

> A custom exception is a user-defined exception class created for application-specific error conditions. It normally inherits from `Exception`, allowing the application to catch and handle that particular error separately.

Example:

```python
class InvalidAgeError(Exception):
    pass
```

---

# 58. Common Interview Question — Why Inherit Custom Exceptions From `Exception`?

Example:

```python
class InvalidAgeError(Exception):
    pass
```

`Exception` is the standard base class for normal application exceptions.

This allows:

```python
except InvalidAgeError:
```

and also:

```python
except Exception:
```

to catch it.

---

# 59. Common Interview Question — What Is Exception Propagation?

Strong answer:

> Exception propagation means that when an exception is not handled in the current function, Python passes it back through the calling functions until a matching exception handler is found. If no handler is found, the program terminates with a traceback.

---

# 60. Common Interview Question — What Is the Difference Between Syntax Error and Runtime Exception?

### Syntax error

The Python code does not follow valid Python syntax.

Example:

```python
if True
    print("Hello")
```

Python cannot properly parse it.

### Runtime exception

The code is syntactically valid but encounters a problem while executing.

Example:

```python
print(10 / 0)
```

This raises:

```text
ZeroDivisionError
```

### Strong Answer

> A syntax error occurs when Python cannot parse the code, while a runtime exception occurs during execution after the code has been successfully parsed.

---

# 61. Common Interview Question — Does Exception Handling Make Errors Disappear?

No.

Exception handling determines **how the program responds to an exception**.

For example:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Handled")
```

The division is still invalid. We have simply handled the resulting exception.

---

# 62. Common Interview Question — Is Exception Handling Expensive?

There is some runtime overhead associated with exceptions, but the bigger design concern is using exceptions appropriately.

Exceptions should generally represent exceptional/error conditions rather than being used as the normal control-flow mechanism when ordinary checks are clearer.

---

# 63. Common Interview Question — Why Should We Not Use Exceptions for Normal Control Flow?

Suppose we want to check whether a dictionary key exists.

Instead of unnecessarily doing:

```python
try:
    value = data["name"]
except KeyError:
    value = None
```

we could use:

```python
value = data.get("name")
```

when that behavior matches our requirement.

Exceptions are valuable for exceptional conditions, but normal logic should remain clear and simple.

---

# 64. Common Coding Question — Safe Division

### Question

Write a function that divides two numbers and handles division by zero.

### Answer

```python
def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"


print(divide(10, 2))
print(divide(10, 0))
```

Output:

```text
5.0
Cannot divide by zero
```

---

# 65. Common Coding Question — Handle Invalid Integer Input

```python
def convert_to_int(value):
    try:
        return int(value)
    except ValueError:
        return None


print(convert_to_int("100"))
print(convert_to_int("abc"))
```

Output:

```text
100
None
```

---

# 66. Common Coding Question — Handle Missing Dictionary Key

```python
def get_age(data):
    try:
        return data["age"]
    except KeyError:
        return "Age not available"


print(get_age({"name": "Harsha"}))
```

Output:

```text
Age not available
```

In this particular case, another clean option is:

```python
def get_age(data):
    return data.get("age", "Age not available")
```

The choice depends on whether a missing key is expected normal behavior or represents an exceptional condition.

---

# 67. Common Coding Question — Custom Exception

```python
class NegativeNumberError(Exception):
    pass


def square_root_input(number):
    if number < 0:
        raise NegativeNumberError("Number cannot be negative")

    return number


try:
    print(square_root_input(-5))
except NegativeNumberError as e:
    print(e)
```

Output:

```text
Number cannot be negative
```

---

# 68. Common Coding Question — `try-except-else-finally`

```python
try:
    number = int("100")
except ValueError:
    print("Invalid value")
else:
    print("Number:", number)
finally:
    print("Finished")
```

Output:

```text
Number: 100
Finished
```

---

# 69. Common Output Question

```python
try:
    print(10 / 0)
except ZeroDivisionError:
    print("Error")
finally:
    print("Done")
```

Output:

```text
Error
Done
```

---

# 70. Common Output Question

```python
try:
    print("A")
except:
    print("B")
else:
    print("C")
finally:
    print("D")
```

Output:

```text
A
C
D
```

Because no exception occurs.

---

# 71. Common Output Question

```python
try:
    print("A")
    print(10 / 0)
except ZeroDivisionError:
    print("B")
else:
    print("C")
finally:
    print("D")
```

Output:

```text
A
B
D
```

The `else` block is skipped because an exception occurred.

---

# 72. Common Output Question

```python
def test():
    try:
        return 10
    finally:
        return 20


print(test())
```

Output:

```text
20
```

The `finally` return overrides the earlier return.

---

# 73. Common Output Question

```python
def test():
    try:
        return 10
    finally:
        print("Finally")


print(test())
```

Output:

```text
Finally
10
```

The `finally` block executes before the function returns.

---

# 74. Common Output Question — Exception Propagation

```python
def first():
    raise ValueError("Error")


def second():
    first()


try:
    second()
except ValueError as e:
    print(e)
```

Output:

```text
Error
```

The exception propagates from `first()` to `second()` and is handled by the caller.

---

# 75. Interview Scenario — API/Data Processing

### Interviewer:

> Suppose you are processing 10,000 records and one record contains invalid data. Would you use exception handling?

### Good Answer:

> Yes, if invalid records are an expected possibility, I can catch the specific exceptions around the conversion or validation that may fail. I would log or move the invalid record to an error or rejected-data flow according to the application's requirements, while continuing with valid records. I would avoid catching every exception blindly because that could hide genuine application or infrastructure problems.

---

# 76. Interview Scenario — File Processing

### Interviewer:

> What happens if the input file doesn't exist?

### Good Answer:

> Opening the file can raise `FileNotFoundError`. I can catch that specific exception and provide an appropriate message or fallback behavior. For production code, I would also consider logging the failure so that the issue can be investigated.

Example:

```python
try:
    with open("data.csv", "r") as file:
        data = file.read()
except FileNotFoundError:
    print("Input file not found")
```

---

# 77. Interview Scenario — Database Connection

A database operation can fail for different reasons such as:

```text
connection failure
authentication problem
timeout
invalid query
```

The exact exceptions depend on the database library being used.

The general approach is:

```python
try:
    # database operation
    pass
except SomeDatabaseException as e:
    # log and handle appropriately
    print(e)
```

The important principle is to catch the specific exceptions provided by the library rather than using a blanket handler for everything.

---

# 78. Interview Scenario — Logging Errors

A production application should generally record useful error information.

For example:

```python
import logging

logging.basicConfig(level=logging.ERROR)

try:
    result = 10 / 0
except ZeroDivisionError:
    logging.exception("Division failed")
```

`logging.exception()` is useful inside an exception handler because it includes traceback information.

---

# 79. Exception Handling vs Logging

These are not the same.

### Exception handling

Determines what the program does when an exception occurs.

```python
try:
    ...
except ValueError:
    ...
```

### Logging

Records information about what happened.

```python
logging.exception("Processing failed")
```

In production systems, they are often used together.

---

# 80. Exception Handling in ETL Pipelines

For an ETL-style process:

```text
Extract
   ↓
Transform
   ↓
Load
```

exceptions can occur at each stage.

Example:

```python
try:
    data = extract_data()
    transformed = transform_data(data)
    load_data(transformed)

except ValueError as e:
    print("Data validation failed:", e)
```

In a real application, different failure categories may be handled differently:

```text
Bad record
   ↓
Log / reject record

Temporary service failure
   ↓
Retry according to policy

Fatal configuration problem
   ↓
Stop pipeline and alert
```

The important point is that exception handling should match the type and recoverability of the failure.

---

# 81. Retry vs Exception Handling

Exception handling and retry are related but not identical.

Catching an exception:

```python
try:
    operation()
except SomeError:
    print("Operation failed")
```

does not automatically retry.

A retry mechanism must explicitly attempt the operation again and should normally have:

- a maximum retry count
- appropriate delay/backoff
- handling for permanent failures

For example:

```python
for attempt in range(3):
    try:
        operation()
        break
    except TemporaryError:
        if attempt == 2:
            raise
```

Retry should only be used when the failure is reasonably expected to be temporary.

---

# 82. Exception Handling and `with`

Context managers are useful for resource management.

Instead of:

```python
file = open("data.txt")

try:
    data = file.read()
finally:
    file.close()
```

we normally use:

```python
with open("data.txt") as file:
    data = file.read()
```

The context manager handles cleanup automatically.

This reduces the amount of manual exception-related cleanup code.

---

# 83. Important Interview Question — Why Use `with` Instead of `finally` for Files?

Strong answer:

> `finally` can be used to guarantee cleanup, but a context manager using `with` is usually cleaner and less error-prone for resources such as files. The context manager handles entering and exiting the resource correctly, including when an exception occurs.

---

# 84. Important Interview Question — Can `finally` Execute if There Is a `return`?

Yes.

Example:

```python
def test():
    try:
        return 10
    finally:
        print("Cleanup")


print(test())
```

Output:

```text
Cleanup
10
```

The `finally` block executes before the function returns.

---

# 85. Important Interview Question — Can We Raise an Exception From Inside `except`?

Yes.

```python
try:
    number = int("abc")
except ValueError as e:
    raise RuntimeError("Input processing failed") from e
```

This is useful when a lower-level exception needs to be converted into a more meaningful application-level exception while preserving the original cause.

---

# 86. Important Interview Question — What Is the Difference Between Handling and Suppressing an Exception?

### Handling

We respond meaningfully:

```python
try:
    number = int(value)
except ValueError:
    print("Invalid input")
```

### Suppressing

We intentionally ignore the exception:

```python
try:
    number = int(value)
except ValueError:
    pass
```

Suppression should be used carefully because silently ignoring errors can make problems difficult to diagnose.

---

# 87. Important Interview Question — What Is a Traceback?

A traceback is the information Python displays when an exception propagates without being handled, showing the call stack and where the exception occurred.

Example:

```text
Traceback (most recent call last):
  ...
ValueError: invalid literal ...
```

A traceback helps developers identify:

- where the error occurred
- which functions were involved
- what exception was raised

---

# 88. Important Interview Question — Why Is the Traceback Useful?

It provides the execution path leading to the exception.

For example:

```text
main()
 ↓
process_data()
 ↓
convert_record()
 ↓
ValueError
```

This makes debugging easier.

---

# 89. Important Interview Question — Should We Catch `Exception`?

Only when there is a clear reason.

For example, at an application boundary, broad handling may be useful for logging and controlled failure:

```python
try:
    run_application()
except Exception:
    logging.exception("Unexpected application failure")
```

But inside normal business logic, catching specific exceptions is generally preferable.

---

# 90. Important Interview Question — What Does "Fail Fast" Mean?

Fail fast means detecting an invalid or unrecoverable condition as early as possible instead of allowing the program to continue with corrupted or invalid state.

Example:

```python
def process_age(age):
    if age < 0:
        raise ValueError("Invalid age")

    # Continue only with valid state
```

This makes errors easier to detect and prevents invalid data from spreading through the application.

---

# 91. Important Interview Question — What Is Defensive Programming?

Defensive programming means writing code that anticipates invalid inputs and failure conditions.

Example:

```python
def divide(a, b):
    if b == 0:
        raise ValueError("b cannot be zero")

    return a / b
```

The function clearly defines how invalid input is handled.

---

# 92. Important Interview Question — What Should You Include in an Exception Message?

A useful exception message should explain what went wrong and provide enough context to diagnose the problem.

Instead of:

```python
raise ValueError("Error")
```

prefer something meaningful:

```python
raise ValueError("Age must be greater than or equal to 0")
```

Avoid putting sensitive information such as passwords, access tokens, or other secrets into exception messages or logs.

---

# 93. Important Interview Question — What Is the Best Way to Handle Exceptions?

There is no single universal pattern.

A good general approach is:

```text
Identify expected failure
        ↓
Catch specific exception
        ↓
Handle/log/recover appropriately
        ↓
Propagate if the current layer cannot handle it
```

Avoid:

```python
except:
    pass
```

as a general strategy.

---

# 94. Core Exception Handling Checklist

Before an interview, make sure you can explain and demonstrate:

- [ ] What is an exception?
- [ ] What is exception handling?
- [ ] `try`
- [ ] `except`
- [ ] `else`
- [ ] `finally`
- [ ] `raise`
- [ ] `raise` vs `raise e`
- [ ] `StopIteration` as an exception from iterators
- [ ] common built-in exceptions
- [ ] multiple `except` blocks
- [ ] multiple exceptions in one `except`
- [ ] exception messages using `as e`
- [ ] exception propagation
- [ ] custom exceptions
- [ ] exception hierarchy
- [ ] exception chaining
- [ ] `with` and resource cleanup
- [ ] specific vs broad exception handling
- [ ] logging exceptions
- [ ] handling errors in data processing
- [ ] retry vs exception handling

---

# 95. Most Important Questions to Prepare First

If you have limited preparation time, prioritize these:

1. What is exception handling?
2. Why do we need exception handling?
3. Explain `try`, `except`, `else`, and `finally`.
4. What is the difference between `raise` and `except`?
5. What is `raise` used for?
6. What is exception propagation?
7. What is a custom exception?
8. Why should we catch specific exceptions?
9. Why should we avoid bare `except`?
10. What is the difference between `ValueError` and `TypeError`?
11. What is `KeyError`?
12. What is `IndexError`?
13. What is `ZeroDivisionError`?
14. What is `FileNotFoundError`?
15. Can one `except` handle multiple exceptions?
16. Why does the order of `except` blocks matter?
17. What is exception chaining?
18. What does `raise` without an argument do?
19. Why is `finally` useful?
20. Can `finally` execute when there is a `return`?
21. Why use `with` for resource management?
22. How would you handle invalid records in a data pipeline?
23. How would you handle a file-processing failure?
24. How would you log an exception?
25. When would you retry an operation?

---

# 96. Final Interview Summary

The core structure to remember is:

```text
try
  ↓
Risky operation
  ↓
Exception?
  ├── Yes → except
  │
  └── No  → else
              ↓
           finally
```

The most important keywords are:

```python
try
except
else
finally
raise
```

And the most important principles are:

```text
Catch specific exceptions
        ↓
Handle what you can recover from
        ↓
Log useful information
        ↓
Propagate what the current layer cannot handle
        ↓
Use finally/context managers for cleanup
```

### Final Interview Answer

> Exception handling in Python is used to manage runtime problems without allowing the application to fail unexpectedly. I can use `try` for potentially risky code, `except` to handle specific exceptions, `else` for code that should run when no exception occurs, and `finally` for cleanup. I can also use `raise` to explicitly signal an invalid condition and create custom exceptions for application-specific errors. In production code, I prefer catching specific exceptions, logging useful information, and allowing exceptions to propagate when the current layer cannot meaningfully handle them.