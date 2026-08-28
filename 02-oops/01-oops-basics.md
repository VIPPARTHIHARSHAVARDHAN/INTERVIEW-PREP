# 01 — OOP Basics

## 1. What is OOP?

### Answer

**Object-Oriented Programming (OOP)** is a programming approach where we organize code using **classes and objects**.

A class defines the **properties and behavior** of an entity, while an object is an **actual instance** of that class.

OOP helps us write code that is:

- Reusable
- Organized
- Maintainable
- Easier to extend
- Easier to model real-world entities

### Simple Example

```python
class Student:
    def study(self):
        print("Student is studying")


student1 = Student()
student1.study()
```

Here:

- `Student` → class
- `student1` → object
- `study()` → method
- `Student()` → creates an object

---

## 2. What is a Class?

### Answer

A **class is a blueprint or template for creating objects**.

It defines the data and behavior that objects created from it can have.

### Example

```python
class Car:
    def start(self):
        print("Car started")
```

Here, `Car` is a class.

We can create multiple objects from the same class:

```python
car1 = Car()
car2 = Car()

car1.start()
car2.start()
```

Both objects use the behavior defined by the `Car` class.

---

## 3. What is an Object?

### Answer

An **object is an instance of a class**.

When we create an object, memory is allocated for that particular instance and we can use the attributes and methods defined by the class.

### Example

```python
class Student:
    def study(self):
        print("Studying")


student1 = Student()
student2 = Student()
```

Here:

- `Student` → class
- `student1` → object
- `student2` → object

Both objects belong to the `Student` class.

---

## 4. Class vs Object

| Class | Object |
|---|---|
| Blueprint/template | Instance of a class |
| Defines structure and behavior | Represents an actual entity |
| Used to create objects | Created from a class |
| Does not represent one particular entity | Represents a particular instance |

### Example

```python
class Employee:
    pass


employee1 = Employee()
employee2 = Employee()
```

`Employee` is the class, while `employee1` and `employee2` are objects.

---

## 5. Why do we use OOP?

### Answer

We use OOP mainly to make large programs easier to **organize, reuse, maintain, and extend**.

Instead of keeping all data and functions separately, related data and behavior can be grouped inside classes.

### Example

In an application, instead of having separate functions for every employee, we can create an `Employee` class and create multiple employee objects.

```python
class Employee:
    def work(self):
        print("Employee is working")


employee1 = Employee()
employee2 = Employee()

employee1.work()
employee2.work()
```

This makes the code more structured and reusable.

---

## 6. What are the main principles of OOP?

The four major principles of OOP are:

1. **Encapsulation**
2. **Abstraction**
3. **Inheritance**
4. **Polymorphism**

These are commonly called the **four pillars of OOP**.

They will be covered in detail in the following OOP files.

---

## 7. What is Encapsulation?

### Answer

**Encapsulation means combining data and the methods that operate on that data inside a class, while controlling how that data is accessed.**

It helps protect the internal state of an object from unnecessary direct modification.

### Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance


account = BankAccount(5000)

print(account.get_balance())
```

Here, `__balance` is treated as a private attribute and is accessed through a method.

---

## 8. What is Abstraction?

### Answer

**Abstraction means hiding unnecessary implementation details and exposing only the important functionality to the user.**

For example, when we use a function, we generally care about what it does rather than how every internal step is implemented.

### Simple Example

```python
class Payment:
    def pay(self):
        print("Payment successful")


payment = Payment()
payment.pay()
```

The user simply calls `pay()` without needing to know the internal implementation of the payment process.

---

## 9. What is Inheritance?

### Answer

**Inheritance allows one class to acquire properties and methods from another class.**

It promotes code reuse and allows us to create a relationship between classes.

### Example

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    pass


dog = Dog()
dog.speak()
```

`Dog` inherits from `Animal`, so the `Dog` object can use the `speak()` method.

---

## 10. What is Polymorphism?

### Answer

**Polymorphism means the same interface or method name can behave differently depending on the object using it.**

### Example

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

Both classes have a `sound()` method, but the behavior is different.

---

## 11. What is the difference between a function and a method?

### Answer

A **function** is a block of reusable code that can exist independently.

A **method** is a function defined inside a class and generally operates on an object or class.

### Function

```python
def add(a, b):
    return a + b


print(add(10, 20))
```

### Method

```python
class Calculator:
    def add(self, a, b):
        return a + b


calculator = Calculator()

print(calculator.add(10, 20))
```

Here, `add()` inside `Calculator` is a method.

---

## 12. What is a constructor?

### Answer

A constructor is a special method that is automatically called when an object is created.

In Python, `__init__()` is commonly used to initialize an object's attributes.

### Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student = Student("Harsha", 22)

print(student.name)
print(student.age)
```

When `Student("Harsha", 22)` is executed, Python calls `__init__()` to initialize the object.

---

## 13. What is `self` in Python?

### Answer

`self` refers to the **current object**.

It allows us to access the attributes and methods belonging to that particular object.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student1 = Student("Harsha")
student2 = Student("Rahul")

student1.display()
student2.display()
```

For `student1`, `self` refers to `student1`.

For `student2`, `self` refers to `student2`.

So each object maintains its own value of `name`.

---

## 14. Why is `self` required?

### Answer

`self` is used to distinguish **instance attributes and methods belonging to the current object**.

For example:

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Here:

- `name` → parameter
- `self.name` → attribute belonging to the object

Without `self`, Python would not know that we want to store the value as an instance attribute.

---

## 15. Can we create multiple objects from one class?

### Answer

Yes.

One class can be used as a blueprint to create multiple objects.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student1 = Student("Harsha")
student2 = Student("Ravi")
student3 = Student("Anil")

student1.display()
student2.display()
student3.display()
```

Each object can have its own data while sharing the same class behavior.

---

## 16. Real-World Example of OOP

Consider an **employee management system**.

We can create an `Employee` class containing:

- Employee name
- Employee ID
- Department
- Salary
- Methods such as displaying employee details or calculating salary

```python
class Employee:
    def __init__(self, name, employee_id, department):
        self.name = name
        self.employee_id = employee_id
        self.department = department

    def display_details(self):
        print(self.name)
        print(self.employee_id)
        print(self.department)


employee = Employee("Harsha", 101, "Data Engineering")

employee.display_details()
```

This approach keeps the employee's data and related behavior together.

---

## 17. Real-World Example in Data Engineering

OOP can also be useful in a **data engineering application**.

For example, we could create a class responsible for processing data:

```python
class DataProcessor:
    def __init__(self, data):
        self.data = data

    def clean_data(self):
        print("Cleaning data")

    def transform_data(self):
        print("Transforming data")


processor = DataProcessor([10, 20, 30])

processor.clean_data()
processor.transform_data()
```

In a larger project, classes can help organize different responsibilities such as data ingestion, validation, transformation, and processing.

---

# Interview Questions

## Q1. What is OOP?

### Answer

OOP is a programming approach where programs are organized around classes and objects. It helps make code reusable, maintainable, and easier to organize.

---

## Q2. What is a class?

### Answer

A class is a blueprint or template used to create objects. It defines the attributes and methods that its objects can have.

---

## Q3. What is an object?

### Answer

An object is an instance of a class. It represents a particular entity created from the class.

---

## Q4. What are the four pillars of OOP?

### Answer

The four pillars are:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

---

## Q5. What is the difference between a class and an object?

### Answer

A class is a blueprint, while an object is an actual instance created from that blueprint.

---

## Q6. Why is OOP useful?

### Answer

OOP helps organize related data and behavior together and provides concepts such as inheritance, encapsulation, abstraction, and polymorphism. This makes applications easier to maintain, reuse, and extend.

---

## Q7. What is `self`?

### Answer

`self` refers to the current object and is used to access its instance attributes and methods.

---

## Q8. What is `__init__()`?

### Answer

`__init__()` is a special method commonly used to initialize an object's attributes when the object is created.

---

## Q9. What is the difference between a function and a method?

### Answer

A function can exist independently, while a method is a function defined inside a class and associated with the class or its objects.

---

## Q10. Can one class have multiple objects?

### Answer

Yes. A single class can be used to create any number of objects, and each object can maintain its own instance data.

---

# Small Coding Practice

## Question 1

Create a `Student` class that stores a student's name and age and displays them.

### Solution

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print("Name:", self.name)
        print("Age:", self.age)


student = Student("Harsha", 22)
student.display()
```

---

## Question 2

Create an `Employee` class with name and salary and display the employee details.

### Solution

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print("Name:", self.name)
        print("Salary:", self.salary)


employee = Employee("Harsha", 50000)
employee.display()
```

---

## Question 3

Create a `Calculator` class with methods for addition and subtraction.

### Solution

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def subtract(self, a, b):
        return a - b


calculator = Calculator()

print(calculator.add(10, 5))
print(calculator.subtract(10, 5))
```

---

# Key Points to Remember for Interviews

- **Class** → blueprint
- **Object** → instance of a class
- **`self`** → current object
- **`__init__()`** → commonly used to initialize object attributes
- **Method** → function defined inside a class
- **Encapsulation** → controlling access to data and combining data with behavior
- **Abstraction** → hiding unnecessary implementation details
- **Inheritance** → acquiring functionality from another class
- **Polymorphism** → same interface/method can have different behavior
- One class can create multiple objects.
- OOP is mainly useful for organizing, reusing, maintaining, and extending code.