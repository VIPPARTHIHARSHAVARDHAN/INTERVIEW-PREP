# 04 — Inheritance

## 1. What is Inheritance?

### Answer

**Inheritance is an OOP concept where one class can acquire the attributes and methods of another class.**

The existing class is called the **parent class**, **base class**, or **superclass**.

The new class is called the **child class**, **derived class**, or **subclass**.

Inheritance mainly helps with **code reusability** and creating relationships between classes.

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

Output:

```text
Animal makes a sound
```

Here:

- `Animal` → parent class
- `Dog` → child class
- `speak()` → inherited method

---

# 2. Why Do We Use Inheritance?

### Answer

The main purpose of inheritance is to **reuse existing code** instead of writing the same functionality again.

It also helps represent an **is-a relationship** between classes.

For example:

```text
Dog is an Animal
Car is a Vehicle
Manager is an Employee
```

### Example

```python
class Employee:
    def work(self):
        print("Employee is working")


class Manager(Employee):
    def manage_team(self):
        print("Manager is managing the team")


manager = Manager()

manager.work()
manager.manage_team()
```

The `Manager` class reuses the `work()` method from `Employee`.

---

# 3. What is a Parent Class?

### Answer

A **parent class** is the class whose attributes and methods are inherited by another class.

It can also be called:

- Base class
- Superclass

### Example

```python
class Animal:
    def speak(self):
        print("Animal speaks")


class Dog(Animal):
    pass
```

Here, `Animal` is the parent class.

---

# 4. What is a Child Class?

### Answer

A **child class** is a class that inherits from another class.

It can also be called:

- Derived class
- Subclass

### Example

```python
class Animal:
    def speak(self):
        print("Animal speaks")


class Dog(Animal):
    pass
```

Here, `Dog` is the child class.

---

# 5. How Do We Implement Inheritance in Python?

### Answer

We specify the parent class inside the parentheses while defining the child class.

```python
class Parent:
    def display(self):
        print("Parent method")


class Child(Parent):
    pass
```

Now the child can use the parent's method:

```python
obj = Child()

obj.display()
```

Output:

```text
Parent method
```

---

# 6. Can a Child Class Have Its Own Methods?

### Answer

Yes.

A child class can inherit methods from the parent and also define its own methods.

```python
class Animal:
    def speak(self):
        print("Animal speaks")


class Dog(Animal):
    def bark(self):
        print("Dog barks")


dog = Dog()

dog.speak()
dog.bark()
```

Output:

```text
Animal speaks
Dog barks
```

---

# 7. Can a Child Class Have Its Own Attributes?

### Answer

Yes.

A child class can define additional attributes that are specific to the child.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed


dog = Dog("Bruno", "Labrador")

print(dog.name)
print(dog.breed)
```

Output:

```text
Bruno
Labrador
```

However, when the parent already has an initializer, using `super()` is generally cleaner. This is covered later in this file.

---

# 8. What are the Types of Inheritance in Python?

The commonly discussed types are:

1. **Single Inheritance**
2. **Multiple Inheritance**
3. **Multilevel Inheritance**
4. **Hierarchical Inheritance**
5. **Hybrid Inheritance**

---

# 9. What is Single Inheritance?

### Answer

**Single inheritance** occurs when one child class inherits from one parent class.

```text
Parent
   ↓
Child
```

### Example

```python
class Animal:
    def speak(self):
        print("Animal speaks")


class Dog(Animal):
    def bark(self):
        print("Dog barks")


dog = Dog()

dog.speak()
dog.bark()
```

Here, `Dog` directly inherits from `Animal`.

---

# 10. What is Multiple Inheritance?

### Answer

**Multiple inheritance** occurs when one child class inherits from more than one parent class.

```text
Parent1    Parent2
    \       /
      Child
```

### Example

```python
class Father:
    def skills_from_father(self):
        print("Driving")


class Mother:
    def skills_from_mother(self):
        print("Cooking")


class Child(Father, Mother):
    pass


child = Child()

child.skills_from_father()
child.skills_from_mother()
```

Output:

```text
Driving
Cooking
```

Here, `Child` inherits from both `Father` and `Mother`.

---

# 11. What is Multilevel Inheritance?

### Answer

**Multilevel inheritance** occurs when inheritance happens across multiple levels.

```text
Grandparent
     ↓
   Parent
     ↓
   Child
```

### Example

```python
class Grandparent:
    def house(self):
        print("Grandparent's house")


class Parent(Grandparent):
    def car(self):
        print("Parent's car")


class Child(Parent):
    def bike(self):
        print("Child's bike")


child = Child()

child.house()
child.car()
child.bike()
```

The `Child` can access methods from both `Parent` and `Grandparent`.

---

# 12. What is Hierarchical Inheritance?

### Answer

**Hierarchical inheritance** occurs when multiple child classes inherit from the same parent class.

```text
       Parent
       /    \
   Child1  Child2
```

### Example

```python
class Animal:
    def eat(self):
        print("Animal eats")


class Dog(Animal):
    def bark(self):
        print("Dog barks")


class Cat(Animal):
    def meow(self):
        print("Cat meows")


dog = Dog()
cat = Cat()

dog.eat()
dog.bark()

cat.eat()
cat.meow()
```

Both `Dog` and `Cat` inherit from `Animal`.

---

# 13. What is Hybrid Inheritance?

### Answer

**Hybrid inheritance** is a combination of two or more types of inheritance.

For example, a design can combine hierarchical and multiple inheritance.

```text
       A
      / \
     B   C
      \ /
       D
```

### Example

```python
class A:
    def method_a(self):
        print("A")


class B(A):
    def method_b(self):
        print("B")


class C(A):
    def method_c(self):
        print("C")


class D(B, C):
    def method_d(self):
        print("D")


obj = D()

obj.method_a()
obj.method_b()
obj.method_c()
obj.method_d()
```

Python resolves the inheritance order using the **Method Resolution Order (MRO)**.

---

# 14. What is Method Overriding in Inheritance?

### Answer

**Method overriding** occurs when a child class provides its own implementation of a method that already exists in the parent class.

### Example

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")


class Dog(Animal):
    def speak(self):
        print("Dog barks")


dog = Dog()

dog.speak()
```

Output:

```text
Dog barks
```

The child implementation overrides the inherited implementation.

---

# 15. Why is Method Overriding Useful?

### Answer

Method overriding allows a child class to provide behavior that is more specific to itself while still maintaining the common structure provided by the parent class.

For example:

```python
class Animal:
    def speak(self):
        print("Animal sound")


class Dog(Animal):
    def speak(self):
        print("Bark")


class Cat(Animal):
    def speak(self):
        print("Meow")
```

Each child provides its own implementation of `speak()`.

This is also an important example of **polymorphism**.

---

# 16. What is `super()`?

### Answer

`super()` is used to access functionality from a parent class.

It is commonly used when a child class overrides a method but still wants to use the parent's implementation.

### Example

```python
class Parent:
    def display(self):
        print("Parent method")


class Child(Parent):
    def display(self):
        super().display()
        print("Child method")


child = Child()

child.display()
```

Output:

```text
Parent method
Child method
```

---

# 17. Why Do We Use `super()` in `__init__()`?

### Answer

When a child class has its own `__init__()`, we can use `super().__init__()` to initialize the attributes defined by the parent.

### Example

```python
class Employee:
    def __init__(self, name):
        self.name = name


class Manager(Employee):
    def __init__(self, name, team_size):
        super().__init__(name)
        self.team_size = team_size


manager = Manager("Harsha", 5)

print(manager.name)
print(manager.team_size)
```

Output:

```text
Harsha
5
```

This avoids repeating the parent's initialization logic.

---

# 18. What Happens If a Child Class Does Not Define `__init__()`?

### Answer

If the child class does not define its own `__init__()`, it can use the inherited `__init__()` from the parent.

```python
class Employee:
    def __init__(self, name):
        self.name = name


class Manager(Employee):
    pass


manager = Manager("Harsha")

print(manager.name)
```

Output:

```text
Harsha
```

---

# 19. What Happens If Both Parent and Child Have `__init__()`?

### Answer

The child class's `__init__()` is used when creating the child object.

If we also want to execute the parent's initialization, we explicitly call:

```python
super().__init__()
```

### Example

```python
class Employee:
    def __init__(self, name):
        self.name = name


class Manager(Employee):
    def __init__(self, name, team_size):
        super().__init__(name)
        self.team_size = team_size
```

This initializes both the parent and child attributes.

---

# 20. Does Python Support Multiple Inheritance?

### Answer

Yes.

Python supports multiple inheritance, where a class can inherit from multiple parent classes.

```python
class A:
    def method_a(self):
        print("A")


class B:
    def method_b(self):
        print("B")


class C(A, B):
    pass


obj = C()

obj.method_a()
obj.method_b()
```

---

# 21. What is the Problem with Multiple Inheritance?

### Answer

Multiple inheritance can create ambiguity when multiple parent classes contain methods with the same name.

For example:

```python
class A:
    def display(self):
        print("A")


class B:
    def display(self):
        print("B")


class C(A, B):
    pass
```

If we call:

```python
obj = C()
obj.display()
```

Python needs to determine which `display()` should be used.

Python solves this using **Method Resolution Order (MRO)**.

---

# 22. What is MRO?

### Answer

**MRO stands for Method Resolution Order.**

It defines the order in which Python searches classes when looking for a method or attribute.

We can see the MRO using:

```python
ClassName.mro()
```

or:

```python
ClassName.__mro__
```

### Example

```python
class A:
    pass


class B(A):
    pass


class C(B):
    pass


print(C.mro())
```

The order will show:

```text
C → B → A → object
```

The exact representation also includes Python's built-in `object` class.

---

# 23. How Does MRO Work in Multiple Inheritance?

### Example

```python
class A:
    def display(self):
        print("A")


class B(A):
    def display(self):
        print("B")


class C(A):
    def display(self):
        print("C")


class D(B, C):
    pass


obj = D()

obj.display()
```

Python follows the MRO to determine which implementation to use.

We can check it with:

```python
print(D.mro())
```

The important interview point is:

> Python uses Method Resolution Order to determine the order in which classes are searched for methods in inheritance hierarchies.

---

# 24. What is the Diamond Problem?

### Answer

The **diamond problem** occurs in multiple inheritance when a class inherits through multiple paths from the same base class.

Example:

```text
       A
      / \
     B   C
      \ /
       D
```

`D` receives inheritance through both `B` and `C`.

Python handles this using **MRO**, which provides a consistent order for method lookup.

### Example

```python
class A:
    def display(self):
        print("A")


class B(A):
    pass


class C(A):
    pass


class D(B, C):
    pass


obj = D()

obj.display()

print(D.mro())
```

Python determines the lookup order through MRO.

---

# 25. What is an "is-a" Relationship?

### Answer

An **is-a relationship** generally represents inheritance.

Examples:

```text
Dog is an Animal
Manager is an Employee
Car is a Vehicle
```

### Example

```python
class Vehicle:
    pass


class Car(Vehicle):
    pass
```

A `Car` is a `Vehicle`, so inheritance can represent this relationship.

---

# 26. Inheritance vs Composition

### Inheritance

Inheritance represents an **is-a** relationship.

```python
class Animal:
    pass


class Dog(Animal):
    pass
```

A dog is an animal.

### Composition

Composition generally represents a **has-a** relationship.

```python
class Engine:
    pass


class Car:
    def __init__(self):
        self.engine = Engine()
```

A car has an engine.

### Easy Way to Remember

```text
Inheritance → IS-A
Composition → HAS-A
```

---

# 27. Is Inheritance Always Better Than Composition?

### Answer

No.

Inheritance is useful when there is a genuine **is-a relationship** and the child logically represents a specialized form of the parent.

Composition is often better when we simply want to combine or reuse functionality without creating a strict parent-child relationship.

For example:

```text
Dog is an Animal        → inheritance makes sense
Car has an Engine       → composition makes sense
```

---

# 28. Real-World Example — Employee System

Suppose an organization has different types of employees.

We can create a common parent class:

```python
class Employee:
    def __init__(self, name):
        self.name = name

    def work(self):
        print(self.name, "is working")


class Developer(Employee):
    def write_code(self):
        print(self.name, "is writing code")


class DataEngineer(Employee):
    def build_pipeline(self):
        print(self.name, "is building a data pipeline")


developer = Developer("Rahul")
data_engineer = DataEngineer("Harsha")

developer.work()
developer.write_code()

data_engineer.work()
data_engineer.build_pipeline()
```

The common employee behavior is defined once in `Employee`, while specialized behavior is defined in the child classes.

---

# 29. Real-World Example — Data Engineering

Inheritance can be used when different data sources or processors share common behavior.

```python
class DataSource:
    def connect(self):
        print("Connecting to data source")


class S3Source(DataSource):
    def read_data(self):
        print("Reading data from S3")


class DatabaseSource(DataSource):
    def read_data(self):
        print("Reading data from database")


s3 = S3Source()
database = DatabaseSource()

s3.connect()
s3.read_data()

database.connect()
database.read_data()
```

Both sources share the `connect()` behavior while implementing their own data-reading behavior.

---

# 30. Interview Question — Explain Inheritance

### Best Answer

Inheritance is an OOP concept where a child class can reuse attributes and methods from a parent class. It promotes code reuse and helps represent an **is-a relationship** between classes.

For example, if `DataEngineer` and `Developer` are both types of `Employee`, common employee functionality can be placed in the `Employee` class and specialized functionality can be added to the child classes.

---

# 31. Interview Question — What are the Types of Inheritance in Python?

### Answer

The commonly discussed types are:

1. Single inheritance
2. Multiple inheritance
3. Multilevel inheritance
4. Hierarchical inheritance
5. Hybrid inheritance

Python supports all of these through its class inheritance mechanism.

---

# 32. Interview Question — What is Method Overriding?

### Answer

Method overriding occurs when a child class provides its own implementation of a method that already exists in the parent class.

```python
class Parent:
    def display(self):
        print("Parent")


class Child(Parent):
    def display(self):
        print("Child")


obj = Child()
obj.display()
```

Output:

```text
Child
```

---

# 33. Interview Question — What is `super()`?

### Best Answer

`super()` provides a convenient way to access functionality from a parent class.

It is commonly used when a child overrides a method but still needs the parent's behavior, especially when initializing parent attributes using `super().__init__()`.

---

# 34. Interview Question — What is MRO?

### Best Answer

MRO stands for **Method Resolution Order**. It defines the order in which Python searches classes for methods and attributes, especially when inheritance involves multiple classes.

We can inspect it using:

```python
print(MyClass.mro())
```

or:

```python
print(MyClass.__mro__)
```

---

# 35. Interview Question — Does Python Support Multiple Inheritance?

### Answer

Yes. Python allows a class to inherit from multiple parent classes.

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

# 36. Interview Question — What is the Difference Between Inheritance and Composition?

### Answer

Inheritance usually represents an **is-a relationship**, while composition represents a **has-a relationship**.

For example:

```text
Dog is an Animal → Inheritance

Car has an Engine → Composition
```

I would use inheritance when the child is genuinely a specialized form of the parent, and composition when I want to combine independent components.

---

# 37. Coding Question — Basic Inheritance

### Question

Create a `Person` class with a `display()` method and inherit it into a `Student` class.

### Solution

```python
class Person:
    def display(self):
        print("This is a person")


class Student(Person):
    def study(self):
        print("Student is studying")


student = Student()

student.display()
student.study()
```

---

# 38. Coding Question — Method Overriding

### Question

Create an `Animal` class with a `sound()` method and override it in a `Dog` class.

### Solution

```python
class Animal:
    def sound(self):
        print("Animal sound")


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

# 39. Coding Question — `super()`

### Question

Create an `Employee` class and a `Manager` class. Use `super()` to initialize the employee name.

### Solution

```python
class Employee:
    def __init__(self, name):
        self.name = name


class Manager(Employee):
    def __init__(self, name, team_size):
        super().__init__(name)
        self.team_size = team_size


manager = Manager("Harsha", 5)

print(manager.name)
print(manager.team_size)
```

Output:

```text
Harsha
5
```

---

# 40. Coding Question — Multiple Inheritance

### Question

Create a class that inherits from two parent classes.

### Solution

```python
class Father:
    def father_skill(self):
        print("Driving")


class Mother:
    def mother_skill(self):
        print("Cooking")


class Child(Father, Mother):
    pass


child = Child()

child.father_skill()
child.mother_skill()
```

Output:

```text
Driving
Cooking
```

---

# 41. Coding Question — Multilevel Inheritance

### Question

Create three classes representing `Animal`, `Dog`, and `Puppy` using multilevel inheritance.

### Solution

```python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


class Puppy(Dog):
    def play(self):
        print("Playing")


puppy = Puppy()

puppy.eat()
puppy.bark()
puppy.play()
```

Output:

```text
Eating
Barking
Playing
```

---

# 42. Important Interview Trap — Does Python Support Method Overloading?

### Answer

Python does not support traditional compile-time method overloading in the same way as languages such as Java.

If we define the same method multiple times in a class, the later definition replaces the earlier one.

Instead, Python commonly uses:

- Default arguments
- Variable-length arguments
- `*args`
- `**kwargs`

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

This provides overloading-like behavior using default arguments.

---

# 43. Inheritance and Polymorphism

Inheritance is often used together with polymorphism.

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

Both objects share the same interface, `sound()`, but provide different implementations.

---

# 44. Key Points to Remember

```text
Inheritance
    ↓
Child class reuses parent functionality
    ↓
Promotes code reuse
    ↓
Represents IS-A relationships
```

### Parent

```text
Base class
Superclass
```

### Child

```text
Derived class
Subclass
```

### Common Types

```text
Single
Multiple
Multilevel
Hierarchical
Hybrid
```

### Important Concepts

```text
Method overriding
super()
MRO
Diamond problem
IS-A vs HAS-A
Inheritance vs Composition
```

### Easy Revision

```text
Inheritance → Reuse parent functionality

super() → Access parent functionality

MRO → Method lookup order

Overriding → Child changes inherited behavior

IS-A → Inheritance

HAS-A → Composition
```

# Frequently Asked Interview Questions

1. What is inheritance?
2. Why do we use inheritance?
3. What is a parent class?
4. What is a child class?
5. How do you implement inheritance in Python?
6. What are the types of inheritance?
7. What is single inheritance?
8. What is multiple inheritance?
9. What is multilevel inheritance?
10. What is hierarchical inheritance?
11. What is hybrid inheritance?
12. What is method overriding?
13. Why is method overriding useful?
14. What is `super()`?
15. Why do we use `super().__init__()`?
16. What happens if a child class doesn't define `__init__()`?
17. What happens if both parent and child have `__init__()`?
18. Does Python support multiple inheritance?
19. What problems can occur with multiple inheritance?
20. What is MRO?
21. How can you check MRO?
22. What is the diamond problem?
23. How does Python solve the diamond problem?
24. What is an `is-a` relationship?
25. What is a `has-a` relationship?
26. What is the difference between inheritance and composition?
27. Is inheritance always better than composition?
28. Does Python support method overloading?
29. How can we achieve overloading-like behavior in Python?
30. How are inheritance and polymorphism related?
31. Write a program for single inheritance.
32. Write a program for multiple inheritance.
33. Write a program for multilevel inheritance.
34. Write a program demonstrating method overriding.
35. Write a program using `super()`.