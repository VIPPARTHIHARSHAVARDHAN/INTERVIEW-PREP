# PySpark DataFrame Operations, Joins and Aggregations

## 1. DataFrame Operations

A **DataFrame** is a distributed collection of structured data organized into named columns.

Example:

```python
data = [
    (1, "Harsha", 50000, "IT"),
    (2, "Rahul", 60000, "HR"),
    (3, "Priya", 55000, "IT"),
    (4, "Arjun", 70000, "Finance")
]

columns = ["id", "name", "salary", "department"]

df = spark.createDataFrame(data, columns)
```

---

# 2. select()

`select()` is used to select specific columns.

```python
df.select("name", "salary").show()
```

Output:

```text
+------+------+
|  name|salary|
+------+------+
|Harsha| 50000|
| Rahul| 60000|
| Priya| 55000|
| Arjun| 70000|
+------+------+
```

You can also use expressions:

```python
df.select(
    "name",
    "salary",
    (df.salary * 12).alias("annual_salary")
).show()
```

---

# 3. filter()

`filter()` is used to filter rows based on a condition.

```python
df.filter(df.salary > 55000).show()
```

You can also use `where()`:

```python
df.where(df.salary > 55000).show()
```

`filter()` and `where()` are commonly used interchangeably for DataFrames.

---

# 4. Multiple Conditions

Use:

```text
&
|
~
```

for:

```text
AND
OR
NOT
```

Example:

```python
df.filter(
    (df.salary > 50000) & (df.department == "IT")
).show()
```

OR:

```python
df.filter(
    (df.department == "IT") | (df.department == "HR")
).show()
```

NOT:

```python
df.filter(
    ~(df.department == "IT")
).show()
```

---

# 5. withColumn()

`withColumn()` is used to create a new column or replace an existing column.

Example:

```python
df = df.withColumn(
    "annual_salary",
    df.salary * 12
)
```

Now the DataFrame contains:

```text
id
name
salary
department
annual_salary
```

---

# 6. Renaming a Column

Use:

```python
withColumnRenamed()
```

Example:

```python
df = df.withColumnRenamed(
    "salary",
    "monthly_salary"
)
```

---

# 7. drop()

`drop()` removes a column.

```python
df = df.drop("annual_salary")
```

Multiple columns:

```python
df = df.drop("annual_salary", "department")
```

---

# 8. distinct()

`distinct()` removes duplicate rows.

```python
df.distinct().show()
```

---

# 9. dropDuplicates()

`dropDuplicates()` removes duplicate rows based on selected columns.

```python
df.dropDuplicates(["name"]).show()
```

---

# 10. orderBy()

`orderBy()` sorts rows.

Ascending:

```python
df.orderBy("salary").show()
```

Descending:

```python
from pyspark.sql.functions import desc

df.orderBy(desc("salary")).show()
```

Multiple columns:

```python
df.orderBy(
    "department",
    desc("salary")
).show()
```

---

# 11. limit()

`limit()` returns a specified number of rows.

```python
df.limit(5).show()
```

---

# 12. count()

`count()` returns the number of rows.

```python
df.count()
```

Example:

```text
4
```

`count()` is an **action**.

---

# 13. collect()

`collect()` brings all rows from the distributed DataFrame to the driver.

```python
rows = df.collect()
```

### Important

Avoid using `collect()` on very large DataFrames because it can overload driver memory.

---

# 14. first() and take()

Get the first row:

```python
df.first()
```

Get a limited number of rows:

```python
df.take(5)
```

These are useful when you only need a small result.

---

# 15. groupBy()

`groupBy()` groups rows based on one or more columns.

Example:

```python
df.groupBy("department").count().show()
```

Output conceptually:

```text
+----------+-----+
|department|count|
+----------+-----+
|IT        |2    |
|HR        |1    |
|Finance   |1    |
+----------+-----+
```

---

# 16. Aggregation Functions

Common aggregation functions:

```text
count()
sum()
avg()
min()
max()
```

Import them:

```python
from pyspark.sql.functions import (
    count,
    sum,
    avg,
    min,
    max
)
```

---

# 17. sum()

Calculate total salary:

```python
df.agg(
    sum("salary").alias("total_salary")
).show()
```

---

# 18. avg()

Calculate average salary:

```python
df.agg(
    avg("salary").alias("average_salary")
).show()
```

---

# 19. min() and max()

```python
df.agg(
    min("salary").alias("minimum_salary"),
    max("salary").alias("maximum_salary")
).show()
```

---

# 20. groupBy() with Aggregations

Example:

```python
df.groupBy("department").agg(
    avg("salary").alias("avg_salary"),
    max("salary").alias("max_salary"),
    min("salary").alias("min_salary")
).show()
```

This is one of the most commonly used PySpark patterns.

---

# 21. Multiple Aggregations

```python
df.groupBy("department").agg(
    count("*").alias("employee_count"),
    sum("salary").alias("total_salary"),
    avg("salary").alias("average_salary")
).show()
```

Conceptually:

```text
Department
    ↓
Group rows
    ↓
Calculate aggregates
    ↓
Result
```

---

# 22. groupBy() vs agg()

```text
groupBy()
→ Defines how rows should be grouped

agg()
→ Defines calculations to perform on those groups
```

Example:

```python
df.groupBy("department").agg(
    avg("salary")
)
```

---

# 23. Joins

A **join** combines rows from two DataFrames based on a related column or condition.

Example:

### Employee DataFrame

```text
+---+------+----------+
|id |name  |dept_id   |
+---+------+----------+
|1  |Harsha|10        |
|2  |Rahul |20        |
|3  |Priya |10        |
+---+------+----------+
```

### Department DataFrame

```text
+-------+----------+
|dept_id|department|
+-------+----------+
|10     |IT        |
|20     |HR        |
+-------+----------+
```

---

# 24. Inner Join

Returns rows that have matching values in both DataFrames.

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "inner"
)
```

Conceptually:

```text
Employee          Department

dept_id = 10  ←→  dept_id = 10
dept_id = 20  ←→  dept_id = 20
```

Only matching rows are returned.

---

# 25. Left Join

Returns:

```text
All rows from left DataFrame
+
Matching rows from right DataFrame
```

Example:

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "left"
)
```

If a department does not exist in the right DataFrame, its columns become `NULL`.

---

# 26. Right Join

Returns:

```text
All rows from right DataFrame
+
Matching rows from left DataFrame
```

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "right"
)
```

---

# 27. Full Outer Join

Returns all rows from both DataFrames.

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "full"
)
```

Non-matching columns contain `NULL`.

---

# 28. Left Semi Join

A **left semi join** returns rows from the left DataFrame where a match exists in the right DataFrame.

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "left_semi"
)
```

Important:

```text
Returns only columns from the left DataFrame.
```

---

# 29. Left Anti Join

A **left anti join** returns rows from the left DataFrame where no match exists in the right DataFrame.

```python
result = employees.join(
    departments,
    employees.dept_id == departments.dept_id,
    "left_anti"
)
```

Useful for finding:

```text
Unmatched records
Missing records
Records without corresponding reference data
```

---

# 30. Join Types Summary

| Join | Result |
|---|---|
| Inner | Matching rows from both |
| Left | All left + matching right |
| Right | All right + matching left |
| Full | All rows from both |
| Left Semi | Left rows having a match |
| Left Anti | Left rows having no match |

### Easy Memory Trick

```text
INNER
→ Only matching

LEFT
→ Everything from left

RIGHT
→ Everything from right

FULL
→ Everything from both

LEFT SEMI
→ Left rows with match

LEFT ANTI
→ Left rows without match
```

---

# 31. Joining Using Same Column Name

If both DataFrames have the same join column name:

```python
result = employees.join(
    departments,
    on="dept_id",
    how="inner"
)
```

This is often cleaner than writing:

```python
employees.dept_id == departments.dept_id
```

---

# 32. Joining on Multiple Columns

You can join using multiple conditions.

```python
result = df1.join(
    df2,
    (df1.id == df2.id) &
    (df1.date == df2.date),
    "inner"
)
```

---

# 33. Handling Duplicate Columns After Join

Suppose both DataFrames contain:

```text
id
```

After a join, you may have ambiguous references.

One approach is to use aliases:

```python
from pyspark.sql.functions import col

e = employees.alias("e")
d = departments.alias("d")

result = e.join(
    d,
    col("e.dept_id") == col("d.dept_id"),
    "inner"
)

result.select(
    col("e.id"),
    col("e.name"),
    col("d.department")
).show()
```

---

# 34. Broadcast Join

A **broadcast join** can be useful when one DataFrame is small enough to be copied to each executor.

Example:

```python
from pyspark.sql.functions import broadcast

result = employees.join(
    broadcast(departments),
    "dept_id"
)
```

Conceptually:

```text
Small DataFrame
      ↓
Broadcast
 ↓    ↓    ↓
E1   E2   E3

Large DataFrame
 ↓    ↓    ↓
E1   E2   E3
```

This can reduce the need for a large shuffle.

---

# 35. When to Use Broadcast Join?

Use it when:

```text
One side of the join is relatively small
+
It can safely fit in executor memory
```

Example:

```text
Large Employee Data
        +
Small Department Lookup
```

---

# 36. Join Performance

Joins can become expensive because they may require:

```text
Shuffle
Network transfer
Sorting
Memory
```

Important optimization ideas:

```text
Broadcast small tables
Filter unnecessary data before joining
Select only required columns
Avoid unnecessary joins
Choose appropriate partitioning
```

---

# 37. Filtering Before Joining

Instead of joining unnecessary data:

```python
filtered_employees = employees.filter(
    employees.salary > 50000
)

result = filtered_employees.join(
    departments,
    "dept_id"
)
```

This can reduce the amount of data involved in the join.

---

# 38. Selecting Required Columns Before Joining

Instead of carrying unnecessary columns:

```python
departments_small = departments.select(
    "dept_id",
    "department"
)

result = employees.join(
    departments_small,
    "dept_id"
)
```

This can reduce data movement and memory usage.

---

# 39. Common PySpark DataFrame Pattern

A common ETL pattern is:

```python
result = (
    df
    .filter(df.salary > 50000)
    .select("id", "name", "salary", "department")
    .withColumn("annual_salary", df.salary * 12)
    .groupBy("department")
    .agg(
        avg("salary").alias("avg_salary"),
        max("salary").alias("max_salary")
    )
)
```

This demonstrates:

```text
Filter
 ↓
Select
 ↓
withColumn
 ↓
GroupBy
 ↓
Aggregation
```

---

# 40. Common Interview Questions

```text
1. What is a DataFrame in PySpark?

2. How do you select columns from a DataFrame?

3. What is the difference between select() and withColumn()?

4. What does filter() do?

5. filter() vs where()?

6. How do you add a new column?

7. How do you rename a column?

8. How do you remove a column?

9. distinct() vs dropDuplicates()?

10. How do you sort a DataFrame?

11. What does groupBy() do?

12. What are common aggregation functions?

13. How do you calculate average salary by department?

14. How do you find the maximum value in each group?

15. What is a join?

16. What are the different types of joins in PySpark?

17. Inner join vs left join?

18. What is a left semi join?

19. What is a left anti join?

20. What is a full outer join?

21. How do you join two DataFrames?

22. How do you join using multiple columns?

23. How do you handle duplicate column names after a join?

24. What is a broadcast join?

25. When should you use a broadcast join?

26. Why can joins be expensive in Spark?

27. How can you optimize a join?

28. Why should you filter data before joining?

29. Why should you select only required columns before joining?

30. What happens when a DataFrame action such as count() is called?
```

---

# 41. ⭐ Most Important Interview Questions

If you have limited time, prepare these first:

```text
1. What is a DataFrame?

2. select() vs withColumn()?

3. filter() vs where()?

4. How do you add/remove/rename columns?

5. What is groupBy()?

6. How do you perform aggregations?

7. Explain all important join types.

8. Inner join vs left join?

9. Left semi vs left anti join?

10. How do you join two DataFrames?

11. What is a broadcast join?

12. When should you use broadcast join?

13. Why are joins expensive in Spark?

14. How can you optimize joins?

15. What is the difference between a transformation and an action?

16. Why can collect() be dangerous for large data?
```

---

# 42. Quick Revision

```text
select()
→ Select columns

filter() / where()
→ Filter rows

withColumn()
→ Add/replace column

withColumnRenamed()
→ Rename column

drop()
→ Remove column

distinct()
→ Remove duplicate rows

dropDuplicates()
→ Remove duplicates based on columns

orderBy()
→ Sort rows

limit()
→ Return limited rows

count()
→ Count rows

collect()
→ Bring all rows to driver

groupBy()
→ Group rows

agg()
→ Perform aggregations

JOIN
→ Combine DataFrames

INNER
→ Matching rows

LEFT
→ All left + matching right

RIGHT
→ All right + matching left

FULL
→ All rows from both

LEFT SEMI
→ Left rows with matching right

LEFT ANTI
→ Left rows without matching right

BROADCAST JOIN
→ Copy small table to executors

SHUFFLE
→ Redistribute data across partitions

JOIN OPTIMIZATION
→ Filter early
→ Select required columns
→ Broadcast small tables when appropriate
→ Avoid unnecessary joins
```

---

# 43. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
DataFrame
select()
filter()
where()
withColumn()
groupBy()
agg()
count()
Inner Join
Left Join
Full Join
Left Semi Join
Left Anti Join
Broadcast Join
Join Performance
```

## ⭐⭐⭐ Good to Know

```text
Right Join
distinct()
dropDuplicates()
orderBy()
collect()
Multiple-column joins
Duplicate-column handling
```

> **For fresher Data Engineer interviews, focus especially on DataFrame operations, `groupBy()` + aggregations, join types, left semi/anti joins, and broadcast joins. You should also be comfortable writing small PySpark DataFrame queries rather than only memorizing definitions.**