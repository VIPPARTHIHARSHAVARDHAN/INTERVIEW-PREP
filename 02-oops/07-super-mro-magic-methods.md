# 07 — `super()`, MRO, and Magic Methods

## 1. What is `super()` in Python?

### Answer

`super()` is used to access methods and attributes from a parent class without directly referring to the parent class by name.

It is commonly used when a child class overrides a method but still wants to use the parent's implementation.

### Example

```python
class Parent:
    def show(self):
        print("Parent show")


class Child(Parent):
    def show(self):
        super().show()
        print("Child show")


obj = Child()

obj.show()
```

Output:

```text
Parent show
Child show
```

Here:

```python
super().show()
```

calls the implementation of `show()` from the parent according to Python's method resolution order.

---

## 2. Why is `super()` Used?

### Answer

`super()` is mainly used to:

- Reuse parent-class functionality
- Avoid directly hardcoding the parent class name
- Call a parent constructor
- Support multiple inheritance
- Follow Python's Method Resolution Order (MRO)

It is especially important when working with inheritance and multiple inheritance.

---

## 3. How Do You Call a Parent Constructor Using `super()`?

### Example

```python
class Parent:
    def __init__(self, name):
        self.name = name


class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age


obj = Child("Harsha", 22)

print(obj.name)
print(obj.age)
```

Output:

```text
Harsha
22
```

Here:

```python
super().__init__(name)
```

calls the parent constructor.

---

## 4. Why Use `super().__init__()` Instead of `Parent.__init__()`?

### Answer

Both can call the parent constructor in simple inheritance, but `super()` is generally preferred because it works with Python's MRO and cooperative multiple inheritance.

Instead of:

```python
Parent.__init__(self, name)
```

we can write:

```python
super().__init__(name)
```

This makes the code more flexible when the inheritance structure becomes more complex.

---

## 5. Does `super()` Always Mean "Parent Class"?

### Best Answer

Not exactly.

A common simplified explanation is that `super()` calls the parent class, but technically it means:

> `super()` returns a proxy object that delegates method lookup to the next class in the Method Resolution Order (MRO).

This distinction becomes important in multiple inheritance.

---

# Method Resolution Order (MRO)

## 6. What is MRO?

### Answer

**MRO stands for Method Resolution Order.**

It defines the order in which Python searches classes when looking for a method or attribute.

For a simple inheritance hierarchy:

```python
class Parent:
    pass


class Child(Parent):
    pass
```

the MRO is approximately:

```text
Child
Parent
object
```

Python checks the child first, then the parent, and finally `object`.

---

## 7. How Can We See the MRO?

Python provides:

```python
__mro__
```

and:

```python
mro()
```

### Example

```python
class A:
    pass


class B(A):
    pass


print(B.__mro__)
print(B.mro())
```

Output will be similar to:

```text
(<class '__main__.B'>, <class '__main__.A'>, <class 'object'>)
[<class '__main__.B'>, <class '__main__.A'>, <class 'object'>]
```

The exact module name in the output can vary.

---

## 8. What is `object` in Python?

### Answer

`object` is the base class of Python's class hierarchy.

When we create a normal class:

```python
class Student:
    pass
```

it ultimately inherits from `object`.

Therefore the MRO contains:

```text
Student
object
```

This is why:

```python
Student.mro()
```

includes `object`.

---

## 9. What Happens When a Method Exists in Both Parent and Child?

### Answer

Python searches according to the MRO.

### Example

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        print("Child")


obj = Child()

obj.show()
```

Output:

```text
Child
```

Python checks `Child` first.

Since `Child` contains `show()`, Python uses that implementation.

---

## 10. What Happens If the Child Does Not Have the Method?

### Example

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    pass


obj = Child()

obj.show()
```

Output:

```text
Parent
```

Python does not find `show()` in `Child`, so it continues according to the MRO and finds it in `Parent`.

---

# MRO and Multiple Inheritance

## 11. What is Multiple Inheritance?

### Answer

Multiple inheritance means a class inherits from more than one parent class.

### Example

```python
class A:
    def show(self):
        print("A")


class B:
    def show(self):
        print("B")


class C(A, B):
    pass


obj = C()

obj.show()
```

Output:

```text
A
```

The order:

```python
class C(A, B)
```

affects the MRO.

---

## 12. What is the MRO of Multiple Inheritance?

### Example

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass


print(C.mro())
```

The result is approximately:

```text
C
A
B
object
```

Therefore, if `C` does not contain a method, Python checks:

```text
C → A → B → object
```

---

## 13. How Does MRO Decide Which Method to Call?

### Example

```python
class A:
    def show(self):
        print("A")


class B:
    def show(self):
        print("B")


class C(A, B):
    pass


obj = C()

obj.show()
```

Output:

```text
A
```

Because the MRO is:

```text
C → A → B → object
```

Python finds `show()` in `A` first.

---

# Diamond Inheritance

## 14. What is the Diamond Problem?

### Answer

The diamond problem occurs when a class inherits from two classes that both inherit from the same base class.

The structure looks like:

```text
        A
       / \
      B   C
       \ /
        D
```

Example:

```python
class A:
    def show(self):
        print("A")


class B(A):
    pass


class C(A):
    pass


class D(B, C):
    pass


obj = D()

obj.show()
```

Python uses MRO to determine the lookup order.

---

## 15. What is the MRO of the Diamond Example?

```python
print(D.mro())
```

The order is approximately:

```text
D
B
C
A
object
```

So Python searches:

```text
D → B → C → A → object
```

This avoids blindly calling the same ancestor multiple times.

---

# C3 Linearization

## 16. What is C3 Linearization?

### Answer

Python uses an algorithm called **C3 Linearization** to calculate the MRO for multiple inheritance.

You usually do not need to implement C3 Linearization in an interview.

A safe interview answer is:

> Python uses C3 Linearization to create a consistent Method Resolution Order in multiple inheritance while preserving the local precedence order and avoiding inconsistent inheritance ordering.

---

## 17. What Should You Know About C3 Linearization for Interviews?

### Answer

For most Python interviews, knowing these points is enough:

```text
C3 Linearization
        ↓
Used to calculate MRO
        ↓
Important for multiple inheritance
        ↓
Produces a consistent method lookup order
```

You generally do not need to manually calculate complex C3 sequences unless the interviewer specifically asks.

---

# `super()` with Multiple Inheritance

## 18. Why is `super()` Important in Multiple Inheritance?

### Answer

In multiple inheritance, `super()` follows the MRO instead of simply calling one specific parent.

This allows classes to cooperate with each other.

### Example

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        super().show()
        print("B")


class C(B):
    def show(self):
        super().show()
        print("C")


obj = C()

obj.show()
```

Output:

```text
A
B
C
```

The lookup follows:

```text
C → B → A → object
```

---

## 19. Example of Cooperative Multiple Inheritance

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        super().show()
        print("B")


class C(A):
    def show(self):
        super().show()
        print("C")


class D(B, C):
    def show(self):
        super().show()
        print("D")


obj = D()

obj.show()
```

Output:

```text
A
C
B
D
```

The important point is that `super()` follows the MRO rather than simply meaning "call my direct parent."

The MRO is:

```python
print(D.mro())
```

approximately:

```text
D
B
C
A
object
```

Each `super()` continues to the next class in that order.

---

## 20. What is the Difference Between `super()` and Direct Parent Call?

### Example

Direct parent call:

```python
Parent.method(self)
```

Using `super()`:

```python
super().method()
```

### Important Difference

`Parent.method(self)` explicitly chooses `Parent`.

`super().method()` follows the MRO and chooses the next appropriate implementation.

This is particularly important in multiple inheritance.

---

# Magic Methods

## 21. What are Magic Methods?

### Answer

Magic methods are special methods in Python whose names usually start and end with double underscores.

They are also called **dunder methods**.

Examples:

```python
__init__()
__str__()
__repr__()
__len__()
__add__()
__eq__()
__lt__()
__iter__()
__next__()
```

They allow classes to interact with Python's built-in syntax and operations.

---

## 22. Why are Magic Methods Important?

### Answer

Magic methods allow custom objects to behave like built-in Python objects.

For example:

```python
len(obj)
```

can work if the class defines:

```python
__len__()
```

Similarly:

```python
obj1 + obj2
```

can work through:

```python
__add__()
```

This allows us to make classes behave naturally with Python syntax.

---

## 23. What is `__init__()`?

### Answer

`__init__()` is an initializer method that runs automatically when an object is created.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Harsha")

print(student.name)
```

Output:

```text
Harsha
```

Strictly speaking, `__init__()` initializes an already-created instance; object creation itself involves `__new__()`.

For normal application-level Python code, `__init__()` is the method commonly used to initialize object state.

---

## 24. What is `__new__()`?

### Answer

`__new__()` is responsible for creating and returning a new instance.

It runs before `__init__()`.

The general order is:

```text
__new__()
   ↓
Object is created
   ↓
__init__()
   ↓
Object is initialized
```

Example:

```python
class Student:
    def __new__(cls):
        print("__new__ called")
        return super().__new__(cls)

    def __init__(self):
        print("__init__ called")


student = Student()
```

Output:

```text
__new__ called
__init__ called
```

For normal classes, you usually only need to implement `__init__()`.

---

## 25. `__new__()` vs `__init__()`

| `__new__()` | `__init__()` |
|---|---|
| Creates/returns the instance | Initializes the instance |
| Called first | Called after `__new__()` |
| Receives `cls` | Receives `self` |
| More advanced use cases | Commonly used in normal classes |

### Interview Answer

> `__new__()` is responsible for creating the object, while `__init__()` initializes the object's state after it has been created.

---

## 26. What is `__str__()`?

### Answer

`__str__()` defines the user-friendly string representation of an object.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student: {self.name}"


student = Student("Harsha")

print(student)
```

Output:

```text
Student: Harsha
```

---

## 27. What is `__repr__()`?

### Answer

`__repr__()` provides a representation intended to be useful for developers and debugging.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Student({self.name!r})"


student = Student("Harsha")

print(repr(student))
```

Output:

```text
Student('Harsha')
```

---

## 28. Difference Between `__str__()` and `__repr__()`

### Answer

`__str__()` is intended to provide a readable representation for users.

`__repr__()` is intended to provide a more detailed or developer-friendly representation.

Example:

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student name: {self.name}"

    def __repr__(self):
        return f"Student({self.name!r})"
```

Then:

```python
student = Student("Harsha")

print(student)
print(repr(student))
```

Output:

```text
Student name: Harsha
Student('Harsha')
```

---

## 29. What is `__len__()`?

### Answer

`__len__()` defines the behavior of the built-in `len()` function for an object.

### Example

```python
class Team:
    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)


team = Team(["A", "B", "C"])

print(len(team))
```

Output:

```text
3
```

---

## 30. What is `__add__()`?

### Answer

`__add__()` defines the behavior of the `+` operator for objects.

### Example

```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Number(self.value + other.value)


num1 = Number(10)
num2 = Number(20)

result = num1 + num2

print(result.value)
```

Output:

```text
30
```

---

## 31. What is `__eq__()`?

### Answer

`__eq__()` defines equality comparison using `==`.

### Example

```python
class Student:
    def __init__(self, roll_no):
        self.roll_no = roll_no

    def __eq__(self, other):
        return self.roll_no == other.roll_no


student1 = Student(101)
student2 = Student(101)

print(student1 == student2)
```

Output:

```text
True
```

---

## 32. What is `__lt__()`?

### Answer

`__lt__()` defines the behavior of the `<` operator.

### Example

```python
class Student:
    def __init__(self, marks):
        self.marks = marks

    def __lt__(self, other):
        return self.marks < other.marks


student1 = Student(70)
student2 = Student(90)

print(student1 < student2)
```

Output:

```text
True
```

---

## 33. What is `__contains__()`?

### Answer

`__contains__()` defines the behavior of the `in` operator.

### Example

```python
class Team:
    def __init__(self, members):
        self.members = members

    def __contains__(self, member):
        return member in self.members


team = Team(["A", "B", "C"])

print("B" in team)
```

Output:

```text
True
```

---

## 34. What is `__call__()`?

### Answer

`__call__()` allows an object to be called like a function.

### Example

```python
class Greeting:
    def __call__(self, name):
        print("Hello", name)


greet = Greeting()

greet("Harsha")
```

Output:

```text
Hello Harsha
```

Normally:

```python
greet(...)
```

requires `greet` to be callable.

Defining `__call__()` makes the instance callable.

---

## 35. What is `__iter__()`?

### Answer

`__iter__()` defines how an object provides an iterator.

It is commonly used with:

```python
for
```

### Example

```python
class Numbers:
    def __init__(self, values):
        self.values = values

    def __iter__(self):
        return iter(self.values)


numbers = Numbers([10, 20, 30])

for number in numbers:
    print(number)
```

Output:

```text
10
20
30
```

---

## 36. What is `__next__()`?

### Answer

`__next__()` defines how the next item is obtained from an iterator.

A custom iterator normally implements both:

```python
__iter__()
__next__()
```

### Example

```python
class Counter:
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


counter = Counter(3)

for number in counter:
    print(number)
```

Output:

```text
1
2
3
```

---

# Common Magic Methods

## 37. Important Magic Methods to Know

| Magic Method | Purpose |
|---|---|
| `__init__()` | Initialize object |
| `__new__()` | Create object |
| `__str__()` | User-friendly string representation |
| `__repr__()` | Developer-oriented representation |
| `__len__()` | Behavior of `len()` |
| `__add__()` | Behavior of `+` |
| `__sub__()` | Behavior of `-` |
| `__mul__()` | Behavior of `*` |
| `__eq__()` | Behavior of `==` |
| `__lt__()` | Behavior of `<` |
| `__gt__()` | Behavior of `>` |
| `__contains__()` | Behavior of `in` |
| `__call__()` | Make an object callable |
| `__iter__()` | Return iterator |
| `__next__()` | Return next iterator item |

You do not need to memorize every magic method.

Focus first on the commonly asked ones.

---

# Practical Interview Examples

## 38. Real-World Example — Data Processing Objects

Suppose a data-processing object stores records.

We can implement `__len__()` so that the number of records can be obtained naturally.

```python
class DataSet:
    def __init__(self, records):
        self.records = records

    def __len__(self):
        return len(self.records)


data = DataSet([
    {"id": 1},
    {"id": 2},
    {"id": 3}
])

print(len(data))
```

Output:

```text
3
```

This makes the custom class behave naturally with Python's built-in `len()` function.

---

## 39. Real-World Example — Custom Data Objects

Suppose we have a data object representing a record.

```python
class DataRecord:
    def __init__(self, record_id, value):
        self.record_id = record_id
        self.value = value

    def __str__(self):
        return f"Record {self.record_id}: {self.value}"

    def __eq__(self, other):
        return self.record_id == other.record_id
```

Now:

```python
record1 = DataRecord(101, 500)
record2 = DataRecord(101, 700)

print(record1)
print(record1 == record2)
```

Output:

```text
Record 101: 500
True
```

Here:

```python
__str__()
```

controls the readable representation, while:

```python
__eq__()
```

controls equality.

---

# Coding Questions

## 40. Coding Question — Use `super()`

### Question

Create a parent class and child class. Use `super()` to call the parent method.

### Solution

```python
class Parent:
    def show(self):
        print("Parent method")


class Child(Parent):
    def show(self):
        super().show()
        print("Child method")


obj = Child()

obj.show()
```

Output:

```text
Parent method
Child method
```

---

## 41. Coding Question — Call Parent Constructor

### Solution

```python
class Person:
    def __init__(self, name):
        self.name = name


class Employee(Person):
    def __init__(self, name, salary):
        super().__init__(name)
        self.salary = salary


employee = Employee("Harsha", 50000)

print(employee.name)
print(employee.salary)
```

Output:

```text
Harsha
50000
```

---

## 42. Coding Question — Find MRO

### Solution

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass


print(C.mro())
```

Output is approximately:

```text
[<class '__main__.C'>,
 <class '__main__.B'>,
 <class '__main__.A'>,
 <class 'object'>]
```

---

## 43. Coding Question — Multiple Inheritance and MRO

### Solution

```python
class A:
    def show(self):
        print("A")


class B(A):
    pass


class C(A):
    def show(self):
        print("C")


class D(B, C):
    pass


obj = D()

obj.show()

print(D.mro())
```

Output:

```text
C
```

The MRO is approximately:

```text
D → B → C → A → object
```

`B` does not define `show()`, so Python continues to `C`.

---

## 44. Coding Question — Custom `__str__()`

### Solution

```python
class Employee:
    def __init__(self, name, role):
        self.name = name
        self.role = role

    def __str__(self):
        return f"{self.name} - {self.role}"


employee = Employee("Harsha", "Data Engineer")

print(employee)
```

Output:

```text
Harsha - Data Engineer
```

---

## 45. Coding Question — Custom `__add__()`

### Solution

```python
class Salary:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Salary(self.amount + other.amount)


salary1 = Salary(30000)
salary2 = Salary(20000)

total = salary1 + salary2

print(total.amount)
```

Output:

```text
50000
```

---

## 46. Coding Question — Custom `__len__()`

### Solution

```python
class Data:
    def __init__(self, values):
        self.values = values

    def __len__(self):
        return len(self.values)


data = Data([10, 20, 30, 40])

print(len(data))
```

Output:

```text
4
```

---

## 47. Coding Question — Custom Iterator Using `__iter__()` and `__next__()`

### Solution

```python
class Counter:
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


counter = Counter(5)

for value in counter:
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

# Frequently Asked Interview Questions

## 48. What is `super()`?

### Best Answer

`super()` returns a proxy that allows us to access the next implementation in the Method Resolution Order. It is commonly used to reuse parent-class functionality and is especially useful in multiple inheritance.

---

## 49. Why is `super()` preferred over directly calling the parent class?

### Best Answer

Directly calling the parent class hardcodes a specific class, while `super()` follows the MRO. This makes the code more flexible and suitable for cooperative multiple inheritance.

---

## 50. Does `super()` always call the direct parent?

### Best Answer

No.

`super()` follows the Method Resolution Order and calls the next appropriate class in that order.

This is especially important in multiple inheritance.

---

## 51. What is MRO?

### Best Answer

MRO stands for Method Resolution Order. It defines the order in which Python searches classes for methods and attributes, especially when inheritance and multiple inheritance are involved.

We can inspect it using:

```python
ClassName.mro()
```

or:

```python
ClassName.__mro__
```

---

## 52. What is the MRO of a simple inheritance hierarchy?

### Answer

For:

```python
class A:
    pass


class B(A):
    pass
```

the MRO is:

```text
B → A → object
```

---

## 53. What is the MRO of multiple inheritance?

### Example

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass
```

The MRO is:

```text
C → A → B → object
```

---

## 54. What is the diamond problem?

### Best Answer

The diamond problem occurs when multiple inheritance creates a hierarchy where two parent classes share the same base class.

Python solves the method lookup problem using MRO and C3 Linearization.

---

## 55. What is C3 Linearization?

### Best Answer

C3 Linearization is the algorithm Python uses to calculate a consistent MRO for multiple inheritance.

It preserves the inheritance ordering rules and avoids inconsistent method lookup sequences.

---

## 56. What are magic methods?

### Best Answer

Magic methods, also called dunder methods, are special methods with names surrounded by double underscores.

Examples include:

```python
__init__()
__str__()
__repr__()
__len__()
__add__()
__eq__()
```

They allow custom objects to work with Python's built-in syntax and operations.

---

## 57. What is `__init__()`?

### Best Answer

`__init__()` is an initializer that is called after an instance has been created and is used to initialize its attributes or state.

---

## 58. What is `__new__()`?

### Best Answer

`__new__()` is responsible for creating and returning a new instance. It runs before `__init__()`.

For normal classes, we usually only need `__init__()`.

---

## 59. What is the difference between `__new__()` and `__init__()`?

### Best Answer

`__new__()` creates and returns the instance, while `__init__()` initializes the state of that instance.

The sequence is:

```text
__new__()
   ↓
object created
   ↓
__init__()
   ↓
object initialized
```

---

## 60. What is `__str__()`?

### Best Answer

`__str__()` provides a user-friendly string representation of an object and is used when we call `str()` or commonly when we use `print()`.

---

## 61. What is `__repr__()`?

### Best Answer

`__repr__()` provides a developer-oriented representation of an object, mainly useful for debugging and inspecting objects.

---

## 62. Difference between `__str__()` and `__repr__()`?

### Best Answer

`__str__()` focuses on a readable representation for users, while `__repr__()` focuses on a detailed representation useful for developers and debugging.

---

## 63. What is `__len__()`?

### Best Answer

`__len__()` defines what happens when Python's `len()` function is used on a custom object.

---

## 64. What is `__add__()`?

### Best Answer

`__add__()` defines the behavior of the `+` operator for custom objects.

---

## 65. What is `__eq__()`?

### Best Answer

`__eq__()` defines how two objects are compared using the `==` operator.

---

## 66. What is `__call__()`?

### Best Answer

`__call__()` allows an instance of a class to be called like a function.

For example:

```python
obj()
```

can work if the class implements:

```python
def __call__(self):
    ...
```

---

## 67. What is `__iter__()`?

### Best Answer

`__iter__()` returns an iterator or otherwise defines how an object provides iteration.

It is used by Python's iteration protocol, including `for` loops.

---

## 68. What is `__next__()`?

### Best Answer

`__next__()` returns the next item from an iterator. When there are no more items, it should raise `StopIteration`.

---

## 69. Why does Python use magic methods?

### Best Answer

Magic methods allow user-defined classes to integrate with Python's built-in language features.

For example:

```python
len(obj)
```

can use:

```python
obj.__len__()
```

and:

```python
obj1 + obj2
```

can use:

```python
obj1.__add__(obj2)
```

---

# Interview Coding Questions to Practice

## 70. Write a program using `super()`.

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        super().show()
        print("Child")


Child().show()
```

Expected output:

```text
Parent
Child
```

---

## 71. Write a program to display the MRO.

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass


print(C.mro())
```

---

## 72. Write a class that supports `len()`.

```python
class Collection:
    def __init__(self, items):
        self.items = items

    def __len__(self):
        return len(self.items)


collection = Collection([1, 2, 3])

print(len(collection))
```

---

## 73. Write a class that supports `+`.

```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Number(self.value + other.value)


result = Number(10) + Number(20)

print(result.value)
```

---

## 74. Write a class with a custom string representation.

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name


employee = Employee("Harsha")

print(employee)
```

---

## 75. Write a custom iterator.

```python
class Counter:
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


for value in Counter(3):
    print(value)
```

Output:

```text
1
2
3
```

---

# Quick Revision

## `super()`

```text
super()
   ↓
Proxy for next class in MRO
   ↓
Reuse inherited behavior
```

## MRO

```text
Method Resolution Order
        ↓
Order Python searches classes
        ↓
Important for inheritance
        ↓
Especially multiple inheritance
```

## Magic Methods

```text
__init__()     → initialize object
__new__()      → create object
__str__()      → readable representation
__repr__()     → developer representation
__len__()      → len()
__add__()      → +
__eq__()       → ==
__lt__()       → <
__contains__() → in
__call__()     → object()
__iter__()     → iteration
__next__()     → next item
```

# Most Important Interview Points

```text
1. super() does not simply mean "parent".
   It follows the MRO.

2. MRO determines the order in which Python searches
   classes for methods and attributes.

3. Python uses C3 Linearization to calculate MRO
   for multiple inheritance.

4. __init__() initializes an object.
   __new__() creates and returns an object.

5. Magic methods allow custom objects to work naturally
   with Python's built-in syntax.

6. __str__() is user-friendly.
   __repr__() is developer-oriented.

7. __iter__() and __next__() are part of Python's
   iterator protocol.

8. super() is especially important for cooperative
   multiple inheritance.
```

# Final Interview Checklist

Before an interview, make sure you can explain and code:

- What is `super()`?
- Why use `super()`?
- Does `super()` always call the direct parent?
- `super()` vs direct parent call
- How to call a parent constructor using `super()`
- What is MRO?
- Why is MRO important?
- How to check MRO using `mro()`
- How to check MRO using `__mro__`
- What is `object`?
- MRO in single inheritance
- MRO in multiple inheritance
- What is the diamond problem?
- How does Python solve the diamond problem?
- What is C3 Linearization?
- What are magic methods?
- Why are magic methods useful?
- What is `__init__()`?
- What is `__new__()`?
- Difference between `__new__()` and `__init__()`
- What is `__str__()`?
- What is `__repr__()`?
- Difference between `__str__()` and `__repr__()`
- What is `__len__()`?
- What is `__add__()`?
- What is `__eq__()`?
- What is `__lt__()`?
- What is `__contains__()`?
- What is `__call__()`?
- What is `__iter__()`?
- What is `__next__()`?
- Write a program using `super()`
- Write a program showing MRO
- Write a program demonstrating multiple inheritance
- Write a custom `__str__()`
- Write a custom `__add__()`
- Write a custom `__len__()`
- Write a custom iterator
- Explain how `super()`, MRO, and multiple inheritance are connected