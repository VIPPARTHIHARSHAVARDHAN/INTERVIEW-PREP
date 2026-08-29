# SQL Basics and Filtering

## 1. What is SQL?

**SQL (Structured Query Language)** is a language used to communicate with relational databases.

We use SQL to:

- Create tables
- Insert data
- Read data
- Update data
- Delete data
- Filter data
- Sort data
- Group data
- Join multiple tables

Example:

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

This query retrieves employees whose salary is greater than 50,000.

### Interview Answer

> SQL is a standard language used to interact with relational databases. It is mainly used to perform operations such as retrieving, inserting, updating, deleting, and managing data stored in tables.

---

# 2. What is a Database?

A **database** is an organized collection of data that can be stored, managed, and retrieved efficiently.

For example, a company database may contain:

```text
Employees
Departments
Customers
Orders
Products
```

---

# 3. What is a Table?

A table stores data in the form of **rows and columns**.

Example:

| id | name | department | salary |
|---:|---|---|---:|
| 1 | Rahul | IT | 60000 |
| 2 | Priya | HR | 50000 |
| 3 | Arjun | IT | 70000 |

Here:

- `id`, `name`, `department`, `salary` are columns.
- Each employee record is a row.

### Interview Answer

> A table is a structured collection of related data organized into rows and columns.

---

# 4. What is a Row?

A **row** represents one complete record in a table.

Example:

```text
1 | Rahul | IT | 60000
```

This represents one employee.

A row is also commonly called a **record**.

---

# 5. What is a Column?

A **column** represents a particular attribute of the data.

Example:

```text
id
name
department
salary
```

Each column normally has a specific data type.

---

# 6. What is RDBMS?

**RDBMS** stands for **Relational Database Management System**.

It stores data in related tables and uses relationships between those tables.

Examples:

- MySQL
- PostgreSQL
- Oracle Database
- Microsoft SQL Server
- SQLite

### Interview Answer

> An RDBMS is a database management system that stores data in tables and allows relationships between tables using concepts such as primary keys and foreign keys.

---

# 7. SQL vs MySQL

These are not the same thing.

| SQL | MySQL |
|---|---|
| Language | Database Management System |
| Used to communicate with databases | Used to store and manage databases |
| Standard query language | One implementation of a relational database system |
| Example: `SELECT * FROM employees` | Software that executes SQL queries |

### Interview Answer

> SQL is the language used to interact with relational databases, while MySQL is an RDBMS that uses SQL to manage and query data.

---

# 8. What is DBMS vs RDBMS?

| DBMS | RDBMS |
|---|---|
| Database Management System | Relational Database Management System |
| May not require relationships between tables | Data is organized into related tables |
| Relationship support may be limited | Supports relationships using keys |
| General database management | Relational database management |

### Simple Explanation

```text
DBMS
 ↓
Manages data

RDBMS
 ↓
Manages data
+
Stores data in related tables
```

---

# 9. What are SQL Command Categories?

SQL commands are commonly divided into categories.

## DDL — Data Definition Language

Used to define or modify database structure.

Examples:

```sql
CREATE
ALTER
DROP
TRUNCATE
```

Example:

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100),
    salary DECIMAL(10,2)
);
```

---

## DML — Data Manipulation Language

Used to modify data inside tables.

Examples:

```sql
INSERT
UPDATE
DELETE
```

Example:

```sql
INSERT INTO employees (id, name, salary)
VALUES (1, 'Rahul', 60000);
```

---

## DQL — Data Query Language

Used to retrieve data.

Main command:

```sql
SELECT
```

Example:

```sql
SELECT *
FROM employees;
```

---

## DCL — Data Control Language

Used for permissions and access control.

Examples:

```sql
GRANT
REVOKE
```

---

## TCL — Transaction Control Language

Used to manage transactions.

Examples:

```sql
COMMIT
ROLLBACK
SAVEPOINT
```

### Interview Tip

For fresher interviews, knowing these categories and their common commands is usually sufficient.

---

# 10. SELECT Statement

`SELECT` is used to retrieve data from a table.

Example:

```sql
SELECT *
FROM employees;
```

This retrieves all columns.

To retrieve specific columns:

```sql
SELECT name, salary
FROM employees;
```

### Best Practice

Instead of always using:

```sql
SELECT *
FROM employees;
```

prefer:

```sql
SELECT name, salary
FROM employees;
```

when you only need specific columns.

---

# 11. What does `*` mean?

The `*` means **all columns**.

```sql
SELECT *
FROM employees;
```

It means:

> Return all columns from the `employees` table.

---

# 12. WHERE Clause

`WHERE` is used to filter rows based on a condition.

Example:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Only employees with salary greater than 50,000 are returned.

---

# 13. Comparison Operators

Common comparison operators are:

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `<>` | Not equal |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |

Examples:

```sql
SELECT *
FROM employees
WHERE salary = 50000;
```

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

```sql
SELECT *
FROM employees
WHERE department <> 'HR';
```

---

# 14. Logical Operators

## AND

Both conditions must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

---

## OR

At least one condition must be true.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

---

## NOT

Negates a condition.

```sql
SELECT *
FROM employees
WHERE NOT department = 'HR';
```

A common alternative is:

```sql
SELECT *
FROM employees
WHERE department <> 'HR';
```

---

# 15. Combining AND and OR

Be careful when combining conditions.

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000
OR department = 'HR';
```

SQL evaluates logical expressions according to operator precedence.

To make the intended logic clear, use parentheses:

```sql
SELECT *
FROM employees
WHERE (department = 'IT' AND salary > 50000)
   OR department = 'HR';
```

### Interview Tip

Using parentheses makes complicated filtering conditions easier to understand and reduces logical mistakes.

---

# 16. DISTINCT

`DISTINCT` removes duplicate values from the result.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

If the table contains:

```text
IT
HR
IT
Sales
HR
```

the result will be:

```text
IT
HR
Sales
```

---

# 17. DISTINCT with Multiple Columns

You can use `DISTINCT` on multiple columns.

```sql
SELECT DISTINCT department, job_role
FROM employees;
```

Here, SQL removes duplicate **combinations** of `department` and `job_role`.

It does not independently remove duplicates from each column.

---

# 18. ORDER BY

`ORDER BY` sorts query results.

## Ascending Order

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

`ASC` means ascending.

This is also the default in most SQL implementations:

```sql
SELECT *
FROM employees
ORDER BY salary;
```

---

## Descending Order

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# 19. Sorting by Multiple Columns

You can sort using multiple columns.

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

This means:

1. Sort by department alphabetically.
2. Within each department, sort salary from highest to lowest.

---

# 20. LIMIT

`LIMIT` restricts the number of rows returned in databases such as MySQL and PostgreSQL.

Example:

```sql
SELECT *
FROM employees
LIMIT 5;
```

Returns at most 5 rows.

### Important

`LIMIT` syntax varies between database systems.

For example, SQL Server commonly uses:

```sql
SELECT TOP 5 *
FROM employees;
```

Modern SQL Server also supports `OFFSET ... FETCH` for pagination.

---

# 21. LIMIT with ORDER BY

To get the highest-paid employee:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

To get the top 3 highest-paid employees:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

### Important Interview Point

If you want the **top N records**, use `ORDER BY` before limiting the result.

This:

```sql
SELECT *
FROM employees
LIMIT 3;
```

does not mean "top 3 highest-paid employees."

Instead:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

does.

---

# 22. Column Aliases

An alias temporarily changes the name displayed in the result.

```sql
SELECT name AS employee_name
FROM employees;
```

You can also omit `AS` in many SQL systems:

```sql
SELECT name employee_name
FROM employees;
```

Using `AS` is generally clearer.

---

# 23. Table Aliases

Aliases can also be given to tables.

```sql
SELECT e.name, e.salary
FROM employees AS e;
```

This becomes especially useful when working with joins.

Example:

```sql
SELECT e.name, d.department_name
FROM employees AS e
JOIN departments AS d
    ON e.department_id = d.department_id;
```

---

# 24. INSERT

`INSERT` adds new records to a table.

Example:

```sql
INSERT INTO employees (id, name, department, salary)
VALUES (1, 'Rahul', 'IT', 60000);
```

Multiple rows can often be inserted together:

```sql
INSERT INTO employees (id, name, department, salary)
VALUES
    (2, 'Priya', 'HR', 50000),
    (3, 'Arjun', 'IT', 70000);
```

---

# 25. UPDATE

`UPDATE` modifies existing records.

Example:

```sql
UPDATE employees
SET salary = 65000
WHERE id = 1;
```

### ⚠️ Important

Always be careful with the `WHERE` condition.

Without `WHERE`:

```sql
UPDATE employees
SET salary = 65000;
```

the statement can update **every row** in the table.

### Interview Answer

> I use a precise WHERE condition with UPDATE to make sure only the intended records are modified.

---

# 26. DELETE

`DELETE` removes rows from a table.

Example:

```sql
DELETE FROM employees
WHERE id = 1;
```

Without `WHERE`:

```sql
DELETE FROM employees;
```

all rows can be deleted from the table.

---

# 27. DELETE vs TRUNCATE vs DROP

This is a common interview question.

| DELETE | TRUNCATE | DROP |
|---|---|---|
| Removes rows | Removes all rows | Removes table |
| Can use WHERE | Normally cannot use WHERE | Table structure is removed |
| DML | Usually classified as DDL | DDL |
| Table remains | Table remains | Table no longer exists |
| Can selectively remove rows | Removes all table rows | Removes entire table |

Example:

```sql
DELETE FROM employees
WHERE department = 'HR';
```

```sql
TRUNCATE TABLE employees;
```

```sql
DROP TABLE employees;
```

### Interview Answer

> DELETE removes selected rows and supports a WHERE condition. TRUNCATE removes all rows while keeping the table structure. DROP removes the table itself along with its structure.

### Important Note

Exact transaction, rollback, identity-reset, and locking behavior can differ between database systems, so avoid making overly broad claims unless the interviewer specifies the database.

---

# 28. NULL in SQL

`NULL` represents a missing, unknown, or unavailable value.

It is **not** the same as:

```text
0
```

or:

```text
''
```

or:

```text
'NULL'
```

Example:

| id | name | phone |
|---:|---|---|
| 1 | Rahul | 9876543210 |
| 2 | Priya | NULL |

Priya's phone value is missing/unknown.

---

# 29. How to Check NULL?

Do not use:

```sql
WHERE phone = NULL;
```

Use:

```sql
WHERE phone IS NULL;
```

For non-NULL:

```sql
WHERE phone IS NOT NULL;
```

### Why?

`NULL` represents an unknown/missing value, so normal equality comparison with `NULL` does not work as expected.

---

# 30. IS NULL Example

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

This returns employees whose phone value is NULL.

---

# 31. IN Operator

`IN` checks whether a value belongs to a list.

Instead of:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Sales';
```

we can write:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Sales');
```

This is cleaner and easier to maintain.

---

# 32. NOT IN

`NOT IN` excludes values from a list.

```sql
SELECT *
FROM employees
WHERE department NOT IN ('HR', 'Sales');
```

### Important NULL Note

`NOT IN` can produce unexpected results when the compared data or list contains `NULL`.

For more complex cases involving possible NULLs, `NOT EXISTS` is often safer and clearer.

---

# 33. BETWEEN

`BETWEEN` checks whether a value falls within a range.

Example:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;
```

For numeric values, this normally includes both boundaries.

So:

```text
40000 <= salary <= 70000
```

---

# 34. BETWEEN with Dates

Example:

```sql
SELECT *
FROM employees
WHERE joining_date BETWEEN '2026-01-01' AND '2026-01-31';
```

### Important Interview Point

For date/time columns containing timestamps, a half-open range is often safer:

```sql
SELECT *
FROM employees
WHERE joining_date >= '2026-01-01'
  AND joining_date < '2026-02-01';
```

This avoids accidentally excluding records later on January 31 when the column stores time as well.

---

# 35. LIKE Operator

`LIKE` is used for pattern matching.

## `%`

`%` represents zero or more characters.

Example:

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

This finds names starting with `A`.

Examples:

```text
Arjun
Anil
Amit
```

---

## `_`

`_` represents exactly one character.

Example:

```sql
SELECT *
FROM employees
WHERE name LIKE '_a%';
```

This looks for names where the second character is `a`.

---

# 36. Common LIKE Patterns

| Pattern | Meaning |
|---|---|
| `'A%'` | Starts with A |
| `'%A'` | Ends with A |
| `'%A%'` | Contains A |
| `'_A%'` | Second character is A |
| `'A_'` | Exactly two-character value beginning with A |

Example:

```sql
SELECT *
FROM customers
WHERE email LIKE '%@gmail.com';
```

---

# 37. Arithmetic Operators

SQL supports arithmetic operations such as:

```text
+
-
*
/
%
```

Example:

```sql
SELECT name, salary, salary * 12 AS annual_salary
FROM employees;
```

This calculates an approximate annual salary assuming the monthly salary is stored.

---

# 38. Calculated Columns

You can perform calculations directly inside `SELECT`.

Example:

```sql
SELECT
    name,
    salary,
    salary * 12 AS annual_salary
FROM employees;
```

Another example:

```sql
SELECT
    product_name,
    price,
    price * quantity AS total_amount
FROM order_items;
```

---

# 39. SQL Operator Example

Suppose we have:

```text
employees
------------------------------------------------
id | name  | department | salary | experience
------------------------------------------------
1  | Rahul | IT         | 60000  | 3
2  | Priya | HR         | 50000  | 2
3  | Arjun | IT         | 70000  | 5
4  | Sneha | Sales      | 45000  | 1
```

Find IT employees earning more than 55,000:

```sql
SELECT name, salary
FROM employees
WHERE department = 'IT'
  AND salary > 55000;
```

Result:

```text
Rahul | 60000
Arjun | 70000
```

---

# 40. Combining Filtering and Sorting

Example:

```sql
SELECT name, department, salary
FROM employees
WHERE salary > 50000
ORDER BY salary DESC;
```

Execution conceptually produces:

```text
1. FROM
2. WHERE
3. SELECT
4. ORDER BY
```

However, the actual SQL logical processing order is more accurately described as:

```text
FROM
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
LIMIT/OFFSET
```

The database optimizer may physically execute operations differently.

### Interview Answer

> The logical query processing order helps explain how SQL interprets a query. It starts with FROM and WHERE, then grouping and filtering groups, then SELECT, DISTINCT, ORDER BY, and finally row limiting. The optimizer can choose a different physical execution plan for performance.

---

# 41. Can We Use WHERE with Aggregate Functions?

Generally, aggregate functions such as `COUNT()` or `AVG()` cannot be used directly in `WHERE` because `WHERE` filters rows before grouping/aggregation.

Incorrect:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE AVG(salary) > 60000
GROUP BY department;
```

Use `HAVING`:

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### Key Idea

```text
WHERE  → filters rows
HAVING → filters groups
```

This topic will be covered in more detail in the aggregation file.

---

# 42. Common SQL Query Examples

## Find all employees

```sql
SELECT *
FROM employees;
```

---

## Find only employee names

```sql
SELECT name
FROM employees;
```

---

## Find employees with salary above 50000

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

## Find IT employees

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

---

## Find IT employees earning above 50000

```sql
SELECT *
FROM employees
WHERE department = 'IT'
  AND salary > 50000;
```

---

## Find employees from IT or HR

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

---

## Find employees whose names start with A

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

## Find employees without a phone number

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

---

## Find the highest-paid employee

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

---

## Find the lowest-paid employee

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 1;
```

---

## Find top 3 highest-paid employees

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

---

# 43. Real-World Example — Employee Search

Imagine an HR application where the interviewer asks:

> "Show active IT employees earning more than ₹60,000, sorted from highest salary to lowest."

Query:

```sql
SELECT
    name,
    department,
    salary
FROM employees
WHERE department = 'IT'
  AND salary > 60000
  AND status = 'Active'
ORDER BY salary DESC;
```

### How to Explain It

> First, I select only the columns required for the report. Then I filter the employees using the WHERE clause based on department, salary, and status. Finally, I sort the remaining employees by salary in descending order so that the highest-paid employee appears first.

This explanation shows that you understand the **logic of the query**, not just the syntax.

---

# 44. Real-World Example — E-Commerce

Suppose an online shopping company has:

```text
products
----------------------------------
id | name | category | price
----------------------------------
1  | Phone | Electronics | 30000
2  | Laptop | Electronics | 60000
3  | Chair | Furniture | 8000
4  | Mouse | Electronics | 1000
```

Question:

> Find electronics products costing more than ₹10,000 and display the most expensive products first.

Query:

```sql
SELECT
    name,
    category,
    price
FROM products
WHERE category = 'Electronics'
  AND price > 10000
ORDER BY price DESC;
```

### Interview Explanation

> I first filter the records to the Electronics category and then apply the price condition. After filtering, I sort the result in descending order so the highest-priced products appear first.

---

# 45. Real-World Example — Customer Search

Question:

> Find customers whose names start with "A".

```sql
SELECT
    customer_id,
    name
FROM customers
WHERE name LIKE 'A%';
```

Question:

> Find customers who have not provided an email address.

```sql
SELECT
    customer_id,
    name
FROM customers
WHERE email IS NULL;
```

---

# 46. Common Interview Questions

## Q1. What is SQL?

### Answer

> SQL is a standard language used to communicate with relational databases. It is used to retrieve, insert, update, delete, and manage data.

---

## Q2. What is the difference between SQL and MySQL?

### Answer

> SQL is a query language, whereas MySQL is a relational database management system that uses SQL to store and manage data.

---

## Q3. What is a database?

### Answer

> A database is an organized collection of data that can be stored, managed, and retrieved efficiently.

---

## Q4. What is a table?

### Answer

> A table stores related data in rows and columns. Each row generally represents a record, while each column represents an attribute.

---

## Q5. What is the difference between a row and a column?

### Answer

> A row represents one record, while a column represents one attribute or field shared by the records in the table.

---

## Q6. What is the use of SELECT?

### Answer

> SELECT is used to retrieve data from one or more tables.

Example:

```sql
SELECT name, salary
FROM employees;
```

---

## Q7. What is the use of WHERE?

### Answer

> WHERE filters individual rows based on a condition.

Example:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

## Q8. What is DISTINCT?

### Answer

> DISTINCT removes duplicate result rows based on the selected columns.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

---

## Q9. What is ORDER BY?

### Answer

> ORDER BY sorts the query result based on one or more columns.

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## Q10. What is LIMIT?

### Answer

> LIMIT restricts the number of rows returned by a query in databases that support that syntax, such as MySQL and PostgreSQL.

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

## Q11. What is the difference between WHERE and HAVING?

### Answer

> WHERE filters individual rows before grouping, while HAVING filters groups after GROUP BY and aggregation.

Example:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

## Q12. What is NULL?

### Answer

> NULL represents a missing, unknown, or unavailable value. It is different from zero, an empty string, or the text 'NULL'.

---

## Q13. How do you find NULL values?

### Answer

Use:

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

Do not use:

```sql
WHERE phone = NULL;
```

---

## Q14. What is the difference between IN and OR?

### Answer

> IN is a concise way to check whether a value matches any value in a specified list. It is often cleaner than writing multiple OR conditions.

Example:

```sql
WHERE department IN ('IT', 'HR', 'Sales');
```

instead of:

```sql
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Sales';
```

---

## Q15. What is LIKE?

### Answer

> LIKE is used for pattern matching in SQL. `%` represents zero or more characters, while `_` represents one character.

Example:

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

## Q16. What is BETWEEN?

### Answer

> BETWEEN checks whether a value falls within a specified range. For ordinary numeric ranges, the boundary values are included.

Example:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 70000;
```

---

## Q17. What is an alias?

### Answer

> An alias is a temporary name given to a column or table to make the query output or query itself easier to understand.

Example:

```sql
SELECT
    name AS employee_name
FROM employees;
```

---

## Q18. What happens if UPDATE is used without WHERE?

### Answer

> The UPDATE can modify every row in the table. Therefore, I always verify the WHERE condition before executing an UPDATE on production data.

Example of risky query:

```sql
UPDATE employees
SET salary = 70000;
```

Safer:

```sql
UPDATE employees
SET salary = 70000
WHERE id = 10;
```

---

## Q19. What happens if DELETE is used without WHERE?

### Answer

> DELETE without a WHERE condition removes all rows from the table. The table structure itself remains.

Example:

```sql
DELETE FROM employees;
```

---

## Q20. DELETE vs TRUNCATE vs DROP?

### Answer

> DELETE removes rows and can use WHERE for selective deletion. TRUNCATE removes all rows while keeping the table structure. DROP removes the table itself.

---

## Q21. Can we use multiple conditions in WHERE?

### Answer

Yes.

```sql
SELECT *
FROM employees
WHERE department = 'IT'
  AND salary > 50000;
```

---

## Q22. Can we sort by multiple columns?

### Answer

Yes.

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

---

## Q23. What is the difference between `COUNT(*)` and `COUNT(column)`?

### Answer

> `COUNT(*)` counts rows, while `COUNT(column)` counts non-NULL values in that specific column.

Example:

```sql
SELECT COUNT(*)
FROM employees;
```

counts all rows.

```sql
SELECT COUNT(phone)
FROM employees;
```

counts only rows where `phone` is not NULL.

---

# 47. Interview Coding Questions to Practice

Before moving to the next SQL file, you should be able to write these without looking at the answers.

### Question 1

Write a query to display all employees.

### Question 2

Write a query to display only employee names and salaries.

### Question 3

Find employees earning more than 50,000.

### Question 4

Find employees belonging to the IT department.

### Question 5

Find employees belonging to IT or HR.

### Question 6

Find employees whose salary is between 40,000 and 70,000.

### Question 7

Find employees whose names start with `A`.

### Question 8

Find employees whose names contain `an`.

### Question 9

Find employees whose phone number is NULL.

### Question 10

Find employees whose phone number is not NULL.

### Question 11

Display unique departments.

### Question 12

Sort employees by salary from highest to lowest.

### Question 13

Find the top 5 highest-paid employees.

### Question 14

Find employees from IT earning more than 60,000 and sort them by salary descending.

### Question 15

Update the salary of employee ID 10.

### Question 16

Delete employee ID 10.

### Question 17

Find the number of rows in the employees table.

### Question 18

Find employees who are not from HR or Sales.

### Question 19

Display employee name and annual salary assuming salary represents monthly salary.

### Question 20

Write a query using both `AND` and `OR` with parentheses to make the intended logic explicit.

---

# 48. Quick Revision Sheet

```text
SQL
↓
Language used to interact with relational databases

SELECT
↓
Retrieve data

WHERE
↓
Filter rows

DISTINCT
↓
Remove duplicate result rows

ORDER BY
↓
Sort results

LIMIT
↓
Restrict number of returned rows

IN
↓
Match against a list

BETWEEN
↓
Check a range

LIKE
↓
Pattern matching

%
↓
Zero or more characters

_
↓
Exactly one character

IS NULL
↓
Check missing/unknown value

IS NOT NULL
↓
Check non-NULL value

AND
↓
All conditions must be true

OR
↓
At least one condition must be true

NOT
↓
Negate a condition

INSERT
↓
Add rows

UPDATE
↓
Modify rows

DELETE
↓
Remove rows

TRUNCATE
↓
Remove all rows while keeping table structure

DROP
↓
Remove the table itself
```

---

# 49. Key Interview Mindset

When an interviewer gives a SQL problem, do not immediately start typing.

First identify:

```text
1. What data do I need?
        ↓
2. Which table contains it?
        ↓
3. Do I need one table or multiple tables?
        ↓
4. What rows need to be filtered?
        ↓
5. Do I need sorting?
        ↓
6. Do I need grouping?
        ↓
7. Do I need a JOIN?
        ↓
8. Do I need a subquery / CTE?
        ↓
9. Do I need a window function?
        ↓
10. Write and explain the query
```

For example, if the interviewer says:

> "Find the top 5 highest-paid IT employees."

Think:

```text
employees table
      ↓
department = IT
      ↓
ORDER BY salary DESC
      ↓
LIMIT 5
```

Then write:

```sql
SELECT
    name,
    salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 5;
```

### Strong Interview Explanation

> I first filter the employees to the IT department using WHERE. Then I sort those employees by salary in descending order and limit the result to five records. This gives me the five highest-paid IT employees.

This approach is much stronger in an interview than simply writing the query without explaining the reasoning.