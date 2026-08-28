# 05 — Polymorphism

## 1. What is Polymorphism?

### Answer

**Polymorphism means "many forms".**

In OOP, polymorphism means that the **same method or interface can behave differently depending on the object using it**.

A simple example is:

```python
class Dog:
    def sound(self):
        print("Bark")


class Cat:
    def sound(self):
        print("Meow")


dog = Dog()
cat = Cat()

dog.sound()
cat.sound()
```

Output:

```text
Bark
Meow
```

Both objects use the same method:

```python
sound()
```

but the behavior is different.

---

## 2. Why is Polymorphism Important?

### Answer

Polymorphism allows us to write code that works with different types of objects without writing separate logic for every class.

### Example

```python
class Dog:
    def sound(self):
        print("Bark")


class Cat:
    def sound(self):
        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()
```

Output:

```text
Bark
Meow
```

The loop does not need to know whether the object is a `Dog` or a `Cat`.

It simply expects the object to provide:

```python
sound()
```

This makes code more flexible and maintainable.

---

## 3. Common Forms of Polymorphism in Python

Important forms to know for interviews:

1. Method overriding
2. Duck typing
3. Operator overloading
4. Polymorphism through common interfaces
5. Function/method behavior with different object types

Python does **not** support traditional compile-time method overloading in the same way as Java or C++.

---

## 4. What is Method Overriding?

### Answer

Method overriding occurs when a child class provides its own implementation of a method that already exists in the parent class.

### Example

```python
class Animal:
    def sound(self):
        print("Animal sound")


class Dog(Animal):
    def sound(self):
        print("Bark")


class Cat(Animal):
    def sound(self):
        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()
```

Output:

```text
Bark
Meow
```

Here, `Dog` and `Cat` override the `sound()` method inherited from `Animal`.

This is a common example of **runtime polymorphism**.

---

## 5. What is Runtime Polymorphism?

### Answer

Runtime polymorphism occurs when the method that executes depends on the actual object available at runtime.

### Example

```python
class Animal:
    def sound(self):
        print("Animal sound")


class Dog(Animal):
    def sound(self):
        print("Bark")


class Cat(Animal):
    def sound(self):
        print("Meow")


def make_sound(animal):
    animal.sound()


make_sound(Dog())
make_sound(Cat())
```

Output:

```text
Bark
Meow
```

The same function:

```python
make_sound()
```

works with different objects.

---

## 6. What is Duck Typing?

### Answer

**Duck typing** is a Python concept based on the idea:

> If an object behaves like the required type, we can use it without caring about its exact class.

Python focuses on **what an object can do** rather than strictly checking what class it belongs to.

### Example

```python
class Dog:
    def speak(self):
        print("Bark")


class Person:
    def speak(self):
        print("Hello")


def make_speak(obj):
    obj.speak()


make_speak(Dog())
make_speak(Person())
```

Output:

```text
Bark
Hello
```

`make_speak()` does not require the object to inherit from a particular class.

It only needs the object to provide:

```python
speak()
```

---

## 7. Why is Duck Typing Important in Python?

### Answer

Duck typing makes Python code flexible.

Instead of writing:

```python
if isinstance(obj, Dog):
    ...
elif isinstance(obj, Cat):
    ...
```

we can often simply call the required method:

```python
obj.speak()
```

If the object supports that operation, the code works.

This fits Python's dynamic nature.

---

## 8. What is Operator Overloading?

### Answer

**Operator overloading** allows operators such as:

```text
+
-
*
==
<
>
```

to behave differently for user-defined objects.

Python implements this using **special methods**, also called **dunder methods**.

For example:

```python
__add__()
```

controls the behavior of `+`.

---

## 9. Example of Operator Overloading

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

Here:

```python
num1 + num2
```

internally invokes the addition behavior defined by:

```python
__add__()
```

---

## 10. What are Dunder Methods?

### Answer

Dunder methods are special methods whose names start and end with double underscores.

Examples:

```python
__init__()
__str__()
__add__()
__len__()
__eq__()
```

They allow Python objects to interact with built-in language features and operators.

---

## 11. What is `__str__()`?

### Answer

`__str__()` defines the user-friendly string representation of an object.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name


student = Student("Harsha")

print(student)
```

Output:

```text
Harsha
```

Without defining `__str__()`, printing an object normally gives a default object representation.

---

## 12. What is `__len__()`?

### Answer

`__len__()` allows an object to work with Python's built-in `len()` function.

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

## 13. What is `__eq__()`?

### Answer

`__eq__()` defines how equality comparison using `==` works for objects.

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

## 14. How is Operator Overloading Related to Polymorphism?

### Answer

The same operator can behave differently depending on the objects involved.

For example:

```python
print(10 + 20)
```

Output:

```text
30
```

But:

```python
print("Hello " + "World")
```

Output:

```text
Hello World
```

The same `+` operator has different behavior depending on the operands.

For custom classes, we can define its behavior using methods such as:

```python
__add__()
```

This demonstrates polymorphic behavior.

---

## 15. What is Function Polymorphism?

### Answer

A function can operate on different types of objects as long as those objects support the required operation.

### Example

```python
def display(value):
    print(value)


display(10)
display("Hello")
display([1, 2, 3])
```

Output:

```text
10
Hello
[1, 2, 3]
```

The same function works with different types.

---

## 16. What is Method Overloading?

### Answer

Traditional method overloading means defining multiple methods with the same name but different parameter lists.

Python does **not** support traditional method overloading in the same way as Java or C++.

For example:

```python
class Calculator:
    def add(self, a):
        return a

    def add(self, a, b):
        return a + b
```

The second `add()` definition replaces the first one.

Therefore:

```python
calculator = Calculator()
calculator.add(10)
```

would fail because the final definition expects two arguments.

---

## 17. How Can We Achieve Overloading-Like Behavior in Python?

### Answer

Python commonly uses:

- Default arguments
- `*args`
- `**kwargs`

### Example Using Default Arguments

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c


calculator = Calculator()

print(calculator.add(10))
print(calculator.add(10, 20))
print(calculator.add(10, 20, 30))
```

Output:

```text
10
30
60
```

This provides overloading-like behavior.

---

## 18. Method Overriding vs Method Overloading

| Feature | Method Overriding | Method Overloading |
|---|---|---|
| Meaning | Child changes parent method behavior | Same method name with different parameter lists |
| Inheritance | Usually requires inheritance | Does not necessarily require inheritance |
| Python support | Yes | No traditional support |
| Common Python approach | Redefine method in child | Default arguments, `*args`, `**kwargs` |

### Easy Way to Remember

```text
Overriding
Parent → Child
Same method → New implementation


Overloading
Same method name
Different arguments
Traditional form not directly supported in Python
```

---

## 19. What is Polymorphism Through a Common Interface?

### Answer

Different classes can provide the same method name and interface while implementing different behavior.

### Example

```python
class CSVProcessor:
    def process(self):
        print("Processing CSV")


class JSONProcessor:
    def process(self):
        print("Processing JSON")


class DatabaseProcessor:
    def process(self):
        print("Processing database data")


processors = [
    CSVProcessor(),
    JSONProcessor(),
    DatabaseProcessor()
]

for processor in processors:
    processor.process()
```

Output:

```text
Processing CSV
Processing JSON
Processing database data
```

The calling code does not need to know the internal implementation of each processor.

---

## 20. Real-World Example — Payment System

Suppose an application supports multiple payment methods.

```python
class CreditCard:
    def pay(self, amount):
        print("Paid", amount, "using credit card")


class UPI:
    def pay(self, amount):
        print("Paid", amount, "using UPI")


class NetBanking:
    def pay(self, amount):
        print("Paid", amount, "using net banking")


def process_payment(payment_method, amount):
    payment_method.pay(amount)


process_payment(CreditCard(), 1000)
process_payment(UPI(), 500)
process_payment(NetBanking(), 2000)
```

Output:

```text
Paid 1000 using credit card
Paid 500 using UPI
Paid 2000 using net banking
```

The function:

```python
process_payment()
```

works with different payment objects.

Each payment class implements the same operation:

```python
pay()
```

but performs it differently.

---

## 21. Real-World Example — Data Engineering

Polymorphism can be useful when different data sources expose a common operation.

```python
class S3Source:
    def read(self):
        print("Reading data from S3")


class DatabaseSource:
    def read(self):
        print("Reading data from database")


class APIDataSource:
    def read(self):
        print("Reading data from API")


def load_data(source):
    source.read()


sources = [
    S3Source(),
    DatabaseSource(),
    APIDataSource()
]

for source in sources:
    load_data(source)
```

Output:

```text
Reading data from S3
Reading data from database
Reading data from API
```

The `load_data()` function only expects the object to provide a `read()` method.

This is a good example of Python's duck typing.

---

## 22. Inheritance-Based Polymorphism

Polymorphism can be combined with inheritance.

```python
class DataSource:
    def read(self):
        print("Reading data")


class S3Source(DataSource):
    def read(self):
        print("Reading from S3")


class DatabaseSource(DataSource):
    def read(self):
        print("Reading from database")


sources = [S3Source(), DatabaseSource()]

for source in sources:
    source.read()
```

Output:

```text
Reading from S3
Reading from database
```

Here:

- `DataSource` provides the common interface.
- Child classes override `read()`.
- The same `read()` call produces different behavior.

---

## 23. Polymorphism vs Inheritance

### Inheritance

Inheritance allows one class to acquire functionality from another class.

```text
Parent
  ↓
Child
```

### Polymorphism

Polymorphism allows the same interface or operation to produce different behavior depending on the object.

```text
same method
    ↓
different objects
    ↓
different behavior
```

They are related but are **not the same concept**.

---

## 24. Polymorphism vs Encapsulation

### Encapsulation

Focuses on:

```text
How data is bundled and controlled
```

### Polymorphism

Focuses on:

```text
How the same interface can have different behavior
```

For example:

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0
```

The private balance demonstrates encapsulation.

Different payment classes implementing:

```python
pay()
```

demonstrate polymorphism.

---

## 25. Polymorphism vs Abstraction

### Abstraction

Abstraction focuses on exposing essential functionality while hiding implementation details.

### Polymorphism

Polymorphism allows different implementations to be used through a common interface.

A common design can use both:

```text
Abstraction
    ↓
Define common interface
    ↓
Polymorphism
    ↓
Different classes implement that interface differently
```

---

## 26. What is Structural Typing in Simple Terms?

### Answer

Structural typing focuses on what an object can do rather than what class it belongs to.

Duck typing is the common Python approach.

### Example

```python
class Dog:
    def run(self):
        print("Dog running")


class Robot:
    def run(self):
        print("Robot running")


def start(obj):
    obj.run()


start(Dog())
start(Robot())
```

Output:

```text
Dog running
Robot running
```

The function does not care whether the object is a `Dog` or `Robot`.

It only needs:

```python
run()
```

---

## 27. What Happens If an Object Does Not Have the Required Method?

### Answer

With duck typing, Python generally discovers the problem when the operation is attempted.

### Example

```python
class Dog:
    def speak(self):
        print("Bark")


class Car:
    pass


def make_speak(obj):
    obj.speak()


make_speak(Dog())
make_speak(Car())
```

The second call raises:

```text
AttributeError
```

because `Car` does not provide the `speak()` method.

This demonstrates why the object must support the expected interface.

---

## 28. How Does Python's Dynamic Typing Help Polymorphism?

### Answer

Python variables are not restricted to one declared type.

The same function can receive objects of different classes.

```python
def display(obj):
    obj.show()
```

Any object that provides:

```python
show()
```

can potentially be passed to the function.

This flexibility is one reason polymorphism and duck typing are common in Python.

---

## 29. Coding Question — Basic Polymorphism

### Question

Create two classes, `Dog` and `Cat`, with the same method `sound()` but different implementations.

### Solution

```python
class Dog:
    def sound(self):
        print("Bark")


class Cat:
    def sound(self):
        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()
```

Output:

```text
Bark
Meow
```

---

## 30. Coding Question — Polymorphism Using Inheritance

### Solution

```python
class Animal:
    def sound(self):
        print("Animal sound")


class Dog(Animal):
    def sound(self):
        print("Bark")


class Cat(Animal):
    def sound(self):
        print("Meow")


def make_sound(animal):
    animal.sound()


make_sound(Dog())
make_sound(Cat())
```

Output:

```text
Bark
Meow
```

---

## 31. Coding Question — Duck Typing

### Solution

```python
class Dog:
    def speak(self):
        print("Bark")


class Person:
    def speak(self):
        print("Hello")


def speak(obj):
    obj.speak()


speak(Dog())
speak(Person())
```

Output:

```text
Bark
Hello
```

No common parent class is required.

---

## 32. Coding Question — Operator Overloading

### Solution

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

## 33. Coding Question — `__str__()`

### Solution

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Employee: {self.name}"


employee = Employee("Harsha")

print(employee)
```

Output:

```text
Employee: Harsha
```

---

## 34. Coding Question — `__len__()`

### Solution

```python
class Team:
    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)


team = Team(["A", "B", "C", "D"])

print(len(team))
```

Output:

```text
4
```

---

## 35. Coding Question — Common Interface

### Question

Create multiple data-source classes that provide a common `read()` method.

### Solution

```python
class S3Source:
    def read(self):
        print("Reading from S3")


class DatabaseSource:
    def read(self):
        print("Reading from database")


class APISource:
    def read(self):
        print("Reading from API")


def read_data(source):
    source.read()


sources = [
    S3Source(),
    DatabaseSource(),
    APISource()
]

for source in sources:
    read_data(source)
```

Output:

```text
Reading from S3
Reading from database
Reading from API
```

---

# Interview Questions and Best Answers

## 36. Explain Polymorphism.

### Best Answer

Polymorphism means **many forms**. In OOP, it allows the same interface or method call to behave differently depending on the object.

For example, `Dog` and `Cat` can both implement a `sound()` method, but `Dog.sound()` produces `"Bark"` while `Cat.sound()` produces `"Meow"`.

In Python, polymorphism commonly appears through method overriding, duck typing, and operator overloading.

---

## 37. What is Duck Typing?

### Best Answer

Duck typing is Python's approach where we care about whether an object supports the required operation rather than checking its exact class.

For example, if two unrelated classes both provide a `read()` method, a function can call `source.read()` on either object.

This makes Python code flexible.

---

## 38. Does Python Support Method Overloading?

### Best Answer

Python does not support traditional method overloading based on different parameter lists.

If the same method is defined multiple times in a class, the latest definition replaces the previous one.

However, we can achieve similar behavior using default arguments, `*args`, and `**kwargs`.

---

## 39. What is Method Overriding?

### Best Answer

Method overriding occurs when a child class provides its own implementation of a method inherited from its parent.

It is commonly used to achieve runtime polymorphism.

```python
class Animal:
    def sound(self):
        print("Animal")


class Dog(Animal):
    def sound(self):
        print("Bark")
```

---

## 40. What is Operator Overloading?

### Best Answer

Operator overloading allows us to define how operators behave for user-defined objects.

Python uses special methods such as:

```python
__add__()
__eq__()
__lt__()
```

For example, implementing `__add__()` allows custom objects to work with the `+` operator.

---

## 41. Give a Real-World Example of Polymorphism.

### Best Answer

A payment system is a simple example.

Different classes such as `CreditCard`, `UPI`, and `NetBanking` can all provide a `pay()` method.

The payment-processing function can call `pay()` without knowing the exact payment type.

Each class performs the payment differently, but they share the same interface.

---

## 42. How is Polymorphism Used in Data Engineering?

### Best Answer

Suppose a pipeline can read data from S3, a database, or an API.

I can define a common operation such as `read()` for each source.

The pipeline can then call:

```python
source.read()
```

without needing separate logic for every source type.

This makes it easier to add another data source later without changing the main processing logic.

---

## 43. What is the Difference Between Overloading and Overriding?

### Best Answer

**Overloading** means using the same method name with different parameter combinations. Python does not support traditional method overloading directly.

**Overriding** means a child class provides a different implementation of a method inherited from its parent, and Python supports this.

---

## 44. Is Duck Typing the Same as Polymorphism?

### Best Answer

Duck typing is one way Python enables polymorphic behavior.

With duck typing, an object does not have to belong to a specific inheritance hierarchy.

If it supports the required method or behavior, it can be used.

```text
Polymorphism
    ↓
Broader OOP concept

Duck typing
    ↓
One Python approach for flexible polymorphic behavior
```

---

## 45. Does the Same Method Name Automatically Mean Inheritance?

### Answer

No.

Consider:

```python
class Dog:
    def speak(self):
        print("Bark")


class Person:
    def speak(self):
        print("Hello")
```

`Dog` and `Person` do not inherit from each other.

Still, this can demonstrate polymorphic behavior through duck typing:

```python
def speak(obj):
    obj.speak()


speak(Dog())
speak(Person())
```

---

## 46. Why Can `+` Have Different Behavior in Python?

### Answer

The `+` operator can behave differently depending on the operands.

For example:

```python
10 + 20
```

performs numerical addition.

```python
"Hello " + "World"
```

performs string concatenation.

For custom classes, we can define the behavior using:

```python
__add__()
```

This is an example of operator overloading.

---

# Important Interview Traps

## Trap 1 — Python Method Overloading

Do not say:

> "Python directly supports traditional method overloading."

A better answer is:

> "Python does not support traditional method overloading based on different parameter lists. If the same method is defined multiple times, the latest definition replaces the previous one. We can achieve similar behavior using default arguments, `*args`, or `**kwargs`."

---

## Trap 2 — Duck Typing Does Not Require Inheritance

Two classes can be completely unrelated and still work with the same function if they provide the required method.

```python
class A:
    def show(self):
        print("A")


class B:
    def show(self):
        print("B")


def display(obj):
    obj.show()


display(A())
display(B())
```

Output:

```text
A
B
```

---

## Trap 3 — Polymorphism and Inheritance Are Not the Same

Inheritance describes a relationship between classes.

Polymorphism describes the ability to use a common interface or operation with different objects and obtain different behavior.

Inheritance can be used to achieve polymorphism, but polymorphism can also be achieved through duck typing without inheritance.

---

# Quick Revision

```text
Polymorphism
    ↓
Many forms
    ↓
Same interface / operation
    ↓
Different behavior
```

## Method Overriding

```text
Parent method
      ↓
Child provides new implementation
```

## Duck Typing

```text
Don't focus on exact type
        ↓
Focus on required behavior
```

## Operator Overloading

```text
Operator
   ↓
Special method
   ↓
Custom object behavior
```

Important examples:

```text
+    → __add__()
==   → __eq__()
<    → __lt__()
len  → __len__()
str  → __str__()
```

## Overloading vs Overriding

```text
Overloading
→ Same method name
→ Different arguments
→ Traditional form not directly supported in Python


Overriding
→ Parent-child relationship
→ Child changes inherited method behavior
→ Supported in Python
```

# Frequently Asked Interview Questions

1. What is polymorphism?
2. Why is polymorphism important?
3. What are the common forms of polymorphism in Python?
4. What is method overriding?
5. What is runtime polymorphism?
6. What is duck typing?
7. Why is duck typing important in Python?
8. What is operator overloading?
9. What are dunder methods?
10. What is `__str__()`?
11. What is `__len__()`?
12. What is `__eq__()`?
13. How is operator overloading related to polymorphism?
14. What is function polymorphism?
15. What is method overloading?
16. Does Python support traditional method overloading?
17. How can overloading-like behavior be achieved in Python?
18. What is the difference between method overloading and overriding?
19. What is polymorphism through a common interface?
20. Give a real-world example of polymorphism.
21. How can polymorphism be used in data engineering?
22. What is inheritance-based polymorphism?
23. What is the difference between inheritance and polymorphism?
24. What is the difference between polymorphism and encapsulation?
25. What is the difference between polymorphism and abstraction?
26. What is structural typing?
27. What happens if an object does not have the required method?
28. How does dynamic typing help polymorphism?
29. Write a program demonstrating polymorphism.
30. Write a program demonstrating method overriding.
31. Write a program demonstrating duck typing.
32. Write a program demonstrating operator overloading.
33. Write a program using `__str__()`.
34. Write a program using `__len__()`.
35. Create multiple classes with a common interface.
36. Explain polymorphism using a payment system.
37. Explain polymorphism using a data-engineering example.
38. Is duck typing the same as polymorphism?
39. Does the same method name automatically mean inheritance?
40. Explain why `+` can have different behavior in Python.