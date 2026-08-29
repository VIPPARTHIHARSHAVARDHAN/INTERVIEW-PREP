# Data Engineering Basics and ETL

## 1. What is Data Engineering?

**Data Engineering** is the process of collecting, storing, transforming, and delivering data so that it can be used for analysis, reporting, and applications.

A Data Engineer typically works on:

```text
Data Sources
     ↓
Data Ingestion
     ↓
Data Storage
     ↓
Data Transformation
     ↓
Data Warehouse / Data Lake
     ↓
Analytics / BI / ML
```

---

# 2. What Does a Data Engineer Do?

Main responsibilities include:

```text
1. Collect data from different sources
2. Build data pipelines
3. Transform and clean data
4. Store data efficiently
5. Maintain data warehouses/lakes
6. Schedule and monitor pipelines
7. Handle failures and data-quality issues
8. Optimize pipeline performance
```

### Interview Answer

> A Data Engineer builds and maintains pipelines that collect, transform, store, and deliver data reliably for analytics and other business use cases.

---

# 3. What is a Data Pipeline?

A **data pipeline** is a series of steps that moves data from a source to a destination while performing required processing.

Example:

```text
MySQL
  ↓
Extract
  ↓
S3
  ↓
Transform
  ↓
Data Warehouse
  ↓
Dashboard
```

A pipeline can include:

```text
Extraction
Ingestion
Transformation
Validation
Storage
Loading
Monitoring
```

---

# 4. What is Data Ingestion?

**Data ingestion** is the process of collecting and moving data from source systems into a storage or processing system.

Examples of sources:

```text
Databases
APIs
CSV files
JSON files
Application logs
Streaming systems
```

Example:

```text
MySQL → S3
API → S3
CSV → Data Lake
```

---

# 5. Batch Processing

**Batch processing** processes data in groups at scheduled intervals.

Example:

```text
Every day at 12 AM

Source
  ↓
Collect today's data
  ↓
Process
  ↓
Store
```

Examples:

```text
Daily sales report
Daily ETL pipeline
Monthly billing processing
```

---

# 6. Streaming Processing

**Streaming processing** processes data continuously or with very low latency as it arrives.

Example:

```text
Event
 ↓
Streaming System
 ↓
Processing
 ↓
Output
```

Examples:

```text
Real-time transactions
IoT data
Application events
Real-time monitoring
```

---

# 7. Batch vs Streaming

| Batch | Streaming |
|---|---|
| Processes data in groups | Processes data continuously |
| Higher latency | Lower latency |
| Scheduled | Continuous/event-driven |
| Simpler to implement | More complex |
| Example: daily report | Example: real-time monitoring |

### Interview Answer

> Batch processing handles data at scheduled intervals, while streaming processes data continuously or with low latency as it arrives.

---

# 8. What is ETL?

**ETL** stands for:

```text
E → Extract
T → Transform
L → Load
```

The data is extracted from a source, transformed, and then loaded into the target system.

```text
Source
  ↓
Extract
  ↓
Transform
  ↓
Load
  ↓
Target
```

---

# 9. Extract

Extraction means retrieving data from a source system.

Examples:

```text
MySQL
PostgreSQL
REST API
CSV
JSON
Application logs
```

Example:

```text
MySQL → Extract customer data
```

---

# 10. Transform

Transformation means changing data into the required format.

Common transformations:

```text
Remove duplicates
Handle NULL values
Change data types
Filter records
Join datasets
Aggregate data
Rename columns
Apply business rules
```

Example:

```text
Raw salary = "50000"
        ↓
Convert to numeric
        ↓
50000
```

---

# 11. Load

Loading means putting transformed data into the target system.

Examples:

```text
S3
Data Warehouse
Database
Data Lake
```

Example:

```text
Source
 ↓
Extract
 ↓
Transform
 ↓
Load
 ↓
Redshift
```

---

# 12. ETL Example

Suppose a company has customer data in MySQL.

The requirement is to create a daily analytics table.

```text
MySQL
  ↓
Extract customer data
  ↓
Remove duplicate customers
  ↓
Handle NULL values
  ↓
Apply business rules
  ↓
Load into Data Warehouse
```

This is an ETL pipeline.

---

# 13. What is ELT?

**ELT** stands for:

```text
E → Extract
L → Load
T → Transform
```

In ELT, raw data is first loaded into the target storage system and transformations happen afterward.

```text
Source
  ↓
Extract
  ↓
Load
  ↓
Data Lake / Warehouse
  ↓
Transform
  ↓
Analytics
```

---

# 14. ETL vs ELT

| ETL | ELT |
|---|---|
| Extract → Transform → Load | Extract → Load → Transform |
| Transformation happens before loading | Transformation happens after loading |
| Target receives transformed data | Target can store raw data first |
| Traditionally common with traditional warehouses | Common with modern cloud data platforms |

### Easy Memory Trick

```text
ETL → Transform before Load

ELT → Transform after Load
```

---

# 15. When Would You Use ETL?

ETL can be useful when:

```text
Data must be transformed before entering the target
Target storage has limited processing capability
Strict preprocessing is required
```

---

# 16. When Would You Use ELT?

ELT is useful when:

```text
Target system has strong processing capabilities
You want to retain raw data
Large-scale transformations are performed in the target
```

---

# 17. Full Load

A **full load** loads the complete dataset from the source into the target.

Example:

```text
Source
1 million rows
     ↓
Load all 1 million rows
     ↓
Target
```

It is simple but can be expensive for large datasets.

---

# 18. Incremental Load

An **incremental load** processes only new or changed records instead of loading the entire dataset every time.

Example:

```text
Day 1 → Load 1,000,000 rows

Day 2 → Load only 5,000 new/changed rows
```

This can significantly reduce:

```text
Processing time
Data movement
Cost
```

---

# 19. Full Load vs Incremental Load

| Full Load | Incremental Load |
|---|---|
| Loads all data | Loads only new/changed data |
| Simple | More complex |
| More processing | Less processing |
| Can be expensive | Usually more efficient |
| Useful for small datasets | Useful for large datasets |

---

# 20. How Can Incremental Loading Be Implemented?

Common approaches include:

```text
Timestamp column
Incrementing ID
Change Data Capture (CDC)
Last modified timestamp
Source-system change tracking
```

Example:

```sql
SELECT *
FROM employees
WHERE updated_at > '2026-08-28 00:00:00';
```

Only records modified after the previous successful load are processed.

---

# 21. What is Change Data Capture (CDC)?

**Change Data Capture** is a technique used to identify changes made to source data.

Changes can include:

```text
INSERT
UPDATE
DELETE
```

Instead of repeatedly reading the entire source table, a pipeline can process only the changes.

---

# 22. Structured Data

Structured data has a predefined schema.

Examples:

```text
SQL tables
Relational databases
```

Example:

```text
id | name   | salary
---|--------|-------
1  | Harsha | 50000
2  | Rahul  | 60000
```

---

# 23. Semi-Structured Data

Semi-structured data does not follow a strict tabular structure but contains organizational information such as keys and values.

Examples:

```text
JSON
XML
```

Example:

```json
{
  "id": 1,
  "name": "Harsha",
  "salary": 50000
}
```

---

# 24. Unstructured Data

Unstructured data does not have a predefined tabular structure.

Examples:

```text
Images
Videos
Audio
Documents
```

---

# 25. Structured vs Semi-Structured vs Unstructured

| Type | Examples |
|---|---|
| Structured | SQL tables |
| Semi-structured | JSON, XML |
| Unstructured | Images, videos, audio |

---

# 26. What is Data Transformation?

Data transformation converts raw data into a format suitable for analysis or downstream processing.

Examples:

```text
Filtering
Joining
Aggregating
Cleaning
Type conversion
Deduplication
Formatting
Business-rule application
```

---

# 27. What is Data Cleaning?

Data cleaning identifies and fixes problems in raw data.

Common problems:

```text
NULL values
Duplicate records
Invalid values
Incorrect data types
Inconsistent formats
Missing records
```

Example:

```text
"India"
"india"
"INDIA"
```

can be standardized to:

```text
India
```

---

# 28. What is Data Validation?

Data validation checks whether data meets expected rules before it is accepted by the pipeline.

Examples:

```text
ID should not be NULL
Salary should be positive
Email should have valid format
Expected columns should exist
Record count should be within expected range
```

---

# 29. What is a Data Warehouse?

A **Data Warehouse** is a centralized system designed primarily for analytics and reporting.

It typically stores processed and structured data.

Example:

```text
Operational Databases
        ↓
      ETL/ELT
        ↓
Data Warehouse
        ↓
BI / Reporting
```

Examples:

```text
Amazon Redshift
Snowflake
Google BigQuery
```

---

# 30. What is a Data Lake?

A **Data Lake** is a storage system that can store large amounts of raw data in different formats.

It can contain:

```text
CSV
JSON
Parquet
Logs
Images
Videos
```

A common cloud example is:

```text
Amazon S3
```

---

# 31. Data Warehouse vs Data Lake

| Data Warehouse | Data Lake |
|---|---|
| Mainly structured/processed data | Can store raw and varied data |
| Analytics focused | Storage for many data types/use cases |
| Strong schema/structure | More flexible schema |
| Typically queried directly for BI | Often requires processing/query engines |

### Easy Memory Trick

```text
Warehouse → Organized analytics data

Lake → Large collection of raw/varied data
```

---

# 32. Basic Data Engineering Architecture

A common architecture looks like:

```text
        DATA SOURCES
             ↓
    ┌─────────────────┐
    │ MySQL / API /   │
    │ CSV / JSON      │
    └─────────────────┘
             ↓
        INGESTION
             ↓
        DATA LAKE
             ↓
      TRANSFORMATION
             ↓
     DATA WAREHOUSE
             ↓
      BI / ANALYTICS
```

AWS example:

```text
MySQL / API
     ↓
AWS Glue
     ↓
Amazon S3
     ↓
PySpark
     ↓
Amazon Redshift
     ↓
Athena / BI
```

---

# 33. What Makes a Good Data Pipeline?

A good pipeline should be:

```text
Reliable
Scalable
Maintainable
Fault-tolerant
Monitored
Efficient
```

It should also handle:

```text
Failures
Duplicate data
Missing data
Schema changes
Large volumes of data
```

---

# 34. Common Data Engineering Interview Questions

```text
1. What is Data Engineering?

2. What does a Data Engineer do?

3. What is a data pipeline?

4. What are the main components of a data pipeline?

5. What is data ingestion?

6. What is ETL?

7. Explain Extract, Transform and Load.

8. What is ELT?

9. ETL vs ELT?

10. When would you choose ETL over ELT?

11. When would you choose ELT?

12. What is batch processing?

13. What is streaming?

14. Batch vs streaming?

15. What is full load?

16. What is incremental load?

17. Full load vs incremental load?

18. How do you implement incremental loading?

19. What is CDC?

20. What is data transformation?

21. What is data cleaning?

22. What is data validation?

23. What is structured data?

24. What is semi-structured data?

25. What is unstructured data?

26. Structured vs semi-structured vs unstructured data?

27. What is a data warehouse?

28. What is a data lake?

29. Data warehouse vs data lake?

30. What makes a good data pipeline?
```

---

# 35. ⭐ Most Important Questions

If you have limited time, prepare these first:

```text
1. What is Data Engineering?

2. What does a Data Engineer do?

3. What is a data pipeline?

4. What is ETL?

5. ETL vs ELT?

6. What is data ingestion?

7. Batch vs streaming?

8. Full load vs incremental load?

9. How do you implement incremental loading?

10. What is CDC?

11. What is data transformation?

12. What is data cleaning?

13. What is data validation?

14. Data warehouse vs data lake?

15. What is structured, semi-structured and unstructured data?

16. Explain a basic data engineering pipeline.
```

---

# 36. Quick Revision

```text
DATA ENGINEERING
→ Collect, process, store and deliver data

DATA PIPELINE
→ Moves data from source to destination

DATA INGESTION
→ Collects/moves data into a storage or processing system

ETL
→ Extract → Transform → Load

ELT
→ Extract → Load → Transform

BATCH
→ Processes data in groups

STREAMING
→ Processes data continuously / with low latency

FULL LOAD
→ Load all data

INCREMENTAL LOAD
→ Load only new/changed data

CDC
→ Captures INSERT/UPDATE/DELETE changes

DATA CLEANING
→ Fix data-quality problems

DATA VALIDATION
→ Check whether data meets expected rules

STRUCTURED
→ SQL tables

SEMI-STRUCTURED
→ JSON/XML

UNSTRUCTURED
→ Images/videos/audio/documents

DATA WAREHOUSE
→ Analytics-focused structured/processed data

DATA LAKE
→ Large-scale storage for raw and varied data
```

---

# 37. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
Data Engineering
Data Pipeline
ETL
ELT
ETL vs ELT
Data Ingestion
Batch vs Streaming
Full vs Incremental Load
CDC
Data Warehouse
Data Lake
Warehouse vs Lake
```

## ⭐⭐⭐⭐ Good to Know

```text
Data Cleaning
Data Validation
Data Types
Pipeline reliability
Basic pipeline architecture
```

> **For a fresher interview, understand these concepts and be able to explain one real pipeline end-to-end. You do not need deep distributed-system theory in this file because Python, SQL, DBMS, PySpark, and other core topics are already covered separately in your preparation.**