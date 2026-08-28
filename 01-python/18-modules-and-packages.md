# 18 — Modules and Packages

## 1. What Is a Module?

A **module** is a Python file (`.py`) that contains Python code such as:

- variables
- functions
- classes
- statements

A module helps us organize code into separate files and reuse it in other programs.

For example, suppose we have:

```text
math_utils.py
```

with:

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

We can use it from another Python file:

```python
import math_utils

print(math_utils.add(10, 5))
print(math_utils.subtract(10, 5))
```

Output:

```text
15
5
```

### Interview Answer

> A module is a Python file containing reusable code such as functions, classes, and variables. Modules help us organize code and avoid duplication.

---

# 2. Why Do We Use Modules?

Modules provide several benefits:

- code reusability
- better organization
- easier maintenance
- separation of responsibilities
- reduced code duplication
- easier testing
- better readability

Instead of keeping everything inside one large Python file:

```text
main.py
```

we can organize it:

```text
project/
│
├── main.py
├── database.py
├── utils.py
├── config.py
└── validation.py
```

Each file can have a specific responsibility.

---

# 3. What Is a Package?

A **package** is a way of organizing related Python modules into a directory structure.

Example:

```text
project/
│
├── main.py
│
└── utilities/
    ├── __init__.py
    ├── math_utils.py
    └── string_utils.py
```

Here:

```text
utilities
```

is the package, while:

```text
math_utils.py
string_utils.py
```

are modules.

### Simple Difference

```text
Package
   ↓
Directory containing related modules
   ↓
Module 1
Module 2
Module 3
```

---

# 4. Module vs Package

| Module | Package |
|---|---|
| Usually a `.py` file | Usually a directory containing modules/subpackages |
| Contains reusable Python code | Organizes related modules |
| Example: `math_utils.py` | Example: `utilities/` |
| Smaller unit | Higher-level organizational structure |

### Interview Answer

> A module is generally a single Python file containing reusable code, while a package is a directory structure used to organize related modules and subpackages.

---

# 5. What Is `import`?

`import` is used to bring a module into the current Python program.

Example:

```python
import math

print(math.sqrt(25))
```

Output:

```text
5.0
```

Here:

```python
import math
```

imports Python's built-in `math` module.

---

# 6. Importing a Specific Function

Instead of importing the complete module:

```python
import math

print(math.sqrt(25))
```

we can import only a specific function:

```python
from math import sqrt

print(sqrt(25))
```

---

# 7. Importing Multiple Functions

```python
from math import sqrt, factorial

print(sqrt(25))
print(factorial(5))
```

---

# 8. Importing Everything Using `*`

Python allows:

```python
from math import *
```

However, this is generally discouraged in production code because it can:

- make it unclear where names came from
- cause naming conflicts
- reduce readability

Prefer:

```python
import math

math.sqrt(25)
```

or:

```python
from math import sqrt

sqrt(25)
```

---

# 9. Import Aliases

We can give a module a shorter name using `as`.

```python
import math as m

print(m.sqrt(25))
```

Another common example:

```python
import pandas as pd
```

Then:

```python
df = pd.DataFrame()
```

### Interview Answer

> An alias gives an imported module or object another local name. It is useful for readability and for commonly used library conventions such as `pandas as pd`.

---

# 10. Module Aliases vs Function Aliases

Module alias:

```python
import math as m
```

Function alias:

```python
from math import sqrt as square_root

print(square_root(25))
```

---

# 11. Standard Library Modules

Python comes with a large standard library.

Examples:

```python
import math
import os
import sys
import json
import csv
import datetime
import random
import re
```

These modules can be used without separately installing third-party packages.

---

# 12. Commonly Used Python Modules

| Module | Common Purpose |
|---|---|
| `math` | Mathematical operations |
| `os` | Operating-system interaction |
| `sys` | Python runtime/system information |
| `json` | JSON processing |
| `csv` | CSV processing |
| `re` | Regular expressions |
| `datetime` | Date and time |
| `random` | Random values |
| `collections` | Specialized container types |
| `pathlib` | Object-oriented filesystem paths |

---

# 13. Creating Your Own Module

Create:

```text
calculator.py
```

Code:

```python
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b
```

Then create:

```text
main.py
```

Code:

```python
import calculator

print(calculator.add(10, 20))
print(calculator.multiply(5, 4))
```

Output:

```text
30
20
```

This is one of the most important practical examples of modules.

---

# 14. Importing From Your Own Module

Suppose:

```text
calculator.py
```

contains:

```python
def add(a, b):
    return a + b
```

Then:

```python
from calculator import add

print(add(10, 20))
```

---

# 15. Module Search Path

When Python executes:

```python
import calculator
```

Python searches locations listed in:

```python
sys.path
```

We can inspect them:

```python
import sys

print(sys.path)
```

The exact entries depend on how Python was launched and the environment.

---

# 16. What Is `sys.path`?

`sys.path` is a list of locations where Python looks for modules when resolving imports.

Example:

```python
import sys

for path in sys.path:
    print(path)
```

This can help diagnose:

```text
ModuleNotFoundError
```

when Python cannot find a module.

---

# 17. What Is `PYTHONPATH`?

`PYTHONPATH` is an environment variable that can be used to add directories to Python's module search path.

Conceptually:

```text
PYTHONPATH
     ↓
Additional module search locations
     ↓
sys.path
```

However, modern Python projects usually prefer proper package/project structures rather than relying heavily on manually configured `PYTHONPATH`.

---

# 18. What Is `__name__`?

Every Python module has a special variable:

```python
__name__
```

When a file is executed directly, its value is:

```text
__main__
```

When it is imported, its value is normally the module's import name.

Example:

```python
print(__name__)
```

If we run that file directly:

```text
__main__
```

---

# 19. What Is `if __name__ == "__main__"`?

This pattern is used to execute code only when the file is run directly, not when it is imported.

Example:

```python
def add(a, b):
    return a + b


if __name__ == "__main__":
    print(add(10, 20))
```

If we run the file directly:

```text
30
```

If another file imports it:

```python
import calculator
```

the code inside:

```python
if __name__ == "__main__":
```

does not execute merely because the module was imported.

### Interview Answer

> `if __name__ == "__main__":` allows a module to have code that runs when the file is executed directly while preventing that code from running automatically when the module is imported.

---

# 20. Why Is `if __name__ == "__main__"` Useful?

It allows a Python file to serve two purposes:

1. reusable module
2. executable script

Example:

```python
def square(n):
    return n * n


if __name__ == "__main__":
    print(square(5))
```

Other modules can import:

```python
square
```

without executing the demonstration/test code.

---

# 21. What Happens When We Import a Module?

When Python imports a module, it generally:

```text
Find module
    ↓
Load module
    ↓
Execute module-level code
    ↓
Create/reuse module object
    ↓
Make its names available through the import
```

This is important because importing a module is not simply copying its text into the current file.

---

# 22. Does Python Execute a Module When It Is Imported?

Yes.

Module-level statements are executed when the module is first imported.

Example:

```python
# test.py

print("Module loaded")
```

Then:

```python
import test
```

prints:

```text
Module loaded
```

This is one reason why executable/test code is often placed inside:

```python
if __name__ == "__main__":
```

---

# 23. What Is Module Caching?

After a module is imported, Python normally stores the loaded module in:

```python
sys.modules
```

Example:

```python
import sys
import math

print("math" in sys.modules)
```

Output:

```text
True
```

This caching helps avoid repeatedly loading and executing the same module during the same Python process.

---

# 24. Can a Module Be Imported More Than Once?

A module can appear in multiple import statements, but within the same Python process, normal imports use the cached module in `sys.modules` rather than executing the module from scratch every time.

Example:

```python
import math
import math
```

Python does not normally re-execute `math` because of the second import.

---

# 25. What Is `importlib.reload()`?

Python provides:

```python
import importlib
```

and:

```python
importlib.reload(module)
```

to re-execute a previously imported module.

Example:

```python
import calculator
import importlib

importlib.reload(calculator)
```

This is mostly useful in interactive development and debugging.

---

# 26. What Is `__init__.py`?

`__init__.py` is a special file associated with Python packages.

Example:

```text
utilities/
│
├── __init__.py
├── math_utils.py
└── string_utils.py
```

It can contain package initialization code and can expose selected names.

Modern Python also supports **namespace packages**, so a regular package directory does not always require an `__init__.py`. However, `__init__.py` remains common and useful for traditional package structures.

---

# 27. What Can Be Written Inside `__init__.py`?

It can contain normal Python code.

For example:

```python
# utilities/__init__.py

VERSION = "1.0"
```

Then:

```python
import utilities

print(utilities.VERSION)
```

---

# 28. Importing From a Package

Suppose:

```text
project/
│
├── main.py
│
└── utilities/
    ├── __init__.py
    └── math_utils.py
```

`math_utils.py`:

```python
def add(a, b):
    return a + b
```

Then:

```python
from utilities.math_utils import add

print(add(10, 20))
```

Output:

```text
30
```

---

# 29. Package Structure Example

A realistic Python project might look like:

```text
project/
│
├── main.py
│
├── config/
│   ├── __init__.py
│   └── settings.py
│
├── database/
│   ├── __init__.py
│   └── connection.py
│
├── services/
│   ├── __init__.py
│   └── user_service.py
│
└── utils/
    ├── __init__.py
    └── helpers.py
```

This separates responsibilities.

---

# 30. Why Packages Are Useful in Real Projects

Imagine an application with thousands of lines of code.

Keeping everything in:

```text
main.py
```

would make the application difficult to maintain.

Instead:

```text
database/
services/
models/
utils/
config/
```

can separate responsibilities.

This improves:

- maintainability
- readability
- testing
- collaboration
- reusability

---

# 31. Absolute Imports

An absolute import specifies the package/module path from the project's import root.

Example:

```python
from utilities.math_utils import add
```

This clearly identifies where `add` comes from.

Absolute imports are often preferred because they make the import source explicit.

---

# 32. Relative Imports

Relative imports use dots to refer to the current package structure.

Example:

```python
from .math_utils import add
```

Here:

```text
.
```

means the current package.

Another example:

```python
from ..utils import helper
```

Here:

```text
..
```

refers to the parent package.

Relative imports are useful inside packages.

---

# 33. Absolute vs Relative Imports

| Absolute Import | Relative Import |
|---|---|
| Uses full package path | Uses `.` / `..` |
| More explicit | Depends on package location |
| Example: `from app.utils import helper` | Example: `from .utils import helper` |
| Common in many projects | Useful inside package structures |

---

# 34. What Is a Third-Party Package?

A third-party package is software created outside Python's standard library.

Examples:

```text
requests
pandas
numpy
FastAPI
SQLAlchemy
PySpark
```

These generally need to be installed separately.

For example:

```bash
pip install requests
```

Then:

```python
import requests
```

---

# 35. What Is `pip`?

`pip` is Python's standard package installer tool.

Example:

```bash
pip install pandas
```

This installs the package into the relevant Python environment.

Other common commands:

```bash
pip uninstall pandas
pip list
pip show pandas
pip freeze
```

---

# 36. What Is `requirements.txt`?

`requirements.txt` is a common file used to record Python dependencies.

Example:

```text
fastapi
sqlalchemy
pandas
requests
```

A user can install them with:

```bash
pip install -r requirements.txt
```

A more reproducible project often pins versions, for example:

```text
pandas==2.3.0
```

The exact versions should match the project's compatibility requirements.

---

# 37. Why Is Dependency Management Important?

Suppose your application uses:

```text
pandas
fastapi
sqlalchemy
```

Another developer needs the same dependencies to run your project.

A dependency file makes it easier to recreate the environment.

```text
Project
   ↓
Dependency list
   ↓
Install dependencies
   ↓
Run project
```

---

# 38. What Is a Virtual Environment?

A virtual environment creates an isolated Python environment for a project.

Example:

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS/Linux:

```bash
source venv/bin/activate
```

Then install packages:

```bash
pip install pandas
```

The project can have its own dependencies without unnecessarily affecting other projects.

---

# 39. Why Use Virtual Environments?

Suppose:

```text
Project A → pandas version X
Project B → pandas version Y
```

Installing everything globally can create dependency conflicts.

Virtual environments isolate dependencies:

```text
Project A
   ↓
venv A
   ↓
Dependencies A

Project B
   ↓
venv B
   ↓
Dependencies B
```

---

# 40. Module vs Library vs Package

These terms are often confused.

### Module

Usually one Python file.

```text
utils.py
```

### Package

A structured collection of Python modules/subpackages.

```text
utils/
```

### Library

A broader term for reusable software functionality. A library can consist of one or many packages/modules.

For interviews, avoid treating these terms as exact synonyms.

---

# 41. What Is a Built-in Module?

A built-in module is provided as part of Python or its standard environment and can be imported without installing a third-party package.

Examples from the standard library:

```python
import math
import os
import json
import sys
```

Note that "built-in module" and "standard-library module" are technically not identical concepts in every implementation detail; for interview purposes, it is safer to say **standard-library module** when referring to modules such as `os`, `json`, and `math`.

---

# 42. What Is `os` Module?

The `os` module provides operating-system-related functionality.

Example:

```python
import os

print(os.getcwd())
```

This returns the current working directory.

Other examples:

```python
print(os.listdir())
```

and:

```python
print(os.environ)
```

---

# 43. What Is `pathlib`?

`pathlib` provides an object-oriented way to work with filesystem paths.

Example:

```python
from pathlib import Path

path = Path("data.txt")

print(path.exists())
```

Reading:

```python
data = path.read_text(encoding="utf-8")
```

Writing:

```python
path.write_text("Hello Python", encoding="utf-8")
```

`pathlib` is often preferred over manually constructing filesystem paths with string concatenation.

---

# 44. What Is `json` Module?

The `json` module is used to encode and decode JSON data.

Example:

```python
import json

data = {
    "name": "Harsha",
    "skill": "Python"
}

json_data = json.dumps(data)

print(json_data)
```

Writing to a file:

```python
with open("data.json", "w", encoding="utf-8") as file:
    json.dump(data, file, indent=4)
```

---

# 45. What Is `csv` Module?

The `csv` module provides functionality for reading and writing CSV files.

Example:

```python
import csv

with open("students.csv", "r", encoding="utf-8", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

---

# 46. What Is a Namespace?

A namespace is a mapping between names and objects.

Modules provide a useful namespace.

Example:

```python
import math

print(math.pi)
```

Here:

```text
math
```

is the module namespace and:

```text
pi
```

is a name inside that namespace.

Using:

```python
math.pi
```

helps avoid conflicts with names in the current program.

---

# 47. Why Is `import module` Sometimes Better Than `from module import *`?

Consider:

```python
import math

math.sqrt(25)
```

It is clear that `sqrt` came from `math`.

With:

```python
from math import *
```

we might write:

```python
sqrt(25)
```

but the source of `sqrt` is less obvious and names can conflict.

### Interview Answer

> I generally prefer explicit imports because they improve readability and reduce namespace pollution and naming conflicts.

---

# 48. What Is Circular Import?

A circular import occurs when modules depend on each other directly or indirectly.

Example:

```text
module_a
   ↓
module_b
   ↓
module_a
```

For example:

```python
# a.py
import b
```

and:

```python
# b.py
import a
```

This can cause partially initialized modules or import errors.

---

# 49. How Can We Avoid Circular Imports?

Common approaches include:

- reorganizing responsibilities
- moving shared functionality into a third module
- reducing unnecessary dependencies
- using local imports only when appropriate

For example:

```text
a.py ─────┐
          ↓
       common.py
          ↑
          │
b.py ─────┘
```

Instead of:

```text
a.py ↔ b.py
```

---

# 50. What Is `ModuleNotFoundError`?

Python raises:

```text
ModuleNotFoundError
```

when it cannot find a module that is being imported.

Example:

```python
import something_that_does_not_exist
```

Possible reasons include:

- package not installed
- wrong import path
- incorrect environment
- module not located on the search path
- typo in module name

---

# 51. `ModuleNotFoundError` vs `ImportError`

`ModuleNotFoundError` is a more specific import-related error.

Example:

```python
import missing_module
```

can raise:

```text
ModuleNotFoundError
```

An `ImportError` can occur in other import situations, such as when a requested name cannot be imported from an existing module.

Example:

```python
from math import something_that_does_not_exist
```

---

# 52. What Is Lazy Import?

A lazy import means delaying an import until it is actually needed.

Example:

```python
def generate_report():
    import pandas as pd

    return pd.DataFrame()
```

Here `pandas` is imported when the function is called rather than at module import time.

This can sometimes help with:

- optional dependencies
- startup time
- circular-import workarounds in limited situations

However, it should not be used as a general replacement for proper project structure.

---

# 53. What Is `__all__`?

A module can define:

```python
__all__ = ["add", "subtract"]
```

This specifies names intended for wildcard imports:

```python
from calculator import *
```

It is mainly useful for controlling what names are exported by wildcard imports.

Explicit imports are generally clearer.

---

# 54. What Is Package Initialization?

When a package is imported, package-level initialization code may execute.

For example:

```python
# utilities/__init__.py

print("Utilities package loaded")
```

Then:

```python
import utilities
```

can execute that initialization code.

Therefore, package initialization should generally be kept simple and predictable.

---

# 55. What Is a Subpackage?

A package can contain another package.

Example:

```text
project/
│
└── app/
    ├── __init__.py
    │
    └── services/
        ├── __init__.py
        └── users/
            ├── __init__.py
            └── service.py
```

Here:

```text
app
```

is a package,

```text
services
```

is a subpackage,

and:

```text
users
```

is another nested package.

---

# 56. Practical Project Example

Consider a Python backend:

```text
flight_booking/
│
├── main.py
│
├── config/
│   ├── __init__.py
│   └── settings.py
│
├── models/
│   ├── __init__.py
│   └── flight.py
│
├── services/
│   ├── __init__.py
│   └── booking_service.py
│
├── database/
│   ├── __init__.py
│   └── connection.py
│
└── utils/
    ├── __init__.py
    └── validators.py
```

The responsibilities are separated.

For example:

```python
from services.booking_service import create_booking
from database.connection import get_connection
```

This makes the project easier to understand than putting everything inside `main.py`.

---

# 57. Practical Data Engineering Example

A data engineering project could be structured as:

```text
data_pipeline/
│
├── main.py
│
├── config/
│   └── settings.py
│
├── ingestion/
│   └── source_reader.py
│
├── transformation/
│   └── clean_data.py
│
├── validation/
│   └── validate.py
│
└── utils/
    └── helpers.py
```

Then:

```python
from ingestion.source_reader import read_source
from transformation.clean_data import clean_data
from validation.validate import validate_data
```

This follows separation of responsibilities.

---

# 58. Modules in a Full-Stack Python Application

A FastAPI project might contain:

```text
app/
│
├── main.py
├── models/
├── schemas/
├── routes/
├── services/
├── database/
└── utils/
```

For example:

```python
from app.services.user_service import create_user
```

This demonstrates why understanding modules and packages is useful for Python backend development.

---

# 59. Common Interview Coding Question — Create a Custom Module

### `calculator.py`

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
```

### `main.py`

```python
import calculator

print(calculator.add(10, 5))
print(calculator.subtract(10, 5))
```

Output:

```text
15
5
```

---

# 60. Coding Question — Import a Function From a Module

### `calculator.py`

```python
def multiply(a, b):
    return a * b
```

### `main.py`

```python
from calculator import multiply

print(multiply(5, 4))
```

Output:

```text
20
```

---

# 61. Coding Question — Use `__name__`

```python
def greet():
    print("Hello")


if __name__ == "__main__":
    greet()
```

If the file is executed directly:

```text
Hello
```

If imported:

```python
import greeting
```

the `greet()` call inside the main guard does not execute automatically.

---

# 62. Coding Question — Create a Package

Structure:

```text
project/
│
├── main.py
│
└── calculations/
    ├── __init__.py
    └── arithmetic.py
```

`arithmetic.py`:

```python
def add(a, b):
    return a + b
```

`main.py`:

```python
from calculations.arithmetic import add

print(add(10, 20))
```

Output:

```text
30
```

---

# 63. Coding Question — Create a Utility Module

### `utils.py`

```python
def is_even(n):
    return n % 2 == 0


def square(n):
    return n * n
```

### `main.py`

```python
from utils import is_even, square

print(is_even(10))
print(square(5))
```

Output:

```text
True
25
```

---

# 64. Important Interview Question — What Is the Difference Between `import module` and `from module import function`?

Using:

```python
import math
```

requires:

```python
math.sqrt(25)
```

Using:

```python
from math import sqrt
```

allows:

```python
sqrt(25)
```

The first keeps the module namespace explicit.

The second imports the specific name into the current namespace.

---

# 65. Important Interview Question — What Is the Difference Between a Module and a Library?

A module is generally one Python file containing reusable code.

A library is a broader collection of reusable functionality and can contain multiple modules and packages.

### Interview Answer

> A module is a single reusable unit, usually a Python file, while a library is a broader collection of reusable functionality that may contain multiple modules and packages.

---

# 66. Important Interview Question — What Is the Difference Between a Package and a Module?

### Module

```text
math_utils.py
```

### Package

```text
utilities/
├── __init__.py
├── math_utils.py
└── string_utils.py
```

### Interview Answer

> A module is generally a single Python file, while a package organizes related modules and possibly subpackages into a directory structure.

---

# 67. Important Interview Question — Why Do We Use Packages?

### Strong Answer

> Packages help organize a large application into logical components. Instead of putting all functionality into one file, we can separate database logic, business logic, configuration, utilities, and models into different modules and packages. This improves maintainability, readability, testing, and code reuse.

---

# 68. Important Interview Question — What Is `__name__ == "__main__"`?

### Strong Answer

> `__name__` tells us how the current module is being used. When the file is executed directly, `__name__` is `"__main__"`. When the file is imported, it normally contains the module's import name. Therefore, `if __name__ == "__main__":` is used to run script-specific code only when the file is executed directly.

---

# 69. Important Interview Question — What Happens During Import?

### Strong Answer

> Python resolves the module using its import system and search path, loads the module, executes its module-level code, and makes the module available through the import. The loaded module is normally cached in `sys.modules`, so subsequent imports in the same process generally reuse it.

---

# 70. Important Interview Question — What Is `sys.path`?

### Strong Answer

> `sys.path` is the list of locations Python searches when resolving imports. It includes locations determined by the Python installation, the execution environment, and the current project context. If Python cannot find a module in those locations, we may get `ModuleNotFoundError`.

---

# 71. Important Interview Question — What Is a Circular Import?

### Strong Answer

> A circular import occurs when two modules directly or indirectly depend on each other during import. It can result in partially initialized modules or import errors. A common solution is to reorganize shared functionality into a separate module and reduce unnecessary dependencies between modules.

---

# 72. Important Interview Question — What Is `pip`?

### Strong Answer

> `pip` is Python's package installation tool. It is commonly used to install, upgrade, remove, and inspect Python packages, for example using `pip install pandas`.

---

# 73. Important Interview Question — What Is a Virtual Environment?

### Strong Answer

> A virtual environment provides an isolated Python environment for a project. It allows each project to have its own dependency versions and helps prevent dependency conflicts between projects.

---

# 74. Important Interview Question — What Is `requirements.txt`?

### Strong Answer

> `requirements.txt` is a common dependency file that lists packages required by a Python project. Another developer can install those dependencies using `pip install -r requirements.txt`. In production projects, dependency versions are often pinned or otherwise managed for reproducibility.

---

# 75. Important Interview Question — How Do You Organize a Large Python Project?

### Strong Answer

> I would separate the project based on responsibilities. For example, I could keep configuration in a config package, database-related functionality in a database package, business logic in services, reusable helpers in utils, and data models in models. This keeps individual modules focused and makes the project easier to maintain and test.

---

# 76. Important Interview Question — Why Avoid `from module import *`?

### Strong Answer

> I avoid wildcard imports because they make it difficult to understand where names came from, can introduce naming conflicts, and can pollute the current namespace. Explicit imports are generally clearer and easier to maintain.

---

# 77. Important Interview Question — Can a Python File Be Both a Module and a Script?

Yes.

Example:

```python
def add(a, b):
    return a + b


if __name__ == "__main__":
    print(add(10, 20))
```

It can be:

```text
executed directly → script
```

or:

```text
imported → module
```

---

# 78. Important Interview Question — Why Is Code Organization Important?

A good answer:

> Good organization separates responsibilities and prevents a codebase from becoming difficult to maintain. Modules and packages allow us to keep related functionality together while keeping unrelated functionality separate. This also makes testing, debugging, collaboration, and reuse easier.

---

# 79. Important Interview Question — What Is the Difference Between Standard Library and Third-Party Packages?

### Standard Library

Comes with Python.

Examples:

```python
import os
import json
import math
```

### Third-Party

Installed separately.

Examples:

```text
pandas
numpy
requests
fastapi
sqlalchemy
pyspark
```

### Interview Answer

> Standard-library modules are provided with Python, while third-party packages are developed separately and generally need to be installed into the environment.

---

# 80. Important Interview Question — How Would You Debug `ModuleNotFoundError`?

A practical approach:

```text
1. Check the spelling of the module.
2. Check whether the package is installed.
3. Check which Python interpreter is being used.
4. Check the active virtual environment.
5. Check sys.path if necessary.
6. Check the project/package structure.
```

For example:

```python
import sys

print(sys.executable)
print(sys.path)
```

This helps determine which Python environment is executing the code.

---

# 81. Interview Coding Practice

## Question 1

Create a module named `temperature.py` with a function that converts Celsius to Fahrenheit.

### Answer

```python
# temperature.py

def celsius_to_fahrenheit(celsius):
    return (celsius * 9 / 5) + 32
```

Use it:

```python
from temperature import celsius_to_fahrenheit

print(celsius_to_fahrenheit(25))
```

Output:

```text
77.0
```

---

## Question 2

Create a module containing a function that checks whether a number is positive.

### Answer

```python
# number_utils.py

def is_positive(n):
    return n > 0
```

Use:

```python
from number_utils import is_positive

print(is_positive(10))
```

Output:

```text
True
```

---

## Question 3

Write code that runs only when a Python file is executed directly.

### Answer

```python
def main():
    print("Program started")


if __name__ == "__main__":
    main()
```

---

## Question 4

Create a package with a utility function.

### Answer

Structure:

```text
project/
│
├── main.py
│
└── utils/
    ├── __init__.py
    └── calculator.py
```

`calculator.py`:

```python
def add(a, b):
    return a + b
```

`main.py`:

```python
from utils.calculator import add

print(add(5, 10))
```

---

# 82. Real-World Example — Data Engineering

Imagine a data pipeline:

```text
data_pipeline/
│
├── main.py
│
├── ingestion/
│   └── reader.py
│
├── transformation/
│   └── transform.py
│
├── validation/
│   └── validator.py
│
└── utils/
    └── logger.py
```

`reader.py`:

```python
def read_data():
    print("Reading source data")
```

`transform.py`:

```python
def transform_data(data):
    return data
```

`validator.py`:

```python
def validate_data(data):
    return True
```

`main.py`:

```python
from ingestion.reader import read_data
from transformation.transform import transform_data
from validation.validator import validate_data

data = read_data()
data = transform_data(data)

if validate_data(data):
    print("Data is valid")
```

The important idea is that each module has a focused responsibility.

---

# 83. Real-World Example — Python Full Stack

A backend application could be organized as:

```text
app/
│
├── main.py
├── routes/
├── services/
├── models/
├── schemas/
├── database/
└── utils/
```

For example:

```python
from app.services.user_service import create_user
```

The route handles the API request, the service handles business logic, the model represents database data, and the database package manages persistence.

This separation prevents the API route from becoming responsible for everything.

---

# 84. Real-World Example — Reusable Utility Module

Instead of repeatedly writing:

```python
def clean_text(text):
    return text.strip().lower()
```

in multiple files, create:

```text
utils.py
```

```python
def clean_text(text):
    return text.strip().lower()
```

Then reuse it:

```python
from utils import clean_text

name = clean_text("  HARsha  ")

print(name)
```

Output:

```text
harsha
```

This demonstrates the main purpose of modules: **reuse and organization**.

---

# 85. Common Mistakes

### Mistake 1 — Using wildcard imports

Avoid:

```python
from module import *
```

Prefer:

```python
from module import function
```

or:

```python
import module
```

### Mistake 2 — Putting all application logic into one file

Large projects should be separated into logical modules.

### Mistake 3 — Creating unnecessary circular dependencies

Keep dependencies between modules clear.

### Mistake 4 — Installing packages globally for every project

Prefer virtual environments.

### Mistake 5 — Confusing module and package

Remember:

```text
module → usually a .py file
package → organized collection of modules/subpackages
```

---

# 86. Quick Revision

```text
Module
  ↓
Usually a Python .py file

Package
  ↓
Organized collection of modules/subpackages

import
  ↓
Import a module/name

from ... import ...
  ↓
Import a specific name

as
  ↓
Create an alias

__name__
  ↓
Special module variable

__main__
  ↓
Indicates direct execution

if __name__ == "__main__":
  ↓
Run code only when directly executed

sys.path
  ↓
Module search locations

sys.modules
  ↓
Loaded module cache

pip
  ↓
Install/manage packages

venv
  ↓
Isolated Python environment

requirements.txt
  ↓
Project dependencies
```

---

# 87. Must-Know Interview Questions

Before an interview, make sure you can answer these without memorizing word-for-word:

1. What is a module in Python?
2. What is a package?
3. Difference between a module and a package?
4. Why do we use modules?
5. Why do we use packages?
6. What does `import` do?
7. Difference between `import module` and `from module import function`.
8. What is an import alias?
9. Why should we avoid wildcard imports?
10. What is `__name__`?
11. What is `__main__`?
12. Why do we use `if __name__ == "__main__"`?
13. What happens when a module is imported?
14. Does Python execute module-level code during import?
15. What is `sys.path`?
16. What is `sys.modules`?
17. What is `ModuleNotFoundError`?
18. Difference between `ModuleNotFoundError` and `ImportError`.
19. What is `__init__.py`?
20. Is `__init__.py` always required for a package?
21. What is a subpackage?
22. What is an absolute import?
23. What is a relative import?
24. Difference between absolute and relative imports.
25. What is a circular import?
26. How can circular imports be avoided?
27. What is a standard-library module?
28. What is a third-party package?
29. What is `pip`?
30. What is `requirements.txt`?
31. Why do we use virtual environments?
32. What is a namespace?
33. What is `__all__`?
34. What is lazy importing?
35. How would you organize a large Python project?
36. How are modules useful in data engineering?
37. How are modules useful in backend/full-stack development?
38. How would you debug `ModuleNotFoundError`?
39. Can one Python file act as both a module and a script?
40. What happens if the same module is imported multiple times?

---

# 88. Final Interview Summary

The most important concepts from this topic are:

```text
Module
    ↓
Reusable Python file

Package
    ↓
Organized collection of modules

Import
    ↓
Reuse code from another module/package

__name__
    ↓
Identifies the module's execution context

__main__
    ↓
Directly executed module

sys.path
    ↓
Where Python searches for imports

sys.modules
    ↓
Loaded module cache

pip
    ↓
Package management

Virtual environment
    ↓
Dependency isolation
```

### Strong Final Interview Answer

> Python provides modules and packages to organize and reuse code. A module is generally a Python file containing functions, classes, or other reusable code, while packages organize related modules into a structured project. I can use `import` or `from ... import ...` to reuse functionality. For larger applications, I separate responsibilities into packages such as models, services, database, configuration, and utilities. I also use virtual environments to isolate project dependencies and dependency files such as `requirements.txt` to make the environment easier to reproduce. Understanding imports, `__name__ == "__main__"`, `sys.path`, module caching, and circular imports is important for debugging and maintaining Python projects.