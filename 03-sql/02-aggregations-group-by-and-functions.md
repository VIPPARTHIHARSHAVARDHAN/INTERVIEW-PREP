# SQL Aggregations, GROUP BY and Functions

## 1. What Are Aggregate Functions?

Aggregate functions perform a calculation on **multiple rows** and return a single result for each group.

The most important aggregate functions are:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

Example table:

| id | name | department | salary |
|---:|---|---|---:|
| 1 | Rahul | IT | 60000 |
| 2 | Priya | HR | 50000 |
| 3 | Arjun | IT | 70000 |
| 4 | Sneha | Sales | 45000 |
| 5 | Kiran | IT | 80000 |

---

# 2. COUNT()

`COUNT()` is used to count rows or non-NULL values.

## COUNT(*)

Counts all rows.

```sql
SELECT COUNT(*) AS employee_count
FROM employees;
```

Output:

```text
employee_count
--------------
5
```

`COUNT(*)` counts rows regardless of whether individual columns contain NULL values.

---

# 3. COUNT(column)

`COUNT(column)` counts only the **non-NULL values** in that column.

Suppose:

| id | name | phone |
|---:|---|---|
| 1 | Rahul | 9876543210 |
| 2 | Priya | NULL |
| 3 | Arjun | 9123456789 |

Query:

```sql
SELECT COUNT(phone) AS phone_count
FROM employees;
```

Output:

```text
phone_count
-----------
2
```

Because Priya's phone is NULL.

---

# 4. COUNT(*) vs COUNT(column)

This is a very common interview question.

| `COUNT(*)` | `COUNT(column)` |
|---|---|
| Counts rows | Counts non-NULL values |
| NULL values in columns do not affect it | NULL values in that column are ignored |
| Useful for counting records | Useful for counting available values |

### Interview Answer

> `COUNT(*)` counts rows in the result, whereas `COUNT(column)` counts only the non-NULL values in that column.

---

# 5. SUM()

`SUM()` calculates the total of numeric values.

Example:

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

For:

```text
60000
50000
70000
45000
80000
```

the result is:

```text
305000
```

---

# 6. AVG()

`AVG()` calculates the average of numeric values.

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

Conceptually:

```text
Total salary
----------------
Number of values
```

### Important NULL Behavior

`AVG()` ignores NULL values.

For example:

```text
60000
50000
NULL
80000
```

the average is calculated using:

```text
60000 + 50000 + 80000
---------------------
         3
```

not 4.

---

# 7. MIN()

`MIN()` returns the smallest value.

```sql
SELECT MIN(salary) AS minimum_salary
FROM employees;
```

Output:

```text
45000
```

---

# 8. MAX()

`MAX()` returns the largest value.

```sql
SELECT MAX(salary) AS maximum_salary
FROM employees;
```

Output:

```text
80000
```

---

# 9. Using Multiple Aggregate Functions

You can use multiple aggregate functions in one query.

```sql
SELECT
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

This is useful for generating summary reports.

---

# 10. What is GROUP BY?

`GROUP BY` groups rows that have the same value in one or more columns.

It is commonly used with aggregate functions.

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Result:

| department | employee_count |
|---|---:|
| HR | 1 |
| IT | 3 |
| Sales | 1 |

Instead of calculating one count for the entire table, SQL calculates a count for each department.

---

# 11. GROUP BY with SUM()

Find total salary for each department:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

Example result:

| department | total_salary |
|---|---:|
| HR | 50000 |
| IT | 210000 |
| Sales | 45000 |

---

# 12. GROUP BY with AVG()

Find the average salary of each department:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 13. GROUP BY with MIN() and MAX()

Find minimum and maximum salary in each department:

```sql
SELECT
    department,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```

---

# 14. GROUP BY Multiple Columns

You can group by more than one column.

Suppose we have:

| department | job_role | salary |
|---|---|---:|
| IT | Developer | 60000 |
| IT | Developer | 70000 |
| IT | Tester | 50000 |
| HR | Recruiter | 45000 |

Query:

```sql
SELECT
    department,
    job_role,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department, job_role;
```

SQL creates groups based on the **combination** of department and job role.

---

# 15. Important GROUP BY Rule

If you select a column that is not inside an aggregate function, it generally needs to be included in the `GROUP BY` clause.

Correct:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Here:

```text
department → grouped column
AVG(salary) → aggregate
```

A query such as:

```sql
SELECT
    department,
    name,
    AVG(salary)
FROM employees
GROUP BY department;
```

is not valid in standard SQL because `name` is neither grouped nor aggregated.

### Interview Answer

> When using GROUP BY, every selected expression generally must either be part of the grouping or be aggregated, unless the database has additional rules that allow it.

---

# 16. HAVING

`HAVING` filters groups after aggregation.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

This returns only departments whose average salary is greater than 60,000.

---

# 17. WHERE vs HAVING

This is one of the most frequently asked SQL interview questions.

## WHERE

Filters individual rows **before grouping**.

```sql
SELECT
    department,
    AVG(salary)
FROM employees
WHERE status = 'Active'
GROUP BY department;
```

Only active employees participate in the grouping.

---

## HAVING

Filters groups **after grouping and aggregation**.

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### Easy Way to Remember

```text
WHERE
↓
Filter rows

GROUP BY
↓
Create groups

HAVING
↓
Filter groups
```

### Interview Answer

> WHERE filters individual rows before grouping, while HAVING filters the groups produced by GROUP BY, usually using aggregate conditions.

---

# 18. WHERE and HAVING Together

You can use both.

Example:

> Find departments whose active employees have an average salary greater than 60,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 60000;
```

The logic is:

```text
1. Keep only active employees
2. Group them by department
3. Calculate average salary
4. Keep departments with average > 60000
```

---

# 19. Can WHERE Use Aggregate Functions?

Normally, no.

Incorrect:

```sql
SELECT department, AVG(salary)
FROM employees
WHERE AVG(salary) > 60000
GROUP BY department;
```

Use `HAVING`:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### Why?

Because `WHERE` operates before the grouping/aggregation step, while `HAVING` is designed to filter grouped results.

---

# 20. GROUP BY Without Aggregate Functions

`GROUP BY` can technically be used without an aggregate function, although `DISTINCT` is often clearer when the goal is simply to remove duplicates.

Example:

```sql
SELECT department
FROM employees
GROUP BY department;
```

This returns one row per department.

Usually, if the intention is simply to get unique departments, prefer:

```sql
SELECT DISTINCT department
FROM employees;
```

### Interview Point

> GROUP BY is primarily used to create groups for aggregation, while DISTINCT is generally used when we only need unique result values.

---

# 21. Aggregate Functions and NULL

Most aggregate functions ignore NULL values.

For example:

```text
salary
------
60000
50000
NULL
80000
```

Then:

```sql
SELECT AVG(salary)
FROM employees;
```

calculates the average using:

```text
60000
50000
80000
```

The NULL value is not treated as zero.

### Important

Do not assume that NULL is automatically converted to `0`.

If you explicitly want to replace NULL with another value, functions such as `COALESCE()` can be used.

---

# 22. COALESCE()

`COALESCE()` returns the first non-NULL expression.

Example:

```sql
SELECT
    name,
    COALESCE(phone, 'Not Provided') AS phone
FROM employees;
```

If `phone` is NULL, the result becomes:

```text
Not Provided
```

### Real-World Use

This is useful when displaying incomplete customer information in reports.

---

# 23. COALESCE() with Calculations

Suppose some employees have a NULL bonus.

```sql
SELECT
    name,
    salary,
    COALESCE(bonus, 0) AS bonus
FROM employees;
```

You can then calculate total compensation:

```sql
SELECT
    name,
    salary + COALESCE(bonus, 0) AS total_compensation
FROM employees;
```

Without handling NULL, arithmetic involving NULL can produce NULL.

---

# 24. NULLIF()

`NULLIF()` returns NULL when two expressions are equal; otherwise, it returns the first expression.

Example:

```sql
SELECT NULLIF(10, 10);
```

Result:

```text
NULL
```

Example:

```sql
SELECT NULLIF(10, 5);
```

Result:

```text
10
```

### Common Use

It can help prevent division-by-zero problems.

```sql
SELECT
    revenue / NULLIF(quantity, 0) AS revenue_per_unit
FROM sales;
```

If `quantity` is zero, `NULLIF(quantity, 0)` returns NULL instead of zero.

---

# 25. CASE WHEN

`CASE` provides conditional logic inside a SQL query.

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

Example result:

| name | salary | salary_category |
|---|---:|---|
| Rahul | 60000 | Medium |
| Priya | 50000 | Low |
| Arjun | 70000 | Medium |
| Sneha | 45000 | Low |
| Kiran | 80000 | High |

---

# 26. CASE with Aggregation

`CASE` can be combined with aggregate functions for conditional aggregation.

Example:

> Count IT employees.

```sql
SELECT
    SUM(
        CASE
            WHEN department = 'IT' THEN 1
            ELSE 0
        END
    ) AS it_employee_count
FROM employees;
```

Another common approach:

```sql
SELECT
    COUNT(CASE WHEN department = 'IT' THEN 1 END) AS it_employee_count
FROM employees;
```

### Interview Tip

Conditional aggregation is a useful technique for solving reporting problems without writing separate queries.

---

# 27. Multiple Conditional Counts

Example:

```sql
SELECT
    SUM(CASE WHEN department = 'IT' THEN 1 ELSE 0 END) AS it_count,
    SUM(CASE WHEN department = 'HR' THEN 1 ELSE 0 END) AS hr_count,
    SUM(CASE WHEN department = 'Sales' THEN 1 ELSE 0 END) AS sales_count
FROM employees;
```

This can produce:

| it_count | hr_count | sales_count |
|---:|---:|---:|
| 3 | 1 | 1 |

---

# 28. String Functions

SQL provides functions for working with text.

Common functions include:

```text
UPPER()
LOWER()
LENGTH()
TRIM()
SUBSTRING()
CONCAT()
```

Exact function names and syntax can vary between database systems.

---

# 29. UPPER()

Converts text to uppercase.

```sql
SELECT UPPER(name) AS name_upper
FROM employees;
```

Example:

```text
rahul
```

becomes:

```text
RAHUL
```

---

# 30. LOWER()

Converts text to lowercase.

```sql
SELECT LOWER(name) AS name_lower
FROM employees;
```

---

# 31. LENGTH()

Returns the length of a string in databases that support this syntax.

```sql
SELECT
    name,
    LENGTH(name) AS name_length
FROM employees;
```

### Important

String-length functions can differ between SQL databases. For example, SQL Server commonly uses `LEN()`.

---

# 32. TRIM()

Removes leading and trailing spaces.

```sql
SELECT TRIM(name)
FROM employees;
```

This is especially useful when cleaning imported data.

---

# 33. CONCAT()

Combines strings.

```sql
SELECT
    CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```

Example:

```text
first_name = Rahul
last_name  = Kumar
```

Result:

```text
Rahul Kumar
```

### Important

Concatenation syntax differs between database systems, so check the SQL dialect being used.

---

# 34. SUBSTRING()

Extracts part of a string.

Syntax varies by database, but a common form is:

```sql
SELECT SUBSTRING(name, 1, 3)
FROM employees;
```

For:

```text
Rahul
```

the result can be:

```text
Rah
```

---

# 35. Date Functions

SQL databases provide functions for working with dates and timestamps.

Common requirements include:

- Current date
- Current timestamp
- Extract year
- Extract month
- Extract day
- Date difference
- Adding/subtracting dates

Syntax differs significantly between MySQL, PostgreSQL, SQL Server, Oracle, and other systems.

### Interview Tip

Know the **concept** first and then learn the syntax for the database mentioned in the job description.

---

# 36. Extracting Year

A common SQL approach is:

```sql
SELECT
    EXTRACT(YEAR FROM joining_date) AS joining_year
FROM employees;
```

Some database systems use different syntax, for example:

```sql
SELECT YEAR(joining_date)
FROM employees;
```

The exact syntax depends on the SQL dialect.

---

# 37. Date Filtering

Suppose:

```text
joining_date
------------
2026-01-10
2026-02-15
2026-03-20
```

To find employees who joined during January 2026:

```sql
SELECT *
FROM employees
WHERE joining_date >= '2026-01-01'
  AND joining_date < '2026-02-01';
```

This approach is particularly useful when the column contains timestamps.

---

# 38. Aggregate Functions with WHERE

You can filter rows before calculating an aggregate.

Example:

> Find the average salary of IT employees.

```sql
SELECT AVG(salary) AS average_salary
FROM employees
WHERE department = 'IT';
```

The sequence is conceptually:

```text
All employees
      ↓
Filter IT employees
      ↓
Calculate AVG
```

---

# 39. Aggregate Functions with GROUP BY and WHERE

Example:

> Find the average salary of active employees in each department.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE status = 'Active'
GROUP BY department;
```

---

# 40. GROUP BY and HAVING Example

Question:

> Find departments having more than 5 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

### Interview Explanation

> I group the employees by department, count the employees in each department, and then use HAVING because I need to filter the aggregated groups.

---

# 41. Real-World Example — Sales Report

Suppose an e-commerce company has:

```text
sales
------------------------------------------------
order_id | product | category | amount
------------------------------------------------
1        | Phone   | Electronics | 30000
2        | Laptop  | Electronics | 60000
3        | Chair   | Furniture   | 8000
4        | Mouse   | Electronics | 1000
5        | Desk    | Furniture   | 12000
```

Question:

> Find total sales for each category.

```sql
SELECT
    category,
    SUM(amount) AS total_sales
FROM sales
GROUP BY category;
```

Result:

| category | total_sales |
|---|---:|
| Electronics | 91000 |
| Furniture | 20000 |

---

# 42. Real-World Example — Department Report

Question:

> Find departments with an average salary greater than ₹60,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

### Interview Explanation

> Since I need the average salary for each department, I first group employees by department. Then I use HAVING to filter departments based on the calculated average.

---

# 43. Real-World Example — Customer Orders

Suppose:

```text
orders
--------------------------------
order_id | customer_id | amount
--------------------------------
1        | 101         | 500
2        | 101         | 700
3        | 102         | 300
4        | 101         | 200
5        | 103         | 1000
```

Question:

> Find customers who have spent more than 1,000.

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 1000;
```

Customer 101 spent:

```text
500 + 700 + 200 = 1400
```

so customer 101 qualifies.

---

# 44. Real-World Example — Conditional Reporting

Question:

> Count active and inactive employees in one query.

```sql
SELECT
    SUM(CASE WHEN status = 'Active' THEN 1 ELSE 0 END) AS active_count,
    SUM(CASE WHEN status = 'Inactive' THEN 1 ELSE 0 END) AS inactive_count
FROM employees;
```

This is a practical example of **conditional aggregation**.

---

# 45. Important Interview Question — What is GROUP BY?

### Answer

> GROUP BY groups rows having the same values in specified columns, usually so that aggregate functions such as COUNT, SUM, or AVG can be calculated for each group.

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

---

# 46. Important Interview Question — What is HAVING?

### Answer

> HAVING filters groups after GROUP BY and is commonly used with aggregate functions.

Example:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

---

# 47. Important Interview Question — WHERE vs HAVING?

### Answer

> WHERE filters rows before grouping, whereas HAVING filters groups after grouping.

Example:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 60000;
```

Here:

```text
WHERE  → removes inactive employees
GROUP BY → creates department groups
HAVING → removes departments whose average is <= 60000
```

---

# 48. Important Interview Question — What are Aggregate Functions?

### Answer

> Aggregate functions perform calculations over multiple rows and return a summary value. Common aggregate functions are COUNT, SUM, AVG, MIN, and MAX.

Example:

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

---

# 49. Important Interview Question — Does AVG() Include NULL?

### Answer

> Generally, AVG ignores NULL values. It calculates the average using the non-NULL values.

Example:

```text
60000
50000
NULL
80000
```

The average is based on:

```text
60000, 50000, 80000
```

not four values.

---

# 50. Important Interview Question — Does COUNT(*) Count NULL Rows?

### Answer

> Yes. COUNT(*) counts rows, so NULL values in individual columns do not prevent a row from being counted.

However:

```sql
COUNT(phone)
```

counts only rows where `phone` is non-NULL.

---

# 51. Important Interview Question — Can We Use Multiple Aggregate Functions Together?

### Answer

Yes.

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

---

# 52. Important Interview Question — Can GROUP BY Use Multiple Columns?

### Answer

Yes.

```sql
SELECT
    department,
    job_role,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department, job_role;
```

The grouping is based on the combination of both columns.

---

# 53. Important Interview Question — GROUP BY vs DISTINCT?

### Answer

> DISTINCT is mainly used to remove duplicate result rows, while GROUP BY is primarily used to create groups, especially for aggregation.

Example:

```sql
SELECT DISTINCT department
FROM employees;
```

For aggregation:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

---

# 54. Important Interview Question — What is COALESCE()?

### Answer

> COALESCE returns the first non-NULL expression from the values provided.

Example:

```sql
SELECT
    name,
    COALESCE(phone, 'Not Provided') AS phone
FROM employees;
```

If phone is NULL, it returns `Not Provided`.

---

# 55. Important Interview Question — What is CASE WHEN?

### Answer

> CASE WHEN provides conditional logic inside a SQL expression and allows us to return different values based on conditions.

Example:

```sql
SELECT
    name,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 56. Important Interview Question — What is Conditional Aggregation?

### Answer

> Conditional aggregation combines aggregate functions with conditional expressions such as CASE to calculate different summaries based on conditions.

Example:

```sql
SELECT
    SUM(CASE WHEN department = 'IT' THEN 1 ELSE 0 END) AS it_count,
    SUM(CASE WHEN department = 'HR' THEN 1 ELSE 0 END) AS hr_count
FROM employees;
```

---

# 57. Common Coding Questions

## Question 1

Find the total number of employees.

```sql
SELECT COUNT(*) AS employee_count
FROM employees;
```

---

## Question 2

Find the total salary paid by the company.

```sql
SELECT SUM(salary) AS total_salary
FROM employees;
```

---

## Question 3

Find the average salary.

```sql
SELECT AVG(salary) AS average_salary
FROM employees;
```

---

## Question 4

Find the highest salary.

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

---

## Question 5

Find the lowest salary.

```sql
SELECT MIN(salary) AS lowest_salary
FROM employees;
```

---

## Question 6

Find the number of employees in each department.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

---

## Question 7

Find the average salary in each department.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

## Question 8

Find the highest salary in each department.

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

## Question 9

Find departments with more than 5 employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

---

## Question 10

Find departments whose average salary is greater than 60,000.

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

## Question 11

Find the total salary for employees in each department, considering only active employees.

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
WHERE status = 'Active'
GROUP BY department;
```

---

## Question 12

Find departments with more than 5 active employees.

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING COUNT(*) > 5;
```

---

## Question 13

Count employees in IT, HR, and Sales using one query.

```sql
SELECT
    SUM(CASE WHEN department = 'IT' THEN 1 ELSE 0 END) AS it_count,
    SUM(CASE WHEN department = 'HR' THEN 1 ELSE 0 END) AS hr_count,
    SUM(CASE WHEN department = 'Sales' THEN 1 ELSE 0 END) AS sales_count
FROM employees;
```

---

## Question 14

Display each employee's salary category.

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

## Question 15

Calculate total compensation where NULL bonuses should be treated as zero.

```sql
SELECT
    name,
    salary + COALESCE(bonus, 0) AS total_compensation
FROM employees;
```

---

# 58. Interview Problem — Think Before Writing

### Question

> Find departments where the total salary is greater than ₹2,00,000, but consider only employees earning more than ₹50,000.

### Step 1 — Identify the filter

Only employees with salary greater than 50,000:

```sql
WHERE salary > 50000
```

### Step 2 — Identify the grouping

We need the total salary **department-wise**:

```sql
GROUP BY department
```

### Step 3 — Identify the aggregate condition

We need total salary greater than 2,00,000:

```sql
HAVING SUM(salary) > 200000
```

### Final Query

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
WHERE salary > 50000
GROUP BY department
HAVING SUM(salary) > 200000;
```

### Strong Interview Explanation

> First, I filter out employees whose salary is 50,000 or less because that condition applies to individual rows. Then I group the remaining employees by department and calculate the total salary for each department. Finally, I use HAVING because the condition is based on the aggregated salary of each department.

---

# 59. Interview Problem — Employee Count and Average Salary

### Question

> Find departments that have at least 3 employees and an average salary above ₹60,000.

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING COUNT(*) >= 3
   AND AVG(salary) > 60000;
```

### What This Tests

This single query tests:

```text
GROUP BY
COUNT()
AVG()
HAVING
Multiple aggregate conditions
```

---

# 60. Interview Problem — Conditional Aggregation

### Question

> Find the number of high-salary and low-salary employees.

Assume high salary means at least 60,000.

```sql
SELECT
    SUM(CASE WHEN salary >= 60000 THEN 1 ELSE 0 END) AS high_salary_count,
    SUM(CASE WHEN salary < 60000 THEN 1 ELSE 0 END) AS low_salary_count
FROM employees;
```

### Interview Explanation

> I use CASE to classify each row and then SUM the resulting 1s and 0s to count each category in a single query.

---

# 61. Logical Query Processing

For interview discussions, remember this simplified logical order:

```text
FROM
↓
WHERE
↓
GROUP BY
↓
HAVING
↓
SELECT
↓
DISTINCT
↓
ORDER BY
↓
LIMIT / OFFSET
```

### Example

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
WHERE status = 'Active'
GROUP BY department
HAVING AVG(salary) > 60000
ORDER BY average_salary DESC;
```

Conceptually:

```text
FROM
↓
Get employees

WHERE
↓
Keep active employees

GROUP BY
↓
Create department groups

HAVING
↓
Keep departments with average salary > 60000

SELECT
↓
Return department and average salary

ORDER BY
↓
Sort by average salary
```

The database optimizer may physically execute operations differently, but this logical order is useful for understanding SQL semantics and interview questions.

---

# 62. Most Important Concepts to Remember

```text
COUNT()
↓
Count rows / non-NULL values

SUM()
↓
Total

AVG()
↓
Average

MIN()
↓
Smallest value

MAX()
↓
Largest value

GROUP BY
↓
Create groups

HAVING
↓
Filter groups

WHERE
↓
Filter rows

COALESCE()
↓
Replace NULL with the first available non-NULL value

NULLIF()
↓
Return NULL when two expressions are equal

CASE
↓
Conditional logic

Conditional Aggregation
↓
Aggregate values based on conditions
```

---

# 63. Interview Priority

## 🔴 Must Know Very Well

```text
COUNT()
SUM()
AVG()
MIN()
MAX()

GROUP BY

HAVING

WHERE vs HAVING

COUNT(*) vs COUNT(column)

NULL with aggregate functions

GROUP BY with multiple columns

CASE WHEN

COALESCE()

Conditional aggregation
```

## 🟡 Know Clearly

```text
String functions

Date functions

NULLIF()

GROUP BY vs DISTINCT

Date filtering

Multiple aggregate functions
```

## 🟢 Basic Understanding Is Enough

```text
Database-specific date syntax

Database-specific string functions

Advanced function-specific behavior
```

---

# 64. Final Interview Checklist

Before moving to the next SQL topic, make sure you can answer these without looking at notes:

- What is an aggregate function?
- What are the five common aggregate functions?
- What is COUNT(*)?
- What is COUNT(column)?
- How does NULL affect COUNT?
- How does NULL affect AVG?
- What is GROUP BY?
- Why do we use GROUP BY?
- Can we group by multiple columns?
- What is HAVING?
- WHERE vs HAVING?
- Why can't aggregate conditions normally be placed in WHERE?
- Can WHERE and HAVING be used together?
- GROUP BY vs DISTINCT?
- What is COALESCE?
- What is NULLIF?
- What is CASE WHEN?
- What is conditional aggregation?
- How do you find department-wise employee counts?
- How do you find department-wise average salary?
- How do you find departments with more than N employees?
- How do you find departments whose average salary is greater than a given amount?
- How do you count multiple categories in one query?
- How do you handle NULL values in calculations?
- Can you explain the logical processing order of a SQL query?

---

# Summary

The core idea of this file is:

```text
WHERE
↓
Filter individual rows

GROUP BY
↓
Create groups

Aggregate Functions
↓
Calculate summary values

HAVING
↓
Filter those groups

CASE / COALESCE
↓
Add conditional logic and NULL handling
```

If an interviewer gives you an aggregation problem, first identify whether the condition applies to **individual rows** or to an **aggregated group**.

```text
Individual row condition
        ↓
      WHERE

Need groups
        ↓
    GROUP BY

Need calculation
        ↓
COUNT / SUM / AVG / MIN / MAX

Condition on calculation
        ↓
      HAVING
```

This reasoning pattern will help you solve most basic and intermediate SQL aggregation questions instead of memorizing individual queries.