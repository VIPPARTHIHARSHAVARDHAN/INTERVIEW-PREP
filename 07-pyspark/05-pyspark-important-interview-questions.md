# PySpark Important Interview Questions

> **Placement-focused revision file:** If you are short on time, prepare this file along with the previous PySpark files. These questions cover the main concepts commonly expected from a fresher/Data Engineer candidate.

---

# 1. PySpark Basics

### 1. What is Apache Spark?

Apache Spark is a distributed data-processing framework used to process large datasets across multiple machines.

---

### 2. What is PySpark?

PySpark is the Python API for Apache Spark. It allows us to use Spark's distributed processing capabilities using Python.

---

### 3. Why is PySpark used?

PySpark is mainly used for:

```text
Large-scale data processing
ETL
Data transformation
Data analysis
Distributed computing
```

---

### 4. Spark vs PySpark?

```text
Spark
→ Distributed data-processing framework

PySpark
→ Python API used to interact with Spark
```

---

### 5. What is SparkSession?

`SparkSession` is the main entry point for working with Spark DataFrames and Spark SQL.

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Example") \
    .getOrCreate()
```

---

# 2. Spark Architecture

### 6. What is a Driver?

The Driver is the main process that coordinates a Spark application.

It:

```text
Creates SparkSession
Builds execution plans
Schedules tasks
Coordinates executors
Tracks execution
```

---

### 7. What is an Executor?

An Executor is a process that runs tasks assigned by the Driver.

It:

```text
Executes tasks
Processes data
Can cache data
Returns results
```

---

### 8. Driver vs Executor?

| Driver | Executor |
|---|---|
| Coordinates application | Executes tasks |
| Creates execution plan | Processes data |
| Schedules tasks | Runs tasks |
| Tracks application | Can cache data |

Easy way to remember:

```text
Driver → Coordinates
Executor → Executes
```

---

### 9. What is a Cluster Manager?

A Cluster Manager manages resources required by Spark applications.

Examples:

```text
Standalone
YARN
Kubernetes
```

---

### 10. What are Job, Stage and Task?

```text
Job
→ Triggered by an action

Stage
→ Group of tasks separated by shuffle boundaries

Task
→ Unit of work executed on a partition
```

Hierarchy:

```text
Application
    ↓
   Job
    ↓
  Stage
    ↓
  Task
    ↓
Partition
```

---

# 3. DataFrames and RDDs

### 11. What is a DataFrame?

A DataFrame is a distributed collection of structured data organized into named columns.

It is similar to a table in SQL.

---

### 12. What is an RDD?

RDD stands for **Resilient Distributed Dataset**.

It is a distributed collection of objects that can be processed in parallel.

Important characteristics:

```text
Distributed
Immutable
Fault-tolerant
Parallel processing
```

---

### 13. RDD vs DataFrame?

| RDD | DataFrame |
|---|---|
| Lower-level abstraction | Higher-level abstraction |
| Collection of objects | Structured data |
| Less optimized | Spark can optimize operations |
| More verbose | Easier to use |
| More control | Better for structured data |

### Interview answer:

> DataFrames are generally preferred for structured data because they provide a higher-level API and allow Spark to optimize the execution plan.

---

### 14. Why are DataFrames preferred over RDDs?

Because DataFrames provide:

```text
Schema
Higher-level API
SQL support
Query optimization
Better readability
Built-in functions
```

---

### 15. What is a DataFrame schema?

A schema defines the structure of a DataFrame, including:

```text
Column names
Data types
Structure
```

Check it using:

```python
df.printSchema()
```

---

### 16. How do you create a DataFrame?

```python
data = [
    (1, "Harsha", 22),
    (2, "Rahul", 23)
]

columns = ["id", "name", "age"]

df = spark.createDataFrame(data, columns)
```

---

# 4. Transformations and Actions

### 17. What is lazy evaluation?

Spark does not immediately execute transformations.

Instead, Spark builds an execution plan and executes it when an action is called.

```text
Transformation
      ↓
Execution Plan
      ↓
Action
      ↓
Execution
```

---

### 18. What is a transformation?

A transformation creates a new DataFrame/RDD from an existing one.

Examples:

```text
filter()
select()
withColumn()
drop()
```

---

### 19. What is an action?

An action triggers Spark execution and produces a result or output.

Examples:

```text
show()
count()
collect()
first()
take()
write
```

---

### 20. Transformation vs Action?

| Transformation | Action |
|---|---|
| Creates new dataset/DataFrame | Triggers execution |
| Lazily evaluated | Executes computation |
| `filter()` | `count()` |
| `select()` | `show()` |
| `withColumn()` | `collect()` |

---

# 5. DataFrame Operations

### 21. How do you select columns?

```python
df.select("name", "salary").show()
```

---

### 22. How do you filter rows?

```python
df.filter(df.salary > 50000).show()
```

You can also use:

```python
df.where(df.salary > 50000).show()
```

---

### 23. filter() vs where()?

For DataFrames, `filter()` and `where()` are commonly used interchangeably.

```python
df.filter(df.salary > 50000)
```

and:

```python
df.where(df.salary > 50000)
```

perform the same type of filtering.

---

### 24. How do you add a new column?

Use `withColumn()`.

```python
df = df.withColumn(
    "annual_salary",
    df.salary * 12
)
```

---

### 25. How do you rename a column?

```python
df = df.withColumnRenamed(
    "salary",
    "monthly_salary"
)
```

---

### 26. How do you remove a column?

```python
df = df.drop("salary")
```

---

### 27. distinct() vs dropDuplicates()?

```text
distinct()
→ Removes duplicate rows

dropDuplicates()
→ Removes duplicates based on specified columns
```

Example:

```python
df.dropDuplicates(["email"])
```

---

# 6. Aggregations

### 28. What is groupBy()?

`groupBy()` groups rows based on one or more columns.

```python
df.groupBy("department").count().show()
```

---

### 29. What are common aggregation functions?

```text
count()
sum()
avg()
min()
max()
```

Example:

```python
from pyspark.sql.functions import avg

df.groupBy("department").agg(
    avg("salary").alias("avg_salary")
).show()
```

---

### 30. How do you find average salary by department?

```python
from pyspark.sql.functions import avg

result = df.groupBy("department").agg(
    avg("salary").alias("avg_salary")
)
```

---

### 31. How do you find maximum salary by department?

```python
from pyspark.sql.functions import max

result = df.groupBy("department").agg(
    max("salary").alias("max_salary")
)
```

---

# 7. Joins

### 32. What is a join?

A join combines rows from two DataFrames based on a related column or condition.

```python
result = df1.join(
    df2,
    "id",
    "inner"
)
```

---

### 33. What are the important join types?

```text
Inner
Left
Right
Full
Left Semi
Left Anti
```

---

### 34. Explain Inner Join.

Returns rows that have matching values in both DataFrames.

```python
df1.join(df2, "id", "inner")
```

---

### 35. Explain Left Join.

Returns:

```text
All rows from left DataFrame
+
Matching rows from right DataFrame
```

```python
df1.join(df2, "id", "left")
```

---

### 36. Explain Full Outer Join.

Returns all rows from both DataFrames.

```python
df1.join(df2, "id", "full")
```

Non-matching columns contain `NULL`.

---

### 37. What is a Left Semi Join?

A left semi join returns rows from the left DataFrame for which a matching row exists in the right DataFrame.

```python
df1.join(
    df2,
    "id",
    "left_semi"
)
```

Only columns from the left DataFrame are returned.

---

### 38. What is a Left Anti Join?

A left anti join returns rows from the left DataFrame where no matching row exists in the right DataFrame.

```python
df1.join(
    df2,
    "id",
    "left_anti"
)
```

It is useful for finding:

```text
Unmatched records
Missing records
Records without reference data
```

---

### 39. Left Semi vs Left Anti?

```text
Left Semi
→ Left rows WITH a match

Left Anti
→ Left rows WITHOUT a match
```

---

# 8. Window Functions

### 40. What is a Window Function?

A window function performs calculations across related rows while retaining the individual rows.

Unlike `groupBy()`, it does not collapse the rows into one row per group.

---

### 41. What is partitionBy() in a Window?

`partitionBy()` divides rows into logical groups for the window calculation.

```python
window = Window.partitionBy("department")
```

---

### 42. What is orderBy() in a Window?

`orderBy()` determines the order in which rows are considered within each window.

```python
window = Window \
    .partitionBy("department") \
    .orderBy("salary")
```

---

### 43. row_number() vs rank() vs dense_rank()?

For:

```text
100
90
90
80
```

Results:

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

| Function | Ties | Gaps |
|---|---|---|
| `row_number()` | Unique number | No |
| `rank()` | Same rank | Yes |
| `dense_rank()` | Same rank | No |

---

### 44. What is lag()?

`lag()` accesses a value from a previous row.

```python
lag("salary", 1).over(window)
```

Easy memory trick:

```text
lag → previous
```

---

### 45. What is lead()?

`lead()` accesses a value from a following row.

```python
lead("salary", 1).over(window)
```

Easy memory trick:

```text
lead → next
```

---

### 46. How do you find the top 3 employees in each department?

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number, desc

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn <= 3")
```

---

### 47. groupBy() vs Window Function?

```text
groupBy()
→ Groups rows and reduces them

Window Function
→ Calculates across related rows while retaining individual rows
```

---

# 9. Spark SQL

### 48. What is Spark SQL?

Spark SQL is Spark's module for processing structured data using SQL.

---

### 49. How do you create a temporary view?

```python
df.createOrReplaceTempView("employees")
```

---

### 50. How do you execute SQL in PySpark?

```python
result = spark.sql("""
    SELECT *
    FROM employees
    WHERE salary > 50000
""")
```

---

### 51. DataFrame API vs Spark SQL?

Both can perform many of the same structured-data operations.

```text
DataFrame API
→ Programmatic transformations

Spark SQL
→ SQL-based transformations
```

Use whichever is clearer for the task.

---

# 10. Partitions and Shuffle

### 52. What is a Partition?

A partition is a logical chunk of data that Spark can process in parallel.

```text
Dataset
 ↓
P1 | P2 | P3 | P4
 ↓    ↓    ↓    ↓
Tasks
```

---

### 53. Why are partitions important?

Partitions enable:

```text
Parallel processing
Distributed execution
Better resource utilization
```

---

### 54. What is Shuffle?

Shuffle is the redistribution of data across partitions.

It commonly occurs during operations such as:

```text
groupBy()
join()
distinct()
orderBy()
repartition()
```

---

### 55. Why is Shuffle expensive?

Shuffle may involve:

```text
Network I/O
Disk I/O
Data redistribution
Serialization
Sorting
Memory usage
```

Therefore, unnecessary shuffle should generally be avoided.

---

### 56. What is a Narrow Transformation?

A narrow transformation does not require a full redistribution of data between partitions.

Examples:

```text
filter()
select()
withColumn()
```

---

### 57. What is a Wide Transformation?

A wide transformation requires data redistribution between partitions.

Examples:

```text
groupBy()
join()
distinct()
orderBy()
```

---

# 11. repartition() and coalesce()

### 58. What is repartition()?

`repartition()` changes the number of partitions and generally involves a shuffle.

```python
df = df.repartition(10)
```

It can increase or decrease the number of partitions.

---

### 59. What is coalesce()?

`coalesce()` is generally used to reduce the number of partitions.

```python
df = df.coalesce(5)
```

It is usually cheaper than `repartition()` when simply reducing partitions.

---

### 60. repartition() vs coalesce()?

| repartition() | coalesce() |
|---|---|
| Can increase/decrease partitions | Mainly reduces partitions |
| Generally causes shuffle | Usually avoids full shuffle |
| More expensive | Usually cheaper |
| Redistributes data | Combines partitions |

Easy memory trick:

```text
repartition()
→ Redistribute

coalesce()
→ Reduce
```

---

# 12. Data Skew

### 61. What is Data Skew?

Data skew occurs when data is distributed unevenly across partitions.

Example:

```text
Partition 1 → 10 MB
Partition 2 → 12 MB
Partition 3 → 11 MB
Partition 4 → 800 MB
```

One task becomes much slower than the others.

---

### 62. Why is Data Skew a problem?

It can cause:

```text
Slow tasks
Long-running stages
Poor cluster utilization
Memory problems
```

---

### 63. How can you handle Data Skew?

Basic approaches include:

```text
Better partitioning
Filter unnecessary data
Broadcast small tables
Salting for highly skewed joins
```

---

# 13. Broadcast Join

### 64. What is a Broadcast Join?

A broadcast join copies a small DataFrame to executors so that Spark can join it with a large DataFrame without requiring a large shuffle of the small side.

```python
from pyspark.sql.functions import broadcast

result = large_df.join(
    broadcast(small_df),
    "id"
)
```

---

### 65. When should you use a Broadcast Join?

Use it when:

```text
One DataFrame is relatively small
+
It can safely fit in executor memory
```

Example:

```text
Large employee dataset
+
Small department lookup
```

---

# 14. Caching and Performance

### 66. What is Caching?

Caching stores computed data so it can potentially be reused without recomputing the entire lineage.

```python
df.cache()
```

---

### 67. When should you cache a DataFrame?

Cache when the same DataFrame is reused multiple times.

Avoid caching everything because it consumes cluster resources.

---

### 68. cache() vs persist()?

```text
cache()
→ Convenient default caching

persist()
→ Allows choosing a storage level
```

Example:

```python
df.persist()
```

---

### 69. Why should you avoid collect() on large data?

`collect()` brings all rows to the Driver.

```python
df.collect()
```

For a very large DataFrame, this can cause driver memory problems or an out-of-memory error.

Prefer:

```python
df.show()
```

when you only need to inspect the data.

---

### 70. How can you improve PySpark performance?

Important approaches:

```text
1. Filter unnecessary data early.

2. Select only required columns.

3. Avoid unnecessary shuffles.

4. Use broadcast joins when appropriate.

5. Choose appropriate partitioning.

6. Handle data skew.

7. Cache reused DataFrames.

8. Avoid collect() on large datasets.

9. Avoid unnecessary transformations.
```

---

# 15. Scenario-Based Questions

### 71. You have a large employee DataFrame and a small department DataFrame. How would you optimize the join?

Use a broadcast join if the department DataFrame is small enough to safely fit in executor memory.

```python
from pyspark.sql.functions import broadcast

result = employees.join(
    broadcast(departments),
    "dept_id"
)
```

---

### 72. You need the highest-paid employee from each department. How would you solve it?

Use a window function:

```python
window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn = 1")
```

---

### 73. You need the top 3 employees from every department. What would you use?

Use:

```text
Window
+
partitionBy()
+
orderBy()
+
row_number() / rank()
```

Example:

```python
result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn <= 3")
```

---

### 74. A PySpark job is running slowly because one task takes much longer than the others. What could be the reason?

A likely reason is **data skew**.

One or more partitions may contain much more data than the others.

---

### 75. A DataFrame is used several times in a pipeline. What can you do?

Consider caching the DataFrame:

```python
df.cache()
```

if the cost of recomputation is significant and caching fits available resources.

---

### 76. You only need to reduce the number of partitions. Should you use repartition() or coalesce()?

Usually:

```python
df.coalesce(n)
```

is preferred when simply reducing partitions because it generally avoids a full shuffle.

---

### 77. Your application has a huge amount of data going through a join. What should you investigate?

Check:

```text
Join strategy
Data size
Data skew
Shuffle
Partitioning
Whether one side can be broadcast
```

---

### 78. You need to find records that exist in one DataFrame but not another. Which join is useful?

Use a **left anti join**.

```python
result = df1.join(
    df2,
    "id",
    "left_anti"
)
```

---

### 79. You need records from the left DataFrame that have a match in the right DataFrame, but you don't need columns from the right. Which join is useful?

Use a **left semi join**.

```python
result = df1.join(
    df2,
    "id",
    "left_semi"
)
```

---

# 16. Coding Questions to Practice

## 80. Filter employees with salary greater than 50,000.

```python
df.filter(df.salary > 50000).show()
```

---

## 81. Select employee name and salary.

```python
df.select(
    "name",
    "salary"
).show()
```

---

## 82. Add annual salary.

```python
df.withColumn(
    "annual_salary",
    df.salary * 12
).show()
```

---

## 83. Find average salary by department.

```python
from pyspark.sql.functions import avg

df.groupBy("department").agg(
    avg("salary").alias("avg_salary")
).show()
```

---

## 84. Find maximum salary by department.

```python
from pyspark.sql.functions import max

df.groupBy("department").agg(
    max("salary").alias("max_salary")
).show()
```

---

## 85. Find the highest-paid employee from each department.

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number, desc

window = Window \
    .partitionBy("department") \
    .orderBy(desc("salary"))

result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn = 1")
```

---

## 86. Find the top 3 employees from each department.

```python
result = df.withColumn(
    "rn",
    row_number().over(window)
).filter("rn <= 3")
```

---

## 87. Find the previous employee salary.

```python
from pyspark.sql.functions import lag

result = df.withColumn(
    "previous_salary",
    lag("salary", 1).over(window)
)
```

---

## 88. Join two DataFrames.

```python
result = employees.join(
    departments,
    "dept_id",
    "inner"
)
```

---

## 89. Find unmatched records.

```python
result = employees.join(
    departments,
    "dept_id",
    "left_anti"
)
```

---

# 17. ⭐ Top 25 Questions to Revise Before Interview

```text
1. What is Spark?

2. What is PySpark?

3. What is SparkSession?

4. Driver vs Executor?

5. What are Job, Stage and Task?

6. What is a DataFrame?

7. What is an RDD?

8. RDD vs DataFrame?

9. What is lazy evaluation?

10. Transformation vs Action?

11. What is groupBy()?

12. What are the different types of joins?

13. Inner Join vs Left Join?

14. Left Semi vs Left Anti Join?

15. What is a Window Function?

16. row_number() vs rank() vs dense_rank()?

17. lag() vs lead()?

18. How do you find top N records per group?

19. What is Spark SQL?

20. DataFrame API vs Spark SQL?

21. What is a partition?

22. What is shuffle?

23. repartition() vs coalesce()?

24. What is a broadcast join?

25. How do you optimize a PySpark job?
```

---

# 18. ⭐ Final Quick Revision

```text
PySpark
→ Python API for Spark

Spark
→ Distributed data-processing framework

Driver
→ Coordinates

Executor
→ Executes

Job
→ Triggered by action

Stage
→ Group of tasks

Task
→ Unit of work

DataFrame
→ Distributed structured data

RDD
→ Distributed collection of objects

Transformation
→ Creates new dataset/DataFrame

Action
→ Triggers execution

Lazy Evaluation
→ Execution is delayed until an action

groupBy()
→ Groups and reduces rows

Window
→ Calculates across related rows while retaining rows

row_number()
→ Unique sequence

rank()
→ Ties + gaps

dense_rank()
→ Ties + no gaps

lag()
→ Previous row

lead()
→ Next row

Partition
→ Chunk of data

Shuffle
→ Redistributes data

Narrow Transformation
→ No full redistribution

Wide Transformation
→ Requires redistribution

repartition()
→ Redistributes / changes partitions

coalesce()
→ Reduces partitions

Data Skew
→ Uneven data distribution

Broadcast Join
→ Replicate small table to executors

cache()
→ Reuse computed data

collect()
→ Brings all data to Driver

Spark SQL
→ SQL interface for Spark
```

---

# 19. Final Preparation Strategy

For a **fresher/Data Engineer interview**, prioritize:

```text
⭐⭐⭐⭐⭐
DataFrames
Transformations & Actions
Joins
Aggregations
Window Functions
Partitions
Shuffle
Broadcast Joins
Basic Performance Optimization

⭐⭐⭐⭐
Spark Architecture
RDD vs DataFrame
Spark SQL
Data Skew
Caching

⭐⭐⭐
Advanced Spark Internals
Advanced Optimization
Advanced RDD Programming
```

> **You do not need to memorize every answer word-for-word. Understand the concept, remember the important PySpark syntax, and practice writing small DataFrame queries. For a fresher interview, this level of PySpark preparation is sufficient unless the job description specifically asks for advanced Spark expertise.**