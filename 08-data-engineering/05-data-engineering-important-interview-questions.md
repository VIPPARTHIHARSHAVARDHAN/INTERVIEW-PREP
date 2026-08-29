# Data Engineering Important Interview Questions

> Placement-focused Data Engineering interview questions with **interview-ready answers for every question**.
>
> Focus on understanding the concept, giving a simple explanation, and connecting it to a practical Data Engineering project.

---

# 1. Data Engineering Basics

### 1. What is Data Engineering?

**Answer:**

Data Engineering is the process of collecting, storing, processing, transforming, and delivering data so that it can be used for analytics, reporting, and machine learning.

A Data Engineer builds and maintains the pipelines and infrastructure required to move data from sources to destinations.

---

### 2. What does a Data Engineer do?

**Answer:**

A Data Engineer designs, develops, and maintains data pipelines.

Typical responsibilities include:

- Data ingestion
- ETL/ELT
- Data transformation
- Data quality
- Data storage
- Pipeline monitoring
- Performance optimization
- Working with Data Lakes and Data Warehouses

---

### 3. What is a data pipeline?

**Answer:**

A data pipeline is a series of steps that moves data from a source to a destination while performing required processing or transformation.

Example:

```text
Source
  ↓
Ingestion
  ↓
Raw Storage
  ↓
Transformation
  ↓
Processed Data
  ↓
Data Warehouse
  ↓
Analytics
```

---

### 4. What are the main components of a data pipeline?

**Answer:**

The main components are:

1. **Source** – Where data comes from.
2. **Ingestion** – Brings data into the pipeline.
3. **Storage** – Stores raw or processed data.
4. **Transformation** – Cleans and transforms data.
5. **Loading** – Moves data to the target system.
6. **Orchestration** – Controls execution order.
7. **Monitoring** – Tracks failures and performance.

---

### 5. What is data ingestion?

**Answer:**

Data ingestion is the process of collecting and moving data from different sources into a storage or processing system.

Example:

```text
API / Database / CSV
        ↓
      S3
```

---

### 6. What is ETL?

**Answer:**

ETL stands for **Extract, Transform, Load**.

```text
Extract
→ Get data from source

Transform
→ Clean and modify data

Load
→ Store data in target system
```

---

### 7. Explain Extract, Transform, and Load.

**Answer:**

**Extract** means retrieving data from a source such as a database, API, or file.

**Transform** means cleaning, filtering, joining, aggregating, or changing the data.

**Load** means storing the transformed data in a target system such as a Data Warehouse.

---

### 8. What is ELT?

**Answer:**

ELT stands for **Extract, Load, Transform**.

In ELT, data is first extracted and loaded into the target storage system, and transformations are performed later.

```text
Source
  ↓
Extract
  ↓
Load
  ↓
Transform
```

---

### 9. ETL vs ELT?

**Answer:**

| ETL | ELT |
|---|---|
| Transform before loading | Transform after loading |
| Data is cleaned before target | Raw data can be loaded first |
| Common in traditional systems | Common in modern cloud systems |
| Processing occurs before target | Target system performs transformation |

---

### 10. When would you choose ETL over ELT?

**Answer:**

I would choose ETL when the target system should receive only cleaned or transformed data, or when the target system is not designed for heavy transformation.

For example, sensitive or unnecessary data can be removed before loading it into the target.

---

### 11. What is batch processing?

**Answer:**

Batch processing processes data in groups at scheduled or predefined intervals.

Example:

```text
Every day at 1 AM
      ↓
Process yesterday's data
```

---

### 12. What is streaming processing?

**Answer:**

Streaming processing processes data continuously or with very low latency as data arrives.

Example:

```text
Event
 ↓
Stream
 ↓
Processing
 ↓
Output
```

---

### 13. Batch vs Streaming?

**Answer:**

| Batch | Streaming |
|---|---|
| Processes data in groups | Processes data continuously |
| Higher latency | Lower latency |
| Suitable for daily reports | Suitable for real-time use cases |
| Example: Daily sales processing | Example: Real-time events |

---

### 14. What is full load?

**Answer:**

A full load copies all available data from the source to the target.

Example:

```text
Source: 1 million records
        ↓
Target: Load all 1 million records
```

---

### 15. What is incremental load?

**Answer:**

Incremental loading processes only new or changed records instead of processing the complete dataset every time.

Example:

```text
Existing records
      ↓
Find new/changed records
      ↓
Process only those records
```

---

### 16. Full load vs incremental load?

**Answer:**

| Full Load | Incremental Load |
|---|---|
| Processes all data | Processes only new/changed data |
| More expensive for large data | More efficient |
| Simple to implement | Requires change detection |
| Useful for small datasets | Useful for large datasets |

---

### 17. How do you implement incremental loading?

**Answer:**

One common approach is to use a timestamp or ID to identify new records.

Example:

```text
Last successful timestamp = 2026-08-28 23:00

Read records:
updated_at > last_successful_timestamp

Process them

Update the watermark
```

Other approaches include:

- Change Data Capture
- Increasing IDs
- Modification timestamps
- Source-specific change tracking

---

### 18. What is Change Data Capture (CDC)?

**Answer:**

CDC is a technique used to identify changes made to source data.

It can capture:

```text
INSERT
UPDATE
DELETE
```

Instead of processing the entire source every time, the pipeline processes only the changes.

---

### 19. What is data transformation?

**Answer:**

Data transformation means changing raw data into a useful format.

Examples:

```text
Filtering
Joining
Aggregating
Renaming columns
Changing data types
Removing duplicates
Handling NULLs
```

---

### 20. What is data cleaning?

**Answer:**

Data cleaning is the process of identifying and correcting or removing incorrect, incomplete, duplicate, or inconsistent data.

Examples:

```text
Remove duplicates
Handle NULL values
Correct data types
Standardize formats
Remove invalid records
```

---

### 21. What is data validation?

**Answer:**

Data validation checks whether data meets expected rules and quality requirements.

Examples:

```text
Age should not be negative
Customer ID should be unique
Required columns should not be NULL
Order amount should be valid
```

---

### 22. What is structured data?

**Answer:**

Structured data has a fixed and well-defined schema.

Example:

```text
Customer_ID | Name | Age
101         | Ravi | 25
102         | Arun | 28
```

Relational databases are commonly used for structured data.

---

### 23. What is semi-structured data?

**Answer:**

Semi-structured data does not follow a strict table structure but contains organizational information such as keys and values.

Examples:

```text
JSON
XML
```

---

### 24. What is unstructured data?

**Answer:**

Unstructured data does not have a predefined tabular structure.

Examples:

```text
Images
Videos
Audio
PDFs
Documents
```

---

### 25. Structured vs semi-structured vs unstructured data?

**Answer:**

| Type | Structure | Examples |
|---|---|---|
| Structured | Fixed schema | SQL tables, CSV |
| Semi-structured | Flexible schema | JSON, XML |
| Unstructured | No fixed schema | Images, videos, documents |

---

# 2. Data Warehouse and Data Lake

### 26. What is a Data Warehouse?

**Answer:**

A Data Warehouse is a centralized system designed to store structured, processed data for analytics and reporting.

Examples include:

```text
Amazon Redshift
Snowflake
Google BigQuery
```

---

### 27. Why do we use a Data Warehouse?

**Answer:**

A Data Warehouse is used to efficiently analyze large amounts of structured data.

It is commonly used for:

- Reporting
- Business Intelligence
- Dashboards
- Historical analysis
- Aggregations

---

### 28. What is a Data Lake?

**Answer:**

A Data Lake is a storage system that can store large amounts of raw and processed data in different formats.

It can store:

```text
CSV
JSON
Parquet
Logs
Images
Videos
```

Amazon S3 is commonly used as Data Lake storage.

---

### 29. Data Warehouse vs Data Lake?

**Answer:**

| Data Warehouse | Data Lake |
|---|---|
| Mostly structured data | Structured, semi-structured, unstructured |
| Usually processed data | Can store raw data |
| Mainly analytics | Analytics, processing, ML, exploration |
| Schema-on-write | Often schema-on-read |

---

### 30. What is a Data Lakehouse?

**Answer:**

A Data Lakehouse combines characteristics of Data Lakes and Data Warehouses.

It aims to provide:

```text
Data Lake flexibility
+
Data Warehouse analytics capabilities
```

It can support both large-scale data storage and analytical workloads.

---

### 31. What is OLTP?

**Answer:**

OLTP stands for **Online Transaction Processing**.

It is designed for frequent transactional operations such as:

```text
INSERT
UPDATE
DELETE
```

Examples:

```text
Bank transactions
Online orders
Customer accounts
```

---

### 32. What is OLAP?

**Answer:**

OLAP stands for **Online Analytical Processing**.

It is designed for analyzing large amounts of data.

Examples:

```text
Reports
Dashboards
Sales analysis
Business analytics
```

---

### 33. OLTP vs OLAP?

**Answer:**

| OLTP | OLAP |
|---|---|
| Transactional | Analytical |
| Frequent inserts/updates | Complex queries |
| Current operational data | Historical/analytical data |
| Example: Application DB | Example: Data Warehouse |

---

### 34. What is a Fact Table?

**Answer:**

A Fact Table stores measurable business events or metrics.

Example:

```text
Sales_Fact

order_id
customer_id
product_id
date_id
quantity
sales_amount
```

---

### 35. What is a Dimension Table?

**Answer:**

A Dimension Table stores descriptive information about business entities.

Example:

```text
Customer_Dimension

customer_id
customer_name
city
country
```

---

### 36. Fact Table vs Dimension Table?

**Answer:**

```text
Fact Table
→ Measurements / Business Events

Dimension Table
→ Descriptive Information
```

Example:

```text
Fact
→ sales_amount = 500

Dimension
→ customer_name = Ravi
```

---

### 37. What is a Star Schema?

**Answer:**

A Star Schema contains a central Fact Table connected directly to multiple Dimension Tables.

Example:

```text
             Customer
                |
                |
Product ---- Sales Fact ---- Date
                |
                |
             Location
```

---

### 38. What is a Snowflake Schema?

**Answer:**

A Snowflake Schema is a normalized version of a dimensional model where dimension tables can be split into additional related tables.

Example:

```text
Sales Fact
    ↓
Customer
    ↓
City
    ↓
Country
```

---

### 39. Star Schema vs Snowflake Schema?

**Answer:**

| Star Schema | Snowflake Schema |
|---|---|
| Dimensions are less normalized | Dimensions are more normalized |
| Simpler | More complex |
| Fewer joins | More joins |
| Often easier for analytics | Can reduce redundancy |

---

### 40. What is Data Modeling?

**Answer:**

Data Modeling is the process of designing how data is organized, related, stored, and accessed.

It includes:

```text
Tables
Columns
Relationships
Keys
Constraints
Schemas
```

---

### 41. What is a Surrogate Key?

**Answer:**

A Surrogate Key is an artificial key created specifically to uniquely identify a record.

Example:

```text
customer_sk = 1001
```

It usually has no business meaning.

---

### 42. What is a Natural Key?

**Answer:**

A Natural Key is a key derived from actual business data.

Example:

```text
email
employee_id
passport_number
```

---

### 43. Surrogate Key vs Natural Key?

**Answer:**

```text
Surrogate Key
→ Artificial identifier

Natural Key
→ Real-world/business identifier
```

Surrogate keys are commonly useful in Data Warehouses because business identifiers can change.

---

### 44. What is a Data Mart?

**Answer:**

A Data Mart is a smaller, subject-specific part of a Data Warehouse.

Examples:

```text
Sales Data Mart
Finance Data Mart
Marketing Data Mart
```

---

### 45. What is a Staging Area?

**Answer:**

A staging area is an intermediate location where data is temporarily stored before transformation or loading into the final target.

Example:

```text
Source
 ↓
Staging
 ↓
Transformation
 ↓
Warehouse
```

---

### 46. What are Bronze, Silver, and Gold layers?

**Answer:**

They are commonly used to organize Data Lake data into processing stages.

```text
Bronze
→ Raw data

Silver
→ Cleaned and transformed data

Gold
→ Business-ready / curated data
```

---

### 47. What is Parquet?

**Answer:**

Parquet is a columnar storage file format commonly used in Data Engineering.

It stores data by columns rather than rows.

---

### 48. Why is Parquet commonly used in Data Engineering?

**Answer:**

Parquet is useful because:

- It is columnar.
- It supports efficient compression.
- It can reduce storage size.
- Queries can read only required columns.
- It works well with Spark and analytical engines.

---

### 49. CSV vs Parquet?

**Answer:**

| CSV | Parquet |
|---|---|
| Row-oriented text format | Columnar binary format |
| Usually larger | Usually more storage-efficient |
| No strong schema | Stores schema information |
| Simple and portable | Better for analytics |
| Can be slower for large analytical workloads | Efficient for analytical processing |

---

### 50. What is partitioning in a Data Lake?

**Answer:**

Partitioning divides data into separate paths based on one or more columns.

Example:

```text
sales/
├── year=2025/
│   ├── month=01/
│   └── month=02/
└── year=2026/
    ├── month=01/
    └── month=02/
```

---

### 51. What is Partition Pruning?

**Answer:**

Partition pruning means reading only the partitions required by a query instead of scanning all partitions.

Example:

```sql
SELECT *
FROM sales
WHERE year = 2026;
```

If the data is partitioned by year, only the required partition may need to be scanned.

---

### 52. What is Schema Evolution?

**Answer:**

Schema Evolution is the ability to handle changes in the structure of data over time.

Examples:

```text
Adding a new column
Changing a field
Removing a field
Changing data structure
```

A pipeline should handle schema changes without unnecessarily breaking existing processing.

---

# 3. AWS Data Engineering

### 53. Why is AWS used in Data Engineering?

**Answer:**

AWS provides scalable and managed services for data storage, processing, querying, orchestration, and monitoring.

Example:

```text
S3
→ Storage

Glue
→ ETL / Processing

Athena
→ Query S3

Redshift
→ Data Warehouse

CloudWatch
→ Monitoring
```

---

### 54. What is Amazon S3?

**Answer:**

Amazon S3 is an object storage service used to store large amounts of data.

It is commonly used for Data Lakes and can store:

```text
CSV
JSON
Parquet
Logs
Images
Videos
```

---

### 55. What is an S3 Bucket?

**Answer:**

An S3 Bucket is a container used to store objects in Amazon S3.

Example:

```text
my-bucket/
├── raw/
├── processed/
└── curated/
```

---

### 56. What is an S3 Object?

**Answer:**

An S3 Object is a piece of data stored in an S3 bucket.

Example:

```text
s3://my-bucket/raw/orders/orders.csv
```

The file is the object and its key identifies its location within the bucket.

---

### 57. Why is S3 commonly used as Data Lake storage?

**Answer:**

S3 is highly scalable and can store large amounts of data in different formats.

It can store:

```text
Raw Data
Processed Data
Curated Data
Historical Data
```

It can also be accessed by services such as Glue, Athena, and Redshift.

---

### 58. What are S3 Storage Classes?

**Answer:**

S3 provides different storage classes based on access patterns and cost requirements.

Examples include:

```text
S3 Standard
S3 Intelligent-Tiering
S3 Standard-IA
S3 One Zone-IA
S3 Glacier Instant Retrieval
S3 Glacier Flexible Retrieval
S3 Glacier Deep Archive
```

Frequently accessed data can use Standard, while archival data can use Glacier classes.

---

### 59. What is IAM?

**Answer:**

IAM stands for **Identity and Access Management**.

It controls who can access AWS resources and what actions they can perform.

---

### 60. What is an IAM Policy?

**Answer:**

An IAM Policy defines permissions for AWS resources.

It specifies actions that are allowed or denied for particular resources.

Example:

```text
Allow
s3:GetObject
on specific S3 objects
```

---

### 61. What is an IAM Role?

**Answer:**

An IAM Role is an identity with permissions that can be assumed by users, applications, or AWS services.

For example:

```text
Glue Job
   ↓
IAM Role
   ↓
S3 Permissions
```

---

### 62. IAM User vs IAM Role?

**Answer:**

```text
IAM User
→ Represents an identity

IAM Role
→ Assumable identity with permissions
```

AWS services commonly use IAM Roles to access other AWS services.

---

### 63. What is AWS Glue?

**Answer:**

AWS Glue is a managed serverless data integration and ETL service.

It can be used for:

```text
Data Integration
ETL
Data Transformation
Schema Discovery
PySpark Processing
```

---

### 64. What is a Glue Crawler?

**Answer:**

A Glue Crawler scans data sources and discovers schema information.

It can create or update metadata in the Glue Data Catalog.

---

### 65. What is Glue Data Catalog?

**Answer:**

Glue Data Catalog is a centralized metadata repository.

It stores information such as:

```text
Table names
Column names
Data types
Data locations
Partitions
```

It stores metadata rather than the actual data.

---

### 66. What is a Glue Job?

**Answer:**

A Glue Job performs data processing and ETL operations.

It can use PySpark to read, transform, and write large datasets.

Example:

```text
S3 Raw
   ↓
Glue Job
   ↓
PySpark
   ↓
Transformation
   ↓
S3 Processed
```

---

### 67. Glue Crawler vs Glue Job?

**Answer:**

```text
Glue Crawler
→ Discovers schema and metadata

Glue Job
→ Processes and transforms data
```

---

### 68. What is Amazon Athena?

**Answer:**

Amazon Athena is a serverless interactive query service that allows users to query data stored in S3 using SQL.

Example:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

---

### 69. Why is Athena used?

**Answer:**

Athena is useful for querying data directly from S3 without loading it into a traditional database.

It is useful for:

- Ad-hoc analysis
- Data exploration
- SQL queries on Data Lake data
- Quick analytical queries

---

### 70. Athena vs Redshift?

**Answer:**

```text
Athena
→ Queries data directly in S3

Redshift
→ Dedicated Data Warehouse
```

Athena is useful for querying Data Lake data, while Redshift is designed for data warehousing and analytical workloads.

---

### 71. What is Amazon Redshift?

**Answer:**

Amazon Redshift is a cloud Data Warehouse designed for analytical workloads.

It can be used for:

```text
Reporting
Business Intelligence
Analytics
Complex SQL Queries
```

---

### 72. Why is Redshift used?

**Answer:**

Redshift is used when an organization needs a dedicated analytical data warehouse for querying large amounts of structured data.

---

### 73. S3 vs Redshift?

**Answer:**

```text
S3
→ Object Storage / Data Lake

Redshift
→ Data Warehouse / Analytics
```

S3 is primarily used for storing data, while Redshift is designed for analytical querying and warehousing.

---

### 74. What is AWS Lambda?

**Answer:**

AWS Lambda is a serverless compute service that runs code in response to events or requests.

Example:

```text
S3 File Upload
      ↓
Lambda
      ↓
Run Function
```

---

### 75. How can Lambda be used in Data Engineering?

**Answer:**

Lambda is useful for lightweight, event-driven tasks.

Example:

```text
File arrives in S3
      ↓
S3 Event
      ↓
Lambda
      ↓
Trigger Glue Job
```

---

### 76. What is Amazon CloudWatch?

**Answer:**

CloudWatch is an AWS monitoring and observability service.

It can collect and monitor:

```text
Logs
Metrics
Alarms
Events
```

---

### 77. Why is CloudWatch important?

**Answer:**

CloudWatch helps monitor AWS resources and data pipelines.

It can help identify:

```text
Pipeline failures
Errors
High resource usage
Performance issues
Application problems
```

---

### 78. What is a serverless service?

**Answer:**

A serverless service allows users to run workloads without managing the underlying servers themselves.

Examples:

```text
AWS Lambda
AWS Glue
Amazon Athena
```

The servers still exist, but AWS manages the infrastructure.

---

### 79. Glue vs EMR?

**Answer:**

Both can be used for big-data processing with Spark, but they provide different levels of infrastructure management.

```text
AWS Glue
→ Managed/serverless ETL service
→ Less infrastructure management

Amazon EMR
→ Managed cluster-based big-data platform
→ More control and flexibility over the environment
```

For many standard ETL workloads, Glue can be simpler to operate.

---

# 4. Airflow and Pipeline Orchestration

### 80. What is Apache Airflow?

**Answer:**

Apache Airflow is an open-source workflow orchestration platform used to develop, schedule, and monitor workflows.

It is commonly used to coordinate Data Engineering pipelines.

---

### 81. Why is Airflow used?

**Answer:**

Airflow is used to:

- Schedule pipelines
- Define task dependencies
- Monitor workflows
- Retry failed tasks
- Manage complex workflows

Example:

```text
Extract
  ↓
Transform
  ↓
Load
  ↓
Validate
```

---

### 82. What is a DAG?

**Answer:**

DAG stands for **Directed Acyclic Graph**.

In Airflow, a DAG defines the workflow structure, including tasks and their dependencies.

---

### 83. What does DAG stand for?

**Answer:**

DAG stands for:

```text
D → Directed
A → Acyclic
G → Graph
```

Directed means tasks have an execution direction.

Acyclic means the workflow should not contain a cycle.

---

### 84. What is a Task in Airflow?

**Answer:**

A Task is an individual unit of work in an Airflow workflow.

Example:

```text
Task 1 → Extract Data
Task 2 → Transform Data
Task 3 → Load Data
```

---

### 85. What is an Operator?

**Answer:**

An Operator defines what a task should do in Airflow.

Examples include operators for:

```text
Python
Bash
SQL
AWS services
```

---

### 86. Task vs Operator?

**Answer:**

An Operator is a template/class that defines an operation, while a Task is a specific instance of that operation inside a DAG.

Simple way to remember:

```text
Operator
→ Defines the work

Task
→ Specific execution of that work
```

---

### 87. What are task dependencies?

**Answer:**

Task dependencies define the order in which tasks should execute.

Example:

```text
Extract
   ↓
Transform
   ↓
Load
```

Transform depends on Extract, and Load depends on Transform.

---

### 88. How do you define task dependencies?

**Answer:**

Airflow allows dependencies to be defined using operators such as:

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

---

### 89. What is scheduling in Airflow?

**Answer:**

Scheduling determines when a DAG should run.

For example, a pipeline can be scheduled to run:

```text
Every hour
Every day
Every week
```

---

### 90. What is a Retry?

**Answer:**

A Retry allows Airflow to execute a failed task again automatically.

It is useful when failures are temporary, such as:

```text
Temporary network issue
Temporary service unavailability
Temporary connection failure
```

---

### 91. What happens when an Airflow task fails?

**Answer:**

Depending on the configuration:

```text
Task fails
   ↓
Retry if configured
   ↓
If retries fail
   ↓
Task remains failed
   ↓
Downstream tasks may not execute
```

The failure can then be investigated using Airflow logs and monitoring.

---

### 92. What is Backfill?

**Answer:**

Backfill means running a pipeline for historical dates or periods that were missed or need to be reprocessed.

Example:

```text
Daily pipeline failed for:
August 20
August 21
August 22

Backfill
→ Process those historical dates
```

---

### 93. What is Catchup?

**Answer:**

Catchup is an Airflow behavior where scheduled DAG runs that were missed from the start date can be created and executed for past periods, depending on DAG configuration.

It is useful when historical scheduled runs need to be generated.

---

### 94. What is XCom?

**Answer:**

XCom stands for **Cross-Communication**.

It allows Airflow tasks to exchange small pieces of information.

Example:

```text
Task 1
→ Produces file path

Task 2
→ Reads that file path
```

---

### 95. Why should XCom not be used for large datasets?

**Answer:**

XCom is designed for passing small pieces of metadata between tasks, not for transferring large datasets.

Large datasets should be stored in systems such as:

```text
S3
Database
Data Warehouse
```

and tasks should pass references such as file paths or IDs.

---

### 96. What is a Sensor?

**Answer:**

A Sensor is an Airflow task that waits for a condition or event to occur.

Example:

```text
Wait for file in S3
        ↓
File arrives
        ↓
Continue pipeline
```

---

### 97. Airflow vs PySpark?

**Answer:**

They solve different problems.

```text
Airflow
→ Workflow orchestration

PySpark
→ Distributed data processing
```

Example:

```text
Airflow
   ↓
Triggers PySpark Job
   ↓
PySpark processes data
```

---

# 5. Data Pipeline Scenarios

## Scenario 1: Design a Data Pipeline

### 98. How would you design an end-to-end data pipeline?

**Answer:**

A simple architecture could be:

```text
Source
  ↓
Ingestion
  ↓
S3 Raw
  ↓
Transformation
  ↓
S3 Processed
  ↓
Data Warehouse
  ↓
Analytics
```

For example, AWS services could be:

```text
Source
  ↓
S3
  ↓
Glue / PySpark
  ↓
S3 Processed
  ↓
Redshift
  ↓
Analytics
```

Airflow can orchestrate the workflow and CloudWatch can help with monitoring.

---

## Scenario 2: Pipeline Failure

### 99. What would you do if a pipeline fails?

**Answer:**

I would follow these steps:

```text
1. Identify the failed task.
2. Check the logs.
3. Find the root cause.
4. Determine whether the failure is transient.
5. Retry if appropriate.
6. Fix the issue.
7. Rerun or backfill affected data.
8. Validate the output.
```

---

## Scenario 3: Duplicate Data

### 100. What would you do if the same data is loaded twice?

**Answer:**

First, I would identify why duplicate data was created.

Possible solutions include:

```text
Unique keys
Deduplication
MERGE / UPSERT
Idempotent processing
Tracking processed records
```

I would also modify the pipeline so that reprocessing does not create duplicates.

---

## Scenario 4: Idempotency

### 101. What is idempotency?

**Answer:**

Idempotency means that performing the same operation multiple times produces the same final result as performing it once.

Example:

```text
Run pipeline once
→ 1,000 records

Run same pipeline again
→ Still 1,000 correct records
```

It should not create another 1,000 duplicate records.

---

### 102. Why is idempotency important in Data Engineering?

**Answer:**

Pipelines can fail and may need to be retried or reprocessed.

Without idempotency, retries can create:

```text
Duplicate records
Incorrect totals
Inconsistent data
```

Idempotent pipelines are safer to retry.

---

### 103. How would you make a pipeline idempotent?

**Answer:**

Possible approaches include:

```text
Use unique keys
Use MERGE / UPSERT
Deduplicate input
Overwrite deterministic partitions
Track processed files/records
Use batch IDs
```

The exact approach depends on the pipeline architecture.

---

## Scenario 5: Late Data

### 104. What is late-arriving data?

**Answer:**

Late-arriving data is data that belongs to an earlier time period but arrives after the expected processing time.

Example:

```text
Data belongs to August 20
Expected arrival → August 20
Actual arrival → August 22
```

---

### 105. How would you handle late-arriving data?

**Answer:**

I would use techniques such as:

```text
Watermarks
Reprocessing
Backfill
Partition updates
```

The pipeline should identify the affected time period and update the corresponding data.

---

## Scenario 6: Schema Change

### 106. What happens if the source schema changes?

**Answer:**

A schema change can cause a pipeline to fail or produce incorrect results if the pipeline expects the old schema.

For example:

```text
Old:
id, name, age

New:
id, name, age, email
```

The pipeline should detect and handle the change appropriately.

---

### 107. How would you handle schema evolution?

**Answer:**

I would use:

```text
Schema validation
Schema evolution rules
Versioning
Backward compatibility
Alerts
```

I would first identify whether the change is compatible with existing processing before updating the pipeline.

---

## Scenario 7: Incremental Pipeline

### 108. How would you design an incremental pipeline?

**Answer:**

A typical approach is:

```text
Source
  ↓
Find new/changed records
  ↓
Transform
  ↓
Validate
  ↓
Load
  ↓
Update watermark
```

For example, a timestamp can be stored as a watermark.

```text
last_processed_time
```

The next run processes only records after that point.

---

## Scenario 8: Data Quality

### 109. How would you ensure data quality in a pipeline?

**Answer:**

I would implement validation checks such as:

```text
NULL checks
Duplicate checks
Data type checks
Range checks
Record count checks
Uniqueness checks
```

Example:

```text
customer_id → NOT NULL
age → >= 0
order_id → UNIQUE
```

Invalid records can be rejected, quarantined, or sent for further investigation depending on the requirements.

---

## Scenario 9: Large Dataset

### 110. How would you process a very large dataset?

**Answer:**

I would use distributed processing and optimize the data layout.

Important techniques include:

```text
Distributed processing
Partitioning
Parquet
Filtering early
Selecting required columns
Incremental processing
Efficient joins
```

For example, PySpark can distribute processing across multiple machines.

---

## Scenario 10: Slow Pipeline

### 111. What would you do if a pipeline suddenly becomes slow?

**Answer:**

I would investigate:

```text
Data volume
Partitioning
Shuffle
Data skew
Join strategy
Resource utilization
Query performance
External service latency
```

I would compare the current execution with previous successful runs to identify what changed.

---

# 6. Project-Based Questions

> These questions are **very important** if you have a Data Engineering project on your resume.
>
> Your answers should be based on your **actual project**. Do not claim that you implemented something if you did not.

---

### 112. Explain your Data Engineering project.

**Answer:**

A good answer should follow this structure:

```text
1. What was the project?
2. What was the data source?
3. How was the data ingested?
4. Where was raw data stored?
5. How was it transformed?
6. Where was processed data stored?
7. How was it queried?
8. How was the pipeline monitored?
9. What challenges did you solve?
```

Example:

> "I built a Data Engineering pipeline where data was collected from the source and stored in S3. I used AWS Glue with PySpark to clean and transform the data and stored the processed data back in S3. I used Athena or Redshift for analytics and used monitoring and logging to identify pipeline issues."

---

### 113. What was the source of your data?

**Answer:**

The answer should describe the actual source used in your project.

Possible sources include:

```text
API
Database
CSV files
JSON files
Application logs
Streaming platform
```

Example:

> "The source data was provided as CSV files. I uploaded the raw files into the S3 raw-data layer before processing them."

---

### 114. How did you ingest the data?

**Answer:**

Explain the actual method used to move data from the source into your storage layer.

For example:

```text
Source
  ↓
AWS CLI / SDK / Application
  ↓
S3
```

If your project uses a different ingestion method, explain that instead.

---

### 115. Where did you store the raw data?

**Answer:**

A typical AWS Data Engineering project stores raw data in Amazon S3.

Example:

```text
S3
└── raw/
    ├── customers/
    └── orders/
```

---

### 116. Why did you choose S3?

**Answer:**

I chose S3 because it provides scalable object storage and can store large datasets in different formats.

It is also commonly used as the storage layer for Data Lakes and integrates with services such as Glue and Athena.

---

### 117. How did you transform the data?

**Answer:**

I transformed the data using operations such as:

```text
Filtering
Cleaning
Joining
Aggregating
Handling NULL values
Removing duplicates
Changing data types
```

If PySpark was used:

```text
S3 Raw
   ↓
PySpark
   ↓
Transformations
   ↓
S3 Processed
```

---

### 118. Why did you use PySpark?

**Answer:**

PySpark provides distributed data processing capabilities and is suitable for processing large datasets.

It allows transformations to be executed across a cluster rather than depending only on one machine.

---

### 119. Where did you store the processed data?

**Answer:**

The answer should describe the actual architecture.

A common design is:

```text
S3
├── raw/
├── processed/
└── curated/
```

Processed data can also be loaded into a Data Warehouse such as Redshift depending on the project.

---

### 120. Why did you use Parquet?

**Answer:**

I used Parquet because it is a columnar storage format that is efficient for analytical workloads.

It provides:

```text
Columnar storage
Compression
Efficient column reads
Schema information
```

This can reduce the amount of data that needs to be scanned during analytical queries.

---

### 121. Did you implement incremental loading?

**Answer:**

If you implemented it, explain the method used.

Example:

> "Yes. I used a timestamp/watermark to identify new or changed records and processed only those records instead of processing the complete dataset every time."

If you did not implement it:

> "No. The current version of my project uses a full load. I understand that incremental loading would be more efficient for large datasets."

---

### 122. How did you handle duplicate records?

**Answer:**

I would identify duplicates using an appropriate business key or unique identifier and then apply deduplication logic.

Possible methods:

```text
DISTINCT
Window functions
Unique keys
MERGE / UPSERT
```

The exact method depends on the project.

---

### 123. How did you handle NULL values?

**Answer:**

I first identify whether NULL is valid or represents missing/invalid data.

Possible approaches include:

```text
Keep NULL
Replace with a default value
Remove invalid records
Fill using business rules
```

For example, a missing optional field can remain NULL, while a required ID should generally be validated.

---

### 124. How did you handle data-quality issues?

**Answer:**

I would implement checks such as:

```text
NULL checks
Duplicate checks
Data type validation
Range validation
Uniqueness checks
Record count checks
```

Invalid records can be rejected or separated for further investigation.

---

### 125. How did you handle pipeline failures?

**Answer:**

I would:

```text
1. Identify the failed task.
2. Check logs.
3. Find the root cause.
4. Determine whether it is transient.
5. Retry if appropriate.
6. Fix the issue.
7. Rerun or backfill affected data.
8. Validate the output.
```

---

### 126. How did you monitor your pipeline?

**Answer:**

I would use the monitoring and logging capabilities of the services involved.

For AWS pipelines, CloudWatch can be used for:

```text
Logs
Metrics
Errors
Alarms
Resource monitoring
```

Airflow can also provide workflow-level monitoring if it is used for orchestration.

---

### 127. Why did you choose AWS Glue?

**Answer:**

I chose AWS Glue because it provides managed data integration and ETL capabilities.

It can work with S3 and use Spark/PySpark for distributed data processing.

---

### 128. Why did you use Redshift?

**Answer:**

I used Redshift when a dedicated analytical Data Warehouse was required.

It is designed for analytical workloads such as:

```text
Reporting
Dashboards
Aggregations
Business Intelligence
```

---

### 129. Why did you use Athena?

**Answer:**

I used Athena when I needed to query data stored in S3 directly using SQL without loading it into a traditional database.

---

### 130. Explain your complete pipeline from source to destination.

**Answer:**

A typical answer is:

```text
Source
  ↓
Data Ingestion
  ↓
S3 Raw
  ↓
AWS Glue / PySpark
  ↓
Data Transformation
  ↓
S3 Processed
  ↓
Athena / Redshift
  ↓
Analytics
```

I would then explain what each component does in my actual project.

---

# 7. High-Priority Comparison Questions

### 131. ETL vs ELT?

**Answer:**

```text
ETL
→ Extract → Transform → Load

ELT
→ Extract → Load → Transform
```

ETL transforms before loading, while ELT loads data first and performs transformation later.

---

### 132. Batch vs Streaming?

**Answer:**

```text
Batch
→ Process data periodically in groups

Streaming
→ Process data continuously as it arrives
```

Batch is suitable for periodic processing, while streaming is suitable for low-latency use cases.

---

### 133. Full Load vs Incremental Load?

**Answer:**

```text
Full Load
→ Process all records

Incremental Load
→ Process only new/changed records
```

Incremental loading is generally more efficient for large datasets.

---

### 134. Data Warehouse vs Data Lake?

**Answer:**

```text
Data Warehouse
→ Structured, processed data
→ Analytics and reporting

Data Lake
→ Raw + processed data
→ Multiple data formats
→ Analytics and processing
```

---

### 135. Data Lake vs Data Lakehouse?

**Answer:**

```text
Data Lake
→ Flexible large-scale data storage

Data Lakehouse
→ Data Lake flexibility
  +
  Data Warehouse-style analytical capabilities
```

A Lakehouse aims to combine benefits of both architectures.

---

### 136. OLTP vs OLAP?

**Answer:**

```text
OLTP
→ Transaction processing

OLAP
→ Analytical processing
```

Example:

```text
OLTP
→ Place an online order

OLAP
→ Analyze monthly sales
```

---

### 137. Fact Table vs Dimension Table?

**Answer:**

```text
Fact Table
→ Measures / business events

Dimension Table
→ Descriptive attributes
```

Example:

```text
Fact
→ sales_amount

Dimension
→ customer_name, city
```

---

### 138. Star Schema vs Snowflake Schema?

**Answer:**

```text
Star Schema
→ Simpler dimensions
→ Fewer joins

Snowflake Schema
→ More normalized dimensions
→ More joins
```

---

### 139. Surrogate Key vs Natural Key?

**Answer:**

```text
Surrogate Key
→ Artificial identifier

Natural Key
→ Business identifier
```

Example:

```text
Surrogate:
customer_sk = 101

Natural:
customer_id = CUST1001
```

---

### 140. S3 vs Redshift?

**Answer:**

```text
S3
→ Object Storage / Data Lake

Redshift
→ Data Warehouse
```

S3 stores data, while Redshift is optimized for analytical querying and warehousing.

---

### 141. Athena vs Redshift?

**Answer:**

```text
Athena
→ Query data directly in S3

Redshift
→ Dedicated Data Warehouse
```

Athena is useful for ad-hoc querying of S3 data, while Redshift is suitable for dedicated analytical workloads.

---

### 142. Glue Crawler vs Glue Job?

**Answer:**

```text
Glue Crawler
→ Discovers schema and metadata

Glue Job
→ Processes and transforms data
```

---

### 143. IAM User vs IAM Role?

**Answer:**

```text
IAM User
→ Represents an identity

IAM Role
→ Assumable identity with permissions
```

Roles are commonly used by AWS services to access other AWS services.

---

### 144. Airflow vs PySpark?

**Answer:**

```text
Airflow
→ Orchestrates workflows

PySpark
→ Processes large datasets
```

They are complementary rather than direct alternatives.

Example:

```text
Airflow
   ↓
Trigger PySpark
   ↓
Process Data
```

---

### 145. CSV vs Parquet?

**Answer:**

```text
CSV
→ Row-oriented text format
→ Simple and portable

Parquet
→ Columnar format
→ Efficient for analytical workloads
→ Supports compression
```

For large analytical datasets, Parquet is generally more suitable.

---

# 8. ⭐ Top 30 Questions to Prepare First

> If you have very limited time, prepare these first. You should be able to explain each answer in a few simple sentences and connect it to your project.

### 1. What is Data Engineering?

**Answer:**

Data Engineering is the process of collecting, storing, processing, transforming, and delivering data for analytics and other use cases.

---

### 2. What does a Data Engineer do?

**Answer:**

A Data Engineer builds and maintains data pipelines and data infrastructure. They work with ingestion, transformation, storage, data quality, orchestration, and monitoring.

---

### 3. What is a data pipeline?

**Answer:**

A data pipeline is a sequence of steps that moves data from a source to a destination while performing required processing or transformations.

---

### 4. What is ETL?

**Answer:**

ETL means Extract, Transform, Load. Data is extracted from the source, transformed, and then loaded into the target system.

---

### 5. ETL vs ELT?

**Answer:**

ETL transforms data before loading it, while ELT loads data first and transforms it later.

---

### 6. Batch vs Streaming?

**Answer:**

Batch processing processes data periodically in groups, while streaming processes data continuously as it arrives.

---

### 7. Full Load vs Incremental Load?

**Answer:**

Full load processes all available data, while incremental load processes only new or changed data.

---

### 8. How do you implement incremental loading?

**Answer:**

A common approach is to use a timestamp, increasing ID, or CDC mechanism to identify new or changed records. The pipeline processes those records and updates the watermark after successful processing.

---

### 9. What is CDC?

**Answer:**

CDC stands for Change Data Capture. It identifies changes such as inserts, updates, and deletes in a source so that only changed data needs to be processed.

---

### 10. What is a Data Warehouse?

**Answer:**

A Data Warehouse is a centralized system that stores structured data for analytics, reporting, and business intelligence.

---

### 11. What is a Data Lake?

**Answer:**

A Data Lake stores large amounts of raw and processed data in different formats such as CSV, JSON, and Parquet.

---

### 12. Data Warehouse vs Data Lake?

**Answer:**

A Data Warehouse mainly stores structured and processed data for analytics, while a Data Lake can store raw and processed data in multiple formats.

---

### 13. OLTP vs OLAP?

**Answer:**

OLTP is designed for transactional operations such as orders and payments. OLAP is designed for analytical queries such as reports and sales analysis.

---

### 14. What is a Fact Table?

**Answer:**

A Fact Table stores measurable business events or metrics, such as sales amount, quantity, or transaction count.

---

### 15. What is a Dimension Table?

**Answer:**

A Dimension Table stores descriptive information such as customer, product, location, or date details.

---

### 16. Star Schema vs Snowflake Schema?

**Answer:**

Star Schema has a central fact table connected to relatively simple dimension tables. Snowflake Schema further normalizes dimensions, which can result in more tables and joins.

---

### 17. What is Parquet?

**Answer:**

Parquet is a columnar storage file format designed for efficient analytical processing. It supports compression and efficient column-level reads.

---

### 18. Why is Parquet used?

**Answer:**

Parquet is used because it is efficient for analytical workloads, supports compression, and allows engines to read only the required columns.

---

### 19. What is Amazon S3?

**Answer:**

Amazon S3 is an object storage service commonly used to store raw, processed, and curated Data Lake data.

---

### 20. What is AWS Glue?

**Answer:**

AWS Glue is a managed serverless data integration and ETL service that can use Spark/PySpark for data processing.

---

### 21. Glue Crawler vs Glue Job?

**Answer:**

A Glue Crawler discovers schema and metadata, while a Glue Job performs data processing and transformation.

---

### 22. What is Glue Data Catalog?

**Answer:**

Glue Data Catalog is a centralized metadata repository that stores information about tables, columns, data types, locations, and partitions.

---

### 23. What is Amazon Athena?

**Answer:**

Athena is a serverless query service that allows SQL queries to be run directly against data stored in S3.

---

### 24. What is Amazon Redshift?

**Answer:**

Redshift is a cloud Data Warehouse designed for analytical workloads, reporting, and business intelligence.

---

### 25. What is Apache Airflow?

**Answer:**

Apache Airflow is a workflow orchestration platform used to schedule, execute, monitor, and manage data pipelines.

---

### 26. What is a DAG?

**Answer:**

A DAG is a Directed Acyclic Graph that defines tasks and their dependencies in an Airflow workflow.

---

### 27. Airflow vs PySpark?

**Answer:**

Airflow is used for workflow orchestration, while PySpark is used for distributed data processing.

---

### 28. What is idempotency?

**Answer:**

Idempotency means running the same operation multiple times produces the same final result as running it once.

---

### 29. How would you handle a failed pipeline?

**Answer:**

I would identify the failed task, check the logs, find the root cause, retry if the failure is transient, fix the issue, rerun or backfill affected data, and validate the output.

---

### 30. Explain your complete Data Engineering project.

**Answer:**

A good structure is:

```text
Source
  ↓
Ingestion
  ↓
S3 Raw
  ↓
Glue / PySpark
  ↓
Transformation
  ↓
S3 Processed
  ↓
Athena / Redshift
  ↓
Analytics
```

Then explain the actual technologies, transformations, challenges, and results from your project.

---

# 9. ⭐ Top Scenario Questions

## 1. Design an end-to-end data pipeline.

**Answer:**

I would first identify the source and ingestion method, then store the raw data, transform it, validate it, and load it into an analytical target.

Example:

```text
Source
  ↓
Ingestion
  ↓
S3 Raw
  ↓
Glue / PySpark
  ↓
S3 Processed
  ↓
Redshift
  ↓
Analytics
```

Airflow can orchestrate the pipeline and CloudWatch can monitor it.

---

## 2. Your pipeline failed. What will you do?

**Answer:**

I would check which task failed, inspect its logs, identify the root cause, determine whether it is transient, retry if appropriate, fix the issue, rerun the affected part, and validate the output.

---

## 3. Your pipeline ran twice and created duplicate records. How will you fix it?

**Answer:**

I would first identify why the pipeline was executed twice and then use a combination of:

```text
Unique keys
Deduplication
MERGE / UPSERT
Idempotent processing
Processed-record tracking
```

I would also modify the pipeline so that retries do not create duplicates.

---

## 4. The source schema changed. What will you do?

**Answer:**

I would detect the schema change using validation or metadata checks, determine whether it is backward compatible, update the transformation logic if required, test the pipeline, and monitor for further schema changes.

---

## 5. Data arrived late. How will you handle it?

**Answer:**

I would identify the time period affected by the late data and reprocess or update the relevant partition.

Depending on the system, I may use:

```text
Watermarks
Backfill
Partition updates
Reprocessing
```

---

## 6. How will you implement incremental loading?

**Answer:**

I would identify a reliable change indicator such as:

```text
updated_at
Increasing ID
CDC
```

Then:

```text
Read new/changed records
        ↓
Transform
        ↓
Validate
        ↓
Load
        ↓
Update watermark
```

---

## 7. How will you make your pipeline idempotent?

**Answer:**

I would make sure that rerunning the same input does not create duplicate or inconsistent results.

Possible methods include:

```text
Unique keys
MERGE / UPSERT
Deterministic partition overwrite
Deduplication
Processed-record tracking
```

---

## 8. How will you ensure data quality?

**Answer:**

I would add validation checks such as:

```text
NULL checks
Duplicate checks
Data type checks
Range checks
Uniqueness checks
Record count checks
```

I would also monitor failures and separate invalid data when appropriate.

---

## 9. Your pipeline became slow. How will you troubleshoot it?

**Answer:**

I would compare the current run with previous runs and investigate:

```text
Data volume
Partitioning
Shuffle
Data skew
Joins
Resource utilization
Query execution
External service latency
```

Then I would optimize the specific bottleneck instead of making random changes.

---

## 10. You need to process billions of records. How will you approach it?

**Answer:**

I would use distributed processing and avoid processing all data unnecessarily.

I would consider:

```text
PySpark / Distributed Processing
Partitioning
Parquet
Column pruning
Predicate filtering
Incremental processing
Efficient joins
```

---

## 11. How will you monitor a production pipeline?

**Answer:**

I would monitor:

```text
Task status
Execution time
Failures
Logs
Data quality
Record counts
Resource utilization
```

For AWS workloads, CloudWatch can be used for logs, metrics, and alarms. Airflow can provide workflow monitoring.

---

## 12. How will you recover from a failed pipeline?

**Answer:**

I would identify the failure point, determine the root cause, fix it, and rerun only the required portion where possible.

If historical periods were missed, I would use backfill or controlled reprocessing.

---

## 13. How will you prevent duplicate records during reprocessing?

**Answer:**

I would use idempotent processing with techniques such as:

```text
Unique business keys
Deduplication
MERGE / UPSERT
Deterministic partition overwrite
Processed-record tracking
```

---

## 14. How would you design a daily AWS data pipeline?

**Answer:**

One possible architecture is:

```text
Source
  ↓
S3 Raw
  ↓
AWS Glue / PySpark
  ↓
S3 Processed
  ↓
Athena / Redshift
  ↓
Analytics
```

Airflow can schedule and orchestrate the workflow if required.

---

## 15. Explain your project end-to-end.

**Answer:**

I would explain:

```text
1. Source
2. Ingestion
3. Raw storage
4. Transformation
5. Data quality
6. Processed storage
7. Warehouse/query layer
8. Orchestration
9. Monitoring
10. Challenges and solutions
```

The explanation should match what was actually implemented.

---

# 10. Final Revision Map

```text
DATA ENGINEERING
│
├── ETL / ELT
│   ├── Extraction
│   ├── Transformation
│   ├── Loading
│   ├── Batch
│   ├── Streaming
│   ├── Full Load
│   ├── Incremental Load
│   └── CDC
│
├── DATA STORAGE
│   ├── Data Warehouse
│   ├── Data Lake
│   ├── Data Lakehouse
│   ├── Fact Tables
│   ├── Dimension Tables
│   ├── Star Schema
│   ├── Snowflake Schema
│   └── Parquet
│
├── AWS
│   ├── S3
│   ├── IAM
│   ├── Glue
│   ├── Glue Crawler
│   ├── Glue Data Catalog
│   ├── Athena
│   ├── Redshift
│   ├── Lambda
│   └── CloudWatch
│
├── ORCHESTRATION
│   ├── Airflow
│   ├── DAG
│   ├── Tasks
│   ├── Operators
│   ├── Dependencies
│   ├── Scheduling
│   ├── Retries
│   ├── Backfill
│   └── Catchup
│
└── PIPELINE SCENARIOS
    ├── Failure Handling
    ├── Duplicate Data
    ├── Idempotency
    ├── Late Data
    ├── Schema Changes
    ├── Incremental Processing
    ├── Data Quality
    ├── Monitoring
    └── Performance
```

---

# 11. Final Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Data Engineering Basics
ETL / ELT
Batch vs Streaming
Full vs Incremental Load
Incremental Loading
CDC
Data Warehouse
Data Lake
OLTP vs OLAP
Fact Tables
Dimension Tables
Star Schema
Parquet
S3
IAM
AWS Glue
Glue Crawler
Glue Data Catalog
Athena
Redshift
Airflow
DAG
Pipeline Failures
Idempotency
Data Quality
End-to-End Pipeline
Project Explanation
```

## ⭐⭐⭐⭐ Prepare If Time Allows

```text
Data Lakehouse
Snowflake Schema
Surrogate Keys
Natural Keys
Lambda
CloudWatch
XCom
Sensors
Backfill
Catchup
Schema Evolution
Watermarks
Late-arriving Data
Pipeline Performance
Glue vs EMR
```

---

# 12. Interview Answer Strategy

For most fresher interview questions, use this structure:

```text
1. Give the definition.
2. Explain it in simple words.
3. Give a small example.
4. Connect it to your project if relevant.
```

Example:

### Question: What is incremental loading?

**Good Interview Answer:**

> "Incremental loading means processing only new or changed records instead of loading the complete dataset every time. For example, I can use an `updated_at` timestamp to identify records changed after the previous successful run. This reduces processing time and resource usage, especially when the dataset is large."

---

# 13. Final Preparation Checklist

Before attending a Data Engineer interview, make sure you can explain these without memorizing long definitions:

```text
☐ What is Data Engineering?
☐ What does a Data Engineer do?
☐ What is ETL?
☐ ETL vs ELT
☐ Batch vs Streaming
☐ Full vs Incremental Load
☐ Incremental Loading
☐ CDC
☐ Data Warehouse
☐ Data Lake
☐ OLTP vs OLAP
☐ Fact vs Dimension
☐ Star Schema
☐ Parquet
☐ Partitioning
☐ Partition Pruning
☐ S3
☐ IAM
☐ IAM Role
☐ Glue
☐ Glue Crawler
☐ Glue Data Catalog
☐ Athena
☐ Redshift
☐ Airflow
☐ DAG
☐ Airflow vs PySpark
☐ Idempotency
☐ Duplicate Handling
☐ Late Data
☐ Schema Evolution
☐ Data Quality
☐ Pipeline Failure Handling
☐ Pipeline Performance
☐ End-to-End Pipeline
☐ Your Project Architecture
☐ Why you selected each technology
```

> **Most important:** Do not memorize answers word-for-word. Understand the concepts well enough to explain them naturally in **2–5 sentences**, give a simple example, and explain how they apply to your project. The questions and topics in this file are the placement-focused set from the provided question bank. :contentReference[oaicite:0]{index=0}