# SQL Query Interview Problems

## 1. Introduction

This file contains the most important **SQL query-based interview problems** that are commonly useful for fresher and entry-level interviews.

The goal is not just to memorize queries.

For each problem, understand:

- What the question is asking
- Which SQL concept is being tested
- How the query works
- Why that particular approach is used
- Possible alternative approaches

The most important concepts covered here are:

```text
WHERE
DISTINCT
ORDER BY
LIMIT / TOP
Aggregate Functions
GROUP BY
HAVING
JOINS
SUBQUERIES
CTEs
CASE
WINDOW FUNCTIONS
ROW_NUMBER()
RANK()
DENSE_RANK()
LEAD()
LAG()
NULL handling
Duplicates
Second highest salary
Nth highest salary
Top N records
Department-wise problems
Employee-manager problems
Date-based problems
```

---

# 2. Sample Tables Used in the Problems

Most questions in this file use the following conceptual tables.

## employees

| employee_id | employee_name | department_id | salary | manager_id | hire_date |
|---:|---|---:|---:|---:|---|
| 1 | Alice | 10 | 60000 | NULL | 2022-01-10 |
| 2 | Bob | 20 | 75000 | 1 | 2021-05-15 |
| 3 | Charlie | 10 | 80000 | 1 | 2020-03-20 |
| 4 | David | 30 | 55000 | 2 | 2023-07-10 |
| 5 | Emma | 20 | 90000 | 2 | 2019-11-05 |
| 6 | Frank | 10 | 80000 | 1 | 2021-08-12 |

## departments

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |
| 30 | Finance |
| 40 | Sales |

---

# 3. Find All Employees

### Question

Write a query to display all employees.

### Answer

```sql
SELECT *
FROM employees;
```

### Concept

Basic `SELECT`.

---

# 4. Select Specific Columns

### Question

Display employee names and salaries.

### Answer

```sql
SELECT employee_name, salary
FROM employees;
```

---

# 5. Find Employees With Salary Greater Than 60000

### Question

Find employees whose salary is greater than 60000.

### Answer

```sql
SELECT *
FROM employees
WHERE salary > 60000;
```

### Concept

```text
SELECT
WHERE
Comparison operator
```

---

# 6. Find Employees With Salary Between Two Values

### Question

Find employees whose salary is between 60000 and 80000.

### Answer

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 60000 AND 80000;
```

`BETWEEN` is inclusive in standard SQL usage.

---

# 7. Find Employees From a Specific Department

### Question

Find employees working in department 10.

### Answer

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

---

# 8. Find Employees From Multiple Departments

### Question

Find employees from departments 10 and 20.

### Answer

```sql
SELECT *
FROM employees
WHERE department_id IN (10, 20);
```

Alternative:

```sql
SELECT *
FROM employees
WHERE department_id = 10
   OR department_id = 20;
```

---

# 9. Find Employees Whose Name Starts With A

### Question

Find employees whose name starts with `A`.

### Answer

```sql
SELECT *
FROM employees
WHERE employee_name LIKE 'A%';
```

### Pattern

```text
A%
```

means:

```text
Starts with A
```

---

# 10. Find Employees Whose Name Ends With A

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%a';
```

---

# 11. Find Employees Whose Name Contains A

```sql
SELECT *
FROM employees
WHERE employee_name LIKE '%a%';
```

---

# 12. Find Distinct Department IDs

### Question

Display unique department IDs.

### Answer

```sql
SELECT DISTINCT department_id
FROM employees;
```

---

# 13. Count Total Employees

### Question

Find the total number of employees.

### Answer

```sql
SELECT COUNT(*) AS total_employees
FROM employees;
```

---

# 14. Find Maximum Salary

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

---

# 15. Find Minimum Salary

```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```

---

# 16. Find Average Salary

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

---

# 17. Find Total Salary

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

---

# 18. Find Second Highest Salary

This is one of the **most frequently asked SQL interview questions**.

## Method 1 — Subquery

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### How it works

Inner query:

```sql
SELECT MAX(salary)
FROM employees;
```

finds the highest salary.

Then:

```sql
WHERE salary < highest_salary
```

removes the highest salary.

Finally:

```sql
MAX(salary)
```

finds the highest remaining salary.

---

# 19. Second Highest Salary Using DISTINCT

```sql
SELECT MAX(salary) AS second_highest_salary
FROM (
    SELECT DISTINCT salary
    FROM employees
) AS s
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

The important idea is handling duplicate salary values.

---

# 20. Second Highest Salary Using ORDER BY

Some databases support:

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;
```

This syntax is common in MySQL and PostgreSQL.

SQL Server commonly uses:

```sql
SELECT DISTINCT TOP 1 salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
)
ORDER BY salary DESC;
```

Syntax varies by database.

---

# 21. Find Nth Highest Salary

A common interview requirement is:

> Find the 3rd highest salary.

Using `DENSE_RANK()`:

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) AS ranked
WHERE rnk = 3;
```

### Why DENSE_RANK?

Suppose salaries are:

```text
90000
80000
80000
75000
60000
```

Dense ranks are:

```text
90000 → 1
80000 → 2
80000 → 2
75000 → 3
60000 → 4
```

So the 3rd highest **distinct** salary is:

```text
75000
```

---

# 22. Top 3 Salaries

### Question

Find the top 3 distinct salaries.

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

For SQL Server:

```sql
SELECT DISTINCT TOP 3 salary
FROM employees
ORDER BY salary DESC;
```

---

# 23. Find Employees With the Highest Salary

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

### Why use `=` instead of `>`?

Because multiple employees can have the same highest salary.

---

# 24. Find Employees With the Lowest Salary

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MIN(salary)
    FROM employees
);
```

---

# 25. Find Employees Earning More Than Average Salary

### Question

Find employees whose salary is greater than the company average.

### Answer

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

### Concept

Aggregate subquery.

---

# 26. Find Employees Earning Less Than Average Salary

```sql
SELECT *
FROM employees
WHERE salary < (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 27. Find Department-Wise Employee Count

### Question

Find the number of employees in each department.

### Answer

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

---

# 28. Find Department-Wise Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

---

# 29. Find Department With More Than 2 Employees

### Question

Find departments having more than 2 employees.

### Answer

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

### Important

Use:

```sql
WHERE
```

for row-level filtering.

Use:

```sql
HAVING
```

for filtering grouped/aggregate results.

---

# 30. Find Departments With Average Salary Greater Than 70000

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```

---

# 31. Find Highest Salary in Each Department

This is another **very important interview question**.

### Method 1 — GROUP BY

```sql
SELECT
    department_id,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department_id;
```

This gives the highest salary value per department.

---

# 32. Find Employee Details of Highest Paid Employee in Each Department

A simple `GROUP BY` only returns the salary.

To return employee details, use a window function.

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk = 1;
```

### Why `DENSE_RANK()`?

If two employees have the same highest salary in a department, both employees are returned.

---

# 33. Find Second Highest Salary in Each Department

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk = 2;
```

---

# 34. Find Top 3 Employees in Each Department

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk <= 3;
```

### Important Concept

```text
PARTITION BY department_id
```

means ranking starts separately for every department.

---

# 35. ROW_NUMBER vs RANK vs DENSE_RANK

Suppose salaries are:

```text
90000
80000
80000
70000
```

### ROW_NUMBER

```text
90000 → 1
80000 → 2
80000 → 3
70000 → 4
```

Every row gets a unique number.

### RANK

```text
90000 → 1
80000 → 2
80000 → 2
70000 → 4
```

Ranks have gaps after ties.

### DENSE_RANK

```text
90000 → 1
80000 → 2
80000 → 2
70000 → 3
```

Ranks do not have gaps.

---

# 36. Find Duplicate Salaries

```sql
SELECT
    salary,
    COUNT(*) AS salary_count
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;
```

---

# 37. Find Duplicate Employee Names

```sql
SELECT
    employee_name,
    COUNT(*) AS name_count
FROM employees
GROUP BY employee_name
HAVING COUNT(*) > 1;
```

---

# 38. Find Duplicate Rows

If a particular combination should be unique:

```sql
SELECT
    employee_name,
    department_id,
    salary,
    COUNT(*) AS duplicate_count
FROM employees
GROUP BY
    employee_name,
    department_id,
    salary
HAVING COUNT(*) > 1;
```

---

# 39. Find Employees Without a Manager

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

### Important

Do not write:

```sql
WHERE manager_id = NULL;
```

Use:

```sql
IS NULL
```

---

# 40. Find Employees With a Manager

```sql
SELECT *
FROM employees
WHERE manager_id IS NOT NULL;
```

---

# 41. INNER JOIN Employees and Departments

### Question

Display employee name and department name.

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 42. LEFT JOIN Employees and Departments

```sql
SELECT
    e.employee_name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

This keeps all employees even if a matching department does not exist.

---

# 43. Find Employees Whose Department Does Not Exist

Using `LEFT JOIN`:

```sql
SELECT
    e.employee_id,
    e.employee_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

### Concept

```text
LEFT JOIN
+
IS NULL
```

is a common pattern for finding unmatched rows.

---

# 44. Find Departments With No Employees

```sql
SELECT
    d.department_id,
    d.department_name
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

---

# 45. SELF JOIN — Employee and Manager

A self join joins a table with itself.

### Question

Display employee name and manager name.

```sql
SELECT
    e.employee_name AS employee,
    m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

### Important Concept

The same table is referenced twice:

```text
employees e
employees m
```

---

# 46. Find Employees Earning More Than Their Manager

This is a common interview problem.

```sql
SELECT
    e.employee_name AS employee,
    e.salary AS employee_salary,
    m.employee_name AS manager,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.salary > m.salary;
```

---

# 47. Find Employees Earning Less Than Their Manager

```sql
SELECT
    e.employee_name AS employee,
    e.salary AS employee_salary,
    m.employee_name AS manager,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.salary < m.salary;
```

---

# 48. Find Employees With the Same Salary

```sql
SELECT
    e1.employee_name AS employee_1,
    e2.employee_name AS employee_2,
    e1.salary
FROM employees e1
JOIN employees e2
    ON e1.salary = e2.salary
   AND e1.employee_id < e2.employee_id;
```

The condition:

```sql
e1.employee_id < e2.employee_id
```

prevents:

```text
Alice - Bob
Bob - Alice
```

from both appearing.

---

# 49. Find Employees in the IT Department

Using a join:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.salary
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'IT';
```

---

# 50. Find Employees Not in the IT Department

```sql
SELECT
    e.employee_id,
    e.employee_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_name <> 'IT';
```

---

# 51. Find Departments With Average Salary Above Company Average

```sql
SELECT
    department_id,
    AVG(salary) AS department_average
FROM employees
GROUP BY department_id
HAVING AVG(salary) > (
    SELECT AVG(salary)
    FROM employees
);
```

### Important Concept

Aggregate result compared with another aggregate result.

---

# 52. Find Employees Who Earn More Than Their Department Average

This is an important interview problem.

Using a correlated subquery:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

### Logic

For each employee:

```text
Find that employee's department
        ↓
Calculate department average
        ↓
Compare employee salary
```

---

# 53. Find Employees With the Same Department as Alice

```sql
SELECT *
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE employee_name = 'Alice'
);
```

---

# 54. Find Employees With Salary Greater Than Alice

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT salary
    FROM employees
    WHERE employee_name = 'Alice'
);
```

---

# 55. Find Employees Hired After Alice

```sql
SELECT *
FROM employees
WHERE hire_date > (
    SELECT hire_date
    FROM employees
    WHERE employee_name = 'Alice'
);
```

---

# 56. Find the Latest Hired Employee

```sql
SELECT *
FROM employees
WHERE hire_date = (
    SELECT MAX(hire_date)
    FROM employees
);
```

---

# 57. Find the Earliest Hired Employee

```sql
SELECT *
FROM employees
WHERE hire_date = (
    SELECT MIN(hire_date)
    FROM employees
);
```

---

# 58. Find Employees Hired in a Particular Year

Database-specific date functions vary.

For systems supporting `EXTRACT`:

```sql
SELECT *
FROM employees
WHERE EXTRACT(YEAR FROM hire_date) = 2023;
```

Another common approach is a date range:

```sql
SELECT *
FROM employees
WHERE hire_date >= '2023-01-01'
  AND hire_date < '2024-01-01';
```

The range approach can be preferable for indexed date columns because it can avoid applying a function directly to the column.

---

# 59. Find Employees Hired After 2022

```sql
SELECT *
FROM employees
WHERE hire_date >= '2023-01-01';
```

---

# 60. Find Employees Hired Before 2020

```sql
SELECT *
FROM employees
WHERE hire_date < '2020-01-01';
```

---

# 61. Find Number of Employees Hired Each Year

Using a database-specific year extraction function:

```sql
SELECT
    EXTRACT(YEAR FROM hire_date) AS hire_year,
    COUNT(*) AS employee_count
FROM employees
GROUP BY EXTRACT(YEAR FROM hire_date)
ORDER BY hire_year;
```

Date functions vary between databases.

---

# 62. Find Highest Salary in Each Department Using a CTE

```sql
WITH department_salary AS (
    SELECT
        department_id,
        MAX(salary) AS highest_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM department_salary;
```

---

# 63. Find Employees With Highest Salary in Each Department Using CTE

```sql
WITH ranked_employees AS (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
)
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM ranked_employees
WHERE rnk = 1;
```

---

# 64. Find Employees Whose Salary Is Above Average Using CTE

```sql
WITH average_salary AS (
    SELECT AVG(salary) AS avg_salary
    FROM employees
)
SELECT
    e.employee_id,
    e.employee_name,
    e.salary
FROM employees e
CROSS JOIN average_salary a
WHERE e.salary > a.avg_salary;
```

---

# 65. Use CASE to Categorize Salaries

### Question

Categorize employees as:

```text
High → salary >= 80000
Medium → salary >= 60000
Low → otherwise
```

### Answer

```sql
SELECT
    employee_name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 66. Count Employees in Each Salary Category

```sql
SELECT
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END;
```

Some DBMSs also allow grouping by the alias, but that behavior varies.

---

# 67. Find Employees Whose Salary Is NULL

```sql
SELECT *
FROM employees
WHERE salary IS NULL;
```

---

# 68. Replace NULL Salary With 0

Using `COALESCE`:

```sql
SELECT
    employee_name,
    COALESCE(salary, 0) AS salary
FROM employees;
```

`COALESCE` returns the first non-NULL expression.

---

# 69. Find Number of Employees With NULL Manager

```sql
SELECT COUNT(*) AS employees_without_manager
FROM employees
WHERE manager_id IS NULL;
```

---

# 70. Find Employees With NULL Department

```sql
SELECT *
FROM employees
WHERE department_id IS NULL;
```

---

# 71. Find Employees Who Belong to a Department

Using `EXISTS`:

```sql
SELECT *
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
);
```

---

# 72. Find Employees Who Do Not Belong to Any Existing Department

Using `NOT EXISTS`:

```sql
SELECT *
FROM employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
);
```

---

# 73. EXISTS vs IN

Both can be used for certain membership checks.

Example using `IN`:

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
);
```

Using `EXISTS`:

```sql
SELECT *
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
);
```

The optimizer may transform queries internally, but `EXISTS` is particularly natural when the question is whether a matching row exists.

---

# 74. Find Departments With at Least One Employee

Using `EXISTS`:

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

# 75. Find Departments With No Employees

Using `NOT EXISTS`:

```sql
SELECT *
FROM departments d
WHERE NOT EXISTS (
    SELECT 1
    FROM employees e
    WHERE e.department_id = d.department_id
);
```

---

# 76. Find the Highest Paid Employee Using ORDER BY

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 1;
```

For SQL Server:

```sql
SELECT TOP 1 *
FROM employees
ORDER BY salary DESC;
```

If ties must all be returned, use a different approach such as `DENSE_RANK()` or a `MAX()` subquery.

---

# 77. Find the Lowest Paid Employee

```sql
SELECT *
FROM employees
ORDER BY salary ASC
LIMIT 1;
```

---

# 78. Find Top 5 Highest Paid Employees

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

For SQL Server:

```sql
SELECT TOP 5 *
FROM employees
ORDER BY salary DESC;
```

---

# 79. Find Top 5 Distinct Salaries

```sql
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

---

# 80. Find Employees Ranked by Salary

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 81. Find Employees With Their Salary Rank Without Gaps

Use:

```sql
SELECT
    employee_id,
    employee_name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 82. Find Each Employee's Previous Salary

If salary history existed in a table with multiple salary records per employee, `LAG()` could be used.

Example conceptual query:

```sql
SELECT
    employee_id,
    salary,
    LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS previous_salary
FROM employee_salary_history;
```

### Concept

```text
LAG()
→ Previous row
```

---

# 83. Find Each Employee's Next Salary

```sql
SELECT
    employee_id,
    salary,
    LEAD(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS next_salary
FROM employee_salary_history;
```

### Concept

```text
LEAD()
→ Next row
```

---

# 84. Find Salary Difference From Previous Record

```sql
SELECT
    employee_id,
    salary,
    salary - LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS salary_difference
FROM employee_salary_history;
```

---

# 85. Find Running Total

Suppose an `orders` table contains:

```text
order_date
amount
```

Query:

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

# 86. Find Department-Wise Running Salary Total

```sql
SELECT
    employee_id,
    department_id,
    salary,
    SUM(salary) OVER (
        PARTITION BY department_id
        ORDER BY employee_id
    ) AS running_department_salary
FROM employees;
```

---

# 87. Find Average Salary Along With Each Employee

```sql
SELECT
    employee_name,
    department_id,
    salary,
    AVG(salary) OVER () AS company_average
FROM employees;
```

Unlike `GROUP BY`, the window function keeps individual employee rows.

---

# 88. Find Department Average Along With Each Employee

```sql
SELECT
    employee_name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average
FROM employees;
```

This is a very useful window-function pattern.

---

# 89. Find Employees Earning Above Their Department Average Using Window Function

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees
) AS e
WHERE salary > department_average;
```

---

# 90. Find Top 2 Salaries Per Department

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk <= 2;
```

---

# 91. Find the Most Recent Employee in Each Department

Using `ROW_NUMBER()`:

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    hire_date
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        hire_date,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY hire_date DESC
        ) AS rn
    FROM employees
) AS ranked
WHERE rn = 1;
```

### Why ROW_NUMBER?

We want exactly one employee per department.

---

# 92. Find the Earliest Employee in Each Department

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    hire_date
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        hire_date,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY hire_date
        ) AS rn
    FROM employees
) AS ranked
WHERE rn = 1;
```

---

# 93. Find Employees With the Same Department and Salary

```sql
SELECT
    department_id,
    salary,
    COUNT(*) AS employee_count
FROM employees
GROUP BY
    department_id,
    salary
HAVING COUNT(*) > 1;
```

---

# 94. Find Department With Highest Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
ORDER BY average_salary DESC
LIMIT 1;
```

For SQL Server:

```sql
SELECT TOP 1
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
ORDER BY average_salary DESC;
```

If ties must all be returned, use ranking instead of limiting to one row.

---

# 95. Find Department With Maximum Total Salary

```sql
SELECT
    department_id,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department_id
ORDER BY total_salary DESC
LIMIT 1;
```

---

# 96. Find Department With Maximum Number of Employees

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
ORDER BY employee_count DESC
LIMIT 1;
```

---

# 97. Find Employees Who Are Managers

An employee is a manager if their employee ID appears as another employee's manager ID.

```sql
SELECT DISTINCT
    m.employee_id,
    m.employee_name
FROM employees m
JOIN employees e
    ON m.employee_id = e.manager_id;
```

---

# 98. Find Number of Employees Reporting to Each Manager

```sql
SELECT
    manager_id,
    COUNT(*) AS employee_count
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id;
```

To show manager names:

```sql
SELECT
    m.employee_name AS manager,
    COUNT(e.employee_id) AS employee_count
FROM employees m
JOIN employees e
    ON m.employee_id = e.manager_id
GROUP BY
    m.employee_id,
    m.employee_name;
```

---

# 99. Find Manager With the Most Employees

```sql
SELECT
    m.employee_name AS manager,
    COUNT(e.employee_id) AS employee_count
FROM employees m
JOIN employees e
    ON m.employee_id = e.manager_id
GROUP BY
    m.employee_id,
    m.employee_name
ORDER BY employee_count DESC
LIMIT 1;
```

---

# 100. Find Employees Who Have No Direct Reports

```sql
SELECT
    e.employee_id,
    e.employee_name
FROM employees e
LEFT JOIN employees sub
    ON e.employee_id = sub.manager_id
WHERE sub.employee_id IS NULL;
```

---

# 101. UNION vs UNION ALL Query Problem

Suppose two queries return employee IDs.

```sql
SELECT employee_id
FROM employees
WHERE department_id = 10

UNION

SELECT employee_id
FROM employees
WHERE salary > 80000;
```

`UNION` removes duplicate rows.

Using:

```sql
UNION ALL
```

keeps duplicates.

---

# 102. Find Employees Belonging to Either of Two Conditions

Using `UNION`:

```sql
SELECT employee_id
FROM employees
WHERE department_id = 10

UNION

SELECT employee_id
FROM employees
WHERE salary > 80000;
```

This returns unique employee IDs.

---

# 103. Find Employees Common to Two Conditions

In databases supporting `INTERSECT`:

```sql
SELECT employee_id
FROM employees
WHERE department_id = 10

INTERSECT

SELECT employee_id
FROM employees
WHERE salary > 80000;
```

This returns employees satisfying both query result sets.

Support and syntax can vary by database.

---

# 104. Find Employees in One Result but Not Another

In databases supporting `EXCEPT`:

```sql
SELECT employee_id
FROM employees
WHERE department_id = 10

EXCEPT

SELECT employee_id
FROM employees
WHERE salary > 80000;
```

This returns IDs appearing in the first result but not the second.

Some databases use:

```text
MINUS
```

instead of:

```text
EXCEPT
```

---

# 105. Count Employees Per Department Including Empty Departments

This is an important `LEFT JOIN` problem.

```sql
SELECT
    d.department_id,
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY
    d.department_id,
    d.department_name;
```

### Important

Use:

```sql
COUNT(e.employee_id)
```

rather than:

```sql
COUNT(*)
```

because `COUNT(*)` would count the department row even when no employee matches.

---

# 106. Find Average Salary Per Department With Department Name

```sql
SELECT
    d.department_name,
    AVG(e.salary) AS average_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_name;
```

---

# 107. Find Highest Salary Per Department With Department Name

```sql
SELECT
    d.department_name,
    MAX(e.salary) AS highest_salary
FROM departments d
JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_name;
```

---

# 108. Find Employees From Departments With More Than 2 Employees

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING COUNT(*) > 2
);
```

---

# 109. Find Employees From the Department With the Highest Average Salary

```sql
WITH department_avg AS (
    SELECT
        department_id,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department_id
),
ranked AS (
    SELECT
        department_id,
        average_salary,
        DENSE_RANK() OVER (
            ORDER BY average_salary DESC
        ) AS rnk
    FROM department_avg
)
SELECT *
FROM ranked
WHERE rnk = 1;
```

---

# 110. Find Employees Who Earn the Highest Salary in Their Department

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

This is a **correlated subquery**.

---

# 111. Find Employees Who Earn the Second Highest Salary in Their Department

Using `DENSE_RANK()`:

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk = 2;
```

---

# 112. Find Employees With Salary Higher Than at Least One Employee in Another Department

A conceptual solution can use `ANY` where supported:

```sql
SELECT *
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE department_id = 20
);
```

This means the employee's salary is greater than at least one salary returned by the subquery.

Support and exact semantics should be checked for the specific DBMS.

---

# 113. Find Employees With Salary Higher Than Every Employee in Another Department

Using `ALL` where supported:

```sql
SELECT *
FROM employees
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE department_id = 20
);
```

This means the employee's salary is greater than every salary returned by the subquery.

---

# 114. Find Employees Who Were Hired Before Their Manager

```sql
SELECT
    e.employee_name AS employee,
    e.hire_date AS employee_hire_date,
    m.employee_name AS manager,
    m.hire_date AS manager_hire_date
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.hire_date < m.hire_date;
```

---

# 115. Find Employees Who Were Hired After Their Manager

```sql
SELECT
    e.employee_name AS employee,
    e.hire_date AS employee_hire_date,
    m.employee_name AS manager,
    m.hire_date AS manager_hire_date
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.hire_date > m.hire_date;
```

---

# 116. Find Employees Whose Salary Is Above Department Average

### Correlated Subquery

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

### Window Function

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees
) AS x
WHERE salary > department_average;
```

### Interview Point

Both approaches can solve the problem.

The window-function approach is often convenient when you need to keep row-level details together with aggregate information.

---

# 117. Find the Nth Highest Salary — General Pattern

A reusable pattern is:

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk = N;
```

Replace:

```text
N
```

with the required rank.

For example, 4th highest:

```sql
WHERE rnk = 4;
```

---

# 118. Top N Per Group — General Pattern

This is one of the most useful SQL interview patterns.

```sql
SELECT *
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS ranked
WHERE rnk <= N;
```

Replace:

```text
N
```

with the required number.

---

# 119. Find Duplicate Records and Keep One Row

A common approach uses `ROW_NUMBER()`.

Suppose duplicates are defined by:

```text
employee_name
department_id
salary
```

Query:

```sql
SELECT *
FROM (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY
                employee_name,
                department_id,
                salary
            ORDER BY employee_id
        ) AS rn
    FROM employees
) AS x
WHERE rn > 1;
```

This identifies rows beyond the first occurrence of each duplicate group.

---

# 120. Delete Duplicate Records

A common pattern, supported with syntax variations across DBMSs, is:

```sql
WITH duplicates AS (
    SELECT
        employee_id,
        ROW_NUMBER() OVER (
            PARTITION BY
                employee_name,
                department_id,
                salary
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

### Important

Never execute a duplicate-delete query directly on production data without first verifying the rows selected for deletion.

First run:

```sql
SELECT *
FROM (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY
                employee_name,
                department_id,
                salary
            ORDER BY employee_id
        ) AS rn
    FROM employees
) AS x
WHERE rn > 1;
```

to verify the intended rows.

Exact `DELETE` behavior with CTEs varies by DBMS.

---

# 121. Find Employees With Salary Between Department Minimum and Maximum

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM employees e
WHERE salary BETWEEN
    (
        SELECT MIN(e2.salary)
        FROM employees e2
        WHERE e2.department_id = e.department_id
    )
    AND
    (
        SELECT MAX(e3.salary)
        FROM employees e3
        WHERE e3.department_id = e.department_id
    );
```

Note that this condition is naturally true for all non-NULL salaries in the employee's department; the pattern is mainly useful for understanding correlated aggregate subqueries.

---

# 122. Find Departments With More Than One Employee

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 1;
```

---

# 123. Find Departments With Exactly One Employee

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) = 1;
```

---

# 124. Find Employees With Unique Salaries

```sql
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) = 1
);
```

---

# 125. Find the Most Common Salary

```sql
SELECT
    salary,
    COUNT(*) AS salary_count
FROM employees
GROUP BY salary
ORDER BY salary_count DESC
LIMIT 1;
```

---

# 126. Find Employees Whose Names Have More Than 5 Characters

The exact string-length function varies by database.

Common SQL form:

```sql
SELECT *
FROM employees
WHERE LENGTH(employee_name) > 5;
```

SQL Server commonly uses:

```sql
SELECT *
FROM employees
WHERE LEN(employee_name) > 5;
```

---

# 127. Find Employees Whose Names Start and End With the Same Character

A database-specific string expression is required.

For databases supporting `LEFT`, `RIGHT`, and `LENGTH`:

```sql
SELECT *
FROM employees
WHERE LOWER(LEFT(employee_name, 1)) =
      LOWER(RIGHT(employee_name, 1));
```

Function names can vary between database systems.

---

# 128. Find Employees Sorted by Salary

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

# 129. Find Employees Sorted by Department and Salary

```sql
SELECT *
FROM employees
ORDER BY
    department_id,
    salary DESC;
```

---

# 130. Find Top Salary Per Department With Ties

Use:

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) AS x
WHERE rnk = 1;
```

`RANK()` returns all employees tied for first place.

`DENSE_RANK()` also returns all tied employees for rank 1.

---

# 131. When Should You Use ROW_NUMBER()?

Use `ROW_NUMBER()` when you want:

```text
Exactly one sequential number per row
```

Example:

```sql
SELECT
    employee_name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

---

# 132. When Should You Use RANK()?

Use `RANK()` when ties should receive the same rank and gaps should appear afterward.

Example:

```sql
SELECT
    employee_name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 133. When Should You Use DENSE_RANK()?

Use `DENSE_RANK()` when ties should receive the same rank but rank numbers should not have gaps.

Example:

```sql
SELECT
    employee_name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 134. Find Employees Whose Salary Is Not the Highest

```sql
SELECT *
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

---

# 135. Find Employees Whose Salary Is Not the Lowest

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT MIN(salary)
    FROM employees
);
```

---

# 136. Find the Difference Between Maximum and Minimum Salary

```sql
SELECT
    MAX(salary) - MIN(salary) AS salary_difference
FROM employees;
```

---

# 137. Find Total Salary Per Department

```sql
SELECT
    department_id,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department_id;
```

---

# 138. Find Employees in the Department With the Lowest Average Salary

```sql
WITH department_avg AS (
    SELECT
        department_id,
        AVG(salary) AS average_salary
    FROM employees
    GROUP BY department_id
),
ranked AS (
    SELECT
        department_id,
        average_salary,
        DENSE_RANK() OVER (
            ORDER BY average_salary
        ) AS rnk
    FROM department_avg
)
SELECT *
FROM ranked
WHERE rnk = 1;
```

---

# 139. Find Employees Hired Most Recently

```sql
SELECT *
FROM employees
ORDER BY hire_date DESC
LIMIT 5;
```

For SQL Server:

```sql
SELECT TOP 5 *
FROM employees
ORDER BY hire_date DESC;
```

---

# 140. Find Employees Hired Before a Given Date

```sql
SELECT *
FROM employees
WHERE hire_date < '2022-01-01';
```

---

# 141. Find Employees Hired Between Two Dates

```sql
SELECT *
FROM employees
WHERE hire_date >= '2021-01-01'
  AND hire_date < '2023-01-01';
```

Using a half-open range like:

```text
>= start
< end
```

is often safer when the column is a timestamp rather than a date.

---

# 142. Find Number of Employees in Each Department With More Than 2 Employees

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

This is one of the most basic and important `GROUP BY + HAVING` interview patterns.

---

# 143. Find Employees Who Have the Same Manager

```sql
SELECT
    manager_id,
    COUNT(*) AS employee_count
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id
HAVING COUNT(*) > 1;
```

This identifies managers with multiple direct reports.

---

# 144. Find Employees With the Same Manager as a Given Employee

Suppose we want employees having the same manager as Bob.

```sql
SELECT *
FROM employees
WHERE manager_id = (
    SELECT manager_id
    FROM employees
    WHERE employee_name = 'Bob'
);
```

To exclude Bob:

```sql
SELECT *
FROM employees
WHERE manager_id = (
    SELECT manager_id
    FROM employees
    WHERE employee_name = 'Bob'
)
AND employee_name <> 'Bob';
```

---

# 145. Find Employees Whose Salary Is Higher Than All Employees in Their Department Except Themselves

The simplest conceptual approach is to find the department maximum:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

This returns all employees tied for the maximum salary.

---

# 146. Find Employees Who Are in the Same Department as the Highest Paid Employee

```sql
SELECT *
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM employees
    WHERE salary = (
        SELECT MAX(salary)
        FROM employees
    )
);
```

If multiple highest-paid employees belong to different departments, this scalar-subquery approach may not be valid.

A safer set-based approach is:

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    WHERE salary = (
        SELECT MAX(salary)
        FROM employees
    )
);
```

---

# 147. Find Employees Who Are Not Managers

```sql
SELECT
    e.employee_id,
    e.employee_name
FROM employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM employees sub
    WHERE sub.manager_id = e.employee_id
);
```

---

# 148. Find Managers

```sql
SELECT DISTINCT
    m.employee_id,
    m.employee_name
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

# 149. Find Employee Count and Average Salary Per Department

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

---

# 150. Find Department-Wise Minimum and Maximum Salary

```sql
SELECT
    department_id,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department_id;
```

---

# 151. Find Salary Range Per Department

```sql
SELECT
    department_id,
    MAX(salary) - MIN(salary) AS salary_range
FROM employees
GROUP BY department_id;
```

---

# 152. Find Employees With Salary Equal to Department Maximum

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
JOIN (
    SELECT
        department_id,
        MAX(salary) AS max_salary
    FROM employees
    GROUP BY department_id
) d
    ON e.department_id = d.department_id
   AND e.salary = d.max_salary;
```

---

# 153. Find Employees With Salary Equal to Department Minimum

```sql
SELECT
    e.employee_id,
    e.employee_name,
    e.department_id,
    e.salary
FROM employees e
JOIN (
    SELECT
        department_id,
        MIN(salary) AS min_salary
    FROM employees
    GROUP BY department_id
) d
    ON e.department_id = d.department_id
   AND e.salary = d.min_salary;
```

---

# 154. Find Employees Whose Salary Is Greater Than Department Minimum

```sql
SELECT *
FROM employees e
WHERE e.salary > (
    SELECT MIN(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# 155. Find Employees Whose Salary Is Less Than Department Maximum

```sql
SELECT *
FROM employees e
WHERE e.salary < (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# 156. Important Pattern — WHERE vs HAVING

### WHERE

Filters rows **before grouping**.

```sql
SELECT
    department_id,
    COUNT(*)
FROM employees
WHERE salary > 60000
GROUP BY department_id;
```

Only employees earning above 60000 participate in grouping.

### HAVING

Filters groups **after grouping**.

```sql
SELECT
    department_id,
    COUNT(*)
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

---

# 157. Important Pattern — GROUP BY + HAVING

Remember:

```sql
SELECT
    department_id,
    AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```

Think:

```text
GROUP BY
→ Create groups

Aggregate
→ Calculate something for each group

HAVING
→ Filter those groups
```

---

# 158. Important Pattern — Top N Overall

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 5;
```

Think:

```text
ORDER BY DESC
→ Highest first

LIMIT
→ Take N rows
```

---

# 159. Important Pattern — Nth Highest Distinct Value

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = N;
```

Think:

```text
DENSE_RANK
→ Handles duplicate values correctly
```

---

# 160. Important Pattern — Highest Per Group

```sql
SELECT *
FROM (
    SELECT
        *,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 1;
```

Think:

```text
PARTITION BY
→ Separate each department

ORDER BY salary DESC
→ Highest salary first

DENSE_RANK = 1
→ Highest salary
```

---

# 161. Important Pattern — Above Group Average

```sql
SELECT *
FROM (
    SELECT
        *,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees
) x
WHERE salary > department_average;
```

Think:

```text
Window function
→ Calculate group average
without collapsing rows
```

---

# 162. Important Pattern — Find Duplicates

```sql
SELECT
    column_name,
    COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

This is one of the most reusable SQL interview patterns.

---

# 163. Important Pattern — Find Missing Matches

Using `LEFT JOIN`:

```sql
SELECT a.*
FROM table_a a
LEFT JOIN table_b b
    ON a.id = b.id
WHERE b.id IS NULL;
```

Think:

```text
LEFT JOIN
+
right-side IS NULL
=
unmatched rows
```

---

# 164. Important Pattern — Employee and Manager

```sql
SELECT
    e.employee_name,
    m.employee_name AS manager_name
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Think:

```text
Same table
+
different aliases
=
SELF JOIN
```

---

# 165. Important Pattern — Above Average

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

Think:

```text
Calculate average
        ↓
Compare each row
```

---

# 166. Important Pattern — Second Highest Salary

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

Think:

```text
Find highest
        ↓
Remove highest
        ↓
Find highest remaining
```

---

# 167. Important Pattern — Department-Wise Highest Salary

```sql
SELECT
    department_id,
    MAX(salary)
FROM employees
GROUP BY department_id;
```

If employee details are required:

```sql
SELECT *
FROM (
    SELECT
        *,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 1;
```

---

# 168. Important Pattern — Latest Row Per Group

```sql
SELECT *
FROM (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY hire_date DESC
        ) AS rn
    FROM employees
) x
WHERE rn = 1;
```

Think:

```text
PARTITION BY group
ORDER BY date DESC
ROW_NUMBER = 1
```

---

# 169. Important Pattern — Previous Row

```sql
LAG(column_name) OVER (
    PARTITION BY group_column
    ORDER BY order_column
)
```

Example:

```sql
SELECT
    employee_id,
    effective_date,
    salary,
    LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS previous_salary
FROM employee_salary_history;
```

---

# 170. Important Pattern — Next Row

```sql
LEAD(column_name) OVER (
    PARTITION BY group_column
    ORDER BY order_column
)
```

---

# 171. Important Pattern — Running Total

```sql
SUM(amount) OVER (
    ORDER BY order_date
)
```

Example:

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

# 172. Important Pattern — Conditional Aggregation

Suppose we want to count employees earning above 70000.

```sql
SELECT
    COUNT(
        CASE
            WHEN salary > 70000 THEN 1
        END
    ) AS high_salary_count
FROM employees;
```

Another common pattern:

```sql
SELECT
    SUM(
        CASE
            WHEN salary > 70000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count
FROM employees;
```

---

# 173. Department-Wise High Salary Employee Count

```sql
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary > 70000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees
GROUP BY department_id;
```

---

# 174. Department-Wise Salary Categories

```sql
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary >= 80000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count,
    SUM(
        CASE
            WHEN salary >= 60000
             AND salary < 80000 THEN 1
            ELSE 0
        END
    ) AS medium_salary_count,
    SUM(
        CASE
            WHEN salary < 60000 THEN 1
            ELSE 0
        END
    ) AS low_salary_count
FROM employees
GROUP BY department_id;
```

---

# 175. Find Departments Where Everyone Earns More Than 50000

One approach:

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING MIN(salary) > 50000;
```

### Logic

If the minimum salary is greater than 50000:

```text
Everyone in the department
→ earns more than 50000
```

---

# 176. Find Departments Where Someone Earns More Than 100000

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 100000;
```

---

# 177. Find Departments Where Everyone Has a Manager

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING COUNT(*) = COUNT(manager_id);
```

### Why?

```text
COUNT(*)
→ Counts every row

COUNT(manager_id)
→ Counts non-NULL manager IDs
```

If they are equal, every employee has a manager.

---

# 178. Find Departments With At Least One Employee Without a Manager

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING COUNT(*) > COUNT(manager_id);
```

---

# 179. Find Percentage of Employees Earning More Than 70000

A database-specific numeric cast may be needed to avoid integer division.

One common pattern:

```sql
SELECT
    100.0 * SUM(
        CASE
            WHEN salary > 70000 THEN 1
            ELSE 0
        END
    ) / COUNT(*) AS percentage_high_salary
FROM employees;
```

---

# 180. Find Department With Highest Percentage of High-Salary Employees

```sql
SELECT
    department_id,
    100.0 * SUM(
        CASE
            WHEN salary > 70000 THEN 1
            ELSE 0
        END
    ) / COUNT(*) AS high_salary_percentage
FROM employees
GROUP BY department_id
ORDER BY high_salary_percentage DESC
LIMIT 1;
```

---

# 181. Query Execution Order

A very important interview concept.

Although we write SQL like:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
```

the conceptual logical processing order is approximately:

```text
1. FROM
2. JOIN / ON
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. DISTINCT
8. ORDER BY
9. LIMIT / OFFSET
```

Exact internal execution is optimizer-dependent, but this logical order helps explain many SQL behaviors.

---

# 182. Why Can't We Normally Use an Aggregate in WHERE?

This is invalid in typical SQL:

```sql
SELECT department_id
FROM employees
WHERE COUNT(*) > 2
GROUP BY department_id;
```

Because:

```text
WHERE
→ filters rows before grouping
```

Use:

```sql
HAVING
```

instead:

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

---

# 183. Why Do We Use Subqueries?

A subquery allows one query to use the result of another query.

Example:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

Think:

```text
Inner query
→ produces value

Outer query
→ uses that value
```

---

# 184. What Is a Correlated Subquery?

A correlated subquery references a column from the outer query.

Example:

```sql
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

The inner query depends on the current row of the outer query.

---

# 185. What Is a CTE?

A CTE is a **Common Table Expression**.

Example:

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 70000
)
SELECT *
FROM high_salary;
```

CTEs can make complex queries easier to read and structure.

---

# 186. CTE vs Subquery

### Subquery

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

### CTE

```sql
WITH avg_salary AS (
    SELECT AVG(salary) AS avg_salary
    FROM employees
)
SELECT e.*
FROM employees e
CROSS JOIN avg_salary a
WHERE e.salary > a.avg_salary;
```

Both can solve the problem.

Use a CTE when it makes a complex query easier to understand or when a logical intermediate result is useful.

---

# 187. Common Interview Mistake — Second Highest Salary

A common incorrect query is:

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < MAX(salary);
```

This does not work because an aggregate function cannot be used that way in `WHERE`.

Correct approach:

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

---

# 188. Common Interview Mistake — NULL Comparison

Incorrect:

```sql
WHERE manager_id = NULL;
```

Correct:

```sql
WHERE manager_id IS NULL;
```

For non-NULL:

```sql
WHERE manager_id IS NOT NULL;
```

---

# 189. Common Interview Mistake — WHERE Instead of HAVING

Incorrect:

```sql
SELECT department_id
FROM employees
WHERE COUNT(*) > 2
GROUP BY department_id;
```

Correct:

```sql
SELECT department_id
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

---

# 190. Common Interview Mistake — LEFT JOIN Turning Into INNER JOIN

Suppose:

```sql
SELECT *
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.salary > 50000;
```

The `WHERE` condition removes rows where `e` is NULL, so the result may behave like an inner join for that condition.

If you want to preserve departments with no matching employee, move the condition into the join:

```sql
SELECT *
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
   AND e.salary > 50000;
```

This is an important interview concept.

---

# 191. Common Interview Mistake — COUNT(*) vs COUNT(column)

Suppose a department has no employees.

With:

```sql
COUNT(*)
```

after a `LEFT JOIN`, the department row itself can still be counted.

With:

```sql
COUNT(e.employee_id)
```

only matching employee rows are counted because NULL values are ignored.

Therefore:

```sql
COUNT(e.employee_id)
```

is usually the appropriate choice when counting matching employees after a `LEFT JOIN`.

---

# 192. Common Interview Mistake — DISTINCT Does Not Mean GROUP BY

Example:

```sql
SELECT DISTINCT department_id
FROM employees;
```

returns unique department IDs.

But:

```sql
SELECT department_id, COUNT(*)
FROM employees
GROUP BY department_id;
```

creates groups and calculates an aggregate for each group.

They solve different problems.

---

# 193. Common Interview Mistake — RANK vs DENSE_RANK

For:

```text
100
90
90
80
```

### RANK

```text
100 → 1
90  → 2
90  → 2
80  → 4
```

### DENSE_RANK

```text
100 → 1
90  → 2
90  → 2
80  → 3
```

For finding the Nth **distinct salary**, `DENSE_RANK()` is often the appropriate choice.

---

# 194. Common Interview Mistake — ROW_NUMBER for Ties

If you use:

```sql
ROW_NUMBER()
```

two employees with the same salary will receive different row numbers.

If the requirement is:

> Return everyone tied for the highest salary

use:

```sql
RANK()
```

or:

```sql
DENSE_RANK()
```

instead.

---

# 195. Interview Problem — Find Second Highest Salary

### Preferred Interview Answer

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### If They Ask About Duplicates

Explain:

> The `MAX()` subquery finds the highest salary, and the outer query excludes that value before finding the next maximum. This naturally handles duplicate highest salaries.

---

# 196. Interview Problem — Find Third Highest Salary

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 3;
```

---

# 197. Interview Problem — Find Highest Salary Per Department

```sql
SELECT
    department_id,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department_id;
```

If they ask for employee details:

```sql
SELECT *
FROM (
    SELECT
        *,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 1;
```

---

# 198. Interview Problem — Find Employees Earning More Than Their Manager

```sql
SELECT
    e.employee_name,
    e.salary,
    m.employee_name AS manager_name,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.salary > m.salary;
```

### Concept

```text
SELF JOIN
```

---

# 199. Interview Problem — Find Duplicate Records

```sql
SELECT
    employee_name,
    department_id,
    salary,
    COUNT(*) AS duplicate_count
FROM employees
GROUP BY
    employee_name,
    department_id,
    salary
HAVING COUNT(*) > 1;
```

### Concept

```text
GROUP BY
+
HAVING COUNT(*) > 1
```

---

# 200. Interview Problem — Top 3 Employees Per Department

```sql
SELECT
    employee_id,
    employee_name,
    department_id,
    salary
FROM (
    SELECT
        employee_id,
        employee_name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk <= 3;
```

---

# 201. Interview Problem — Employees Above Department Average

```sql
SELECT *
FROM (
    SELECT
        e.*,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees e
) x
WHERE salary > department_average;
```

---

# 202. Interview Problem — Department With No Employees

```sql
SELECT
    d.department_id,
    d.department_name
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

---

# 203. Interview Problem — Employees Without a Manager

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

# 204. Interview Problem — Employee and Manager Names

```sql
SELECT
    e.employee_name AS employee,
    m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

# 205. Interview Problem — Highest Salary in Company

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

To return the employee:

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

# 206. Interview Problem — Average Salary

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

---

# 207. Interview Problem — Total Employees Per Department

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

---

# 208. Interview Problem — Departments With More Than 5 Employees

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

# 209. Interview Problem — Employees Above Company Average

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 210. Interview Problem — Employees in the Highest-Paid Department

One possible approach:

```sql
WITH department_salary AS (
    SELECT
        department_id,
        SUM(salary) AS total_salary
    FROM employees
    GROUP BY department_id
),
ranked AS (
    SELECT
        department_id,
        total_salary,
        DENSE_RANK() OVER (
            ORDER BY total_salary DESC
        ) AS rnk
    FROM department_salary
)
SELECT *
FROM ranked
WHERE rnk = 1;
```

---

# 211. Interview Problem — Find Latest Employee Per Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY hire_date DESC
        ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

---

# 212. Interview Problem — Find Employees Who Share a Salary

```sql
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) > 1
);
```

---

# 213. Interview Problem — Find Unique Salaries

```sql
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) = 1
);
```

---

# 214. Interview Problem — Find Employees Hired Before 2020

```sql
SELECT *
FROM employees
WHERE hire_date < '2020-01-01';
```

---

# 215. Interview Problem — Find Employees Hired in 2023

A portable range-based approach is:

```sql
SELECT *
FROM employees
WHERE hire_date >= '2023-01-01'
  AND hire_date < '2024-01-01';
```

---

# 216. Interview Problem — Find Department Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

---

# 217. Interview Problem — Find Department With Highest Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
ORDER BY average_salary DESC
LIMIT 1;
```

For SQL Server:

```sql
SELECT TOP 1
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
ORDER BY average_salary DESC;
```

---

# 218. Interview Problem — Find Employee Count Per Department Including Empty Departments

```sql
SELECT
    d.department_id,
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY
    d.department_id,
    d.department_name;
```

---

# 219. Interview Problem — Find Managers With More Than 3 Employees

```sql
SELECT
    manager_id,
    COUNT(*) AS employee_count
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id
HAVING COUNT(*) > 3;
```

---

# 220. Interview Problem — Find Employees Earning More Than Their Department Average

### Correlated Subquery

```sql
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

### Window Function

```sql
SELECT *
FROM (
    SELECT
        e.*,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees e
) x
WHERE salary > department_average;
```

---

# 221. Interview Problem — Running Total

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

---

# 222. Interview Problem — Previous Value

```sql
SELECT
    employee_id,
    effective_date,
    salary,
    LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS previous_salary
FROM employee_salary_history;
```

---

# 223. Interview Problem — Next Value

```sql
SELECT
    employee_id,
    effective_date,
    salary,
    LEAD(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS next_salary
FROM employee_salary_history;
```

---

# 224. Interview Problem — Salary Rank

```sql
SELECT
    employee_name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 225. Interview Problem — Department Salary Rank

```sql
SELECT
    employee_name,
    department_id,
    salary,
    DENSE_RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS department_salary_rank
FROM employees;
```

---

# 226. Interview Problem — Top 2 Salaries Per Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk <= 2;
```

---

# 227. Interview Problem — Find Employees Whose Salary Is the Second Highest in Their Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk = 2;
```

---

# 228. Interview Problem — Find Departments Where Average Salary Is Greater Than 60000

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 60000;
```

---

# 229. Interview Problem — Find Employees From Departments With Average Salary Greater Than 60000

```sql
SELECT *
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM employees
    GROUP BY department_id
    HAVING AVG(salary) > 60000
);
```

---

# 230. Interview Problem — Find Employees Whose Salary Is Between Company Average and Maximum

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
AND salary < (
    SELECT MAX(salary)
    FROM employees
);
```

---

# 231. Interview Problem — Find Maximum Salary Difference Between Two Employees

```sql
SELECT
    MAX(salary) - MIN(salary) AS maximum_salary_difference
FROM employees;
```

---

# 232. Interview Problem — Find Department Salary Difference

```sql
SELECT
    department_id,
    MAX(salary) - MIN(salary) AS salary_difference
FROM employees
GROUP BY department_id;
```

---

# 233. Interview Problem — Find Employees Whose Salary Is a Duplicate

```sql
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) > 1
);
```

---

# 234. Interview Problem — Find Employees Whose Salary Is Unique

```sql
SELECT *
FROM employees
WHERE salary IN (
    SELECT salary
    FROM employees
    GROUP BY salary
    HAVING COUNT(*) = 1
);
```

---

# 235. Interview Problem — Find the Most Common Department

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
ORDER BY employee_count DESC
LIMIT 1;
```

---

# 236. Interview Problem — Find the Least Common Department

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
ORDER BY employee_count ASC
LIMIT 1;
```

---

# 237. Interview Problem — Find Departments With Average Salary Equal to Maximum Salary of Another Department

This type of problem is more advanced and can be solved using CTEs/subqueries.

Example:

```sql
WITH department_stats AS (
    SELECT
        department_id,
        AVG(salary) AS average_salary,
        MAX(salary) AS maximum_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM department_stats;
```

The exact comparison depends on the business requirement.

The important interview skill is knowing how to build the intermediate aggregate result first.

---

# 238. How to Approach Any SQL Query Interview Problem

Do not immediately start writing SQL.

Use this process:

```text
1. Identify the table(s)
        ↓
2. Identify required columns
        ↓
3. Identify row filtering
        ↓
4. Identify whether JOIN is required
        ↓
5. Identify whether aggregation is required
        ↓
6. Identify GROUP BY columns
        ↓
7. Identify HAVING conditions
        ↓
8. Identify ranking/window requirements
        ↓
9. Identify sorting
        ↓
10. Check duplicates and NULL values
        ↓
11. Write query
        ↓
12. Test with sample data
```

---

# 239. How to Recognize the SQL Concept From the Question

| Question wording | Likely concept |
|---|---|
| Highest salary | `MAX()` |
| Lowest salary | `MIN()` |
| Average salary | `AVG()` |
| Total salary | `SUM()` |
| Number of employees | `COUNT()` |
| Unique values | `DISTINCT` |
| Each department | `GROUP BY` |
| Departments having more than... | `HAVING` |
| Employee + department | `JOIN` |
| Employee + manager | `SELF JOIN` |
| Second highest | Subquery / `DENSE_RANK()` |
| Nth highest | `DENSE_RANK()` |
| Top N per department | `PARTITION BY` + ranking |
| Above department average | Correlated subquery / window function |
| Previous record | `LAG()` |
| Next record | `LEAD()` |
| Running total | `SUM() OVER()` |
| Duplicate records | `GROUP BY` + `HAVING` |
| Missing records | `LEFT JOIN` + `IS NULL` / `NOT EXISTS` |
| Categorize data | `CASE` |
| Compare with another row | Self join / window function |

---

# 240. The 20 Most Important Query Problems to Master

If interview preparation time is limited, prioritize these:

## 1. Second Highest Salary

```sql
SELECT MAX(salary)
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

## 2. Nth Highest Salary

```sql
SELECT salary
FROM (
    SELECT
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 3;
```

## 3. Highest Salary Per Department

```sql
SELECT
    department_id,
    MAX(salary)
FROM employees
GROUP BY department_id;
```

## 4. Highest Paid Employee Per Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk = 1;
```

## 5. Top 3 Employees Per Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rnk
    FROM employees e
) x
WHERE rnk <= 3;
```

## 6. Employees Above Company Average

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

## 7. Employees Above Department Average

```sql
SELECT *
FROM (
    SELECT
        e.*,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees e
) x
WHERE salary > department_average;
```

## 8. Duplicate Salaries

```sql
SELECT
    salary,
    COUNT(*)
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;
```

## 9. Employee and Manager

```sql
SELECT
    e.employee_name,
    m.employee_name AS manager_name
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

## 10. Employees Earning More Than Manager

```sql
SELECT
    e.employee_name,
    e.salary,
    m.employee_name AS manager_name,
    m.salary AS manager_salary
FROM employees e
JOIN employees m
    ON e.manager_id = m.employee_id
WHERE e.salary > m.salary;
```

## 11. Departments With More Than N Employees

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 2;
```

## 12. Departments With No Employees

```sql
SELECT
    d.department_id,
    d.department_name
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

## 13. Employee Count Per Department

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

## 14. Department Average Salary

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department_id;
```

## 15. Latest Employee Per Department

```sql
SELECT *
FROM (
    SELECT
        e.*,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY hire_date DESC
        ) AS rn
    FROM employees e
) x
WHERE rn = 1;
```

## 16. Running Total

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
    ) AS running_total
FROM orders;
```

## 17. Previous Row

```sql
SELECT
    employee_id,
    effective_date,
    salary,
    LAG(salary) OVER (
        PARTITION BY employee_id
        ORDER BY effective_date
    ) AS previous_salary
FROM employee_salary_history;
```

## 18. Employees Without Manager

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

## 19. Duplicate Records

```sql
SELECT
    employee_name,
    department_id,
    salary,
    COUNT(*)
FROM employees
GROUP BY
    employee_name,
    department_id,
    salary
HAVING COUNT(*) > 1;
```

## 20. Conditional Aggregation

```sql
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary > 70000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count
FROM employees
GROUP BY department_id;
```

---

# 241. Final SQL Query Interview Checklist

Before an interview, make sure you can write these without looking at the answer:

```text
□ SELECT with WHERE
□ DISTINCT
□ LIKE
□ BETWEEN
□ IN
□ COUNT
□ SUM
□ AVG
□ MIN
□ MAX
□ GROUP BY
□ HAVING
□ INNER JOIN
□ LEFT JOIN
□ SELF JOIN
□ Second highest salary
□ Nth highest salary
□ Highest salary per department
□ Top N per department
□ Duplicate records
□ Employees above average
□ Employees above department average
□ Employee-manager query
□ Employees earning more than manager
□ Departments with no employees
□ Employees without manager
□ CASE
□ COALESCE
□ Subquery
□ Correlated subquery
□ CTE
□ ROW_NUMBER
□ RANK
□ DENSE_RANK
□ LAG
□ LEAD
□ Running total
□ Conditional aggregation
□ UNION
□ UNION ALL
□ EXISTS
□ NOT EXISTS
□ NULL handling
```

---

# 242. Final Interview Strategy

For SQL interviews, don't try to memorize 200 completely different queries.

Most interview problems are combinations of a smaller number of patterns.

Master these patterns:

```text
Pattern 1
WHERE
→ Filter rows

Pattern 2
GROUP BY + aggregate
→ Calculate per-group values

Pattern 3
GROUP BY + HAVING
→ Filter groups

Pattern 4
JOIN
→ Combine tables

Pattern 5
SELF JOIN
→ Compare rows within the same table

Pattern 6
Subquery
→ Compare against another query result

Pattern 7
Correlated subquery
→ Compare each row with its group/related rows

Pattern 8
DENSE_RANK()
→ Nth highest / top N with ties

Pattern 9
ROW_NUMBER()
→ Exactly one row per group

Pattern 10
LAG()
→ Previous row

Pattern 11
LEAD()
→ Next row

Pattern 12
SUM() OVER()
→ Running total

Pattern 13
LEFT JOIN + IS NULL
→ Find missing matches

Pattern 14
GROUP BY + HAVING COUNT(*) > 1
→ Find duplicates

Pattern 15
CASE
→ Conditional logic

Pattern 16
COALESCE
→ Handle NULL values
```

If you understand these patterns deeply, you can solve a large number of SQL interview coding questions instead of memorizing every query individually.