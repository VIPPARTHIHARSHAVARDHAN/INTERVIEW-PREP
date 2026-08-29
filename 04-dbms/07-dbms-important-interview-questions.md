# DBMS Important Interview Questions

> **Placement-focused revision file:** If you are short on time, prepare this file thoroughly. It covers the most important DBMS concepts and commonly asked interview questions from the topics in the previous files.

---

# 1. DBMS Basics

## Q1. What is a DBMS?

> A DBMS (Database Management System) is software used to create, store, manage, retrieve, and manipulate data in a database.

Examples:

```text
MySQL
PostgreSQL
Oracle
SQL Server
```

---

## Q2. What are the advantages of a DBMS?

- Reduces data redundancy
- Provides data consistency
- Provides security
- Supports concurrent access
- Provides backup and recovery
- Provides data integrity
- Makes data management easier

---

## Q3. What is a database?

> A database is an organized collection of data that can be stored, accessed, and managed efficiently.

---

## Q4. DBMS vs File System?

| DBMS | File System |
|---|---|
| Manages structured data | Stores files/data |
| Supports querying | Limited querying |
| Provides concurrency control | Limited support |
| Provides security mechanisms | Basic file permissions |
| Supports transactions | Usually lacks DB transactions |
| Provides backup/recovery mechanisms | More application-dependent |

---

## Q5. What is an RDBMS?

> An RDBMS (Relational Database Management System) stores data in tables consisting of rows and columns and maintains relationships between tables.

Examples:

```text
MySQL
PostgreSQL
Oracle
SQL Server
```

---

## Q6. DBMS vs RDBMS?

| DBMS | RDBMS |
|---|---|
| General database management system | Relational database management system |
| May not use relational tables | Uses tables |
| Relationships are not necessarily relational | Supports relationships between tables |
| Relational constraints may not apply | Supports relational integrity constraints |

---

# 2. Keys

## Q7. What is a key?

> A key is an attribute or set of attributes used to identify records or establish relationships between tables.

---

## Q8. What is a Primary Key?

> A primary key uniquely identifies each row in a table. It cannot contain `NULL` values.

Example:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

---

## Q9. What is a Foreign Key?

> A foreign key is a column or set of columns that references a key in another table, usually a primary key or candidate key, to establish a relationship and enforce referential integrity.

Example:

```sql
CREATE TABLE departments (
    department_id INT PRIMARY KEY
);

CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

## Q10. Primary Key vs Foreign Key?

| Primary Key | Foreign Key |
|---|---|
| Identifies rows in its table | References a key in another table |
| Must be unique | Can contain duplicate values |
| Cannot be `NULL` | Can be `NULL` unless restricted |
| Identifies entity | Establishes relationship |

---

## Q11. What is a Candidate Key?

> A candidate key is a minimal set of attributes that can uniquely identify a row.

A table can have multiple candidate keys, but one is selected as the primary key.

---

## Q12. What is a Super Key?

> A super key is any set of attributes that uniquely identifies a row, possibly containing extra attributes.

Example:

```text
employee_id
employee_id + name
```

If `employee_id` is unique, both can be super keys, but only `employee_id` is minimal.

---

## Q13. Candidate Key vs Super Key?

> Every candidate key is a super key, but every super key is not a candidate key because a super key may contain unnecessary attributes.

---

## Q14. What is a Composite Key?

> A composite key is a key consisting of two or more columns.

Example:

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```

---

# 3. Relationships and ER Model

## Q15. What is an ER Model?

> An Entity-Relationship model represents entities, their attributes, and relationships between entities.

Example:

```text
Student
   |
   | enrolls
   |
Course
```

---

## Q16. What is an Entity?

> An entity is a real-world object or concept about which data is stored.

Examples:

```text
Student
Employee
Product
Department
```

---

## Q17. What is a Relationship?

> A relationship represents an association between entities.

Example:

```text
Employee → works in → Department
```

---

## Q18. What are cardinalities?

Common relationship cardinalities are:

```text
1 : 1
1 : N
N : 1
M : N
```

Examples:

```text
Person : Passport
1 : 1

Department : Employee
1 : N

Student : Course
M : N
```

---

# 4. Normalization

## Q19. What is Normalization?

> Normalization is the process of organizing data to reduce redundancy and avoid data anomalies.

---

## Q20. Why is normalization needed?

It helps reduce:

```text
Data redundancy
Update anomalies
Insertion anomalies
Deletion anomalies
```

---

## Q21. What is 1NF?

A relation is in **First Normal Form (1NF)** when attributes contain atomic values and repeating groups are eliminated.

Bad:

```text
Student | Phone
Ravi    | 9876, 8765
```

Better:

```text
Student | Phone
Ravi    | 9876
Ravi    | 8765
```

---

## Q22. What is 2NF?

A relation is in **Second Normal Form (2NF)** when:

```text
It is in 1NF
+
No partial dependency on a proper subset of a candidate key
```

Partial dependency is mainly relevant when the candidate key is composite.

---

## Q23. What is 3NF?

A relation is in **Third Normal Form (3NF)** when:

```text
It is in 2NF
+
There is no problematic transitive dependency of non-key attributes on a candidate key
```

---

## Q24. What is BCNF?

> BCNF is a stronger form of 3NF where every determinant is a candidate key.

---

## Q25. What is denormalization?

> Denormalization intentionally introduces some redundancy to improve read performance or simplify queries.

### Important

```text
Normalization
→ Less redundancy
→ Better consistency

Denormalization
→ More controlled redundancy
→ Can improve read performance
```

---

# 5. Functional Dependency

## Q26. What is Functional Dependency?

A functional dependency describes a relationship where one attribute determines another.

Written as:

```text
A → B
```

Meaning:

> If two rows have the same value of `A`, they must have the same value of `B`.

Example:

```text
employee_id → employee_name
```

---

## Q27. What is Partial Dependency?

> Partial dependency occurs when a non-key attribute depends on only part of a composite candidate key.

---

## Q28. What is Transitive Dependency?

Example:

```text
A → B
B → C
```

Therefore:

```text
A → C
```

When a non-key attribute depends on another non-key attribute through the key, this can create a transitive dependency relevant to 3NF.

---

# 6. Transactions

## Q29. What is a Transaction?

> A transaction is a logical unit of work consisting of one or more database operations that should be treated as a unit.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

---

# 7. ACID Properties

## Q30. What are ACID properties?

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

---

## Q31. What is Atomicity?

> Atomicity means a transaction is treated as an all-or-nothing unit.

Example:

```text
Debit succeeds
Credit fails
     ↓
Rollback transaction
```

The partial transaction should not remain committed.

---

## Q32. What is Consistency?

> Consistency means a successful transaction takes the database from one valid state to another valid state while preserving defined integrity constraints.

---

## Q33. What is Isolation?

> Isolation controls how concurrently executing transactions interact with each other's intermediate changes.

---

## Q34. What is Durability?

> Durability means that once a transaction is committed, its changes should survive a subsequent system failure, subject to the DBMS's durability guarantees.

---

# 8. COMMIT and ROLLBACK

## Q35. What is COMMIT?

> `COMMIT` makes the changes of the current transaction permanent.

Example:

```sql
COMMIT;
```

---

## Q36. What is ROLLBACK?

> `ROLLBACK` undoes uncommitted changes in the current transaction.

Example:

```sql
ROLLBACK;
```

---

## Q37. COMMIT vs ROLLBACK?

| COMMIT | ROLLBACK |
|---|---|
| Makes transaction changes permanent | Undoes uncommitted changes |
| Ends successful transaction work | Cancels/undoes current transaction work |

---

# 9. Concurrency Problems

## Q38. What is a Dirty Read?

A dirty read occurs when one transaction reads data written by another transaction that has not yet committed.

```text
T1 → updates data
T2 → reads updated data
T1 → rollback
```

T2 read a value that was never committed.

---

## Q39. What is a Non-Repeatable Read?

A transaction reads the same row twice and gets different values because another committed transaction modified the row between the two reads.

---

## Q40. What is a Phantom Read?

A transaction executes the same range query twice and sees additional or missing rows because another transaction inserted or deleted rows in that range and committed.

---

## Q41. Dirty Read vs Non-Repeatable Read vs Phantom Read

| Problem | What changes? |
|---|---|
| Dirty Read | Uncommitted value is read |
| Non-Repeatable Read | Existing row's value changes |
| Phantom Read | Set of matching rows changes |

---

# 10. Isolation Levels

## Q42. What are common transaction isolation levels?

```text
Read Uncommitted
Read Committed
Repeatable Read
Serializable
```

Some DBMSs also support additional levels such as snapshot-based isolation.

---

## Q43. What is Read Uncommitted?

> It allows the lowest level of isolation and can permit dirty reads.

---

## Q44. What is Read Committed?

> A transaction generally reads only committed data. Dirty reads are prevented, but non-repeatable reads can still occur.

---

## Q45. What is Repeatable Read?

> It provides stronger isolation so that repeated reads of the same rows are protected from certain concurrent changes; exact behavior, especially for phantoms, is DBMS-specific.

---

## Q46. What is Serializable?

> Serializable provides the strongest standard isolation level and aims to produce results equivalent to some serial execution of transactions.

---

# 11. Indexing

## Q47. What is an Index?

> An index is a data structure that helps the DBMS locate rows efficiently for suitable queries.

Example:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

---

## Q48. Advantages of Indexes?

```text
Faster suitable reads
Faster filtering
Can improve joins
Can help sorting
Can help grouping
```

---

## Q49. Disadvantages of Indexes?

```text
Extra storage
Slower INSERT
Slower UPDATE
Slower DELETE
Index maintenance overhead
```

---

## Q50. What is a Composite Index?

> A composite index is an index created on multiple columns.

Example:

```sql
CREATE INDEX idx_emp
ON employees(department_id, salary);
```

---

## Q51. Does the order of columns matter in a composite index?

> Yes. The order matters because the index is organized beginning with the leading column(s).

For:

```text
(department_id, salary)
```

the index is generally more useful for:

```text
department_id
department_id + salary
```

than for:

```text
salary only
```

---

## Q52. What is a Clustered Index?

> In DBMSs that support clustered indexing in this manner, a clustered index determines or closely controls the physical organization of table rows according to the index key.

---

## Q53. What is a Non-Clustered Index?

> A non-clustered index is a separate index structure containing keys and references to the corresponding table data.

---

## Q54. Why doesn't the DBMS always use an index?

Possible reasons:

```text
Low selectivity
Small table
Large percentage of rows requested
Statistics
Cost of table lookups
Query structure
Optimizer cost estimates
```

Important:

```text
Index exists
≠
Index will definitely be used
```

---

# 12. Query Processing

## Q55. What is Query Processing?

> Query processing is the process through which a DBMS parses, analyzes, optimizes, and executes a SQL query.

Conceptually:

```text
SQL Query
   ↓
Parsing
   ↓
Validation
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

## Q56. What is Query Optimization?

> Query optimization is the process of selecting an efficient execution strategy for a query.

---

## Q57. What is an Execution Plan?

> An execution plan describes the operations the DBMS intends to perform to execute a query.

Example:

```text
Index Access
     ↓
Filter
     ↓
Join
     ↓
Result
```

---

## Q58. What is a Table Scan?

> A table scan reads table rows to find rows satisfying the query conditions.

For a large table, this can be expensive when only a small number of rows are needed.

---

## Q59. What is a Query Optimizer?

> A query optimizer evaluates possible execution strategies and chooses an execution plan based on estimated cost and other factors.

---

## Q60. What are common Join Algorithms?

```text
Nested Loop Join
Hash Join
Merge Join
```

---

# 13. Recovery

## Q61. What is Database Recovery?

> Database recovery is the process of restoring the database to a consistent state after a failure.

---

## Q62. What is UNDO?

> UNDO removes the effects of changes that should not be preserved, such as changes from a failed or rolled-back transaction.

---

## Q63. What is REDO?

> REDO reapplies changes that should be preserved, typically committed changes that were not fully reflected in persistent storage after a failure.

---

## Q64. What is a Database Log?

> A database log records transaction-related changes and helps the DBMS perform recovery after failures.

---

# 14. Database Security

## Q65. What is Database Security?

> Database security protects database data against unauthorized access, modification, disclosure, or misuse.

---

## Q66. Authentication vs Authorization?

### Authentication

```text
Who are you?
```

### Authorization

```text
What are you allowed to do?
```

### Interview Answer

> Authentication verifies the identity of a user, while authorization determines what that authenticated user is permitted to access or perform.

---

## Q67. What is GRANT?

`GRANT` gives privileges to a user or role.

```sql
GRANT SELECT
ON employees
TO analyst;
```

---

## Q68. What is REVOKE?

`REVOKE` removes privileges.

```sql
REVOKE SELECT
ON employees
FROM analyst;
```

---

## Q69. What is SQL Injection?

> SQL injection is a vulnerability in which untrusted input is able to alter the intended SQL statement.

Common defense:

```text
Parameterized queries
Prepared statements
Proper input handling
Least-privilege database accounts
```

---

# 15. Important Scenario Questions

## Q70. A table has 10 million rows. You need one employee using employee_id. What would you consider?

Query:

```sql
SELECT *
FROM employees
WHERE employee_id = 5000000;
```

### Answer

Consider an index on `employee_id`, especially if it is highly selective or unique.

```sql
CREATE INDEX idx_employee_id
ON employees(employee_id);
```

The optimizer will decide whether using it is cheaper than other available plans.

---

## Q71. Why might an index not improve a query?

Possible reasons:

```text
The query returns many rows
Column has low selectivity
Table is small
Statistics favor another plan
Index does not match the query
Additional table lookups are expensive
```

---

## Q72. A table has too many indexes. What problem can occur?

> Reads may benefit from indexes, but writes can become more expensive because indexes must be maintained during `INSERT`, `UPDATE`, and `DELETE`.

---

## Q73. You have an index:

```sql
CREATE INDEX idx_emp
ON employees(department_id, salary);
```

Which query is more naturally supported?

```sql
WHERE department_id = 10
```

or:

```sql
WHERE salary > 50000
```

### Answer

```sql
WHERE department_id = 10
```

because `department_id` is the leading column of the composite index.

---

## Q74. Two transactions access the same data at the same time. What problem can occur?

Potential concurrency problems include:

```text
Dirty reads
Non-repeatable reads
Phantom reads
Lost updates
```

The exact problems depend on the transaction operations and isolation/concurrency-control mechanisms.

---

## Q75. A transaction transfers money between two accounts. What ACID properties are important?

All four:

```text
Atomicity
Consistency
Isolation
Durability
```

Especially:

```text
Atomicity
→ Debit and credit should succeed together or be rolled back.

Consistency
→ Database rules must remain valid.

Isolation
→ Concurrent transactions should not produce incorrect intermediate effects.

Durability
→ Once committed, the transfer should survive failures.
```

---

# 16. Frequently Asked Comparisons

## Q76. DELETE vs TRUNCATE vs DROP?

| DELETE | TRUNCATE | DROP |
|---|---|---|
| Removes rows | Removes all rows in supported systems | Removes the table/object |
| Can use `WHERE` | Normally no `WHERE` | Removes table definition |
| DML statement in common SQL systems | Often categorized separately depending on DBMS | DDL |
| Table structure remains | Table structure remains | Table is removed |
| Transaction behavior is DBMS-specific | Transaction behavior is DBMS-specific | Transaction behavior is DBMS-specific |

---

## Q77. WHERE vs HAVING?

| WHERE | HAVING |
|---|---|
| Filters rows before grouping | Filters groups after aggregation |
| Used with row-level conditions | Commonly used with aggregate conditions |

Example:

```sql
SELECT department_id, COUNT(*)
FROM employees
WHERE salary > 50000
GROUP BY department_id
HAVING COUNT(*) > 5;
```

---

## Q78. Primary Key vs Unique Key?

> A primary key uniquely identifies rows and cannot be `NULL`. A `UNIQUE` constraint enforces uniqueness, while its handling of `NULL` values depends on the DBMS.

---

## Q79. DBMS vs RDBMS?

```text
DBMS
→ General database management

RDBMS
→ Relational database management
→ Tables
→ Relationships
→ Relational constraints
```

---

## Q80. Normalization vs Denormalization?

```text
Normalization
→ Reduce redundancy
→ Improve consistency

Denormalization
→ Intentionally introduce redundancy
→ Can improve read performance
```

---

## Q81. DELETE vs ROLLBACK?

> `DELETE` is a SQL operation that removes rows. `ROLLBACK` is a transaction control operation that undoes uncommitted changes according to the DBMS transaction semantics.

---

## Q82. COMMIT vs ROLLBACK?

```text
COMMIT
→ Make transaction changes permanent

ROLLBACK
→ Undo uncommitted transaction changes
```

---

## Q83. Authentication vs Authorization?

```text
Authentication
→ Who are you?

Authorization
→ What can you do?
```

---

## Q84. Clustered vs Non-Clustered Index?

```text
Clustered
→ Physical row organization is associated with index order
→ DBMS-specific implementation

Non-Clustered
→ Separate index structure
→ References table data
```

---

# 17. Tricky Interview Questions

## Q85. Can a table have multiple primary keys?

> No. A table can have only one primary key constraint, although that primary key can contain multiple columns.

---

## Q86. Can a primary key contain NULL?

> No.

---

## Q87. Can a foreign key contain NULL?

> Yes, unless the column is defined with a restriction such as `NOT NULL`.

---

## Q88. Can a foreign key have duplicate values?

> Yes. Multiple child rows can reference the same parent row.

---

## Q89. Can a table have multiple candidate keys?

> Yes. A table can have multiple candidate keys, and one of them is chosen as the primary key.

---

## Q90. Can a composite primary key contain multiple columns?

> Yes.

Example:

```sql
PRIMARY KEY (student_id, course_id)
```

---

## Q91. Is an index always faster?

> No. An index can improve suitable read queries, but it also has storage and maintenance costs, and the optimizer may choose a scan instead.

---

## Q92. Does normalization always improve performance?

> No. Normalization reduces redundancy and improves data integrity, but highly normalized schemas can require more joins. In some workloads, controlled denormalization can improve read performance.

---

## Q93. Is `NULL` equal to `0`?

> No.

`NULL` represents a missing, unknown, or inapplicable value, while `0` is an actual numeric value.

---

## Q94. Is `NULL = NULL` true?

> In standard SQL three-valued logic, `NULL = NULL` does not evaluate to `TRUE`; it evaluates to `UNKNOWN`.

Use:

```sql
IS NULL
```

instead.

Example:

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

---

## Q95. Why are indexes not created on every column?

> Because indexes consume storage and increase the cost of data modifications. An index should be created when it provides enough benefit for the workload.

---

# 18. Highest-Priority Questions

If you have **very little time before an interview**, prepare these first:

```text
⭐⭐⭐⭐⭐

1. What is DBMS?
2. DBMS vs RDBMS
3. Primary key
4. Foreign key
5. Candidate key
6. Super key
7. Composite key
8. ER model
9. Types of relationships
10. Normalization
11. 1NF
12. 2NF
13. 3NF
14. BCNF
15. Functional dependency
16. Partial dependency
17. Transitive dependency
18. Transaction
19. ACID properties
20. COMMIT vs ROLLBACK
21. Dirty read
22. Non-repeatable read
23. Phantom read
24. Isolation levels
25. Index
26. Clustered vs non-clustered index
27. Composite index
28. Why indexes improve performance
29. Why an index may not be used
30. Query optimization
31. Execution plan
32. Query optimizer
33. Join algorithms
34. Database recovery
35. UNDO vs REDO
36. Authentication vs authorization
37. GRANT vs REVOKE
38. SQL injection
39. DELETE vs TRUNCATE vs DROP
40. WHERE vs HAVING
```

---

# 19. Final DBMS Revision Sheet

```text
DBMS
→ Manages databases

RDBMS
→ Stores relational data in tables

PRIMARY KEY
→ Unique + NOT NULL
→ Identifies a row

FOREIGN KEY
→ References a key in another table
→ Establishes relationship

CANDIDATE KEY
→ Minimal unique identifier

SUPER KEY
→ Any unique identifier, may contain extra attributes

COMPOSITE KEY
→ Multiple columns

NORMALIZATION
→ Reduce redundancy and anomalies

1NF
→ Atomic values

2NF
→ 1NF + No partial dependency

3NF
→ 2NF + No problematic transitive dependency

BCNF
→ Every determinant is a candidate key

FUNCTIONAL DEPENDENCY
→ A → B

TRANSACTION
→ Logical unit of work

ACID
→ Atomicity
→ Consistency
→ Isolation
→ Durability

COMMIT
→ Save transaction changes

ROLLBACK
→ Undo uncommitted changes

DIRTY READ
→ Read uncommitted data

NON-REPEATABLE READ
→ Same row gives different committed values

PHANTOM READ
→ Matching row set changes

INDEX
→ Faster suitable data access

COMPOSITE INDEX
→ Multiple columns
→ Column order matters

CLUSTERED
→ Physical organization associated with index order
→ DBMS-specific

NON-CLUSTERED
→ Separate index structure

QUERY OPTIMIZER
→ Chooses execution strategy

EXECUTION PLAN
→ Describes query execution

TABLE SCAN
→ Reads table rows

RECOVERY
→ Restore consistency after failure

UNDO
→ Remove unwanted changes

REDO
→ Reapply required changes

AUTHENTICATION
→ Who are you?

AUTHORIZATION
→ What can you do?

GRANT
→ Give permission

REVOKE
→ Remove permission

SQL INJECTION
→ Untrusted input alters SQL
→ Use parameterized queries
```

# 20. What to Prepare Before a Placement Interview

Focus your preparation in this order:

```text
1. SQL
2. OOP
3. DBMS
4. Data Structures & Algorithms
5. Operating Systems
6. Computer Networks
```

For DBMS specifically:

```text
★★★★★
Keys
Normalization
Transactions + ACID
Concurrency
Indexes
Query Processing

★★★★
DBMS Architecture
ER Model
Relationships
Recovery
Security

★★★
Detailed internal implementation
Advanced storage concepts
Advanced recovery algorithms
```

> **If you thoroughly prepare this file and understand the concepts behind the answers, it can serve as your main DBMS interview revision file.** For deeper preparation, use the individual topic files to strengthen concepts rather than trying to memorize every detail.