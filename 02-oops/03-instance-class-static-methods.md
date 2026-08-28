# 03 — Instance, Class & Static Methods

## 1. What are Instance Methods?

### Answer

An **instance method** is a method that works with the data of a particular object.

It takes `self` as its first parameter and can access instance attributes and other instance methods.

```python
class Student:
    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def display(self):
        print(self.name)
        print(self.marks)


student = Student("Harsha", 85)

student.display()
```

Here, `display()` is an instance method because it uses `self` to access the data of the current object.

---

## 2. Why is `self` Used in Instance Methods?

### Answer

`self` represents the **current object**.

It allows an instance method to access the attributes and other methods belonging to that particular object.

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


employee1 = Employee("Harsha")
employee2 = Employee("Rahul")

employee1.display()
employee2.display()
```

For `employee1.display()`, `self` refers to `employee1`.

For `employee2.display()`, `self` refers to `employee2`.

---

# 3. What are Class Methods?

### Answer

A **class method** is a method that works with the class rather than a particular object.

It is created using the `@classmethod` decorator and takes `cls` as its first parameter.

`cls` refers to the class itself.

```python
class Student:
    college = "ABC College"

    @classmethod
    def change_college(cls, new_college):
        cls.college = new_college


Student.change_college("XYZ College")

print(Student.college)
```

Output:

```text
XYZ College
```

Here, `cls` refers to the `Student` class.

---

# 4. What is `cls`?

### Answer

`cls` is the conventional name for the first parameter of a class method.

It refers to the **class itself**.

```python
class Employee:
    company = "ABC"

    @classmethod
    def display_company(cls):
        print(cls.company)


Employee.display_company()
```

Here:

```text
cls → Employee class
cls.company → Employee.company
```

Just like `self` is conventionally used for an object, `cls` is conventionally used for a class.

---

# 5. What is the `@classmethod` Decorator?

### Answer

`@classmethod` converts a normal method into a class method.

A class method receives the class as its first argument instead of an individual object.

```python
class Employee:
    company = "ABC"

    @classmethod
    def display_company(cls):
        print(cls.company)


Employee.display_company()
```

Class methods can be called directly using the class.

---

# 6. What are Static Methods?

### Answer

A **static method** is a method that does not depend on a particular object or class.

It is defined using the `@staticmethod` decorator.

It does not require `self` or `cls`.

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

The `add()` method does not need any object-specific or class-specific data, so it is suitable as a static method.

---

# 7. Why Do We Use Static Methods?

### Answer

We use static methods when a function is logically related to a class but does not need access to either:

- Instance data
- Class data

For example:

```python
class Calculator:

    @staticmethod
    def multiply(a, b):
        return a * b


print(Calculator.multiply(5, 4))
```

`multiply()` only works with the values provided to it, so it does not need `self` or `cls`.

---

# 8. Instance Method vs Class Method vs Static Method

| Feature | Instance Method | Class Method | Static Method |
|---|---|---|---|
| Decorator | None required | `@classmethod` | `@staticmethod` |
| First parameter | `self` | `cls` | None required |
| Works with | Object | Class | Neither specifically |
| Access instance attributes | Yes | No, not directly | No |
| Access class attributes | Yes | Yes | No, not through `self`/`cls` |
| Can be called using object | Yes | Yes | Yes |
| Can be called using class | Generally requires an object | Yes | Yes |

---

# 9. Simple Example of All Three Methods

```python
class Student:
    college = "ABC College"

    def __init__(self, name):
        self.name = name

    # Instance method
    def display_name(self):
        print(self.name)

    # Class method
    @classmethod
    def display_college(cls):
        print(cls.college)

    # Static method
    @staticmethod
    def add(a, b):
        return a + b


student = Student("Harsha")

student.display_name()

Student.display_college()

print(Student.add(10, 20))
```

Output:

```text
Harsha
ABC College
30
```

The three methods have different responsibilities:

```text
Instance method → works with object data
Class method    → works with class data
Static method   → independent utility functionality
```

---

# 10. When Should We Use an Instance Method?

### Answer

Use an instance method when the operation needs information stored inside a particular object.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def annual_salary(self):
        return self.salary * 12


employee = Employee("Harsha", 50000)

print(employee.annual_salary())
```

`annual_salary()` needs the employee's salary, so it is an instance method.

---

# 11. When Should We Use a Class Method?

### Answer

Use a class method when the operation needs to work with **class-level data** or when we want to provide an alternative way to create objects.

Example:

```python
class Employee:
    company = "ABC"

    @classmethod
    def change_company(cls, company_name):
        cls.company = company_name


Employee.change_company("XYZ")

print(Employee.company)
```

Here, the method changes class-level data, so `@classmethod` is appropriate.

---

# 12. When Should We Use a Static Method?

### Answer

Use a static method when the functionality is related to the class but does not require object or class data.

```python
class Validator:

    @staticmethod
    def is_valid_age(age):
        return age >= 18


print(Validator.is_valid_age(22))
```

The method only needs the `age` passed to it.

---

# 13. Can a Class Method Access Class Variables?

### Answer

Yes.

A class method receives the class through `cls`, so it can access and modify class variables.

```python
class Employee:
    company = "ABC"

    @classmethod
    def display_company(cls):
        print(cls.company)


Employee.display_company()
```

Output:

```text
ABC
```

---

# 14. Can an Instance Method Access Class Variables?

### Answer

Yes.

An instance method can access both instance attributes and class attributes.

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)
        print(self.company)


employee = Employee("Harsha")

employee.display()
```

Output:

```text
Harsha
ABC
```

---

# 15. Can a Static Method Access Instance Variables?

### Answer

Not directly, because a static method does not automatically receive `self`.

```python
class Student:
    def __init__(self, name):
        self.name = name

    @staticmethod
    def display():
        print(self.name)
```

This will not work because `self` is not available inside the static method.

If an object is explicitly passed as an argument, it can be used, but then the method is no longer using the normal static-method pattern.

---

# 16. Can a Static Method Access Class Variables?

### Answer

A static method does not automatically receive `cls`, so it cannot directly access class data through `cls`.

For example:

```python
class Student:
    college = "ABC"

    @staticmethod
    def display():
        print(Student.college)


Student.display()
```

This works because the class name is explicitly used.

However, if the method needs class-specific data, a class method is generally more appropriate.

---

# 17. Can We Call an Instance Method Using the Class?

### Answer

Yes, but we must explicitly provide the object as an argument.

```python
class Student:
    def display(self):
        print("Student")


student = Student()

Student.display(student)
```

Normally, we use:

```python
student.display()
```

because Python automatically passes `student` as `self`.

---

# 18. Can We Call a Class Method Using an Object?

### Answer

Yes.

A class method can be called through either the class or an instance.

```python
class Student:
    college = "ABC"

    @classmethod
    def display_college(cls):
        print(cls.college)


student = Student()

Student.display_college()
student.display_college()
```

Both calls refer to the class.

For class-level functionality, calling it through the class is usually clearer.

---

# 19. Can We Call a Static Method Using an Object?

### Answer

Yes.

A static method can be called using either the class or an object.

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b


calculator = Calculator()

print(Calculator.add(10, 20))
print(calculator.add(10, 20))
```

Both calls work.

Usually, if the method does not depend on an object, calling it through the class makes the intent clearer.

---

# 20. What is the Difference Between `self` and `cls`?

### Answer

`self` refers to the **current object**, while `cls` refers to the **current class**.

```python
class Student:
    college = "ABC"

    def __init__(self, name):
        self.name = name

    def instance_method(self):
        print(self.name)

    @classmethod
    def class_method(cls):
        print(cls.college)
```

Here:

```text
self → object
cls  → class
```

---

# 21. Can a Class Have All Three Types of Methods?

### Answer

Yes.

A class can contain instance methods, class methods, and static methods.

```python
class Employee:
    company = "ABC"

    def __init__(self, name):
        self.name = name

    def display_name(self):
        print(self.name)

    @classmethod
    def display_company(cls):
        print(cls.company)

    @staticmethod
    def add(a, b):
        return a + b


employee = Employee("Harsha")

employee.display_name()
Employee.display_company()

print(Employee.add(10, 20))
```

---

# 22. What is a Factory Method?

### Answer

A common use of a class method is to create objects in different ways.

A class method used to provide an alternative object-creation mechanism is often called a **factory method**.

### Example

```python
class Employee:
    def __init__(self, name, department):
        self.name = name
        self.department = department

    @classmethod
    def from_string(cls, data):
        name, department = data.split(",")
        return cls(name, department)


employee = Employee.from_string("Harsha,Data Engineering")

print(employee.name)
print(employee.department)
```

Output:

```text
Harsha
Data Engineering
```

Here, `from_string()` provides an alternative way to create an `Employee` object.

---

# 23. Why Use `cls()` Instead of the Class Name in a Class Method?

### Answer

Using `cls()` makes the class method more flexible, especially when inheritance is involved.

```python
class Employee:
    def __init__(self, name):
        self.name = name

    @classmethod
    def create(cls, name):
        return cls(name)
```

Using `cls` allows subclasses to inherit the method and create an instance of the subclass rather than always creating an `Employee`.

---

# 24. Real-World Example — Employee Management

Suppose an employee management system needs:

- Employee-specific operations
- Company-wide information
- Utility validation

We can separate these responsibilities:

```python
class Employee:
    company = "ABC Technologies"

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    # Instance method
    def annual_salary(self):
        return self.salary * 12

    # Class method
    @classmethod
    def company_name(cls):
        return cls.company

    # Static method
    @staticmethod
    def is_valid_salary(salary):
        return salary > 0


employee = Employee("Harsha", 50000)

print(employee.annual_salary())
print(Employee.company_name())
print(Employee.is_valid_salary(50000))
```

The responsibilities are separated clearly:

```text
Instance method → employee-specific information
Class method    → company-level information
Static method   → independent validation
```

---

# 25. Real-World Example — Data Engineering

In a data engineering application, we might have a data processor where:

- Instance methods process a particular dataset.
- Class methods manage configuration shared by the processor.
- Static methods perform independent validation.

```python
class DataProcessor:
    default_format = "CSV"

    def __init__(self, data):
        self.data = data

    # Instance method
    def process(self):
        print("Processing:", self.data)

    # Class method
    @classmethod
    def set_default_format(cls, file_format):
        cls.default_format = file_format

    # Static method
    @staticmethod
    def is_valid_file(file_name):
        return file_name.endswith(".csv")


processor = DataProcessor("sales.csv")

processor.process()

DataProcessor.set_default_format("JSON")

print(DataProcessor.default_format)

print(DataProcessor.is_valid_file("sales.csv"))
```

This demonstrates how different method types can represent different responsibilities in an application.

---

# 26. Interview Question — Explain Instance, Class and Static Methods

### Best Answer

Python provides three commonly used method types.

**Instance methods** use `self` and work with object-specific data.

**Class methods** use `cls` and work with class-level data. They are created using `@classmethod`.

**Static methods** don't automatically receive either `self` or `cls`. They are useful for utility operations that are logically related to the class but don't depend on its state.

For example, in an employee class, calculating an individual employee's salary would be an instance method, changing a company-wide setting could be a class method, and validating an input could be a static method.

---

# 27. Interview Question — What is the Difference Between `@classmethod` and `@staticmethod`?

### Answer

The main difference is that a class method receives the class as `cls`, while a static method does not automatically receive either the class or object.

```python
class Example:

    @classmethod
    def class_method(cls):
        print(cls)

    @staticmethod
    def static_method():
        print("Static method")
```

A class method is useful when we need class-level information or behavior.

A static method is useful when the operation is independent of class and instance state.

---

# 28. Interview Question — When Would You Choose a Static Method Over an Instance Method?

### Answer

I would choose a static method when the operation does not need any information from the object.

For example, if I have a `Validator` class and need to validate whether a number is positive, the method only needs the number passed to it and doesn't need object state.

```python
class Validator:

    @staticmethod
    def is_positive(number):
        return number > 0
```

---

# 29. Interview Question — When Would You Choose a Class Method?

### Answer

I would choose a class method when the operation needs to work with class-level data or when I need an alternative way to create objects.

For example:

```python
class Employee:
    company = "ABC"

    @classmethod
    def change_company(cls, name):
        cls.company = name
```

Since the method modifies class-level data, a class method is appropriate.

---

# 30. Interview Question — Can a Class Method Access Instance Data?

### Answer

Not directly.

A class method receives the class through `cls`, not a particular object through `self`.

If an instance is explicitly provided as an argument, it can access that instance, but that is not the normal purpose of a class method.

---

# 31. Interview Question — Can a Static Method Access `self`?

### Answer

No, not automatically.

A static method does not receive `self`, because it is not bound to a particular object.

```python
class Student:

    @staticmethod
    def display():
        print(self.name)
```

The above will fail because `self` is not defined.

---

# 32. Interview Question — Does `@staticmethod` Make a Method Faster?

### Answer

The main purpose of `@staticmethod` is **not performance optimization**.

It communicates that the method does not depend on instance or class state and keeps the utility logically grouped with the class.

---

# 33. Interview Question — Is `self` Mandatory as a Name?

### Answer

No.

`self` is a convention, not a reserved keyword.

Python expects the first parameter of an instance method to receive the object, but the parameter can technically have another name.

However, using `self` is the standard and recommended practice.

---

# 34. Interview Question — Is `cls` a Keyword?

### Answer

No.

`cls` is a convention used for the first parameter of a class method.

The important part is that `@classmethod` causes Python to pass the class as the first argument.

---

# 35. Coding Question — Create All Three Methods

### Question

Create a class that contains:

- An instance method to display a person's name.
- A class method to display the organization.
- A static method to add two numbers.

### Solution

```python
class Person:
    organization = "ABC Technologies"

    def __init__(self, name):
        self.name = name

    def display_name(self):
        print("Name:", self.name)

    @classmethod
    def display_organization(cls):
        print("Organization:", cls.organization)

    @staticmethod
    def add(a, b):
        return a + b


person = Person("Harsha")

person.display_name()
Person.display_organization()

print(Person.add(10, 20))
```

Output:

```text
Name: Harsha
Organization: ABC Technologies
30
```

---

# 36. Coding Question — Class Method to Modify Class Data

### Question

Create a `Student` class with a class variable `school`. Create a class method to change the school name.

### Solution

```python
class Student:
    school = "ABC School"

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school


print(Student.school)

Student.change_school("XYZ School")

print(Student.school)
```

Output:

```text
ABC School
XYZ School
```

---

# 37. Coding Question — Static Method

### Question

Create a static method that checks whether a number is even.

### Solution

```python
class Number:

    @staticmethod
    def is_even(number):
        return number % 2 == 0


print(Number.is_even(10))
print(Number.is_even(7))
```

Output:

```text
True
False
```

---

# 38. Coding Question — Instance Method

### Question

Create an `Employee` class with salary and create an instance method to calculate annual salary.

### Solution

```python
class Employee:
    def __init__(self, salary):
        self.salary = salary

    def annual_salary(self):
        return self.salary * 12


employee = Employee(50000)

print(employee.annual_salary())
```

Output:

```text
600000
```

---

# 39. Quick Revision

```text
Instance Method
    ↓
Uses self
    ↓
Works with object-specific data


Class Method
    ↓
Uses cls
    ↓
Works with class-level data
    ↓
Uses @classmethod


Static Method
    ↓
No self or cls automatically
    ↓
Independent utility operation
    ↓
Uses @staticmethod
```

## Easy Way to Remember

```text
self → Object
cls  → Class
static → Neither
```

## Most Important Interview Questions

1. What is an instance method?
2. What is a class method?
3. What is a static method?
4. What is `self`?
5. What is `cls`?
6. Difference between instance, class and static methods?
7. Why do we use `@classmethod`?
8. Why do we use `@staticmethod`?
9. When should you use an instance method?
10. When should you use a class method?
11. When should you use a static method?
12. Can an instance method access class variables?
13. Can a class method access instance variables?
14. Can a static method access instance variables?
15. Can a static method access class variables?
16. Can class methods be called using objects?
17. Can static methods be called using objects?
18. Can instance methods be called using the class?
19. What is a factory method?
20. Why use `cls()` instead of the class name?
21. Is `self` a keyword?
22. Is `cls` a keyword?
23. Can a class contain all three types of methods?
24. Give a real-world example of instance, class and static methods.
25. Write code demonstrating all three method types.