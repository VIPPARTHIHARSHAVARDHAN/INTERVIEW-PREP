# PySpark Basics and DataFrames

## 1. What is Apache Spark?

**Apache Spark** is a distributed data-processing framework used to process large amounts of data efficiently across multiple machines.

It supports:

```text
Batch Processing
SQL
Streaming
Machine Learning
Graph Processing
```

Spark can process data in parallel across a cluster.

---

# 2. What is PySpark?

**PySpark** is the Python API for Apache Spark.

It allows us to use Spark's distributed data-processing capabilities using Python.

```text
Python
   ↓
PySpark
   ↓
Apache Spark
   ↓
Distributed Processing
```

### Why use PySpark?

```text
Process large datasets
Distributed processing
Parallel execution
Data transformation
Data analysis
ETL pipelines
```

---

# 3. Spark vs PySpark

| Spark | PySpark |
|---|---|
| Distributed processing framework | Python API for Spark |
| Supports multiple languages | Primarily used with Python |
| Core Spark engine | Interface to use Spark from Python |
| Written mainly in Scala/Java | Python-based API |

Common Spark APIs include:

```text
Scala
Java
Python
R
```

---

# 4. Important Spark Components

The most important components to understand for interviews are:

```text
Driver
Executor
Cluster Manager
Job
Stage
Task
```

---

# 5. Spark Driver

The **Driver** is the main process responsible for coordinating a Spark application.

It:

```text
Creates SparkSession
Builds execution plan
Coordinates execution
Schedules work
Tracks application progress
```

Conceptually:

```text
             Driver
                |
       -------------------
       |        |        |
   Executor  Executor  Executor
```

---

# 6. Spark Executor

An **Executor** is a process that runs tasks assigned by the driver.

Executors:

```text
Execute tasks
Process data
Store cached data
Return results to the driver
```

Conceptually:

```text
Driver
  |
  +---- Executor 1
  |
  +---- Executor 2
  |
  +---- Executor 3
```

---

# 7. Cluster Manager

The **Cluster Manager** manages resources in the cluster.

It helps allocate resources such as:

```text
CPU
Memory
Worker resources
```

Common cluster managers include:

```text
Standalone
YARN
Kubernetes
```

---

# 8. Driver vs Executor

| Driver | Executor |
|---|---|
| Coordinates application | Executes tasks |
| Creates execution plan | Runs assigned tasks |
| Schedules work | Processes data |
| Tracks application | Can cache data |
| Usually one driver per application | Usually multiple executors |

### Easy way to remember

```text
Driver
→ Decides and coordinates

Executor
→ Executes
```

---

# 9. Spark Application

A **Spark application** consists of:

```text
Driver
+
Executors
```

The driver coordinates the application while executors perform distributed computation.

---

# 10. Spark Job

A **job** is created when an **action** is executed.

For example:

```python
df.count()
```

can trigger a Spark job.

Conceptually:

```text
Action
   ↓
Spark Job
```

---

# 11. Spark Stage

A Spark job is divided into one or more **stages**.

Stages are separated by operations that require data to be redistributed across partitions, commonly called **shuffle operations**.

Conceptually:

```text
Job
 ↓
Stage 1
 ↓
Shuffle
 ↓
Stage 2
```

---

# 12. Spark Task

A **task** is a unit of work executed by an executor.

Tasks generally operate on individual partitions.

Conceptually:

```text
Stage
 ↓
Partition 1 → Task
Partition 2 → Task
Partition 3 → Task
```

---

# 13. Job vs Stage vs Task

| Concept | Meaning |
|---|---|
| Job | Triggered by an action |
| Stage | A group of tasks separated by shuffle boundaries |
| Task | Unit of work operating on a partition |

### Easy hierarchy

```text
Application
    ↓
   Job
    ↓
  Stages
    ↓
  Tasks
    ↓
Partitions
```

---

# 14. SparkSession

`SparkSession` is the main entry point for working with Spark DataFrames and Spark SQL in PySpark.

Example:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyApplication") \
    .getOrCreate()
```

Now we can use:

```python
spark
```

to create DataFrames and execute Spark SQL.

---

# 15. Creating a DataFrame

A **DataFrame** is a distributed collection of data organized into named columns.

Example:

```python
data = [
    (1, "Harsha", 22),
    (2, "Rahul", 23),
    (3, "Priya", 21)
]

columns = ["id", "name", "age"]

df = spark.createDataFrame(data, columns)

df.show()
```

Output:

```text
+---+------+---+
| id|  name|age|
+---+------+---+
|  1|Harsha| 22|
|  2| Rahul| 23|
|  3| Priya| 21|
+---+------+---+
```

---

# 16. What is a DataFrame?

A PySpark DataFrame is a distributed, table-like collection of data with named columns and a schema.

It is conceptually similar to a table in SQL.

Example:

```text
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 1  | Harsha| 22  |
| 2  | Rahul | 23  |
| 3  | Priya | 21  |
+----+-------+-----+
```

---

# 17. DataFrame Schema

A DataFrame has a **schema** that describes its columns and data types.

Example:

```python
df.printSchema()
```

Possible output:

```text
root
 |-- id: long
 |-- name: string
 |-- age: long
```

The schema tells Spark:

```text
Column Name
Data Type
Structure
```

---

# 18. Common PySpark Data Types

Important data types include:

```text
StringType
IntegerType
LongType
DoubleType
FloatType
BooleanType
DateType
TimestampType
ArrayType
MapType
StructType
```

For placement interviews, understand the commonly used types rather than memorizing every type.

---

# 19. Showing DataFrame Data

Use:

```python
df.show()
```

Example:

```python
df.show()
```

By default, Spark displays a limited number of rows in a readable table format.

---

# 20. Viewing the Schema

Use:

```python
df.printSchema()
```

Example:

```python
df.printSchema()
```

This is commonly used to understand the structure of a DataFrame.

---

# 21. DataFrame vs Pandas DataFrame

| PySpark DataFrame | Pandas DataFrame |
|---|---|
| Distributed | Primarily in-memory on one machine |
| Designed for large-scale data | Best suited to smaller/local datasets |
| Runs on Spark | Runs locally in Python |
| Can process data across a cluster | Usually limited by one machine's resources |
| Lazy execution for Spark transformations | Operations generally execute eagerly |

---

# 22. RDD

**RDD (Resilient Distributed Dataset)** is a distributed collection of objects that can be processed in parallel across a cluster.

RDDs are one of Spark's fundamental abstractions.

Important characteristics:

```text
Distributed
Immutable
Fault-tolerant
Parallel processing
```

---

# 23. RDD vs DataFrame

| RDD | DataFrame |
|---|---|
| Lower-level abstraction | Higher-level abstraction |
| Collection of objects | Structured data with named columns |
| Less optimization by Spark | Spark can optimize DataFrame operations |
| More control | Easier for structured data |
| Generally more verbose | More concise |
| Useful for low-level/custom processing | Preferred for most structured-data workloads |

### Interview Answer

> DataFrames are generally preferred for structured data because they provide a higher-level API and allow Spark to optimize the execution plan.

---

# 24. Immutability in Spark

Spark DataFrames and RDDs are **immutable**.

This means an existing DataFrame is not modified directly.

Instead, transformations create a new DataFrame.

Example:

```python
df2 = df.filter(df.age > 21)
```

Here:

```text
df
 ↓
filter()
 ↓
df2
```

The original `df` remains unchanged.

---

# 25. Lazy Evaluation

Spark uses **lazy evaluation** for transformations.

When we write:

```python
df2 = df.filter(df.age > 21)
```

Spark does not immediately execute the filtering operation.

It builds an execution plan.

Execution generally happens when an **action** is called.

Example:

```python
df2.show()
```

Conceptually:

```text
Transformation
      ↓
Build execution plan
      ↓
Action
      ↓
Execution
```

---

# 26. Transformations

A **transformation** creates a new dataset/DataFrame from an existing one.

Common examples:

```python
filter()
select()
withColumn()
drop()
distinct()
```

Transformations are generally lazily evaluated.

Example:

```python
df2 = df.filter(df.age > 21)
```

---

# 27. Actions

An **action** triggers execution and produces a result or writes data.

Common examples:

```python
show()
count()
collect()
first()
take()
write...
```

Example:

```python
df.count()
```

This triggers execution.

---

# 28. Transformation vs Action

| Transformation | Action |
|---|---|
| Creates a new dataset/DataFrame | Produces result or performs output |
| Lazily evaluated | Triggers execution |
| Example: `filter()` | Example: `count()` |
| Example: `select()` | Example: `show()` |

### Easy Memory Trick

```text
Transformation
→ What should Spark do?

Action
→ Now execute it.
```

---

# 29. Narrow Transformation

A **narrow transformation** can process each output partition using data from a small number of input partitions without requiring a full redistribution of data.

Examples commonly include:

```text
filter
map
select
```

Conceptually:

```text
Partition 1 → Partition 1
Partition 2 → Partition 2
Partition 3 → Partition 3
```

---

# 30. Wide Transformation

A **wide transformation** requires data to be redistributed across partitions.

This redistribution is called a:

```text
Shuffle
```

Examples:

```text
groupBy
join
distinct
orderBy
```

Conceptually:

```text
Partition 1 ──┐
Partition 2 ──┼──→ Shuffle → New Partitions
Partition 3 ──┘
```

---

# 31. Why is Shuffle Important?

Shuffle can be expensive because Spark may need to:

```text
Redistribute data
Move data across executors
Perform network I/O
Write/read intermediate data
```

This is why minimizing unnecessary shuffle is an important Spark optimization concept.

---

# 32. Catalyst Optimizer

Spark SQL/DataFrame operations can be optimized by Spark's **Catalyst optimizer**.

Conceptually:

```text
DataFrame / SQL
       ↓
Logical Plan
       ↓
Catalyst Optimization
       ↓
Physical Plan
       ↓
Execution
```

For interviews, remember:

> Catalyst is Spark SQL's query optimization framework.

---

# 33. Tungsten

**Tungsten** refers to Spark's execution-engine improvements focused on efficient CPU and memory usage.

It is associated with areas such as:

```text
Memory management
CPU efficiency
Binary processing
Whole-stage code generation
```

For fresher interviews, knowing the basic purpose is enough.

---

# 34. Why are DataFrames Preferred?

DataFrames are generally preferred for structured data because they provide:

```text
High-level API
Schema
SQL support
Query optimization
Better readability
Convenient built-in functions
```

---

# 35. Basic DataFrame Example

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("EmployeeExample") \
    .getOrCreate()

data = [
    (1, "Harsha", 50000),
    (2, "Rahul", 60000),
    (3, "Priya", 55000)
]

columns = ["id", "name", "salary"]

df = spark.createDataFrame(data, columns)

df.show()
df.printSchema()

high_salary = df.filter(df.salary > 55000)

high_salary.show()
```

---

# 36. Important Interview Questions

```text
1. What is Apache Spark?

2. What is PySpark?

3. Spark vs PySpark?

4. Why is PySpark used?

5. What is SparkSession?

6. What is a Spark application?

7. What is a Driver?

8. What is an Executor?

9. What is a Cluster Manager?

10. Driver vs Executor?

11. What is a Spark Job?

12. What is a Stage?

13. What is a Task?

14. Job vs Stage vs Task?

15. What is a DataFrame?

16. What is a DataFrame schema?

17. What is an RDD?

18. RDD vs DataFrame?

19. Why are DataFrames preferred over RDDs?

20. What is lazy evaluation?

21. What is a transformation?

22. What is an action?

23. Transformation vs Action?

24. What is a narrow transformation?

25. What is a wide transformation?

26. What is a shuffle?

27. Why is shuffle expensive?

28. What is immutability in Spark?

29. What is Catalyst Optimizer?

30. What is Tungsten?

31. PySpark DataFrame vs Pandas DataFrame?

32. How do you create a DataFrame in PySpark?

33. How do you check a DataFrame's schema?

34. How do you display DataFrame data?

35. What happens when an action is called?
```

---

# 37. ⭐ Most Important Questions for Placements

If you have limited time, focus on these:

```text
1. What is Spark?

2. What is PySpark?

3. What is SparkSession?

4. What is Driver?

5. What is Executor?

6. Driver vs Executor?

7. What are Job, Stage and Task?

8. What is a DataFrame?

9. What is RDD?

10. RDD vs DataFrame?

11. What is lazy evaluation?

12. Transformation vs Action?

13. What are narrow and wide transformations?

14. What is shuffle?

15. Why are DataFrames preferred?

16. PySpark DataFrame vs Pandas DataFrame?
```

---

# 38. Quick Revision

```text
PYSPARK
→ Python API for Apache Spark

SPARK
→ Distributed data-processing framework

SPARKSESSION
→ Main entry point for DataFrames and Spark SQL

DRIVER
→ Coordinates application

EXECUTOR
→ Executes tasks

CLUSTER MANAGER
→ Allocates cluster resources

JOB
→ Triggered by an action

STAGE
→ Group of tasks separated by shuffle boundaries

TASK
→ Unit of work executed on a partition

DATAFRAME
→ Distributed structured data with named columns

RDD
→ Distributed collection of objects

DATAFRAME
→ Higher-level + optimized + preferred for structured data

IMMUTABLE
→ Existing DataFrame/RDD is not modified

TRANSFORMATION
→ Creates new dataset/DataFrame

ACTION
→ Triggers execution

LAZY EVALUATION
→ Transformations are not immediately executed

NARROW TRANSFORMATION
→ No full data redistribution

WIDE TRANSFORMATION
→ Requires data redistribution

SHUFFLE
→ Redistribution of data across partitions

CATALYST
→ Spark SQL query optimizer

TUNGSTEN
→ Spark execution/memory/CPU efficiency improvements
```

---

# 39. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
Spark
PySpark
SparkSession
Driver
Executor
Job
Stage
Task
DataFrame
RDD
RDD vs DataFrame
Transformations
Actions
Lazy Evaluation
Narrow vs Wide Transformation
Shuffle
```

## ⭐⭐⭐ Good to Know

```text
Cluster Manager
Schema
Catalyst Optimizer
Tungsten
PySpark vs Pandas
```

> **For a fresher interview, you do not need deep Spark internals here. Be able to clearly explain the architecture basics, DataFrames, RDD vs DataFrame, lazy evaluation, transformations/actions, and shuffle.**