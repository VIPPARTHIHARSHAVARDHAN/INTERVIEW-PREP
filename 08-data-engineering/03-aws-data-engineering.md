# AWS Data Engineering

## 1. Why is AWS Used in Data Engineering?

AWS provides cloud services for:

```text
Data Storage
Data Ingestion
Data Processing
Data Transformation
Data Warehousing
Querying
Orchestration
Monitoring
Security
```

A common AWS data pipeline can look like:

```text
Data Sources
     ↓
    S3
     ↓
AWS Glue / PySpark
     ↓
    S3
     ↓
Amazon Redshift
     ↓
Athena / BI Tools
```

---

# 2. Important AWS Services for Data Engineers

For fresher interviews, focus mainly on:

```text
Amazon S3
AWS IAM
AWS Glue
Amazon Athena
Amazon Redshift
AWS Lambda
Amazon CloudWatch
```

You do not need to memorize every AWS service.

---

# 3. What is Amazon S3?

**Amazon S3 (Simple Storage Service)** is an object storage service used to store large amounts of data.

It is commonly used as a **data lake storage layer**.

Example:

```text
S3
├── raw/
├── processed/
└── curated/
```

It can store:

```text
CSV
JSON
Parquet
Logs
Images
Videos
```

---

# 4. What is an S3 Bucket?

A **bucket** is a container used to store objects in S3.

Example:

```text
Bucket
└── data/
    ├── customers.csv
    ├── orders.csv
    └── sales.parquet
```

The bucket name must be globally unique within the AWS partition.

---

# 5. What is an S3 Object?

An object is the actual piece of data stored in S3.

An object consists conceptually of:

```text
Data
+
Key
+
Metadata
```

Example:

```text
s3://my-bucket/raw/orders/orders.csv
```

Here:

```text
my-bucket
→ Bucket

raw/orders/orders.csv
→ Object key/path
```

---

# 6. Why is S3 Important for Data Engineering?

S3 is commonly used for:

```text
Raw data storage
Data lake storage
Processed data
Backup
Historical data
Intermediate pipeline data
```

A common architecture is:

```text
Source
  ↓
S3 Raw
  ↓
Processing
  ↓
S3 Processed
  ↓
Data Warehouse
```

---

# 7. What are S3 Storage Classes?

S3 provides different storage classes based on access patterns and cost.

Important examples:

```text
S3 Standard
S3 Intelligent-Tiering
S3 Standard-IA
S3 Glacier
```

For interviews, understand the basic idea:

```text
Frequently accessed
→ Standard

Infrequently accessed
→ IA

Long-term archival
→ Glacier
```

---

# 8. What is AWS IAM?

**IAM (Identity and Access Management)** controls access to AWS resources.

It manages:

```text
Users
Groups
Roles
Policies
Permissions
```

---

# 9. What is an IAM Policy?

An IAM policy defines what actions are allowed or denied on AWS resources.

Conceptually:

```text
Who?
 ↓
Can perform what action?
 ↓
On which resource?
```

Example:

```text
Allow
s3:GetObject
on
specific S3 objects
```

---

# 10. What is an IAM Role?

An IAM Role provides temporary permissions that can be assumed by AWS services or users.

Example:

```text
AWS Glue
   ↓
Assume IAM Role
   ↓
Access S3
```

A Glue job may use an IAM role to access an S3 bucket.

---

# 11. IAM User vs IAM Role

| IAM User | IAM Role |
|---|---|
| Identity for a person/application | Assumable identity |
| Can have long-term credentials | Typically uses temporary credentials |
| Often used for human access | Commonly used by AWS services |
| Permissions controlled by policies | Permissions controlled by policies |

### Interview Point

For AWS services communicating with each other, **IAM roles** are commonly preferred over embedding long-term access keys.

---

# 12. What is AWS Glue?

**AWS Glue** is a managed serverless data integration service.

It is commonly used for:

```text
Data discovery
ETL
Data transformation
Data cataloging
Pipeline processing
```

---

# 13. What is a Glue Crawler?

A **Glue Crawler** scans data sources and discovers schema information.

It can create or update metadata in the **Glue Data Catalog**.

Conceptually:

```text
S3 Data
   ↓
Glue Crawler
   ↓
Discover Schema
   ↓
Glue Data Catalog
```

---

# 14. What is AWS Glue Data Catalog?

The **Glue Data Catalog** is a centralized metadata repository.

It stores information such as:

```text
Table names
Column names
Data types
Location of data
Partitions
```

It does not store the actual dataset itself.

Example:

```text
Actual data
→ S3

Metadata about data
→ Glue Data Catalog
```

---

# 15. What is a Glue Job?

A **Glue Job** performs data processing and ETL operations.

It can use:

```text
Python
PySpark
Spark
```

Example:

```text
S3 Raw
  ↓
Glue Job
  ↓
Clean / Transform
  ↓
S3 Processed
```

---

# 16. Glue Crawler vs Glue Job

| Glue Crawler | Glue Job |
|---|---|
| Discovers schema | Processes data |
| Creates/updates metadata | Performs transformations |
| Works with Data Catalog | Reads/writes/transforms data |
| Does not perform your main ETL logic | Executes ETL logic |

### Easy Memory Trick

```text
Crawler → Discover

Job → Process
```

---

# 17. What is Amazon Athena?

**Amazon Athena** is a serverless interactive query service used to query data stored in S3 using SQL.

Example:

```sql
SELECT *
FROM sales
WHERE amount > 10000;
```

Conceptually:

```text
S3
 ↓
Athena
 ↓
SQL Query
 ↓
Result
```

---

# 18. Why is Athena Useful?

Athena is useful when you want to query data in S3 without managing database servers.

Common use cases:

```text
Ad-hoc analysis
Log analysis
Data lake querying
Quick SQL analysis
```

---

# 19. Athena vs Redshift

| Athena | Redshift |
|---|---|
| Serverless query service | Managed cloud data warehouse |
| Queries data commonly stored in S3 | Stores/query data in warehouse |
| Good for ad-hoc S3 queries | Good for warehouse analytics |
| No cluster management | Warehouse resources need management/configuration |

### Easy Memory Trick

```text
Athena → Query S3

Redshift → Data Warehouse
```

---

# 20. What is Amazon Redshift?

**Amazon Redshift** is a fully managed cloud data warehouse service.

It is designed for analytical workloads.

Example:

```text
S3
 ↓
ETL / ELT
 ↓
Redshift
 ↓
BI / Analytics
```

---

# 21. Why is Redshift Used?

Redshift is commonly used for:

```text
Data warehousing
Analytics
Reporting
Large-scale SQL queries
Aggregations
BI workloads
```

---

# 22. S3 vs Redshift

| S3 | Redshift |
|---|---|
| Object storage | Data warehouse |
| Stores raw/processed files | Stores structured analytical data |
| Can store many file types | Primarily used for analytical datasets |
| Data lake storage | Data warehouse |
| Example: CSV/JSON/Parquet | Tables queried using SQL |

### Easy Memory Trick

```text
S3 → Store

Redshift → Analyze structured warehouse data
```

---

# 23. What is AWS Lambda?

**AWS Lambda** is a serverless compute service that runs code in response to events or requests.

Example:

```text
File uploaded to S3
       ↓
S3 Event
       ↓
Lambda
       ↓
Trigger processing
```

It is useful for lightweight event-driven tasks.

---

# 24. Lambda in Data Engineering

Lambda can be used for:

```text
Triggering pipelines
Processing lightweight events
Validating files
Starting Glue jobs
Sending notifications
Automating small tasks
```

It is generally not the first choice for large-scale data processing.

---

# 25. What is Amazon CloudWatch?

**Amazon CloudWatch** is used for monitoring AWS resources and applications.

It can help with:

```text
Logs
Metrics
Alarms
Monitoring
Troubleshooting
```

Example:

```text
Glue Job
   ↓
CloudWatch Logs
   ↓
Monitor errors
```

---

# 26. Why is CloudWatch Important in Data Engineering?

A production data pipeline needs monitoring.

CloudWatch can help identify:

```text
Pipeline failures
Errors
Resource problems
Performance issues
Unexpected behavior
```

---

# 27. Common AWS Data Engineering Architecture

A common AWS pipeline:

```text
             DATA SOURCES
                  ↓
        ┌──────────────────┐
        │ MySQL / API /    │
        │ CSV / JSON       │
        └──────────────────┘
                  ↓
                 S3
              RAW DATA
                  ↓
           Glue Crawler
                  ↓
          Glue Data Catalog
                  ↓
             Glue Job
             PySpark
                  ↓
                 S3
           PROCESSED DATA
                  ↓
              Redshift
                  ↓
            BI / Analytics
```

Athena can also query suitable data directly in S3:

```text
S3
 ↓
Glue Catalog
 ↓
Athena
 ↓
SQL Analysis
```

---

# 28. Explain an AWS Data Engineering Project

A good interview explanation can follow this structure:

```text
1. Source
2. Ingestion
3. Storage
4. Transformation
5. Loading
6. Querying
7. Monitoring
```

Example:

> Data was collected from the source system and stored in Amazon S3. AWS Glue was used for data cataloging and PySpark-based transformations. The processed data was stored in S3 and loaded into Amazon Redshift for analytical queries. Athena was used for querying suitable data directly in S3, and CloudWatch was used for monitoring and troubleshooting.

---

# 29. How Would You Design a Simple AWS Data Pipeline?

Example:

```text
CSV/API
   ↓
S3 Raw
   ↓
Glue Crawler
   ↓
Glue Data Catalog
   ↓
Glue PySpark Job
   ↓
S3 Processed
   ↓
Redshift
   ↓
BI Dashboard
```

Monitoring:

```text
Glue / AWS resources
        ↓
    CloudWatch
```

Security:

```text
IAM Roles
    ↓
Control access to resources
```

---

# 30. How Do You Secure an AWS Data Pipeline?

Important practices:

```text
Use IAM roles
Follow least privilege
Avoid hardcoding credentials
Restrict S3 access
Encrypt sensitive data
Monitor access and activity
```

### Least Privilege

Give users/services only the permissions they actually need.

Example:

```text
Glue Job
→ Read specific S3 location
→ Write specific S3 location
```

rather than giving unrestricted access to everything.

---

# 31. What is Serverless?

A serverless service allows you to use computing capabilities without directly managing the underlying servers.

Examples:

```text
AWS Lambda
AWS Glue
Amazon Athena
```

You still use compute resources, but AWS manages much of the underlying infrastructure.

---

# 32. What is a Managed Service?

A managed service is a service where AWS handles much of the underlying infrastructure and operational management.

Examples:

```text
Redshift
Glue
RDS
```

The amount of management varies by service.

---

# 33. What is the Difference Between S3 and S3 Data Lake?

S3 is the **storage service**.

A data lake is an **architecture/concept** for storing and managing large amounts of data.

Example:

```text
S3
 ↓
Used as storage layer
 ↓
Data Lake
```

So:

```text
S3 ≠ Data Lake

S3 can be used to build a Data Lake.
```

---

# 34. What is the Difference Between Glue and EMR?

Both can be used for big-data processing, but they serve different purposes.

```text
AWS Glue
→ Serverless data integration / ETL

Amazon EMR
→ Managed cluster platform for big-data frameworks
```

For fresher interviews, knowing this basic difference is generally enough.

---

# 35. Common AWS Data Engineering Interview Questions

```text
1. What is AWS?

2. Why is AWS used in Data Engineering?

3. What is Amazon S3?

4. What is an S3 bucket?

5. What is an S3 object?

6. Why is S3 commonly used in Data Lakes?

7. What are S3 storage classes?

8. What is IAM?

9. What is an IAM policy?

10. What is an IAM role?

11. IAM User vs IAM Role?

12. What is AWS Glue?

13. What is a Glue Crawler?

14. What is Glue Data Catalog?

15. What is a Glue Job?

16. Glue Crawler vs Glue Job?

17. What is Amazon Athena?

18. Why is Athena used?

19. Athena vs Redshift?

20. What is Amazon Redshift?

21. Why is Redshift used?

22. S3 vs Redshift?

23. What is AWS Lambda?

24. How is Lambda used in Data Engineering?

25. What is CloudWatch?

26. Why is CloudWatch important?

27. What is a serverless service?

28. How would you design an AWS data pipeline?

29. How would you secure an AWS data pipeline?

30. Explain your AWS Data Engineering project.
```

---

# 36. ⭐ Most Important Questions

If you have limited time, prepare these first:

```text
1. What is Amazon S3?

2. Why is S3 used as a Data Lake?

3. What is an S3 bucket?

4. What is IAM?

5. IAM User vs IAM Role?

6. What is AWS Glue?

7. What is a Glue Crawler?

8. What is Glue Data Catalog?

9. What is a Glue Job?

10. Glue Crawler vs Glue Job?

11. What is Amazon Athena?

12. Athena vs Redshift?

13. What is Amazon Redshift?

14. S3 vs Redshift?

15. What is AWS Lambda?

16. What is CloudWatch?

17. How would you design an AWS data pipeline?

18. How would you secure an AWS data pipeline?

19. Explain an AWS Data Engineering project.

20. Explain the complete flow of data from source to warehouse on AWS.
```

---

# 37. ⭐ Quick Revision

```text
S3
→ Object storage
→ Common Data Lake storage

S3 BUCKET
→ Container for objects

S3 OBJECT
→ Actual stored data + key/metadata

IAM
→ AWS access control

IAM POLICY
→ Defines permissions

IAM ROLE
→ Assumable identity commonly used by AWS services

GLUE
→ Serverless data integration / ETL

GLUE CRAWLER
→ Discovers schema and updates catalog metadata

GLUE DATA CATALOG
→ Central metadata repository

GLUE JOB
→ Performs ETL/data processing

ATHENA
→ Serverless SQL queries on S3 data

REDSHIFT
→ Cloud Data Warehouse

LAMBDA
→ Serverless event-driven compute

CLOUDWATCH
→ Monitoring, logs, metrics and alarms

EMR
→ Managed big-data cluster platform

DATA LAKE
→ Architecture for storing large amounts of raw/varied data

S3
→ Can be the storage layer of a Data Lake
```

---

# 38. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
S3
IAM
Glue
Glue Crawler
Glue Data Catalog
Glue Job
Athena
Redshift
Basic AWS Pipeline Architecture
```

## ⭐⭐⭐⭐ Good to Know

```text
Lambda
CloudWatch
S3 Storage Classes
IAM Roles vs Users
Serverless
EMR vs Glue
Basic AWS Security
```

> **For a fresher Data Engineering interview, focus heavily on S3, IAM, Glue, Athena, Redshift, and how they connect in an end-to-end pipeline. You do not need deep AWS infrastructure knowledge unless the job specifically asks for AWS cloud expertise.**