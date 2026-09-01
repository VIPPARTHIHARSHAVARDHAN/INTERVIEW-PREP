# Data Pipelines, Airflow and Scenarios

## 1. What is a Data Pipeline?

A **data pipeline** is a sequence of processes that moves data from one or more sources to a destination while performing required transformations.

```text
Data Source
    ↓
Ingestion
    ↓
Storage
    ↓
Transformation
    ↓
Data Warehouse
    ↓
Analytics
```

Example:

```text
MySQL
  ↓
S3
  ↓
PySpark / Glue
  ↓
S3 Processed
  ↓
Redshift
  ↓
BI Dashboard
```

---

# 2. What is Data Pipeline Orchestration?

**Orchestration** means managing and coordinating different tasks in a data pipeline.

It handles things such as:

```text
Task dependencies
Scheduling
Retries
Failure handling
Monitoring
Execution order
```

Example:

```text
Extract
  ↓
Transform
  ↓
Load
```

The transformation should not start until extraction has completed successfully.

---

# 3. What is Apache Airflow?

**Apache Airflow** is an open-source platform used to **develop, schedule, and monitor workflows**.

It is commonly used to orchestrate data pipelines.

Example:

```text
Airflow
   ↓
Extract Data
   ↓
Run Transformation
   ↓
Load Warehouse
   ↓
Send Notification
```

---

# 4. Why is Airflow Used?

Airflow helps with:

```text
Scheduling
Task dependencies
Workflow management
Retries
Monitoring
Failure handling
Backfilling
```

It is an **orchestration tool**, not primarily a data-processing engine.

---

# 5. Airflow vs PySpark

This is an important interview question.

```text
Airflow
→ Orchestrates and schedules tasks

PySpark
→ Processes large datasets
```

Example:

```text
Airflow
   ↓
Start PySpark Job
   ↓
PySpark
   ↓
Transform Data
```

### Easy Memory Trick

```text
Airflow → Controls

PySpark → Processes
```

---

# 6. What is a DAG?

DAG stands for **Directed Acyclic Graph**.

In Airflow, a DAG represents a workflow and defines:

```text
Tasks
Dependencies
Schedule
```

Example:

```text
Extract
   ↓
Transform
   ↓
Load
```

This represents a DAG because the workflow moves in a defined direction and does not contain a circular dependency.

---

# 7. What Does DAG Mean?

### Directed

Tasks have a direction.

```text
A → B
```

### Acyclic

The workflow cannot contain a cycle.

Invalid:

```text
A → B → C
↑       ↓
└───────┘
```

### Graph

The workflow consists of connected tasks.

---

# 8. What is a Task?

A **task** is a single unit of work inside an Airflow DAG.

Examples:

```text
Extract data
Run PySpark job
Execute SQL query
Load data
Send notification
```

Conceptually:

```text
DAG
 ↓
Task 1
Task 2
Task 3
```

---

# 9. What is an Operator?

An **Operator** defines what a task should do.

Common examples include:

```text
PythonOperator
BashOperator
SQL operators
Cloud-related operators
```

Example:

```python
from airflow.operators.python import PythonOperator

task = PythonOperator(
    task_id="extract_data",
    python_callable=extract_data
)
```

---

# 10. Task vs Operator

```text
Operator
→ Defines the type of work

Task
→ A specific instance of that operator in a DAG
```

For example:

```text
PythonOperator
       ↓
extract_task
```

---

# 11. What are Task Dependencies?

Task dependencies define the order in which tasks execute.

Example:

```python
extract >> transform >> load
```

This means:

```text
extract
   ↓
transform
   ↓
load
```

The `transform` task waits for `extract`.

The `load` task waits for `transform`.

---

# 12. Why are Dependencies Important?

Dependencies ensure that tasks execute in the correct order.

Example:

```text
Extract
   ↓
Transform
   ↓
Load
```

You should not load data before transformation has completed.

---

# 13. What is Scheduling in Airflow?

Scheduling determines when a DAG should run.

Examples:

```text
Every hour
Every day
Every week
Specific cron schedule
```

Example use case:

```text
Daily sales pipeline
→ Run once every day
```

---

# 14. What is a Retry?

A retry allows Airflow to execute a failed task again.

Example:

```text
Task
 ↓
Failure
 ↓
Retry
 ↓
Success
```

Retries are useful for temporary failures such as:

```text
Temporary network issue
Temporary service unavailability
Transient database issue
```

---

# 15. What Happens When a Task Fails?

Depending on the DAG configuration:

```text
Task fails
   ↓
Retry
   ↓
If still failing
   ↓
Task marked failed
   ↓
Dependent tasks may not run
```

The exact behavior depends on the task dependencies and trigger rules.

---

# 16. What is Backfill?

**Backfill** means running a workflow for historical dates that were missed or need to be processed again.

Example:

```text
Daily pipeline

July 1 → Success
July 2 → Success
July 3 → Failed
July 4 → Success
```

You may need to process the missing July 3 data.

That historical reprocessing is a form of backfill.

---

# 17. What is Catchup?

Airflow can run scheduled DAG intervals that were missed since the DAG's start date when catchup is enabled.

Conceptually:

```text
DAG start date
      ↓
Missed scheduled intervals
      ↓
Airflow runs them
```

For interviews, remember:

```text
Backfill
→ Intentionally process historical periods

Catchup
→ Airflow automatically runs missed scheduled intervals when configured to do so
```

---

# 18. What is XCom?

**XCom (Cross-communication)** allows Airflow tasks to exchange small amounts of information.

Example:

```text
Task 1
  ↓
Stores small value
  ↓
XCom
  ↓
Task 2
  ↓
Reads value
```

It can be useful for passing metadata such as:

```text
File path
Execution information
Small identifiers
```

XCom should **not** be used to transfer large datasets.

---

# 19. What is a Sensor?

A **Sensor** waits for a condition to become true.

Examples:

```text
Wait for a file
Wait for another task
Wait for an external event
Wait for data availability
```

Conceptually:

```text
Sensor
  ↓
Condition?
  ↓
No → Keep waiting
  ↓
Yes
  ↓
Continue pipeline
```

---

# 20. What is Idempotency?

A pipeline or operation is **idempotent** when running it multiple times produces the same intended final result rather than creating incorrect duplicates.

Example:

```text
Run pipeline once
→ 1,000 records

Run pipeline again
→ Still correct 1,000 records
```

instead of:

```text
Run 1 → 1,000 records
Run 2 → 2,000 records
```

Idempotency is very important in production data pipelines.

---

# 21. How Can You Make a Pipeline Idempotent?

Common approaches:

```text
Use unique keys
Use MERGE/UPSERT logic
Overwrite the correct partition
Track processed records
Use checkpoints/watermarks
Avoid blindly appending the same data
```

---

# 22. What is a Retry vs Rerun?

### Retry

A task automatically runs again after failure according to its retry configuration.

```text
Failure
 ↓
Retry
```

### Rerun

A task or workflow is manually or intentionally executed again.

```text
Previous execution
       ↓
Manual re-execution
```

---

# 23. What is Incremental Data Processing?

Incremental processing means processing only new or changed data instead of processing the complete dataset every time.

Example:

```text
Day 1
→ 1,000,000 records

Day 2
→ Process only 5,000 new/changed records
```

This reduces:

```text
Processing time
Data movement
Cost
```

---

# 24. What is a Watermark?

A **watermark** is a value used to track how far a pipeline has processed data.

A common example is a timestamp.

```text
Last processed timestamp
        ↓
2026-08-28 23:59:59
```

The next run can process records after that point.

```sql
SELECT *
FROM orders
WHERE updated_at > last_processed_timestamp;
```

---

# 25. What is Data Quality?

**Data quality** means ensuring that data is accurate, complete, consistent, valid, and usable.

Common checks include:

```text
NULL checks
Duplicate checks
Data type checks
Range checks
Record count checks
Uniqueness checks
Referential checks
```

---

# 26. What Happens if a Pipeline Receives Duplicate Data?

Possible approaches:

```text
Identify duplicates
Use unique keys
Deduplicate during transformation
Use MERGE/UPSERT
Make pipeline idempotent
```

Example:

```text
Incoming data
   ↓
Deduplication
   ↓
Clean data
   ↓
Target
```

---

# 27. What Happens if a Pipeline Fails?

A production pipeline should have:

```text
Error detection
Logging
Retries
Alerts
Failure handling
Restart/reprocessing strategy
```

Example:

```text
Pipeline
   ↓
Task fails
   ↓
Retry
   ↓
Still fails
   ↓
Log error
   ↓
Send alert
   ↓
Investigate / reprocess
```

---

# 28. What Happens if the Source Schema Changes?

Example:

Original:

```text
id
name
salary
```

Source changes to:

```text
id
name
salary
department
```

The pipeline should be designed to detect and appropriately handle schema changes.

Possible approaches:

```text
Schema validation
Schema evolution
Versioning
Backward-compatible changes
Pipeline updates
Alerts
```

---

# 29. What Happens if Data Arrives Late?

Late-arriving data means data arrives after the expected processing window.

Possible approaches:

```text
Watermarks
Reprocessing
Backfilling
Late-data handling logic
Partition updates
```

Example:

```text
Expected:
August 28 data → August 28

Actually arrives:
August 29
```

The pipeline should have a strategy for processing that late data correctly.

---

# 30. How Would You Design a Daily Data Pipeline?

Example:

```text
             Source
                ↓
             Extract
                ↓
             S3 Raw
                ↓
          Data Validation
                ↓
          PySpark / Glue
                ↓
          S3 Processed
                ↓
            Redshift
                ↓
          BI / Analytics
```

Airflow can orchestrate the workflow:

```text
Airflow
   ↓
Extract
   ↓
Validate
   ↓
Transform
   ↓
Load
   ↓
Notify
```

---

# 31. How Would You Handle a Failed Pipeline?

Interview-ready answer:

> First, I would identify the failed task and check the logs to understand the root cause. If it is a temporary failure, I would use retries. If the issue is related to data or code, I would fix the root cause and rerun or backfill the affected portion. I would also make sure the pipeline is idempotent so that reprocessing does not create duplicate data.

---

# 32. How Would You Handle Duplicate Data?

Interview-ready answer:

> I would identify a unique business key for the records and apply deduplication during processing. For incremental pipelines, I would use appropriate MERGE or upsert logic and make the pipeline idempotent so that rerunning it does not create duplicate records.

---

# 33. How Would You Handle a Large Dataset?

Important considerations:

```text
Use distributed processing
Partition data appropriately
Use columnar formats such as Parquet
Filter data early
Select required columns
Avoid unnecessary shuffles
Use appropriate joins
Process incrementally when possible
```

For your stack:

```text
S3
 ↓
PySpark / Glue
 ↓
Parquet
 ↓
Redshift / Athena
```

---

# 34. How Would You Monitor a Data Pipeline?

Monitor:

```text
Pipeline status
Task failures
Execution time
Record counts
Data quality
Resource usage
Logs
```

Possible tools:

```text
Airflow
CloudWatch
AWS Glue monitoring
```

---

# 35. How Would You Make a Pipeline Reliable?

Important practices:

```text
1. Retries
2. Logging
3. Monitoring
4. Alerts
5. Data validation
6. Idempotency
7. Incremental processing
8. Failure recovery
9. Proper dependency management
10. Testing
```

---

# 36. How Would You Handle a Pipeline That Suddenly Becomes Slow?

Investigate:

```text
Data volume
Data skew
Shuffle
Partitioning
Join strategy
Query performance
External service latency
Resource utilization
```

For a PySpark pipeline, check:

```text
Partitions
Shuffle
Data skew
Broadcast joins
Caching
Execution plan
```

---

# 37. Common Airflow Interview Questions

```text
1. What is Apache Airflow?

2. Why is Airflow used?

3. What is a DAG?

4. What does DAG stand for?

5. What is a task?

6. What is an operator?

7. Task vs Operator?

8. What are task dependencies?

9. How do you define task dependencies?

10. What is scheduling?

11. What is a retry?

12. What happens when a task fails?

13. What is backfill?

14. What is catchup?

15. What is XCom?

16. Why should XCom not be used for large datasets?

17. What is a Sensor?

18. Airflow vs PySpark?

19. How would you schedule a daily ETL pipeline?

20. How would you handle a failed Airflow task?
```

---

# 38. ⭐ Most Important Airflow Questions

If you have limited time:

```text
1. What is Airflow?

2. Why is Airflow used?

3. What is a DAG?

4. What is a task?

5. What is an operator?

6. Task vs Operator?

7. What are task dependencies?

8. What is scheduling?

9. What are retries?

10. What is backfill?

11. What is catchup?

12. What is XCom?

13. What is a Sensor?

14. Airflow vs PySpark?
```

---

# 39. Common Data Pipeline Scenario Questions

```text
1. How would you design a daily data pipeline?

2. What would you do if a pipeline fails?

3. How would you handle duplicate records?

4. How would you handle late-arriving data?

5. How would you handle schema changes?

6. How would you implement incremental loading?

7. What is idempotency and why is it important?

8. How would you monitor a pipeline?

9. How would you improve a slow pipeline?

10. How would you process a very large dataset?

11. How would you recover from a failed pipeline?

12. How would you prevent duplicate data after rerunning a pipeline?

13. How would you validate data before loading it into a warehouse?

14. How would you design a fault-tolerant pipeline?

15. How would you explain your project pipeline end-to-end?
```

---

# 40. ⭐ Most Important Scenarios

Prepare these especially well:

```text
1. Design an end-to-end data pipeline.

2. Pipeline failed — what will you do?

3. Pipeline ran twice — how will you prevent duplicates?

4. Source schema changed — what will you do?

5. Data arrived late — how will you handle it?

6. How will you implement incremental loading?

7. How will you monitor the pipeline?

8. Pipeline became slow — how will you troubleshoot it?

9. How will you ensure data quality?

10. How will you make the pipeline reliable and fault-tolerant?
```

---

# 41. Quick Revision

```text
DATA PIPELINE
→ Moves and processes data from source to destination

ORCHESTRATION
→ Coordinates pipeline tasks

AIRFLOW
→ Workflow orchestration and scheduling

DAG
→ Defines workflow and dependencies

TASK
→ Unit of work

OPERATOR
→ Defines what a task does

DEPENDENCY
→ Execution relationship between tasks

RETRY
→ Automatically try failed task again

BACKFILL
→ Process historical periods

CATCHUP
→ Run missed scheduled intervals when enabled

XCOM
→ Exchange small amounts of information between tasks

SENSOR
→ Wait for a condition

IDEMPOTENCY
→ Repeated execution produces the same intended result

INCREMENTAL PROCESSING
→ Process only new/changed data

WATERMARK
→ Tracks processing progress

DATA QUALITY
→ Ensures data is accurate and usable

MONITORING
→ Track pipeline health and failures
```

---

# 42. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
Data Pipeline
ETL Pipeline
Airflow
DAG
Task
Operator
Task Dependencies
Scheduling
Retries
Backfill
Airflow vs PySpark
Incremental Processing
Idempotency
Pipeline Failure Handling
Data Quality
```

## ⭐⭐⭐⭐ Good to Know

```text
Catchup
XCom
Sensors
Watermarks
Late-arriving data
Schema changes
Pipeline monitoring
Fault tolerance
```

> **For a fresher/Data Engineer interview, focus mainly on understanding how an end-to-end pipeline works, what Airflow does, DAGs/tasks/dependencies, retries, incremental loading, idempotency, data-quality checks, and common pipeline failure scenarios. You do not need deep Airflow internals unless the job specifically requires Airflow expertise.**