# 08 — OOP Important Interview Questions

# Python OOP — Important Interview Questions

This file is the **main revision file for Python OOP interviews**.

The goal is not to memorize every possible OOP question. Focus strongly on the questions below because they cover the core concepts, common follow-up questions, and basic coding questions that can come from Python OOP.

---

## 1. What is OOP?

### Answer

OOP stands for **Object-Oriented Programming**.

It is a programming approach where we organize code around **objects and classes**.

An object contains:

- Data → attributes
- Behavior → methods

Python supports OOP and allows us to create reusable and maintainable code using concepts such as:

- Class
- Object
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

### Simple Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def study(self):
        print(self.name, "is studying")


student = Student("Harsha")

print(student.name)
student.study()
```

Output:

```text
Harsha
Harsha is studying
```

### Interview Tip

A strong answer is:

> OOP is a programming paradigm where we model a problem using classes and objects. It helps organize data and behavior together and provides features such as encapsulation, inheritance, polymorphism, and abstraction.

---

# 2. What is a Class?

### Answer

A class is a **blueprint or template** used to create objects.

It defines the attributes and methods that objects created from the class can have.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self):
        print("Student is studying")
```

Here:

```text
Student
   ↓
Class
   ↓
Blueprint for creating Student objects
```

---

# 3. What is an Object?

### Answer

An object is an **instance of a class**.

The class defines the structure and behavior, while the object represents an actual instance of that class.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name


student1 = Student("Harsha")
student2 = Student("Rahul")
```

Here:

```text
Student → Class

student1 → Object
student2 → Object
```

Both objects belong to the same class but can contain different data.

---

# 4. Class vs Object

| Class | Object |
|---|---|
| Blueprint/template | Instance of a class |
| Defines structure | Contains actual data |
| Does not represent one specific instance | Represents a specific instance |
| Used to create objects | Created from a class |

### Example

```python
class Car:
    pass


car1 = Car()
car2 = Car()
```

Here:

```text
Car  → Class
car1 → Object
car2 → Object
```

---

# 5. What are the Four Main Pillars of OOP?

### Answer

The four commonly discussed pillars of OOP are:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

### Quick Revision

```text
Encapsulation
    ↓
Bundle data and methods + control access

Inheritance
    ↓
Reuse/extend functionality from another class

Polymorphism
    ↓
Same interface/operation, different behavior

Abstraction
    ↓
Expose essential behavior while hiding implementation details
```

---

# 6. What is Encapsulation?

### Answer

Encapsulation means bundling data and the methods that operate on that data inside a class, while controlling how the internal state is accessed or modified.

Python does not enforce private fields in the same way as some languages, but it provides conventions and mechanisms such as:

```python
_public
__private
```

### Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def deposit(self, amount):
        self.__balance += amount


account = BankAccount(1000)

account.deposit(500)

print(account.get_balance())
```

Output:

```text
1500
```

The balance is kept internally and modified through methods.

---

# 7. What is Inheritance?

### Answer

Inheritance allows a child class to reuse and extend functionality from a parent class.

### Example

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


dog = Dog()

dog.eat()
dog.bark()
```

Output:

```text
Animal is eating
Dog is barking
```

`Dog` inherits `eat()` from `Animal`.

---

# 8. Why is Inheritance Used?

### Answer

Inheritance is mainly used for:

- Code reuse
- Extending existing functionality
- Creating hierarchical relationships
- Supporting polymorphism
- Avoiding unnecessary duplication

However, inheritance should be used when there is a genuine **is-a relationship**.

For example:

```text
Dog is an Animal
Car is a Vehicle
Manager is an Employee
```

---

# 9. What is Polymorphism?

### Answer

Polymorphism means that the same interface or operation can work with different object types and produce behavior appropriate to those objects.

### Example

```python
class Dog:
    def speak(self):
        print("Bark")


class Cat:
    def speak(self):
        print("Meow")


def make_sound(animal):
    animal.speak()


make_sound(Dog())
make_sound(Cat())
```

Output:

```text
Bark
Meow
```

The function:

```python
make_sound()
```

works with different objects as long as they provide the required `speak()` behavior.

---

# 10. What is Abstraction?

### Answer

Abstraction means exposing the essential interface while hiding unnecessary implementation details.

Python supports abstraction using the `abc` module and abstract base classes.

### Example

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


class Car(Vehicle):
    def start(self):
        print("Car starts")


car = Car()

car.start()
```

Output:

```text
Car starts
```

The `Vehicle` class defines what a vehicle must provide, while `Car` defines how it works.

---

# 11. Encapsulation vs Abstraction

| Encapsulation | Abstraction |
|---|---|
| Bundles data and methods | Hides implementation complexity |
| Controls access to internal state | Focuses on essential interface |
| Concerned with data protection/access | Concerned with what should be exposed |
| Can use naming conventions, properties, etc. | Can use abstract classes/interfaces |

### Interview Answer

> Encapsulation focuses on bundling data and behavior together and controlling access to internal state, while abstraction focuses on exposing only the essential interface and hiding implementation details.

---

# 12. Inheritance vs Composition

### Inheritance

Represents an **is-a** relationship.

```text
Dog is an Animal
```

### Composition

Represents a **has-a** relationship.

```text
Car has an Engine
```

### Example

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()


car = Car()

car.start()
```

Here:

```text
Car HAS-A Engine
```

This is composition.

---

# 13. Why is Composition Often Preferred Over Deep Inheritance?

### Answer

Composition can make code more flexible because objects can be combined without creating a large inheritance hierarchy.

For example:

```python
class Engine:
    pass


class Car:
    def __init__(self):
        self.engine = Engine()
```

Instead of creating many levels of inheritance, functionality can be composed from smaller objects.

### Interview Answer

> I prefer composition when the relationship is naturally "has-a" or when I want flexibility without creating a deep inheritance hierarchy. Inheritance is useful when there is a genuine "is-a" relationship.

---

# 14. What is `self`?

### Answer

`self` refers to the **current instance** of a class.

It allows us to access instance attributes and methods.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)


student = Student("Harsha")

student.show()
```

Here:

```python
self.name
```

refers to the `name` belonging to the current object.

---

# 15. Is `self` a Keyword in Python?

### Answer

No.

`self` is a naming convention for the first parameter of an instance method.

Python does not require the name to literally be `self`, although using `self` is the standard and recommended practice.

Example:

```python
class Student:
    def show(current_object):
        print(current_object)
```

This can work, but we should normally use:

```python
def show(self):
```

because it is the standard convention.

---

# 16. What is `__init__()`?

### Answer

`__init__()` is an initializer method that is called after an instance has been created.

It is commonly used to initialize instance attributes.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student = Student("Harsha", 22)
```

The constructor call supplies the values used to initialize the object.

---

# 17. Is `__init__()` Actually a Constructor?

### Interview-Safe Answer

In everyday Python discussions, `__init__()` is often called the constructor.

More precisely:

- `__new__()` creates and returns the instance.
- `__init__()` initializes the already-created instance.

### Example

```python
class Student:
    def __new__(cls):
        print("Creating object")
        return super().__new__(cls)

    def __init__(self):
        print("Initializing object")


student = Student()
```

Output:

```text
Creating object
Initializing object
```

For normal application development, `__init__()` is the method you usually work with.

---

# 18. What is `__new__()`?

### Answer

`__new__()` is responsible for creating and returning a new instance.

It receives `cls` rather than `self`.

It runs before `__init__()`.

```text
__new__()
   ↓
Object created
   ↓
__init__()
   ↓
Object initialized
```

It is mainly useful for advanced object creation scenarios.

---

# 19. What is the Difference Between Instance, Class, and Static Methods?

### Instance Method

Works with an instance and normally receives:

```python
self
```

### Class Method

Works with the class and receives:

```python
cls
```

It is defined using:

```python
@classmethod
```

### Static Method

Does not automatically receive `self` or `cls`.

It is defined using:

```python
@staticmethod
```

### Example

```python
class Student:

    def instance_method(self):
        print("Instance method")

    @classmethod
    def class_method(cls):
        print("Class method")

    @staticmethod
    def static_method():
        print("Static method")
```

---

# 20. What is an Instance Method?

### Answer

An instance method operates on a particular object and receives the object as the first parameter, conventionally named `self`.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)


student = Student("Harsha")

student.show()
```

---

# 21. What is a Class Method?

### Answer

A class method receives the class as its first argument, conventionally called `cls`.

It is created using:

```python
@classmethod
```

### Example

```python
class Student:
    school = "ABC School"

    @classmethod
    def show_school(cls):
        print(cls.school)


Student.show_school()
```

Output:

```text
ABC School
```

Class methods are useful when the operation needs to work with class-level state or when providing alternative constructors.

---

# 22. What is a Static Method?

### Answer

A static method is a method that belongs logically to a class but does not automatically receive the instance or class as an argument.

It is defined using:

```python
@staticmethod
```

### Example

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


print(Calculator.add(10, 20))
```

Output:

```text
30
```

---

# 23. Instance Method vs Class Method vs Static Method

| Type | First automatic argument | Used for |
|---|---|---|
| Instance method | `self` | Instance-specific behavior |
| Class method | `cls` | Class-level behavior |
| Static method | None | Utility behavior logically related to class |

### Quick Example

```python
class Example:

    def instance_method(self):
        pass

    @classmethod
    def class_method(cls):
        pass

    @staticmethod
    def static_method():
        pass
```

---

# 24. What is a Class Variable?

### Answer

A class variable is associated with the class and is shared by instances unless an instance creates its own attribute with the same name.

### Example

```python
class Student:
    school = "ABC School"

    def __init__(self, name):
        self.name = name


student1 = Student("A")
student2 = Student("B")

print(student1.school)
print(student2.school)
```

Output:

```text
ABC School
ABC School
```

---

# 25. What is an Instance Variable?

### Answer

An instance variable belongs to a particular object.

It is usually created using:

```python
self.attribute
```

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name


student1 = Student("A")
student2 = Student("B")
```

Here:

```python
student1.name
student2.name
```

are separate instance attributes.

---

# 26. Class Variable vs Instance Variable

| Class Variable | Instance Variable |
|---|---|
| Associated with class | Associated with individual object |
| Shared unless shadowed | Separate for each object |
| Accessed through class or instance | Usually accessed through instance |
| Example: company name | Example: employee name |

### Example

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name
```

Here:

```python
company
```

is a class variable.

```python
self.name
```

is an instance variable.

---

# 27. What is Method Overriding?

### Answer

Method overriding occurs when a child class provides its own implementation of a method already defined in the parent class.

### Example

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    def speak(self):
        print("Bark")


dog = Dog()

dog.speak()
```

Output:

```text
Bark
```

The child implementation overrides the inherited implementation.

---

# 28. Does Python Support Method Overloading?

### Answer

Python does not support traditional compile-time method overloading like Java or C++.

If we define multiple methods with the same name in a class, the later definition replaces the earlier one.

However, similar behavior can be achieved using:

- Default arguments
- `*args`
- `**kwargs`
- Type checking
- Other design techniques

### Example

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

---

# 29. Method Overloading vs Method Overriding

| Overloading | Overriding |
|---|---|
| Same method name with different parameter patterns | Child replaces inherited method implementation |
| Traditional compile-time overloading is not directly supported in Python | Supported |
| Can simulate with defaults/`*args`/`**kwargs` | Common in inheritance |
| Usually within a class | Requires inheritance |

---

# 30. What is Duck Typing?

### Answer

Duck typing means Python often focuses on whether an object supports the required behavior rather than its exact class.

The common idea is:

> If an object behaves like the required type, it can be used.

### Example

```python
class Dog:
    def speak(self):
        print("Bark")


class Cat:
    def speak(self):
        print("Meow")


def make_sound(animal):
    animal.speak()


make_sound(Dog())
make_sound(Cat())
```

The function does not need to check whether the object is specifically a `Dog` or `Cat`.

It only requires the object to provide:

```python
speak()
```

---

# 31. What is Python's Approach to Polymorphism?

### Answer

Python supports polymorphism through several mechanisms, including:

- Method overriding
- Duck typing
- Operator overloading
- Common interfaces/protocols
- Abstract base classes

Python's dynamic nature allows different object types to be used through the same expected interface.

---

# 32. What is Operator Overloading?

### Answer

Operator overloading allows us to define how operators behave for custom objects.

Python uses special methods for this.

Examples:

```text
+  → __add__()
-  → __sub__()
*  → __mul__()
== → __eq__()
<  → __lt__()
```

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

# 33. What are Magic Methods?

### Answer

Magic methods, also called dunder methods, are special methods whose names generally begin and end with double underscores.

Examples:

```python
__init__()
__str__()
__repr__()
__len__()
__add__()
__eq__()
__iter__()
__next__()
```

They allow user-defined objects to integrate with Python's built-in operations and syntax.

---

# 34. Important Magic Methods

| Method | Purpose |
|---|---|
| `__init__()` | Initialize object |
| `__new__()` | Create object |
| `__str__()` | User-friendly representation |
| `__repr__()` | Developer-oriented representation |
| `__len__()` | Behavior of `len()` |
| `__add__()` | Behavior of `+` |
| `__eq__()` | Behavior of `==` |
| `__lt__()` | Behavior of `<` |
| `__contains__()` | Behavior of `in` |
| `__call__()` | Make object callable |
| `__iter__()` | Return iterator |
| `__next__()` | Return next iterator item |

---

# 35. What is `__str__()`?

### Answer

`__str__()` provides a readable string representation of an object.

### Example

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

# 36. What is `__repr__()`?

### Answer

`__repr__()` provides a developer-oriented representation of an object.

It is useful when inspecting objects and debugging.

### Example

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Employee({self.name!r})"


employee = Employee("Harsha")

print(repr(employee))
```

Output:

```text
Employee('Harsha')
```

---

# 37. Difference Between `__str__()` and `__repr__()`

### Answer

`__str__()` is generally intended for a readable representation.

`__repr__()` is generally intended for a detailed developer-oriented representation.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"Student: {self.name}"

    def __repr__(self):
        return f"Student({self.name!r})"
```

---

# 38. What is `super()`?

### Answer

`super()` returns a proxy that allows access to the next implementation in the Method Resolution Order.

It is commonly used to:

- Reuse parent functionality
- Call inherited methods
- Call a parent initializer
- Support cooperative multiple inheritance

### Example

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

Output:

```text
Parent
Child
```

---

# 39. Does `super()` Always Mean Parent?

### Answer

Not exactly.

A simple explanation is that `super()` is used to call inherited behavior, often from a parent.

Technically:

> `super()` follows the Method Resolution Order and accesses the next appropriate implementation.

This becomes particularly important in multiple inheritance.

---

# 40. What is MRO?

### Answer

MRO stands for **Method Resolution Order**.

It determines the order in which Python searches classes for methods and attributes.

### Example

```python
class A:
    pass


class B(A):
    pass


print(B.mro())
```

The order is approximately:

```text
B → A → object
```

---

# 41. What is Multiple Inheritance?

### Answer

Multiple inheritance occurs when a class inherits from more than one parent class.

### Example

```python
class A:
    def show_a(self):
        print("A")


class B:
    def show_b(self):
        print("B")


class C(A, B):
    pass


obj = C()

obj.show_a()
obj.show_b()
```

Output:

```text
A
B
```

---

# 42. What is the Diamond Problem?

### Answer

The diamond problem occurs when two parent classes inherit from the same base class and another class inherits from both parents.

Structure:

```text
        A
       / \
      B   C
       \ /
        D
```

Python uses MRO to determine the method lookup order.

---

# 43. What is C3 Linearization?

### Answer

C3 Linearization is the algorithm Python uses to calculate a consistent MRO for multiple inheritance.

For most interviews, you should know:

- It is related to MRO.
- It is used in multiple inheritance.
- It produces a consistent lookup order.
- It preserves inheritance ordering constraints.

You normally do not need to manually implement the algorithm unless specifically asked.

---

# 44. What is Abstraction Using `ABC`?

### Answer

Python provides the `abc` module for defining abstract base classes.

A method decorated with:

```python
@abstractmethod
```

must be implemented by a concrete subclass before that subclass can normally be instantiated.

### Example

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class CreditCardPayment(Payment):
    def pay(self, amount):
        print("Paid", amount)


payment = CreditCardPayment()

payment.pay(1000)
```

Output:

```text
Paid 1000
```

---

# 45. Can We Create an Object of an Abstract Class?

### Answer

Not if it still contains unimplemented abstract methods.

### Example

```python
from abc import ABC, abstractmethod


class Animal(ABC):

    @abstractmethod
    def speak(self):
        pass
```

Trying to create:

```python
animal = Animal()
```

raises a `TypeError` because `speak()` is abstract.

---

# 46. What is an Abstract Method?

### Answer

An abstract method is a method declared by an abstract base class that subclasses are expected to implement.

Example:

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass
```

A concrete subclass must provide `start()` before it can normally be instantiated.

---

# 47. What is Name Mangling in Python?

### Answer

When an instance attribute starts with two leading underscores, Python performs **name mangling**.

For example:

```python
self.__balance
```

is internally transformed approximately to:

```python
_ClassName__balance
```

### Example

```python
class Account:
    def __init__(self):
        self.__balance = 1000


account = Account()

print(account._Account__balance)
```

Output:

```text
1000
```

This demonstrates that Python's `__private` naming convention does not provide absolute security or true private access.

---

# 48. What is the Difference Between `_variable` and `__variable`?

### `_variable`

A single leading underscore is a convention indicating:

> This is intended for internal use.

Example:

```python
self._balance
```

### `__variable`

Two leading underscores trigger name mangling.

Example:

```python
self.__balance
```

which is approximately stored as:

```python
_ClassName__balance
```

---

# 49. Does Python Have Truly Private Variables?

### Answer

Python does not provide the same strict private-member access enforcement found in some languages.

Instead:

- `_name` → convention for internal/protected-like use
- `__name` → name mangling

Name mangling mainly helps avoid accidental name conflicts, especially in inheritance.

---

# 50. What is a Property in Python?

### Answer

A property allows us to access a method like an attribute.

It is commonly used to control access to internal data without exposing direct implementation details.

### Example

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

# 51. Why Use `@property`?

### Answer

Properties are useful when we want attribute-like access while still controlling or validating the underlying value.

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
            raise ValueError("Marks must be between 0 and 100")


student = Student(80)

student.marks = 90

print(student.marks)
```

Output:

```text
90
```

---

# 52. What is the Difference Between `@property` and Getter/Setter Methods?

### Traditional Approach

```python
student.get_marks()
student.set_marks(90)
```

### Property Approach

```python
student.marks
student.marks = 90
```

Properties provide a cleaner interface while still allowing validation and controlled access.

---

# 53. What is an Association?

### Answer

Association is a general relationship between two objects.

For example:

```text
Teacher teaches Student
Doctor treats Patient
```

The objects can exist independently.

---

# 54. What is Aggregation?

### Answer

Aggregation represents a **has-a relationship** where the contained object can exist independently of the container.

Example:

```text
Department has Teachers
```

A teacher can exist even if the department is removed.

---

# 55. What is Composition?

### Answer

Composition is a stronger form of a has-a relationship where the contained object's lifecycle is strongly tied to the containing object.

Example:

```text
House has Rooms
```

Conceptually, the rooms are considered parts of the house.

### Python Example

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()


car = Car()

car.engine.start()
```

---

# 56. Aggregation vs Composition

| Aggregation | Composition |
|---|---|
| Weaker has-a relationship | Stronger has-a relationship |
| Parts can exist independently | Parts are strongly associated with the whole |
| Example: Department → Teacher | Example: Car → Engine |
| Lifecycle is less dependent | Lifecycle is more dependent |

---

# 57. What is `is-a` vs `has-a` Relationship?

### Is-A

Usually represented through inheritance.

```text
Dog is an Animal
```

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

### Has-A

Usually represented through composition/aggregation.

```text
Car has an Engine
```

```python
class Engine:
    pass


class Car:
    def __init__(self):
        self.engine = Engine()
```

---

# 58. What is an Object's Identity?

### Answer

Every Python object has an identity, type, and value.

The identity identifies the particular object during its lifetime.

We can inspect identity using:

```python
id(obj)
```

### Example

```python
a = []
b = []

print(id(a))
print(id(b))
```

The two objects have different identities.

---

# 59. What is `is` vs `==`?

### Answer

`==` checks whether two objects are equal according to their equality semantics.

`is` checks whether two references point to the **same object**.

### Example

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)
print(a is b)
```

Output:

```text
True
False
```

The lists have equal contents but are different objects.

---

# 60. Why is `is` Usually Used with `None`?

### Answer

The standard Python style is:

```python
if value is None:
    ...
```

because `None` is a singleton object and `is` checks identity.

Use:

```python
is None
```

rather than:

```python
== None
```

---

# 61. What is Object Equality?

### Answer

Object equality determines whether two objects should be considered equal.

For custom classes, this can be controlled using:

```python
__eq__()
```

### Example

```python
class Student:
    def __init__(self, roll_no):
        self.roll_no = roll_no

    def __eq__(self, other):
        return self.roll_no == other.roll_no


s1 = Student(101)
s2 = Student(101)

print(s1 == s2)
```

Output:

```text
True
```

---

# 62. What is Object Identity?

### Answer

Object identity refers to whether two references refer to the exact same object.

It can be checked using:

```python
is
```

### Example

```python
a = [1, 2]
b = a

print(a is b)
```

Output:

```text
True
```

Both variables reference the same list object.

---

# 63. What Happens When We Create an Object?

### Simplified Explanation

When we write:

```python
student = Student("Harsha")
```

Python:

```text
1. Calls __new__() to create the instance
        ↓
2. Calls __init__() to initialize it
        ↓
3. Stores the resulting reference in student
```

For normal Python classes, we usually customize `__init__()` rather than `__new__()`.

---

# 64. Can a Class Have Multiple Constructors?

### Answer

Python does not support traditional constructor overloading by defining multiple `__init__()` methods with different signatures.

The later definition would replace the earlier one.

Instead, we can use:

- Default arguments
- `*args`
- `**kwargs`
- Class methods as alternative constructors

### Example

```python
class Student:
    def __init__(self, name, age=None):
        self.name = name
        self.age = age
```

---

# 65. What is an Alternative Constructor?

### Answer

A class method can be used as an alternative way to create an object.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split(",")
        return cls(name, int(age))


student = Student.from_string("Harsha,22")

print(student.name)
print(student.age)
```

Output:

```text
Harsha
22
```

---

# 66. What is Method Resolution Order in Multiple Inheritance?

### Example

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
```

Output:

```text
C
```

The MRO is approximately:

```text
D → B → C → A → object
```

Python checks:

```text
D
↓
B
↓
C
↓
A
↓
object
```

`B` does not define `show()`, so Python finds it in `C`.

---

# 67. Why is `super()` Important in Multiple Inheritance?

### Answer

`super()` allows classes to cooperate according to the MRO rather than hardcoding a particular parent class.

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


C().show()
```

Output:

```text
A
B
C
```

---

# 68. What is the Liskov Substitution Principle?

### Interview-Safe Answer

The Liskov Substitution Principle says that objects of a child class should be usable wherever objects of the parent class are expected without breaking the expected behavior of the program.

In simple terms:

> A subclass should properly behave like its base class.

This is one of the SOLID principles.

---

# 69. What are SOLID Principles?

### Answer

SOLID is a set of five object-oriented design principles:

```text
S → Single Responsibility Principle
O → Open/Closed Principle
L → Liskov Substitution Principle
I → Interface Segregation Principle
D → Dependency Inversion Principle
```

For a Python developer interview, you should know the basic purpose of each.

---

# 70. What is Single Responsibility Principle?

### Answer

A class should have one main responsibility and one reason to change.

Instead of putting:

```text
Data processing
Database operations
Email sending
Report generation
```

into one huge class, responsibilities can be separated.

---

# 71. What is Open/Closed Principle?

### Answer

Software entities should generally be:

- Open for extension
- Closed for modification

We should prefer adding new behavior without unnecessarily changing stable existing code.

---

# 72. What is Liskov Substitution Principle?

### Answer

Subclasses should be usable wherever their base class is expected without breaking the program's expected behavior.

---

# 73. What is Interface Segregation Principle?

### Answer

Clients should not be forced to depend on methods they do not need.

In practice, prefer smaller, focused interfaces/contracts over one huge interface.

---

# 74. What is Dependency Inversion Principle?

### Answer

High-level code should depend on abstractions rather than directly depending on low-level implementation details.

This makes code easier to change and test.

---

# 75. What is Abstraction vs Interface in Python?

### Answer

Python does not have a separate `interface` keyword like Java.

Interfaces are commonly represented through:

- Abstract base classes
- Protocols
- Duck typing

For interview purposes:

> In Python, an interface is generally expressed through an expected set of methods or a formal abstraction such as an ABC or Protocol.

---

# 76. What is Dependency Injection?

### Answer

Dependency injection means providing an object's dependencies from outside rather than making the object create them internally.

### Example

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self, engine):
        self.engine = engine

    def start(self):
        self.engine.start()


engine = Engine()

car = Car(engine)

car.start()
```

Here the `Car` receives its `Engine` instead of creating one itself.

This can improve flexibility and testability.

---

# 77. What is Coupling?

### Answer

Coupling describes how strongly different parts of a system depend on each other.

### High Coupling

Components depend heavily on specific implementations.

### Low Coupling

Components interact through clearer interfaces and have fewer unnecessary dependencies.

Generally, we prefer **low coupling**.

---

# 78. What is Cohesion?

### Answer

Cohesion describes how closely related the responsibilities within a class or module are.

A highly cohesive class has a focused responsibility.

For example:

```text
EmployeeRepository
```

should primarily handle employee data persistence rather than also sending emails and generating UI.

Generally, we prefer **high cohesion** and **low coupling**.

---

# 79. High Cohesion vs Low Coupling

### Ideal Design

```text
High Cohesion
      +
Low Coupling
      ↓
More maintainable code
```

### Interview Answer

> I generally aim for high cohesion, where each component has a focused responsibility, and low coupling, where components are not unnecessarily dependent on each other's implementations.

---

# 80. Can Python Support Multiple Inheritance?

### Answer

Yes.

Python supports multiple inheritance.

### Example

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass
```

Python uses MRO to determine the method lookup order.

---

# 81. Can Python Support Multilevel Inheritance?

### Answer

Yes.

### Example

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass
```

The inheritance chain is:

```text
A
↓
B
↓
C
```

---

# 82. Can Python Support Hierarchical Inheritance?

### Answer

Yes.

Multiple child classes can inherit from the same parent.

### Example

```python
class Animal:
    pass


class Dog(Animal):
    pass


class Cat(Animal):
    pass
```

Structure:

```text
      Animal
      /    \
    Dog    Cat
```

---

# 83. What are the Types of Inheritance in Python?

Commonly discussed types include:

1. Single inheritance
2. Multiple inheritance
3. Multilevel inheritance
4. Hierarchical inheritance
5. Hybrid inheritance

---

# 84. What is Single Inheritance?

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

One child inherits from one parent.

```text
Animal
   ↓
 Dog
```

---

# 85. What is Multiple Inheritance?

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass
```

One child inherits from multiple parents.

```text
A     B
 \   /
   C
```

---

# 86. What is Multilevel Inheritance?

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass
```

```text
A
↓
B
↓
C
```

---

# 87. What is Hierarchical Inheritance?

```python
class Animal:
    pass


class Dog(Animal):
    pass


class Cat(Animal):
    pass
```

```text
     Animal
     /    \
   Dog    Cat
```

---

# 88. What is Hybrid Inheritance?

### Answer

Hybrid inheritance combines multiple inheritance patterns.

For example, a hierarchy may combine:

- Multilevel inheritance
- Multiple inheritance
- Hierarchical inheritance

Python's MRO is important when resolving methods in complex hybrid hierarchies.

---

# Coding Questions

# 89. Write a Simple Class and Create an Object

```python
class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)


student = Student("Harsha")

student.show()
```

Output:

```text
Harsha
```

---

# 90. Write an Example of Inheritance

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

---

# 91. Write an Example of Method Overriding

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    def speak(self):
        print("Bark")


dog = Dog()

dog.speak()
```

Output:

```text
Bark
```

---

# 92. Write an Example Using `super()`

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

Output:

```text
Parent
Child
```

---

# 93. Write a Program Demonstrating Encapsulation

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
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

---

# 94. Write a Program Demonstrating Polymorphism

```python
class Dog:
    def speak(self):
        print("Bark")


class Cat:
    def speak(self):
        print("Meow")


def make_sound(animal):
    animal.speak()


make_sound(Dog())
make_sound(Cat())
```

Output:

```text
Bark
Meow
```

---

# 95. Write a Program Using an Abstract Class

```python
from abc import ABC, abstractmethod


class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass


class Car(Vehicle):

    def start(self):
        print("Car started")


car = Car()

car.start()
```

---

# 96. Write a Program Demonstrating Class and Static Methods

```python
class Calculator:

    @classmethod
    def description(cls):
        print("This is a calculator")

    @staticmethod
    def add(a, b):
        return a + b


Calculator.description()

print(Calculator.add(10, 20))
```

Output:

```text
This is a calculator
30
```

---

# 97. Write a Program Demonstrating a Class Variable

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name


employee1 = Employee("A")
employee2 = Employee("B")

print(employee1.company)
print(employee2.company)
```

---

# 98. Write a Program Demonstrating `__str__()`

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

# 99. Write a Program Demonstrating Operator Overloading

```python
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return Number(self.value + other.value)


a = Number(10)
b = Number(20)

result = a + b

print(result.value)
```

Output:

```text
30
```

---

# 100. Write a Program Demonstrating Composition

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()


car = Car()

car.start()
```

Output:

```text
Engine started
```

---

# 101. Write a Program to Display MRO

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

# 102. Write a Program Demonstrating Multiple Inheritance

```python
class A:
    def show_a(self):
        print("A")


class B:
    def show_b(self):
        print("B")


class C(A, B):
    pass


obj = C()

obj.show_a()
obj.show_b()
```

---

# 103. Write a Custom Iterator

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

# 104. Coding Question — Implement a Bank Account

### Question

Create a `BankAccount` class with:

- Account holder
- Balance
- Deposit
- Withdraw
- Balance display

### Solution

```python
class BankAccount:
    def __init__(self, holder, balance=0):
        self.holder = holder
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


account = BankAccount("Harsha", 5000)

account.deposit(1000)
account.withdraw(2000)

print(account.get_balance())
```

Output:

```text
4000
```

### Concepts Covered

```text
Class
Object
Encapsulation
Instance variables
Methods
Validation
```

---

# 105. Coding Question — Employee Hierarchy

### Solution

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def work(self):
        print(self.name, "is working")


class Developer(Employee):
    def work(self):
        print(self.name, "is writing code")


class Tester(Employee):
    def work(self):
        print(self.name, "is testing software")


employees = [
    Developer("A"),
    Tester("B")
]

for employee in employees:
    employee.work()
```

Output:

```text
A is writing code
B is testing software
```

### Concepts Covered

```text
Inheritance
Method overriding
Polymorphism
```

---

# 106. Coding Question — Use an Abstract Base Class

### Solution

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


payments = [
    UPI(),
    Card()
]

for payment in payments:
    payment.pay(1000)
```

Output:

```text
Paid using UPI: 1000
Paid using Card: 1000
```

### Concepts Covered

```text
Abstraction
Inheritance
Polymorphism
Abstract methods
```

---

# 107. Coding Question — Class Method as Alternative Constructor

### Solution

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def from_string(cls, data):
        name, salary = data.split(",")
        return cls(name, int(salary))


employee = Employee.from_string("Harsha,50000")

print(employee.name)
print(employee.salary)
```

Output:

```text
Harsha
50000
```

---

# 108. Coding Question — Property Validation

### Solution

```python
class Student:
    def __init__(self, marks):
        self.marks = marks

    @property
    def marks(self):
        return self._marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self._marks = value
        else:
            raise ValueError("Invalid marks")


student = Student(85)

print(student.marks)

student.marks = 90

print(student.marks)
```

Output:

```text
85
90
```

---

# Scenario-Based Interview Questions

# 109. How Would You Design a Payment System Using OOP?

### Interview Answer

I would define a common payment abstraction and create separate implementations for different payment methods.

For example:

```text
Payment
   ↓
----------------
UPI
Card
NetBanking
```

The common interface can define:

```python
pay(amount)
```

Each payment type can implement its own behavior.

This gives us abstraction and polymorphism and makes it easier to add another payment method later.

### Example

```python
from abc import ABC, abstractmethod


class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass


class UPI(Payment):
    def pay(self, amount):
        print("UPI payment:", amount)


class Card(Payment):
    def pay(self, amount):
        print("Card payment:", amount)
```

---

# 110. How Would You Design a Vehicle System?

### Answer

I could define a common `Vehicle` abstraction and create classes such as:

```text
Vehicle
   ↓
----------------
Car
Bike
Truck
```

Common behavior could be defined in the base class, while specific behavior could be implemented in subclasses.

This demonstrates:

- Abstraction
- Inheritance
- Polymorphism

---

# 111. How Would You Design a Library Management System?

### Answer

I would separate responsibilities into classes such as:

```text
Book
Member
Library
Loan
```

For example:

```python
class Book:
    def __init__(self, title):
        self.title = title
        self.available = True


class Member:
    def __init__(self, name):
        self.name = name
```

The `Library` class could manage books and members.

I would avoid putting every responsibility into one large class because that would reduce cohesion.

---

# 112. How Would You Design a Flight Booking System Using OOP?

### Interview Answer

I would separate the system into entities such as:

```text
Flight
Passenger
Ticket
Booking
Airport
Payment
```

For example:

```text
Flight
  ↓
contains flight details

Passenger
  ↓
contains passenger details

Booking
  ↓
connects passenger and flight

Payment
  ↓
handles payment behavior
```

Different payment methods could implement a common payment interface, allowing polymorphism.

This design keeps responsibilities separated and makes the system easier to maintain.

---

# 113. How Would You Design a Social Network Using OOP?

### Interview Answer

I would identify entities such as:

```text
User
Post
Comment
Message
Notification
```

For example:

```python
class User:
    def __init__(self, name):
        self.name = name
        self.posts = []

    def create_post(self, content):
        self.posts.append(content)
```

The main idea is to keep each class responsible for a focused part of the system.

---

# 114. How Would You Decide Between Inheritance and Composition?

### Best Interview Answer

I first look at the relationship.

If there is a genuine:

```text
is-a
```

relationship, inheritance may be appropriate.

If there is a:

```text
has-a
```

relationship, composition is usually more appropriate.

For example:

```text
Dog is an Animal → inheritance

Car has an Engine → composition
```

I also consider maintainability and avoid deep inheritance when composition can provide a simpler design.

---

# 115. If a Parent and Child Both Have the Same Method, Which One Runs?

### Answer

If the object is an instance of the child class and the child overrides the method, the child's implementation is selected first.

### Example

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        print("Child")


Child().show()
```

Output:

```text
Child
```

---

# 116. How Can the Child Still Call the Parent Method?

### Answer

Using:

```python
super()
```

### Example

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        super().show()
        print("Child")
```

---

# 117. What Happens if You Don't Call `super().__init__()`?

### Answer

The parent initializer will not automatically execute as part of the child initializer.

If the parent initializer is responsible for setting important attributes, those attributes may not be initialized.

### Example

```python
class Parent:
    def __init__(self):
        self.name = "Parent"


class Child(Parent):
    def __init__(self):
        pass


obj = Child()

print(obj.name)
```

This raises:

```text
AttributeError
```

because `Parent.__init__()` was not called.

---

# 118. Can a Child Class Override `__init__()`?

### Answer

Yes.

### Example

```python
class Parent:
    def __init__(self):
        self.name = "Parent"


class Child(Parent):
    def __init__(self):
        super().__init__()
        self.age = 22
```

The child can add its own initialization while still reusing the parent's initialization.

---

# 119. What Happens if a Child Class Does Not Define `__init__()`?

### Answer

The child can inherit the parent's `__init__()` if the parent provides one and no child initializer overrides it.

### Example

```python
class Parent:
    def __init__(self, name):
        self.name = name


class Child(Parent):
    pass


obj = Child("Harsha")

print(obj.name)
```

Output:

```text
Harsha
```

---

# 120. Can We Access Parent Members Without `super()`?

### Answer

Yes, technically we can explicitly refer to the parent class.

Example:

```python
Parent.show(self)
```

However, `super()` is usually preferable because it follows MRO and supports cooperative multiple inheritance better.

---

# 121. Why Should We Avoid Deep Inheritance?

### Answer

Deep inheritance can make code:

- Harder to understand
- Harder to maintain
- More tightly coupled
- More difficult to debug

A practical design often favors simpler hierarchies and composition when appropriate.

---

# 122. What is the Difference Between OOP and Procedural Programming?

### OOP

Organizes code around:

```text
Objects
Classes
Data
Methods
```

### Procedural Programming

Organizes code primarily around:

```text
Functions
Procedures
Sequential operations
```

Python supports both procedural and object-oriented programming styles.

---

# 123. Why is OOP Useful in Real Projects?

### Answer

OOP can help with:

- Organizing large codebases
- Reusing functionality
- Separating responsibilities
- Modeling real-world entities
- Encapsulating state
- Extending behavior
- Maintaining complex systems

For example, a booking application can represent:

```text
Passenger
Flight
Booking
Payment
Ticket
```

as separate objects.

---

# 124. What are the Advantages of OOP?

### Answer

Important advantages include:

- Reusability
- Modularity
- Maintainability
- Encapsulation
- Extensibility
- Easier modeling of complex systems
- Better separation of responsibilities

---

# 125. What are the Disadvantages of OOP?

### Answer

OOP can introduce:

- More classes and boilerplate
- Additional abstraction
- More complex design for very small programs
- Overengineering if used unnecessarily
- More relationships to understand

### Interview-Safe Answer

> OOP is useful for organizing complex systems, but I would not force an object-oriented design where a simple function or data structure is sufficient.

---

# 126. What is the Most Important OOP Concept in Python Interviews?

### Answer

There is no single concept that covers everything.

You should be strongest in:

```text
Class and Object
        ↓
self
        ↓
__init__
        ↓
Instance/Class/Static methods
        ↓
Inheritance
        ↓
Method overriding
        ↓
Polymorphism
        ↓
Encapsulation
        ↓
Abstraction
        ↓
super()
        ↓
MRO
        ↓
Magic methods
```

These concepts are more important than memorizing obscure OOP details.

---

# 127. Most Important OOP Coding Questions to Practice

Before an interview, make sure you can write these without copying:

### Basic

```text
1. Create a class and object
2. Use __init__()
3. Use instance variables
4. Use class variables
5. Create instance methods
6. Create class methods
7. Create static methods
```

### Inheritance

```text
8. Single inheritance
9. Multilevel inheritance
10. Multiple inheritance
11. Method overriding
12. super()
13. Parent constructor using super()
```

### OOP Principles

```text
14. Encapsulation
15. Polymorphism
16. Abstraction
17. Abstract class
18. Abstract method
```

### Magic Methods

```text
19. __str__()
20. __repr__()
21. __len__()
22. __add__()
23. __eq__()
24. __iter__()
25. __next__()
```

### Design

```text
26. Composition
27. Aggregation
28. Dependency injection
29. Simple payment system
30. Simple booking system
```

---

# 128. Rapid-Fire OOP Questions

## Q1. What is OOP?

OOP is a programming paradigm that organizes code using objects and classes.

## Q2. What is a class?

A class is a blueprint used to create objects.

## Q3. What is an object?

An object is an instance of a class.

## Q4. What are the four pillars?

Encapsulation, inheritance, polymorphism, and abstraction.

## Q5. What is inheritance?

Inheritance allows a child class to reuse and extend functionality from a parent class.

## Q6. What is polymorphism?

Polymorphism allows a common interface or operation to work with different object types and behaviors.

## Q7. What is encapsulation?

Encapsulation bundles data and behavior and controls access to internal state.

## Q8. What is abstraction?

Abstraction exposes essential behavior while hiding implementation details.

## Q9. What is `self`?

`self` conventionally refers to the current instance.

## Q10. Is `self` a keyword?

No. It is a naming convention.

## Q11. What is `__init__()`?

It initializes an already-created instance.

## Q12. What is `__new__()`?

It creates and returns a new instance.

## Q13. What is method overriding?

A child class provides its own implementation of an inherited method.

## Q14. Does Python support traditional method overloading?

No, not in the same way as Java or C++. Similar behavior can be achieved using defaults, `*args`, `**kwargs`, etc.

## Q15. What is `super()`?

A proxy used to access the next implementation according to MRO.

## Q16. What is MRO?

Method Resolution Order.

## Q17. How do you check MRO?

```python
ClassName.mro()
```

or:

```python
ClassName.__mro__
```

## Q18. What is multiple inheritance?

A class inheriting from multiple parent classes.

## Q19. What is the diamond problem?

A multiple-inheritance hierarchy where two parents share a common ancestor.

## Q20. How does Python handle the diamond problem?

Using MRO and C3 Linearization.

## Q21. What is a class variable?

A variable associated with the class and shared by instances unless shadowed.

## Q22. What is an instance variable?

A variable associated with an individual object.

## Q23. What is a static method?

A method that does not automatically receive `self` or `cls`.

## Q24. What is a class method?

A method that receives the class as `cls`.

## Q25. What is duck typing?

Python focuses on whether an object supports the required behavior rather than requiring a specific class.

## Q26. What are magic methods?

Special dunder methods that integrate custom objects with Python's built-in operations.

## Q27. What is `__str__()`?

Readable string representation.

## Q28. What is `__repr__()`?

Developer-oriented representation.

## Q29. What is operator overloading?

Defining how operators behave for custom objects using special methods.

## Q30. What is composition?

A has-a relationship where an object contains another object.

## Q31. What is inheritance vs composition?

Inheritance represents an is-a relationship; composition represents a has-a relationship.

## Q32. What is an abstract class?

A class designed to define an abstraction and potentially contain abstract methods.

## Q33. Can an abstract class be instantiated?

Not while it has unimplemented abstract methods.

## Q34. What is an abstract method?

A method declared as required for concrete subclasses to implement.

## Q35. What is name mangling?

Python transforms names beginning with two underscores to reduce accidental name conflicts.

## Q36. Is `__private` truly private?

No. Python's name mangling is not strict access control.

## Q37. What is `@property`?

It allows method-backed attribute access.

## Q38. What is dependency injection?

Providing dependencies from outside an object rather than making the object create them internally.

## Q39. What is coupling?

The degree of dependency between components.

## Q40. What is cohesion?

How closely related the responsibilities within a component are.

---

# 129. Final OOP Revision Map

```text
                         PYTHON OOP
                              |
          +-------------------+-------------------+
          |                   |                   |
        CLASS               OBJECT             METHODS
          |                   |                   |
      Blueprint          Instance            Behavior
          |                   |
          +---------+---------+
                    |
             OOP PRINCIPLES
                    |
      +-------------+-------------+-------------+
      |             |             |             |
 Encapsulation  Inheritance  Polymorphism  Abstraction
      |             |             |             |
  __private       Parent       Overriding      ABC
  property        Child        Duck Typing     abstractmethod
                                 |
                           Operator Overloading
                                 |
                            Magic Methods
                                 |
                    +------------+-------------+
                    |            |             |
                 __str__       __add__       __eq__
                 __len__       __iter__      __next__

Inheritance
     |
     +---- super()
     |
     +---- MRO
            |
            +---- Multiple Inheritance
            |
            +---- Diamond Problem
            |
            +---- C3 Linearization

Design
  |
  +---- Composition
  +---- Aggregation
  +---- Dependency Injection
  +---- Low Coupling
  +---- High Cohesion
  +---- SOLID
```

# Final Interview Strategy

For Python OOP interviews, prioritize the concepts in this order:

### Priority 1 — Must Know

```text
Class
Object
self
__init__
Instance variables
Class variables
Instance methods
Inheritance
Method overriding
Polymorphism
Encapsulation
Abstraction
```

### Priority 2 — Very Important

```text
super()
MRO
Multiple inheritance
Class methods
Static methods
Magic methods
__str__
__repr__
Operator overloading
@property
```

### Priority 3 — Good to Know

```text
Composition
Aggregation
Duck typing
Dependency injection
Coupling
Cohesion
SOLID principles
__new__
C3 Linearization
```

### The safest way to answer OOP questions

When an interviewer asks a theoretical question:

```text
Definition
    ↓
Simple explanation
    ↓
Small code example
    ↓
Real-world use case
```

For example, for inheritance:

> Inheritance allows a child class to reuse and extend functionality from a parent class. For example, a `Dog` can inherit common behavior from an `Animal` class and add its own behavior such as `bark()`. In real applications, it can be useful when several related objects share common behavior.

Then, if asked to code:

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


dog = Dog()

dog.eat()
dog.bark()
```

This approach keeps the answer clear, practical, and easy to extend if the interviewer asks follow-up questions.