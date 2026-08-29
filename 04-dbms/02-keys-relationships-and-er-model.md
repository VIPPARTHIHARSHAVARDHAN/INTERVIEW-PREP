# Keys, Relationships and ER Model

## 1. What is a Key in DBMS?

A **key** is an attribute or a combination of attributes used to identify records in a table or establish relationships between tables.

Example:

```text
STUDENTS

+------------+--------+-----+
| student_id | name   | age |
+------------+--------+-----+
| 101        | Ravi   | 22  |
| 102        | Priya  | 21  |
| 103        | Arun   | 23  |
+------------+--------+-----+
```

Here, `student_id` can uniquely identify each student.

---

# 2. Why are Keys Important?

Keys are used to:

- Uniquely identify records
- Prevent duplicate records
- Establish relationships between tables
- Maintain data integrity
- Enforce constraints
- Connect related data

Example:

```text
Students
    |
    | student_id
    ↓
Orders
```

A student's ID can be used to connect the student with their orders.

---

# 3. Types of Keys

The important keys for interviews are:

1. Super Key
2. Candidate Key
3. Primary Key
4. Alternate Key
5. Foreign Key
6. Composite Key

---

# 4. What is a Super Key?

A **super key** is any attribute or combination of attributes that can uniquely identify a row in a table.

Example:

```text
STUDENTS

student_id | email              | name
-----------|--------------------|------
101        | ravi@gmail.com     | Ravi
102        | priya@gmail.com    | Priya
103        | arun@gmail.com     | Arun
```

Possible super keys include:

```text
{student_id}
{email}
{student_id, name}
{student_id, email}
{email, name}
{student_id, email, name}
```

As long as the combination uniquely identifies a row, it can be a super key.

### Important Point

A super key may contain **extra attributes**.

For example:

```text
{student_id, name}
```

can uniquely identify a student, but `name` is unnecessary because `student_id` alone is sufficient.

---

# 5. What is a Candidate Key?

A **candidate key** is a minimal super key.

It uniquely identifies a row and contains **no unnecessary attributes**.

Using the previous example:

```text
student_id
email
```

can each uniquely identify a student.

Therefore:

```text
Candidate Keys:
{student_id}
{email}
```

### Important Difference

```text
Super Key
→ Can contain unnecessary attributes

Candidate Key
→ Minimal super key
```

---

# 6. What is a Primary Key?

A **primary key** is the candidate key selected to uniquely identify each row in a table.

Example:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(100)
);
```

Here:

```text
student_id
```

is the primary key.

### Properties

A primary key:

- Must uniquely identify each row
- Cannot contain `NULL`
- Should be stable
- There can be only one primary key constraint per table
- It can consist of one or multiple columns

---

# 7. Can a Table Have Multiple Primary Keys?

No.

A table can have **only one primary key constraint**.

However, that primary key can contain multiple columns.

Example:

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

Here there is one primary key constraint consisting of two columns.

This is called a **composite primary key**.

---

# 8. What is an Alternate Key?

An **alternate key** is a candidate key that was not selected as the primary key.

Example:

```text
Candidate Keys:

student_id
email
```

Suppose:

```text
student_id → Primary Key
email      → Alternate Key
```

So:

> Every alternate key is a candidate key, but it was not selected as the primary key.

---

# 9. What is a Foreign Key?

A **foreign key** is a column or set of columns in one table that references a key in another table, commonly the primary key.

Example:

### Students

```text
student_id | name
-----------|------
101        | Ravi
102        | Priya
```

### Orders

```text
order_id | student_id | amount
---------|------------|-------
1        | 101        | 500
2        | 102        | 700
```

Here:

```text
Students.student_id
        ↑
        |
Orders.student_id
```

`Orders.student_id` can be a foreign key referencing `Students.student_id`.

### SQL Example

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    student_id INT,
    amount DECIMAL(10,2),

    FOREIGN KEY (student_id)
        REFERENCES students(student_id)
);
```

---

# 10. Why is a Foreign Key Used?

Foreign keys are mainly used to:

- Establish relationships between tables
- Maintain referential integrity
- Prevent invalid references

For example, if `student_id = 101` does not exist in the `students` table, the database can prevent inserting an order referencing that nonexistent student, depending on the constraint and operation.

---

# 11. What is Referential Integrity?

**Referential integrity** ensures that a foreign key value correctly refers to an existing referenced key, subject to the rules defined by the database.

Example:

```text
Students
student_id
----------
101
102
```

An order with:

```text
student_id = 101
```

is valid because student 101 exists.

But:

```text
student_id = 999
```

would violate referential integrity if student 999 does not exist and the foreign key constraint does not allow the operation.

---

# 12. What is a Composite Key?

A **composite key** is a key consisting of two or more columns.

Example:

```text
ENROLLMENT

student_id | course_id
-----------|----------
101        | 10
101        | 20
102        | 10
```

Neither `student_id` nor `course_id` alone uniquely identifies an enrollment.

But:

```text
(student_id, course_id)
```

can uniquely identify an enrollment.

### SQL Example

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id)
);
```

---

# 13. Super Key vs Candidate Key vs Primary Key

| Key | Meaning |
|---|---|
| Super Key | Any set of attributes that uniquely identifies a row |
| Candidate Key | Minimal super key |
| Primary Key | Candidate key selected to identify rows |
| Alternate Key | Candidate key not selected as primary key |

### Easy Memory Trick

```text
Super Key
   ↓ remove unnecessary attributes
Candidate Key
   ↓ select one
Primary Key

Remaining candidate keys
   ↓
Alternate Keys
```

---

# 14. Primary Key vs Foreign Key

| Primary Key | Foreign Key |
|---|---|
| Identifies rows in its table | References a key in another table |
| Must be unique | Can contain duplicate values |
| Cannot be NULL | May allow NULL depending on definition |
| One primary key constraint per table | A table can have multiple foreign keys |
| Maintains entity identity | Helps maintain referential integrity |

---

# 15. Can a Foreign Key Have Duplicate Values?

Yes.

Example:

```text
STUDENTS

student_id
----------
101
102

ORDERS

order_id | student_id
---------|-----------
1        | 101
2        | 101
3        | 102
```

Student `101` has multiple orders.

Therefore:

```text
student_id = 101
student_id = 101
```

can appear multiple times in the child table.

---

# 16. Can a Foreign Key Be NULL?

Yes, a foreign key can be `NULL` if the column allows `NULL` and the database operation satisfies the applicable constraints.

Example:

```text
employee_id | manager_id
------------|----------
101         | NULL
102         | 101
103         | 101
```

Employee 101 may have no manager.

---

# 17. What is a Relationship in DBMS?

A **relationship** represents an association between entities.

Example:

```text
Student ───── enrolls in ───── Course
```

A student can enroll in a course.

Another example:

```text
Customer ───── places ───── Order
```

---

# 18. What is an Entity?

An **entity** is a distinguishable real-world object or concept about which data is stored.

Examples:

- Student
- Employee
- Customer
- Product
- Order
- Department

For example:

```text
Student
```

can be an entity.

Individual students are entity instances:

```text
Ravi
Priya
Arun
```

---

# 19. What is an Attribute?

An **attribute** describes a property of an entity.

Example:

```text
Student
 ├── student_id
 ├── name
 ├── age
 └── email
```

Here:

```text
student_id
name
age
email
```

are attributes of the Student entity.

---

# 20. What is an Entity Set?

An **entity set** is a collection of similar entities.

Example:

```text
Student Entity Set

Ravi
Priya
Arun
Kiran
```

All these students belong to the same entity set.

---

# 21. What is an ER Model?

**ER (Entity-Relationship) Model** is a conceptual model used to represent:

- Entities
- Attributes
- Relationships

before implementing the database.

Example:

```text
+----------+       enrolls       +----------+
| STUDENT  | ------------------- | COURSE   |
+----------+                     +----------+
| student_id|                    | course_id|
| name      |                    | name     |
+----------+                     +----------+
```

The ER model helps us understand the database structure before creating tables.

---

# 22. What is an ER Diagram?

An **ER diagram** is a graphical representation of an ER model.

It shows:

- Entities
- Attributes
- Relationships
- Cardinality

A simplified representation:

```text
[STUDENT] -------- enrolls -------- [COURSE]
```

---

# 23. Common ER Diagram Symbols

Traditional ER diagrams commonly use:

```text
Rectangle → Entity

Oval      → Attribute

Diamond   → Relationship
```

Example:

```text
             (name)
                |
                |
          +-----------+
          |  STUDENT  |
          +-----------+
```

A relationship is traditionally represented using a diamond:

```text
+---------+       ◇ ENROLLS ◇       +---------+
| STUDENT | ----------------------- | COURSE  |
+---------+                         +---------+
```

Different ER diagram notations may use different visual conventions, but the concepts remain the same.

---

# 24. What is Cardinality?

**Cardinality** describes how many instances of one entity can be associated with instances of another entity.

The major types are:

1. One-to-One
2. One-to-Many
3. Many-to-One
4. Many-to-Many

---

# 25. One-to-One Relationship (1:1)

In a one-to-one relationship, one entity instance is associated with at most one instance of another entity, and vice versa, under the relationship constraints.

Example:

```text
Person ───── Passport
```

A person may have one passport, and a passport belongs to one person in a simplified model.

```text
PERSON 1 ───────── 1 PASSPORT
```

---

# 26. One-to-Many Relationship (1:N)

In a one-to-many relationship, one entity can be associated with many instances of another entity.

Example:

```text
Department ───── Employees
```

One department can have many employees.

```text
DEPARTMENT 1 ───────── N EMPLOYEES
```

Example:

```text
Department 10
     |
     +── Employee 101
     +── Employee 102
     +── Employee 103
```

---

# 27. Many-to-One Relationship (N:1)

Many-to-one is the reverse direction of one-to-many.

Example:

```text
Employees ───── Department
```

Many employees can belong to one department.

```text
EMPLOYEES N ───────── 1 DEPARTMENT
```

### Important

These describe the same relationship from opposite directions:

```text
Department → Employees = 1:N

Employees → Department = N:1
```

---

# 28. Many-to-Many Relationship (M:N)

In a many-to-many relationship, many instances of one entity can be associated with many instances of another entity.

Example:

```text
STUDENT ↔ COURSE
```

One student can take multiple courses.

One course can have multiple students.

```text
STUDENT M ───────── N COURSE
```

---

# 29. How is Many-to-Many Implemented in a Relational Database?

A many-to-many relationship is usually implemented using a **junction/associative table**.

Example:

```text
STUDENT
---------
student_id
name

COURSE
---------
course_id
course_name

ENROLLMENT
----------
student_id
course_id
```

Relationship:

```text
STUDENT
   |
   | 1
   |
ENROLLMENT
   |
   | N
   |
COURSE
```

More accurately:

```text
STUDENT 1 ─── N ENROLLMENT N ─── 1 COURSE
```

### SQL Example

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50)
);

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
);

CREATE TABLE enrollment (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(student_id),

    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);
```

---

# 30. What is Participation Constraint?

Participation specifies whether every entity instance must participate in a relationship.

There are two types:

1. Total participation
2. Partial participation

---

# 31. Total Participation

In **total participation**, every entity instance must participate in the relationship.

Example:

```text
Employee ───── works_for ───── Department
```

If the business rule requires every employee to belong to a department, then employee participation is total.

Conceptually:

```text
Every Employee
      ↓
Must participate
      ↓
Works for a Department
```

---

# 32. Partial Participation

In **partial participation**, participation is optional for some entity instances.

Example:

```text
Employee ───── manages ───── Department
```

Not every employee needs to manage a department.

Therefore, employee participation in the `manages` relationship can be partial.

---

# 33. Total vs Partial Participation

| Total Participation | Partial Participation |
|---|---|
| Every entity must participate | Participation is optional for some entities |
| Mandatory | Optional |
| Example: every employee must belong to a department | Example: not every employee manages a department |

---

# 34. What is a Weak Entity?

A **weak entity** is an entity that cannot be uniquely identified by its own attributes alone and depends on another entity, called the owner/strong entity, for identification.

Example:

```text
EMPLOYEE
employee_id
name

DEPENDENT
dependent_name
age
```

A dependent may be identified using:

```text
employee_id + dependent_name
```

because `dependent_name` alone may not be unique across all employees.

---

# 35. Strong Entity vs Weak Entity

| Strong Entity | Weak Entity |
|---|---|
| Can be identified independently | Depends on an owner entity |
| Has its own identifying key | Uses owner's key with its partial key |
| Independent existence in the model | Existence depends on owner |
| Example: Employee | Example: Dependent |

---

# 36. What is a Partial Key?

A **partial key** is an attribute of a weak entity that distinguishes weak entity instances belonging to the same owner.

Example:

```text
Employee ID = 101

Dependents:
Child
Spouse
```

`dependent_name` may distinguish dependents for one employee, but it may not uniquely identify a dependent across the entire database.

Therefore:

```text
Employee_ID + Dependent_Name
```

can identify the weak entity.

---

# 37. What is a Recursive Relationship?

A **recursive relationship** is a relationship where an entity is related to itself.

Example:

```text
EMPLOYEE
   |
   | manages
   ↓
EMPLOYEE
```

One employee can manage another employee.

Example:

```text
Employee 101 → manages → Employee 102
Employee 101 → manages → Employee 103
```

The same entity participates in different roles.

---

# 38. What is a Unary Relationship?

A **unary relationship** is a relationship involving one entity type.

A recursive relationship is a common example.

```text
EMPLOYEE
   ↘
   manages
   ↙
EMPLOYEE
```

---

# 39. What is a Binary Relationship?

A **binary relationship** involves two entity types.

Example:

```text
STUDENT ───── enrolls ───── COURSE
```

There are two entity types:

```text
Student
Course
```

---

# 40. What is a Ternary Relationship?

A **ternary relationship** involves three entity types.

Example:

```text
Supplier
    \
     \
     Supplies
     /      \
 Product    Project
```

The relationship may represent:

```text
Supplier supplies Product to Project
```

Ternary relationships are less commonly discussed in basic interviews but are useful to recognize.

---

# 41. What is an Associative Entity?

An **associative entity** is used to represent a relationship, especially a many-to-many relationship, as an entity/table.

Example:

```text
STUDENT
   |
   |
ENROLLMENT
   |
   |
COURSE
```

`ENROLLMENT` can contain additional relationship attributes:

```text
student_id
course_id
enrollment_date
grade
```

This is useful because the relationship itself has data.

---

# 42. Entity vs Attribute

| Entity | Attribute |
|---|---|
| Represents an object/concept | Describes a property |
| Can have attributes | Describes an entity |
| Example: Student | Example: Name |
| Example: Employee | Example: Salary |

Example:

```text
Student
  |
  +── student_id
  +── name
  +── age
```

`Student` = entity

`student_id`, `name`, `age` = attributes

---

# 43. Entity vs Relationship

| Entity | Relationship |
|---|---|
| Represents an object/concept | Represents an association |
| Example: Student | Example: Enrolls |
| Example: Course | Example: Teaches |

Example:

```text
STUDENT ───── enrolls ───── COURSE
```

Here:

```text
Student → Entity
Course  → Entity
Enrolls → Relationship
```

---

# 44. Key Concepts to Remember

```text
Super Key
→ Any unique-identifying attribute set

Candidate Key
→ Minimal super key

Primary Key
→ Selected candidate key

Alternate Key
→ Candidate key not selected as primary

Foreign Key
→ References a key in another table

Composite Key
→ Key containing multiple columns

Entity
→ Real-world object/concept

Attribute
→ Property of an entity

Relationship
→ Association between entities

Cardinality
→ Number of entity instances participating in a relationship

ER Model
→ Conceptual model of entities, attributes, and relationships
```

---

# 45. Frequently Asked Interview Questions

## Q1. What is a key in DBMS?

### Answer

> A key is an attribute or combination of attributes used to uniquely identify records or establish relationships between tables.

---

## Q2. What is a super key?

### Answer

> A super key is an attribute or combination of attributes that uniquely identifies a row in a table. It may contain unnecessary attributes.

---

## Q3. What is a candidate key?

### Answer

> A candidate key is a minimal super key that uniquely identifies a row.

---

## Q4. What is a primary key?

### Answer

> A primary key is the candidate key selected to uniquely identify records in a table. It cannot contain NULL values.

---

## Q5. What is an alternate key?

### Answer

> An alternate key is a candidate key that was not selected as the primary key.

---

## Q6. What is a foreign key?

### Answer

> A foreign key is a column or set of columns that references a key in another table and is used to establish relationships and maintain referential integrity.

---

## Q7. What is a composite key?

### Answer

> A composite key is a key consisting of two or more columns used together to uniquely identify a record.

---

## Q8. Can a table have multiple candidate keys?

### Answer

> Yes. A table can have multiple candidate keys, but only one candidate key is selected as the primary key.

---

## Q9. Can a table have multiple primary keys?

### Answer

> No. A table can have only one primary key constraint, although that primary key can consist of multiple columns.

---

## Q10. Can a foreign key contain duplicate values?

### Answer

> Yes. A foreign key can contain duplicate values because multiple rows in the child table can reference the same parent row.

---

## Q11. Can a foreign key contain NULL?

### Answer

> Yes, if the foreign key column allows NULL and no other constraint prevents it.

---

## Q12. What is referential integrity?

### Answer

> Referential integrity ensures that foreign key references remain valid according to the relationship constraints defined in the database.

---

## Q13. What is an entity?

### Answer

> An entity is a distinguishable real-world object or concept about which data is stored, such as Student, Employee, or Product.

---

## Q14. What is an attribute?

### Answer

> An attribute is a property that describes an entity, such as student_id, name, or age.

---

## Q15. What is an ER model?

### Answer

> An ER model is a conceptual model used to represent entities, their attributes, and relationships before implementing the database.

---

## Q16. What is an ER diagram?

### Answer

> An ER diagram is a graphical representation of entities, attributes, relationships, and their constraints.

---

## Q17. What is cardinality?

### Answer

> Cardinality describes how many instances of one entity can be associated with instances of another entity.

---

## Q18. What are the types of cardinality?

### Answer

The common types are:

- One-to-One
- One-to-Many
- Many-to-One
- Many-to-Many

---

## Q19. What is a one-to-one relationship?

### Answer

> In a one-to-one relationship, one entity instance is associated with at most one instance of the other entity, and vice versa, according to the relationship constraints.

Example:

```text
Person 1 ───── 1 Passport
```

---

## Q20. What is a one-to-many relationship?

### Answer

> In a one-to-many relationship, one instance of an entity can be associated with multiple instances of another entity.

Example:

```text
Department 1 ───── N Employees
```

---

## Q21. What is a many-to-many relationship?

### Answer

> In a many-to-many relationship, multiple instances of one entity can be associated with multiple instances of another entity.

Example:

```text
Student M ───── N Course
```

---

## Q22. How do you implement a many-to-many relationship in SQL?

### Answer

> We normally create a junction or associative table containing foreign keys referencing the two related tables.

Example:

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,

    PRIMARY KEY (student_id, course_id),

    FOREIGN KEY (student_id)
        REFERENCES students(student_id),

    FOREIGN KEY (course_id)
        REFERENCES courses(course_id)
);
```

---

## Q23. What is a weak entity?

### Answer

> A weak entity is an entity that cannot be uniquely identified by its own attributes alone and depends on an owner entity for identification.

---

## Q24. What is a strong entity?

### Answer

> A strong entity can be uniquely identified using its own key and does not depend on another entity for identification.

---

## Q25. What is total participation?

### Answer

> Total participation means every entity instance must participate in a particular relationship.

---

## Q26. What is partial participation?

### Answer

> Partial participation means participation in a relationship is optional for some entity instances.

---

## Q27. What is a recursive relationship?

### Answer

> A recursive relationship is a relationship where an entity is related to itself.

Example:

```text
Employee ─── manages ─── Employee
```

---

## Q28. What is the difference between a primary key and a unique key?

### Answer

> A primary key is the main key selected to identify rows in a table and cannot contain NULL values. A UNIQUE constraint ensures uniqueness for its constrained column or columns; its treatment of NULL depends on the DBMS.

---

## Q29. What is the difference between a candidate key and a primary key?

### Answer

> Candidate keys are all minimal keys capable of uniquely identifying a row. The primary key is the candidate key selected for primary identification.

---

## Q30. What is the difference between a super key and a candidate key?

### Answer

> A super key can contain unnecessary attributes, while a candidate key is a minimal super key.

Example:

```text
student_id
```

can be a candidate key.

```text
student_id + name
```

can be a super key, but it is not minimal.

---

# 46. Scenario-Based Interview Questions

## Scenario 1: Student and Course

You have:

```text
Students
Courses
```

A student can enroll in multiple courses, and each course can have multiple students.

### Question

What type of relationship exists?

### Answer

```text
Many-to-Many
```

It should normally be implemented using an intermediate table:

```text
Enrollment
```

---

## Scenario 2: Department and Employees

One department can have many employees, but each employee belongs to one department.

### Question

What is the relationship?

### Answer

```text
Department 1 ───── N Employee
```

This is a **one-to-many relationship**.

---

## Scenario 3: Employee and Manager

An employee can manage other employees.

### Question

What type of relationship is this?

### Answer

A **recursive relationship** because the Employee entity is related to itself.

```text
Employee ─── manages ─── Employee
```

---

## Scenario 4: Enrollment Table

Suppose:

```text
student_id
course_id
```

together uniquely identify each enrollment.

### Question

What type of key can be used?

### Answer

A **composite key**:

```text
(student_id, course_id)
```

---

## Scenario 5: Multiple Candidate Keys

Suppose:

```text
student_id
email
```

are both unique and minimal.

### Question

What are they?

### Answer

Both are **candidate keys**.

If `student_id` is selected as the primary key:

```text
student_id → Primary Key
email      → Alternate Key
```

---

# 47. Final Interview Revision

Before an interview, make sure you can explain these without memorizing long definitions:

```text
1. What is a key?
2. What is a super key?
3. What is a candidate key?
4. What is a primary key?
5. What is an alternate key?
6. What is a foreign key?
7. What is a composite key?
8. Primary key vs foreign key
9. Super key vs candidate key
10. Candidate key vs primary key
11. What is referential integrity?
12. What is an entity?
13. What is an attribute?
14. What is a relationship?
15. What is an ER model?
16. What is an ER diagram?
17. What is cardinality?
18. What are 1:1, 1:N, N:1, and M:N relationships?
19. How is M:N implemented in relational databases?
20. What is a weak entity?
21. What is a strong entity?
22. What is total participation?
23. What is partial participation?
24. What is a recursive relationship?
25. What is an associative entity?
```

# 48. One-Minute Memory Sheet

```text
KEYS
────
Super Key
→ Unique identification, may contain extra attributes

Candidate Key
→ Minimal Super Key

Primary Key
→ Selected Candidate Key

Alternate Key
→ Candidate Key not selected as Primary

Foreign Key
→ References a key in another table

Composite Key
→ Multiple columns together form a key


ER MODEL
────────
Entity
→ Object/concept

Attribute
→ Property of entity

Relationship
→ Association between entities

Cardinality
→ How many entities participate

1:1
→ One-to-One

1:N
→ One-to-Many

N:1
→ Many-to-One

M:N
→ Many-to-Many


IMPORTANT
─────────
M:N relationship
→ Usually implemented using a junction/associative table

Foreign Key
→ Maintains referential integrity

Weak Entity
→ Depends on owner entity for identification

Recursive Relationship
→ Entity related to itself

Total Participation
→ Mandatory participation

Partial Participation
→ Optional participation
```