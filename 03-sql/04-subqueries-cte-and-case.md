# SQL Subqueries, CTEs and CASE

## 1. What Are Subqueries, CTEs and CASE?

These are three important SQL concepts used to solve more complex queries:

- **Subquery** → A query inside another query
- **CTE (Common Table Expression)** → A temporary named result set used within a query
- **CASE** → Conditional logic inside SQL

They are commonly used in interview coding questions because they help solve problems such as:

- Finding employees earning more than the average salary
- Finding the second-highest salary
- Finding customers with orders
- Categorizing records
- Reusing intermediate query results
- Making complex queries easier to read

---

# 2. What Is a Subquery?

A **subquery** is a query written inside another SQL query.

Example:

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query:

```sql
SELECT AVG(salary)
FROM employees;
```

calculates the average salary.

The outer query then finds employees whose salary is greater than that average.

### Interview Answer

> A subquery is a query nested inside another query. The inner query produces a result that is used by the outer query.

---

# 3. Basic Subquery Structure

```sql
SELECT columns
FROM table
WHERE column operator (
    SELECT column
    FROM table
    WHERE condition
);
```

Example:

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 4. Why Do We Use Subqueries?

Subqueries are useful when the result of one query is needed by another query.

For example:

> Find employees earning more than the average salary.

Without a subquery, you would need another approach to calculate the average first.

With a subquery:

```sql
SELECT
    name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

This is concise and easy to understand.

---

# 5. Types of Subqueries

Important types to know for interviews:

```text
Scalar subquery
Single-row subquery
Multi-row subquery
Correlated subquery
Subquery in WHERE
Subquery in FROM
Subquery in SELECT
```

You do not need to memorize every classification. Understanding how and where subqueries are used is more important.

---

# 6. Scalar Subquery

A scalar subquery returns exactly one value.

Example:

```sql
SELECT AVG(salary)
FROM employees;
```

It returns something like:

```text
55000
```

Then:

```sql
SELECT
    name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query returns one value, so the outer query can compare each salary against it.

---

# 7. Single-Row Subquery

A single-row subquery returns one row.

Example:

```sql
SELECT name
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

The inner query identifies the IT department.

The outer query finds employees belonging to that department.

---

# 8. Multi-Row Subquery

A multi-row subquery returns multiple values.

For multiple values, operators such as:

```text
IN
ANY
ALL
```

can be used.

Example:

```sql
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Hyderabad'
);
```

The inner query may return:

```text
10
20
30
```

Then the outer query finds employees whose department is one of those values.

---

# 9. IN with Subquery

`IN` checks whether a value exists in the result of a subquery.

Example:

```sql
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE department_name IN ('IT', 'HR')
);
```

This is useful when the subquery returns multiple values.

---

# 10. NOT IN with Subquery

Example:

```sql
SELECT name
FROM employees
WHERE department_id NOT IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Chennai'
);
```

This returns employees whose department is not in the subquery result.

### Important NULL Consideration

Be careful with `NOT IN` when the subquery can return `NULL`.

For anti-matching logic, `NOT EXISTS` is often safer when NULLs are possible.

---

# 11. EXISTS

`EXISTS` checks whether the subquery returns at least one row.

Example:

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

This returns customers who have at least one order.

The important point is that `EXISTS` is checking for the existence of a matching row.

---

# 12. NOT EXISTS

`NOT EXISTS` checks whether the subquery returns no rows.

Example:

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

This finds customers who have never placed an order.

---

# 13. EXISTS vs IN

Both can sometimes solve similar problems.

### IN

```sql
SELECT name
FROM employees
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Hyderabad'
);
```

### EXISTS

```sql
SELECT
    e.name
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM departments d
    WHERE d.department_id = e.department_id
      AND d.location = 'Hyderabad'
);
```

### Interview Answer

> IN compares a value against a set of values returned by a subquery, while EXISTS checks whether at least one matching row exists. The better choice depends on the query and data, and performance should be evaluated using the database's execution plan rather than assuming one is always faster.

---

# 14. Correlated Subquery

A correlated subquery references a column from the outer query.

Example:

```sql
SELECT
    e.name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

The inner query refers to:

```sql
e.department_id
```

from the outer query.

Therefore, the inner query is correlated with the outer query.

---

# 15. What Is a Correlated Subquery?

### Interview Answer

> A correlated subquery is a subquery that depends on a value from the outer query. Conceptually, the inner query is evaluated in the context of each outer row, although the optimizer may transform the execution plan.

---

# 16. Real-World Example of Correlated Subquery

Question:

> Find employees whose salary is greater than the average salary of their own department.

```sql
SELECT
    e.name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

This is a very useful interview example because it tests:

```text
Subqueries
Aliases
Aggregation
Correlation
```

---

# 17. Subquery in WHERE

This is the most common form.

Example:

```sql
SELECT name
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The subquery provides a value used by the `WHERE` condition.

---

# 18. Subquery in FROM

A subquery can be used as a derived table.

Example:

```sql
SELECT
    department_id,
    avg_salary
FROM (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS dept_avg;
```

The inner query creates an intermediate result.

The outer query reads from it.

### Important

A derived table in the `FROM` clause normally needs an alias:

```sql
AS dept_avg
```

---

# 19. Subquery in SELECT

A scalar subquery can appear in the `SELECT` list.

Example:

```sql
SELECT
    name,
    salary,
    (SELECT AVG(salary) FROM employees) AS company_avg_salary
FROM employees;
```

Result conceptually:

| name | salary | company_avg_salary |
|---|---:|---:|
| Rahul | 60000 | 55000 |
| Priya | 50000 | 55000 |
| Arjun | 70000 | 55000 |

The company average is displayed alongside every employee.

---

# 20. Subquery vs JOIN

Example using JOIN:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

A subquery can sometimes retrieve related information, but JOINs are generally natural when you need to combine columns from related tables.

### Interview Answer

> JOINs are generally used to combine related tables, while subqueries are useful when one query's result is needed as input to another query. They can sometimes solve the same problem, and the better approach depends on readability, semantics, and the database execution plan.

---

# 21. Subquery vs CTE

A subquery:

```sql
SELECT *
FROM (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS d;
```

A CTE:

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM dept_avg;
```

The CTE often makes complex queries easier to read.

---

# 22. What Is a CTE?

CTE stands for:

**Common Table Expression**

A CTE creates a named temporary result set that exists for the duration of a single SQL statement.

Syntax:

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT ...
FROM cte_name;
```

Example:

```sql
WITH high_salary AS (
    SELECT
        name,
        salary
    FROM employees
    WHERE salary > 60000
)
SELECT *
FROM high_salary;
```

---

# 23. Why Use CTEs?

CTEs are useful for:

- Improving readability
- Breaking complex queries into logical steps
- Reusing an intermediate result within a statement
- Writing recursive queries
- Making debugging easier

Instead of writing one huge query, you can divide the logic into meaningful stages.

---

# 24. CTE Example

Question:

> Find departments whose average salary is greater than 60,000.

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT
    department_id,
    avg_salary
FROM dept_avg
WHERE avg_salary > 60000;
```

The CTE first calculates department averages.

The outer query filters them.

---

# 25. Multiple CTEs

You can define multiple CTEs.

Example:

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
),
high_salary_depts AS (
    SELECT
        department_id
    FROM dept_avg
    WHERE avg_salary > 60000
)
SELECT
    e.name,
    e.department_id,
    e.salary
FROM employees e
JOIN high_salary_depts h
    ON e.department_id = h.department_id;
```

The second CTE can use the first CTE.

---

# 26. CTE vs Temporary Table

A CTE:

```text
Exists for one SQL statement
```

A temporary table:

```text
Can generally be referenced across multiple statements during its lifetime
```

A CTE is mainly useful for organizing query logic.

A temporary table is useful when you need an actual temporary table that can be reused across multiple statements or when you need specific temporary-table behavior.

---

# 27. Does a CTE Store Data Permanently?

No.

A CTE is not a permanent database object.

It exists only for the statement in which it is defined.

Example:

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 60000
)
SELECT *
FROM high_salary;
```

After the statement finishes, the CTE definition is gone.

---

# 28. CTE Does Not Automatically Mean Better Performance

A common misconception is:

> CTE is always faster.

This is not necessarily true.

A CTE is primarily a **query organization and readability feature**. Its actual execution depends on the database engine and optimizer.

### Interview Answer

> CTEs improve query readability and structure, but I would not assume they automatically improve performance. I would inspect the execution plan when performance matters.

---

# 29. Recursive CTE

A recursive CTE refers to itself.

It is useful for hierarchical data such as:

```text
CEO
 ↓
Manager
 ↓
Team Lead
 ↓
Employee
```

A recursive CTE generally contains:

```text
Anchor query
+
Recursive query
```

Conceptual example:

```sql
WITH RECURSIVE employee_hierarchy AS (
    SELECT
        employee_id,
        name,
        manager_id,
        1 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT
        e.employee_id,
        e.name,
        e.manager_id,
        eh.level + 1
    FROM employees e
    JOIN employee_hierarchy eh
        ON e.manager_id = eh.employee_id
)
SELECT *
FROM employee_hierarchy;
```

Exact recursive CTE syntax varies between database systems.

---

# 30. What Is CASE?

`CASE` provides conditional logic in SQL.

It is similar to:

```text
if
elif
else
```

in programming.

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 31. Basic CASE Syntax

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result3
END
```

Example:

```sql
SELECT
    name,
    CASE
        WHEN salary >= 60000 THEN 'High Salary'
        ELSE 'Low Salary'
    END AS salary_status
FROM employees;
```

---

# 32. CASE with Multiple Conditions

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'Excellent'
        WHEN salary >= 70000 THEN 'Good'
        WHEN salary >= 40000 THEN 'Average'
        ELSE 'Low'
    END AS salary_level
FROM employees;
```

The conditions are evaluated in order.

Once a matching condition is found, that result is returned.

---

# 33. Order of WHEN Conditions Matters

Consider:

```sql
CASE
    WHEN salary >= 40000 THEN 'Average'
    WHEN salary >= 70000 THEN 'Good'
    WHEN salary >= 100000 THEN 'Excellent'
    ELSE 'Low'
END
```

An employee earning:

```text
120000
```

will match:

```sql
salary >= 40000
```

first.

Therefore, the result will be:

```text
Average
```

The correct ordering is usually from the most specific/highest threshold to the lower threshold:

```sql
CASE
    WHEN salary >= 100000 THEN 'Excellent'
    WHEN salary >= 70000 THEN 'Good'
    WHEN salary >= 40000 THEN 'Average'
    ELSE 'Low'
END
```

---

# 34. CASE in SELECT

This is the most common use.

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 60000 THEN 'High'
        ELSE 'Low'
    END AS category
FROM employees;
```

---

# 35. CASE in ORDER BY

You can use CASE to implement custom sorting.

Example:

```sql
SELECT
    name,
    status
FROM employees
ORDER BY
    CASE
        WHEN status = 'Critical' THEN 1
        WHEN status = 'Pending' THEN 2
        WHEN status = 'Completed' THEN 3
        ELSE 4
    END;
```

This allows business-specific ordering.

---

# 36. CASE in WHERE

CASE can sometimes be used in filtering logic, but often a direct boolean condition is clearer.

Example:

```sql
SELECT *
FROM employees
WHERE
    CASE
        WHEN department_id = 10 THEN salary
        ELSE 0
    END > 50000;
```

This is valid in systems that support the expression as written, but usually a direct condition is easier to understand:

```sql
SELECT *
FROM employees
WHERE department_id = 10
  AND salary > 50000;
```

### Interview Tip

Use `CASE` when you need to **produce conditional values**. Do not use it unnecessarily when a simple `WHERE` condition expresses the logic more clearly.

---

# 37. CASE with Aggregate Functions

CASE becomes extremely powerful when combined with aggregation.

Question:

> Count employees earning more than 60,000.

One approach:

```sql
SELECT
    COUNT(
        CASE
            WHEN salary > 60000 THEN 1
        END
    ) AS high_salary_count
FROM employees;
```

Another common approach:

```sql
SELECT
    SUM(
        CASE
            WHEN salary > 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count
FROM employees;
```

---

# 38. Conditional Aggregation

Conditional aggregation is a very important interview technique.

Example:

```sql
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees
GROUP BY department_id;
```

This counts employees meeting a condition for each department.

---

# 39. Multiple Conditional Counts

Example:

```sql
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary >= 80000 THEN 1
            ELSE 0
        END
    ) AS high_salary,
    SUM(
        CASE
            WHEN salary < 80000 THEN 1
            ELSE 0
        END
    ) AS low_salary
FROM employees
GROUP BY department_id;
```

This can produce multiple conditional metrics in one query.

---

# 40. CASE with NULL

You can explicitly handle NULL values:

```sql
SELECT
    name,
    CASE
        WHEN department_id IS NULL THEN 'No Department'
        ELSE 'Assigned'
    END AS department_status
FROM employees;
```

Remember:

```sql
NULL = NULL
```

does not evaluate to TRUE.

Use:

```sql
IS NULL
```

or:

```sql
IS NOT NULL
```

for NULL checks.

---

# 41. CASE vs COALESCE

These solve different problems.

### CASE

Used for conditional logic:

```sql
CASE
    WHEN salary > 60000 THEN 'High'
    ELSE 'Low'
END
```

### COALESCE

Returns the first non-NULL value:

```sql
COALESCE(phone, email, 'Not Available')
```

Example:

```sql
SELECT
    name,
    COALESCE(phone, 'No Phone') AS phone
FROM customers;
```

### Interview Answer

> CASE is used for conditional branching, while COALESCE is commonly used to replace NULL with the first available non-NULL value.

---

# 42. Simple CASE Expression

There are two common forms of CASE.

### Searched CASE

```sql
CASE
    WHEN salary > 60000 THEN 'High'
    WHEN salary > 40000 THEN 'Medium'
    ELSE 'Low'
END
```

### Simple CASE

```sql
CASE department_id
    WHEN 10 THEN 'IT'
    WHEN 20 THEN 'HR'
    WHEN 30 THEN 'Sales'
    ELSE 'Other'
END
```

Simple CASE compares one expression with multiple values.

---

# 43. Searched CASE vs Simple CASE

### Simple CASE

```sql
CASE department_id
    WHEN 10 THEN 'IT'
    WHEN 20 THEN 'HR'
    ELSE 'Other'
END
```

### Searched CASE

```sql
CASE
    WHEN salary > 60000 THEN 'High'
    WHEN salary > 40000 THEN 'Medium'
    ELSE 'Low'
END
```

Use searched CASE when you need conditions such as:

```text
>
<
>=
<=
BETWEEN
IS NULL
multiple expressions
```

---

# 44. Important Interview Question — What Is a Subquery?

### Strong Answer

> A subquery is a query nested inside another SQL statement. It is used when the result of one query is needed as input to another query. Subqueries can appear in places such as WHERE, FROM, and SELECT, and they can be correlated with the outer query.

---

# 45. Important Interview Question — What Is a Correlated Subquery?

### Strong Answer

> A correlated subquery references a column from the outer query, so its logic depends on the current outer row. It is useful for problems such as comparing an employee's salary with the average salary of that employee's department.

Example:

```sql
SELECT
    e.name,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# 46. Important Interview Question — What Is a CTE?

### Strong Answer

> A CTE, or Common Table Expression, is a named temporary result set defined using WITH and available for the duration of a single SQL statement. It is mainly useful for making complex queries easier to read, organize, and maintain.

Example:

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM dept_avg;
```

---

# 47. Important Interview Question — CTE vs Subquery?

### Answer

> Both can represent intermediate query results. A CTE gives that result a name and usually makes multi-step logic easier to read. A subquery is often convenient for a small nested operation. The choice is primarily about query structure and readability, while actual performance depends on the database optimizer and execution plan.

---

# 48. Important Interview Question — What Is CASE?

### Strong Answer

> CASE is SQL's conditional expression. It evaluates conditions and returns a corresponding result, similar to if-else logic in programming. It is commonly used for categorization, conditional calculations, custom sorting, and conditional aggregation.

Example:

```sql
SELECT
    name,
    CASE
        WHEN salary >= 60000 THEN 'High'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 49. Important Interview Question — What Is EXISTS?

### Answer

> EXISTS checks whether a subquery returns at least one row. It is commonly used to test whether a related record exists.

Example:

```sql
SELECT
    c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# 50. Important Interview Question — EXISTS vs NOT EXISTS?

```text
EXISTS
→ Matching record exists

NOT EXISTS
→ Matching record does not exist
```

Example:

```sql
-- Customers with orders
SELECT c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

```sql
-- Customers without orders
SELECT c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# 51. Important Coding Question — Employees Earning Above Average

```sql
SELECT
    name,
    salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 52. Important Coding Question — Employees Earning Above Their Department Average

```sql
SELECT
    e.name,
    e.salary,
    e.department_id
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

---

# 53. Important Coding Question — Find Second Highest Salary

A common solution is:

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

This returns the second distinct highest salary when one exists.

Another common solution is:

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

For more complex ranking requirements, window functions are often preferable.

---

# 54. Important Coding Question — Find Employees in IT

Using a subquery:

```sql
SELECT
    name
FROM employees
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE department_name = 'IT'
);
```

If the department name is not unique, use `IN` or enforce the appropriate uniqueness constraint.

---

# 55. Important Coding Question — Find Customers Without Orders Using NOT EXISTS

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

This is an important alternative to:

```sql
LEFT JOIN ... IS NULL
```

---

# 56. Important Coding Question — Categorize Employees by Salary

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 100000 THEN 'High'
        WHEN salary >= 60000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employees;
```

---

# 57. Important Coding Question — Count Employees by Salary Category

```sql
SELECT
    SUM(
        CASE
            WHEN salary >= 100000 THEN 1
            ELSE 0
        END
    ) AS high_salary,
    SUM(
        CASE
            WHEN salary >= 60000
             AND salary < 100000 THEN 1
            ELSE 0
        END
    ) AS medium_salary,
    SUM(
        CASE
            WHEN salary < 60000 THEN 1
            ELSE 0
        END
    ) AS low_salary
FROM employees;
```

This is an example of conditional aggregation.

---

# 58. Important Coding Question — Find Departments with Average Salary Above 60,000 Using CTE

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT
    department_id,
    avg_salary
FROM dept_avg
WHERE avg_salary > 60000;
```

---

# 59. Important Coding Question — Use Multiple CTEs

```sql
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
),
high_salary_depts AS (
    SELECT
        department_id
    FROM dept_avg
    WHERE avg_salary > 60000
)
SELECT
    e.name,
    e.salary,
    e.department_id
FROM employees e
JOIN high_salary_depts h
    ON e.department_id = h.department_id;
```

---

# 60. Important Coding Question — Create a Derived Table

```sql
SELECT
    department_id,
    avg_salary
FROM (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS dept_avg;
```

This is a subquery in the `FROM` clause.

---

# 61. Important Coding Question — Company Average Alongside Every Employee

```sql
SELECT
    name,
    salary,
    (
        SELECT AVG(salary)
        FROM employees
    ) AS company_average
FROM employees;
```

---

# 62. Important Coding Question — Custom Employee Status

Suppose employees have a status:

```text
Active
Inactive
On Leave
```

We can categorize them:

```sql
SELECT
    name,
    CASE
        WHEN status = 'Active' THEN 'Currently Working'
        WHEN status = 'On Leave' THEN 'Temporarily Away'
        ELSE 'Not Working'
    END AS employee_status
FROM employees;
```

---

# 63. Important Coding Question — Conditional Aggregation by Department

```sql
SELECT
    department_id,
    COUNT(*) AS total_employees,
    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_employees
FROM employees
GROUP BY department_id;
```

This returns both:

```text
Total employees
High-salary employees
```

for every department.

---

# 64. Common Mistakes with Subqueries

### Mistake 1 — Using `=` when multiple rows are returned

Incorrect if the subquery returns multiple rows:

```sql
WHERE department_id = (
    SELECT department_id
    FROM departments
    WHERE location = 'Hyderabad'
);
```

If multiple departments are returned, use:

```sql
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE location = 'Hyderabad'
);
```

---

### Mistake 2 — Ignoring NULL with NOT IN

Be careful with:

```sql
WHERE id NOT IN (
    SELECT id
    FROM table_b
);
```

If the subquery contains NULL, three-valued SQL logic can produce unexpected results.

Consider:

```sql
NOT EXISTS
```

when appropriate.

---

# 65. Common Mistakes with CTEs

### Mistake 1 — Thinking CTE is permanent

It is not.

```text
CTE
→ Exists only for the current statement
```

### Mistake 2 — Assuming CTE always improves performance

It does not necessarily.

Use the execution plan when performance matters.

### Mistake 3 — Using CTE when a simple query is clearer

Do not add complexity just for the sake of using a CTE.

---

# 66. Common Mistakes with CASE

### Mistake 1 — Wrong condition order

Incorrect:

```sql
CASE
    WHEN salary >= 40000 THEN 'Average'
    WHEN salary >= 80000 THEN 'High'
    ELSE 'Low'
END
```

Correct:

```sql
CASE
    WHEN salary >= 80000 THEN 'High'
    WHEN salary >= 40000 THEN 'Average'
    ELSE 'Low'
END
```

### Mistake 2 — Forgetting ELSE

If no condition matches and there is no ELSE, the result is generally NULL.

Example:

```sql
CASE
    WHEN salary >= 60000 THEN 'High'
END
```

Employees below 60000 receive NULL.

---

# 67. Subquery + CASE Example

These concepts can be combined.

Question:

> Categorize employees based on whether their salary is above the company average.

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary > (
            SELECT AVG(salary)
            FROM employees
        )
        THEN 'Above Average'
        ELSE 'Below or Equal Average'
    END AS salary_status
FROM employees;
```

---

# 68. CTE + CASE Example

```sql
WITH employee_data AS (
    SELECT
        name,
        salary
    FROM employees
)
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_category
FROM employee_data;
```

---

# 69. CTE + JOIN + CASE Example

```sql
WITH dept_salary AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT
    d.department_name,
    ds.avg_salary,
    CASE
        WHEN ds.avg_salary >= 80000 THEN 'High Paying'
        WHEN ds.avg_salary >= 50000 THEN 'Medium Paying'
        ELSE 'Low Paying'
    END AS department_category
FROM dept_salary ds
JOIN departments d
    ON ds.department_id = d.department_id;
```

This combines:

```text
CTE
JOIN
GROUP BY
AVG
CASE
```

---

# 70. Interview Scenario — Which Should You Choose?

### Scenario 1

> I need to compare a value with one calculated value.

Use:

```text
Scalar subquery
```

Example:

```sql
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
```

---

### Scenario 2

> I need to check whether a related record exists.

Use:

```text
EXISTS
```

Example:

```sql
WHERE EXISTS (...)
```

---

### Scenario 3

> I need a complex query broken into logical steps.

Consider:

```text
CTE
```

Example:

```sql
WITH step1 AS (...),
step2 AS (...)
SELECT ...
```

---

### Scenario 4

> I need if/else-like logic.

Use:

```text
CASE
```

Example:

```sql
CASE
    WHEN condition THEN result
    ELSE result
END
```

---

### Scenario 5

> I need different counts based on conditions.

Use:

```text
CASE + aggregation
```

Example:

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

---

# 71. High-Value Interview Concepts

You should be particularly comfortable with these:

```text
1. Subquery
2. Scalar subquery
3. IN with subquery
4. EXISTS
5. NOT EXISTS
6. Correlated subquery
7. CTE
8. Multiple CTEs
9. Recursive CTE basics
10. CTE vs subquery
11. CASE
12. Simple CASE
13. Searched CASE
14. CASE with aggregation
15. Conditional aggregation
16. CASE + NULL
17. Subquery + JOIN
18. CTE + JOIN
```

---

# 72. Quick Revision Table

| Concept | Main Purpose | Example |
|---|---|---|
| Subquery | Query inside another query | `WHERE salary > (SELECT AVG(...))` |
| Scalar subquery | Return one value | `SELECT AVG(salary)` |
| `IN` | Match against multiple values | `WHERE id IN (SELECT id...)` |
| `EXISTS` | Check whether rows exist | `WHERE EXISTS (...)` |
| `NOT EXISTS` | Check whether rows don't exist | `WHERE NOT EXISTS (...)` |
| Correlated subquery | Inner query depends on outer row | Department average |
| CTE | Organize intermediate query results | `WITH x AS (...)` |
| Recursive CTE | Hierarchical/recursive data | Employee hierarchy |
| CASE | Conditional logic | Salary category |
| Conditional aggregation | Aggregate based on condition | `SUM(CASE...)` |

---

# 73. Most Important Coding Patterns to Memorize

## Pattern 1 — Above Average

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

## Pattern 2 — Above Department Average

```sql
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

## Pattern 3 — Exists

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

## Pattern 4 — Does Not Exist

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

## Pattern 5 — CTE

```sql
WITH result AS (
    SELECT ...
)
SELECT *
FROM result;
```

## Pattern 6 — CASE

```sql
CASE
    WHEN condition THEN value
    ELSE value
END
```

## Pattern 7 — Conditional Count

```sql
SUM(
    CASE
        WHEN condition THEN 1
        ELSE 0
    END
)
```

---

# 74. Interview Questions for Practice

## Conceptual Questions

1. What is a subquery?
2. Why do we use subqueries?
3. What is a scalar subquery?
4. What is a correlated subquery?
5. What is the difference between correlated and non-correlated subqueries?
6. What is the difference between `IN` and `EXISTS`?
7. What is `NOT EXISTS`?
8. What problems can occur with `NOT IN` and NULL values?
9. Can a subquery be used in the SELECT clause?
10. Can a subquery be used in the FROM clause?
11. What is a derived table?
12. What is a CTE?
13. Why are CTEs useful?
14. CTE vs subquery?
15. CTE vs temporary table?
16. Does a CTE permanently store data?
17. Does a CTE always improve performance?
18. What is a recursive CTE?
19. What is CASE?
20. What is the difference between simple CASE and searched CASE?
21. Can CASE be used with aggregate functions?
22. What is conditional aggregation?
23. CASE vs COALESCE?
24. What happens if no CASE condition matches?
25. Why does the order of WHEN conditions matter?

---

# 75. Coding Questions for Practice

Try solving these without looking at the answers first.

### Q1. Find employees whose salary is greater than the company average.

### Q2. Find employees whose salary is greater than their department average.

### Q3. Find customers who have placed at least one order.

### Q4. Find customers who have never placed an order.

### Q5. Find the second-highest distinct salary.

### Q6. Find employees who belong to departments located in Hyderabad.

### Q7. Categorize employees as High, Medium, or Low salary.

### Q8. Count high-salary employees in each department.

### Q9. Calculate average salary per department using a CTE.

### Q10. Find departments whose average salary is greater than 60,000 using a CTE.

### Q11. Display the company average salary alongside every employee.

### Q12. Find employees earning more than their department average using a correlated subquery.

### Q13. Use a CTE to find high-paying departments and then return employees from those departments.

### Q14. Use `NOT EXISTS` to find customers without orders.

### Q15. Use CASE to create a custom employee status.

---

# 76. Final Interview Cheat Sheet

```text
SUBQUERY
→ Query inside another query

SCALAR SUBQUERY
→ Returns one value

IN
→ Compare against a set of values

EXISTS
→ Does at least one matching row exist?

NOT EXISTS
→ Does no matching row exist?

CORRELATED SUBQUERY
→ Inner query depends on outer query

CTE
→ Named temporary result for one SQL statement

RECURSIVE CTE
→ Useful for hierarchical/recursive relationships

CASE
→ SQL conditional logic

CONDITIONAL AGGREGATION
→ SUM/COUNT + CASE
```

### The Four Patterns You Should Know Extremely Well

```sql
-- 1. Subquery
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

```sql
-- 2. Correlated subquery
SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

```sql
-- 3. CTE
WITH dept_avg AS (
    SELECT
        department_id,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT *
FROM dept_avg
WHERE avg_salary > 60000;
```

```sql
-- 4. CASE + conditional aggregation
SELECT
    department_id,
    SUM(
        CASE
            WHEN salary >= 60000 THEN 1
            ELSE 0
        END
    ) AS high_salary_count
FROM employees
GROUP BY department_id;
```

If you understand these patterns and can modify them for different interview scenarios, you have covered the core interview-level concepts of **subqueries, CTEs, and CASE expressions**.