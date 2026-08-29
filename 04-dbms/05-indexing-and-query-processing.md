# Indexing and Query Processing

## 1. What is an Index?

An **index** is a database data structure that helps the DBMS find rows more efficiently without scanning the entire table.

It is similar to an index in a book.

### Without an Index

Suppose we have:

```text
Employees
--------------------------------
id     name       department
1      Ravi       IT
2      Anu        HR
3      John       IT
...
1,000,000 rows
```

Query:

```sql
SELECT *
FROM employees
WHERE id = 500000;
```

Without a suitable index, the database may need to examine many rows.

### With an Index

If `id` has an index:

```text
Index
 ↓
Find id = 500000
 ↓
Locate corresponding row
```

The database can avoid scanning the entire table.

---

# 2. Why are Indexes Used?

Indexes are mainly used to:

- Speed up data retrieval
- Reduce the amount of data that must be scanned
- Improve performance of suitable `WHERE` conditions
- Help with some `JOIN` operations
- Help with some `ORDER BY` operations
- Help with some `GROUP BY` operations

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

An index on `department` may help depending on the data distribution and the query plan.

---

# 3. Basic Index Example

Create an index:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

Now the DBMS has an index on:

```text
employees.name
```

A query such as:

```sql
SELECT *
FROM employees
WHERE name = 'Ravi';
```

may use this index if the optimizer determines that it is beneficial.

---

# 4. Index Does Not Store a Complete Copy of the Table

An index generally stores information that allows the DBMS to locate the corresponding table data.

Conceptually:

```text
Index
----------------
Key        Row Location
Ravi       → Row 10
John       → Row 25
Sam        → Row 40
```

The exact physical structure depends on the DBMS and index type.

---

# 5. What is a B-Tree Index?

A **B-tree-style index** is a tree-based index structure commonly used by relational databases.

It keeps keys organized so that searches, range queries, and ordered access can be performed efficiently.

Conceptually:

```text
                 [50]
                /    \
          [20, 30]   [70, 90]
          /   |   \    /   \
        ...  ...  ... ...  ...
```

The DBMS follows the appropriate branch instead of scanning every key.

---

# 6. Why are B-Trees Useful?

B-tree-style indexes are useful for queries involving:

```sql
=
>
<
>=
<=
BETWEEN
ORDER BY
```

Example:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

An appropriate B-tree index may help locate the relevant range efficiently.

---

# 7. What is a Hash Index?

A **hash index** uses a hash-based structure to locate values.

Conceptually:

```text
Key
 ↓
Hash Function
 ↓
Bucket
 ↓
Matching data
```

Hash indexes are especially useful for equality lookups such as:

```sql
WHERE id = 100
```

They are generally not suitable for ordered range searches in the way B-tree indexes are.

---

# 8. B-Tree vs Hash Index

| B-Tree | Hash |
|---|---|
| Supports equality searches | Supports equality searches |
| Good for range queries | Generally not suitable for range queries |
| Can support ordered access | Does not naturally provide ordered access |
| Useful for `>`, `<`, `BETWEEN` | Mainly useful for exact matches |

---

# 9. What is a Clustered Index?

A **clustered index** determines how table rows are physically organized according to the index key in systems that implement clustered indexes in this manner.

A table can generally have only one such physical ordering because the rows cannot be physically organized in multiple different orders simultaneously.

The exact implementation is DBMS-specific.

---

# 10. What is a Non-Clustered Index?

A **non-clustered index** is a separate index structure that stores indexed values and references to the corresponding table rows or data locations.

Conceptually:

```text
Non-clustered Index
        ↓
Index Key
        ↓
Row/Data Location
        ↓
Actual Table Row
```

A table can have multiple non-clustered indexes, subject to DBMS limitations.

---

# 11. Clustered vs Non-Clustered Index

| Clustered | Non-Clustered |
|---|---|
| Determines/closely controls physical row organization in systems that support it | Separate structure from table data |
| Usually one physical ordering | Multiple indexes can exist |
| Can be efficient for range access | Useful for targeted lookups |
| Exact behavior is DBMS-specific | Exact behavior is DBMS-specific |

### Important Interview Point

Do not assume every DBMS implements clustered indexes identically.

---

# 12. What is a Composite Index?

A **composite index** is an index created on multiple columns.

Example:

```sql
CREATE INDEX idx_emp_dept_salary
ON employees(department, salary);
```

This index contains:

```text
department
+
salary
```

---

# 13. Why Use a Composite Index?

Suppose the common query is:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

An index on:

```text
(department, salary)
```

may be useful.

The order of columns matters.

---

# 14. Column Order in a Composite Index

Consider:

```sql
CREATE INDEX idx_emp
ON employees(department, salary);
```

The index is ordered conceptually by:

```text
department
    ↓
salary
```

This can be useful for queries filtering by:

```sql
department
```

or:

```sql
department + salary
```

But a query filtering only by:

```sql
salary
```

may not be able to use this index as effectively.

This is related to the **leftmost-prefix principle** for B-tree-style composite indexes.

---

# 15. Leftmost-Prefix Principle

For:

```sql
CREATE INDEX idx_emp
ON employees(department, salary, age);
```

The index can generally be useful for conditions involving the leading columns, such as:

```text
department
department + salary
department + salary + age
```

But an index beginning with:

```text
department
```

is not automatically optimal for:

```text
salary only
```

or:

```text
age only
```

The exact optimizer behavior depends on the DBMS.

---

# 16. What is a Unique Index?

A **unique index** ensures that duplicate indexed key values are not allowed.

Example:

```sql
CREATE UNIQUE INDEX idx_employee_email
ON employees(email);
```

This prevents two rows from having the same indexed email value, subject to the DBMS's handling of `NULL`.

---

# 17. Primary Key and Index

A primary key identifies each row uniquely.

Most relational DBMSs create or require an index-like structure to efficiently enforce a primary key, although the exact implementation is DBMS-specific.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

The DBMS typically creates an index associated with the primary key.

---

# 18. Foreign Key and Index

A foreign key does not universally require an automatically created index.

However, indexing foreign-key columns can often improve:

- Joins
- Parent-row updates/deletes
- Referential-integrity checks

Example:

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

---

# 19. When Should You Create an Index?

Indexes are useful when columns are frequently used for:

```text
WHERE
JOIN
ORDER BY
GROUP BY
```

especially when they significantly reduce the number of rows that need to be processed.

Example:

```sql
SELECT *
FROM orders
WHERE customer_id = 100;
```

An index on:

```text
customer_id
```

may improve this query.

---

# 20. When Should You Avoid an Index?

Indexes are not automatically beneficial.

Too many indexes can:

- Consume storage
- Increase `INSERT` cost
- Increase `UPDATE` cost
- Increase `DELETE` cost
- Increase maintenance overhead

Every time indexed data changes, relevant indexes may also need to be updated.

---

# 21. Indexing Trade-Off

Remember:

```text
More indexes
     ↓
Faster suitable reads
     +
More storage
     +
Slower writes
     +
More maintenance
```

Therefore, indexes should be created based on actual workload and query patterns.

---

# 22. What is Selectivity?

**Selectivity** describes how effectively a predicate narrows down the rows.

A column with many distinct values generally has higher selectivity than a column with very few distinct values.

Example:

```text
employee_id
→ 1,000,000 distinct values

gender
→ few distinct values
```

An index on `employee_id` is often more selective than an index on a low-cardinality column.

---

# 23. High vs Low Selectivity

Example:

```text
employee_id
1
2
3
4
5
...
```

Very high number of distinct values.

Potentially high selectivity.

Compare:

```text
department
IT
HR
Sales
IT
HR
Sales
...
```

Few distinct values.

Lower selectivity.

### Interview Point

An index is not automatically useful simply because the column appears in a `WHERE` clause. The optimizer considers selectivity and other factors.

---

# 24. What is Query Processing?

**Query processing** is the process by which a DBMS takes a SQL query, determines how to execute it, and produces the result.

Conceptually:

```text
SQL Query
   ↓
Parsing
   ↓
Validation / Binding
   ↓
Optimization
   ↓
Execution Plan
   ↓
Execution
   ↓
Result
```

---

# 25. Main Stages of Query Processing

Important stages include:

```text
1. Parsing
2. Validation / Semantic Analysis
3. Query Rewriting / Transformation
4. Optimization
5. Plan Selection
6. Execution
```

Exact stages vary between database systems.

---

# 26. What is Parsing?

Parsing checks the SQL statement's syntax and converts it into an internal representation.

Example:

```sql
SELECT name
FROM employees
WHERE salary > 50000;
```

The DBMS parses the query and checks whether its syntax is valid.

If syntax is invalid:

```sql
SELEC name FROM employees;
```

the database returns a syntax error.

---

# 27. What is Semantic Analysis?

After parsing, the DBMS verifies that the query makes sense in the database context.

It may check:

- Does the table exist?
- Does the column exist?
- Are names ambiguous?
- Does the user have the required permissions?
- Are data types compatible?

Example:

```sql
SELECT salary
FROM employee;
```

If the actual table is:

```text
employees
```

the DBMS can report that the referenced table does not exist.

---

# 28. What is Query Optimization?

**Query optimization** is the process of selecting an efficient execution strategy for a SQL query.

The DBMS may consider:

```text
Indexes
Join methods
Join order
Filtering
Sorting
Table statistics
Estimated costs
```

---

# 29. Why is Query Optimization Needed?

The same SQL query can often be executed in multiple ways.

Example:

```sql
SELECT *
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

The DBMS could choose different:

```text
Join order
Join algorithm
Access method
```

The optimizer tries to choose a low-cost plan.

---

# 30. What is an Execution Plan?

An **execution plan** describes how the DBMS intends to execute a query.

It may contain operations such as:

```text
Table Scan
Index Scan
Index Seek
Join
Sort
Aggregate
Filter
```

The exact names depend on the DBMS.

---

# 31. Example Execution Plan

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 100;
```

Possible plan:

```text
Index Lookup
     ↓
Find employee_id = 100
     ↓
Fetch row
```

Without a useful index, the plan might instead use:

```text
Table Scan
     ↓
Check every row
```

---

# 32. What is a Table Scan?

A **table scan** reads rows from the table to evaluate the query.

For a large table, scanning the entire table can be expensive when only a small number of rows are required.

Example:

```sql
SELECT *
FROM employees
WHERE name = 'Ravi';
```

If no useful index exists, the optimizer may choose a table scan.

---

# 33. What is an Index Scan?

An **index scan** reads a substantial portion or all of an index to find qualifying entries.

It may be useful when a large portion of the index needs to be examined.

The exact terminology differs across DBMSs.

---

# 34. What is an Index Seek?

An **index seek** navigates an index to locate a relatively specific key or key range.

Conceptually:

```text
Index
 ↓
Navigate to target
 ↓
Find matching entries
```

It can be highly efficient for selective predicates.

Again, exact terminology and behavior depend on the DBMS.

---

# 35. Index Scan vs Index Seek

| Index Scan | Index Seek |
|---|---|
| Examines many index entries | Navigates directly to relevant key/range |
| Can be appropriate when many rows qualify | Often useful for selective lookups |
| May read a large part of the index | Usually examines a smaller relevant portion |
| Exact behavior depends on DBMS | Exact behavior depends on DBMS |

---

# 36. What is Cost-Based Optimization?

A **cost-based optimizer (CBO)** evaluates possible execution plans and estimates their costs.

Conceptually:

```text
Query
 ↓
Possible Plans
 ↓
Estimate Costs
 ↓
Choose Lower-Cost Plan
 ↓
Execute
```

Cost estimates may consider:

```text
I/O
CPU
Memory
Number of rows
Data distribution
Indexes
Statistics
```

---

# 37. What are Database Statistics?

Database statistics provide information about data distribution that the optimizer can use to estimate query costs.

Examples include information about:

```text
Number of rows
Number of distinct values
Value distribution
Data density
```

The exact statistics maintained depend on the DBMS.

---

# 38. Why are Statistics Important?

Suppose the optimizer needs to decide whether to use an index.

If it estimates that:

```text
1 row matches
```

using the index may be attractive.

If it estimates:

```text
900,000 rows match
```

a table scan may be cheaper.

Therefore:

```text
Statistics
    ↓
Cardinality estimates
    ↓
Cost estimates
    ↓
Execution plan
```

---

# 39. What is Cardinality?

**Cardinality** can refer to the number of rows produced by an operation or the number of distinct values in a particular context.

In query optimization, **cardinality estimation** commonly means estimating how many rows an operation will produce.

Example:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

If the optimizer estimates:

```text
10,000 rows
```

that estimate affects plan selection.

---

# 40. What is a Query Optimizer?

The **query optimizer** is the DBMS component that evaluates possible ways to execute a query and chooses an execution plan.

Conceptually:

```text
SQL
 ↓
Optimizer
 ↓
Possible Plans
 ↓
Cost Estimation
 ↓
Chosen Plan
```

---

# 41. What is a Query Execution Engine?

The **query execution engine** executes the selected plan.

Conceptually:

```text
Optimizer
    ↓
Execution Plan
    ↓
Execution Engine
    ↓
Database Operations
    ↓
Result
```

---

# 42. Query Processing Flow

A useful interview diagram is:

```text
                  SQL Query
                      ↓
                   Parser
                      ↓
             Semantic Analysis
                      ↓
              Query Transformation
                      ↓
                Query Optimizer
                      ↓
              Execution Plan
                      ↓
             Execution Engine
                      ↓
                 Data Access
                      ↓
                  Result
```

---

# 43. What is Query Rewriting?

**Query rewriting** transforms a query into another logically equivalent form that may be easier or cheaper to execute.

Examples of optimizer transformations can include:

```text
Predicate pushdown
Join reordering
Removing unnecessary operations
```

---

# 44. What is Predicate Pushdown?

**Predicate pushdown** means applying filtering conditions as early as possible so that fewer rows need to be processed by later operations.

Example:

```sql
SELECT *
FROM employees e
JOIN departments d
ON e.department_id = d.department_id
WHERE e.salary > 50000;
```

Conceptually:

```text
Filter employees
        ↓
Only relevant employees
        ↓
Join with departments
```

instead of carrying unnecessary rows through the join.

---

# 45. Why Does Predicate Pushdown Help?

Suppose:

```text
Employees = 1,000,000 rows
```

After filtering:

```text
salary > 50000
→ 10,000 rows
```

Joining 10,000 rows may be much cheaper than joining all 1,000,000 rows.

Conceptually:

```text
1,000,000 rows
       ↓ filter
10,000 rows
       ↓ join
Less work
```

---

# 46. What is Join Ordering?

When a query contains multiple joins, the optimizer may choose the order in which tables are joined.

Example:

```text
A JOIN B JOIN C
```

Possible orders:

```text
(A JOIN B) JOIN C
```

or:

```text
A JOIN (B JOIN C)
```

Different orders can have very different costs.

---

# 47. Why Does Join Order Matter?

Suppose:

```text
Table A → 1,000,000 rows
Table B → 100 rows
Table C → 500 rows
```

If filtering early reduces A to:

```text
1,000 rows
```

then joining the smaller intermediate result can significantly reduce work.

Therefore:

```text
Good join order
→ Smaller intermediate results
→ Less work
→ Better performance
```

---

# 48. Common Join Algorithms

Important join algorithms include:

```text
Nested Loop Join
Hash Join
Merge Join
```

The optimizer chooses among them based on the query and estimated costs.

---

# 49. What is Nested Loop Join?

A **nested loop join** compares rows from one input with rows from another input.

Conceptually:

```text
For each row in A:
    Find matching rows in B
```

Example:

```text
A:
1
2
3

B:
1
2
3
```

The DBMS checks matching values according to the join condition.

Nested loop joins can be effective when one input is small and the other has an appropriate index.

---

# 50. What is Hash Join?

A **hash join** typically builds a hash structure on one input and probes it using rows from the other input.

Conceptually:

```text
Build hash table
      ↓
Hash matching rows
      ↓
Probe with other input
      ↓
Return matches
```

Hash joins are commonly useful for equality joins.

Example:

```sql
SELECT *
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

---

# 51. What is Merge Join?

A **merge join** combines two inputs that are ordered by the join key.

Conceptually:

```text
Sorted A
   +
Sorted B
   ↓
Merge matching values
```

It can be efficient when suitable sorted inputs are already available or sorting is otherwise worthwhile.

---

# 52. Join Algorithm Summary

| Algorithm | Common Strength |
|---|---|
| Nested Loop Join | Small outer input / useful index |
| Hash Join | Equality joins |
| Merge Join | Ordered inputs / suitable sorted data |

The optimizer chooses based on estimated costs and DBMS implementation.

---

# 53. What is an SARGable Predicate?

A **SARGable** predicate is a search condition that allows the DBMS to use an index efficiently.

Example:

```sql
SELECT *
FROM employees
WHERE salary = 50000;
```

An index on:

```text
salary
```

may be usable.

---

# 54. Non-SARGable Example

Suppose:

```sql
SELECT *
FROM employees
WHERE UPPER(name) = 'RAVI';
```

If there is a normal index on:

```text
name
```

the function applied to the column may prevent efficient use of that index in many DBMSs.

A better design may involve an appropriate function-based/generated-column index where supported.

---

# 55. Another Non-SARGable Example

Instead of:

```sql
WHERE salary + 1000 > 50000
```

the condition can sometimes be rewritten as:

```sql
WHERE salary > 49000
```

This transformation can make index usage easier, although the exact optimizer behavior depends on the DBMS.

---

# 56. SARGable vs Non-SARGable

| SARGable | Non-SARGable |
|---|---|
| Can often use an index efficiently | May prevent efficient index access |
| Usually avoids applying functions to the indexed column | Often applies functions/calculations to the column |
| Helps efficient filtering | Can increase scanning/work |

---

# 57. Why Does `SELECT *` Matter?

Consider:

```sql
SELECT *
FROM employees
WHERE employee_id = 100;
```

Even if the index finds the row quickly, the DBMS may still need to access the table to retrieve columns not contained in the index.

Selecting only required columns can reduce unnecessary data access.

Better:

```sql
SELECT name, salary
FROM employees
WHERE employee_id = 100;
```

---

# 58. What is a Covering Index?

A **covering index** contains all columns needed by a particular query, allowing the DBMS to satisfy the query from the index without fetching the full table row, when supported by the DBMS and chosen by the optimizer.

Example query:

```sql
SELECT name, salary
FROM employees
WHERE department_id = 10;
```

An index containing:

```text
department_id
name
salary
```

could potentially cover this query.

---

# 59. Covering Index Benefit

Without covering:

```text
Index
 ↓
Find row
 ↓
Table lookup
 ↓
Get remaining columns
```

With a suitable covering index:

```text
Index
 ↓
Find row
 ↓
Get required columns
 ↓
Return result
```

This can reduce additional table access.

---

# 60. What is Index Fragmentation?

Index fragmentation occurs when the physical organization of index pages becomes less efficient due to changes such as inserts, updates, and deletes.

Possible effects include:

```text
More page reads
Poorer locality
Extra storage
Slower scans
```

The exact impact and maintenance techniques depend on the DBMS.

---

# 61. Why Can Too Many Indexes Hurt Performance?

Suppose a table has:

```text
5 indexes
```

and we execute:

```sql
INSERT INTO employees
VALUES (...);
```

The DBMS may need to update multiple index structures.

Therefore:

```text
More indexes
→ More write maintenance
```

Similarly:

```text
UPDATE
DELETE
```

may also require index maintenance.

---

# 62. Why Doesn't the DBMS Always Use an Index?

This is a very common interview question.

The optimizer may choose not to use an index because:

- The query returns many rows
- The index has low selectivity
- A table scan is cheaper
- The table is small
- Statistics suggest another plan is better
- The predicate is not index-friendly
- Required columns cause expensive table lookups
- The index does not match the query well

### Important

```text
Index exists
≠
Index must be used
```

The optimizer chooses the execution plan.

---

# 63. How Do You Check a Query's Execution Plan?

Most DBMSs provide an `EXPLAIN` or similar command.

Example:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_id = 100;
```

Some DBMSs use variants such as:

```sql
EXPLAIN ANALYZE
```

or:

```sql
SET SHOWPLAN
```

The exact syntax is DBMS-specific.

---

# 64. What Should You Look for in an Execution Plan?

Important things to inspect include:

```text
1. Table scans
2. Index scans/seeks
3. Join algorithms
4. Join order
5. Estimated rows
6. Actual rows
7. Sort operations
8. Aggregate operations
9. Expensive operators
10. Filter operations
```

A major concern is often a large mismatch between estimated and actual row counts.

---

# 65. Query Performance Example

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 500000;
```

Suppose:

```text
Employees = 10 million rows
```

Without a useful index:

```text
Potential table scan
↓
Many rows examined
↓
Higher I/O
```

With a suitable index:

```text
Index access
↓
Locate employee_id = 500000
↓
Fetch row
```

The second plan may be significantly cheaper.

---

# 66. Index on a Low-Cardinality Column

Suppose:

```text
employees = 1,000,000
```

and:

```text
gender = Male/Female
```

An index on `gender` may not be very selective for a query such as:

```sql
SELECT *
FROM employees
WHERE gender = 'Male';
```

If almost half the table matches, the optimizer may determine that scanning the table is cheaper.

---

# 67. Index on a High-Cardinality Column

Suppose:

```text
employee_id
```

contains unique values:

```text
1
2
3
...
1,000,000
```

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 987654;
```

Only one row matches.

An index is likely to be useful.

---

# 68. Indexing and WHERE Clause

A common rule is:

```text
Frequently filtered column
+
High usefulness/selectivity
→
Potential index candidate
```

Example:

```sql
SELECT *
FROM orders
WHERE customer_id = 100;
```

Potential index:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

But actual usefulness should be confirmed using workload and execution plans.

---

# 69. Indexing and JOIN

Suppose:

```sql
SELECT *
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

Indexes on join columns can sometimes improve join performance.

For example:

```sql
CREATE INDEX idx_employee_department
ON employees(department_id);
```

Whether the index is used depends on the chosen execution plan.

---

# 70. Indexing and ORDER BY

Query:

```sql
SELECT *
FROM employees
ORDER BY employee_id;
```

An appropriate index may allow the DBMS to obtain rows in the required order without an additional sort, depending on the DBMS and plan.

---

# 71. Indexing and GROUP BY

Query:

```sql
SELECT department_id, COUNT(*)
FROM employees
GROUP BY department_id;
```

An appropriate index may help the DBMS access data in an order useful for grouping, but the optimizer may still choose another strategy.

---

# 72. Important Index Design Principles

Remember these:

```text
1. Index columns frequently used for selective filtering.
2. Consider columns used in joins.
3. Consider columns used in sorting/grouping.
4. Think carefully about composite-index column order.
5. Avoid unnecessary indexes.
6. Remember indexes increase write cost.
7. Check execution plans.
8. Keep statistics reasonably current according to the DBMS.
9. Consider covering indexes for important queries.
10. Always evaluate indexes using the actual workload.
```

---

# 73. Frequently Asked Interview Questions

## Q1. What is an index?

### Answer

> An index is a database data structure that helps the DBMS locate rows efficiently without scanning the entire table in suitable cases.

---

## Q2. Why are indexes used?

### Answer

> Indexes are mainly used to improve the performance of suitable read operations such as filtering, joining, sorting, and grouping.

---

## Q3. What is the disadvantage of indexes?

### Answer

> Indexes consume storage and increase the cost of `INSERT`, `UPDATE`, and `DELETE` operations because the relevant index structures may also need to be maintained.

---

## Q4. What is a B-tree index?

### Answer

> A B-tree-style index is a tree-based structure that keeps keys organized and supports efficient equality, range, and ordered access.

---

## Q5. What is a hash index?

### Answer

> A hash index uses hashing to locate keys and is particularly useful for equality lookups. It is generally not designed for ordered range queries.

---

## Q6. B-tree vs Hash index?

### Answer

> B-tree indexes support both equality and range-based access, while hash indexes are primarily suited to equality lookups.

---

## Q7. What is a composite index?

### Answer

> A composite index is an index created on multiple columns.

Example:

```sql
CREATE INDEX idx_emp
ON employees(department_id, salary);
```

---

## Q8. Does column order matter in a composite index?

### Answer

> Yes. The order matters because B-tree-style composite indexes are organized starting with the first column. An index on `(department_id, salary)` is generally more useful for queries involving `department_id` than for queries filtering only on `salary`.

---

## Q9. What is the leftmost-prefix principle?

### Answer

> For a composite B-tree-style index, queries that use the leading columns can generally use the index more effectively than queries that skip the leading columns.

---

## Q10. What is a clustered index?

### Answer

> A clustered index determines or closely controls the physical organization of table rows according to the index key in DBMSs that support clustered indexing in this manner. Exact behavior is DBMS-specific.

---

## Q11. What is a non-clustered index?

### Answer

> A non-clustered index is a separate index structure containing indexed keys and references to the corresponding table data.

---

## Q12. Why can a table generally have only one clustered index?

### Answer

> Because the physical rows can have only one primary physical ordering at a time in systems where a clustered index defines that ordering.

---

## Q13. What is a covering index?

### Answer

> A covering index contains all columns needed by a query, allowing the DBMS to satisfy the query directly from the index without additional table-row lookups when the optimizer chooses that plan.

---

## Q14. What is query optimization?

### Answer

> Query optimization is the process of selecting an efficient execution strategy for a SQL query.

---

## Q15. What is an execution plan?

### Answer

> An execution plan describes the operations the DBMS intends to perform to execute a query.

---

## Q16. What is a query optimizer?

### Answer

> A query optimizer evaluates possible execution strategies and chooses an execution plan based on estimated cost and other factors.

---

## Q17. What is a table scan?

### Answer

> A table scan reads table rows to evaluate a query, potentially examining a large portion or all of the table.

---

## Q18. What is an index scan?

### Answer

> An index scan examines many index entries, potentially a large portion or all of the index, to find qualifying rows.

---

## Q19. What is an index seek?

### Answer

> An index seek navigates an index to locate a specific key or key range efficiently.

---

## Q20. Why doesn't the database always use an index?

### Answer

> Because the optimizer may determine that another plan, such as a table scan, is cheaper based on selectivity, table size, statistics, estimated row counts, and other factors.

---

## Q21. What is selectivity?

### Answer

> Selectivity describes how effectively a condition narrows down the rows. A highly selective condition returns a relatively small portion of the table.

---

## Q22. What are database statistics?

### Answer

> Database statistics describe data distribution and help the optimizer estimate row counts and execution costs.

---

## Q23. What is cardinality estimation?

### Answer

> Cardinality estimation is the optimizer's estimation of how many rows an operation will produce.

---

## Q24. What is a cost-based optimizer?

### Answer

> A cost-based optimizer compares possible execution plans using estimated costs and chooses a plan expected to be efficient.

---

## Q25. What is predicate pushdown?

### Answer

> Predicate pushdown applies filtering conditions as early as possible so fewer rows need to be processed by later operations.

---

## Q26. What are common join algorithms?

### Answer

```text
Nested Loop Join
Hash Join
Merge Join
```

---

## Q27. When is a nested loop join useful?

### Answer

> It can be effective when the outer input is small and the inner input has an appropriate index or can otherwise be searched efficiently.

---

## Q28. When is a hash join useful?

### Answer

> Hash joins are commonly useful for equality joins, especially when suitable indexes are not available and the DBMS can efficiently build and probe a hash structure.

---

## Q29. When is a merge join useful?

### Answer

> A merge join can be efficient when both inputs are already sorted or can be obtained in suitable order efficiently.

---

## Q30. What is a SARGable predicate?

### Answer

> A SARGable predicate is a search condition that allows the database to use an index efficiently for locating matching rows.

---

# 74. Scenario-Based Interview Questions

## Scenario 1: Large Table Search

You have:

```text
employees = 10 million rows
```

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 5000000;
```

There is an index on `employee_id`.

### Question

Why can the index improve performance?

### Answer

Because `employee_id` is highly selective if it is unique, so the DBMS can potentially locate the required row through the index rather than scanning millions of rows.

---

# 75. Scenario 2: Low Selectivity

Table:

```text
employees = 1,000,000 rows
```

Query:

```sql
SELECT *
FROM employees
WHERE gender = 'Male';
```

Suppose 500,000 rows match.

### Question

Will the database definitely use the index on `gender`?

### Answer

No.

The optimizer may determine that scanning the table is cheaper because a very large percentage of rows match.

---

# 76. Scenario 3: Composite Index

Index:

```sql
CREATE INDEX idx_emp
ON employees(department_id, salary);
```

### Query A

```sql
SELECT *
FROM employees
WHERE department_id = 10;
```

### Question

Can the index be useful?

### Answer

Yes. The query uses the leading column.

---

### Query B

```sql
SELECT *
FROM employees
WHERE department_id = 10
AND salary > 50000;
```

### Question

Can the index be useful?

### Answer

Yes. It uses the leading column and can also use the second column depending on the optimizer and predicate.

---

### Query C

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### Question

Is the composite index automatically ideal?

### Answer

No. Since `salary` is not the leading column, the index may not be efficiently usable for this query.

---

# 77. Scenario 4: Function on Indexed Column

Index:

```sql
CREATE INDEX idx_name
ON employees(name);
```

Query:

```sql
SELECT *
FROM employees
WHERE UPPER(name) = 'RAVI';
```

### Question

Can the normal index on `name` always be used efficiently?

### Answer

No. Applying a function to the indexed column can make the predicate non-SARGable in many systems.

An appropriate function-based index or generated-column strategy may be needed depending on the DBMS.

---

# 78. Scenario 5: Query Plan

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 100;
```

You run:

```sql
EXPLAIN
SELECT *
FROM employees
WHERE employee_id = 100;
```

The plan shows:

```text
Table Scan
```

### Question

Does this automatically mean the database is badly designed?

### Answer

No.

The table may be small, the predicate may not be selective, statistics may favor a scan, or the optimizer may have another reason to choose a scan.

The execution plan and workload should be analyzed before changing indexes.

---

# 79. Scenario 6: Too Many Indexes

A table has:

```text
20 indexes
```

and receives millions of inserts every day.

### Question

What problem can occur?

### Answer

Every insert may require maintenance of multiple indexes, increasing write overhead, storage usage, and maintenance cost.

---

# 80. Scenario 7: Covering Index

Query:

```sql
SELECT name, salary
FROM employees
WHERE department_id = 10;
```

Possible index:

```text
(department_id, name, salary)
```

### Question

Why might this be useful?

### Answer

The index contains both the filtering column and the columns required in the result, so the DBMS may be able to satisfy the query directly from the index without fetching the full table rows.

---

# 81. Scenario 8: Join Performance

Query:

```sql
SELECT e.name, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

### Question

What should you consider when optimizing this query?

### Answer

Consider:

```text
Indexes on join columns
Table sizes
Join order
Join algorithm
Statistics
Number of rows produced
Execution plan
```

---

# 82. Most Important Interview Topics

If you have limited time, prioritize:

```text
⭐⭐⭐⭐⭐

1. What is an index?
2. Advantages and disadvantages of indexes
3. B-tree index
4. Hash index
5. Clustered vs non-clustered index
6. Composite indexes
7. Leftmost-prefix principle
8. Selectivity
9. Query processing
10. Query optimization
11. Execution plans
12. Table scan vs index access
13. Why an index may not be used
14. Cost-based optimization
15. Database statistics
16. Cardinality
17. Predicate pushdown
18. Join algorithms
19. SARGable predicates
20. Covering indexes
```

---

# 83. One-Minute Revision

```text
INDEX
→ Helps locate data efficiently

B-TREE
→ Equality + range + ordered access

HASH
→ Mainly equality

COMPOSITE INDEX
→ Multiple columns

COLUMN ORDER
→ Matters

LEFTMOST PREFIX
→ Leading columns matter

CLUSTERED
→ Controls/closely relates to physical row organization
   in supporting DBMSs

NON-CLUSTERED
→ Separate index structure

SELECTIVITY
→ How much a condition narrows rows

QUERY PROCESSING
→ Parse
→ Validate
→ Transform
→ Optimize
→ Execute

OPTIMIZER
→ Chooses execution plan

EXECUTION PLAN
→ How query will be executed

TABLE SCAN
→ Reads table rows

INDEX SCAN
→ Reads many index entries

INDEX SEEK
→ Navigates to relevant key/range

STATISTICS
→ Help optimizer estimate costs

CARDINALITY
→ Estimated/actual number of rows produced

PREDICATE PUSHDOWN
→ Filter earlier

JOIN ALGORITHMS
→ Nested Loop
→ Hash Join
→ Merge Join

SARGABLE
→ Index-friendly search condition

COVERING INDEX
→ Index contains all required query columns

TOO MANY INDEXES
→ Faster reads but slower writes
```

# 84. Final Interview Takeaway

The main concept to remember is:

```text
SQL Query
    ↓
Parser
    ↓
Validation
    ↓
Query Transformation
    ↓
Optimizer
    ↓
Statistics + Indexes + Costs
    ↓
Best/Low-Cost Execution Plan
    ↓
Scan / Index Access / Join / Sort / Aggregate
    ↓
Execution
    ↓
Result
```

For indexing, remember:

```text
Index
→ Faster suitable reads

But:

Index
→ Extra storage
→ Extra write cost
→ Maintenance overhead
```

The most important interview idea is:

> **Having an index does not guarantee that the database will use it. The query optimizer chooses the execution plan based on factors such as selectivity, statistics, estimated cardinality, available indexes, and estimated cost.**