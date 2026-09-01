# Data Warehousing and Data Lakes

## 1. What is a Data Warehouse?

A **Data Warehouse** is a centralized system used to store structured, processed, and historical data mainly for **analytics and reporting**.

A typical flow is:

```text
Operational Sources
        ↓
     ETL / ELT
        ↓
  Data Warehouse
        ↓
 Analytics / BI
```

Examples:

```text
Amazon Redshift
Snowflake
Google BigQuery
```

---

# 2. Why is a Data Warehouse Used?

A data warehouse is mainly used for:

```text
Reporting
Business Intelligence
Analytics
Historical analysis
Aggregations
Decision making
```

It is designed primarily for analytical workloads rather than day-to-day transactional operations.

---

# 3. What is OLTP?

**OLTP** stands for **Online Transaction Processing**.

OLTP systems handle day-to-day business transactions.

Examples:

```text
Bank transaction
Online order
Payment
Customer registration
Inventory update
```

Characteristics:

```text
Frequent INSERT / UPDATE / DELETE
Many small transactions
Fast transaction processing
Current operational data
```

Examples:

```text
MySQL
PostgreSQL
Oracle
```

---

# 4. What is OLAP?

**OLAP** stands for **Online Analytical Processing**.

OLAP systems are designed for analyzing large amounts of data.

Examples:

```text
Sales analysis
Monthly revenue
Customer analysis
Business reports
Trend analysis
```

Characteristics:

```text
Large queries
Aggregations
Historical data
Read-heavy workloads
Analytics and reporting
```

---

# 5. OLTP vs OLAP

| OLTP | OLAP |
|---|---|
| Transaction processing | Analytical processing |
| Day-to-day operations | Reporting and analysis |
| Many small transactions | Complex analytical queries |
| Frequent INSERT/UPDATE/DELETE | Mostly read/aggregation workloads |
| Current operational data | Historical/analytical data |
| Example: MySQL | Example: Redshift |

### Easy Memory Trick

```text
OLTP → Transactions

OLAP → Analysis
```

---

# 6. What is a Data Lake?

A **Data Lake** is a centralized storage system that can store large amounts of data in its raw or processed form.

It can store:

```text
Structured data
Semi-structured data
Unstructured data
```

Examples:

```text
CSV
JSON
Parquet
Logs
Images
Videos
```

A common cloud-based data lake storage solution is:

```text
Amazon S3
```

---

# 7. Why is a Data Lake Used?

A data lake is useful when you need:

```text
Large-scale storage
Flexible data formats
Raw data storage
Historical data
Data for analytics
Data for machine learning
```

---

# 8. Data Warehouse vs Data Lake

| Data Warehouse | Data Lake |
|---|---|
| Mainly stores structured/processed data | Can store raw and varied data |
| Analytics focused | Flexible storage for many use cases |
| More structured | More flexible |
| Schema is usually defined before/around loading/querying | Can defer schema interpretation |
| Mainly BI and reporting | Analytics, processing, ML, and other use cases |
| Example: Redshift | Example: S3 |

### Easy Memory Trick

```text
Warehouse → Organized analytical data

Lake → Raw + varied data
```

---

# 9. What is a Data Lakehouse?

A **Data Lakehouse** combines important characteristics of data lakes and data warehouses.

Conceptually:

```text
Data Lake
   +
Warehouse-like capabilities
   ↓
Data Lakehouse
```

It aims to provide:

```text
Flexible data storage
+
Analytical capabilities
+
Better data management
```

---

# 10. Data Lake vs Data Lakehouse

```text
Data Lake
→ Primarily flexible large-scale storage

Data Lakehouse
→ Data lake storage + warehouse-style data management and analytics capabilities
```

For fresher interviews, understand the basic difference rather than going deeply into lakehouse internals.

---

# 11. What is a Fact Table?

A **Fact Table** stores measurable business events or metrics.

Examples:

```text
Sales
Orders
Payments
Transactions
```

Example:

```text
sales_fact

order_id
customer_id
product_id
date_id
quantity
sales_amount
```

Measures may include:

```text
quantity
revenue
sales_amount
profit
```

---

# 12. What is a Dimension Table?

A **Dimension Table** stores descriptive information used to analyze facts.

Examples:

```text
Customer
Product
Date
Location
Employee
```

Example:

```text
customer_dimension

customer_id
customer_name
city
country
age
```

---

# 13. Fact Table vs Dimension Table

| Fact Table | Dimension Table |
|---|---|
| Stores business events/measures | Stores descriptive information |
| Usually contains many rows | Usually smaller than fact tables |
| Numeric measures are common | Descriptive attributes are common |
| Example: sales | Example: customer |
| Used for calculations | Used for filtering/grouping |

### Easy Memory Trick

```text
Fact → What happened?

Dimension → Who / What / Where / When?
```

---

# 14. What is a Star Schema?

A **Star Schema** contains:

```text
        Customer
           |
Product — Fact — Date
           |
        Location
```

The fact table is in the center and dimension tables surround it.

Example:

```text
              Dim_Customer
                   |
                   |
Dim_Product — Fact_Sales — Dim_Date
                   |
                   |
              Dim_Store
```

---

# 15. Advantages of Star Schema

```text
Simple structure
Easy to understand
Good for analytical queries
Fewer joins compared with highly normalized designs
Commonly used in data warehouses
```

---

# 16. What is a Snowflake Schema?

A **Snowflake Schema** is a variation of the star schema where dimension tables are further normalized into related tables.

Example:

```text
             Dim_Customer
                  |
             Dim_City
                  |
             Dim_Country

                  |
                  ↓
              Fact_Sales
```

---

# 17. Star Schema vs Snowflake Schema

| Star Schema | Snowflake Schema |
|---|---|
| Dimensions are generally denormalized | Dimensions are normalized |
| Simpler | More complex |
| Fewer joins | More joins |
| Easier to query | More structured |
| Common for analytics | Useful when dimension normalization is desired |

### Easy Memory Trick

```text
Star → Simple

Snowflake → More normalized
```

---

# 18. What is Data Modeling?

**Data modeling** is the process of designing how data is structured, related, and stored.

It defines:

```text
Tables
Columns
Relationships
Keys
Facts
Dimensions
```

The goal is to organize data so that it can be efficiently stored and queried.

---

# 19. What is a Schema in a Data Warehouse?

A schema defines the structure and organization of data.

In dimensional modeling, common concepts include:

```text
Fact tables
Dimension tables
Relationships
Keys
Measures
Attributes
```

---

# 20. What is a Dimension Key?

A dimension key is used to identify a dimension record.

A common approach is to use a **surrogate key**.

Example:

```text
customer_key
------------
101
102
103
```

The fact table can reference:

```text
customer_key
```

instead of relying directly on the source-system identifier.

---

# 21. What is a Surrogate Key?

A **surrogate key** is an artificial/system-generated identifier used to uniquely identify a record in a data warehouse.

Example:

```text
customer_key | customer_id | customer_name
-------------|-------------|--------------
101          | C001        | Harsha
102          | C002        | Rahul
```

Here:

```text
customer_key → Surrogate key
customer_id  → Business/source identifier
```

---

# 22. What is a Natural Key?

A **natural key** is an identifier that comes from the business or source system.

Example:

```text
customer_id = C001
employee_id = E1001
```

Unlike a surrogate key, it has meaning in the source/business domain.

---

# 23. Surrogate Key vs Natural Key

| Surrogate Key | Natural Key |
|---|---|
| Artificial/system-generated | Comes from business/source |
| Usually has no business meaning | Has business meaning |
| Useful in dimensional warehouses | Common in source systems |
| Stable warehouse identifier | Can sometimes change |

---

# 24. What is a Data Mart?

A **Data Mart** is a smaller data store focused on a particular business area or department.

Examples:

```text
Sales Data Mart
Finance Data Mart
Marketing Data Mart
HR Data Mart
```

Conceptually:

```text
Enterprise Data Warehouse
          ↓
    ┌─────┼─────┐
    ↓     ↓     ↓
 Sales  Finance Marketing
 Mart    Mart     Mart
```

---

# 25. Data Warehouse vs Data Mart

```text
Data Warehouse
→ Broad enterprise-level analytical data

Data Mart
→ Focused on a specific business area
```

---

# 26. What is a Staging Area?

A **staging area** is an intermediate location where data is temporarily stored during an ETL/ELT process before it is loaded into its final destination.

Example:

```text
Source
  ↓
Staging
  ↓
Transformation
  ↓
Data Warehouse
```

It can help with:

```text
Data validation
Transformation
Temporary storage
Pipeline organization
```

---

# 27. What is a Raw Layer?

A raw layer stores data close to its original source format.

Example:

```text
Source
  ↓
Raw Layer
  ↓
Transformation
```

It is useful because the original data can be retained for:

```text
Reprocessing
Auditing
Debugging
Historical reference
```

---

# 28. What is a Curated Layer?

A curated layer contains cleaned and transformed data prepared for downstream use.

Example:

```text
Raw Data
   ↓
Transformation
   ↓
Curated Data
   ↓
Analytics
```

---

# 29. Common Data Lake Layers

A common architecture is:

```text
Source
  ↓
Raw / Bronze
  ↓
Cleaned / Silver
  ↓
Curated / Gold
  ↓
Analytics
```

### Bronze

```text
Raw / minimally processed data
```

### Silver

```text
Cleaned and transformed data
```

### Gold

```text
Business-ready / analytics-ready data
```

---

# 30. What is Parquet?

**Parquet** is a columnar file format commonly used in data engineering and big-data systems.

Example:

```text
data.parquet
```

It is commonly preferred for analytical workloads because it stores data by columns and supports efficient reading of required columns.

---

# 31. Why is Parquet Commonly Used?

Important benefits include:

```text
Columnar storage
Efficient analytical queries
Compression support
Efficient storage
Works well with Spark
```

Example:

If a dataset contains:

```text
id
name
age
salary
department
```

and a query needs only:

```text
salary
department
```

a columnar format can efficiently read the required columns.

---

# 32. CSV vs Parquet

| CSV | Parquet |
|---|---|
| Text-based | Columnar binary format |
| Easy to read manually | Optimized for data processing |
| Usually larger | Usually more storage-efficient |
| Schema information is limited | Stores schema information |
| Common for simple data exchange | Common in data engineering |

---

# 33. What is Partitioning in a Data Lake?

Partitioning organizes data into separate directories based on one or more columns.

Example:

```text
sales/
├── year=2026/
│   ├── month=01/
│   ├── month=02/
│   └── month=03/
```

If a query needs only:

```text
year = 2026
month = 03
```

the system can potentially avoid reading unrelated partitions.

---

# 34. Why is Data Lake Partitioning Useful?

It can reduce:

```text
Amount of data read
Query time
Processing work
Storage scanning cost
```

A commonly used partition column is a date:

```text
year
month
day
```

---

# 35. What is Partition Pruning?

**Partition pruning** means reading only the partitions that are relevant to a query instead of scanning all partitions.

Example:

```text
Data:
2024
2025
2026
```

Query:

```sql
WHERE year = 2026
```

The system can potentially read only:

```text
2026 partition
```

instead of scanning all years.

---

# 36. What is Schema Evolution?

**Schema evolution** means handling changes to the structure of data over time.

Example:

Initial schema:

```text
id
name
salary
```

Later:

```text
id
name
salary
department
```

A pipeline needs to handle the new column correctly.

Common schema changes include:

```text
Adding columns
Removing columns
Changing data types
Renaming columns
```

---

# 37. Why is Schema Evolution Important?

Real-world data sources change over time.

Without proper handling, a schema change can cause:

```text
Pipeline failures
Incorrect data
Missing columns
Downstream errors
```

---

# 38. What is Historical Data?

Historical data represents data collected over time and retained for analysis.

Example:

```text
Sales — 2022
Sales — 2023
Sales — 2024
Sales — 2025
Sales — 2026
```

Data warehouses and data lakes commonly retain historical data for trend analysis.

---

# 39. Basic Data Warehouse Architecture

```text
             DATA SOURCES
                  ↓
        ┌─────────────────┐
        │ Databases       │
        │ APIs             │
        │ Files            │
        └─────────────────┘
                  ↓
             ETL / ELT
                  ↓
              Staging
                  ↓
          Data Warehouse
             ↙       ↘
       Fact Tables   Dimensions
             ↓
          BI / Reports
```

---

# 40. Basic Data Lake Architecture

```text
             DATA SOURCES
                  ↓
              INGESTION
                  ↓
             RAW / BRONZE
                  ↓
          CLEANED / SILVER
                  ↓
         CURATED / GOLD
                  ↓
        Analytics / BI / ML
```

---

# 41. Common Interview Questions

```text
1. What is a Data Warehouse?

2. Why do we use a Data Warehouse?

3. What is OLTP?

4. What is OLAP?

5. OLTP vs OLAP?

6. What is a Data Lake?

7. Data Warehouse vs Data Lake?

8. What is a Data Lakehouse?

9. What is a Fact Table?

10. What is a Dimension Table?

11. Fact Table vs Dimension Table?

12. What is a Star Schema?

13. What is a Snowflake Schema?

14. Star Schema vs Snowflake Schema?

15. What is Data Modeling?

16. What is a Surrogate Key?

17. What is a Natural Key?

18. Surrogate Key vs Natural Key?

19. What is a Data Mart?

20. Data Warehouse vs Data Mart?

21. What is a Staging Area?

22. What are Raw, Silver and Gold layers?

23. What is Parquet?

24. Why is Parquet commonly used?

25. CSV vs Parquet?

26. What is Data Lake partitioning?

27. What is Partition Pruning?

28. What is Schema Evolution?

29. Why is historical data important?

30. Explain a basic Data Warehouse architecture.
```

---

# 42. ⭐ Most Important Questions

If you have limited time, prepare these first:

```text
1. What is a Data Warehouse?

2. What is a Data Lake?

3. Data Warehouse vs Data Lake?

4. What is OLTP?

5. What is OLAP?

6. OLTP vs OLAP?

7. What is a Fact Table?

8. What is a Dimension Table?

9. Fact vs Dimension?

10. What is Star Schema?

11. Star vs Snowflake Schema?

12. What is a Data Lakehouse?

13. What is a Surrogate Key?

14. What is a Data Mart?

15. What is Parquet and why is it used?

16. What is partitioning in a Data Lake?

17. What is Partition Pruning?

18. What is Schema Evolution?

19. Explain Bronze, Silver and Gold layers.

20. Explain a basic Data Warehouse/Data Lake architecture.
```

---

# 43. Quick Revision

```text
OLTP
→ Transaction processing

OLAP
→ Analytical processing

DATA WAREHOUSE
→ Structured/processed data for analytics

DATA LAKE
→ Large-scale storage for raw and varied data

DATA LAKEHOUSE
→ Data lake + warehouse-style capabilities

FACT TABLE
→ Business events + measurements

DIMENSION TABLE
→ Descriptive information

STAR SCHEMA
→ Central fact + surrounding dimensions

SNOWFLAKE SCHEMA
→ Normalized dimensions

SURROGATE KEY
→ System-generated warehouse identifier

NATURAL KEY
→ Business/source identifier

DATA MART
→ Department/business-area-specific analytical data

STAGING
→ Intermediate processing area

BRONZE
→ Raw data

SILVER
→ Cleaned/transformed data

GOLD
→ Business-ready data

PARQUET
→ Columnar file format

PARTITIONING
→ Organizing data into separate partitions

PARTITION PRUNING
→ Reading only relevant partitions

SCHEMA EVOLUTION
→ Handling schema changes over time
```

---

# 44. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
Data Warehouse
Data Lake
Data Warehouse vs Data Lake
OLTP vs OLAP
Fact and Dimension Tables
Star Schema
Snowflake Schema
Data Lakehouse
Parquet
Data Lake Partitioning
```

## ⭐⭐⭐⭐ Good to Know

```text
Surrogate vs Natural Keys
Data Mart
Staging Area
Bronze/Silver/Gold
Partition Pruning
Schema Evolution
```

> **For a fresher/Data Engineer interview, focus strongly on OLTP vs OLAP, Data Warehouse vs Data Lake, fact/dimension tables, star/snowflake schema, lakehouse, Parquet, and basic data-lake architecture. These are the highest-value concepts in this file.**