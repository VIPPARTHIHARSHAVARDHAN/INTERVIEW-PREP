# Window Functions and Spark SQL

## 1. What are Window Functions?

A **window function** performs a calculation across a group of related rows while still keeping the individual rows in the result.

Unlike `groupBy()`, a window function **does not collapse multiple rows into one row**.

Example:

```text
groupBy()
→ Multiple rows become one row per group

Window Function
→ Original rows are retained
→ Calculation is performed across related rows
```

---

# 2. Why Use Window Functions?

Window functions are commonly used for:

```text
Ranking
Top N records
Finding previous/next records
Running totals
Comparing rows
Finding highest salary per department
Finding second highest salary
```

---

# 3. Creating a Window

Import:

```python
from pyspark.sql.window import Window
```

Example:

```python
window = Window.partitionBy("department")
```

A window can be defined using:

```text
partitionBy()
orderBy()
```

---

# 4. partitionBy()

`partitionBy()` divides rows into logical groups for the window calculation.

Example:

```python
window = Window.partitionBy("department")
```

If the data contains:

```text
IT
IT
HR
HR
Finance
```

the calculation is performed separately for each department.

Conceptually:

```text
IT
 ├── Employee 1
 └── Employee 2

HR
 ├── Employee 3
 └── Employee 4

Finance
 └── Employee 5
```

---

# 5. orderBy()

`orderBy()` defines the order in which rows should be considered inside the window.

Example:

```python
window = Window \
    .partitionBy("department") \
    .orderBy("salary")
```

Descending:

```python
from pyspark.sql.functions import desc

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))
```

---

# 6. partitionBy() vs orderBy()

```text
partitionBy()
→ Defines groups

orderBy()
→ Defines order within those groups
```

Example:

```python
window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))
```

Means:

```text
Group employees by department
        ↓
Sort employees by salary
        ↓
Apply window function
```

---

# 7. row_number()

`row_number()` assigns a unique sequential number to each row within a window.

Example:

```python
from pyspark.sql.functions import row_number

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df.withColumn(
    "row_number",
    row_number().over(window)
)

result.show()
```

Example result:

```text
+------+----------+------+----------+
| name |department|salary|row_number|
+------+----------+------+----------+
| A    |IT        |90000 |1         |
| B    |IT        |80000 |2         |
| C    |HR        |70000 |1         |
| D    |HR        |60000 |2         |
+------+----------+------+----------+
```

The numbering restarts for every department.

---

# 8. rank()

`rank()` assigns ranks while giving the same rank to tied values.

Example salaries:

```text
90000
80000
80000
70000
```

Ranks:

```text
90000 → 1
80000 → 2
80000 → 2
70000 → 4
```

Notice that rank `3` is skipped.

Example:

```python
from pyspark.sql.functions import rank

result = df.withColumn(
    "rank",
    rank().over(window)
)
```

---

# 9. dense_rank()

`dense_rank()` also gives the same rank to tied values, but it does not skip the next rank.

Example:

```text
90000 → 1
80000 → 2
80000 → 2
70000 → 3
```

Example:

```python
from pyspark.sql.functions import dense_rank

result = df.withColumn(
    "dense_rank",
    dense_rank().over(window)
)
```

---

# 10. row_number vs rank vs dense_rank

| Function | Handles ties | Skips rank? |
|---|---|---|
| `row_number()` | No, gives unique numbers | No |
| `rank()` | Yes | Yes |
| `dense_rank()` | Yes | No |

### Example

For:

```text
100
90
90
80
```

```text
row_number:
1
2
3
4

rank:
1
2
2
4

dense_rank:
1
2
2
3
```

This is a **very common interview question**.

---

# 11. Top N Records Per Group

One of the most common uses of window functions is finding the top N records within each group.

Example: Find the highest-paid employee in each department.

```python
from pyspark.sql.functions import row_number, desc
from pyspark.sql.window import Window

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn = 1")
```

For top 3:

```python
result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn <= 3")
```

---

# 12. lag()

`lag()` accesses a value from a previous row.

Example:

```python
from pyspark.sql.functions import lag

window = Window \
    .partitionBy("department") \
    .orderBy("salary")

result = df.withColumn(
    "previous_salary",
    lag("salary", 1).over(window)
)
```

Conceptually:

```text
Current Row
    ↓
Look at previous row
```

Example:

```text
salary    previous_salary
50000     NULL
60000     50000
70000     60000
```

---

# 13. lead()

`lead()` accesses a value from a following row.

```python
from pyspark.sql.functions import lead

result = df.withColumn(
    "next_salary",
    lead("salary", 1).over(window)
)
```

Example:

```text
salary    next_salary
50000     60000
60000     70000
70000     NULL
```

---

# 14. lag() vs lead()

```text
lag()
→ Previous row

lead()
→ Next row
```

Easy memory trick:

```text
LAG  → Look backward
LEAD → Look forward
```

---

# 15. Running Total

Window functions can calculate a running total.

Example:

```python
from pyspark.sql.functions import sum

window = Window \
    .partitionBy("department") \
    .orderBy("salary") \
    .rowsBetween(
        Window.unboundedPreceding,
        Window.currentRow
    )

result = df.withColumn(
    "running_total",
    sum("salary").over(window)
)
```

Conceptually:

```text
50000
50000 + 60000
50000 + 60000 + 70000
```

---

# 16. rowsBetween()

`rowsBetween()` defines which rows should be included in the window frame.

Example:

```python
.rowsBetween(
    Window.unboundedPreceding,
    Window.currentRow
)
```

Means:

```text
Start from the first row
        ↓
Continue up to current row
```

This is commonly used for running totals.

---

# 17. Common Window Functions

The important ones for interviews are:

```text
row_number()
rank()
dense_rank()
lag()
lead()
sum()
avg()
min()
max()
count()
```

---

# 18. Window Aggregations

Aggregate functions can also be used with windows.

Example:

```python
from pyspark.sql.functions import avg

window = Window.partitionBy("department")

result = df.withColumn(
    "department_avg_salary",
    avg("salary").over(window)
)
```

Unlike `groupBy()`, each employee row is retained.

Example:

```text
Employee    Salary    Department Avg
A           50000     60000
B           70000     60000
C           60000     60000
```

---

# 19. groupBy() vs Window Function

### groupBy()

```python
df.groupBy("department").agg(
    avg("salary")
)
```

Result:

```text
department    avg_salary
IT            65000
HR            60000
```

Rows are grouped into fewer rows.

### Window

```python
window = Window.partitionBy("department")

df.withColumn(
    "avg_salary",
    avg("salary").over(window)
)
```

Result:

```text
name    department    salary    avg_salary
A       IT            60000     65000
B       IT            70000     65000
C       HR            60000     60000
```

### Interview Answer

> `groupBy()` reduces rows by grouping them, while a window function performs calculations across related rows while retaining the individual rows.

---

# 20. Spark SQL

**Spark SQL** is Spark's module for working with structured data using SQL.

It allows us to write SQL queries against Spark DataFrames.

---

# 21. Creating a Temporary View

Suppose we have:

```python
df
```

Create a temporary SQL view:

```python
df.createOrReplaceTempView("employees")
```

Now Spark SQL can query it:

```python
result = spark.sql("""
    SELECT *
    FROM employees
""")

result.show()
```

---

# 22. SELECT Using Spark SQL

```python
result = spark.sql("""
    SELECT name, salary
    FROM employees
""")
```

---

# 23. WHERE Using Spark SQL

```python
result = spark.sql("""
    SELECT *
    FROM employees
    WHERE salary > 50000
""")
```

---

# 24. GROUP BY Using Spark SQL

```python
result = spark.sql("""
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
""")
```

---

# 25. JOIN Using Spark SQL

```python
result = spark.sql("""
    SELECT e.name, d.department
    FROM employees e
    JOIN departments d
    ON e.dept_id = d.dept_id
""")
```

---

# 26. Window Function Using Spark SQL

Example:

```python
result = spark.sql("""
    SELECT
        name,
        department,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rn
    FROM employees
""")
```

This is equivalent to creating a `Window` object in the DataFrame API.

---

# 27. DataFrame API vs Spark SQL

### DataFrame API

```python
result = df.filter(
    df.salary > 50000
)
```

### Spark SQL

```python
result = spark.sql("""
    SELECT *
    FROM employees
    WHERE salary > 50000
""")
```

Both can be used to perform structured-data operations in Spark.

---

# 28. When to Use DataFrame API?

DataFrame API is useful when:

```text
Working primarily in Python
Building programmatic transformations
Creating dynamic logic
Writing reusable transformation pipelines
```

---

# 29. When to Use Spark SQL?

Spark SQL is useful when:

```text
You are comfortable with SQL
Working with SQL-heavy transformations
Migrating SQL-based logic
Building queries using temporary views
```

---

# 30. DataFrame API vs Spark SQL — Interview Answer

> Spark SQL and the DataFrame API can express many of the same operations. Spark SQL is convenient for SQL-oriented users, while the DataFrame API is convenient for programmatic transformations in Python. Both are optimized by Spark's SQL engine.

---

# 31. Complete Window Function Example

```python
from pyspark.sql import SparkSession
from pyspark.sql.window import Window
from pyspark.sql.functions import (
    row_number,
    rank,
    dense_rank,
    lag,
    lead,
    desc
)

spark = SparkSession.builder \
    .appName("WindowExample") \
    .getOrCreate()

data = [
    (1, "Harsha", "IT", 90000),
    (2, "Rahul", "IT", 80000),
    (3, "Priya", "IT", 80000),
    (4, "Arjun", "HR", 70000),
    (5, "Sneha", "HR", 60000)
]

columns = ["id", "name", "department", "salary"]

df = spark.createDataFrame(data, columns)

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df \
    .withColumn(
        "row_number",
        row_number().over(window)
    ) \
    .withColumn(
        "rank",
        rank().over(window)
    ) \
    .withColumn(
        "dense_rank",
        dense_rank().over(window)
    )

result.show()
```

---

# 32. Common Interview Questions

```text
1. What is a window function?

2. Why are window functions used?

3. What is partitionBy()?

4. What is orderBy() in a window?

5. What is row_number()?

6. What is rank()?

7. What is dense_rank()?

8. row_number() vs rank() vs dense_rank()?

9. What is lag()?

10. What is lead()?

11. lag() vs lead()?

12. How do you find the top N employees in each department?

13. How do you find the highest salary in each department?

14. How do you find the second-highest salary in each department?

15. How do you calculate a running total?

16. What is rowsBetween()?

17. groupBy() vs window functions?

18. What is Spark SQL?

19. How do you create a temporary view?

20. How do you execute SQL in PySpark?

21. DataFrame API vs Spark SQL?

22. Can window functions be used with aggregate functions?

23. How do you use ROW_NUMBER() in Spark SQL?

24. How do you find duplicate records using window functions?
```

---

# 33. ⭐ Most Important Interview Questions

If you have limited time, prepare these first:

```text
1. What is a window function?

2. partitionBy() vs orderBy()?

3. row_number() vs rank() vs dense_rank()?

4. lag() vs lead()?

5. How do you find top 3 employees from each department?

6. How do you find the second-highest salary from each department?

7. How do you calculate a running total?

8. groupBy() vs window functions?

9. What is Spark SQL?

10. How do you create a temporary view?

11. DataFrame API vs Spark SQL?

12. How do you use window functions in Spark SQL?
```

---

# 34. Quick Revision

```text
WINDOW FUNCTION
→ Calculates across related rows without collapsing them

partitionBy()
→ Defines groups

orderBy()
→ Defines order within groups

row_number()
→ Unique sequential number

rank()
→ Same rank for ties + gaps

dense_rank()
→ Same rank for ties + no gaps

lag()
→ Previous row

lead()
→ Next row

rowsBetween()
→ Defines window frame

RUNNING TOTAL
→ SUM() + Window + rowsBetween()

groupBy()
→ Groups and reduces rows

WINDOW
→ Groups/calculates while retaining rows

SPARK SQL
→ SQL interface for Spark structured data

createOrReplaceTempView()
→ Creates a temporary SQL view

spark.sql()
→ Executes SQL query

DATAFRAME API
→ Programmatic Spark operations

SPARK SQL
→ SQL-based Spark operations
```

---

# 35. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
Window Functions
partitionBy()
orderBy()
row_number()
rank()
dense_rank()
lag()
lead()
Top N per group
groupBy() vs Window
Spark SQL
createOrReplaceTempView()
spark.sql()
DataFrame API vs Spark SQL
```

## ⭐⭐⭐ Good to Know

```text
rowsBetween()
Running totals
Window aggregations
Using window functions in Spark SQL
```

> **For fresher interviews, focus heavily on `row_number()`, `rank()`, `dense_rank()`, `lag()`, `lead()`, top-N-per-group problems, and the difference between `groupBy()` and window functions. You do not need deep Spark SQL internals at this stage.**