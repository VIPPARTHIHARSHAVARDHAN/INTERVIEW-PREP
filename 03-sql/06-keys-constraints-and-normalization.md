# SQL Keys, Constraints and Normalization

## 1. Why This Topic Is Important

Keys, constraints, and normalization are important SQL/database interview topics because they test whether you understand how databases maintain:

- Data uniqueness
- Data integrity
- Relationships between tables
- Valid data
- Duplicate prevention
- Database design
- Reducing unnecessary data duplication

For interviews, you should especially know:

```text
Primary Key
Foreign Key
Candidate Key
Super Key
Alternate Key
Composite Key
UNIQUE
NOT NULL
CHECK
DEFAULT
Referential Integrity
Normalization
1NF
2NF
3NF
BCNF
Denormalization
```

---

# 2. What Is a Key?

A **key** is a column or combination of columns used to identify rows or establish relationships between tables.

Example:

```sql
CREATE TABLE employees (
    employee_id INT,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

Here:

```text
employee_id
```

can be used as a key if every employee has a unique ID.

---

# 3. Why Are Keys Important?

Keys help us:

- Uniquely identify records
- Prevent duplicate records
- Establish relationships between tables
- Maintain data integrity
- Retrieve specific records efficiently
- Define relationships between parent and child tables

---

# 4. Primary Key

A **primary key** uniquely identifies each row in a table.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

Here:

```text
employee_id
```

is the primary key.

---

# 5. Properties of a Primary Key

A primary key:

- Must uniquely identify each row
- Cannot contain `NULL`
- A table can have only one primary key constraint
- Can consist of one column or multiple columns
- Is commonly used as the target of foreign-key relationships

Example:

```sql
employee_id INT PRIMARY KEY
```

---

# 6. Can a Primary Key Contain NULL?

No.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

This is invalid:

```sql
INSERT INTO employees
VALUES (NULL, 'Rahul');
```

A primary key must identify a row, so it cannot be `NULL`.

---

# 7. Can a Table Have Multiple Primary Keys?

A table can have only **one primary key constraint**.

However, that primary key can contain multiple columns.

This is called a:

```text
Composite Primary Key
```

Example:

```sql
CREATE TABLE student_courses (
    student_id INT,
    course_id INT,
    enrollment_date DATE,

    PRIMARY KEY (student_id, course_id)
);
```

The combination:

```text
student_id + course_id
```

uniquely identifies an enrollment.

---

# 8. Composite Key

A **composite key** consists of two or more columns that together identify a row.

Example:

```sql
CREATE TABLE order_items (
    order_id INT,
    product_id INT,
    quantity INT,

    PRIMARY KEY (order_id, product_id)
);
```

Neither column may be unique by itself.

But:

```text
order_id + product_id
```

together can uniquely identify an order item.

---

# 9. Candidate Key

A **candidate key** is a minimal set of columns that can uniquely identify a row.

Suppose:

```text
employee_id
email
phone_number
```

are all guaranteed to be unique.

Then each could potentially be a candidate key.

Example:

```text
employee_id → Candidate Key
email       → Candidate Key
phone       → Candidate Key
```

One candidate key is selected as the primary key.

---

# 10. Alternate Key

Candidate keys that are **not selected as the primary key** are called alternate keys.

Example:

```text
employee_id → Primary Key
email       → Alternate Key
phone       → Alternate Key
```

assuming all three are candidate keys.

---

# 11. Super Key

A **super key** is any set of one or more columns that can uniquely identify a row.

Example:

```text
employee_id
```

can uniquely identify an employee.

So:

```text
{employee_id}
```

is a super key.

If `employee_id` is already unique, then:

```text
{employee_id, name}
```

is also a super key because it still uniquely identifies the row.

However, it is not minimal.

---

# 12. Super Key vs Candidate Key

This is a common interview question.

### Super Key

Can uniquely identify a row but may contain unnecessary columns.

### Candidate Key

Is a **minimal super key**.

Example:

```text
employee_id
```

uniquely identifies an employee.

Then:

```text
{employee_id}
```

is a candidate key.

And:

```text
{employee_id, name}
```

is a super key but not a candidate key because `name` is unnecessary.

---

# 13. Primary Key vs Candidate Key

Suppose:

```text
employee_id
email
```

are both unique.

Then:

```text
employee_id → Candidate Key
email       → Candidate Key
```

If we choose:

```text
employee_id
```

as the primary key:

```text
employee_id → Primary Key
email       → Alternate Key
```

So:

> A primary key is the candidate key selected to uniquely identify records.

---

# 14. Foreign Key

A **foreign key** is a column or set of columns used to establish a relationship between tables.

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Here:

```text
departments.department_id
```

is the parent key.

```text
employees.department_id
```

is the foreign key.

---

# 15. Why Do We Use Foreign Keys?

Foreign keys help maintain **referential integrity**.

They prevent a child record from referencing a parent record that does not exist, subject to the database's constraints and actions.

Example:

```text
Department 10 exists
Employee → department_id = 10
```

is valid.

But:

```text
Department 999 does not exist
Employee → department_id = 999
```

would violate the foreign-key constraint.

---

# 16. Parent Table and Child Table

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);
```

This is the:

```text
Parent table
```

Then:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This is the:

```text
Child table
```

The child table contains the foreign key.

---

# 17. Can a Foreign Key Contain NULL?

Yes, unless another constraint such as `NOT NULL` prevents it.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

If `department_id` is nullable, an employee can have:

```text
department_id = NULL
```

This means the employee is not currently associated with a department.

If every employee must have a department:

```sql
department_id INT NOT NULL,
FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
```

---

# 18. UNIQUE Constraint

`UNIQUE` ensures that values in a column or combination of columns are not duplicated.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

Two employees cannot have the same email value.

---

# 19. PRIMARY KEY vs UNIQUE

This is a very common interview question.

| Feature | PRIMARY KEY | UNIQUE |
|---|---|---|
| Uniqueness | Yes | Yes |
| NULL allowed | No | DBMS-dependent behavior; commonly one or more NULLs may be allowed |
| Number per table | One primary-key constraint | Multiple UNIQUE constraints allowed |
| Main purpose | Row identification | Enforce uniqueness |

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20) UNIQUE
);
```

Here:

```text
employee_id → Primary Key
email       → Unique
phone       → Unique
```

---

# 20. NOT NULL Constraint

`NOT NULL` ensures that a column must contain a value.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

This is invalid:

```sql
INSERT INTO employees(employee_id, name)
VALUES (1, NULL);
```

---

# 21. CHECK Constraint

`CHECK` ensures that values satisfy a condition.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    age INT CHECK (age >= 18)
);
```

This should not be allowed:

```sql
INSERT INTO employees
VALUES (1, 15);
```

because:

```text
15 < 18
```

---

# 22. CHECK Constraint Example with Salary

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    salary DECIMAL(10,2)
        CHECK (salary >= 0)
);
```

This prevents negative salary values.

---

# 23. DEFAULT Constraint

`DEFAULT` provides a value when no value is supplied for that column.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    status VARCHAR(20) DEFAULT 'Active'
);
```

Then:

```sql
INSERT INTO employees(employee_id, name)
VALUES (1, 'Rahul');
```

The status can automatically become:

```text
Active
```

---

# 24. Common SQL Constraints

The major constraints you should know are:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# 25. Example Using Multiple Constraints

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 18),
    salary DECIMAL(10,2) CHECK (salary >= 0),
    status VARCHAR(20) DEFAULT 'Active',
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This demonstrates several important constraints together.

---

# 26. Referential Integrity

**Referential integrity** ensures that relationships between related tables remain valid.

Example:

```text
departments
-----------
department_id
10
20
```

```text
employees
---------
employee_id | department_id
1           | 10
2           | 20
```

Both employee references are valid because departments `10` and `20` exist.

But:

```text
employee_id | department_id
3           | 99
```

would be invalid if department `99` does not exist.

---

# 27. ON DELETE CASCADE

Suppose:

```text
Department
   ↓
Employees
```

If a department is deleted, you may want its employees to be deleted automatically.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
        ON DELETE CASCADE
);
```

Then deleting a department can automatically delete related employee rows.

### Interview Warning

`CASCADE` should be used carefully because deleting a parent can cause many child rows to be deleted.

---

# 28. ON DELETE SET NULL

Another option is:

```sql
FOREIGN KEY (department_id)
    REFERENCES departments(department_id)
    ON DELETE SET NULL
```

If the parent department is deleted, the child foreign-key value becomes:

```text
NULL
```

The foreign-key column must allow `NULL`.

---

# 29. ON DELETE RESTRICT / NO ACTION

A restrictive foreign-key action can prevent deleting the parent while dependent child rows exist.

Conceptually:

```text
Parent has child records
        ↓
Attempt to delete parent
        ↓
Deletion prevented
```

The exact supported action and behavior can vary by database system.

---

# 30. What Happens If We Delete a Parent Row Referenced by a Foreign Key?

The result depends on the foreign-key action.

Common possibilities include:

```text
CASCADE
SET NULL
RESTRICT
NO ACTION
```

Without an appropriate action, the database generally prevents deleting the referenced parent row when doing so would violate referential integrity.

---

# 31. What Is Normalization?

**Normalization** is the process of organizing data into tables to reduce unnecessary duplication and improve data integrity.

The main goals are:

- Reduce redundancy
- Avoid update anomalies
- Avoid insertion anomalies
- Avoid deletion anomalies
- Improve data consistency

---

# 32. Why Is Normalization Needed?

Suppose we have:

| student_id | student_name | course | instructor |
|---:|---|---|---|
| 1 | Rahul | SQL | Arun |
| 1 | Rahul | Python | Priya |
| 2 | Sneha | SQL | Arun |

The student's name is repeated.

If Rahul's name needs to be changed, multiple rows may need updating.

This creates unnecessary duplication.

Normalization helps separate related information into appropriate tables.

---

# 33. Data Anomalies

Poorly designed tables can cause:

```text
Insertion Anomaly
Update Anomaly
Deletion Anomaly
```

These are very important normalization interview concepts.

---

# 34. Insertion Anomaly

An insertion anomaly occurs when you cannot insert some information without also inserting unrelated information.

Example:

Suppose a table stores:

```text
Student + Course + Instructor
```

If you want to add a new course before any student enrolls in it, you may have no appropriate place to store the course information without inserting unnecessary student information.

Normalization can separate:

```text
Students
Courses
Enrollments
```

---

# 35. Update Anomaly

An update anomaly occurs when the same piece of information is stored in multiple rows and must be updated in multiple places.

Example:

| student_id | student_name | course |
|---:|---|---|
| 1 | Rahul | SQL |
| 1 | Rahul | Python |

If Rahul's name changes, multiple records contain the same information.

If one row is updated and another is not, inconsistent data can result.

---

# 36. Deletion Anomaly

A deletion anomaly occurs when deleting one piece of information unintentionally removes another important piece of information.

Example:

Suppose:

| student | course |
|---|---|
| Rahul | SQL |
| Sneha | Python |

If Rahul is the only student enrolled in SQL and we delete Rahul's row, we may also lose the only record showing that the SQL course exists.

Separating course information avoids this problem.

---

# 37. First Normal Form — 1NF

A table is in **First Normal Form (1NF)** when each field contains a single atomic value and repeating groups are avoided.

Bad design:

| student_id | name | phone_numbers |
|---:|---|---|
| 1 | Rahul | 9876, 8765 |

The `phone_numbers` field contains multiple values.

A better design could be:

| student_id | name | phone |
|---:|---|---|
| 1 | Rahul | 9876 |
| 1 | Rahul | 8765 |

Or, if phone numbers are independent entities, a separate phone table can be used.

---

# 38. 1NF Example

### Not in 1NF

```text
Student
-------------------------
student_id | phones
1          | 9876, 8765
```

### In 1NF

```text
StudentPhones
-------------------------
student_id | phone
1          | 9876
1          | 8765
```

Each field contains a single value.

---

# 39. Second Normal Form — 2NF

A table is in **2NF** when:

1. It is already in 1NF.
2. Every non-key attribute is fully dependent on the entire candidate key.

2NF mainly matters when the key is **composite**.

---

# 40. Partial Dependency

Suppose:

```text
(student_id, course_id)
```

is the composite key.

And the table contains:

```text
student_id
course_id
student_name
course_name
grade
```

Dependencies:

```text
student_id → student_name
course_id → course_name
(student_id, course_id) → grade
```

`student_name` depends only on `student_id`.

`course_name` depends only on `course_id`.

Therefore, they do not depend on the complete composite key.

This is a **partial dependency**.

---

# 41. Converting a Table to 2NF

Instead of:

```text
Enrollment
--------------------------------------
student_id
course_id
student_name
course_name
grade
```

Separate the data:

```text
Students
-------------------
student_id
student_name
```

```text
Courses
-------------------
course_id
course_name
```

```text
Enrollments
-------------------
student_id
course_id
grade
```

Now:

```text
student_name
```

depends on the student.

```text
course_name
```

depends on the course.

```text
grade
```

depends on the student-course relationship.

---

# 42. Third Normal Form — 3NF

A table is in **3NF** when:

1. It is in 2NF.
2. It has no problematic transitive dependency of non-key attributes on a key.

The simplified interview definition is:

> Every non-key attribute should depend on the key, the whole key, and nothing but the key.

---

# 43. Transitive Dependency

Consider:

```text
employee_id
employee_name
department_id
department_name
```

Suppose:

```text
employee_id → department_id
department_id → department_name
```

Therefore:

```text
employee_id → department_name
```

through `department_id`.

This is a transitive dependency.

---

# 44. Converting a Table to 3NF

Instead of:

```text
Employees
--------------------------------
employee_id
employee_name
department_id
department_name
```

Use:

```text
Employees
-------------------
employee_id
employee_name
department_id
```

and:

```text
Departments
-------------------
department_id
department_name
```

Now department information is stored in the department table.

---

# 45. BCNF

**BCNF** stands for:

```text
Boyce-Codd Normal Form
```

BCNF is a stronger version of 3NF.

A simplified definition:

> A relation is in BCNF if every determinant is a candidate key.

BCNF is more advanced than the basic 1NF/2NF/3NF concepts but is still a useful interview topic.

---

# 46. 1NF vs 2NF vs 3NF

| Normal Form | Main Idea |
|---|---|
| 1NF | Atomic values; no repeating groups |
| 2NF | 1NF + no partial dependency |
| 3NF | 2NF + no problematic transitive dependency |
| BCNF | Every determinant is a candidate key |

### Easy Memory Trick

```text
1NF
→ Atomic

2NF
→ Whole key

3NF
→ Nothing but the key
```

---

# 47. What Is a Functional Dependency?

A functional dependency describes a relationship where one attribute determines another.

Written as:

```text
A → B
```

This means:

> If we know A, we can determine B.

Example:

```text
employee_id → employee_name
```

If every employee ID is unique, knowing the employee ID determines the employee's name.

---

# 48. Functional Dependency Example

Consider:

```text
student_id → student_name
```

A student ID identifies one student.

Therefore:

```text
student_id
```

determines:

```text
student_name
```

---

# 49. Full Functional Dependency

Suppose the key is:

```text
(student_id, course_id)
```

and:

```text
(student_id, course_id) → grade
```

If `grade` depends on both columns together, it is fully functionally dependent on the composite key.

---

# 50. Partial Functional Dependency

Suppose:

```text
(student_id, course_id)
```

is the key and:

```text
student_id → student_name
```

Then `student_name` depends only on part of the composite key.

That is a:

```text
Partial Dependency
```

---

# 51. Transitive Dependency

Suppose:

```text
employee_id → department_id
department_id → department_name
```

Then:

```text
employee_id → department_name
```

This indirect dependency is called:

```text
Transitive Dependency
```

---

# 52. Normalization Example

Suppose we start with:

```text
Employee
----------------------------------------------------------------
employee_id | employee_name | department_id | department_name
```

Example:

```text
1 | Rahul | 10 | IT
2 | Priya | 10 | IT
3 | Arjun | 20 | HR
```

The department name is repeated.

---

# 53. Normalized Design

Create:

```text
Employees
--------------------------------
employee_id | employee_name | department_id
```

and:

```text
Departments
---------------------------
department_id | department_name
```

Example:

```text
Employees

1 | Rahul | 10
2 | Priya | 10
3 | Arjun | 20
```

```text
Departments

10 | IT
20 | HR
```

The relationship is established using:

```text
department_id
```

---

# 54. Benefits of Normalization

Normalization helps:

- Reduce duplicate data
- Improve consistency
- Reduce storage redundancy
- Prevent update anomalies
- Prevent insertion anomalies
- Prevent deletion anomalies
- Improve logical database design
- Make relationships clearer

---

# 55. Disadvantages of Excessive Normalization

Normalization is not always about creating as many tables as possible.

Highly normalized databases can require more joins.

This can sometimes make:

```text
Queries
Reports
Analytics
```

more complex.

For read-heavy systems, carefully chosen denormalization can sometimes improve performance.

---

# 56. What Is Denormalization?

**Denormalization** intentionally introduces some redundancy into a database to improve performance or simplify querying.

Example:

Instead of joining:

```text
Orders
Customers
Products
```

every time, some frequently accessed information may be duplicated in an appropriate design.

---

# 57. Normalization vs Denormalization

| Normalization | Denormalization |
|---|---|
| Reduces redundancy | May increase redundancy |
| Improves data consistency | Can simplify reads |
| Usually creates more related tables | May combine or duplicate data |
| More joins may be required | Fewer joins may be required |
| Common in transactional systems | Common in selected analytical/read-heavy designs |

---

# 58. Is Normalization Always Better?

No.

A good database design depends on the workload.

For transactional systems:

```text
Consistency
Integrity
Avoiding redundancy
```

are often major priorities.

For analytical systems:

```text
Read performance
Reporting
Simplified queries
```

may justify controlled denormalization.

---

# 59. Primary Key vs Foreign Key

| Primary Key | Foreign Key |
|---|---|
| Identifies rows in its own table | References a key in another table |
| Must be unique | Values can repeat |
| Cannot be NULL | Can be NULL unless constrained otherwise |
| One primary-key constraint per table | A table can have multiple foreign keys |
| Defines entity identity | Helps define relationships |

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

# 60. Primary Key vs UNIQUE

```text
PRIMARY KEY
→ Main identifier

UNIQUE
→ Prevent duplicate values
```

Example:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

Here:

```text
user_id → identifies user
email   → must be unique
```

---

# 61. Candidate Key vs Primary Key

```text
Candidate Keys
      ↓
Possible unique identifiers
      ↓
One is selected
      ↓
Primary Key
```

Other candidate keys become alternate keys.

---

# 62. Composite Primary Key vs Surrogate Key

A **surrogate key** is an artificial identifier created specifically to identify a row.

Example:

```sql
employee_id INT PRIMARY KEY
```

where `employee_id` has no business meaning.

A natural key may instead be something like:

```text
email
passport_number
```

if it is guaranteed to uniquely identify the entity and is appropriate for the domain.

---

# 63. Natural Key

A **natural key** is an attribute that naturally exists in the real-world data and can identify a record.

Examples could include:

```text
Email
Government-issued identifier
Product code
```

depending on the application.

---

# 64. Surrogate Key

A surrogate key is an artificial identifier.

Example:

```sql
employee_id INT PRIMARY KEY
```

The database may generate:

```text
1
2
3
4
```

These values exist primarily for identification rather than representing a business attribute.

---

# 65. Natural Key vs Surrogate Key

| Natural Key | Surrogate Key |
|---|---|
| Has business meaning | Usually has no business meaning |
| Comes from real-world data | Generated by the system |
| Can change in some domains | Usually stable |
| May be large/complex | Usually simple |
| Can be difficult to use in relationships | Often convenient for relationships |

The right choice depends on the application and data model.

---

# 66. Can a Foreign Key Reference a UNIQUE Key?

Yes, depending on the database system and constraints, a foreign key can reference a candidate/unique key, not only a primary key.

Example:

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

Another table may reference the unique email:

```sql
CREATE TABLE subscriptions (
    subscription_id INT PRIMARY KEY,
    user_email VARCHAR(100),

    FOREIGN KEY (user_email)
        REFERENCES users(email)
);
```

The exact requirements for referenced keys can vary by database system, but the referenced columns generally need an appropriate uniqueness constraint.

---

# 67. Can a Foreign Key Reference Another Table's Composite Key?

Yes.

Example:

```sql
CREATE TABLE course_offerings (
    course_id INT,
    semester_id INT,
    instructor VARCHAR(100),

    PRIMARY KEY (course_id, semester_id)
);
```

A child table can reference both columns:

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    semester_id INT,

    FOREIGN KEY (course_id, semester_id)
        REFERENCES course_offerings(course_id, semester_id)
);
```

The number and order of referenced columns must match the referenced key.

---

# 68. Can a Table Have Multiple Foreign Keys?

Yes.

Example:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    salesperson_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id),

    FOREIGN KEY (salesperson_id)
        REFERENCES employees(employee_id)
);
```

One table can contain multiple foreign keys.

---

# 69. Can a Table Have Multiple UNIQUE Constraints?

Yes.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(20) UNIQUE
);
```

Both:

```text
email
phone
```

must be unique.

---

# 70. Important Interview Question — What Is a Constraint?

### Strong Answer

> A constraint is a rule enforced by the database to control the validity and integrity of data stored in a table. Common constraints include PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL, CHECK, and DEFAULT.

---

# 71. Important Interview Question — What Is a Primary Key?

### Strong Answer

> A primary key is a column or combination of columns that uniquely identifies each row in a table. It cannot contain NULL values, and a table has one primary-key constraint, although that constraint can contain multiple columns.

---

# 72. Important Interview Question — What Is a Foreign Key?

### Strong Answer

> A foreign key is a column or combination of columns in one table that references a key in another table. It is primarily used to maintain referential integrity and establish relationships between tables.

---

# 73. Important Interview Question — What Is Normalization?

### Strong Answer

> Normalization is the process of organizing data into related tables to reduce unnecessary redundancy and prevent insertion, update, and deletion anomalies while improving data integrity.

---

# 74. Important Interview Question — Explain 1NF, 2NF and 3NF

### Strong Answer

> 1NF requires atomic values and no repeating groups. 2NF requires 1NF and removes partial dependencies on part of a composite key. 3NF requires 2NF and removes problematic transitive dependencies of non-key attributes.

---

# 75. Important Interview Question — What Is an Update Anomaly?

### Strong Answer

> An update anomaly occurs when the same piece of information is stored in multiple rows and changing it requires updating multiple records. If some rows are updated and others are not, inconsistent data can result.

---

# 76. Important Interview Question — What Is an Insertion Anomaly?

### Strong Answer

> An insertion anomaly occurs when a table's design prevents us from inserting information about one entity without also requiring unrelated information.

---

# 77. Important Interview Question — What Is a Deletion Anomaly?

### Strong Answer

> A deletion anomaly occurs when deleting one record unintentionally removes other useful information because multiple types of information were stored together in the same table.

---

# 78. Important Interview Question — What Is a Composite Key?

### Strong Answer

> A composite key is a key made up of two or more columns that together uniquely identify a row.

Example:

```sql
PRIMARY KEY (student_id, course_id)
```

---

# 79. Important Interview Question — What Is a Candidate Key?

### Strong Answer

> A candidate key is a minimal set of columns that can uniquely identify a row. One candidate key is selected as the primary key, while the remaining candidate keys can be considered alternate keys.

---

# 80. Important Interview Question — What Is a Super Key?

### Strong Answer

> A super key is any set of one or more columns that can uniquely identify a row. A candidate key is a minimal super key, meaning it contains no unnecessary attributes.

---

# 81. Important Interview Question — What Is Referential Integrity?

### Strong Answer

> Referential integrity ensures that a foreign-key value correctly references an existing parent key, unless the relationship allows NULL. It prevents invalid relationships between related tables.

---

# 82. Important Interview Question — Can a Foreign Key Have Duplicate Values?

Yes.

Example:

```text
department_id
10
10
10
20
20
```

Multiple employees can belong to the same department.

The foreign key does not need to be unique.

---

# 83. Important Interview Question — Can a Primary Key Have Duplicate Values?

No.

A primary key must uniquely identify each row.

This is invalid:

```text
employee_id
1
1
2
```

---

# 84. Important Interview Question — Can a UNIQUE Column Have NULL?

The exact behavior is database-dependent.

Many SQL databases allow `NULL` values in a `UNIQUE` column because `NULL` represents an unknown/non-value and is not treated as equal to another `NULL` in the same way as ordinary values.

However, the exact number of `NULL`s allowed can vary by DBMS.

For interviews, the safest answer is:

> A UNIQUE constraint prevents duplicate non-NULL values, but NULL handling is database-specific.

If a column must always have a value and also be unique:

```sql
email VARCHAR(100) NOT NULL UNIQUE
```

---

# 85. Important Interview Question — Why Is Normalization Important?

### Strong Answer

> Normalization reduces unnecessary duplication and helps maintain consistency. It also prevents insertion, update, and deletion anomalies by separating different entities and their relationships into appropriate tables.

---

# 86. Important Interview Question — What Is Denormalization?

### Strong Answer

> Denormalization is the intentional introduction of some redundancy into a database to reduce joins or improve read performance. It should be used carefully because it can increase storage and create consistency-maintenance challenges.

---

# 87. Important Interview Question — Is 3NF Always Enough?

For most application/database-design interviews, understanding 1NF, 2NF, and 3NF is essential.

BCNF is a stronger normal form and can be discussed when the interviewer asks about advanced normalization.

A good answer is:

> 3NF is commonly sufficient for many practical relational designs, but BCNF provides a stricter condition where every determinant must be a candidate key.

---

# 88. SQL Example — Complete Relational Design

### Departments

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);
```

### Employees

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    salary DECIMAL(10,2) CHECK (salary >= 0),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This design demonstrates:

```text
Primary Key
Foreign Key
UNIQUE
NOT NULL
CHECK
Relationships
```

---

# 89. Practical Example — Student Enrollment Database

Instead of one large table:

```text
Student
----------------------------------------------------
student_id
student_name
course_id
course_name
instructor_name
grade
```

Use:

```text
Students
-------------------------
student_id
student_name
```

```text
Courses
-------------------------
course_id
course_name
instructor_id
```

```text
Instructors
-------------------------
instructor_id
instructor_name
```

```text
Enrollments
-------------------------
student_id
course_id
grade
```

This separates entities and reduces unnecessary repetition.

---

# 90. Real-World Example — E-Commerce

An e-commerce database might contain:

```text
Customers
Products
Orders
OrderItems
Payments
```

Instead of storing:

```text
customer_name
customer_email
product_name
product_price
order_date
```

repeatedly in every order row, the information can be separated according to its entity.

For example:

```text
Customers
    ↓
Orders
    ↓
OrderItems
    ↓
Products
```

Keys and foreign keys establish these relationships.

---

# 91. Real-World Example — Banking

A banking system may have:

```text
Customers
Accounts
Transactions
Branches
```

A customer's identity should not be duplicated unnecessarily in every transaction row.

Instead:

```text
customer_id
account_id
transaction_id
```

can establish relationships.

This improves consistency and makes updates safer.

---

# 92. Real-World Example — HR System

An HR database may use:

```text
Employees
Departments
Projects
EmployeeProjects
```

For a many-to-many relationship between employees and projects:

```sql
CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,

    PRIMARY KEY (employee_id, project_id),

    FOREIGN KEY (employee_id)
        REFERENCES employees(employee_id),

    FOREIGN KEY (project_id)
        REFERENCES projects(project_id)
);
```

The composite primary key prevents the same employee from being assigned to the same project more than once.

---

# 93. Many-to-Many Relationship

A many-to-many relationship usually requires a junction/associative table.

Example:

```text
Students
    ↕
Enrollments
    ↕
Courses
```

One student can enroll in many courses.

One course can have many students.

The middle table:

```text
Enrollments
```

represents the relationship.

---

# 94. One-to-Many Relationship

Example:

```text
Department
     |
     | 1
     |
     | many
     ↓
Employees
```

One department can have many employees.

The foreign key is usually stored on the many side:

```sql
department_id INT
```

inside `employees`.

---

# 95. One-to-One Relationship

A one-to-one relationship means one record in one table corresponds to at most one record in another table.

Example:

```text
Person
   |
   | 1
   |
   | 1
   ↓
Passport
```

A foreign key with a `UNIQUE` constraint can enforce the one-to-one relationship.

Example:

```sql
CREATE TABLE passports (
    passport_id INT PRIMARY KEY,
    person_id INT UNIQUE,

    FOREIGN KEY (person_id)
        REFERENCES persons(person_id)
);
```

---

# 96. Keys and Constraints — Quick Revision

```text
PRIMARY KEY
→ Uniquely identifies each row

FOREIGN KEY
→ References a key in another table

CANDIDATE KEY
→ Minimal possible unique identifier

ALTERNATE KEY
→ Candidate key not selected as primary key

SUPER KEY
→ Any set of columns that uniquely identifies a row

COMPOSITE KEY
→ Key made from multiple columns

UNIQUE
→ Prevents duplicate values

NOT NULL
→ Value is required

CHECK
→ Value must satisfy a condition

DEFAULT
→ Supplies a value when none is provided
```

---

# 97. Normalization — Quick Revision

```text
1NF
→ Atomic values
→ No repeating groups

2NF
→ 1NF
→ No partial dependency

3NF
→ 2NF
→ No problematic transitive dependency

BCNF
→ Every determinant is a candidate key

DENORMALIZATION
→ Intentionally adds some redundancy for selected performance/readability goals
```

---

# 98. Most Important Interview Questions

You should prepare these particularly well:

1. What is a primary key?
2. What is a foreign key?
3. Primary key vs foreign key?
4. Primary key vs UNIQUE?
5. Can a foreign key contain NULL?
6. Can a foreign key contain duplicate values?
7. Can a table have multiple foreign keys?
8. Can a table have multiple primary keys?
9. What is a composite key?
10. What is a candidate key?
11. What is a super key?
12. Candidate key vs primary key?
13. What is an alternate key?
14. What is a surrogate key?
15. Natural key vs surrogate key?
16. What is referential integrity?
17. What happens when a referenced parent row is deleted?
18. What is `ON DELETE CASCADE`?
19. What is `ON DELETE SET NULL`?
20. What are SQL constraints?
21. What is `NOT NULL`?
22. What is `UNIQUE`?
23. What is `CHECK`?
24. What is `DEFAULT`?
25. What is normalization?
26. Why do we normalize databases?
27. What is 1NF?
28. What is 2NF?
29. What is 3NF?
30. What is BCNF?
31. What is functional dependency?
32. What is partial dependency?
33. What is transitive dependency?
34. What are insertion, update, and deletion anomalies?
35. What is denormalization?
36. Normalization vs denormalization?
37. When would you use a composite key?
38. How do you model a many-to-many relationship?
39. Can a foreign key reference a UNIQUE key?
40. How would you design an employee-department database?

---

# 99. High-Priority Coding Questions

## Question 1 — Create a Table with Constraints

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10,2) CHECK (salary >= 0),
    status VARCHAR(20) DEFAULT 'Active'
);
```

---

## Question 2 — Create Parent and Child Tables

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);
```

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

## Question 3 — Create a Composite Primary Key

```sql
CREATE TABLE enrollments (
    student_id INT,
    course_id INT,
    grade VARCHAR(2),

    PRIMARY KEY (student_id, course_id)
);
```

---

## Question 4 — Create a Many-to-Many Relationship

```sql
CREATE TABLE employee_projects (
    employee_id INT,
    project_id INT,

    PRIMARY KEY (employee_id, project_id),

    FOREIGN KEY (employee_id)
        REFERENCES employees(employee_id),

    FOREIGN KEY (project_id)
        REFERENCES projects(project_id)
);
```

---

# 100. Best Interview Explanation — Complete Example

If the interviewer asks:

> "How would you design an employee and department database?"

A strong answer:

> I would create separate `employees` and `departments` tables because department information should not be repeated for every employee. I would use `department_id` as the primary key in the departments table and as a foreign key in the employees table. The employee table would have its own `employee_id` primary key, and I could add constraints such as `NOT NULL`, `UNIQUE`, and `CHECK` where appropriate. This keeps the design normalized, reduces redundancy, and maintains referential integrity.

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    salary DECIMAL(10,2) CHECK (salary >= 0),
    department_id INT,

    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

This answer demonstrates:

```text
Database design
Primary keys
Foreign keys
Constraints
Normalization
Referential integrity
```

---

# 101. Final Interview Cheat Sheet

## Keys

```text
Super Key
    ↓
Candidate Key
    ↓
Choose one
    ↓
Primary Key

Remaining candidate keys
    ↓
Alternate Keys
```

## Relationships

```text
Parent Table
    ↓
Primary/Unique Key
    ↓
Foreign Key
    ↓
Child Table
```

## Constraints

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

## Normalization

```text
1NF
→ Atomic values

2NF
→ Remove partial dependency

3NF
→ Remove transitive dependency

BCNF
→ Every determinant is a candidate key
```

## Anomalies

```text
Insertion Anomaly
Update Anomaly
Deletion Anomaly
```

## Design Trade-off

```text
Normalization
→ Less redundancy + stronger consistency

Denormalization
→ More redundancy + potentially simpler/faster reads
```

---

# 102. What You Should Be Able to Explain in an Interview

Before moving to the next SQL topic, make sure you can explain these naturally without memorizing definitions word-for-word:

```text
1. Primary key
2. Foreign key
3. Candidate key
4. Super key
5. Composite key
6. Primary key vs UNIQUE
7. Primary key vs foreign key
8. Foreign key and referential integrity
9. ON DELETE CASCADE
10. SQL constraints
11. Normalization
12. 1NF
13. 2NF
14. 3NF
15. Functional dependency
16. Partial dependency
17. Transitive dependency
18. Insertion/update/deletion anomalies
19. Normalization vs denormalization
20. Many-to-many relationship
```

The most valuable skill is not simply knowing the definitions. You should be able to **look at an unnormalized table, identify the redundancy/dependency problem, and explain how you would split it into related tables using primary keys and foreign keys.**