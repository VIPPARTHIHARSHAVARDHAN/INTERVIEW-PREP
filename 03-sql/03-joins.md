# SQL Joins

## 1. What is a JOIN?

A `JOIN` is used to combine rows from two or more tables based on a related column.

In real-world databases, data is usually divided into multiple tables instead of storing everything in one large table.

For example:

### employees

| employee_id | name | department_id |
|---:|---|---:|
| 1 | Rahul | 10 |
| 2 | Priya | 20 |
| 3 | Arjun | 10 |
| 4 | Sneha | 30 |

### departments

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |
| 30 | Sales |
| 40 | Finance |

The common column is:

```text
employees.department_id
departments.department_id
```

We can use this relationship to combine the tables.

---

# 2. Why Do We Need JOINs?

Suppose employee information is stored in one table and department information is stored in another.

Instead of duplicating:

```text
IT
IT
HR
Sales
```

for every employee, we store the department information separately and connect the tables using `department_id`.

This provides:

- Less data duplication
- Better organization
- Easier maintenance
- Better normalization
- Flexible querying

### Real-World Example

An e-commerce application may have:

```text
customers
orders
products
payments
```

An order may contain a `customer_id`, allowing us to connect an order to its customer.

---

# 3. Basic JOIN Syntax

```sql
SELECT columns
FROM table1
JOIN table2
    ON table1.common_column = table2.common_column;
```

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Result:

| name | department_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| Arjun | IT |
| Sneha | Sales |

---

# 4. Types of JOINs

The most important JOIN types for interviews are:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
CROSS JOIN
SELF JOIN
```

The most frequently used ones in practical SQL are:

```text
INNER JOIN
LEFT JOIN
```

---

# 5. INNER JOIN

`INNER JOIN` returns only rows that have matching values in both tables.

Syntax:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

If every employee has a matching department, all employees appear.

---

# 6. INNER JOIN Example with Unmatched Data

Suppose:

### employees

| employee_id | name | department_id |
|---:|---|---:|
| 1 | Rahul | 10 |
| 2 | Priya | 20 |
| 3 | Arjun | 50 |

### departments

| department_id | department_name |
|---:|---|
| 10 | IT |
| 20 | HR |
| 30 | Sales |

Employee Arjun has:

```text
department_id = 50
```

but department 50 does not exist.

Query:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

Result:

| name | department_name |
|---|---|
| Rahul | IT |
| Priya | HR |

Arjun is excluded because there is no matching department.

---

# 7. LEFT JOIN

`LEFT JOIN` returns:

```text
All rows from the LEFT table
+
Matching rows from the RIGHT table
```

If there is no match, columns from the right table become `NULL`.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

Result:

| name | department_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| Arjun | NULL |

Arjun is included because `employees` is the left table.

---

# 8. Why is LEFT JOIN Important?

A very common interview requirement is:

> Find all customers, including customers who have never placed an order.

For example:

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

Customers without orders will still appear, with:

```text
order_id = NULL
```

This is one of the most important practical uses of `LEFT JOIN`.

---

# 9. RIGHT JOIN

`RIGHT JOIN` returns:

```text
All rows from the RIGHT table
+
Matching rows from the LEFT table
```

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
RIGHT JOIN departments d
    ON e.department_id = d.department_id;
```

If Finance has no employees:

| name | department_name |
|---|---|
| Rahul | IT |
| Priya | HR |
| Sneha | Sales |
| NULL | Finance |

Finance is still included because `departments` is the right table.

### Interview Tip

A `RIGHT JOIN` can usually be rewritten as a `LEFT JOIN` by swapping the table order.

For readability, many developers prefer `LEFT JOIN`.

---

# 10. FULL OUTER JOIN

`FULL OUTER JOIN` returns:

```text
Matching rows
+
Unmatched rows from the left table
+
Unmatched rows from the right table
```

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
FULL OUTER JOIN departments d
    ON e.department_id = d.department_id;
```

If:

```text
Employee has department_id = 50
```

and:

```text
Department has department_id = 40
```

but neither has a matching row, both can still appear.

Conceptually:

```text
LEFT unmatched rows
+
MATCHED rows
+
RIGHT unmatched rows
```

### Important

Not every database system supports `FULL OUTER JOIN` directly.

---

# 11. CROSS JOIN

`CROSS JOIN` produces the Cartesian product of two tables.

If:

```text
Table A = 3 rows
Table B = 4 rows
```

then:

```text
3 × 4 = 12 rows
```

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
CROSS JOIN departments d;
```

Every employee is combined with every department.

### Real-World Example

Cross joins can be useful when generating combinations, such as:

```text
Products × Sizes
Products × Colors
Dates × Store Locations
```

However, an accidental Cartesian product can create a huge result set.

---

# 12. SELF JOIN

A `SELF JOIN` joins a table with itself.

It is useful when rows in the same table are related to each other.

Example employee table:

| employee_id | name | manager_id |
|---:|---|---:|
| 1 | Rahul | NULL |
| 2 | Priya | 1 |
| 3 | Arjun | 1 |
| 4 | Sneha | 2 |

Here:

```text
employee_id
```

identifies an employee, while:

```text
manager_id
```

points to another employee in the same table.

Query:

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Result:

| employee | manager |
|---|---|
| Rahul | NULL |
| Priya | Rahul |
| Arjun | Rahul |
| Sneha | Priya |

This is a classic `SELF JOIN` interview example.

---

# 13. JOIN with Table Aliases

Aliases make JOIN queries shorter and easier to read.

Instead of:

```sql
SELECT
    employees.name,
    departments.department_name
FROM employees
INNER JOIN departments
    ON employees.department_id = departments.department_id;
```

we can write:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

Here:

```text
e → employees
d → departments
```

---

# 14. What is the ON Clause?

The `ON` clause specifies the condition used to match rows between tables.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

The matching condition is:

```sql
e.department_id = d.department_id
```

### Interview Answer

> The ON clause defines the relationship or matching condition between the tables being joined.

---

# 15. JOIN ON Primary Key and Foreign Key

A common relationship is:

```text
departments.department_id
        ↑
        |
employees.department_id
```

Usually:

```text
departments.department_id → Primary Key
employees.department_id    → Foreign Key
```

Then:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

This is a typical relational database design.

---

# 16. INNER JOIN vs LEFT JOIN

This is one of the most frequently asked interview questions.

| INNER JOIN | LEFT JOIN |
|---|---|
| Returns matching rows only | Returns all rows from left table |
| Unmatched left rows are removed | Unmatched left rows remain |
| Unmatched right rows are removed | Unmatched right values become NULL |
| Useful when a match is required | Useful when unmatched left records must also be shown |

### Simple Memory Trick

```text
INNER JOIN
= Only matches

LEFT JOIN
= Everything from left + matches
```

---

# 17. LEFT JOIN vs RIGHT JOIN

```text
LEFT JOIN
→ Keep everything from left table

RIGHT JOIN
→ Keep everything from right table
```

Example:

```sql
FROM employees e
LEFT JOIN departments d
```

means:

```text
Keep all employees
```

Whereas:

```sql
FROM employees e
RIGHT JOIN departments d
```

means:

```text
Keep all departments
```

---

# 18. INNER JOIN vs FULL OUTER JOIN

```text
INNER JOIN
→ Only matching rows

FULL OUTER JOIN
→ Matching + unmatched rows from both sides
```

Conceptually:

```text
INNER:
       MATCH
        ███

FULL:
LEFT + MATCH + RIGHT
████████████████████
```

---

# 19. JOIN with WHERE

You can filter a joined result using `WHERE`.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_name = 'IT';
```

This returns only employees belonging to IT.

---

# 20. JOIN with ORDER BY

Example:

```sql
SELECT
    e.name,
    d.department_name,
    e.salary
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id
ORDER BY e.salary DESC;
```

This joins the tables and then sorts the result by salary.

---

# 21. JOIN with GROUP BY

Example:

> Find the number of employees in each department.

```sql
SELECT
    d.department_name,
    COUNT(*) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;
```

Using `LEFT JOIN` ensures departments with zero employees can also be included.

---

# 22. JOIN with HAVING

Example:

> Find departments having more than 5 employees.

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING COUNT(e.employee_id) > 5;
```

---

# 23. Why COUNT(column) Matters with LEFT JOIN

Consider:

```sql
SELECT
    d.department_name,
    COUNT(*) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_name;
```

For a department with no employees, the LEFT JOIN still produces a row containing NULL values from `employees`.

Therefore, if you want to count actual employees, this is usually safer:

```sql
COUNT(e.employee_id)
```

because:

```text
COUNT(e.employee_id)
```

ignores NULL.

So:

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;
```

can correctly return:

```text
Finance | 0
```

for a department with no employees.

---

# 24. Multiple JOINs

A query can join more than two tables.

Suppose we have:

```text
customers
orders
products
```

Example:

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

This combines information from three tables.

---

# 25. Real-World Example — E-Commerce

Suppose:

### customers

```text
customer_id
name
```

### orders

```text
order_id
customer_id
product_id
```

### products

```text
product_id
product_name
price
```

Question:

> Display customer name, order ID, product name, and price.

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name,
    p.price
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

### Interview Explanation

> I join customers with orders using customer_id and then join orders with products using product_id. This allows me to combine customer, order, and product information in one result.

---

# 26. Real-World Example — Customers Without Orders

Question:

> Find all customers who have never placed an order.

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

### Why This Works

First:

```text
LEFT JOIN
```

keeps every customer.

For customers with no order:

```text
o.customer_id = NULL
```

Then:

```sql
WHERE o.customer_id IS NULL
```

keeps only those customers.

### Interview Answer

> I use a LEFT JOIN to retain all customers and then filter for NULL on the order side to find customers without matching orders.

---

# 27. Real-World Example — Departments Without Employees

Question:

> Find departments that currently have no employees.

```sql
SELECT
    d.department_id,
    d.department_name
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
WHERE e.employee_id IS NULL;
```

This is a very common `LEFT JOIN + IS NULL` pattern.

---

# 28. Real-World Example — Employees with Their Managers

Question:

> Display each employee and their manager.

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

This is a `SELF JOIN`.

---

# 29. JOIN and NULL

Suppose:

```text
employees.department_id = NULL
```

Then:

```sql
e.department_id = d.department_id
```

does not evaluate to TRUE because NULL represents an unknown value.

Therefore, an `INNER JOIN` will not match that employee through this equality condition.

A `LEFT JOIN` can still keep the employee, but the department columns will be NULL.

---

# 30. JOIN Conditions Can Use Multiple Columns

Sometimes a relationship depends on more than one column.

Example:

```sql
SELECT *
FROM table_a a
JOIN table_b b
    ON a.customer_id = b.customer_id
   AND a.order_id = b.order_id;
```

Both conditions must match.

This is common with composite keys.

---

# 31. JOIN with Additional Conditions

You can include additional conditions in the `ON` clause.

Example:

```sql
SELECT
    c.customer_id,
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
   AND o.status = 'Completed';
```

This means the query keeps all customers, but only matches completed orders.

---

# 32. Important Difference — Condition in ON vs WHERE

This is a very important interview concept.

Consider:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
   AND o.status = 'Completed';
```

This keeps all customers and only matches completed orders.

Compare with:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.status = 'Completed';
```

The second query removes rows where `o.status` is NULL, so it can effectively behave like an INNER JOIN for this condition.

### Interview Answer

> With an outer join, placing a condition in ON controls which rows match while preserving unmatched rows from the preserved side. Putting a condition on the nullable side in WHERE can eliminate those unmatched rows and change the effective behavior of the query.

---

# 33. Common JOIN Mistake — Missing ON Condition

Consider:

```sql
SELECT *
FROM employees e
JOIN departments d;
```

Depending on SQL dialect, this may be invalid or may be treated as a Cartesian product if written as a cross-style join.

The intended relationship should normally be explicit:

```sql
SELECT *
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Always identify the relationship between the tables.

---

# 34. Common JOIN Mistake — Wrong Join Column

Suppose:

```text
employees.department_id
departments.department_id
```

The correct relationship is:

```sql
ON e.department_id = d.department_id
```

Joining unrelated columns can produce incorrect results.

### Interview Tip

Before writing a JOIN, ask:

```text
What is the relationship between these tables?
Which column connects them?
Is the relationship one-to-one, one-to-many, or many-to-many?
Which unmatched rows should remain?
```

---

# 35. Duplicate Rows After JOIN

A JOIN can produce multiple rows for one row in the original table.

Example:

One customer:

```text
customer_id = 101
```

has three orders.

Joining customers to orders produces:

```text
101 → Order 1
101 → Order 2
101 → Order 3
```

The customer appears three times.

This is not necessarily an error.

It happens because the relationship is:

```text
One customer
      ↓
Many orders
```

### Interview Explanation

> Duplicate-looking rows after a JOIN often occur because of a one-to-many relationship. The JOIN returns one result row for each matching combination.

---

# 36. One-to-Many JOIN

Example:

```text
Customer
   |
   | 1
   |
   | many
   ↓
Orders
```

Query:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

One customer can appear multiple times because they can have multiple orders.

---

# 37. Many-to-Many JOIN

Many-to-many relationships are usually implemented using a junction/bridge table.

Example:

```text
students
courses
student_courses
```

A student can take many courses.

A course can have many students.

The bridge table:

```text
student_courses
----------------
student_id
course_id
```

connects them.

Query:

```sql
SELECT
    s.student_name,
    c.course_name
FROM students s
JOIN student_courses sc
    ON s.student_id = sc.student_id
JOIN courses c
    ON sc.course_id = c.course_id;
```

---

# 38. JOIN vs UNION

This is a common interview question.

### JOIN

Combines columns from related tables.

```text
Table A + Table B
→ More columns
```

Example:

```sql
SELECT *
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

### UNION

Combines result sets vertically.

```text
Result A
+
Result B
→ More rows
```

Example:

```sql
SELECT name FROM employees
UNION
SELECT name FROM managers;
```

### Easy Memory Trick

```text
JOIN
→ Combine tables horizontally

UNION
→ Combine result sets vertically
```

---

# 39. JOIN vs Subquery

Both JOINs and subqueries can solve some of the same problems.

Example:

Using JOIN:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

A subquery can sometimes achieve similar results, but JOINs are generally the natural choice when you need columns from related tables.

### Interview Tip

Do not claim that JOINs are always faster than subqueries or vice versa. Performance depends on the database optimizer, query structure, indexes, data distribution, and other factors.

---

# 40. Important Interview Question — What is INNER JOIN?

### Answer

> INNER JOIN returns only rows where the join condition matches in both tables.

Example:

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 41. Important Interview Question — What is LEFT JOIN?

### Answer

> LEFT JOIN returns all rows from the left table and the matching rows from the right table. If there is no match, the right-side columns contain NULL.

Example:

```sql
SELECT
    c.name,
    o.order_id
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id;
```

---

# 42. Important Interview Question — What is RIGHT JOIN?

### Answer

> RIGHT JOIN returns all rows from the right table and matching rows from the left table. Unmatched left-side columns become NULL.

---

# 43. Important Interview Question — What is FULL OUTER JOIN?

### Answer

> FULL OUTER JOIN returns matching rows plus unmatched rows from both tables, with NULLs used for the missing side.

---

# 44. Important Interview Question — What is CROSS JOIN?

### Answer

> CROSS JOIN returns the Cartesian product of two tables, meaning every row from the first table is combined with every row from the second table.

If:

```text
Table A = 5 rows
Table B = 4 rows
```

then:

```text
5 × 4 = 20 rows
```

---

# 45. Important Interview Question — What is SELF JOIN?

### Answer

> A SELF JOIN is when a table is joined with itself. It is useful when rows in the same table have relationships with other rows in that table, such as employees and their managers.

Example:

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

# 46. Important Interview Question — INNER JOIN vs LEFT JOIN?

### Strong Interview Answer

> INNER JOIN returns only records that have a match in both tables. LEFT JOIN preserves every record from the left table and adds matching records from the right table; when no match exists, the right-side columns become NULL. I use LEFT JOIN when I need to retain records even when related data is missing.

---

# 47. Important Interview Question — How Do You Find Records Without a Match?

A common pattern is:

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;
```

This finds customers without orders.

### General Pattern

```sql
SELECT ...
FROM A
LEFT JOIN B
    ON A.key = B.key
WHERE B.key IS NULL;
```

This is commonly known as an **anti-join pattern**.

---

# 48. Important Interview Question — Can We JOIN More Than Two Tables?

Yes.

Example:

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

A query can join multiple tables as long as the relationships are correctly defined.

---

# 49. Important Interview Question — What Happens When a Row Matches Multiple Rows?

Suppose one customer has three orders.

A customer-to-order JOIN produces three result rows for that customer.

This happens because JOINs return matching combinations.

### Interview Answer

> If one row from one table matches multiple rows from another table, the result contains one row for each matching combination. This is expected behavior in a one-to-many relationship.

---

# 50. Important Interview Question — Why Do JOINs Sometimes Create Duplicate Rows?

### Answer

> JOINs can create multiple rows when the relationship is one-to-many or many-to-many. What looks like a duplicate may actually represent different matching records from the related table.

Before using `DISTINCT`, determine whether the extra rows are actually incorrect.

---

# 51. Important Interview Question — What is a Cartesian Product?

A Cartesian product contains every possible combination of rows from two tables.

If:

```text
A = 10 rows
B = 5 rows
```

then:

```text
10 × 5 = 50 rows
```

A `CROSS JOIN` intentionally produces this.

An unintended Cartesian product can occur when a join relationship is missing or incorrect.

---

# 52. Important Coding Question — Display Employee and Department

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
INNER JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 53. Important Coding Question — Display All Employees Including Those Without Departments

```sql
SELECT
    e.name,
    d.department_name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id;
```

---

# 54. Important Coding Question — Find Employees Without a Valid Department

```sql
SELECT
    e.employee_id,
    e.name
FROM employees e
LEFT JOIN departments d
    ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
```

---

# 55. Important Coding Question — Find Departments Without Employees

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

# 56. Important Coding Question — Count Employees Per Department

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name;
```

---

# 57. Important Coding Question — Find Departments with More Than 5 Employees

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
    ON d.department_id = e.department_id
GROUP BY d.department_id, d.department_name
HAVING COUNT(e.employee_id) > 5;
```

---

# 58. Important Coding Question — Display Employees and Managers

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

---

# 59. Important Coding Question — Join Three Tables

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

---

# 60. Important Coding Question — Find Customers Who Have Placed No Orders

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

---

# 61. Important Coding Question — Find Customers With At Least One Order

```sql
SELECT DISTINCT
    c.customer_id,
    c.name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

If the goal is simply to test existence rather than return order rows, `EXISTS` can also be a good solution:

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

---

# 62. Important Coding Question — Find Total Order Amount Per Customer

Suppose:

```text
orders
----------------------------
order_id
customer_id
amount
```

Query:

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name;
```

To include customers who have no orders:

```sql
SELECT
    c.customer_id,
    c.name,
    COALESCE(SUM(o.amount), 0) AS total_spent
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name;
```

---

# 63. Important Coding Question — Find Customers Who Spent More Than 10,000

```sql
SELECT
    c.customer_id,
    c.name,
    SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
HAVING SUM(o.amount) > 10000;
```

This combines:

```text
JOIN
GROUP BY
SUM()
HAVING
```

---

# 64. Important Coding Question — Find Highest Salary Employee in Each Department

One simple approach uses aggregation:

```sql
SELECT
    department_id,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department_id;
```

If you need the employee's name too, aggregation alone is not enough in general. A common solution is to use a window function or a subquery.

Using a subquery:

```sql
SELECT
    e.name,
    e.department_id,
    e.salary
FROM employees e
WHERE e.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

This can return multiple employees if there is a tie.

---

# 65. JOIN Order and Query Understanding

Consider:

```sql
SELECT
    c.name,
    o.order_id,
    p.product_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

Understand it conceptually as:

```text
customers
    ↓
match orders using customer_id
    ↓
match products using product_id
    ↓
final result
```

When debugging a complex JOIN, examine each relationship separately.

---

# 66. Practical JOIN Debugging Method

When a JOIN returns unexpected results:

### Step 1

Check the relationship:

```sql
ON A.id = B.id
```

Is this really the correct relationship?

### Step 2

Check the cardinality:

```text
1-to-1?
1-to-many?
many-to-many?
```

### Step 3

Check for NULLs.

### Step 4

Check whether the JOIN should be:

```text
INNER
LEFT
RIGHT
FULL
```

### Step 5

Check whether `WHERE` conditions are removing rows from an outer join.

### Step 6

Check whether duplicate-looking rows are actually valid matches.

---

# 67. JOIN Cheat Sheet

```text
INNER JOIN
→ Matching rows from both tables

LEFT JOIN
→ All left rows + matching right rows

RIGHT JOIN
→ All right rows + matching left rows

FULL OUTER JOIN
→ All matching and unmatched rows from both sides

CROSS JOIN
→ Every combination of rows

SELF JOIN
→ Table joined with itself
```

---

# 68. JOIN Visual Summary

Conceptually:

```text
INNER JOIN

A        B
████████
   ███
   ███
```

Only the matching portion is returned.

```text
LEFT JOIN

A        B
████████
████
```

Everything from A is preserved.

```text
RIGHT JOIN

A        B
████████
     ████
```

Everything from B is preserved.

```text
FULL OUTER JOIN

A        B
████████████
████████████
```

Everything from both sides is preserved.

---

# 69. Most Important JOIN Patterns

## Pattern 1 — Matching Records

```sql
SELECT ...
FROM A
INNER JOIN B
    ON A.id = B.id;
```

Use when:

```text
Only matching records are required.
```

---

## Pattern 2 — Keep All Records from A

```sql
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id;
```

Use when:

```text
Every A record must appear.
```

---

## Pattern 3 — Find Records Without a Match

```sql
SELECT ...
FROM A
LEFT JOIN B
    ON A.id = B.id
WHERE B.id IS NULL;
```

Use when:

```text
Find A records that have no corresponding B record.
```

---

## Pattern 4 — Aggregate Joined Data

```sql
SELECT
    A.category,
    COUNT(B.id)
FROM A
LEFT JOIN B
    ON A.id = B.a_id
GROUP BY A.category;
```

Use when:

```text
You need counts/sums/averages of related records.
```

---

## Pattern 5 — Self Join

```sql
SELECT
    e.name,
    m.name
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.employee_id;
```

Use when:

```text
Rows in the same table are related to each other.
```

---

# 70. Interview Questions You Should Be Able to Solve

Before moving to the next SQL topic, make sure you can answer these:

- What is a JOIN?
- Why do we need JOINs?
- What is INNER JOIN?
- What is LEFT JOIN?
- What is RIGHT JOIN?
- What is FULL OUTER JOIN?
- What is CROSS JOIN?
- What is SELF JOIN?
- INNER JOIN vs LEFT JOIN?
- LEFT JOIN vs RIGHT JOIN?
- INNER JOIN vs FULL OUTER JOIN?
- What is a Cartesian product?
- What is the purpose of the ON clause?
- Can we join more than two tables?
- What happens when one row matches multiple rows?
- Why can JOINs create duplicate-looking rows?
- What is a one-to-many relationship?
- What is a many-to-many relationship?
- How do you find records with no matching record?
- How do you find customers without orders?
- How do you find departments without employees?
- How do you join a table with itself?
- How do you count records after a JOIN?
- Why is COUNT(column) useful with LEFT JOIN?
- What is the difference between a condition in ON and WHERE for an outer join?
- What is JOIN vs UNION?
- JOIN vs subquery?
- How do you join three or more tables?
- How do you aggregate data after a JOIN?
- How do you debug unexpected duplicate rows after a JOIN?

---

# 71. Final Interview Summary

The most important thing is not memorizing JOIN syntax. Understand **which records you want to preserve**.

```text
Need only matching records?
        ↓
INNER JOIN

Need every record from the first table?
        ↓
LEFT JOIN

Need every record from the second table?
        ↓
RIGHT JOIN

Need everything from both tables?
        ↓
FULL OUTER JOIN

Need every possible combination?
        ↓
CROSS JOIN

Need to compare rows within the same table?
        ↓
SELF JOIN

Need records with no match?
        ↓
LEFT JOIN + IS NULL
```

### Strong Interview Mindset

When given a JOIN problem, think in this order:

```text
1. What tables contain the required information?
        ↓
2. What column relates the tables?
        ↓
3. What type of relationship exists?
        ↓
4. Which table's rows must always be preserved?
        ↓
5. INNER / LEFT / RIGHT / FULL?
        ↓
6. Do I need WHERE?
        ↓
7. Do I need GROUP BY?
        ↓
8. Do I need HAVING?
        ↓
9. Could the relationship create multiple matching rows?
        ↓
10. Do I need DISTINCT, aggregation, EXISTS, or another technique?
```

If you can confidently reason through these ten steps, you can handle a large portion of the JOIN questions asked in SQL interviews.