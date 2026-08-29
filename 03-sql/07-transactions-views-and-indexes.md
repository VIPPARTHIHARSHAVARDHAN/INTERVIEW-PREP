# SQL Transactions, Views and Indexes

## 1. Why This Topic Is Important

Transactions, views, and indexes are important SQL interview topics because they test whether you understand:

- How databases safely modify data
- How multiple SQL statements behave as one unit
- How databases maintain consistency
- How to undo or permanently save changes
- How reusable queries can be represented as views
- How indexes improve query performance
- When indexes should and should not be used

For interviews, focus especially on:

```text
Transactions
COMMIT
ROLLBACK
SAVEPOINT
ACID
Isolation Levels
Dirty Read
Non-Repeatable Read
Phantom Read
Views
Indexes
Clustered vs Non-Clustered Index
Composite Index
Unique Index
Index Advantages
Index Disadvantages
When to Create an Index
```

---

# 2. What Is a Transaction?

A **transaction** is a sequence of one or more SQL operations treated as a single logical unit of work.

A transaction should either:

```text
Complete successfully
        OR
Fail and be rolled back
```

Example:

Suppose ₹5,000 is transferred from Account A to Account B.

The transaction involves:

```text
1. Deduct ₹5,000 from Account A
2. Add ₹5,000 to Account B
```

Both operations should succeed together.

If the first succeeds but the second fails, the first operation should be undone.

---

# 3. Real-World Example of a Transaction

Consider a bank transfer:

```text
Account A = ₹20,000
Account B = ₹10,000
```

Transfer:

```text
₹5,000 from A to B
```

Expected result:

```text
Account A = ₹15,000
Account B = ₹15,000
```

We don't want:

```text
Account A = ₹15,000
Account B = ₹10,000
```

because ₹5,000 disappeared.

A transaction helps ensure that the transfer behaves as one logical operation.

---

# 4. Basic Transaction Syntax

A common SQL transaction looks like:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 5000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 5000
WHERE account_id = 2;

COMMIT;
```

If something goes wrong:

```sql
ROLLBACK;
```

The exact transaction-start syntax can vary by database system.

---

# 5. COMMIT

`COMMIT` permanently saves the changes made by the current transaction.

Example:

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 5000
WHERE employee_id = 101;

COMMIT;
```

After the transaction is committed, the changes are finalized according to the database's transaction semantics.

---

# 6. ROLLBACK

`ROLLBACK` undoes changes made in the current transaction that have not already been committed.

Example:

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 5000
WHERE employee_id = 101;

ROLLBACK;
```

The salary update is undone.

---

# 7. COMMIT vs ROLLBACK

| COMMIT | ROLLBACK |
|---|---|
| Saves transaction changes | Undoes uncommitted transaction changes |
| Makes the transaction complete | Returns changes to the transaction's earlier state |
| Used when operation succeeds | Used when operation fails or should be cancelled |

Easy memory:

```text
COMMIT
→ Keep changes

ROLLBACK
→ Undo changes
```

---

# 8. SAVEPOINT

A `SAVEPOINT` creates a point inside a transaction to which you can partially roll back.

Example:

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 1000
WHERE employee_id = 101;

SAVEPOINT salary_update;

UPDATE employees
SET salary = salary + 2000
WHERE employee_id = 102;

ROLLBACK TO salary_update;

COMMIT;
```

The second update can be rolled back while keeping the first update.

---

# 9. Why Use SAVEPOINT?

A savepoint is useful when a transaction contains multiple operations and you want to undo only part of the work.

Example:

```text
Operation 1
    ↓
SAVEPOINT
    ↓
Operation 2
    ↓
Operation 3
    ↓
ROLLBACK TO SAVEPOINT
```

Operations after the savepoint can be undone without necessarily cancelling the entire transaction.

Exact syntax can vary between database systems.

---

# 10. What Is ACID?

ACID describes four important properties of reliable database transactions:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

These are among the **most frequently asked transaction interview concepts**.

---

# 11. Atomicity

Atomicity means a transaction is treated as one indivisible unit.

Either:

```text
All required operations succeed
```

or:

```text
The transaction is rolled back
```

Example:

```text
Transfer money
    ↓
Debit A
    ↓
Credit B
```

If crediting B fails, the debit from A should not remain as a partial transaction result.

---

# 12. Consistency

Consistency means a transaction should move the database from one valid state to another valid state while respecting defined rules and constraints.

Example:

If a database has a constraint:

```text
balance >= 0
```

a transaction should not leave the database violating that rule.

---

# 13. Isolation

Isolation means concurrent transactions should be controlled so that one transaction does not improperly interfere with another.

Example:

Two users attempt to modify the same account at nearly the same time.

The database's isolation mechanisms help control what each transaction can see and how concurrent changes interact.

---

# 14. Durability

Durability means that once a transaction has been successfully committed, its changes are intended to survive subsequent failures such as a system crash, subject to the database system's recovery mechanisms.

Example:

```text
Transaction
    ↓
COMMIT
    ↓
System crashes
    ↓
Committed data should remain
```

---

# 15. ACID — Interview Answer

If the interviewer asks:

> What is ACID?

A strong answer is:

> ACID represents Atomicity, Consistency, Isolation, and Durability. Atomicity ensures a transaction is completed as a unit, Consistency keeps the database in a valid state, Isolation controls interference between concurrent transactions, and Durability ensures committed changes survive failures.

---

# 16. Transaction Isolation Levels

Isolation levels control how one transaction can observe changes made by other concurrent transactions.

Common SQL isolation levels are:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Some database systems also support:

```text
SNAPSHOT
```

or MVCC-based implementations with database-specific behavior.

---

# 17. READ UNCOMMITTED

`READ UNCOMMITTED` allows a transaction to read data that another transaction has modified but not committed.

This can allow:

```text
Dirty Reads
```

It provides the least isolation among the standard isolation levels.

---

# 18. READ COMMITTED

`READ COMMITTED` prevents a transaction from reading data that another transaction has not committed.

However, the same query executed twice within a transaction may return different committed values if another transaction commits an update between the two reads.

This allows:

```text
Non-Repeatable Reads
```

in systems implementing the isolation level according to the standard behavior.

---

# 19. REPEATABLE READ

`REPEATABLE READ` provides stronger consistency for repeated reads within a transaction.

A row read by a transaction generally remains protected from certain concurrent changes for the duration of the transaction, depending on the DBMS implementation.

The exact behavior for phantom rows can vary by database system.

---

# 20. SERIALIZABLE

`SERIALIZABLE` is the strongest standard SQL isolation level.

It aims to make concurrent transactions behave as though they were executed serially.

It provides the strongest isolation but can reduce concurrency and increase locking or other synchronization overhead.

---

# 21. Isolation Level Summary

| Isolation Level | General Strength | Typical Concern |
|---|---|---|
| READ UNCOMMITTED | Lowest | Dirty reads |
| READ COMMITTED | Low/Medium | Non-repeatable reads |
| REPEATABLE READ | Medium/High | Phantom behavior depends on DBMS |
| SERIALIZABLE | Highest | Lower concurrency |

The exact implementation and locking/MVCC behavior depends on the database system.

---

# 22. Dirty Read

A **dirty read** occurs when one transaction reads data written by another transaction before that second transaction commits.

Example:

```text
Transaction A:
UPDATE balance = 5000

Transaction B:
READ balance = 5000

Transaction A:
ROLLBACK
```

Transaction B read a value that was never permanently committed.

That is a dirty read.

---

# 23. Non-Repeatable Read

A non-repeatable read occurs when the same transaction reads the same row twice and gets different committed values because another transaction modified and committed that row between the reads.

Example:

```text
Transaction A:
SELECT salary
→ 50000

Transaction B:
UPDATE salary = 60000
COMMIT

Transaction A:
SELECT salary
→ 60000
```

The same row returned different values within Transaction A.

---

# 24. Phantom Read

A phantom read occurs when a transaction repeats a range query and finds additional or missing rows because another transaction inserted or deleted matching rows and committed.

Example:

First query:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Returns:

```text
5 rows
```

Another transaction inserts a new employee with:

```text
salary = 60000
```

Then the first transaction executes the same query again and may see:

```text
6 rows
```

The newly appearing row is a phantom row.

---

# 25. Dirty Read vs Non-Repeatable Read vs Phantom Read

| Problem | What Changes? |
|---|---|
| Dirty Read | Uncommitted value is read |
| Non-Repeatable Read | Same existing row changes between reads |
| Phantom Read | Set of matching rows changes |

Easy memory:

```text
Dirty
→ Read uncommitted data

Non-repeatable
→ Same row gives different value

Phantom
→ New/missing matching rows appear
```

---

# 26. What Is a View?

A **view** is a database object that represents the result of a stored query.

Example:

```sql
CREATE VIEW employee_details AS
SELECT
    employee_id,
    employee_name,
    department_id
FROM employees;
```

Then:

```sql
SELECT *
FROM employee_details;
```

A view can provide a reusable logical representation of data.

---

# 27. Why Use Views?

Views can be useful for:

- Simplifying complex queries
- Reusing commonly needed query logic
- Restricting access to certain columns or rows
- Providing a stable logical interface over underlying tables
- Hiding unnecessary implementation details from users

---

# 28. View Example

Suppose the table is:

```text
employees
--------------------------------
employee_id
employee_name
salary
department_id
```

We want users to see only:

```text
employee_id
employee_name
department_id
```

Create:

```sql
CREATE VIEW public_employee_info AS
SELECT
    employee_id,
    employee_name,
    department_id
FROM employees;
```

Users can query:

```sql
SELECT *
FROM public_employee_info;
```

without directly writing the underlying query every time.

---

# 29. View vs Table

| View | Table |
|---|---|
| Represents a query result | Stores table data |
| Usually stores the query definition rather than a separate copy of the data | Stores rows physically/logically according to the DBMS |
| Can simplify access | Main storage structure |
| Often reflects current underlying data | Contains its own stored rows |
| Useful for abstraction and access control | Used to persist application data |

A normal view is generally not a separate stored copy of the underlying data.

---

# 30. Does a View Store Data?

A normal view generally stores the **query definition**, not an independent copy of the underlying table data.

When you query the view, the database uses the view definition to obtain the result.

However, some database systems provide **materialized views**, which can store the result physically and refresh it according to database-specific rules.

---

# 31. View vs Materialized View

### Normal View

```text
Stores query definition
        ↓
Reads underlying data
```

### Materialized View

```text
Stores query result
        ↓
Needs refresh/update mechanism
```

Materialized views are database-system-specific and are commonly used when precomputed results can improve read performance.

---

# 32. Creating a View

```sql
CREATE VIEW high_salary_employees AS
SELECT
    employee_id,
    employee_name,
    salary
FROM employees
WHERE salary > 100000;
```

Use it:

```sql
SELECT *
FROM high_salary_employees;
```

---

# 33. Updating a View

Some views are updatable, while others are not.

For example, a simple view based on one table may be updatable in many DBMSs:

```sql
CREATE VIEW employee_names AS
SELECT
    employee_id,
    employee_name
FROM employees;
```

But a view containing operations such as:

```text
GROUP BY
Aggregate functions
DISTINCT
UNION
Certain joins/subqueries
```

may not be directly updatable, depending on the DBMS.

---

# 34. Dropping a View

```sql
DROP VIEW employee_details;
```

This removes the view definition.

It does not normally delete the underlying table data.

---

# 35. What Is an Index?

An **index** is a database data structure that helps the DBMS find rows more efficiently for suitable queries.

Think of a book.

Without an index:

```text
Check every page
        ↓
Find the topic
```

With an index:

```text
Look at index
        ↓
Find location
        ↓
Go directly to relevant pages
```

A database index serves a similar purpose for data retrieval.

---

# 36. Why Do We Use Indexes?

Indexes can improve performance for queries involving columns frequently used in:

```text
WHERE
JOIN
ORDER BY
GROUP BY
```

depending on the query and database optimizer.

Example:

```sql
SELECT *
FROM employees
WHERE email = 'rahul@example.com';
```

If `email` is indexed, the database may be able to locate the matching row more efficiently.

---

# 37. Creating an Index

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

Now the database has an index on:

```text
email
```

---

# 38. Creating a Unique Index

```sql
CREATE UNIQUE INDEX idx_unique_email
ON employees(email);
```

This both:

```text
Supports indexed access
+
Enforces uniqueness
```

The exact relationship between a `UNIQUE` constraint and the physical index used to enforce it depends on the database system.

---

# 39. Dropping an Index

Syntax varies somewhat by database system.

A common form is:

```sql
DROP INDEX idx_employee_email;
```

Always check the syntax for the specific DBMS you are using.

---

# 40. What Happens Without an Index?

Suppose we have:

```text
1 million employees
```

and query:

```sql
SELECT *
FROM employees
WHERE email = 'rahul@example.com';
```

Without a suitable index, the optimizer may need to scan many rows.

This can be expensive for large tables.

With an appropriate index, the database may locate the matching row much more efficiently.

The optimizer ultimately decides whether using the index is beneficial.

---

# 41. Does an Index Always Make a Query Faster?

No.

The database optimizer decides whether an index is useful.

An index may provide little benefit when:

- The table is very small
- The query returns a large percentage of the table
- The indexed column has very low selectivity
- The query cannot effectively use the index
- The index is poorly designed for the query

So:

> More indexes do not automatically mean better performance.

---

# 42. Disadvantages of Indexes

Indexes improve some reads but have costs.

### 1. Extra Storage

Indexes require additional storage.

### 2. Slower Writes

When data changes, related indexes may also need maintenance.

Therefore:

```text
INSERT
UPDATE
DELETE
```

can become more expensive when many indexes exist.

### 3. Maintenance Cost

Indexes need to be maintained as data changes.

Therefore, indexes should be created based on actual workload and query patterns.

---

# 43. When Should You Create an Index?

Consider indexing columns frequently used in selective queries involving:

```text
WHERE
JOIN
ORDER BY
GROUP BY
```

especially when:

```text
Table is large
+
Query runs frequently
+
Index can significantly reduce rows examined
```

Example:

```sql
SELECT *
FROM orders
WHERE customer_id = 1001;
```

If this query is frequent and `orders` is large, an index on `customer_id` may be useful.

---

# 44. When Should You Avoid an Index?

Be careful about indexing:

```text
Every column
```

without analyzing workload.

Potentially poor candidates include columns that:

- Are rarely queried
- Have low selectivity for the workload
- Are on tiny tables
- Are heavily modified and provide little read benefit

The best indexing strategy depends on the database and actual query workload.

---

# 45. Selectivity

**Selectivity** describes how effectively a condition narrows down the number of rows.

Suppose:

```text
1,000,000 rows
```

A column has:

```text
gender
```

with only:

```text
Male
Female
```

The column has low cardinality.

An index on it may not provide much benefit for many queries.

But:

```text
email
```

may have nearly unique values.

An index on email can be highly useful for equality searches.

---

# 46. Cardinality

Cardinality refers to the number of distinct values in a column or, in broader database contexts, the nature of relationships between sets of entities.

For indexing, higher distinct-value counts often make a column more selective for equality lookups.

Example:

```text
gender
→ 2 distinct values

country
→ Hundreds of values

email
→ Potentially millions of distinct values
```

This is one factor the optimizer considers when choosing an execution plan.

---

# 47. Clustered Index

A **clustered index** determines how table rows are physically/logically organized according to the database engine's storage architecture.

The exact implementation differs by DBMS.

A common conceptual model is:

```text
Clustered index
        ↓
Data rows organized around index key
```

Some databases have a specific clustered-index concept, while others organize tables differently.

---

# 48. Non-Clustered Index

A **non-clustered index** is a separate index structure containing indexed key values and references to the corresponding table rows or storage locations.

Conceptually:

```text
Index
  ↓
Indexed value
  ↓
Row location/reference
```

The exact storage and lookup behavior depends on the database engine.

---

# 49. Clustered vs Non-Clustered Index

A safe interview-level comparison is:

| Clustered Index | Non-Clustered Index |
|---|---|
| Determines/closely controls table row organization in DBMSs that support clustered indexes | Separate structure from the main row organization |
| Data access follows the clustered key organization | Index points/references to rows |
| Typically one clustered organization per table | Multiple non-clustered indexes can usually exist |
| Exact behavior is DBMS-specific | Exact behavior is DBMS-specific |

### Important

Do not blindly say:

> "A clustered index physically stores the entire table in sorted order."

That is an oversimplification and can be incorrect depending on the database engine.

---

# 50. Composite Index

A composite index is an index created on multiple columns.

Example:

```sql
CREATE INDEX idx_employee_dept_salary
ON employees(department_id, salary);
```

This index contains:

```text
department_id
salary
```

---

# 51. Why Is Column Order Important in a Composite Index?

Suppose:

```sql
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

The index is ordered according to:

```text
department_id
→ salary
```

Queries filtering by the leading column can generally use the index more effectively.

For example:

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

is a natural match.

A query only on:

```sql
WHERE salary > 50000
```

may not benefit in the same way, depending on the optimizer and DBMS.

This is commonly described as the **leftmost/leading-column principle**, although exact optimizer behavior is database-specific.

---

# 52. Composite Index Example

Suppose we frequently run:

```sql
SELECT *
FROM employees
WHERE department_id = 10
  AND salary > 50000;
```

An index such as:

```sql
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

may be useful.

The index order matches the filtering pattern:

```text
department_id
        ↓
salary
```

---

# 53. Index on WHERE Clause

Example query:

```sql
SELECT *
FROM employees
WHERE employee_id = 101;
```

Since `employee_id` is usually a primary key, the DBMS commonly maintains an appropriate access structure for it.

For another frequently searched column:

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

Then:

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

may benefit.

---

# 54. Index and JOIN

Suppose:

```sql
SELECT e.employee_name, d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Indexes on relevant join columns can improve join performance depending on:

```text
Table size
Data distribution
Query plan
Join type
DBMS optimizer
```

This is why foreign-key columns are often candidates for indexing, especially when they are frequently used in joins.

---

# 55. Index and ORDER BY

Suppose:

```sql
SELECT *
FROM employees
ORDER BY employee_name;
```

An index on:

```sql
employee_name
```

may help the database avoid or reduce sorting work in some cases.

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(employee_name);
```

Whether the index is used depends on the optimizer and the complete query.

---

# 56. Index and GROUP BY

Example:

```sql
SELECT department_id, COUNT(*)
FROM employees
GROUP BY department_id;
```

An index on:

```sql
department_id
```

may sometimes help, depending on the DBMS, data distribution, execution plan, and other factors.

Indexes are not guaranteed to improve every `GROUP BY`.

---

# 57. Index and Primary Key

When you define:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY
);
```

the database generally creates or uses an index-like structure to enforce the primary-key uniqueness and support efficient access.

The exact physical implementation is database-specific.

---

# 58. Index and UNIQUE Constraint

When you define:

```sql
email VARCHAR(100) UNIQUE
```

the database commonly creates or uses an appropriate unique index to enforce uniqueness.

However, the exact implementation is database-specific.

Therefore, in interviews, say:

> A UNIQUE constraint is logically a constraint; the DBMS may use a unique index internally to enforce it.

---

# 59. View and Security

Views can help restrict what users see.

Suppose the employees table contains:

```text
employee_id
employee_name
salary
bank_account
```

We don't want a reporting user to see:

```text
salary
bank_account
```

We can create:

```sql
CREATE VIEW employee_public_info AS
SELECT
    employee_id,
    employee_name
FROM employees;
```

Users can be granted access to the view rather than the underlying table, depending on the DBMS's privilege model.

---

# 60. View for Complex Query

Suppose we frequently need:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Create:

```sql
CREATE VIEW employee_department_details AS
SELECT
    e.employee_id,
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Then:

```sql
SELECT *
FROM employee_department_details;
```

This makes repeated access simpler.

---

# 61. Transactions + Constraints

Transactions and constraints work together.

Example:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 5000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 5000
WHERE account_id = 2;

COMMIT;
```

If a constraint or another database error prevents the transaction from completing, the application can roll back the transaction rather than leaving a partial result.

---

# 62. Real-World Example — E-Commerce Order

Imagine an online shopping application.

A checkout operation may involve:

```text
1. Create order
2. Add order items
3. Reduce inventory
4. Record payment information
5. Finalize order
```

These operations may need transactional coordination so that failures do not leave inconsistent application state.

For example, if inventory is reduced but the order cannot be created successfully, the application may need to roll back the relevant database changes.

---

# 63. Real-World Example — Banking

A bank transfer is a classic transaction example:

```text
BEGIN
    Debit Account A
    Credit Account B
COMMIT
```

If the operation fails:

```text
ROLLBACK
```

The goal is to prevent a partial transfer.

---

# 64. Real-World Example — Index

Consider an e-commerce database with:

```text
10 million orders
```

Users frequently search:

```sql
SELECT *
FROM orders
WHERE customer_id = 10001;
```

An index on:

```sql
customer_id
```

may significantly reduce the amount of data the database needs to inspect.

---

# 65. Real-World Example — View

A company may have:

```text
employees
```

containing confidential salary information.

The reporting team may only need:

```text
employee_id
employee_name
department
```

A view can expose only the required columns:

```sql
CREATE VIEW employee_report AS
SELECT
    employee_id,
    employee_name,
    department_id
FROM employees;
```

This provides a simpler logical interface and can support access-control designs.

---

# 66. Important Interview Question — What Is a Transaction?

### Strong Answer

> A transaction is a logical unit of database work containing one or more operations. The operations are treated together so that the database can commit the successful work or roll it back when appropriate.

---

# 67. Important Interview Question — What Is COMMIT?

### Strong Answer

> COMMIT successfully ends the current transaction and makes its changes permanent according to the database's transaction semantics.

---

# 68. Important Interview Question — What Is ROLLBACK?

### Strong Answer

> ROLLBACK cancels the current transaction and undoes its uncommitted changes.

---

# 69. Important Interview Question — What Is SAVEPOINT?

### Strong Answer

> A savepoint creates an intermediate point within a transaction so that the transaction can roll back to that point without necessarily undoing all previous work in the transaction.

---

# 70. Important Interview Question — Explain ACID

### Strong Answer

> ACID stands for Atomicity, Consistency, Isolation, and Durability. Atomicity treats a transaction as a unit, Consistency maintains valid database states, Isolation controls interference between concurrent transactions, and Durability ensures committed changes survive failures.

---

# 71. Important Interview Question — What Is Atomicity?

### Strong Answer

> Atomicity means a transaction's operations are treated as one logical unit. The transaction should either complete successfully as required or have its uncommitted changes rolled back.

---

# 72. Important Interview Question — What Is Consistency?

### Strong Answer

> Consistency means a successful transaction preserves the database's defined integrity rules and moves it from one valid state to another valid state.

---

# 73. Important Interview Question — What Is Isolation?

### Strong Answer

> Isolation controls how concurrent transactions interact and what changes made by one transaction can be observed by another.

---

# 74. Important Interview Question — What Is Durability?

### Strong Answer

> Durability means that after a transaction is successfully committed, its changes are intended to survive system failures through the database's recovery and storage mechanisms.

---

# 75. Important Interview Question — What Is a Dirty Read?

### Strong Answer

> A dirty read occurs when one transaction reads data written by another transaction before that transaction has committed.

---

# 76. Important Interview Question — What Is a Non-Repeatable Read?

### Strong Answer

> A non-repeatable read occurs when a transaction reads the same existing row more than once and gets different committed values because another transaction modified and committed that row between the reads.

---

# 77. Important Interview Question — What Is a Phantom Read?

### Strong Answer

> A phantom read occurs when repeating a range query within a transaction produces a different set of matching rows because another transaction inserted or deleted matching rows and committed.

---

# 78. Important Interview Question — What Is a View?

### Strong Answer

> A view is a database object based on a stored query. It provides a reusable logical representation of data and can simplify complex queries or restrict access to selected rows and columns.

---

# 79. Important Interview Question — Does a View Store Data?

### Strong Answer

> A normal view generally stores the query definition rather than a separate copy of the underlying data. Materialized views are different because they can store precomputed results, depending on the database system.

---

# 80. Important Interview Question — Why Do We Use Views?

### Strong Answer

> Views can simplify complex queries, provide reusable query logic, expose only required data, and provide a logical abstraction over underlying tables.

---

# 81. Important Interview Question — What Is an Index?

### Strong Answer

> An index is a database data structure that helps the optimizer locate rows more efficiently for suitable queries. It can improve read performance, but indexes require additional storage and maintenance during data modifications.

---

# 82. Important Interview Question — Does an Index Always Improve Performance?

### Strong Answer

> No. An index is beneficial only when the optimizer determines that using it is cheaper than alternatives. Small tables, low-selectivity columns, queries returning many rows, or excessive index maintenance can make an index less useful.

---

# 83. Important Interview Question — What Are the Disadvantages of Indexes?

### Strong Answer

> Indexes require additional storage and need to be maintained when rows are inserted, updated, or deleted. Too many indexes can therefore increase write overhead and maintenance cost.

---

# 84. Important Interview Question — What Is a Composite Index?

### Strong Answer

> A composite index is an index created on multiple columns. Column order matters because the index is organized according to its leading columns, so the order should match important query patterns.

Example:

```sql
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

---

# 85. Important Interview Question — What Is a Clustered Index?

### Strong Answer

> A clustered index is an index organization where the table's row storage is organized according to an index key in database systems that support clustered indexes. The exact implementation is DBMS-specific, and typically a table has only one such physical row organization.

---

# 86. Important Interview Question — What Is a Non-Clustered Index?

### Strong Answer

> A non-clustered index is a separate index structure containing indexed keys and references to the corresponding table rows or storage locations. A table can generally have multiple non-clustered indexes.

---

# 87. Important Interview Question — Clustered vs Non-Clustered Index

### Strong Answer

> A clustered index controls the table's row organization in systems that support clustered indexes, while a non-clustered index is a separate structure that points to the corresponding rows. The exact implementation is database-specific.

---

# 88. Important Interview Question — Should We Index Every Column?

### Strong Answer

> No. Indexes should be created based on actual query patterns and workload. Every index consumes storage and adds maintenance overhead to inserts, updates, and deletes, so unnecessary indexes can hurt write performance.

---

# 89. Important Interview Question — Which Columns Are Good Candidates for Indexing?

### Strong Answer

> Columns frequently used in selective WHERE conditions, JOIN conditions, ORDER BY, or other performance-critical queries are potential candidates. Primary and unique keys are also commonly indexed or supported by index structures. The final decision should be based on query plans and workload.

---

# 90. Important Interview Question — Why Does Column Order Matter in a Composite Index?

### Strong Answer

> A composite index is ordered by its leading columns, so queries that use the leading column or leading combination can generally benefit more. For example, an index on `(department_id, salary)` is naturally useful for queries that filter by `department_id`, while a query using only `salary` may not use it effectively.

---

# 91. Important Interview Question — What Is the Difference Between a View and an Index?

| View | Index |
|---|---|
| Logical representation of a query | Data structure for efficient access |
| Simplifies data access | Improves suitable query performance |
| Can hide columns/rows | Helps locate rows |
| Usually stores query definition | Requires additional storage |
| Does not inherently improve performance | Designed primarily for access efficiency |

---

# 92. Important Interview Question — What Is the Difference Between a View and a Table?

### Strong Answer

> A table is a primary data storage structure containing rows and columns, while a normal view is a logical representation based on a query over one or more tables. A view usually does not maintain a separate copy of the underlying data.

---

# 93. Important Interview Question — What Is the Difference Between DELETE, ROLLBACK and DROP?

This is a common conceptual interview question.

### DELETE

Removes selected rows:

```sql
DELETE FROM employees
WHERE employee_id = 101;
```

### ROLLBACK

Undoes uncommitted transactional changes where transaction rollback applies.

### DROP

Removes a database object such as a table or view:

```sql
DROP TABLE employees;
```

or:

```sql
DROP VIEW employee_details;
```

---

# 94. Transaction Example for Interview

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 5000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 5000
WHERE account_id = 2;

COMMIT;
```

If the second operation fails:

```sql
ROLLBACK;
```

Interview explanation:

> I would treat the debit and credit as one transaction because the transfer should not leave the database in a partially completed state.

---

# 95. Indexing Scenario for Interview

Suppose:

```text
employees = 10 million rows
```

Frequent query:

```sql
SELECT employee_id, employee_name
FROM employees
WHERE email = 'rahul@example.com';
```

A suitable index could be:

```sql
CREATE INDEX idx_employee_email
ON employees(email);
```

If email must be unique:

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employees(email);
```

or, preferably at the logical schema level:

```sql
email VARCHAR(150) NOT NULL UNIQUE
```

and let the DBMS enforce the uniqueness appropriately.

---

# 96. Composite Index Scenario

Suppose this query runs frequently:

```sql
SELECT *
FROM employees
WHERE department_id = 10
  AND salary > 50000;
```

A possible index is:

```sql
CREATE INDEX idx_dept_salary
ON employees(department_id, salary);
```

Why?

Because:

```text
department_id
```

is the leading column and is part of the filtering condition.

The database optimizer can determine whether this index is actually beneficial.

---

# 97. View Scenario

Suppose management frequently needs:

```sql
SELECT
    e.employee_id,
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Create:

```sql
CREATE VIEW employee_department_report AS
SELECT
    e.employee_id,
    e.employee_name,
    d.department_name
FROM employees e
JOIN departments d
    ON e.department_id = d.department_id;
```

Then:

```sql
SELECT *
FROM employee_department_report;
```

This avoids repeatedly writing the same logical query.

---

# 98. Transaction + SAVEPOINT Coding Example

```sql
START TRANSACTION;

UPDATE employees
SET salary = salary + 1000
WHERE employee_id = 101;

SAVEPOINT first_update;

UPDATE employees
SET salary = salary + 2000
WHERE employee_id = 102;

ROLLBACK TO first_update;

COMMIT;
```

Conceptually:

```text
Employee 101 update
        ↓
Saved at SAVEPOINT
        ↓
Employee 102 update
        ↓
ROLLBACK TO SAVEPOINT
        ↓
Employee 102 update undone
        ↓
Employee 101 update remains
        ↓
COMMIT
```

Exact savepoint behavior and syntax can vary across DBMSs.

---

# 99. Interview Scenario — Two Users Update the Same Row

Interviewer:

> What happens if two users try to update the same row at the same time?

A strong answer:

> The database uses its concurrency-control mechanisms, such as locking and/or MVCC depending on the DBMS, to coordinate concurrent transactions. The exact behavior depends on the isolation level and database engine. One transaction may wait, fail, or operate using a versioned view depending on the situation.

This is better than simply saying:

> "The second query will fail."

because the actual behavior depends on the database system and transaction configuration.

---

# 100. Interview Scenario — Why Not Create Indexes on Everything?

A strong answer:

> Indexes improve certain read operations, but they are not free. They consume storage and must be maintained when rows are inserted, updated, or deleted. Too many indexes can therefore increase write overhead, so indexes should be created based on actual query patterns and execution plans.

---

# 101. Interview Scenario — How Would You Optimize a Slow Query?

A strong interview approach:

```text
1. Identify the slow query
        ↓
2. Inspect the execution plan
        ↓
3. Check filtering and join conditions
        ↓
4. Check whether suitable indexes exist
        ↓
5. Check whether indexes are actually being used
        ↓
6. Review query structure
        ↓
7. Check data distribution/cardinality
        ↓
8. Measure before and after changes
```

Don't simply say:

> "I will create an index."

First determine why the query is slow.

---

# 102. EXPLAIN / Execution Plan

Many databases provide an execution-plan mechanism such as:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE department_id = 10;
```

An execution plan can help you understand:

```text
Table scan
Index scan
Index seek/search
Join strategy
Estimated rows
Costs
```

Exact output and terminology depend on the DBMS.

For performance interviews, knowing how to inspect an execution plan is much more valuable than memorizing index definitions.

---

# 103. Important Practical Rule

When discussing indexes in an interview, avoid saying:

> "Indexes always make queries faster."

Instead say:

> "Indexes can improve suitable read queries, but the optimizer chooses whether to use them, and indexes also add storage and write-maintenance overhead."

This sounds more practical and demonstrates real database understanding.

---

# 104. Important Practical Rule for Transactions

Avoid saying:

> "ROLLBACK always undoes everything."

A better answer is:

> "ROLLBACK undoes the applicable uncommitted changes in the current transaction. Once changes are committed, ordinary rollback cannot undo them."

---

# 105. Important Practical Rule for Views

Avoid saying:

> "A view is a temporary table."

A better answer is:

> "A normal view is a database object based on a stored query definition. It provides a logical representation of underlying data rather than normally storing a separate copy of that data."

---

# 106. Important Practical Rule for Clustered Indexes

Avoid making DBMS-independent claims such as:

> "Every database has one clustered index."

A better answer is:

> "Clustered-index behavior is DBMS-specific. In systems that support clustered indexes, the clustered organization determines how table rows are organized around the index key, and there is typically one such row organization per table."

---

# 107. Most Important Interview Questions

Prepare these particularly well:

1. What is a transaction?
2. Why are transactions needed?
3. What is COMMIT?
4. What is ROLLBACK?
5. What is SAVEPOINT?
6. What is ACID?
7. Explain Atomicity.
8. Explain Consistency.
9. Explain Isolation.
10. Explain Durability.
11. What are transaction isolation levels?
12. What is a dirty read?
13. What is a non-repeatable read?
14. What is a phantom read?
15. READ COMMITTED vs REPEATABLE READ?
16. What is SERIALIZABLE?
17. What is a view?
18. Why are views used?
19. View vs table?
20. Does a view store data?
21. What is a materialized view?
22. What is an index?
23. Why do we use indexes?
24. Does an index always improve performance?
25. What are the disadvantages of indexes?
26. Which columns should be indexed?
27. What is a composite index?
28. Why does composite-index column order matter?
29. What is a clustered index?
30. What is a non-clustered index?
31. Clustered vs non-clustered index?
32. What is selectivity?
33. What is cardinality?
34. How does an index affect INSERT/UPDATE/DELETE?
35. How would you optimize a slow SQL query?
36. How do transactions handle concurrent updates?
37. How can views help with security?
38. How would you design an index for a frequently executed query?
39. What is an execution plan?
40. Why should you inspect an execution plan before adding indexes?

---

# 108. Quick Revision — Transactions

```text
Transaction
→ Logical unit of work

COMMIT
→ Save transaction changes

ROLLBACK
→ Undo uncommitted changes

SAVEPOINT
→ Partial rollback point

ACID
→ Atomicity
→ Consistency
→ Isolation
→ Durability
```

---

# 109. Quick Revision — Isolation

```text
READ UNCOMMITTED
→ Can allow dirty reads

READ COMMITTED
→ Prevents dirty reads
→ Non-repeatable reads can occur

REPEATABLE READ
→ Stronger repeated-read guarantees
→ Exact phantom behavior is DBMS-specific

SERIALIZABLE
→ Strongest standard isolation
→ Lower concurrency possible
```

---

# 110. Quick Revision — Views

```text
VIEW
→ Stored query definition
→ Logical representation
→ Simplifies complex queries
→ Can expose selected data

MATERIALIZED VIEW
→ Stores/precomputes query results
→ Requires refresh/update strategy
→ DBMS-specific
```

---

# 111. Quick Revision — Indexes

```text
INDEX
→ Helps efficient data retrieval

BENEFITS
→ Faster suitable reads

COSTS
→ Extra storage
→ Write overhead
→ Maintenance

COMPOSITE INDEX
→ Multiple columns

COLUMN ORDER
→ Leading columns matter

CLUSTERED
→ Row organization around index key in supporting DBMSs

NON-CLUSTERED
→ Separate index structure referencing rows
```

---

# 112. Final Interview Cheat Sheet

## Transactions

```text
Transaction
→ Unit of work

COMMIT
→ Save

ROLLBACK
→ Undo uncommitted work

SAVEPOINT
→ Partial rollback

ACID
→ Atomicity
→ Consistency
→ Isolation
→ Durability
```

## Isolation Problems

```text
Dirty Read
→ Reading uncommitted data

Non-Repeatable Read
→ Same row changes between reads

Phantom Read
→ Matching row set changes
```

## Views

```text
View
→ Stored query definition

Normal View
→ Usually no separate data copy

Materialized View
→ Stores/precomputes results

Uses
→ Simplification
→ Abstraction
→ Reuse
→ Access control
```

## Indexes

```text
Index
→ Efficient data access

Good candidates
→ Frequently filtered/joined/sorted columns

Costs
→ Storage + write maintenance

Composite Index
→ Multiple columns

Leading Column
→ Important for index usability

Execution Plan
→ Check before optimizing
```

---

# 113. What You Should Be Able to Explain Without Memorizing

Before moving to the next SQL topic, make sure you can naturally explain:

```text
1. Why transactions are needed
2. COMMIT vs ROLLBACK
3. SAVEPOINT
4. ACID with a bank-transfer example
5. Dirty read
6. Non-repeatable read
7. Phantom read
8. Isolation levels
9. What a view is
10. View vs table
11. View vs materialized view
12. What an index is
13. Why indexes improve some queries
14. Why indexes can hurt write performance
15. Composite indexes
16. Why index column order matters
17. Clustered vs non-clustered indexes
18. Selectivity and cardinality
19. Execution plans
20. How you would approach a slow query
```

The most impressive interview answers connect the concepts to **real database behavior**:

```text
Transactions
→ Prevent partially completed business operations

Views
→ Provide reusable logical interfaces and controlled data exposure

Indexes
→ Improve suitable reads but introduce storage and write-maintenance costs

Execution Plans
→ Help determine whether the database is actually using an efficient strategy
```