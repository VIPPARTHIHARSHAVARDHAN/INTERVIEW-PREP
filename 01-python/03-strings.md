# Python Strings — Interview Preparation

## 1. What Is a String in Python?

A **string** is an ordered sequence of Unicode characters used to represent text.

Strings can be created using:

- Single quotes `'...'`
- Double quotes `"..."`
- Triple single quotes `'''...'''`
- Triple double quotes `"""..."""`

### Example

```python
name = "Harsha"
language = 'Python'
message = """Python is widely used in data engineering."""

print(name)
print(language)
print(message)
```

### Output

```text
Harsha
Python
Python is widely used in data engineering.
```

### Real-World Example

In a data engineering project, strings are commonly used for:

```python
file_name = "youtube_data.csv"
bucket_name = "de-on-youtube-raw"
table_name = "youtube_statistics"
```

These represent filenames, AWS resource names, database table names, paths, API responses, and other textual data.

---

# 2. Are Strings Mutable or Immutable in Python?

Strings are **immutable**.

Once a string object is created, its individual characters cannot be changed.

### Example

```python
name = "Harsha"

name[0] = "X"
```

This produces:

```text
TypeError: 'str' object does not support item assignment
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

The original string was not modified. A new string object was created.

### Interview Answer

> Strings are immutable in Python, which means their existing characters cannot be changed in place. Any operation that appears to modify a string actually creates a new string object.

---

# 3. Why Are Strings Immutable?

String immutability provides several advantages:

- Strings can be safely shared between different parts of a program.
- Strings can be hashable and therefore used as dictionary keys.
- Python can optimize and reuse some string objects internally.
- It prevents accidental modification of text data.

### Example

```python
name = "Harsha"

data = {
    name: "Data Engineer"
}

print(data)
```

A string can be used as a dictionary key because strings are immutable and hashable.

### Important Interview Point

Do not say:

> "Strings cannot be changed at all."

A more accurate statement is:

> "An existing string object cannot be modified in place, but a variable can be reassigned to another string."

Example:

```python
name = "Harsha"

name = "Rahul"

print(name)
```

Output:

```text
Rahul
```

The variable was reassigned; the original string object was not modified.

---

# 4. How Do You Access Characters in a String?

Strings support indexing.

Python uses **zero-based indexing**.

### Example

```python
name = "Harsha"

print(name[0])
print(name[1])
print(name[4])
```

### Output

```text
H
a
h
```

The indexes are:

```text
H  a  r  s  h  a
0  1  2  3  4  5
```

---

# 5. What Is Negative Indexing in Strings?

Negative indexing allows us to access characters starting from the end.

```text
H  a  r  s  h  a
0  1  2  3  4  5
-6 -5 -4 -3 -2 -1
```

### Example

```python
name = "Harsha"

print(name[-1])
print(name[-2])
```

### Output

```text
a
h
```

### Interview Tip

Remember:

```python
string[-1]
```

returns the **last character**.

---

# 6. What Happens If You Access an Invalid String Index?

Python raises an `IndexError`.

### Example

```python
name = "Harsha"

print(name[10])
```

Output:

```text
IndexError: string index out of range
```

### Interview Follow-Up

**Question:** What happens when slicing goes beyond the string length?

Slicing is more forgiving.

```python
name = "Harsha"

print(name[2:20])
```

Output:

```text
rsha
```

It does not raise an `IndexError` merely because the stop index exceeds the string length.

---

# 7. What Is String Slicing?

Slicing extracts a portion of a string.

The syntax is:

```python
string[start:stop:step]
```

The `stop` index is excluded.

### Example

```python
name = "Harsha"

print(name[1:4])
```

### Output

```text
ars
```

The indexes are:

```text
H a r s h a
0 1 2 3 4 5
```

So `[1:4]` returns indexes `1`, `2`, and `3`.

---

# 8. How Do You Reverse a String?

A common Python technique is slicing with a step of `-1`.

```python
name = "Harsha"

reversed_name = name[::-1]

print(reversed_name)
```

### Output

```text
ahsraH
```

### Interview Answer

> Since strings support slicing, `[::-1]` creates a reversed copy of the string by traversing it from the end to the beginning.

---

# 9. What Does `[::-1]` Mean?

The slicing syntax is:

```python
[start:stop:step]
```

When we write:

```python
[::-1]
```

we omit the start and stop positions and specify a step of `-1`.

This means:

> Traverse the complete sequence backwards.

### Example

```python
text = "Python"

print(text[::-1])
```

Output:

```text
nohtyP
```

---

# 10. How Do You Check the Length of a String?

Use the `len()` function.

```python
name = "Harsha"

print(len(name))
```

Output:

```text
6
```

Spaces are also counted.

```python
text = "Hello World"

print(len(text))
```

Output:

```text
11
```

---

# 11. How Do You Concatenate Strings?

String concatenation means joining strings together.

The `+` operator can be used.

### Example

```python
first_name = "Harsha"
last_name = "Vipparthi"

full_name = first_name + " " + last_name

print(full_name)
```

### Output

```text
Harsha Vipparthi
```

### Important

Python does not automatically concatenate strings with other incompatible types.

```python
age = 22

print("Age: " + age)
```

This raises:

```text
TypeError
```

Use explicit conversion:

```python
print("Age: " + str(age))
```

Output:

```text
Age: 22
```

---

# 12. What Is String Repetition?

The `*` operator can repeat a string.

### Example

```python
text = "Python "

print(text * 3)
```

### Output

```text
Python Python Python
```

This does not modify the original string because strings are immutable.

---

# 13. How Do You Check Whether a Substring Exists in a String?

Use the `in` operator.

### Example

```python
text = "Python is powerful"

print("Python" in text)
print("Java" in text)
```

### Output

```text
True
False
```

### Real-World Example

```python
file_name = "youtube_data.csv"

if ".csv" in file_name:
    print("CSV file")
```

Output:

```text
CSV file
```

---

# 14. What Is the Difference Between `in` and `find()`?

Both can be used to check whether text exists, but they return different kinds of results.

### `in`

Returns a Boolean:

```python
text = "Python"

print("Py" in text)
```

Output:

```text
True
```

### `find()`

Returns the index of the first occurrence, or `-1` if not found.

```python
text = "Python"

print(text.find("Py"))
print(text.find("Java"))
```

Output:

```text
0
-1
```

### Interview Answer

> I would use `in` when I only need a Boolean membership check. I would use `find()` when I also need the position of the substring.

---

# 15. What Is the Difference Between `find()` and `index()`?

Both search for a substring.

### `find()`

Returns `-1` if the substring is not found.

```python
text = "Python"

print(text.find("Java"))
```

Output:

```text
-1
```

### `index()`

Raises `ValueError` if the substring is not found.

```python
text = "Python"

print(text.index("Java"))
```

Output:

```text
ValueError: substring not found
```

### Interview Answer

> `find()` returns `-1` when the substring is absent, whereas `index()` raises `ValueError`. I would choose between them depending on whether I want a sentinel value or an exception when the search fails.

---

# 16. How Do You Count the Occurrences of a Substring?

Use `count()`.

### Example

```python
text = "Python is easy and Python is powerful"

print(text.count("Python"))
```

### Output

```text
2
```

### Real-World Example

It can be useful for basic text analysis:

```python
log = "ERROR INFO ERROR WARNING ERROR"

print(log.count("ERROR"))
```

Output:

```text
3
```

---

# 17. How Do You Convert a String to Uppercase?

Use `upper()`.

```python
text = "python"

print(text.upper())
```

Output:

```text
PYTHON
```

The original string remains unchanged.

```python
text = "python"

text.upper()

print(text)
```

Output:

```text
python
```

This happens because strings are immutable and `upper()` returns a new string.

---

# 18. How Do You Convert a String to Lowercase?

Use `lower()`.

```python
text = "PYTHON"

print(text.lower())
```

Output:

```text
python
```

### Real-World Example

Before comparing user-entered text, we might normalize case:

```python
role = "Developer"

if role.lower() == "developer":
    print("Valid role")
```

Output:

```text
Valid role
```

---

# 19. What Is the Difference Between `lower()` and `casefold()`?

Both are used for case normalization.

`casefold()` is designed for more aggressive, Unicode-aware case-insensitive comparisons.

### Example

```python
text = "HELLO"

print(text.lower())
print(text.casefold())
```

Both produce:

```text
hello
```

For simple English text, they often appear identical.

### Interview Answer

> `lower()` converts characters to lowercase, while `casefold()` is intended for caseless Unicode comparisons and can normalize some characters more aggressively.

---

# 20. What Is `capitalize()`?

`capitalize()` returns a new string with the first character capitalized and the remaining characters converted to lowercase.

### Example

```python
text = "python programming"

print(text.capitalize())
```

Output:

```text
Python programming
```

---

# 21. What Is `title()`?

`title()` converts text to title case.

### Example

```python
text = "python data engineering"

print(text.title())
```

Output:

```text
Python Data Engineering
```

### Important

`title()` follows rules for word boundaries and may not behave perfectly for every form of punctuation or language-specific text.

---

# 22. What Is `strip()`?

`strip()` removes leading and trailing whitespace by default.

### Example

```python
text = "   Python   "

print(text.strip())
```

Output:

```text
Python
```

It does not remove spaces from the middle.

```python
text = "Python   Programming"

print(text.strip())
```

Output:

```text
Python   Programming
```

---

# 23. What Is the Difference Between `strip()`, `lstrip()`, and `rstrip()`?

| Method | Removes from |
|---|---|
| `strip()` | Both ends |
| `lstrip()` | Left/start |
| `rstrip()` | Right/end |

### Example

```python
text = "   Python   "

print(text.strip())
print(text.lstrip())
print(text.rstrip())
```

Output:

```text
Python
Python   
   Python
```

---

# 24. Does `strip()` Remove Any Character You Specify?

It removes characters from the ends based on the supplied character set; it does not remove an exact substring.

### Example

```python
text = "---Python---"

print(text.strip("-"))
```

Output:

```text
Python
```

### Important Interview Trap

This:

```python
text.strip("abc")
```

does **not** mean:

> Remove the exact substring `"abc"`.

It removes any combination of `a`, `b`, or `c` from the beginning and end while those characters are present.

---

# 25. What Does `replace()` Do?

`replace()` returns a new string where occurrences of a specified substring are replaced.

### Example

```python
text = "I like Java"

new_text = text.replace("Java", "Python")

print(new_text)
```

Output:

```text
I like Python
```

The original string remains unchanged.

---

# 26. Can `replace()` Replace Only a Certain Number of Occurrences?

Yes.

The optional third argument specifies the maximum number of replacements.

### Example

```python
text = "Python Python Python"

print(text.replace("Python", "SQL", 2))
```

Output:

```text
SQL SQL Python
```

---

# 27. What Does `split()` Do?

`split()` breaks a string into a list.

### Example

```python
text = "Python SQL PySpark"

skills = text.split()

print(skills)
```

Output:

```text
['Python', 'SQL', 'PySpark']
```

By default, whitespace is used as the separator.

### Using a Separator

```python
data = "Python,SQL,PySpark"

skills = data.split(",")

print(skills)
```

Output:

```text
['Python', 'SQL', 'PySpark']
```

---

# 28. What Is the Difference Between `split()` and `join()`?

`split()` converts a string into a list.

`join()` combines elements of an iterable into a string.

### Example

```python
text = "Python,SQL,PySpark"

skills = text.split(",")

print(skills)

result = " | ".join(skills)

print(result)
```

### Output

```text
['Python', 'SQL', 'PySpark']
Python | SQL | PySpark
```

### Interview Answer

> `split()` is useful when parsing a string into separate components, while `join()` is useful when combining multiple strings into a single string.

---

# 29. How Does `join()` Work?

The string before `.join()` acts as the separator.

### Example

```python
skills = ["Python", "SQL", "PySpark"]

result = ", ".join(skills)

print(result)
```

Output:

```text
Python, SQL, PySpark
```

### Important Interview Trap

The elements being joined generally need to be strings.

This will fail:

```python
numbers = [1, 2, 3]

print(",".join(numbers))
```

because the list contains integers.

Convert them first:

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

# 30. What Is String Formatting?

String formatting means inserting values into a string in a readable way.

Python provides several approaches:

- `%` formatting
- `str.format()`
- f-strings

For modern Python code, **f-strings are usually the preferred approach for straightforward formatting**.

---

# 31. What Are f-Strings?

f-strings allow expressions to be embedded directly inside string literals.

### Example

```python
name = "Harsha"
age = 22

message = f"My name is {name} and I am {age} years old."

print(message)
```

### Output

```text
My name is Harsha and I am 22 years old.
```

### Why Are f-Strings Useful?

They are:

- Readable
- Concise
- Convenient
- Able to evaluate expressions

### Example

```python
a = 10
b = 20

print(f"Sum = {a + b}")
```

Output:

```text
Sum = 30
```

---

# 32. What Is `str.format()`?

`format()` is another way to insert values into strings.

### Example

```python
name = "Harsha"
age = 22

message = "My name is {} and I am {} years old.".format(name, age)

print(message)
```

Output:

```text
My name is Harsha and I am 22 years old.
```

### Named Arguments

```python
message = "Name: {name}, Role: {role}".format(
    name="Harsha",
    role="Data Engineer"
)

print(message)
```

Output:

```text
Name: Harsha, Role: Data Engineer
```

---

# 33. What Is the Difference Between f-Strings and `format()`?

Both can format strings.

### f-string

```python
name = "Harsha"

print(f"Hello {name}")
```

### `format()`

```python
name = "Harsha"

print("Hello {}".format(name))
```

### Interview Answer

> Both support string formatting, but f-strings are generally more concise and readable for modern Python code because expressions can be written directly inside `{}`.

---

# 34. How Do You Format Numbers Using f-Strings?

f-strings support formatting specifications.

### Example — Decimal Places

```python
price = 99.98765

print(f"{price:.2f}")
```

Output:

```text
99.99
```

### Percentage

```python
score = 0.856

print(f"{score:.2%}")
```

Output:

```text
85.60%
```

### Thousands Separator

```python
salary = 550000

print(f"{salary:,}")
```

Output:

```text
550,000
```

---

# 35. What Are Escape Characters?

Escape sequences allow special characters to be represented inside strings.

Common examples:

| Escape | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\'` | Single quote |
| `\"` | Double quote |

### Example

```python
print("Hello\nPython")
print("Python\tSQL")
```

Output:

```text
Hello
Python
Python   SQL
```

---

# 36. What Is a Raw String?

A raw string treats backslashes mostly as literal characters instead of interpreting them as ordinary escape sequences.

It is created using `r` or `R`.

### Example

```python
path = r"C:\Users\Harsha\Documents"

print(path)
```

Output:

```text
C:\Users\Harsha\Documents
```

### Real-World Usage

Raw strings are particularly useful when working with Windows paths and regular expressions.

---

# 37. What Are Multiline Strings?

Triple quotes can be used to create strings spanning multiple lines.

### Example

```python
message = """Hello Harsha,
Welcome to Python.
Good luck with your placements."""

print(message)
```

Output:

```text
Hello Harsha,
Welcome to Python.
Good luck with your placements.
```

They can also be used for documentation strings, known as **docstrings**.

---

# 38. What Is a Docstring?

A docstring is a string literal used to document a module, class, or function.

### Example

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b

print(add.__doc__)
```

Output:

```text
Return the sum of two numbers.
```

Docstrings are different from comments because they are actual string objects associated with Python objects and can be accessed through attributes such as `__doc__`.

---

# 39. What Is the Difference Between a Comment and a Docstring?

### Comment

```python
# This function adds two numbers
```

A comment is ignored by Python's runtime semantics.

### Docstring

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

A docstring is stored as documentation metadata and can be accessed through `__doc__`.

### Interview Answer

> Comments are primarily notes for developers and are not stored as documentation objects by Python, while docstrings are string literals associated with modules, classes, and functions and can be accessed through `__doc__`.

---

# 40. How Do You Compare Strings?

Strings can be compared using operators such as:

```text
==
!=
<
>
<=
>=
```

### Example

```python
print("apple" == "apple")
print("apple" == "Apple")
```

Output:

```text
True
False
```

String comparisons are based on lexicographical ordering using Unicode code points.

### Example

```python
print("apple" < "banana")
```

Output:

```text
True
```

---

# 41. Is String Comparison Case-Sensitive?

Yes.

```python
print("python" == "Python")
```

Output:

```text
False
```

For case-insensitive comparison, a common approach is:

```python
a = "Python"
b = "python"

print(a.casefold() == b.casefold())
```

Output:

```text
True
```

---

# 42. How Do You Check Whether a String Starts or Ends With Specific Text?

Use:

```python
startswith()
endswith()
```

### Example

```python
file_name = "youtube_data.csv"

print(file_name.startswith("youtube"))
print(file_name.endswith(".csv"))
```

### Output

```text
True
True
```

### Real-World Example

These methods are useful for basic file-name or URL checks.

---

# 43. What Is the Difference Between `startswith()` and `find()`?

`startswith()` specifically checks the beginning of a string and returns a Boolean.

```python
text = "Python programming"

print(text.startswith("Python"))
```

Output:

```text
True
```

`find()` searches for a substring anywhere and returns its position.

```python
print(text.find("programming"))
```

Output:

```text
7
```

Use the method that expresses your intention clearly.

---

# 44. What Are `isalpha()`, `isdigit()`, and `isalnum()`?

These methods test the characters in a string.

### `isalpha()`

Returns `True` if all characters are alphabetic and there is at least one character.

```python
print("Python".isalpha())
```

Output:

```text
True
```

### `isdigit()`

Returns `True` if all characters are digits and there is at least one character.

```python
print("12345".isdigit())
```

Output:

```text
True
```

### `isalnum()`

Returns `True` if all characters are alphanumeric and there is at least one character.

```python
print("Python123".isalnum())
```

Output:

```text
True
```

---

# 45. What Happens With an Empty String and `isalpha()`?

```python
print("".isalpha())
print("".isdigit())
print("".isalnum())
```

Output:

```text
False
False
False
```

These methods require at least one character.

---

# 46. What Is the Difference Between `isdigit()`, `isdecimal()`, and `isnumeric()`?

These methods all test numeric-looking characters but have different Unicode definitions.

For common ASCII values:

```python
value = "123"

print(value.isdecimal())
print(value.isdigit())
print(value.isnumeric())
```

Output:

```text
True
True
True
```

The distinction becomes important with certain Unicode numeric characters.

### Interview Answer

> `isdecimal()`, `isdigit()`, and `isnumeric()` are related but not identical Unicode-aware checks. `isdecimal()` is the narrowest of the three, while `isnumeric()` recognizes the broadest range of numeric characters.

For ordinary ASCII input, their results often appear the same.

---

# 47. How Do You Remove Extra Whitespace From User Input?

A common approach is:

```python
name = input("Enter your name: ")

name = name.strip()

print(name)
```

If the user enters:

```text
   Harsha
```

the resulting value becomes:

```text
Harsha
```

### Real-World Usage

This is useful when cleaning input data before storing or processing it.

---

# 48. How Do You Remove All Spaces From a String?

If the requirement is to remove every space, not just leading/trailing spaces:

```python
text = "Python is powerful"

result = text.replace(" ", "")

print(result)
```

Output:

```text
Pythonispowerful
```

### Important

Do not use `strip()` for this requirement.

`strip()` only removes whitespace from the beginning and end.

---

# 49. How Do You Count Words in a String?

A simple approach is:

```python
text = "Python is easy to learn"

words = text.split()

print(len(words))
```

Output:

```text
5
```

### Interview Follow-Up

Why use:

```python
split()
```

instead of:

```python
split(" ")
```

Because `split()` without an argument handles runs of whitespace more naturally.

Example:

```python
text = "Python   is   easy"

print(text.split())
```

Output:

```text
['Python', 'is', 'easy']
```

---

# 50. How Do You Check Whether a String Is a Palindrome?

A palindrome reads the same forward and backward.

### Example

```python
text = "madam"

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not a palindrome")
```

Output:

```text
Palindrome
```

### Interview Answer

> Since strings support slicing, I can reverse the string using `[::-1]` and compare it with the original. This is simple and readable for a basic palindrome check.

---

# 51. How Do You Reverse the Words in a Sentence?

### Example

```python
text = "Python is powerful"

words = text.split()
result = " ".join(words[::-1])

print(result)
```

### Output

```text
powerful is Python
```

This is different from reversing every character.

---

# 52. How Do You Reverse Every Character in a String?

Use:

```python
text = "Python"

print(text[::-1])
```

Output:

```text
nohtyP
```

The difference between reversing characters and reversing words is important in interviews.

---

# 53. How Do You Check Whether Two Strings Are Anagrams?

Two strings are anagrams if they contain the same characters with the same frequencies, ignoring order.

### Simple Approach

```python
a = "listen"
b = "silent"

if sorted(a) == sorted(b):
    print("Anagram")
else:
    print("Not anagram")
```

Output:

```text
Anagram
```

### Interview Follow-Up

For a large input, you may want a frequency-count approach rather than sorting because sorting takes `O(n log n)` time.

A frequency-based solution can achieve approximately `O(n)` time.

---

# 54. How Do You Count Character Frequencies in a String?

A dictionary can be used.

### Example

```python
text = "banana"

frequency = {}

for char in text:
    frequency[char] = frequency.get(char, 0) + 1

print(frequency)
```

Output:

```text
{'b': 1, 'a': 3, 'n': 2}
```

### Real-World Usage

Frequency counting can be useful for basic text analysis, validation, and data preprocessing.

---

# 55. How Do You Remove Duplicate Characters From a String?

One simple approach is to use a set, but that does not preserve the original order.

If order must be preserved:

```python
text = "programming"

result = ""

for char in text:
    if char not in result:
        result += char

print(result)
```

Output:

```text
progamin
```

### Better Approach

For efficient order-preserving removal:

```python
text = "programming"

result = "".join(dict.fromkeys(text))

print(result)
```

Output:

```text
progamin
```

This works because dictionary keys are unique and modern Python dictionaries preserve insertion order.

---

# 56. What Is String Interning?

Python may reuse certain string objects internally, particularly strings that are suitable for interning.

This can sometimes make identity comparisons appear surprising.

### Example

```python
a = "Python"
b = "Python"

print(a == b)
print(a is b)
```

Depending on how the strings are created and Python's implementation details, `a is b` may be `True`.

### Important Interview Rule

Never use `is` to compare string values.

Use:

```python
a == b
```

Use `is` for identity checks.

For example:

```python
value is None
```

is appropriate.

### Strong Interview Answer

> Python may intern or reuse some immutable string objects as an optimization, but that behavior should not be relied upon for value comparison. String values should be compared using `==`, not `is`.

---

# 57. What Is the Difference Between String Concatenation and `join()`?

### Concatenation

```python
a = "Python"
b = "SQL"

result = a + " " + b

print(result)
```

Output:

```text
Python SQL
```

### `join()`

```python
skills = ["Python", "SQL", "PySpark"]

result = ", ".join(skills)

print(result)
```

Output:

```text
Python, SQL, PySpark
```

### Interview Answer

> `+` is straightforward for joining a small number of strings, while `join()` is designed for combining multiple strings from an iterable using a separator and is generally the better choice when joining many pieces.

---

# 58. Why Is Repeated `+` Concatenation Sometimes Avoided in Loops?

Strings are immutable, so repeatedly creating larger strings can result in unnecessary intermediate string objects.

For example:

```python
result = ""

for word in ["Python", "SQL", "PySpark"]:
    result += word
```

For larger workloads, building a list and joining once is generally preferable:

```python
words = ["Python", "SQL", "PySpark"]

result = "".join(words)

print(result)
```

Output:

```text
PythonSQLPySpark
```

### Interview Answer

> Because strings are immutable, repeated concatenation can create many intermediate strings. For combining many pieces, collecting them and using `join()` is generally more efficient and expressive.

---

# 59. What Is the Difference Between `split()` and `partition()`?

`split()` can divide a string into multiple pieces.

`partition()` splits around the first occurrence of a separator and returns exactly three parts:

```text
before separator
separator
after separator
```

### Example

```python
text = "name=Harsha"

print(text.partition("="))
```

Output:

```text
('name', '=', 'Harsha')
```

### Interview Use

`partition()` is useful when you specifically want to split once and retain the separator.

---

# 60. What Is the Difference Between `split()` and `rsplit()`?

`split()` starts splitting from the left.

`rsplit()` starts from the right.

The `maxsplit` argument makes the difference useful.

### Example

```python
path = "folder/subfolder/file.csv"

print(path.split("/", 1))
print(path.rsplit("/", 1))
```

Output:

```text
['folder', 'subfolder/file.csv']
['folder/subfolder', 'file.csv']
```

This can be useful when processing paths or structured strings.

---

# 61. What Is the Difference Between `replace()` and `translate()`?

`replace()` is convenient for replacing a specific substring.

`translate()` is useful for character-by-character translation or removal using a translation table.

### Example

```python
text = "hello"

table = str.maketrans({"h": "H", "e": "E"})

print(text.translate(table))
```

Output:

```text
HEllo
```

For simple substring replacement, `replace()` is usually clearer.

---

# 62. How Do You Escape Quotes Inside a String?

Use the opposite quote type or an escape character.

### Example

```python
text = "Python's syntax is simple"

print(text)
```

Or:

```python
text = 'Python\'s syntax is simple'

print(text)
```

Both represent the same text.

---

# 63. Can a String Contain Unicode Characters?

Yes. Python strings are Unicode-based.

### Example

```python
text = "Hello नमस्ते"

print(text)
```

Python can represent characters from many writing systems.

### Real-World Importance

This matters when processing:

- International names
- Multilingual text
- User input
- APIs
- Files
- Global datasets

---

# 64. What Is Encoding?

Encoding converts text into a sequence of bytes.

Decoding converts bytes back into text.

### Example

```python
text = "Python"

encoded = text.encode("utf-8")
decoded = encoded.decode("utf-8")

print(encoded)
print(decoded)
```

### Output

```text
b'Python'
Python
```

### Interview Answer

> Encoding converts a Unicode string into bytes using a character encoding such as UTF-8. Decoding converts those bytes back into a string.

---

# 65. What Is UTF-8?

UTF-8 is a widely used Unicode encoding that represents Unicode text as bytes.

### Example

```python
text = "Hello"

data = text.encode("utf-8")

print(data)
```

Output:

```text
b'Hello'
```

For non-ASCII text, UTF-8 can use multiple bytes per character.

### Important

A Python `str` represents text, while `bytes` represents binary data.

---

# 66. What Is the Difference Between `str` and `bytes`?

| `str` | `bytes` |
|---|---|
| Represents text | Represents binary data |
| Unicode text | Sequence of bytes |
| Immutable | Immutable |
| Example: `"Python"` | Example: `b"Python"` |
| `.encode()` converts str → bytes | `.decode()` converts bytes → str |

### Example

```python
text = "Python"

data = text.encode("utf-8")
text_again = data.decode("utf-8")

print(type(text))
print(type(data))
print(type(text_again))
```

Output:

```text
<class 'str'>
<class 'bytes'>
<class 'str'>
```

---

# 67. What Is a Common Mistake When Working With `str` and `bytes`?

Trying to directly combine them.

```python
text = "Python"
data = b"SQL"

print(text + data)
```

This raises a `TypeError`.

Convert them to a common type first.

For example:

```python
text = "Python"
data = b"SQL"

result = text + data.decode("utf-8")

print(result)
```

Output:

```text
PythonSQL
```

---

# 68. Can Strings Be Used as Dictionary Keys?

Yes.

Strings are immutable and hashable.

### Example

```python
employee = {
    "name": "Harsha",
    "role": "Data Engineer"
}

print(employee["name"])
```

Output:

```text
Harsha
```

This is one reason strings are commonly used as dictionary keys.

---

# 69. What Happens When You Modify a String Method Result?

String methods generally return a new string rather than modifying the existing one.

### Example

```python
text = "python"

text.upper()

print(text)
```

Output:

```text
python
```

To keep the result:

```python
text = text.upper()

print(text)
```

Output:

```text
PYTHON
```

### Interview Tip

This is a very common beginner interview trap.

---

# 70. Important String Interview Output Questions

## Question 1

```python
text = "Python"

print(text[0])
print(text[-1])
```

### Answer

```text
P
n
```

---

## Question 2

```python
text = "Python"

print(text[1:4])
```

### Answer

```text
yth
```

---

## Question 3

```python
text = "Python"

print(text[::-1])
```

### Answer

```text
nohtyP
```

---

## Question 4

```python
text = "Python"

text.upper()

print(text)
```

### Answer

```text
Python
```

Because `upper()` returns a new string.

---

## Question 5

```python
text = "Python"

print("Py" in text)
print("Java" in text)
```

### Answer

```text
True
False
```

---

## Question 6

```python
text = "banana"

print(text.count("a"))
```

### Answer

```text
3
```

---

## Question 7

```python
text = "Python SQL PySpark"

print(text.split())
```

### Answer

```text
['Python', 'SQL', 'PySpark']
```

---

## Question 8

```python
skills = ["Python", "SQL", "PySpark"]

print("-".join(skills))
```

### Answer

```text
Python-SQL-PySpark
```

---

## Question 9

```python
text = "Python"

print(text.find("Java"))
```

### Answer

```text
-1
```

---

## Question 10

```python
text = "Python"

print(text.replace("Python", "SQL"))
print(text)
```

### Answer

```text
SQL
Python
```

The original string remains unchanged.

---

# 71. Common String Interview Traps

## Trap 1 — Strings Are Mutable

Incorrect:

> Strings are mutable.

Correct:

> Strings are immutable.

---

## Trap 2 — `upper()` Modifies the Original String

Incorrect:

> `upper()` changes the existing string.

Correct:

> `upper()` returns a new string because strings are immutable.

---

## Trap 3 — `is` Compares String Values

Incorrect:

```python
a is b
```

for checking whether two strings contain the same value.

Correct:

```python
a == b
```

`is` checks identity.

---

## Trap 4 — `strip()` Removes a Substring

Incorrect:

> `strip()` removes an exact substring.

Correct:

> `strip()` removes characters from the ends according to the supplied character set.

---

## Trap 5 — `split()` Returns a String

Incorrect:

> `split()` returns another string.

Correct:

> `split()` returns a list of strings.

---

## Trap 6 — `join()` Is Called on the List

Conceptually:

```python
separator.join(iterable)
```

Example:

```python
",".join(["Python", "SQL"])
```

Not:

```python
["Python", "SQL"].join(",")
```

---

# 72. Real-World String Processing Example

Suppose a data pipeline receives a CSV-like record:

```python
record = "101,Harsha,Data Engineer,Python|SQL|PySpark"
```

We can parse it:

```python
parts = record.split(",")

employee_id = parts[0]
name = parts[1]
role = parts[2]
skills = parts[3].split("|")

print(employee_id)
print(name)
print(role)
print(skills)
```

### Output

```text
101
Harsha
Data Engineer
['Python', 'SQL', 'PySpark']
```

This demonstrates how string operations can be used during basic data ingestion and preprocessing.

In real data engineering systems, structured parsers such as CSV or JSON libraries are usually preferred over manually splitting complex data formats.

---

# 73. Real-World API/Data Engineering Example

Suppose an API provides a filename:

```python
file_name = "youtube_statistics_2026.csv"
```

We can perform simple validation:

```python
if file_name.endswith(".csv"):
    print("CSV file detected")
```

Output:

```text
CSV file detected
```

We can also extract the file extension:

```python
extension = file_name.split(".")[-1]

print(extension)
```

Output:

```text
csv
```

For production systems, more robust path/file utilities may be preferable for complicated filenames.

---

# 74. Important String Methods to Remember

| Method | Purpose |
|---|---|
| `upper()` | Convert to uppercase |
| `lower()` | Convert to lowercase |
| `casefold()` | Unicode-aware case normalization |
| `capitalize()` | Capitalize first character |
| `title()` | Title-case text |
| `strip()` | Remove characters/whitespace from both ends |
| `lstrip()` | Remove from left |
| `rstrip()` | Remove from right |
| `replace()` | Replace substring |
| `find()` | Find position or return `-1` |
| `index()` | Find position or raise `ValueError` |
| `count()` | Count occurrences |
| `split()` | String → list |
| `rsplit()` | Split from right |
| `partition()` | Split once into three parts |
| `join()` | Iterable of strings → string |
| `startswith()` | Check beginning |
| `endswith()` | Check ending |
| `isalpha()` | Check alphabetic characters |
| `isdigit()` | Check digit characters |
| `isalnum()` | Check alphanumeric characters |

---

# 75. Interview Questions to Prepare Deeply

1. What is a string in Python?
2. Are strings mutable or immutable?
3. Why are strings immutable?
4. What is string interning?
5. What is the difference between `is` and `==` when comparing strings?
6. How does string indexing work?
7. What is negative indexing?
8. What is string slicing?
9. How do you reverse a string?
10. What does `[::-1]` mean?
11. How do you concatenate strings?
12. Why can repeated string concatenation be inefficient?
13. What is the difference between `+` and `join()`?
14. What does `split()` do?
15. What does `join()` do?
16. What is the difference between `split()` and `rsplit()`?
17. What is the difference between `split()` and `partition()`?
18. What is the difference between `find()` and `index()`?
19. What does `replace()` return?
20. Can `replace()` limit the number of replacements?
21. What is `strip()`?
22. What is the difference between `strip()`, `lstrip()`, and `rstrip()`?
23. What are f-strings?
24. What is the difference between f-strings and `format()`?
25. What are escape sequences?
26. What is a raw string?
27. What is a multiline string?
28. What is a docstring?
29. What is the difference between a comment and a docstring?
30. What is the difference between `lower()` and `casefold()`?
31. What do `isalpha()`, `isdigit()`, and `isalnum()` do?
32. What is the difference between `isdecimal()`, `isdigit()`, and `isnumeric()`?
33. How do you compare strings?
34. Are string comparisons case-sensitive?
35. How do you perform case-insensitive comparison?
36. What is Unicode?
37. What is encoding?
38. What is decoding?
39. What is UTF-8?
40. What is the difference between `str` and `bytes`?
41. Can strings be dictionary keys?
42. Why are strings hashable?
43. How do you count character frequencies?
44. How do you check whether a string is a palindrome?
45. How do you check whether two strings are anagrams?
46. How do you remove duplicate characters?
47. How do you reverse words in a sentence?
48. How do you count words in a sentence?
49. How do you remove whitespace?
50. How do you check whether a filename has a particular extension?

---

# 76. Strong Interview Answer Pattern

When asked about a string concept, avoid giving only a one-line definition.

A stronger answer follows this pattern:

**Definition → Important property → Example → Real-world usage → Follow-up**

### Example: "What is string immutability?"

A strong answer:

> "Strings in Python are immutable, which means an existing string object cannot be modified in place. If I perform an operation such as `upper()` or `replace()`, Python returns a new string instead of changing the original one. This also means strings can safely be used as dictionary keys because they are hashable. For example, if I call `text.upper()`, I need to store the returned value if I want to use the uppercase version."

This answer demonstrates both the concept and its practical behavior.

---

# 77. Quick Revision

## String Basics

```text
str → Unicode text
Immutable → Cannot modify characters in place
Indexing → Starts from 0
Negative indexing → Starts from -1
Slicing → [start:stop:step]
Reverse → [::-1]
Length → len()
```

## Important Operations

```text
+              → Concatenation
*              → Repetition
in             → Membership
==             → Value equality
is             → Object identity
```

## Important Methods

```text
upper()
lower()
casefold()
strip()
replace()
find()
index()
count()
split()
rsplit()
partition()
join()
startswith()
endswith()
```

## Conversion

```text
str → bytes       encode()
bytes → str       decode()
```

## Most Important Interview Concepts

```text
1. String immutability
2. is vs ==
3. String slicing
4. String interning
5. split() vs join()
6. find() vs index()
7. strip() behavior
8. f-strings
9. str vs bytes
10. Encoding and decoding
11. Unicode
12. String performance
```

## Final Placement Focus

For placement interviews, the highest-priority string concepts are:

1. **String immutability**
2. **Indexing and slicing**
3. **`is` vs `==`**
4. **`split()` and `join()`**
5. **`find()` vs `index()`**
6. **`replace()`**
7. **`strip()`**
8. **f-strings**
9. **String formatting**
10. **String methods**
11. **`str` vs `bytes`**
12. **Encoding/decoding**
13. **Common string output questions**
14. **Palindrome/anagram/frequency questions**
15. **Real-world string processing**

The goal is not to memorize every string method. The important part is to understand the **core behavior, why it works, when to use it, and the common follow-up questions an interviewer may ask**.