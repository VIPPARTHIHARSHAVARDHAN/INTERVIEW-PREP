# 02 — Class, Object, Constructor & `self`

## 1. What is a Class?

### Answer

A **class** is a blueprint or template used to create objects.

It defines the data and behavior that objects created from it can have.

```python
class Student:
    def study(self):
        print("Student is studying")
```

Here, `Student` is a class.

---

## 2. What is an Object?

### Answer

An **object** is an instance of a class.

We create an object by calling the class:

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

---

## 3. Can We Create Multiple Objects from One Class?

### Answer

Yes. A single class can be used to create multiple objects.

Each object can have its own instance data.

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

Output:

```text
Harsha
Rahul
```

Both objects use the same class, but each object stores its own `name`.

---

# 4. What is a Constructor in Python?

### Answer

A constructor is used to **initialize an object when it is created**.

In Python, `__init__()` is commonly used for this purpose.

It is automatically called when an object is created.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student = Student("Harsha", 22)

print(student.name)
print(student.age)
```

Output:

```text
Harsha
22
```

When this line executes:

```python
student = Student("Harsha", 22)
```

Python creates the object and calls `__init__()` to initialize its attributes.

---

# 5. Is `__init__()` Actually a Constructor?

### Interview Answer

In Python, `__init__()` is commonly called the constructor, especially in interviews.

More precisely, object creation and initialization are separate steps. `__new__()` is responsible for creating the object, while `__init__()` initializes the already-created object.

For most application-level Python development, `__init__()` is the method we use to initialize object data.

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name
```

For normal interview discussions, saying **"`__init__()` is used as the constructor to initialize an object"** is a safe and practical answer.

---

# 6. What is `self`?

### Answer

`self` refers to the **current object**.

It allows us to access the attributes and methods belonging to that particular object.

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

Here:

- For `student1.display()`, `self` refers to `student1`.
- For `student2.display()`, `self` refers to `student2`.

Therefore, the same method can work with different objects.

---

# 7. Why Do We Use `self.name` Instead of Just `name`?

### Answer

`name` is the local parameter, while `self.name` is an **instance attribute belonging to the object**.

```python
class Student:
    def __init__(self, name):
        self.name = name
```

Here:

```text
name       → value received by the method
self.name  → value stored in the object
```

For example:

```python
student1 = Student("Harsha")
student2 = Student("Rahul")
```

The objects maintain separate values:

```text
student1.name → Harsha
student2.name → Rahul
```

---

# 8. Is `self` a Keyword in Python?

### Answer

No. `self` is **not a reserved keyword** in Python.

It is the conventional name used for the first parameter of an instance method.

Technically, another name can be used, but using `self` is the standard and recommended practice.

```python
class Student:
    def display(self):
        print("Hello")
```

Although Python allows another name:

```python
class Student:
    def display(current_object):
        print("Hello")
```

we should use `self` because it follows Python conventions and makes the code easier to understand.

---

# 9. Does Python Automatically Pass `self`?

### Answer

Yes. When we call an instance method through an object, Python passes that object as the first argument.

```python
class Student:
    def display(self):
        print("Student")


student = Student()
student.display()
```

Conceptually, Python treats the call similar to:

```python
Student.display(student)
```

So `self` receives the current object.

---

# 10. What is an Instance Attribute?

### Answer

An **instance attribute** is an attribute that belongs to a particular object.

It is usually created using `self`.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


student1 = Student("Harsha", 22)
student2 = Student("Rahul", 23)
```

Here:

```text
student1.name → Harsha
student1.age  → 22

student2.name → Rahul
student2.age  → 23
```

Each object has its own instance attributes.

---

# 11. What is an Instance Method?

### Answer

An **instance method** is a method that operates on an object and normally takes `self` as its first parameter.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student = Student("Harsha")
student.display()
```

Here, `display()` is an instance method.

---

# 12. Can We Change an Object's Attribute After Creation?

### Answer

Yes. Instance attributes can be changed after the object is created.

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Harsha")

print(student.name)

student.name = "Rahul"

print(student.name)
```

Output:

```text
Harsha
Rahul
```

The object's `name` attribute has been updated.

---

# 13. Can We Add an Attribute Directly to an Object?

### Answer

Yes. Python allows us to add attributes to an object dynamically.

```python
class Student:
    pass


student = Student()

student.name = "Harsha"
student.age = 22

print(student.name)
print(student.age)
```

Output:

```text
Harsha
22
```

However, in well-structured applications, important attributes are usually initialized inside `__init__()`.

---

# 14. What Happens If an Attribute Does Not Exist?

### Answer

If we try to access an attribute that does not exist, Python raises an `AttributeError`.

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Harsha")

print(student.age)
```

This results in an error similar to:

```text
AttributeError
```

because `age` was not defined for the object.

---

# 15. What is the Difference Between Class Attributes and Instance Attributes?

### Answer

A **class attribute** belongs to the class and can be shared by objects unless an object provides its own attribute with the same name.

An **instance attribute** belongs to a particular object.

### Example

```python
class Student:
    college = "ABC College"

    def __init__(self, name):
        self.name = name


student1 = Student("Harsha")
student2 = Student("Rahul")

print(student1.name)
print(student2.name)

print(student1.college)
print(student2.college)
```

Here:

```text
name    → instance attribute
college → class attribute
```

`name` can be different for each object, while `college` is shared through the class.

---

# 16. Example of Class Attribute

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name


employee1 = Employee("Harsha")
employee2 = Employee("Rahul")

print(employee1.company)
print(employee2.company)
```

Output:

```text
ABC
ABC
```

Both objects can access the class attribute.

---

# 17. Can an Instance Attribute Have the Same Name as a Class Attribute?

### Answer

Yes.

If an object has an instance attribute with the same name, the object's instance attribute takes precedence when accessed through that object.

```python
class Student:
    college = "ABC College"

    def __init__(self, name):
        self.name = name


student = Student("Harsha")

student.college = "XYZ College"

print(student.college)
print(Student.college)
```

Output:

```text
XYZ College
ABC College
```

The class attribute remains unchanged.

---

# 18. How Do We Access a Class Attribute?

### Answer

We can access a class attribute using either the class name or an object.

```python
class Student:
    college = "ABC College"


print(Student.college)

student = Student()

print(student.college)
```

For class-level data, accessing it through the class name is generally clearer.

---

# 19. What is the Difference Between `self` and the Class Name?

### Answer

`self` refers to the **current object**, while the class name refers to the **class itself**.

```python
class Student:
    college = "ABC College"

    def __init__(self, name):
        self.name = name
```

Here:

```text
self.name       → instance attribute
Student.college → class attribute
```

---

# 20. Can a Class Have Multiple Methods?

### Answer

Yes. A class can contain multiple methods representing different behaviors.

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def subtract(self, a, b):
        return a - b

    def multiply(self, a, b):
        return a * b


calculator = Calculator()

print(calculator.add(10, 5))
print(calculator.subtract(10, 5))
print(calculator.multiply(10, 5))
```

Output:

```text
15
5
50
```

---

# 21. Can a Class Have No Constructor?

### Answer

Yes.

If we don't define `__init__()`, Python can still create objects.

```python
class Student:
    def study(self):
        print("Studying")


student = Student()
student.study()
```

Here, no custom `__init__()` is defined, but the object can still be created.

---

# 22. What Happens When We Create an Object?

### Answer

When we create an object, Python creates an instance of the class and initializes it.

For example:

```python
class Student:
    def __init__(self, name):
        self.name = name


student = Student("Harsha")
```

The important flow is:

```text
Student("Harsha")
       ↓
Object is created
       ↓
__init__() is called
       ↓
"Harsha" is assigned to self.name
       ↓
student refers to the object
```

---

# 23. Can `__init__()` Return a Value?

### Answer

No. `__init__()` should return `None`.

It is used for initialization, not for returning a result.

Incorrect:

```python
class Student:
    def __init__(self):
        return 10
```

This causes a `TypeError`.

Correct:

```python
class Student:
    def __init__(self):
        self.name = "Harsha"
```

---

# 24. Can We Have Parameters in `__init__()`?

### Answer

Yes.

Parameters can be passed to `__init__()` to initialize different objects with different values.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary


employee1 = Employee("Harsha", 50000)
employee2 = Employee("Rahul", 60000)

print(employee1.name, employee1.salary)
print(employee2.name, employee2.salary)
```

---

# 25. What is the Difference Between `__init__()` and a Normal Method?

| `__init__()` | Normal Method |
|---|---|
| Used for initialization | Used for specific behavior |
| Automatically called during object creation | Usually called explicitly |
| Commonly initializes attributes | Performs operations |
| Special method | User-defined method |

### Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student = Student("Harsha")
student.display()
```

`__init__()` initializes the object, while `display()` performs an operation.

---

# 26. Real-World Example — Employee

In an employee management system, each employee can have different information.

```python
class Employee:
    def __init__(self, name, employee_id, department):
        self.name = name
        self.employee_id = employee_id
        self.department = department

    def display_details(self):
        print("Name:", self.name)
        print("ID:", self.employee_id)
        print("Department:", self.department)


employee1 = Employee("Harsha", 101, "Data Engineering")
employee2 = Employee("Rahul", 102, "Development")

employee1.display_details()
employee2.display_details()
```

The class provides a common structure, while each object stores different employee information.

---

# 27. Real-World Example — Data Engineering

A data engineering application may have a class that represents a data-processing component.

```python
class DataProcessor:
    def __init__(self, source):
        self.source = source

    def process(self):
        print("Processing data from:", self.source)


processor1 = DataProcessor("S3")
processor2 = DataProcessor("Database")

processor1.process()
processor2.process()
```

The same class can represent different processing objects with different sources.

---

# 28. Interview Coding Question

### Question

Create a `Student` class with `name` and `marks`. Add a method to display the details.

### Answer

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def display(self):
        print("Name:", self.name)
        print("Marks:", self.marks)


student = Student("Harsha", 85)

student.display()
```

---

# 29. Interview Coding Question

### Question

Create an `Employee` class and calculate the annual salary from the monthly salary.

### Answer

```python
class Employee:
    def __init__(self, name, monthly_salary):
        self.name = name
        self.monthly_salary = monthly_salary

    def annual_salary(self):
        return self.monthly_salary * 12


employee = Employee("Harsha", 50000)

print(employee.annual_salary())
```

Output:

```text
600000
```

---

# 30. Interview Coding Question

### Question

Create a `BankAccount` class with deposit and withdrawal methods.

### Answer

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
        else:
            print("Insufficient balance")

    def display_balance(self):
        print("Balance:", self.balance)


account = BankAccount(5000)

account.deposit(2000)
account.withdraw(1000)

account.display_balance()
```

Output:

```text
Balance: 6000
```

---

# 31. Quick Interview Revision

### Class

A blueprint used to create objects.

### Object

An instance of a class.

### `__init__()`

Commonly used to initialize an object when it is created.

### `self`

Reference to the current object.

### Instance Attribute

Data belonging to a particular object.

### Class Attribute

Data associated with the class and commonly shared by its instances.

### Instance Method

A method that operates on an object and normally receives `self`.

### Important Flow

```text
Class
  ↓
Create Object
  ↓
__init__()
  ↓
Initialize Instance Attributes
  ↓
Use Instance Methods
```

### Most Important Interview Questions from This File

1. What is a class?
2. What is an object?
3. What is a constructor in Python?
4. What is `__init__()`?
5. What is `self`?
6. Why do we use `self`?
7. Is `self` a keyword?
8. How does Python pass `self`?
9. What are instance attributes?
10. What are class attributes?
11. Class attribute vs instance attribute?
12. What is an instance method?
13. Can we create multiple objects from one class?
14. Can we change object attributes after creation?
15. Can we add attributes dynamically?
16. What happens if an attribute doesn't exist?
17. Can a class exist without `__init__()`?
18. Can `__init__()` have parameters?
19. Can `__init__()` return a value?
20. Difference between `__init__()` and a normal method?
21. What happens when an object is created?
22. Explain class and object with a real-world example.