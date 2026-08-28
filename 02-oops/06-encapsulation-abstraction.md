# 06 — Encapsulation and Abstraction

## 1. What is Encapsulation?

### Answer

**Encapsulation is the process of bundling data and the methods that operate on that data inside a class, while controlling how that data can be accessed or modified.**

In simple terms:

```text
Encapsulation
    ↓
Data + Methods
    ↓
Bundled inside a class
    ↓
Controlled access to data
```

For example:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance


account = BankAccount(1000)

account.deposit(500)

print(account.get_balance())
```

Output:

```text
1500
```

Here, `balance` is kept inside the class and modified through controlled methods.

---

## 2. Why is Encapsulation Important?

### Answer

Encapsulation is important because it:

- Protects data from uncontrolled modification
- Controls how data is accessed
- Keeps related data and behavior together
- Makes code easier to maintain
- Prevents accidental changes
- Allows validation before modifying data

For example, instead of allowing anyone to directly change a bank balance:

```python
account.balance = -100000
```

we can provide a method that validates the amount before changing the balance.

---

## 3. What are Access Levels in Python?

Python does not have strict access modifiers like Java or C++.

Instead, Python mainly uses naming conventions:

```text
public
protected
private
```

They are represented using:

```python
name
_name
__name
```

---

## 4. What is a Public Member?

### Answer

A public member can be accessed directly from outside the class.

Example:

```python
class Student:
    def __init__(self):
        self.name = "Harsha"


student = Student()

print(student.name)
```

Output:

```text
Harsha
```

`name` is public.

---

## 5. What is a Protected Member?

### Answer

A single underscore is conventionally used to indicate a **protected member**.

```python
class Student:
    def __init__(self):
        self._marks = 90


student = Student()

print(student._marks)
```

Output:

```text
90
```

Python does **not** strictly prevent access to `_marks`.

The underscore mainly communicates:

> "This is intended for internal use or use by subclasses."

So protected access in Python is largely a **convention**, not strict enforcement.

---

## 6. What is a Private Member?

### Answer

A double underscore is used for private-style members.

```python
class BankAccount:
    def __init__(self):
        self.__balance = 1000


account = BankAccount()

print(account.__balance)
```

This results in an `AttributeError`.

Python internally performs **name mangling** for names beginning with two underscores.

---

## 7. What is Name Mangling?

### Answer

When a variable begins with two underscores, Python changes its internal name to reduce accidental access or overriding.

For example:

```python
class BankAccount:
    def __init__(self):
        self.__balance = 1000
```

Python internally represents it approximately as:

```python
self._BankAccount__balance
```

Therefore:

```python
account = BankAccount()

print(account._BankAccount__balance)
```

can access it.

This is why Python's private members are **not truly private** in the strict sense.

The purpose is mainly to prevent accidental access and name conflicts.

---

## 8. Is `__variable` Completely Private in Python?

### Best Answer

No.

Python does not provide strict private access like some languages.

A variable such as:

```python
__balance
```

uses name mangling.

It can technically be accessed using the mangled name:

```python
account._BankAccount__balance
```

However, this is not recommended because it bypasses the intended interface of the class.

---

## 9. What is Data Hiding?

### Answer

Data hiding means restricting direct access to internal data and exposing controlled ways to interact with it.

Example:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance
```

The user interacts with:

```python
deposit()
get_balance()
```

instead of directly modifying:

```python
__balance
```

---

## 10. Encapsulation vs Data Hiding

### Answer

They are related but not exactly the same.

**Encapsulation** means bundling data and methods together inside a class.

**Data hiding** means restricting or controlling direct access to internal data.

Example:

```text
Encapsulation
→ Data + methods bundled together

Data hiding
→ Internal data access is controlled
```

Encapsulation can be used to achieve data hiding.

---

# Abstraction

## 11. What is Abstraction?

### Answer

**Abstraction means hiding unnecessary implementation details and exposing only the essential functionality to the user.**

For example, when we use:

```python
len(data)
```

we don't need to know how Python internally calculates the length.

We only use the required interface.

```text
Complex implementation
        ↓
      Hidden
        ↓
Simple interface
        ↓
      User
```

---

## 12. Real-World Example of Abstraction

Consider an ATM.

When using an ATM, we perform operations such as:

```text
Insert card
Enter PIN
Withdraw money
```

We do not need to know the internal implementation of:

- Bank server communication
- Account validation
- Transaction processing
- Database updates

The ATM exposes the required operations while hiding the internal complexity.

That is abstraction.

---

## 13. How is Abstraction Implemented in Python?

Python commonly provides abstraction using:

```python
ABC
abstractmethod
```

from the `abc` module.

Example:

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass


class Dog(Animal):

    def sound(self):
        print("Bark")


dog = Dog()

dog.sound()
```

Output:

```text
Bark
```

---

## 14. What is an Abstract Class?

### Answer

An abstract class is a class intended to serve as a base class and define a common interface for its subclasses.

Python provides abstract classes through the `abc` module.

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass
```

`Vehicle` defines what subclasses should provide.

---

## 15. What is an Abstract Method?

### Answer

An abstract method is a method declared in an abstract class that subclasses are expected to implement.

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


class Car(Vehicle):

    def start(self):
        print("Car started")
```

Here:

```python
start()
```

is an abstract method in `Vehicle`.

`Car` provides its implementation.

---

## 16. Can We Create an Object of an Abstract Class?

### Answer

Not if the class still contains unimplemented abstract methods.

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


vehicle = Vehicle()
```

This raises:

```text
TypeError
```

because `Vehicle` has an abstract method that has not been implemented.

---

## 17. Why Do We Use Abstract Classes?

### Answer

Abstract classes are useful when multiple classes should follow the same interface.

For example:

```python
class DataSource(ABC):

    @abstractmethod
    def read(self):
        pass
```

Then:

```python
class S3Source(DataSource):
    def read(self):
        print("Reading from S3")


class DatabaseSource(DataSource):
    def read(self):
        print("Reading from database")
```

Both classes are required to provide:

```python
read()
```

This creates a common contract.

---

## 18. What is an Interface-Like Design in Python?

### Answer

Python does not have a separate `interface` keyword like Java.

We can achieve interface-like designs using abstract base classes.

Example:

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class UPI(Payment):

    def pay(self, amount):
        print("Paid using UPI:", amount)


class Card(Payment):

    def pay(self, amount):
        print("Paid using Card:", amount)
```

Both classes follow the same interface:

```python
pay(amount)
```

but provide different implementations.

---

## 19. Encapsulation vs Abstraction

| Encapsulation | Abstraction |
|---|---|
| Bundles data and methods together | Hides unnecessary implementation details |
| Controls access to data | Exposes essential functionality |
| Focuses on data protection/control | Focuses on complexity hiding |
| Uses classes, naming conventions, properties, methods | Commonly uses ABCs and abstract methods |
| Example: private-style `__balance` | Example: abstract `pay()` method |

### Easy Way to Remember

```text
Encapsulation
→ "How do I protect/control the data?"

Abstraction
→ "What should I expose and what should I hide?"
```

---

## 20. Encapsulation vs Abstraction — Interview Answer

### Best Answer

Encapsulation is about **bundling data and methods together and controlling access to the internal data**, while abstraction is about **hiding implementation complexity and exposing only the essential functionality**.

For example, keeping a bank account balance inside the class and controlling changes through `deposit()` demonstrates encapsulation.

Defining a common `pay()` interface while hiding how each payment method actually performs the payment demonstrates abstraction.

---

## 21. How are Encapsulation and Abstraction Related?

### Answer

Both help us build clean and maintainable software, but they solve different problems.

For example:

```text
Abstraction
    ↓
Defines what the object should do

Encapsulation
    ↓
Controls how its internal state is accessed
```

They are often used together.

---

# Properties and Encapsulation

## 22. What is a Property in Python?

### Answer

A property allows us to access a method like an attribute while still controlling how the value is retrieved or modified.

Python provides:

```python
@property
```

Example:

```python
class Student:
    def __init__(self, marks):
        self._marks = marks

    @property
    def marks(self):
        return self._marks


student = Student(90)

print(student.marks)
```

Output:

```text
90
```

We access:

```python
student.marks
```

instead of:

```python
student.marks()
```

---

## 23. How Can a Property Control Data?

### Example

```python
class Student:
    def __init__(self, marks):
        self._marks = marks

    @property
    def marks(self):
        return self._marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self._marks = value
        else:
            print("Invalid marks")


student = Student(90)

student.marks = 95

print(student.marks)
```

Output:

```text
95
```

If we try:

```python
student.marks = 150
```

the setter can reject the value.

This is a practical example of encapsulation.

---

## 24. Why Use Getters and Setters?

### Answer

Getters and setters allow us to control how data is accessed and modified.

Example:

```python
class Employee:
    def __init__(self, salary):
        self._salary = salary

    def get_salary(self):
        return self._salary

    def set_salary(self, salary):
        if salary >= 0:
            self._salary = salary
```

Instead of directly modifying:

```python
employee._salary = -5000
```

we can validate the value through:

```python
set_salary()
```

In modern Python, `@property` is often a cleaner way to provide this controlled access.

---

# Practical Examples

## 25. Real-World Example — Bank Account Encapsulation

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Invalid withdrawal")

    def get_balance(self):
        return self.__balance


account = BankAccount(5000)

account.deposit(1000)
account.withdraw(2000)

print(account.get_balance())
```

Output:

```text
4000
```

### Why is this encapsulation?

Because the balance is maintained inside the class:

```python
__balance
```

and operations on it are controlled through:

```python
deposit()
withdraw()
get_balance()
```

---

## 26. Real-World Example — Data Engineering Abstraction

Suppose a data pipeline can read data from different sources.

Instead of exposing the internal implementation of each source, we define a common interface:

```python
from abc import ABC, abstractmethod


class DataSource(ABC):

    @abstractmethod
    def read(self):
        pass


class S3Source(DataSource):

    def read(self):
        print("Reading raw data from S3")


class DatabaseSource(DataSource):

    def read(self):
        print("Reading data from database")


class APISource(DataSource):

    def read(self):
        print("Reading data from API")
```

The pipeline only needs to know:

```python
source.read()
```

It does not need to know how each source performs the actual reading.

This demonstrates abstraction.

---

## 27. Encapsulation and Abstraction Together

A real application can use both concepts.

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class UPI(Payment):

    def __init__(self, balance):
        self.__balance = balance

    def pay(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
            print("Payment successful")
        else:
            print("Insufficient balance")
```

Here:

### Abstraction

The `Payment` class defines:

```python
pay()
```

as the common interface.

### Encapsulation

The UPI balance is stored as:

```python
__balance
```

and controlled inside the class.

---

# Coding Questions

## 28. Write a Program Demonstrating Encapsulation

### Solution

```python
class Employee:
    def __init__(self, salary):
        self.__salary = salary

    def get_salary(self):
        return self.__salary

    def set_salary(self, salary):
        if salary >= 0:
            self.__salary = salary
        else:
            print("Salary cannot be negative")


employee = Employee(50000)

employee.set_salary(60000)

print(employee.get_salary())
```

Output:

```text
60000
```

---

## 29. Write a Program Demonstrating Abstraction

### Solution

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


class Car(Vehicle):

    def start(self):
        print("Car started")


class Bike(Vehicle):

    def start(self):
        print("Bike started")


car = Car()
bike = Bike()

car.start()
bike.start()
```

Output:

```text
Car started
Bike started
```

---

## 30. Write a Program Using a Property Setter

### Solution

```python
class Student:
    def __init__(self, marks):
        self._marks = marks

    @property
    def marks(self):
        return self._marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self._marks = value
        else:
            print("Invalid marks")


student = Student(80)

student.marks = 95

print(student.marks)
```

Output:

```text
95
```

---

## 31. Write a Program Showing Name Mangling

### Solution

```python
class Test:
    def __init__(self):
        self.__value = 10


obj = Test()

print(obj._Test__value)
```

Output:

```text
10
```

This demonstrates that Python's double underscore uses name mangling rather than absolute privacy.

---

# Frequently Asked Interview Questions

## 32. What is encapsulation?

### Best Answer

Encapsulation is the process of bundling data and the methods that operate on that data inside a class while controlling how the internal data is accessed or modified.

---

## 33. What is abstraction?

### Best Answer

Abstraction means hiding unnecessary implementation details and exposing only the essential functionality to the user.

---

## 34. What is the difference between encapsulation and abstraction?

### Best Answer

Encapsulation focuses on **bundling and controlling access to data**, whereas abstraction focuses on **hiding implementation complexity and exposing essential functionality**.

---

## 35. Does Python support private variables?

### Best Answer

Python does not provide strict private variables. A variable with two leading underscores uses name mangling.

For example:

```python
self.__balance
```

is internally changed approximately to:

```python
self._ClassName__balance
```

This discourages accidental access but does not provide absolute privacy.

---

## 36. What is the difference between `_variable` and `__variable`?

### Best Answer

A single underscore:

```python
_variable
```

is a convention indicating that the member is intended for internal use.

A double underscore:

```python
__variable
```

triggers name mangling.

Neither provides Java-style strict private access.

---

## 37. What is name mangling?

### Best Answer

Name mangling is Python's mechanism for changing the name of members that start with two underscores.

For example:

```python
__salary
```

inside:

```python
Employee
```

becomes approximately:

```python
_Employee__salary
```

This helps avoid accidental name conflicts, especially in inheritance.

---

## 38. What is an abstract class?

### Best Answer

An abstract class is a class designed to act as a base class and define a common interface for subclasses.

In Python, abstract classes can be created using `ABC` and `abstractmethod` from the `abc` module.

---

## 39. What is an abstract method?

### Best Answer

An abstract method is a method declared in an abstract class that subclasses are expected to implement.

Example:

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass
```

---

## 40. Can we instantiate an abstract class?

### Best Answer

No, not while it contains unimplemented abstract methods.

Trying to instantiate it raises a `TypeError`.

---

## 41. Does Python have interfaces?

### Best Answer

Python does not have a separate `interface` keyword like Java.

However, interface-like designs can be created using abstract base classes with `ABC` and `abstractmethod`.

---

## 42. What is data hiding?

### Best Answer

Data hiding means controlling access to an object's internal data so that it is not directly modified without following the intended interface.

In Python, double-underscore members and controlled methods or properties can be used for this purpose.

---

## 43. What is the purpose of getters and setters?

### Best Answer

Getters and setters provide controlled access to object data.

They allow us to validate or modify values before storing them.

In Python, `@property` and its setter are often preferred because they provide attribute-like access while keeping control logic.

---

## 44. What is `@property`?

### Best Answer

`@property` allows a method to be accessed like an attribute.

It is useful for implementing controlled access to internal data without changing the way users access the attribute.

Example:

```python
class Student:
    def __init__(self, marks):
        self._marks = marks

    @property
    def marks(self):
        return self._marks
```

We can then write:

```python
student.marks
```

instead of:

```python
student.marks()
```

---

## 45. Give a real-world example of encapsulation.

### Best Answer

A bank account is a good example.

The account balance should not be modified randomly from outside the class.

Instead, operations such as:

```python
deposit()
withdraw()
```

can validate the transaction and update the balance.

This keeps the account state controlled.

---

## 46. Give a real-world example of abstraction.

### Best Answer

An ATM is a simple example.

The user can perform operations such as withdrawing money without knowing the internal implementation involving bank servers, databases, authentication, and transaction processing.

The ATM exposes the required operations while hiding the underlying complexity.

---

## 47. How are encapsulation and abstraction used together?

### Best Answer

In a real application, abstraction can define **what an object should do**, while encapsulation controls **how its internal state is accessed and modified**.

For example, a payment system can define an abstract `pay()` method while keeping payment-related internal data protected inside each payment class.

---

## 48. Why is encapsulation useful in software development?

### Best Answer

Encapsulation reduces accidental changes to internal data, allows validation, improves maintainability, and keeps related data and behavior together.

If the implementation changes internally, the external interface can remain the same.

---

## 49. Why is abstraction useful?

### Best Answer

Abstraction reduces complexity for the user of a class or system.

Instead of exposing every implementation detail, we expose only the operations that are necessary.

This makes code easier to understand, use, and maintain.

---

# Interview Trap Questions

## 50. Is `__variable` completely private in Python?

### Correct Answer

No.

It uses name mangling rather than strict privacy.

For example:

```python
self.__value
```

can technically be accessed through:

```python
self._ClassName__value
```

but doing so bypasses the intended interface and is generally discouraged.

---

## 51. Is `_variable` private in Python?

### Correct Answer

Not strictly.

A single leading underscore is mainly a convention indicating that the member is intended for internal use.

---

## 52. Is abstraction the same as hiding data?

### Correct Answer

No.

Abstraction focuses on **hiding unnecessary implementation details**.

Encapsulation focuses on **bundling data and methods and controlling access to internal state**.

---

## 53. Is encapsulation only about using `__private` variables?

### Correct Answer

No.

Encapsulation is broader than private variables.

It involves bundling data and behavior together and controlling how the object's internal state is accessed or modified.

We can use:

```python
methods
@property
setters
validation
```

and naming conventions to implement encapsulation.

---

## 54. Is abstraction only possible using abstract classes?

### Correct Answer

No.

Abstract classes are one formal mechanism for abstraction in Python.

Abstraction can also be achieved through functions, classes, APIs, modules, and well-designed interfaces that hide unnecessary implementation details.

---

# Quick Revision

## Encapsulation

```text
Data + Methods
      ↓
    Class
      ↓
Controlled access
```

Common Python mechanisms:

```python
_name
__name
@property
getters
setters
validation
```

## Abstraction

```text
Complex implementation
        ↓
       Hide
        ↓
Essential interface
        ↓
       User
```

Common Python mechanism:

```python
from abc import ABC, abstractmethod
```

## Access Naming

```text
name
→ Public convention

_name
→ Protected-style convention

__name
→ Name mangling
```

## Most Important Differences

```text
Encapsulation
→ Protect/control internal state

Abstraction
→ Hide unnecessary implementation details
```

## Interview One-Liner

> **Encapsulation is about controlling access to data, while abstraction is about hiding implementation complexity and exposing only what is necessary.**

# Final Interview Checklist

Before an interview, make sure you can confidently explain:

- What is encapsulation?
- Why is encapsulation important?
- What is data hiding?
- What is a public member?
- What is a protected member?
- What is a private-style member in Python?
- What is name mangling?
- Is `__variable` truly private?
- Difference between `_variable` and `__variable`
- What are getters and setters?
- What is `@property`?
- What is abstraction?
- Why is abstraction important?
- What is an abstract class?
- What is an abstract method?
- What is `ABC`?
- What is `abstractmethod`?
- Can an abstract class be instantiated?
- Does Python have interfaces?
- How can Python implement interface-like behavior?
- Difference between encapsulation and abstraction
- Difference between data hiding and encapsulation
- Give a real-world example of encapsulation
- Give a real-world example of abstraction
- Write an encapsulation program
- Write an abstraction program
- Write a program using `@property`
- Explain encapsulation and abstraction using a data-engineering example