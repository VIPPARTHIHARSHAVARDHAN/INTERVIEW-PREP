# 17 — File Handling

## 1. What Is File Handling?

File handling in Python means **creating, opening, reading, writing, modifying, and closing files** using Python programs.

It is useful when data needs to be stored permanently instead of keeping it only in memory.

For example:

```python
file = open("data.txt", "r")
content = file.read()
print(content)
file.close()
```

File handling is commonly used for:

- reading configuration files
- processing CSV files
- reading logs
- writing reports
- storing text data
- processing input/output files
- data engineering and ETL workflows

---

# 2. Why Do We Need File Handling?

Variables store data temporarily in memory.

```python
name = "Harsha"
```

When the program ends, that variable normally no longer exists.

A file provides persistent storage.

```text
Python Program
      ↓
    File
      ↓
Persistent data
```

For example, a program can read a CSV file, process the records, and write the results into another file.

---

# 3. Opening a File

Python provides the built-in `open()` function.

Basic syntax:

```python
open(filename, mode)
```

Example:

```python
file = open("data.txt", "r")
```

Here:

- `"data.txt"` → file name
- `"r"` → read mode

---

# 4. Common File Modes

| Mode | Meaning |
|---|---|
| `r` | Read |
| `w` | Write |
| `a` | Append |
| `x` | Create a new file |
| `b` | Binary mode |
| `t` | Text mode |
| `r+` | Read and write |
| `w+` | Write and read |
| `a+` | Append and read |

Modes can also be combined.

Example:

```python
open("image.jpg", "rb")
```

This opens the file in binary read mode.

---

# 5. `r` — Read Mode

`r` is used to read an existing file.

```python
file = open("data.txt", "r")

content = file.read()

print(content)

file.close()
```

If the file does not exist, Python raises:

```text
FileNotFoundError
```

---

# 6. `w` — Write Mode

`w` is used to write data to a file.

```python
file = open("data.txt", "w")

file.write("Hello Python")

file.close()
```

Important:

If the file already exists, `w` **overwrites its existing contents**.

Example:

Existing file:

```text
Hello
World
```

After:

```python
file = open("data.txt", "w")
file.write("Python")
file.close()
```

The file contains:

```text
Python
```

---

# 7. `a` — Append Mode

`a` adds data to the end of an existing file.

```python
file = open("data.txt", "a")

file.write("\nNew line")

file.close()
```

Existing:

```text
Hello
World
```

After execution:

```text
Hello
World
New line
```

Unlike `w`, append mode does not overwrite the existing content.

---

# 8. `x` — Exclusive Creation Mode

`x` creates a new file.

```python
file = open("newfile.txt", "x")
file.write("Hello")
file.close()
```

If the file already exists, Python raises:

```text
FileExistsError
```

This is useful when you want to ensure that you do not accidentally overwrite an existing file.

---

# 9. Text Mode and Binary Mode

### Text mode

Used for text data.

```python
file = open("data.txt", "r")
```

### Binary mode

Used for binary data such as images, PDFs, audio, etc.

```python
file = open("image.jpg", "rb")
```

Common combinations:

```text
r   → text read
w   → text write
rb  → binary read
wb  → binary write
ab  → binary append
```

---

# 10. Reading the Entire File Using `read()`

```python
file = open("data.txt", "r")

content = file.read()

print(content)

file.close()
```

`read()` returns the file contents as a string in text mode.

---

# 11. Reading a Specific Number of Characters

`read()` can accept a size.

```python
file = open("data.txt", "r")

content = file.read(5)

print(content)

file.close()
```

This reads up to 5 characters from the current file position.

---

# 12. Reading One Line Using `readline()`

`readline()` reads one line at a time.

Example file:

```text
Python
SQL
PySpark
```

Code:

```python
file = open("data.txt", "r")

line = file.readline()

print(line)

file.close()
```

Output:

```text
Python
```

---

# 13. Reading All Lines Using `readlines()`

`readlines()` returns the lines as a list.

```python
file = open("data.txt", "r")

lines = file.readlines()

print(lines)

file.close()
```

For:

```text
Python
SQL
PySpark
```

the result is approximately:

```python
["Python\n", "SQL\n", "PySpark\n"]
```

---

# 14. `read()` vs `readline()` vs `readlines()`

| Method | Result |
|---|---|
| `read()` | Reads content from the current position |
| `read(n)` | Reads up to `n` characters/bytes |
| `readline()` | Reads one line |
| `readlines()` | Reads remaining lines into a list |

### Important interview point

For very large files, blindly doing:

```python
file.read()
```

can consume a lot of memory.

Processing the file incrementally can be more memory-efficient.

---

# 15. Iterating Through a File

A file object is iterable.

```python
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())
```

This is commonly preferred for large text files because the program can process lines incrementally.

---

# 16. Why Is Iterating Over a File Memory Efficient?

Consider a very large file.

Instead of:

```python
data = file.read()
```

we can do:

```python
for line in file:
    process(line)
```

The program can process the file incrementally rather than creating one huge string containing the entire file.

This is especially useful in data processing.

---

# 17. The `with` Statement

Python provides context managers to manage resources safely.

Instead of:

```python
file = open("data.txt", "r")

content = file.read()

file.close()
```

we can use:

```python
with open("data.txt", "r") as file:
    content = file.read()
```

The file is automatically closed after the `with` block.

---

# 18. Why Should We Prefer `with open()`?

Suppose an exception occurs:

```python
file = open("data.txt", "r")

data = file.read()

# Some exception occurs here

file.close()
```

If the exception occurs before `close()`, the close operation may never execute.

With:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

the context manager handles cleanup when leaving the block.

### Strong Interview Answer

> I prefer using `with open()` because it manages the file resource automatically and ensures that the file is properly closed even when an exception occurs.

---

# 19. Writing to a File Using `write()`

```python
with open("data.txt", "w") as file:
    file.write("Python")
```

`write()` returns the number of characters written in text mode.

Example:

```python
with open("data.txt", "w") as file:
    count = file.write("Python")

print(count)
```

Output:

```text
6
```

---

# 20. Writing Multiple Lines

We can use `writelines()`.

```python
lines = [
    "Python\n",
    "SQL\n",
    "PySpark\n"
]

with open("data.txt", "w") as file:
    file.writelines(lines)
```

Important:

`writelines()` does **not automatically add newline characters**.

Therefore:

```python
["Python", "SQL"]
```

may result in:

```text
PythonSQL
```

while:

```python
["Python\n", "SQL\n"]
```

produces separate lines.

---

# 21. `write()` vs `writelines()`

### `write()`

Writes a string.

```python
file.write("Hello")
```

### `writelines()`

Writes multiple strings from an iterable.

```python
file.writelines(["Hello\n", "World\n"])
```

---

# 22. File Pointer

When a file is opened, Python maintains a current position called the **file pointer**.

Example:

```python
with open("data.txt", "r") as file:
    print(file.tell())
```

Initially, the position is usually:

```text
0
```

After reading some content, the position changes.

---

# 23. `tell()`

`tell()` returns the current file position.

Example:

```python
with open("data.txt", "r") as file:
    print(file.tell())

    file.read(5)

    print(file.tell())
```

If the file starts at position 0 and 5 characters are read, the position will typically move to 5 for a simple text example.

---

# 24. `seek()`

`seek()` moves the file pointer to a specified position.

Example:

```python
with open("data.txt", "r") as file:
    file.seek(5)
    print(file.read())
```

The next read starts from the specified position, subject to the rules of the file mode and encoding.

---

# 25. `seek()` and `tell()` Together

```python
with open("data.txt", "r") as file:
    print(file.tell())

    file.read(5)

    print(file.tell())

    file.seek(0)

    print(file.tell())
```

Possible output:

```text
0
5
0
```

This demonstrates moving the file pointer.

---

# 26. What Happens When We Open a File in `w` Mode?

This is a common interview question.

```python
open("data.txt", "w")
```

If the file exists, its existing contents are truncated.

If it doesn't exist, Python generally creates it.

Example:

```python
with open("data.txt", "w") as file:
    file.write("New content")
```

The previous contents are replaced.

---

# 27. What Happens When We Open a File in `a` Mode?

If the file exists, new content is written at the end.

If it doesn't exist, Python generally creates it.

```python
with open("data.txt", "a") as file:
    file.write("New content\n")
```

---

# 28. File Encoding

Text files use character encodings.

We can explicitly specify an encoding:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

For writing:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("Hello")
```

Specifying the encoding makes the intended text encoding explicit and can avoid platform-dependent behavior.

---

# 29. Why Is `encoding="utf-8"` Useful?

It helps Python correctly interpret text characters.

For example:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

This is especially useful when working with multilingual or externally generated data.

---

# 30. Handling `FileNotFoundError`

```python
try:
    with open("missing.txt", "r") as file:
        data = file.read()

except FileNotFoundError:
    print("File not found")
```

This combines file handling with exception handling.

---

# 31. Handling `PermissionError`

```python
try:
    with open("restricted.txt", "r") as file:
        data = file.read()

except PermissionError:
    print("Permission denied")
```

The exact behavior depends on the operating system and permissions.

---

# 32. File Handling With Exception Handling

A robust example:

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        data = file.read()

except FileNotFoundError:
    print("Input file does not exist")

except PermissionError:
    print("Permission denied")

except OSError as e:
    print("File operation failed:", e)
```

The more specific exceptions are placed before the broader `OSError`.

---

# 33. Reading a Large File

Avoid:

```python
with open("large.log", "r") as file:
    data = file.read()
```

when the entire file may be very large and you only need to process it incrementally.

Prefer:

```python
with open("large.log", "r") as file:
    for line in file:
        process(line)
```

This allows line-by-line processing.

---

# 34. Real-World Example — Log Processing

Suppose an application generates:

```text
INFO User logged in
ERROR Database connection failed
INFO Request completed
ERROR Invalid input
```

We can find error lines:

```python
with open("application.log", "r") as file:
    for line in file:
        if "ERROR" in line:
            print(line.strip())
```

Output:

```text
ERROR Database connection failed
ERROR Invalid input
```

This is a practical example of file processing.

---

# 35. Real-World Example — Data Engineering

A data engineering pipeline may receive raw files:

```text
raw_data.csv
```

A Python process might:

```text
Read raw file
      ↓
Validate records
      ↓
Transform data
      ↓
Write processed file
```

For example:

```python
with open("raw_data.txt", "r") as source:
    with open("processed_data.txt", "w") as destination:

        for line in source:
            cleaned = line.strip()

            if cleaned:
                destination.write(cleaned + "\n")
```

This demonstrates streaming-style processing from one file to another.

---

# 36. Copying a Text File

```python
with open("source.txt", "r", encoding="utf-8") as source:
    data = source.read()

with open("destination.txt", "w", encoding="utf-8") as destination:
    destination.write(data)
```

For very large files, a chunked approach is generally better.

---

# 37. Reading a File in Chunks

For large files, we can process fixed-size chunks:

```python
with open("large_file.txt", "r", encoding="utf-8") as file:
    while True:
        chunk = file.read(1024)

        if not chunk:
            break

        print(chunk)
```

This avoids loading the entire file into memory at once.

---

# 38. Binary File Handling

Binary files should generally be opened with `b` mode.

Example:

```python
with open("image.jpg", "rb") as file:
    data = file.read()
```

Here `data` is a `bytes` object.

---

# 39. Copying a Binary File

```python
with open("source.jpg", "rb") as source:
    data = source.read()

with open("copy.jpg", "wb") as destination:
    destination.write(data)
```

For very large files, processing in chunks is preferable:

```python
with open("source.jpg", "rb") as source:
    with open("copy.jpg", "wb") as destination:
        while True:
            chunk = source.read(4096)

            if not chunk:
                break

            destination.write(chunk)
```

---

# 40. Text vs Binary Files

| Text | Binary |
|---|---|
| Human-readable text | Raw bytes |
| Uses text encoding | No text decoding at the file layer |
| Example: `.txt`, many `.csv` workflows | Example: images, PDFs, audio |
| `"r"` / `"w"` | `"rb"` / `"wb"` |

---

# 41. What Does `b` Mean?

`b` means binary mode.

Example:

```python
open("image.jpg", "rb")
```

The returned data is bytes rather than decoded text.

---

# 42. What Does `t` Mean?

`t` means text mode.

It is the default mode.

These are equivalent:

```python
open("data.txt", "r")
```

and:

```python
open("data.txt", "rt")
```

---

# 43. What Is the Default File Mode?

The default mode of `open()` is:

```text
r
```

So:

```python
open("data.txt")
```

is equivalent to:

```python
open("data.txt", "r")
```

---

# 44. What Is the Default Text Encoding?

Do not assume the same encoding on every system.

Python uses the environment/platform's default text encoding if you do not explicitly specify one.

For portable text-processing code, explicitly specifying:

```python
encoding="utf-8"
```

is often a good practice when UTF-8 is the intended encoding.

---

# 45. What Is the Difference Between `r+`, `w+`, and `a+`?

| Mode | Read | Write | Existing content |
|---|---:|---:|---|
| `r+` | Yes | Yes | Preserved |
| `w+` | Yes | Yes | Truncated |
| `a+` | Yes | Yes | Preserved, writes at end |

### `r+`

```python
file = open("data.txt", "r+")
```

The file must already exist.

### `w+`

```python
file = open("data.txt", "w+")
```

Creates or truncates the file.

### `a+`

```python
file = open("data.txt", "a+")
```

Creates if necessary and writes at the end.

---

# 46. Important Interview Question — Difference Between `w` and `a`

### `w`

Overwrites/truncates existing content.

```python
with open("data.txt", "w") as file:
    file.write("Hello")
```

### `a`

Preserves existing content and adds new content at the end.

```python
with open("data.txt", "a") as file:
    file.write("Hello")
```

### Strong Interview Answer

> `w` is used when I want to write fresh content and it truncates an existing file, while `a` preserves the existing content and appends new data to the end.

---

# 47. Important Interview Question — Difference Between `read()` and `readline()`

`read()` reads content from the current position, optionally up to a specified size.

```python
file.read()
```

`readline()` reads one line.

```python
file.readline()
```

For large files, iterating directly over the file is often convenient:

```python
for line in file:
    ...
```

---

# 48. Important Interview Question — Difference Between `readlines()` and Iterating Over a File

`readlines()` loads the remaining lines into a list:

```python
lines = file.readlines()
```

Direct iteration processes lines incrementally:

```python
for line in file:
    process(line)
```

For large files, direct iteration is generally more memory efficient.

---

# 49. Important Interview Question — What Does `close()` Do?

`close()` closes the file object and releases the associated resource.

Example:

```python
file = open("data.txt", "r")
data = file.read()
file.close()
```

After closing, normal file operations should not be performed on that file object.

---

# 50. Important Interview Question — What Happens If You Forget to Close a File?

Not closing files can lead to:

- resources remaining open
- file descriptor exhaustion
- data not being flushed as expected in some write scenarios
- inability to access/delete files in some environments
- resource leaks

Using:

```python
with open(...) as file:
```

greatly reduces this risk.

---

# 51. Important Interview Question — What Is a File Descriptor?

At the operating-system level, an open file is associated with a resource handle/file descriptor.

Python's file object manages the underlying resource.

You normally do not need to manipulate the raw file descriptor for ordinary file operations.

---

# 52. Important Interview Question — What Is a Context Manager?

A context manager controls setup and cleanup around a block of code.

Example:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

The file is acquired when entering the context and properly released when leaving it.

---

# 53. Important Interview Question — Why Does `with` Close the File Automatically?

File objects support the context manager protocol.

Conceptually, entering the `with` block gives us the resource, and leaving the block triggers cleanup.

This cleanup happens even if an exception occurs inside the block.

---

# 54. Important Interview Question — Can We Open Multiple Files Using One `with`?

Yes.

```python
with open("source.txt", "r") as source, open("destination.txt", "w") as destination:
    for line in source:
        destination.write(line)
```

This is useful when copying or transforming data between files.

---

# 55. Important Interview Question — How Would You Process a Large File?

A good answer:

> I would avoid loading the entire file into memory unless the file size is known to be manageable. For a line-oriented text file, I can iterate over the file line by line. For binary or arbitrary data, I can process it in chunks. This reduces memory usage and allows the application to handle larger files.

Example:

```python
with open("large_file.txt", "r", encoding="utf-8") as file:
    for line in file:
        process(line)
```

---

# 56. Important Interview Question — How Would You Count Lines in a File?

```python
count = 0

with open("data.txt", "r", encoding="utf-8") as file:
    for line in file:
        count += 1

print(count)
```

This processes the file incrementally.

---

# 57. Coding Question — Count Words in a File

```python
count = 0

with open("data.txt", "r", encoding="utf-8") as file:
    for line in file:
        count += len(line.split())

print("Word count:", count)
```

This is simple file-processing logic rather than a DSA problem.

---

# 58. Coding Question — Find Lines Containing a Word

```python
with open("data.txt", "r", encoding="utf-8") as file:
    for line_number, line in enumerate(file, start=1):
        if "Python" in line:
            print(line_number, line.strip())
```

This demonstrates:

- file iteration
- `enumerate()`
- string searching
- `strip()`

---

# 59. Coding Question — Copy a Large File in Chunks

```python
with open("source.bin", "rb") as source:
    with open("destination.bin", "wb") as destination:

        while True:
            chunk = source.read(4096)

            if not chunk:
                break

            destination.write(chunk)
```

This avoids reading the complete file into memory.

---

# 60. Coding Question — Remove Empty Lines

```python
with open("input.txt", "r", encoding="utf-8") as source:
    with open("output.txt", "w", encoding="utf-8") as destination:

        for line in source:
            if line.strip():
                destination.write(line)
```

This is a practical transformation task.

---

# 61. Coding Question — Read a File Safely

```python
def read_file(filename):
    try:
        with open(filename, "r", encoding="utf-8") as file:
            return file.read()

    except FileNotFoundError:
        return "File not found"

    except PermissionError:
        return "Permission denied"


print(read_file("data.txt"))
```

---

# 62. Coding Question — Append a Log Message

```python
from datetime import datetime

message = "Application started"

with open("application.log", "a", encoding="utf-8") as file:
    file.write(f"{datetime.now()} - {message}\n")
```

This demonstrates a simple logging-style file operation.

---

# 63. File Handling With CSV

For actual CSV data, Python's `csv` module is usually preferable to manually splitting lines.

Example:

```python
import csv

with open("employees.csv", "r", encoding="utf-8", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["name"])
```

This is more reliable than:

```python
line.split(",")
```

because CSV files can contain quoted fields and commas inside values.

---

# 64. File Handling With JSON

JSON files can be processed using Python's `json` module.

Example:

```python
import json

with open("data.json", "r", encoding="utf-8") as file:
    data = json.load(file)

print(data)
```

Writing JSON:

```python
import json

data = {
    "name": "Harsha",
    "skills": ["Python", "SQL"]
}

with open("data.json", "w", encoding="utf-8") as file:
    json.dump(data, file, indent=4)
```

---

# 65. File Handling in Your Data Engineering Preparation

File handling is especially relevant to data engineering because data often arrives as files such as:

```text
CSV
JSON
TXT
Parquet
logs
```

A Python program may perform:

```text
Raw File
   ↓
Read
   ↓
Validate
   ↓
Transform
   ↓
Write / Upload
```

For example:

```python
with open("raw_data.txt", "r", encoding="utf-8") as source:
    with open("clean_data.txt", "w", encoding="utf-8") as destination:

        for line in source:
            line = line.strip()

            if line:
                destination.write(line + "\n")
```

The same basic principles appear in larger ETL systems, although production data pipelines commonly use specialized libraries and distributed processing tools for larger datasets.

---

# 66. File Handling vs Database Storage

Files and databases serve different purposes.

### Files

Useful for:

- raw data
- logs
- configuration
- exports
- batch input/output

### Databases

Useful for:

- structured queryable data
- transactions
- concurrent access
- indexing
- data integrity

For a data engineering pipeline, files can often serve as raw or intermediate data while databases or data warehouses serve analytical/query workloads.

---

# 67. Important Interview Question — Why Not Use `read()` for Every File?

Because `read()` loads the requested content into memory.

For a small file:

```python
data = file.read()
```

is perfectly reasonable.

For a very large file:

```python
data = file.read()
```

can consume significant memory.

Instead:

```python
for line in file:
    process(line)
```

or:

```python
chunk = file.read(4096)
```

can process data incrementally.

---

# 68. Important Interview Question — What Happens If a File Doesn't Exist in `r` Mode?

Python raises:

```text
FileNotFoundError
```

Example:

```python
with open("missing.txt", "r") as file:
    data = file.read()
```

This can be handled using:

```python
try:
    ...
except FileNotFoundError:
    ...
```

---

# 69. Important Interview Question — Does `w` Create a File?

Yes.

If the specified file does not exist, `w` normally creates it.

If it already exists, its contents are truncated.

```python
with open("new.txt", "w") as file:
    file.write("Hello")
```

---

# 70. Important Interview Question — Does `a` Create a File?

Yes.

If the file doesn't exist, append mode normally creates it.

If it exists, writing occurs at the end.

```python
with open("log.txt", "a") as file:
    file.write("New log\n")
```

---

# 71. Important Interview Question — What Is the Difference Between Text and Binary Mode?

Strong answer:

> Text mode treats the file as text and performs encoding/decoding between strings and bytes. Binary mode works directly with bytes and is appropriate for data such as images, audio, and other binary formats.

---

# 72. Important Interview Question — What Is Encoding and Decoding?

### Encoding

Converting text into bytes.

```text
String → Bytes
```

### Decoding

Converting bytes into text.

```text
Bytes → String
```

For example:

```python
text = "Hello"

data = text.encode("utf-8")

print(data)
```

Then:

```python
text_again = data.decode("utf-8")

print(text_again)
```

---

# 73. Important Interview Question — Why Can Encoding Errors Occur?

If a file is written using one encoding and read using an incompatible encoding, Python may fail to decode some byte sequences correctly.

For example, explicitly using:

```python
encoding="utf-8"
```

when the file is actually encoded differently can result in decoding errors.

The solution is to know or correctly detect the source encoding rather than blindly changing encodings.

---

# 74. Important Interview Question — What Is `newline=""` Used For?

When working with Python's `csv` module, it is recommended to open files with:

```python
open("data.csv", "r", newline="", encoding="utf-8")
```

or when writing:

```python
open("data.csv", "w", newline="", encoding="utf-8")
```

This helps the CSV module handle newline processing correctly across platforms.

---

# 75. Important Interview Question — What Is the Difference Between `file.read()` and `file.read(100)`?

```python
file.read()
```

reads from the current position until the end.

```python
file.read(100)
```

requests up to 100 characters in text mode, or up to 100 bytes in binary mode.

---

# 76. Important Interview Question — What Happens to the File Pointer After `read()`?

The file pointer moves forward as data is read.

Example:

```python
with open("data.txt", "r") as file:
    print(file.tell())

    file.read(5)

    print(file.tell())
```

After reading five simple single-byte characters in a basic ASCII example, the position is typically 5.

`seek()` can move it again.

---

# 77. Important Interview Question — How Do You Read a File From the Beginning Again?

Use:

```python
file.seek(0)
```

Example:

```python
with open("data.txt", "r") as file:
    first = file.read(5)

    file.seek(0)

    complete = file.read()

    print(first)
    print(complete)
```

---

# 78. Important Interview Question — Can We Iterate Over a File Multiple Times?

Yes, but after reaching the end, the file pointer must be repositioned if you want to iterate again.

Example:

```python
with open("data.txt", "r") as file:

    for line in file:
        print(line)

    file.seek(0)

    for line in file:
        print(line)
```

---

# 79. Important Interview Question — How Would You Handle a Huge Log File?

Strong answer:

> I would avoid loading the entire file into memory. I would iterate through it line by line, filter or transform only the records I need, and write the results incrementally. If the data is not line-oriented, I could process it in chunks. For distributed-scale data, I would use an appropriate distributed processing system rather than relying on a single Python process.

---

# 80. Common Mistakes in File Handling

### Mistake 1 — Forgetting to close files

```python
file = open("data.txt")
```

without closing it.

Prefer:

```python
with open("data.txt") as file:
    ...
```

### Mistake 2 — Using `w` when you meant `a`

```python
open("log.txt", "w")
```

can erase previous content.

### Mistake 3 — Loading huge files completely

```python
file.read()
```

can consume a lot of memory.

### Mistake 4 — Manually parsing CSV incorrectly

Avoid:

```python
line.split(",")
```

for general CSV parsing.

Prefer:

```python
import csv
```

### Mistake 5 — Ignoring encoding

For portable text processing, explicitly specify the intended encoding.

---

# 81. Most Important Interview Questions

If you have limited preparation time, prioritize these:

1. What is file handling in Python?
2. What does `open()` do?
3. Explain `r`, `w`, `a`, and `x`.
4. Difference between `w` and `a`.
5. Difference between `read()`, `readline()`, and `readlines()`.
6. What does `with open()` do?
7. Why should we use a context manager for files?
8. What happens if an exception occurs while working with a file?
9. What is a file pointer?
10. What are `tell()` and `seek()`?
11. How do you process a large file efficiently?
12. Text mode vs binary mode.
13. What does `rb` mean?
14. What does `wb` mean?
15. What happens if the file doesn't exist in `r` mode?
16. Does `w` create a file?
17. Does `a` create a file?
18. Difference between `r+`, `w+`, and `a+`.
19. What is encoding?
20. Why use `encoding="utf-8"`?
21. How do you handle `FileNotFoundError`?
22. How do you copy a file?
23. How do you read a file line by line?
24. How would you process a huge log file?
25. How is file handling useful in data engineering?
26. How do you read CSV files?
27. How do you read JSON files?
28. Why shouldn't you manually split CSV data using commas?
29. What is the difference between `write()` and `writelines()`?
30. What happens when you forget to close a file?

---

# 82. Quick Revision Table

| Concept | Remember |
|---|---|
| `open()` | Opens a file |
| `r` | Read |
| `w` | Write + truncate |
| `a` | Append |
| `x` | Create exclusively |
| `b` | Binary |
| `t` | Text |
| `read()` | Read from current position |
| `readline()` | Read one line |
| `readlines()` | Read remaining lines into a list |
| `write()` | Write a string |
| `writelines()` | Write multiple strings |
| `tell()` | Current position |
| `seek()` | Move position |
| `close()` | Close resource |
| `with` | Context-managed resource handling |
| `encoding` | Controls text encoding/decoding |

---

# 83. Final Interview Summary

The basic pattern you should remember is:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

For writing:

```python
with open("data.txt", "w", encoding="utf-8") as file:
    file.write("Hello Python")
```

For appending:

```python
with open("data.txt", "a", encoding="utf-8") as file:
    file.write("\nNew data")
```

For binary files:

```python
with open("image.jpg", "rb") as file:
    data = file.read()
```

For large files:

```python
with open("large_file.txt", "r", encoding="utf-8") as file:
    for line in file:
        process(line)
```

### Final Interview Answer

> File handling in Python allows us to work with persistent data by opening, reading, writing, appending, and processing files. Python provides different modes such as `r`, `w`, `a`, and binary modes depending on the operation. I generally prefer using `with open()` because it manages the file resource safely and closes it even if an exception occurs. For large files, I avoid loading everything into memory and process the data incrementally, for example line by line or in chunks. In data engineering, these concepts are useful when dealing with raw files, logs, CSV or JSON data, and intermediate pipeline data.