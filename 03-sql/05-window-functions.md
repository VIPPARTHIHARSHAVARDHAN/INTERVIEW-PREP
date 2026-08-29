# SQL Window Functions

## 1. What Are Window Functions?

A **window function** performs a calculation across a set of rows related to the current row, while still keeping the individual rows in the result.

This is the key difference from `GROUP BY`.

With `GROUP BY`, multiple rows are usually collapsed into one row per group.

With a window function, the original rows remain visible and the calculation is added alongside them.

### Example

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg_salary
FROM employees;
```

The result can look like:

| name | department_id | salary | department_avg_salary |
|---|---:|---:|---:|
| Rahul | 10 | 60000 | 65000 |
| Priya | 10 | 70000 | 65000 |
| Arjun | 20 | 50000 | 55000 |
| Sneha | 20 | 60000 | 55000 |

Every employee remains in the result, while the department average is calculated beside each employee.

---

# 2. Why Are Window Functions Important?

Window functions are one of the **most important SQL topics for interviews**.

They are frequently used for:

- Ranking
- Finding top N records
- Finding the second-highest salary
- Comparing a row with the previous/next row
- Running totals
- Moving averages
- Percentage calculations
- Department-wise comparisons
- Removing duplicates
- Finding the latest record
- Month-over-month comparisons

You should be comfortable writing and explaining window-function queries.

---

# 3. Basic Syntax

```sql
function_name() OVER (
    PARTITION BY column
    ORDER BY column
)
```

Example:

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

The `OVER()` clause tells SQL that the function should operate as a window function.

---

# 4. Important Parts of a Window Function

A window definition can contain:

```sql
OVER (
    PARTITION BY ...
    ORDER BY ...
    ROWS ...
)
```

These parts have different purposes.

### `PARTITION BY`

Divides rows into groups for the window calculation.

### `ORDER BY`

Defines the order in which rows are considered.

### Frame specification

Such as:

```sql
ROWS BETWEEN ...
```

controls exactly which rows are included in the calculation for the current row.

---

# 5. What Is PARTITION BY?

`PARTITION BY` divides the result into logical groups without collapsing the rows.

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg
FROM employees;
```

Employees are logically separated by department.

The average is calculated separately for each department.

---

# 6. PARTITION BY vs GROUP BY

This is a very common interview question.

### GROUP BY

```sql
SELECT
    department_id,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id;
```

Result:

| department_id | avg_salary |
|---:|---:|
| 10 | 65000 |
| 20 | 55000 |

The individual employee rows are no longer present.

### Window Function

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS avg_salary
FROM employees;
```

Result:

| name | department_id | salary | avg_salary |
|---|---:|---:|---:|
| Rahul | 10 | 60000 | 65000 |
| Priya | 10 | 70000 | 65000 |
| Arjun | 20 | 50000 | 55000 |
| Sneha | 20 | 60000 | 55000 |

### Strong Interview Answer

> `GROUP BY` collapses rows into groups, while a window function performs calculations across related rows without removing the individual rows from the result.

---

# 7. ORDER BY Inside OVER()

Consider:

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

The rows are ordered by salary from highest to lowest for the purpose of assigning row numbers.

Important:

```sql
ORDER BY salary DESC
```

inside `OVER()` controls the window calculation.

It does not necessarily control the final display order of the query.

If you want the final output sorted, use an outer:

```sql
ORDER BY
```

Example:

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees
ORDER BY salary DESC;
```

---

# 8. Main Window Functions You Should Know

The most important interview functions are:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM()
AVG()
MIN()
MAX()
COUNT()
```

You should especially understand:

```text
ROW_NUMBER
RANK
DENSE_RANK
LAG
LEAD
SUM OVER
AVG OVER
```

---

# 9. ROW_NUMBER()

`ROW_NUMBER()` assigns a unique sequential number to each row.

Example:

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

Possible result:

| name | salary | row_num |
|---|---:|---:|
| Arjun | 90000 | 1 |
| Rahul | 80000 | 2 |
| Priya | 80000 | 3 |
| Sneha | 70000 | 4 |

Even if two employees have the same salary, their row numbers are different.

---

# 10. RANK()

`RANK()` gives the same rank to tied values and leaves gaps after ties.

Example:

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Possible result:

| name | salary | rank |
|---|---:|---:|
| Arjun | 90000 | 1 |
| Rahul | 80000 | 2 |
| Priya | 80000 | 2 |
| Sneha | 70000 | 4 |

Notice:

```text
1
2
2
4
```

Rank `3` is skipped.

---

# 11. DENSE_RANK()

`DENSE_RANK()` also gives the same rank to tied values, but it does not leave gaps.

```sql
SELECT
    name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Result:

| name | salary | dense_rank |
|---|---:|---:|
| Arjun | 90000 | 1 |
| Rahul | 80000 | 2 |
| Priya | 80000 | 2 |
| Sneha | 70000 | 3 |

Notice:

```text
1
2
2
3
```

---

# 12. ROW_NUMBER vs RANK vs DENSE_RANK

This is one of the **most important SQL interview questions**.

Suppose salaries are:

```text
100000
90000
90000
80000
```

### ROW_NUMBER()

```text
1
2
3
4
```

Every row gets a unique number.

### RANK()

```text
1
2
2
4
```

Ties share rank and gaps are created.

### DENSE_RANK()

```text
1
2
2
3
```

Ties share rank but no gaps are created.

### Easy Way to Remember

```text
ROW_NUMBER
→ Unique position

RANK
→ Same rank for ties + gaps

DENSE_RANK
→ Same rank for ties + no gaps
```

---

# 13. PARTITION BY with ROW_NUMBER()

This is extremely important for interview problems.

```sql
SELECT
    name,
    department_id,
    salary,
    ROW_NUMBER() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS dept_row_num
FROM employees;
```

Now numbering restarts for every department.

Example:

| name | department_id | salary | dept_row_num |
|---|---:|---:|---:|
| Rahul | 10 | 80000 | 1 |
| Priya | 10 | 70000 | 2 |
| Arjun | 20 | 90000 | 1 |
| Sneha | 20 | 60000 | 2 |

---

# 14. Top Employee in Each Department

This is a classic interview problem.

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked_employees
WHERE rn = 1;
```

This returns one highest-paid employee from each department.

---

# 15. Top 3 Employees in Each Department

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked_employees
WHERE rn <= 3;
```

This is one of the most useful window-function patterns to memorize.

---

# 16. Top N per Group Pattern

General pattern:

```sql
WITH ranked_data AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY group_column
            ORDER BY value_column DESC
        ) AS rn
    FROM table_name
)
SELECT *
FROM ranked_data
WHERE rn <= N;
```

Example:

```sql
WITH ranked_employees AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE rn <= 3;
```

---

# 17. Finding the Second-Highest Salary Using DENSE_RANK()

```sql
WITH ranked_employees AS (
    SELECT
        name,
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    salary
FROM ranked_employees
WHERE salary_rank = 2;
```

Using `DENSE_RANK()` means employees sharing the second-highest distinct salary are all returned.

---

# 18. RANK vs DENSE_RANK for Second Highest Salary

Suppose salaries are:

```text
100000
90000
90000
80000
```

Using:

```sql
RANK()
```

produces:

```text
1
2
2
4
```

Second-highest salary is still rank `2`.

Using:

```sql
DENSE_RANK()
```

produces:

```text
1
2
2
3
```

Both can identify the second distinct salary here.

For problems involving the Nth **distinct** salary, `DENSE_RANK()` is usually the clearer choice.

---

# 19. LAG()

`LAG()` accesses a value from a previous row.

Example:

```sql
SELECT
    order_date,
    sales,
    LAG(sales) OVER (
        ORDER BY order_date
    ) AS previous_day_sales
FROM daily_sales;
```

Possible result:

| order_date | sales | previous_day_sales |
|---|---:|---:|
| 2026-01-01 | 10000 | NULL |
| 2026-01-02 | 12000 | 10000 |
| 2026-01-03 | 15000 | 12000 |

---

# 20. Why Is LAG() Useful?

It is useful when comparing the current row with a previous row.

Examples:

```text
Current month vs previous month
Current day vs previous day
Current salary vs previous salary
Current stock price vs previous price
Current order vs previous order
```

---

# 21. LEAD()

`LEAD()` accesses a value from a following row.

Example:

```sql
SELECT
    order_date,
    sales,
    LEAD(sales) OVER (
        ORDER BY order_date
    ) AS next_day_sales
FROM daily_sales;
```

Possible result:

| order_date | sales | next_day_sales |
|---|---:|---:|
| 2026-01-01 | 10000 | 12000 |
| 2026-01-02 | 12000 | 15000 |
| 2026-01-03 | 15000 | NULL |

---

# 22. LAG vs LEAD

```text
LAG
→ Previous row

LEAD
→ Next row
```

Example:

```sql
LAG(salary) OVER (ORDER BY employee_id)
```

gets the previous salary.

```sql
LEAD(salary) OVER (ORDER BY employee_id)
```

gets the next salary.

---

# 23. LAG with Difference Calculation

A common interview problem:

> Find the difference between current sales and previous day's sales.

```sql
SELECT
    order_date,
    sales,
    sales - LAG(sales) OVER (
        ORDER BY order_date
    ) AS sales_difference
FROM daily_sales;
```

The first row will generally have `NULL` for the difference because there is no previous row.

---

# 24. LAG with Percentage Change

```sql
SELECT
    order_date,
    sales,
    (
        sales - LAG(sales) OVER (
            ORDER BY order_date
        )
    ) * 100.0
    / NULLIF(
        LAG(sales) OVER (
            ORDER BY order_date
        ),
        0
    ) AS percentage_change
FROM daily_sales;
```

`NULLIF(..., 0)` helps avoid division by zero.

---

# 25. LAG with PARTITION BY

Suppose sales belong to different stores.

```sql
SELECT
    store_id,
    sales_date,
    sales,
    LAG(sales) OVER (
        PARTITION BY store_id
        ORDER BY sales_date
    ) AS previous_sales
FROM store_sales;
```

The previous value is calculated separately for each store.

This is an important real-world pattern.

---

# 26. Running Total

A running total is a cumulative sum.

Example:

```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM daily_sales;
```

Possible result:

| order_date | sales | running_total |
|---|---:|---:|
| Jan 1 | 100 | 100 |
| Jan 2 | 200 | 300 |
| Jan 3 | 150 | 450 |
| Jan 4 | 250 | 700 |

---

# 27. Simpler Running Total Syntax

Depending on the database and desired frame semantics, you may commonly see:

```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
    ) AS running_total
FROM daily_sales;
```

For interview answers where duplicate ordering values may matter, explicitly specifying the frame can make the intended behavior clearer.

---

# 28. Running Total by Customer

```sql
SELECT
    customer_id,
    order_date,
    amount,
    SUM(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS customer_running_total
FROM orders;
```

The running total starts again for every customer.

---

# 29. Moving Average

A moving average calculates an average over a sliding window of rows.

Example:

```sql
SELECT
    order_date,
    sales,
    AVG(sales) OVER (
        ORDER BY order_date
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS moving_avg
FROM daily_sales;
```

This calculates a three-row moving average:

```text
Current row
+
Previous row
+
Two rows before current
```

---

# 30. Window Frame

A window frame controls the exact rows used by a window calculation.

Example:

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

means:

```text
2 previous rows
+
current row
```

Another example:

```sql
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
```

means:

```text
Beginning of partition
→ current row
```

This is commonly used for running totals.

---

# 31. UNBOUNDED PRECEDING

```sql
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
```

means:

> Start from the first row of the window and continue through the current row.

Example:

```sql
SUM(amount) OVER (
    ORDER BY order_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

---

# 32. FIRST_VALUE()

`FIRST_VALUE()` returns the first value in the window according to the window ordering.

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    FIRST_VALUE(name) OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS highest_paid_employee
FROM employees;
```

Each employee in the department can see the name of the highest-paid employee.

---

# 33. LAST_VALUE()

`LAST_VALUE()` returns the last value according to the window frame.

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    LAST_VALUE(salary) OVER (
        PARTITION BY department_id
        ORDER BY salary
        ROWS BETWEEN UNBOUNDED PRECEDING
                 AND UNBOUNDED FOLLOWING
    ) AS highest_salary
FROM employees;
```

### Important Interview Point

`LAST_VALUE()` can be confusing because the default window frame may end at the current row depending on the database and query.

When you want the last value across the entire partition, explicitly defining the frame is safer:

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
         AND UNBOUNDED FOLLOWING
```

---

# 34. Aggregate Functions as Window Functions

Many aggregate functions can be used with `OVER()`.

Examples:

```sql
SUM() OVER (...)
AVG() OVER (...)
COUNT() OVER (...)
MIN() OVER (...)
MAX() OVER (...)
```

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    MAX(salary) OVER (
        PARTITION BY department_id
    ) AS department_max_salary
FROM employees;
```

---

# 35. Compare Employee Salary with Department Maximum

```sql
SELECT
    name,
    department_id,
    salary,
    MAX(salary) OVER (
        PARTITION BY department_id
    ) AS max_dept_salary
FROM employees;
```

Now every employee row contains the maximum salary of their department.

---

# 36. Find Employees with Maximum Department Salary

```sql
WITH employee_data AS (
    SELECT
        name,
        department_id,
        salary,
        MAX(salary) OVER (
            PARTITION BY department_id
        ) AS max_dept_salary
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM employee_data
WHERE salary = max_dept_salary;
```

Unlike `ROW_NUMBER()`, this returns all employees tied for the maximum salary.

---

# 37. COUNT() OVER()

Example:

```sql
SELECT
    name,
    department_id,
    COUNT(*) OVER (
        PARTITION BY department_id
    ) AS department_employee_count
FROM employees;
```

Every employee row shows the number of employees in their department.

---

# 38. Percentage of Department Total

A very useful business/interview problem:

> What percentage of the department's total salary does each employee contribute?

```sql
SELECT
    name,
    department_id,
    salary,
    salary * 100.0
    / SUM(salary) OVER (
        PARTITION BY department_id
    ) AS salary_percentage
FROM employees;
```

This is a strong example of window functions in real-world analytics.

---

# 39. Percentage of Company Total

```sql
SELECT
    name,
    salary,
    salary * 100.0
    / SUM(salary) OVER () AS company_salary_percentage
FROM employees;
```

Notice:

```sql
OVER ()
```

has no `PARTITION BY`, so the calculation uses the entire result set.

---

# 40. Window Function with No PARTITION BY

Example:

```sql
SELECT
    name,
    salary,
    AVG(salary) OVER () AS company_average
FROM employees;
```

This calculates one company-wide average and displays it on every employee row.

---

# 41. PARTITION BY vs No PARTITION BY

### Without PARTITION BY

```sql
AVG(salary) OVER ()
```

Calculation is across the entire result set.

### With PARTITION BY

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

Calculation is performed separately for each department.

---

# 42. Can Window Functions Be Used in WHERE?

Generally, you cannot directly use a window function in the `WHERE` clause of the same query block.

For example, this is generally invalid:

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS rn
FROM employees
WHERE rn <= 3;
```

Why?

Because the window function is calculated after the filtering phase for that query block.

Instead, use a CTE or derived table.

```sql
WITH ranked_employees AS (
    SELECT
        name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT
    name,
    salary
FROM ranked_employees
WHERE rn <= 3;
```

This is extremely important for interviews.

---

# 43. Window Functions and SQL Logical Processing Order

A simplified logical order is:

```text
FROM
JOIN
WHERE
GROUP BY
HAVING
SELECT
WINDOW FUNCTIONS
ORDER BY
```

The exact implementation and optimizer behavior can vary, but conceptually this explains why you usually cannot reference a window-function alias directly in the same query block's `WHERE`.

---

# 44. Can Window Functions Be Used with GROUP BY?

Yes.

Example:

```sql
SELECT
    department_id,
    COUNT(*) AS employee_count,
    RANK() OVER (
        ORDER BY COUNT(*) DESC
    ) AS department_rank
FROM employees
GROUP BY department_id;
```

Here:

1. Employees are grouped by department.
2. The count is calculated.
3. The resulting department groups are ranked.

This is a useful advanced pattern.

---

# 45. Window Functions with CTE

This combination is extremely common.

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE salary_rank <= 3;
```

The CTE allows you to filter the window-function result in the outer query.

---

# 46. Finding Duplicate Records Using ROW_NUMBER()

Suppose duplicates are defined by:

```text
email
```

You can assign row numbers:

```sql
WITH duplicates AS (
    SELECT
        customer_id,
        email,
        ROW_NUMBER() OVER (
            PARTITION BY email
            ORDER BY customer_id
        ) AS rn
    FROM customers
)
SELECT *
FROM duplicates
WHERE rn > 1;
```

The first record for each email gets:

```text
rn = 1
```

Additional records get:

```text
rn = 2, 3, ...
```

---

# 47. Keeping One Record and Removing Duplicates

A common data-cleaning pattern is:

```sql
WITH duplicates AS (
    SELECT
        customer_id,
        email,
        ROW_NUMBER() OVER (
            PARTITION BY email
            ORDER BY customer_id
        ) AS rn
    FROM customers
)
SELECT *
FROM duplicates
WHERE rn = 1;
```

This keeps one record per email.

For actual deletion, use extreme caution and verify the business rule before executing a `DELETE`.

---

# 48. Finding the Latest Record Per Customer

This is a very common real-world SQL problem.

Suppose customers have multiple transactions.

```sql
WITH ranked_orders AS (
    SELECT
        customer_id,
        order_id,
        order_date,
        amount,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC, order_id DESC
        ) AS rn
    FROM orders
)
SELECT
    customer_id,
    order_id,
    order_date,
    amount
FROM ranked_orders
WHERE rn = 1;
```

This returns the latest order for every customer.

The additional `order_id DESC` provides a deterministic tie-breaker when two orders have the same date.

---

# 49. Real-World Example — Sales Analysis

Imagine an e-commerce company has:

```text
customer_id
order_date
order_amount
```

The business wants:

- Total sales
- Running sales
- Previous order amount
- Difference from previous order

A window-function query can do this:

```sql
SELECT
    customer_id,
    order_date,
    order_amount,

    SUM(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_sales,

    LAG(order_amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS previous_order_amount

FROM orders;
```

This is a practical analytics use case.

---

# 50. Real-World Example — Employee Analytics

HR wants to know:

- Employee salary
- Department average
- Department rank

```sql
SELECT
    name,
    department_id,
    salary,

    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average,

    DENSE_RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS department_rank

FROM employees;
```

This gives multiple analytical metrics without collapsing employee rows.

---

# 51. Real-World Example — Monthly Sales Comparison

Suppose sales data is:

```text
month
sales
```

To compare each month with the previous month:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales,
    sales - LAG(sales) OVER (
        ORDER BY month
    ) AS difference
FROM monthly_sales;
```

This is useful for:

```text
Month-over-month analysis
Growth analysis
Business reporting
Dashboard metrics
```

---

# 52. Important Interview Question — What Is a Window Function?

### Strong Answer

> A window function performs a calculation across a set of rows related to the current row while preserving the individual rows in the result. It is commonly used for ranking, running totals, comparisons with previous or next rows, and analytical calculations.

---

# 53. Important Interview Question — What Does OVER() Do?

### Strong Answer

> `OVER()` defines the window of rows over which a window function operates. It can optionally contain `PARTITION BY`, `ORDER BY`, and a frame specification such as `ROWS BETWEEN`.

Example:

```sql
AVG(salary) OVER (
    PARTITION BY department_id
)
```

---

# 54. Important Interview Question — What Is PARTITION BY?

### Strong Answer

> `PARTITION BY` divides rows into logical groups for the window calculation without collapsing those rows. For example, `AVG(salary) OVER (PARTITION BY department_id)` calculates the average salary separately for each department while keeping every employee row.

---

# 55. Important Interview Question — Difference Between GROUP BY and Window Functions?

### Strong Answer

> `GROUP BY` combines rows into groups and returns one row per group, while window functions calculate across related rows without collapsing the original rows.

---

# 56. Important Interview Question — Difference Between ROW_NUMBER, RANK and DENSE_RANK?

### Strong Answer

> `ROW_NUMBER()` gives every row a unique sequential number. `RANK()` assigns the same rank to ties but leaves gaps after tied values. `DENSE_RANK()` also assigns the same rank to ties but does not leave gaps.

Example:

```text
Values:
100
90
90
80

ROW_NUMBER:
1
2
3
4

RANK:
1
2
2
4

DENSE_RANK:
1
2
2
3
```

---

# 57. Important Interview Question — What Is LAG?

### Answer

> `LAG()` returns a value from a previous row in the window according to the specified ordering. It is commonly used for previous-period comparisons.

Example:

```sql
SELECT
    order_date,
    sales,
    LAG(sales) OVER (
        ORDER BY order_date
    ) AS previous_sales
FROM daily_sales;
```

---

# 58. Important Interview Question — What Is LEAD?

### Answer

> `LEAD()` returns a value from a following row in the window according to the specified ordering. It is useful when comparing the current row with a future row.

Example:

```sql
SELECT
    order_date,
    sales,
    LEAD(sales) OVER (
        ORDER BY order_date
    ) AS next_sales
FROM daily_sales;
```

---

# 59. Important Interview Question — Can Window Functions Be Used in WHERE?

### Strong Answer

> Generally, a window function cannot be directly filtered in the `WHERE` clause of the same query block. A common solution is to calculate the window function in a CTE or derived table and then filter it in the outer query.

Example:

```sql
WITH ranked AS (
    SELECT
        name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

---

# 60. Important Interview Question — What Is a Window Frame?

### Strong Answer

> A window frame specifies the subset of rows within the window that should be used for the calculation of the current row. For example, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` is commonly used for a running total.

---

# 61. Important Coding Question — Rank Employees by Salary

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

---

# 62. Important Coding Question — Rank Employees Within Each Department

```sql
SELECT
    name,
    department_id,
    salary,
    DENSE_RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS department_rank
FROM employees;
```

---

# 63. Important Coding Question — Find Top 3 Salaries in Each Department

If ties should occupy separate positions:

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

If the requirement is **top 3 distinct salary levels**, use `DENSE_RANK()`:

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT *
FROM ranked
WHERE salary_rank <= 3;
```

This distinction is important in interviews.

---

# 64. Important Coding Question — Find Second-Highest Salary

```sql
WITH ranked AS (
    SELECT
        name,
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    salary
FROM ranked
WHERE salary_rank = 2;
```

---

# 65. Important Coding Question — Find Highest-Paid Employee in Each Department

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked
WHERE rn = 1;
```

If all employees tied for the highest salary should be returned:

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked
WHERE salary_rank = 1;
```

---

# 66. Important Coding Question — Running Total

```sql
SELECT
    order_date,
    amount,
    SUM(amount) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM orders;
```

---

# 67. Important Coding Question — Previous Order Amount

```sql
SELECT
    customer_id,
    order_date,
    amount,
    LAG(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS previous_amount
FROM orders;
```

---

# 68. Important Coding Question — Next Order Amount

```sql
SELECT
    customer_id,
    order_date,
    amount,
    LEAD(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS next_amount
FROM orders;
```

---

# 69. Important Coding Question — Difference from Previous Order

```sql
SELECT
    customer_id,
    order_date,
    amount,
    amount - LAG(amount) OVER (
        PARTITION BY customer_id
        ORDER BY order_date
    ) AS difference
FROM orders;
```

---

# 70. Important Coding Question — Department Average Beside Each Employee

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg
FROM employees;
```

---

# 71. Important Coding Question — Employee Count per Department Without GROUP BY

```sql
SELECT
    name,
    department_id,
    COUNT(*) OVER (
        PARTITION BY department_id
    ) AS employee_count
FROM employees;
```

---

# 72. Important Coding Question — Maximum Salary per Department

```sql
SELECT
    name,
    department_id,
    salary,
    MAX(salary) OVER (
        PARTITION BY department_id
    ) AS max_department_salary
FROM employees;
```

---

# 73. Important Coding Question — Salary Percentage of Department Total

```sql
SELECT
    name,
    department_id,
    salary,
    salary * 100.0
    / SUM(salary) OVER (
        PARTITION BY department_id
    ) AS percentage_of_department_salary
FROM employees;
```

---

# 74. Important Coding Question — Latest Order per Customer

```sql
WITH ranked_orders AS (
    SELECT
        customer_id,
        order_id,
        order_date,
        amount,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC, order_id DESC
        ) AS rn
    FROM orders
)
SELECT
    customer_id,
    order_id,
    order_date,
    amount
FROM ranked_orders
WHERE rn = 1;
```

---

# 75. Important Coding Question — Find Duplicate Emails

```sql
WITH duplicates AS (
    SELECT
        customer_id,
        email,
        ROW_NUMBER() OVER (
            PARTITION BY email
            ORDER BY customer_id
        ) AS rn
    FROM customers
)
SELECT
    customer_id,
    email
FROM duplicates
WHERE rn > 1;
```

---

# 76. Important Coding Question — Three-Month Moving Average

Suppose one row represents one month.

```sql
SELECT
    month,
    sales,
    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS three_month_average
FROM monthly_sales;
```

If the business requirement is based on calendar months rather than simply the previous two rows, make sure the data has one row per month or use an appropriate date-based approach for the database system.

---

# 77. Important Coding Question — Month-over-Month Growth

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales,
    (
        sales - LAG(sales) OVER (
            ORDER BY month
        )
    ) * 100.0
    / NULLIF(
        LAG(sales) OVER (
            ORDER BY month
        ),
        0
    ) AS growth_percentage
FROM monthly_sales;
```

---

# 78. Important Coding Question — First Order for Every Customer

```sql
WITH ranked_orders AS (
    SELECT
        customer_id,
        order_id,
        order_date,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date, order_id
        ) AS rn
    FROM orders
)
SELECT
    customer_id,
    order_id,
    order_date
FROM ranked_orders
WHERE rn = 1;
```

---

# 79. Important Coding Question — Find Employees Above Department Average

```sql
WITH employee_data AS (
    SELECT
        name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees
)
SELECT
    name,
    department_id,
    salary,
    department_avg
FROM employee_data
WHERE salary > department_avg;
```

This is a very good alternative to the correlated-subquery solution.

---

# 80. Window Function vs Subquery

Both can sometimes solve the same problem.

For example, employees above department average can be written using a correlated subquery:

```sql
SELECT
    e.name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

Or using a window function:

```sql
WITH employee_data AS (
    SELECT
        name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_avg
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM employee_data
WHERE salary > department_avg;
```

### Interview Answer

> Window functions are often a clean way to calculate group-level metrics while preserving row-level detail. A subquery may also solve the problem. I choose based on readability, requirements, and the execution plan.

---

# 81. Window Function vs GROUP BY

### GROUP BY

Use when you want:

```text
One result row per group
```

Example:

```sql
SELECT
    department_id,
    AVG(salary)
FROM employees
GROUP BY department_id;
```

### Window Function

Use when you want:

```text
Original rows + group-level calculation
```

Example:

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    )
FROM employees;
```

---

# 82. Important Interview Trap — RANK Does Not Mean Unique Rank

Suppose:

```text
Salary:
100000
90000
90000
80000
```

`RANK()` returns:

```text
1
2
2
4
```

So rank `3` does not exist.

If you need consecutive distinct ranks:

```sql
DENSE_RANK()
```

is appropriate.

---

# 83. Important Interview Trap — ROW_NUMBER and Ties

Consider:

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC
)
```

If two rows have the same salary, SQL can assign them different row numbers.

If the ordering does not uniquely identify rows, which tied row receives which number may not be deterministic.

For deterministic results, add a tie-breaker:

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC, employee_id
)
```

---

# 84. Important Interview Trap — Filtering Window Results

Do not write:

```sql
SELECT
    name,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS rn
FROM employees
WHERE rn <= 3;
```

Instead:

```sql
WITH ranked AS (
    SELECT
        name,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

This pattern is extremely important.

---

# 85. Important Interview Trap — LAG on First Row

Example:

```sql
LAG(sales) OVER (
    ORDER BY order_date
)
```

The first row has no previous row.

Therefore, the result is normally:

```text
NULL
```

You can handle it using:

```sql
COALESCE()
```

if appropriate.

Example:

```sql
COALESCE(
    LAG(sales) OVER (
        ORDER BY order_date
    ),
    0
) AS previous_sales
```

---

# 86. Important Interview Trap — Division by Zero

When calculating percentages:

```sql
current_value * 100.0 / previous_value
```

`previous_value` may be zero.

A safer pattern is:

```sql
current_value * 100.0
/ NULLIF(previous_value, 0)
```

This converts a zero denominator to NULL instead of causing a division-by-zero error.

---

# 87. Important Interview Question — Can Multiple Window Functions Be Used in One Query?

Yes.

Example:

```sql
SELECT
    name,
    department_id,
    salary,

    ROW_NUMBER() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS salary_rank,

    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_avg

FROM employees;
```

Multiple window functions can be used in the same `SELECT`.

---

# 88. Important Interview Question — Can Window Functions Be Nested?

You generally cannot directly nest one window function inside another window function in the same expression.

For example, do not try to write:

```sql
SUM(
    ROW_NUMBER() OVER (...)
) OVER (...)
```

Instead, calculate the first window result in a CTE or derived table and then apply another calculation.

Example:

```sql
WITH ranked AS (
    SELECT
        name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT
    *,
    rn * 10 AS calculated_value
FROM ranked;
```

---

# 89. Important Interview Question — What Is the Difference Between PARTITION BY and GROUP BY?

### GROUP BY

```sql
GROUP BY department_id
```

Combines rows into groups.

### PARTITION BY

```sql
PARTITION BY department_id
```

Creates logical windows but keeps the individual rows.

### Best One-Line Answer

> `GROUP BY` reduces rows; `PARTITION BY` divides rows for window calculations without reducing them.

---

# 90. Interview Scenario — Top 3 Employees

### Question

> Find the top 3 employees by salary.

```sql
SELECT
    name,
    salary
FROM (
    SELECT
        name,
        salary,
        ROW_NUMBER() OVER (
            ORDER BY salary DESC
        ) AS rn
    FROM employees
) AS ranked
WHERE rn <= 3;
```

---

# 91. Interview Scenario — Top 3 Distinct Salaries

If the requirement is three distinct salary levels:

```sql
WITH ranked AS (
    SELECT
        name,
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    salary
FROM ranked
WHERE salary_rank <= 3;
```

This distinction can impress an interviewer because it shows you understand ties.

---

# 92. Interview Scenario — Highest Salary Per Department

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked
WHERE salary_rank = 1;
```

---

# 93. Interview Scenario — Second Highest Salary Per Department

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked
WHERE salary_rank = 2;
```

This returns all employees tied at the second-highest distinct salary in each department.

---

# 94. Interview Scenario — Third Highest Salary Per Department

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        DENSE_RANK() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT
    name,
    department_id,
    salary
FROM ranked
WHERE salary_rank = 3;
```

---

# 95. Interview Scenario — Employee's Rank and Department Average

```sql
SELECT
    name,
    department_id,
    salary,

    DENSE_RANK() OVER (
        PARTITION BY department_id
        ORDER BY salary DESC
    ) AS salary_rank,

    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average

FROM employees;
```

This is an excellent example to explain during an interview.

---

# 96. Interview Scenario — Customer's First and Latest Order

```sql
WITH order_data AS (
    SELECT
        customer_id,
        order_id,
        order_date,

        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date, order_id
        ) AS first_order,

        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC, order_id DESC
        ) AS latest_order

    FROM orders
)
SELECT *
FROM order_data
WHERE first_order = 1
   OR latest_order = 1;
```

---

# 97. Interview Scenario — Detect Increasing Sales

```sql
SELECT
    order_date,
    sales,
    LAG(sales) OVER (
        ORDER BY order_date
    ) AS previous_sales
FROM daily_sales;
```

Then compare:

```sql
sales > previous_sales
```

using an outer query:

```sql
WITH sales_data AS (
    SELECT
        order_date,
        sales,
        LAG(sales) OVER (
            ORDER BY order_date
        ) AS previous_sales
    FROM daily_sales
)
SELECT *
FROM sales_data
WHERE sales > previous_sales;
```

---

# 98. Window Functions — Real Interview Knowledge

If an interviewer asks:

> "Why would you use a window function?"

A strong answer is:

> I use a window function when I need an analytical calculation across related rows while still retaining the row-level details. For example, I can rank employees within each department, calculate a department average beside every employee, or compare each month's sales with the previous month using LAG.

This demonstrates practical understanding instead of just memorizing syntax.

---

# 99. Most Important Window Function Patterns to Memorize

## Pattern 1 — Rank All Rows

```sql
RANK() OVER (
    ORDER BY salary DESC
)
```

## Pattern 2 — Rank Within Groups

```sql
RANK() OVER (
    PARTITION BY department_id
    ORDER BY salary DESC
)
```

## Pattern 3 — Top N Per Group

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

## Pattern 4 — Previous Row

```sql
LAG(value) OVER (
    ORDER BY date_column
)
```

## Pattern 5 — Next Row

```sql
LEAD(value) OVER (
    ORDER BY date_column
)
```

## Pattern 6 — Running Total

```sql
SUM(value) OVER (
    ORDER BY date_column
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

## Pattern 7 — Group Average Beside Each Row

```sql
AVG(value) OVER (
    PARTITION BY group_column
)
```

## Pattern 8 — Conditional Filtering of Window Results

```sql
WITH ranked AS (
    SELECT
        *,
        ROW_NUMBER() OVER (...) AS rn
    FROM table_name
)
SELECT *
FROM ranked
WHERE rn <= 3;
```

---

# 100. High-Priority Interview Questions

You should be able to answer these without hesitation:

1. What is a window function?
2. Why do we use window functions?
3. What does `OVER()` do?
4. What is `PARTITION BY`?
5. Difference between `PARTITION BY` and `GROUP BY`?
6. What is `ROW_NUMBER()`?
7. What is `RANK()`?
8. What is `DENSE_RANK()`?
9. Difference between `ROW_NUMBER`, `RANK`, and `DENSE_RANK`?
10. What is `LAG()`?
11. What is `LEAD()`?
12. Difference between `LAG()` and `LEAD()`?
13. How do you find the second-highest salary using a window function?
14. How do you find the top 3 employees in each department?
15. How do you find the highest-paid employee in each department?
16. How do you calculate a running total?
17. How do you calculate a moving average?
18. How do you compare the current row with the previous row?
19. How do you find the latest record for each customer?
20. How do you find duplicate records using `ROW_NUMBER()`?
21. Can a window function be used directly in `WHERE`?
22. Why do we use a CTE with window functions?
23. What is a window frame?
24. What does `UNBOUNDED PRECEDING` mean?
25. Can aggregate functions be used as window functions?
26. Can multiple window functions be used in one query?
27. How do you calculate a percentage of a group total?
28. How do you rank employees within each department?
29. How do you find employees earning above their department average?
30. How do you perform month-over-month comparison?

---

# 101. Final Revision Sheet

```text
WINDOW FUNCTION
→ Calculation across related rows without collapsing them

OVER()
→ Defines the window

PARTITION BY
→ Divides rows into logical groups

ORDER BY inside OVER()
→ Defines calculation order

ROW_NUMBER()
→ Unique sequential number

RANK()
→ Ties share rank + gaps

DENSE_RANK()
→ Ties share rank + no gaps

LAG()
→ Previous row

LEAD()
→ Next row

SUM() OVER()
→ Running/cumulative totals or windowed sums

AVG() OVER()
→ Windowed averages

COUNT() OVER()
→ Count within a window

MIN()/MAX() OVER()
→ Minimum/maximum within a window

ROWS BETWEEN
→ Defines the window frame

UNBOUNDED PRECEDING
→ Start from beginning of the window

CTE + WINDOW FUNCTION
→ Calculate window result, then filter/process it
```

---

# 102. The Most Important Interview Examples

## Example 1 — Top Employee Per Department

```sql
WITH ranked AS (
    SELECT
        name,
        department_id,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department_id
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked
WHERE rn = 1;
```

## Example 2 — Second Highest Distinct Salary

```sql
WITH ranked AS (
    SELECT
        name,
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT *
FROM ranked
WHERE salary_rank = 2;
```

## Example 3 — Previous Value

```sql
SELECT
    order_date,
    sales,
    LAG(sales) OVER (
        ORDER BY order_date
    ) AS previous_sales
FROM daily_sales;
```

## Example 4 — Running Total

```sql
SELECT
    order_date,
    sales,
    SUM(sales) OVER (
        ORDER BY order_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM daily_sales;
```

## Example 5 — Department Average

```sql
SELECT
    name,
    department_id,
    salary,
    AVG(salary) OVER (
        PARTITION BY department_id
    ) AS department_average
FROM employees;
```

## Example 6 — Above Department Average

```sql
WITH employee_data AS (
    SELECT
        name,
        department_id,
        salary,
        AVG(salary) OVER (
            PARTITION BY department_id
        ) AS department_average
    FROM employees
)
SELECT *
FROM employee_data
WHERE salary > department_average;
```

---

# 103. Final Interview Tip

Do not just memorize:

```text
ROW_NUMBER
RANK
DENSE_RANK
LAG
LEAD
SUM OVER
AVG OVER
```

Understand **when to use each one**.

A strong interview response should connect the function to a real problem:

```text
ROW_NUMBER
→ Latest record / top N rows / deduplication

RANK
→ Ranking where ties should share rank and gaps matter

DENSE_RANK
→ Nth distinct highest/lowest value

LAG
→ Compare with previous row

LEAD
→ Compare with next row

SUM OVER
→ Running total / group total

AVG OVER
→ Group average beside each row

PARTITION BY
→ Perform the same analysis separately for each group
```

If you can confidently solve **top N per group, second/third highest salary, latest record per customer, running total, previous-row comparison, department average, duplicate detection, and above-group-average problems**, you have covered the most important interview-level use cases of SQL window functions.