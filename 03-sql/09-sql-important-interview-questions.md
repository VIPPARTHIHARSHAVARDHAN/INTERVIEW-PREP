# 09-sql-important-interview-questions.md

# SQL Important Interview Questions

> **Interview-focused revision file:** If you have limited time before an interview, prioritize this file.  
> It covers the most commonly tested SQL concepts, theory, query-writing patterns, and scenario-based questions.
>
> **Recommended preparation order:**  
> 1. Basics & Filtering  
> 2. Aggregations  
> 3. Joins  
> 4. Subqueries / CTE / CASE  
> 5. Window Functions  
> 6. Keys / Constraints / Normalization  
> 7. Transactions / Views / Indexes  
> 8. Query Problems  
> 9. This file for final revision

---

# 1. SQL Basics — Must Know

## Q1. What is SQL?

SQL stands for **Structured Query Language**.

It is used to interact with relational databases to:

- Create database objects
- Insert data
- Retrieve data
- Update data
- Delete data
- Control access
- Manage transactions

Example:

```sql
SELECT *
FROM employees;
```

---

## Q2. What is a database?

A database is an organized collection of data that can be stored, accessed, managed, and modified efficiently.

Examples:

- MySQL
- PostgreSQL
- Oracle
- SQL Server

---

## Q3. What is a relational database?

A relational database stores data in **tables** consisting of rows and columns.

Tables can be related to each other using keys.

Example:

```text
employees
+----+--------+------------+
| id | name   | dept_id    |
+----+--------+------------+
| 1  | John   | 10         |
| 2  | Alice  | 20         |
+----+--------+------------+
```

---

## Q4. What is a table?

A table stores data in the form of:

- Rows → records
- Columns → attributes

Example:

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(50),
    salary INT
);
```

---

## Q5. What is a row?

A row represents one complete record in a table.

Example:

```text
1 | John | 50000
```

represents one employee.

---

## Q6. What is a column?

A column represents a particular attribute of the data.

Example:

```text
id
name
salary
department
```

---

## Q7. What is a primary key?

A primary key uniquely identifies each row in a table.

Properties:

- Must be unique
- Cannot contain `NULL`
- A table can have only one primary key
- It can contain one or multiple columns

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50)
);
```

---

## Q8. What is a foreign key?

A foreign key creates a relationship between two tables.

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(50),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

## Q9. Primary key vs foreign key

| Primary Key | Foreign Key |
|---|---|
| Uniquely identifies a row | References a key in another table |
| Cannot be NULL | Can usually contain NULL |
| Unique | Can contain duplicates |
| One primary key per table | Multiple foreign keys possible |

---

## Q10. What is a candidate key?

A candidate key is a column or combination of columns that can uniquely identify a row.

A table may have multiple candidate keys, but one is selected as the primary key.

---

## Q11. What is a composite key?

A composite key consists of two or more columns used together to uniquely identify a row.

Example:

```sql
CREATE TABLE student_course (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

---

# 2. SELECT and Filtering

## Q12. What is the basic structure of a SELECT query?

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

Example:

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

---

## Q13. Difference between WHERE and HAVING

### WHERE

Filters rows **before grouping**.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### HAVING

Filters groups **after GROUP BY**.

```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

### Important interview point

```text
WHERE → filters rows
HAVING → filters groups
```

---

## Q14. What is DISTINCT?

`DISTINCT` removes duplicate values from the result.

```sql
SELECT DISTINCT department_id
FROM employees;
```

---

## Q15. What is ORDER BY?

`ORDER BY` sorts the result.

Ascending:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

Descending:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## Q16. What is LIMIT?

`LIMIT` restricts the number of rows returned.

```sql
SELECT *
FROM employees
LIMIT 5;
```

> Syntax can differ between database systems.

---

## Q17. What is BETWEEN?

`BETWEEN` checks whether a value falls within a range.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 30000 AND 60000;
```

---

## Q18. What is IN?

`IN` checks whether a value exists in a list.

```sql
SELECT *
FROM employees
WHERE department_id IN (10, 20, 30);
```

---

## Q19. What is LIKE?

`LIKE` performs pattern matching.

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

Common patterns:

```text
'A%'   → starts with A
'%A'   → ends with A
'%A%'  → contains A
'_A%'  → second character is A
```

---

# 3. NULL

## Q20. What is NULL?

`NULL` represents a missing, unknown, or unavailable value.

It is **not**:

```text
0
''
FALSE
```

---

## Q21. How do you check for NULL?

Correct:

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

Incorrect:

```sql
WHERE manager_id = NULL;
```

---

## Q22. How do you check for NOT NULL?

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

---

## Q23. What is COALESCE?

`COALESCE()` returns the first non-NULL value.

```sql
SELECT name,
       COALESCE(commission, 0) AS commission
FROM employees;
```

---

# 4. Aggregate Functions

## Q24. What are aggregate functions?

Aggregate functions perform calculations on multiple rows and return a single result per group.

Common functions:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

## Q25. Difference between COUNT(*) and COUNT(column)

```sql
COUNT(*)
```

counts rows.

```sql
COUNT(column)
```

counts non-NULL values in that column.

Example:

```sql
SELECT COUNT(*)
FROM employees;
```

```sql
SELECT COUNT(manager_id)
FROM employees;
```

---

## Q26. What is GROUP BY?

`GROUP BY` groups rows having the same values.

Example:

```sql
SELECT department_id, COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

---

## Q27. Find the average salary of each department.

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

---

## Q28. Find departments having more than 5 employees.

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

# 5. SQL Functions

## Q29. What are scalar functions?

Scalar functions operate on individual values and return one value per row.

Examples:

```text
UPPER()
LOWER()
LENGTH()
ROUND()
COALESCE()
```

Example:

```sql
SELECT UPPER(name)
FROM employees;
```

---

## Q30. What is the difference between aggregate and scalar functions?

| Aggregate | Scalar |
|---|---|
| Works on multiple rows | Works on individual values |
| Returns result for a group | Usually returns one result per row |
| SUM, AVG, COUNT | UPPER, LOWER, LENGTH |

---

# 6. Joins — Extremely Important

## Q31. What is a JOIN?

A JOIN combines rows from two or more tables based on a related column.

Example:

```sql
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

---

## Q32. What are the main types of JOIN?

Important joins:

1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL OUTER JOIN
5. CROSS JOIN
6. SELF JOIN

---

## Q33. What is INNER JOIN?

Returns only matching rows from both tables.

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

---

## Q34. What is LEFT JOIN?

Returns:

- All rows from the left table
- Matching rows from the right table

If there is no match, right-side columns become `NULL`.

```sql
SELECT e.name, d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

---

## Q35. What is RIGHT JOIN?

Returns:

- All rows from the right table
- Matching rows from the left table

```sql
SELECT e.name, d.department_name
FROM employees e
RIGHT JOIN departments d
    ON e.department_id = d.department_id;
```

---

## Q36. What is FULL OUTER JOIN?

Returns all matching and non-matching rows from both tables.

```sql
SELECT *
FROM employees e
FULL OUTER JOIN departments d
    ON e.department_id = d.department_id;
```

> Not every database supports `FULL OUTER JOIN` directly.

---

## Q37. What is CROSS JOIN?

Produces the Cartesian product of two tables.

```sql
SELECT *
FROM employees
CROSS JOIN departments;
```

If:

```text
employees = 5 rows
departments = 3 rows
```

Result:

```text
5 × 3 = 15 rows
```

---

## Q38. What is SELF JOIN?

A table is joined with itself.

Example: employee-manager relationship.

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

## Q39. INNER JOIN vs LEFT JOIN

### INNER JOIN

Only matching records.

### LEFT JOIN

All records from the left table + matching records from right table.

This is one of the most frequently asked JOIN questions.

---

## Q40. How do you find employees who don't have a department?

```sql
SELECT e.*
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

---

# 7. Subqueries

## Q41. What is a subquery?

A subquery is a query written inside another query.

Example:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

## Q42. What is a correlated subquery?

A correlated subquery depends on the outer query.

Example:

```sql
SELECT e1.name, e1.salary
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id
);
```

---

## Q43. Subquery vs correlated subquery

| Subquery | Correlated Subquery |
|---|---|
| Can execute independently | Depends on outer query |
| Usually evaluated independently | Evaluated in relation to outer rows |
| Simpler | Often more expensive |

---

## Q44. Find employees earning more than the average salary.

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

## Q45. Find the second highest salary using a subquery.

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

---

# 8. EXISTS and IN

## Q46. What is EXISTS?

`EXISTS` checks whether a subquery returns at least one row.

```sql
SELECT *
FROM departments d
WHERE EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

---

## Q47. EXISTS vs IN

`IN` compares a value against a list/result.

`EXISTS` checks whether at least one matching row exists.

For large correlated datasets, `EXISTS` can sometimes be preferable, but actual performance depends on the database optimizer and query.

---

# 9. CASE

## Q48. What is CASE WHEN?

`CASE` implements conditional logic in SQL.

```sql
SELECT name,
       salary,
       CASE
           WHEN salary >= 100000 THEN 'High'
           WHEN salary >= 50000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_category
FROM employees;
```

---

## Q49. Can CASE be used with ORDER BY?

Yes.

```sql
SELECT *
FROM employees
ORDER BY
    CASE
        WHEN department_id = 10 THEN 1
        WHEN department_id = 20 THEN 2
        ELSE 3
    END;
```

---

# 10. CTE

## Q50. What is a CTE?

CTE stands for **Common Table Expression**.

It creates a temporary named result set that can be referenced by the following query.

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 80000
)
SELECT *
FROM high_salary;
```

---

## Q51. Why use CTEs?

CTEs improve:

- Readability
- Query organization
- Maintainability
- Complex query structure

---

## Q52. CTE vs subquery

Both can solve similar problems.

CTEs are often easier to read when a query becomes complex.

Example:

```sql
WITH dept_avg AS (
    SELECT department_id,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM dept_avg
WHERE avg_salary > 60000;
```

---

# 11. Window Functions — Extremely Important

## Q53. What is a window function?

A window function performs a calculation across related rows without collapsing them into one row.

Example:

```sql
SELECT name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_avg
FROM employees;
```

---

## Q54. GROUP BY vs window function

### GROUP BY

Reduces multiple rows into grouped results.

### Window function

Keeps individual rows while calculating across related rows.

Example:

```sql
SELECT department_id,
       AVG(salary)
FROM employees
GROUP BY department_id;
```

vs:

```sql
SELECT name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS avg_salary
FROM employees;
```

---

## Q55. What is ROW_NUMBER()?

Assigns a unique sequential number to each row.

```sql
SELECT name,
       salary,
       ROW_NUMBER() OVER (
           ORDER BY salary DESC
       ) AS rn
FROM employees;
```

---

## Q56. What is RANK()?

Assigns the same rank to tied values and leaves gaps after ties.

Example salaries:

```text
100000
100000
90000
```

Ranks:

```text
1
1
3
```

---

## Q57. What is DENSE_RANK()?

Assigns the same rank to ties but does not leave gaps.

```text
100000 → 1
100000 → 1
90000  → 2
```

---

## Q58. Difference between ROW_NUMBER, RANK and DENSE_RANK

| Function | Handles ties | Gaps |
|---|---|---|
| ROW_NUMBER | Gives different numbers | No |
| RANK | Same rank | Yes |
| DENSE_RANK | Same rank | No |

---

## Q59. Find the second highest salary using DENSE_RANK.

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk = 2;
```

---

## Q60. Find the highest-paid employee in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

---

## Q61. Find the top 3 salaries in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk <= 3;
```

---

## Q62. What is PARTITION BY?

`PARTITION BY` divides rows into groups for a window function.

Example:

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

calculates the average separately for each department.

---

## Q63. What is ORDER BY inside a window function?

It defines the ordering used by the window function.

Example:

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC
)
```

---

# 12. Keys and Constraints

## Q64. What are SQL constraints?

Constraints enforce rules on table data.

Important constraints:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

## Q65. What is UNIQUE?

Ensures that values in a column or combination of columns are unique.

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

---

## Q66. What is NOT NULL?

Ensures a column cannot contain `NULL`.

```sql
name VARCHAR(50) NOT NULL
```

---

## Q67. What is CHECK?

Ensures data satisfies a condition.

```sql
salary INT CHECK (salary > 0)
```

---

## Q68. What is DEFAULT?

Provides a default value when no value is supplied.

```sql
status VARCHAR(20) DEFAULT 'Active'
```

---

# 13. Normalization

## Q69. What is normalization?

Normalization is the process of organizing data to:

- Reduce redundancy
- Avoid data anomalies
- Improve data consistency

---

## Q70. What is 1NF?

A table is in First Normal Form when:

- Values are atomic
- No repeating groups
- Each column contains indivisible values

Bad:

```text
student_id | subjects
1          | SQL, Python, Java
```

Better:

```text
student_id | subject
1          | SQL
1          | Python
1          | Java
```

---

## Q71. What is 2NF?

A table is in 2NF when:

- It is already in 1NF
- No non-key attribute depends on only part of a composite key

---

## Q72. What is 3NF?

A table is in 3NF when:

- It is already in 2NF
- Non-key attributes do not depend on other non-key attributes

---

## Q73. Why is normalization important?

It helps reduce:

- Duplicate data
- Update anomalies
- Insert anomalies
- Delete anomalies

---

# 14. Transactions and ACID

## Q74. What is a transaction?

A transaction is a sequence of database operations treated as one logical unit of work.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE id = 2;

COMMIT;
```

---

## Q75. What is COMMIT?

`COMMIT` permanently saves transaction changes.

```sql
COMMIT;
```

---

## Q76. What is ROLLBACK?

`ROLLBACK` reverses uncommitted changes.

```sql
ROLLBACK;
```

---

## Q77. What is ACID?

ACID stands for:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

### Atomicity

All operations succeed or none do.

### Consistency

The database remains valid according to its rules.

### Isolation

Concurrent transactions should not improperly interfere with each other.

### Durability

Committed changes survive failures.

---

## Q78. What are isolation levels?

Common isolation levels:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Different databases may support additional levels or implement them differently.

---

## Q79. What are dirty reads?

A dirty read occurs when one transaction reads data that another transaction has changed but not committed.

---

## Q80. What is a deadlock?

A deadlock occurs when two or more transactions wait for each other indefinitely.

Example concept:

```text
Transaction A locks Resource 1
Transaction B locks Resource 2

A waits for Resource 2
B waits for Resource 1
```

Neither can proceed until the database detects and resolves the deadlock.

---

# 15. Views

## Q81. What is a view?

A view is a virtual table based on a query.

```sql
CREATE VIEW employee_details AS
SELECT name, salary
FROM employees;
```

Use:

```sql
SELECT *
FROM employee_details;
```

---

## Q82. Why use views?

Views can provide:

- Simpler queries
- Reusable logic
- Data abstraction
- Restricted access to selected columns/rows

---

## Q83. Table vs view

| Table | View |
|---|---|
| Stores data | Usually stores query definition |
| Physical database object | Virtual result based on query |
| Data exists independently | Depends on underlying objects |

---

# 16. Indexes

## Q84. What is an index?

An index is a database structure used to speed up data retrieval.

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

---

## Q85. Why are indexes useful?

They can improve query performance for operations such as:

```sql
WHERE
JOIN
ORDER BY
```

depending on the query and database design.

---

## Q86. What are disadvantages of indexes?

Indexes:

- Consume storage
- Can slow down INSERT
- Can slow down UPDATE
- Can slow down DELETE
- Need maintenance

---

## Q87. When should you create an index?

Consider columns frequently used in:

```text
WHERE conditions
JOIN conditions
ORDER BY
GROUP BY
```

But don't blindly index every column.

---

## Q88. What is a composite index?

An index created on multiple columns.

```sql
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

The order of columns in a composite index matters.

---

# 17. DELETE vs TRUNCATE vs DROP

## Q89. Difference between DELETE, TRUNCATE and DROP

| DELETE | TRUNCATE | DROP |
|---|---|---|
| Removes rows | Removes all rows | Removes table/object |
| Can use WHERE | Generally no WHERE | Table itself is removed |
| DML | Commonly treated as DDL in many systems | DDL |
| Structure remains | Structure remains | Structure removed |

Example:

```sql
DELETE FROM employees
WHERE department_id = 10;
```

```sql
TRUNCATE TABLE employees;
```

```sql
DROP TABLE employees;
```

> Exact transaction, logging, identity-reset, and rollback behavior can vary by database system.

---

# 18. UNION vs UNION ALL

## Q90. Difference between UNION and UNION ALL

### UNION

Combines results and removes duplicates.

```sql
SELECT name FROM employees_2025
UNION
SELECT name FROM employees_2026;
```

### UNION ALL

Combines results without removing duplicates.

```sql
SELECT name FROM employees_2025
UNION ALL
SELECT name FROM employees_2026;
```

`UNION ALL` is generally faster because duplicate elimination is not required.

---

# 19. SQL Query Execution Order

## Q91. What is the logical order of SQL query execution?

A common logical order is:

```text
FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
DISTINCT
ORDER BY
LIMIT / FETCH
```

Example:

```sql
SELECT department_id, COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department_id
HAVING COUNT(*) > 5
ORDER BY COUNT(*) DESC;
```

Conceptually:

```text
FROM/JOIN
   ↓
WHERE
   ↓
GROUP BY
   ↓
HAVING
   ↓
SELECT
   ↓
ORDER BY
```

---

## Q92. Why can't we normally use a SELECT alias in WHERE?

Because `WHERE` is logically evaluated before `SELECT`.

Example:

```sql
SELECT salary * 12 AS annual_salary
FROM employees
WHERE annual_salary > 600000;
```

This is not generally valid.

Use:

```sql
SELECT salary * 12 AS annual_salary
FROM employees
WHERE salary * 12 > 600000;
```

or a subquery/CTE.

---

# 20. Most Important SQL Coding Questions

# Q93. Find all employees with salary greater than 50000.

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

---

# Q94. Find employees whose name starts with 'A'.

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

---

# Q95. Find employees whose name ends with 'n'.

```sql
SELECT *
FROM employees
WHERE name LIKE '%n';
```

---

# Q96. Find the highest salary.

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

---

# Q97. Find the lowest salary.

```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```

---

# Q98. Find the average salary.

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

---

# Q99. Find the total salary.

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

---

# Q100. Count total employees.

```sql
SELECT COUNT(*) AS employee_count
FROM employees;
```

---

# Q101. Find the number of employees in each department.

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

---

# Q102. Find the average salary of each department.

```sql
SELECT department_id,
       AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

---

# Q103. Find departments whose average salary is greater than 60000.

```sql
SELECT department_id,
       AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 60000;
```

---

# Q104. Find the second highest salary.

### Method 1

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### Method 2 — DENSE_RANK

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) x
WHERE rnk = 2;
```

### Interview point

If duplicate salaries exist, clarify whether the interviewer wants the **second distinct highest salary**.

---

# Q105. Find the third highest salary.

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) x
WHERE rnk = 3;
```

---

# Q106. Find the top 3 salaries.

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

> Use the syntax appropriate for your database.

---

# Q107. Find employees earning more than the average salary.

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# Q108. Find employees earning more than their department's average salary.

```sql
SELECT e.*
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# Q109. Find the highest-paid employee.

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

# Q110. Find the highest-paid employee in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

---

# Q111. Find the second highest-paid employee in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk = 2;
```

---

# Q112. Find duplicate values in a column.

Example: duplicate emails.

```sql
SELECT email,
       COUNT(*) AS count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

---

# Q113. Find duplicate employee records based on name and salary.

```sql
SELECT name,
       salary,
       COUNT(*) AS count
FROM employees
GROUP BY name, salary
HAVING COUNT(*) > 1;
```

---

# Q114. Find employees who do not have a manager.

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

# Q115. Find employees who have a manager.

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

---

# Q116. Find employees belonging to a particular department.

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

---

# Q117. Find employees who don't belong to any department.

Using `LEFT JOIN`:

```sql
SELECT e.*
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

---

# Q118. Find departments that have no employees.

```sql
SELECT d.*
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

---

# Q119. Find the number of employees in each department including departments with zero employees.

```sql
SELECT d.department_id,
       d.department_name,
       COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id,
         d.department_name;
```

### Important interview point

Use:

```sql
COUNT(e.employee_id)
```

instead of:

```sql
COUNT(*)
```

when you want zero for departments with no matching employees.

---

# Q120. Find employees and their department names.

```sql
SELECT e.name,
       d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

---

# Q121. Find all employees including those without departments.

```sql
SELECT e.name,
       d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

---

# Q122. Find employees who earn more than their manager.

```sql
SELECT e.name AS employee,
       e.salary AS employee_salary,
       m.name AS manager,
       m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.salary > m.salary;
```

This is a common **SELF JOIN** interview problem.

---

# Q123. Find employees who earn the same salary.

```sql
SELECT e1.name,
       e1.salary
FROM employees e1
JOIN employees e2
    ON e1.salary = e2.salary
   AND e1.employee_id <> e2.employee_id;
```

A cleaner approach for identifying salary values with duplicates:

```sql
SELECT salary,
       COUNT(*) AS employee_count
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;
```

---

# Q124. Find the nth highest salary.

Using `DENSE_RANK()`:

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) x
WHERE rnk = 5;
```

Change `5` to the required rank.

---

# Q125. Find the top 3 employees by salary in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk <= 3;
```

---

# Q126. Find the employee with the maximum salary in each department using GROUP BY.

One approach is:

```sql
SELECT e.*
FROM employees e
JOIN (
    SELECT department_id,
           MAX(salary) AS max_salary
    FROM employees
    GROUP BY department_id
) x
    ON e.department_id = x.department_id
   AND e.salary = x.max_salary;
```

This can return multiple employees when there is a salary tie.

---

# Q127. Find employees who joined after 2023.

```sql
SELECT *
FROM employees
WHERE joining_date >= '2024-01-01';
```

Date literal syntax may vary by database.

---

# Q128. Find employees who joined in a particular year.

The exact function depends on the database.

For example:

```sql
SELECT *
FROM employees
WHERE EXTRACT(YEAR FROM joining_date) = 2024;
```

---

# Q129. Find the latest employee who joined.

```sql
SELECT *
FROM employees
ORDER BY joining_date DESC
LIMIT 1;
```

---

# Q130. Find the earliest employee who joined.

```sql
SELECT *
FROM employees
ORDER BY joining_date ASC
LIMIT 1;
```

---

# Q131. Find employees who joined on the same date.

```sql
SELECT joining_date,
       COUNT(*) AS employee_count
FROM employees
GROUP BY joining_date
HAVING COUNT(*) > 1;
```

---

# Q132. Find the latest employee in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY department_id
               ORDER BY joining_date DESC
           ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

---

# Q133. Find employees whose salary is between 50000 and 100000.

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 100000;
```

---

# Q134. Find employees from departments 10, 20 and 30.

```sql
SELECT *
FROM employees
WHERE department_id IN (10, 20, 30);
```

---

# Q135. Find employees whose name contains "an".

```sql
SELECT *
FROM employees
WHERE name LIKE '%an%';
```

---

# Q136. Convert employee names to uppercase.

```sql
SELECT UPPER(name) AS name
FROM employees;
```

---

# Q137. Find the length of each employee name.

```sql
SELECT name,
       LENGTH(name) AS name_length
FROM employees;
```

> Function names can differ across database systems.

---

# Q138. Replace NULL salary values with 0.

```sql
SELECT name,
       COALESCE(salary, 0) AS salary
FROM employees;
```

---

# 21. Window Function Interview Problems

# Q139. Add a row number to employees ordered by salary.

```sql
SELECT name,
       salary,
       ROW_NUMBER() OVER (
           ORDER BY salary DESC
       ) AS row_num
FROM employees;
```

---

# Q140. Rank employees by salary.

```sql
SELECT name,
       salary,
       RANK() OVER (
           ORDER BY salary DESC
       ) AS salary_rank
FROM employees;
```

---

# Q141. Rank employees within each department.

```sql
SELECT name,
       department_id,
       salary,
       RANK() OVER (
           PARTITION BY department_id
           ORDER BY salary DESC
       ) AS salary_rank
FROM employees;
```

---

# Q142. Find each employee's department average salary.

```sql
SELECT name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_avg
FROM employees;
```

---

# Q143. Find the difference between employee salary and department average.

```sql
SELECT name,
       department_id,
       salary,
       salary - AVG(salary) OVER (
           PARTITION BY department_id
       ) AS difference
FROM employees;
```

---

# Q144. Find the running total of salaries.

```sql
SELECT employee_id,
       name,
       salary,
       SUM(salary) OVER (
           ORDER BY employee_id
       ) AS running_total
FROM employees;
```

---

# Q145. Find the previous employee salary.

Use `LAG()`:

```sql
SELECT name,
       salary,
       LAG(salary) OVER (
           ORDER BY employee_id
       ) AS previous_salary
FROM employees;
```

---

# Q146. Find the next employee salary.

Use `LEAD()`:

```sql
SELECT name,
       salary,
       LEAD(salary) OVER (
           ORDER BY employee_id
       ) AS next_salary
FROM employees;
```

---

# Q147. What are LAG and LEAD?

### LAG

Accesses a previous row.

### LEAD

Accesses a following row.

Example:

```sql
SELECT employee_id,
       salary,
       LAG(salary) OVER (
           ORDER BY employee_id
       ) AS previous_salary,
       LEAD(salary) OVER (
           ORDER BY employee_id
       ) AS next_salary
FROM employees;
```

---

# 22. SQL Scenario-Based Questions

# Q148. A JOIN is producing duplicate rows. What could be the reason?

Possible reasons:

- One-to-many relationship
- Many-to-many relationship
- Incorrect JOIN condition
- Missing JOIN condition
- Joining on a non-unique column

First inspect the relationship between the tables.

Do not automatically solve every duplicate problem using:

```sql
DISTINCT
```

because that may hide an incorrect JOIN.

---

# Q149. A query is running slowly. How would you investigate?

Check:

1. Execution plan
2. Indexes
3. JOIN conditions
4. Filtering
5. Number of rows processed
6. Unnecessary columns
7. Functions applied to indexed columns
8. Sorting/grouping operations
9. Large scans
10. Data distribution

Use the database's execution-plan tools, such as `EXPLAIN` where supported.

---

# Q150. How can you improve SQL query performance?

Common approaches:

- Select only required columns
- Filter early where appropriate
- Use suitable indexes
- Avoid unnecessary joins
- Check JOIN conditions
- Avoid unnecessary `DISTINCT`
- Avoid unnecessary nested queries
- Review execution plans
- Use appropriate data types
- Avoid functions on indexed columns when they prevent efficient index usage
- Consider partitioning or other database-specific strategies for very large tables

---

# Q151. Why should we avoid SELECT *?

Instead of:

```sql
SELECT *
FROM employees;
```

prefer:

```sql
SELECT employee_id,
       name,
       salary
FROM employees;
```

Benefits:

- Less data transferred
- Better readability
- Avoids retrieving unnecessary columns
- More stable when table structure changes

---

# Q152. What happens if you forget the JOIN condition?

You can accidentally produce a Cartesian product.

Example:

```sql
SELECT *
FROM employees e
JOIN departments d;
```

Depending on SQL dialect, this may be invalid or effectively represent a Cartesian join if expressed as `CROSS JOIN`.

A Cartesian product can produce a huge number of rows.

---

# Q153. Why can LEFT JOIN become INNER JOIN accidentally?

Consider:

```sql
SELECT e.*, d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'IT';
```

The `WHERE` condition removes rows where `d.department_name` is `NULL`.

So unmatched rows disappear.

If you want to preserve unmatched employees, the condition may need to be placed in the `ON` clause:

```sql
SELECT e.*, d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
   AND d.department_name = 'IT';
```

---

# Q154. How would you remove duplicate rows?

First determine what makes a row a duplicate.

For duplicate values:

```sql
SELECT email,
       COUNT(*)
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

To keep one row and remove duplicates, a common approach is:

```sql
WITH duplicates AS (
    SELECT employee_id,
           ROW_NUMBER() OVER (
               PARTITION BY email
               ORDER BY employee_id
           ) AS rn
    FROM employees
)
DELETE FROM employees
WHERE employee_id IN (
    SELECT employee_id
    FROM duplicates
    WHERE rn > 1
);
```

> `DELETE` syntax involving CTEs can vary by database. Always adapt it to the SQL dialect being used.

---

# Q155. How do you find records present in one table but not another?

Using `LEFT JOIN`:

```sql
SELECT a.*
FROM table_a a
LEFT JOIN table_b b
    ON a.id = b.id
WHERE b.id IS NULL;
```

Another approach is `NOT EXISTS`:

```sql
SELECT a.*
FROM table_a a
WHERE NOT EXISTS (
    SELECT 1
    FROM table_b b
    WHERE b.id = a.id
);
```

---

# Q156. How do you find common records between two tables?

Using `INNER JOIN`:

```sql
SELECT a.*
FROM table_a a
INNER JOIN table_b b
    ON a.id = b.id;
```

Or, when supported and appropriate:

```sql
SELECT id FROM table_a
INTERSECT
SELECT id FROM table_b;
```

---

# 23. Frequently Asked Conceptual Questions

# Q157. What is the difference between SQL and MySQL?

**SQL** is a language used to work with relational databases.

**MySQL** is a relational database management system that uses SQL.

Similar examples of database systems include:

```text
MySQL
PostgreSQL
Oracle
SQL Server
```

---

# Q158. What is DBMS?

DBMS stands for **Database Management System**.

It is software used to create, store, manage, retrieve, and manipulate data.

---

# Q159. What is RDBMS?

RDBMS stands for **Relational Database Management System**.

It stores data in related tables.

---

# Q160. DBMS vs RDBMS

| DBMS | RDBMS |
|---|---|
| General database management system | Relational database management system |
| May not use relationships | Uses relationships between tables |
| Can have different storage models | Uses relational tables |

---

# Q161. What is a schema?

A schema defines the structure of database objects such as:

- Tables
- Columns
- Constraints
- Views
- Relationships

The exact meaning of "schema" can vary between database systems.

---

# Q162. What is referential integrity?

Referential integrity ensures that relationships between related tables remain valid.

Foreign keys are commonly used to enforce it.

Example:

```text
employees.department_id
        ↓
departments.department_id
```

An employee should not reference a department that does not exist, unless the database design permits a `NULL` relationship.

---

# Q163. What is data integrity?

Data integrity means maintaining accurate, valid, and consistent data.

Types include:

- Entity integrity
- Referential integrity
- Domain integrity

---

# Q164. What is a surrogate key?

A surrogate key is an artificial/system-generated key used to uniquely identify a row.

Example:

```text
employee_id = 101
```

It may have no business meaning.

---

# Q165. What is a natural key?

A natural key is a real-world attribute that can uniquely identify a record.

Example:

```text
email
passport_number
```

Whether a natural key is suitable depends on whether it is stable and reliably unique.

---

# Q166. What is a composite key?

A key consisting of multiple columns.

```sql
PRIMARY KEY (student_id, course_id)
```

It is useful when no single column uniquely identifies a record.

---

# 24. Common Tricky SQL Questions

# Q167. What is the difference between = NULL and IS NULL?

Incorrect:

```sql
WHERE salary = NULL;
```

Correct:

```sql
WHERE salary IS NULL;
```

`NULL` represents unknown/missing information and requires special comparison semantics.

---

# Q168. Does COUNT(column) count NULL values?

No.

```sql
COUNT(column)
```

counts non-NULL values.

```sql
COUNT(*)
```

counts rows.

---

# Q169. What happens to NULL in arithmetic?

Expressions involving `NULL` generally result in `NULL`.

Example:

```sql
salary + NULL
```

produces `NULL`.

Use:

```sql
salary + COALESCE(commission, 0)
```

when appropriate.

---

# Q170. Can a primary key contain NULL?

No.

A primary key must uniquely identify a row and cannot contain `NULL`.

---

# Q171. Can a foreign key contain NULL?

Yes, generally, unless the column also has a `NOT NULL` constraint.

Example:

```sql
manager_id INT
```

can represent an employee without a manager using `NULL`.

---

# Q172. Can a table have multiple primary keys?

A table can have only **one primary key constraint**.

However, that primary key can contain multiple columns.

```sql
PRIMARY KEY (student_id, course_id)
```

---

# Q173. Can a table have multiple UNIQUE constraints?

Yes.

Example:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE,
    username VARCHAR(50) UNIQUE
);
```

---

# Q174. WHERE vs ON in JOIN

`ON` defines how rows are matched during the JOIN.

`WHERE` filters the result after the JOIN logically occurs.

Example:

```sql
SELECT *
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE e.salary > 50000;
```

---

# Q175. HAVING vs WHERE

```text
WHERE  → filters rows
HAVING → filters groups
```

Example:

```sql
SELECT department_id,
       AVG(salary)
FROM employees
WHERE salary > 30000
GROUP BY department_id
HAVING AVG(salary) > 50000;
```

Here:

```text
WHERE → removes individual employees
HAVING → removes departments/groups
```

---

# Q176. UNION vs JOIN

### UNION

Combines results **vertically**.

```text
Table A rows
     +
Table B rows
```

### JOIN

Combines related columns **horizontally**.

```text
Table A columns + Table B columns
```

---

# Q177. DELETE vs TRUNCATE

`DELETE` can remove selected rows:

```sql
DELETE FROM employees
WHERE department_id = 10;
```

`TRUNCATE` removes all rows:

```sql
TRUNCATE TABLE employees;
```

Their logging, rollback, locking, and identity behavior can differ depending on the database.

---

# Q178. What is the difference between RANK and DENSE_RANK?

For:

```text
100
100
90
80
```

`RANK()`:

```text
1
1
3
4
```

`DENSE_RANK()`:

```text
1
1
2
3
```

---

# Q179. What is the difference between ROW_NUMBER and RANK?

For tied values:

```text
Salary
100
100
90
```

`ROW_NUMBER()`:

```text
1
2
3
```

`RANK()`:

```text
1
1
3
```

---

# Q180. Can window functions be used with GROUP BY?

Yes, but the query must respect SQL's grouping rules.

Example:

```sql
SELECT department_id,
       COUNT(*) AS employee_count,
       RANK() OVER (
           ORDER BY COUNT(*) DESC
       ) AS department_rank
FROM employees
GROUP BY department_id;
```

---

# 25. Practical Interview Scenarios

# Q181. You have 10 million rows. How would you optimize a query?

A good interview answer:

> "First I would inspect the execution plan to identify the expensive operation. Then I would check whether appropriate indexes exist for filtering and joining columns, avoid unnecessary columns and joins, filter efficiently, and check whether sorting or grouping is processing a large number of rows. I would then measure the query again after each change."

---

# Q182. An index exists, but the query is still slow. Why?

Possible reasons:

- The index is not selective enough
- The optimizer chooses a table scan
- The query applies a function to the indexed column
- The indexed columns don't match the query pattern
- Too many rows qualify
- Statistics may be outdated
- The bottleneck is elsewhere

Example:

```sql
WHERE YEAR(joining_date) = 2024
```

may prevent efficient use of an index on `joining_date` in some database systems.

A range predicate may be more index-friendly:

```sql
WHERE joining_date >= '2024-01-01'
  AND joining_date < '2025-01-01'
```

---

# Q183. How would you find the most frequently occurring value?

Example: most common department.

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
ORDER BY employee_count DESC
LIMIT 1;
```

---

# Q184. How would you find the second most frequently occurring value?

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
ORDER BY employee_count DESC
LIMIT 1 OFFSET 1;
```

> Syntax differs between SQL dialects.

---

# Q185. How do you find employees whose salary is greater than all employees in department 10?

```sql
SELECT *
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

---

# Q186. How do you find employees whose salary is greater than at least one employee in department 10?

```sql
SELECT *
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE department_id = 10
);
```

---

# 26. Important Query Patterns to Memorize

## Pattern 1 — Maximum value

```sql
SELECT MAX(salary)
FROM employees;
```

---

## Pattern 2 — Minimum value

```sql
SELECT MIN(salary)
FROM employees;
```

---

## Pattern 3 — Count by group

```sql
SELECT department_id,
       COUNT(*)
FROM employees
GROUP BY department_id;
```

---

## Pattern 4 — Filter groups

```sql
SELECT department_id,
       COUNT(*)
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

## Pattern 5 — Second highest distinct value

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

---

## Pattern 6 — Nth highest value

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) x
WHERE rnk = N;
```

---

## Pattern 7 — Top N per group

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk <= N;
```

---

## Pattern 8 — Find duplicates

```sql
SELECT column_name,
       COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

---

## Pattern 9 — Find records without a match

```sql
SELECT a.*
FROM table_a a
LEFT JOIN table_b b
    ON a.id = b.id
WHERE b.id IS NULL;
```

---

## Pattern 10 — Find records with a match

```sql
SELECT a.*
FROM table_a a
WHERE EXISTS (
    SELECT 1
    FROM table_b b
    WHERE b.id = a.id
);
```

---

## Pattern 11 — Highest value per group

```sql
SELECT *
FROM (
    SELECT t.*,
           ROW_NUMBER() OVER (
               PARTITION BY group_id
               ORDER BY value DESC
           ) AS rn
    FROM table_name t
) x
WHERE rn = 1;
```

---

## Pattern 12 — Running total

```sql
SELECT date,
       amount,
       SUM(amount) OVER (
           ORDER BY date
       ) AS running_total
FROM sales;
```

---

## Pattern 13 — Previous row

```sql
SELECT date,
       amount,
       LAG(amount) OVER (
           ORDER BY date
       ) AS previous_amount
FROM sales;
```

---

## Pattern 14 — Next row

```sql
SELECT date,
       amount,
       LEAD(amount) OVER (
           ORDER BY date
       ) AS next_amount
FROM sales;
```

---

# 27. SQL Interview Rapid-Fire Questions

These are useful for last-minute revision.

## Q187. What does SQL stand for?

**Structured Query Language.**

---

## Q188. What is a primary key?

A unique, non-NULL identifier for rows in a table.

---

## Q189. What is a foreign key?

A column or set of columns referencing a key in another table.

---

## Q190. What is normalization?

Organizing data to reduce redundancy and improve consistency.

---

## Q191. What is denormalization?

Intentionally introducing redundancy to improve read performance or simplify access in some designs.

---

## Q192. What is a JOIN?

Combines related rows from multiple tables.

---

## Q193. What is an INNER JOIN?

Returns matching rows from both tables.

---

## Q194. What is a LEFT JOIN?

Returns all rows from the left table and matching rows from the right.

---

## Q195. What is GROUP BY?

Groups rows based on one or more columns.

---

## Q196. What is HAVING?

Filters grouped results.

---

## Q197. What is WHERE?

Filters rows.

---

## Q198. What is DISTINCT?

Removes duplicate result rows.

---

## Q199. What is an index?

A data structure that can improve retrieval performance.

---

## Q200. What is a view?

A virtual table based on a query.

---

## Q201. What is a transaction?

A logical unit of database work.

---

## Q202. What does ACID stand for?

```text
Atomicity
Consistency
Isolation
Durability
```

---

## Q203. What is a subquery?

A query nested inside another query.

---

## Q204. What is a CTE?

A named temporary result set defined using `WITH`.

---

## Q205. What is a window function?

A function that calculates across related rows while retaining individual rows.

---

## Q206. What is ROW_NUMBER?

Assigns sequential numbers to rows.

---

## Q207. What is RANK?

Assigns ranks with gaps after ties.

---

## Q208. What is DENSE_RANK?

Assigns ranks without gaps after ties.

---

## Q209. What is NULL?

A missing/unknown value.

---

## Q210. How do you check NULL?

```sql
IS NULL
```

---

# 28. Questions Interviewers May Ask About Your Query

When you write a SQL query in an interview, be prepared for follow-up questions.

## Q211. Why did you use LEFT JOIN instead of INNER JOIN?

Explain based on whether unmatched rows from the left table must be preserved.

---

## Q212. Why did you use HAVING instead of WHERE?

Because the condition is applied to an aggregate/group.

Example:

```sql
HAVING COUNT(*) > 5
```

---

## Q213. Why did you use DENSE_RANK instead of ROW_NUMBER?

Use `DENSE_RANK()` when equal values should receive the same rank and you want distinct ranking levels.

Use `ROW_NUMBER()` when each row must receive a unique sequential number.

---

## Q214. Why did you use a CTE?

Usually because it makes a complex query easier to read, structure, and maintain.

---

## Q215. Why did you use a subquery?

Because the outer query needs the result of another query as a condition or intermediate result.

---

## Q216. Why did you use an index?

Because the column is frequently used for filtering, joining, or ordering and the index may reduce the amount of data that must be scanned.

---

# 29. Very Important Interview Problems to Practice Without Looking

Before an interview, you should be able to write these queries from memory:

```text
1. Find the highest salary.
2. Find the second highest salary.
3. Find the third highest salary.
4. Find the Nth highest salary.
5. Find duplicate records.
6. Find employees earning more than average salary.
7. Find employees earning more than their department average.
8. Find the highest-paid employee in each department.
9. Find the second-highest salary in each department.
10. Find the top 3 salaries in each department.
11. Count employees in each department.
12. Find departments with more than N employees.
13. Find departments with no employees.
14. Find employees without a department.
15. Find employees without a manager.
16. Find employees earning more than their manager.
17. Find employees with the same salary.
18. Find employees who joined most recently.
19. Find the latest employee in each department.
20. Find employees whose name starts with a particular letter.
21. Find employees within a salary range.
22. Find employees matching multiple departments.
23. Find records existing in one table but not another.
24. Find common records between two tables.
25. Remove duplicate records.
26. Rank employees by salary.
27. Rank employees within each department.
28. Calculate department average alongside each employee.
29. Calculate running totals.
30. Find previous/next row using LAG/LEAD.
```

---

# 30. Final SQL Interview Checklist

Before attending the interview, make sure you can explain and write examples for:

## SQL Fundamentals

- [ ] SQL
- [ ] DBMS
- [ ] RDBMS
- [ ] Tables
- [ ] Rows
- [ ] Columns
- [ ] Primary key
- [ ] Foreign key
- [ ] Candidate key
- [ ] Composite key
- [ ] NULL
- [ ] Constraints

## Filtering

- [ ] SELECT
- [ ] WHERE
- [ ] DISTINCT
- [ ] ORDER BY
- [ ] LIMIT / equivalent
- [ ] BETWEEN
- [ ] IN
- [ ] LIKE
- [ ] IS NULL
- [ ] COALESCE

## Aggregation

- [ ] COUNT
- [ ] SUM
- [ ] AVG
- [ ] MIN
- [ ] MAX
- [ ] GROUP BY
- [ ] HAVING
- [ ] WHERE vs HAVING
- [ ] COUNT(*) vs COUNT(column)

## Joins

- [ ] INNER JOIN
- [ ] LEFT JOIN
- [ ] RIGHT JOIN
- [ ] FULL OUTER JOIN
- [ ] CROSS JOIN
- [ ] SELF JOIN
- [ ] JOIN vs WHERE
- [ ] Duplicate rows after JOIN
- [ ] Finding unmatched records

## Advanced Querying

- [ ] Subqueries
- [ ] Correlated subqueries
- [ ] EXISTS
- [ ] IN
- [ ] CTE
- [ ] CASE WHEN
- [ ] UNION
- [ ] UNION ALL

## Window Functions

- [ ] OVER
- [ ] PARTITION BY
- [ ] ROW_NUMBER
- [ ] RANK
- [ ] DENSE_RANK
- [ ] LAG
- [ ] LEAD
- [ ] Running total
- [ ] Top N per group

## Database Design

- [ ] Keys
- [ ] Constraints
- [ ] 1NF
- [ ] 2NF
- [ ] 3NF
- [ ] Referential integrity
- [ ] Normalization
- [ ] Denormalization

## Performance

- [ ] Indexes
- [ ] Composite indexes
- [ ] Query optimization
- [ ] Execution plans
- [ ] SELECT *
- [ ] JOIN performance
- [ ] Index limitations

## Transactions

- [ ] Transaction
- [ ] COMMIT
- [ ] ROLLBACK
- [ ] ACID
- [ ] Isolation levels
- [ ] Dirty reads
- [ ] Deadlocks

## Objects

- [ ] Views
- [ ] Stored procedures
- [ ] Functions
- [ ] Triggers
- [ ] Temporary tables

---

# 31. Final Priority — What to Study First

If you have **very limited time**, do not try to memorize every SQL feature equally.

Focus heavily on these:

### Priority 1 — Absolutely Must Know

```text
SELECT
WHERE
GROUP BY
HAVING
ORDER BY
COUNT
SUM
AVG
MIN
MAX
JOIN
INNER JOIN
LEFT JOIN
Subqueries
CASE WHEN
NULL
Primary Key
Foreign Key
```

### Priority 2 — Very Important

```text
CTE
ROW_NUMBER
RANK
DENSE_RANK
PARTITION BY
LAG
LEAD
UNION
UNION ALL
EXISTS
Indexes
Normalization
Transactions
ACID
Views
```

### Priority 3 — Practice Coding

```text
Second highest salary
Nth highest salary
Duplicate records
Highest salary per department
Top 3 per department
Employees above average
Employees above department average
Employees earning more than manager
Departments with no employees
Employees without departments
Running total
Ranking
Previous/next record
```

---

# 32. The 15 Questions You Should Never Go Into an SQL Interview Without Knowing

If you can answer these confidently and write the queries without much help, your SQL interview preparation is in a strong position.

## 1. What is SQL and what is RDBMS?

## 2. Primary key vs foreign key?

## 3. WHERE vs HAVING?

## 4. INNER JOIN vs LEFT JOIN?

## 5. What are GROUP BY and aggregate functions?

## 6. COUNT(*) vs COUNT(column)?

## 7. What is NULL and how do you handle it?

## 8. What is a subquery?

## 9. What is a CTE?

## 10. What are window functions?

## 11. ROW_NUMBER vs RANK vs DENSE_RANK?

## 12. Find the second highest salary.

```sql
SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) x
WHERE rnk = 2;
```

## 13. Find the highest-paid employee in each department.

```sql
SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

## 14. Find duplicate records.

```sql
SELECT email,
       COUNT(*) AS count
FROM employees
GROUP BY email
HAVING COUNT(*) > 1;
```

## 15. Explain how you would optimize a slow SQL query.

A strong answer should mention:

```text
Execution plan
Indexes
JOIN conditions
Filtering
Rows scanned
Unnecessary columns
Sorting/grouping
Query structure
Database statistics
```

---

# Final Preparation Strategy

Do **not** spend equal effort on every question in this file.

Use this file as your **final SQL interview revision sheet**.

For each important topic, follow this pattern:

```text
1. Understand the concept
        ↓
2. Understand one simple example
        ↓
3. Write the query yourself
        ↓
4. Modify the query for a different requirement
        ↓
5. Explain your query verbally
```

For example, don't just memorize:

```sql
DENSE_RANK()
```

Be able to explain:

> "`DENSE_RANK()` assigns the same rank to tied values and does not leave gaps. I can use it for problems such as finding the second-highest distinct salary."

Then write:

```sql
SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
) x
WHERE rnk = 2;
```

That combination of **concept + explanation + query writing** is much more useful in an interview than memorizing definitions alone.

---

# SQL Interview Readiness Target

You do **not** need to memorize every SQL feature in existence.

Your practical target should be:

```text
Can I understand a given schema?
        ↓
Can I identify relationships between tables?
        ↓
Can I write SELECT + WHERE?
        ↓
Can I aggregate with GROUP BY + HAVING?
        ↓
Can I JOIN multiple tables?
        ↓
Can I solve problems using subqueries / CTEs?
        ↓
Can I use CASE WHEN?
        ↓
Can I solve ranking problems using window functions?
        ↓
Can I handle NULLs correctly?
        ↓
Can I explain keys, normalization and constraints?
        ↓
Can I explain transactions and ACID?
        ↓
Can I explain indexes and basic optimization?
        ↓
Can I solve common interview SQL problems?
```

If you can confidently do all of the above, you have covered the **main SQL knowledge normally expected for a general software/data-oriented interview**, rather than wasting time trying to learn every advanced database feature.