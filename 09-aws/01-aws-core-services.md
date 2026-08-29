# AWS Core Services

## 1. What is AWS?

**AWS (Amazon Web Services)** is a cloud computing platform that provides services for:

```text
Compute
Storage
Databases
Networking
Security
Monitoring
Data Engineering
```

For placement interviews, you mainly need to understand the purpose of the important services rather than memorize every AWS service.

---

# 2. Important AWS Services for Interviews

For a fresher, focus mainly on:

| Service | Main Purpose |
|---|---|
| S3 | Object storage |
| IAM | Access control |
| EC2 | Virtual servers |
| Lambda | Serverless compute |
| RDS | Managed relational database |
| VPC | Networking |
| CloudWatch | Monitoring and logs |
| Glue | Data integration / ETL |
| Athena | Query S3 data using SQL |
| Redshift | Data warehouse |

The last three were already covered in your **Data Engineering** section, so this file focuses mainly on the AWS fundamentals around them.

---

# 3. Amazon S3

**Amazon S3 (Simple Storage Service)** is an object storage service.

It can store:

```text
CSV
JSON
Parquet
Images
Videos
Logs
Backups
```

S3 is commonly used as the storage layer for a **Data Lake**.

Example:

```text
S3 Bucket
│
├── raw/
│   ├── customers.csv
│   └── orders.csv
│
├── processed/
│   └── orders.parquet
│
└── curated/
    └── sales.parquet
```

---

## 3.1 S3 Bucket

A **bucket** is a container for objects.

```text
Bucket
   ↓
Objects
```

Example:

```text
my-data-bucket
    ↓
orders.csv
customers.csv
sales.parquet
```

---

## 3.2 S3 Object

An **object** is the data stored in S3.

Example:

```text
s3://my-data-bucket/raw/orders/orders.csv
```

Here:

```text
my-data-bucket
→ Bucket

raw/orders/orders.csv
→ Object key
```

---

## 3.3 Why is S3 Important for Data Engineering?

S3 provides:

```text
Scalable storage
High durability
Flexible file storage
Data Lake storage
Backup storage
Raw and processed data storage
```

---

# 4. IAM

**IAM (Identity and Access Management)** is used to control access to AWS resources.

IAM includes:

```text
Users
Groups
Roles
Policies
Permissions
```

Example:

```text
IAM Role
   ↓
Allow Glue Job
   ↓
Read S3
   ↓
Write S3
```

---

# 5. IAM Policy

An **IAM policy** defines permissions.

It specifies things such as:

```text
Who can perform an action
What action can be performed
Which resource can be accessed
```

Example:

```text
Allow
s3:GetObject
on
specific S3 objects
```

---

# 6. IAM Role

An **IAM Role** provides permissions that can be assumed by an AWS service, application, or user.

Example:

```text
AWS Glue
    ↓
Assumes IAM Role
    ↓
Gets permission
    ↓
Accesses S3
```

IAM roles are commonly used when AWS services need to access other AWS services.

---

# 7. IAM User vs IAM Role

| IAM User | IAM Role |
|---|---|
| Represents a user/identity | Assumable identity |
| Can have long-term credentials | Commonly uses temporary credentials |
| Often used for individual users | Commonly used by AWS services |
| Permissions come from policies | Permissions come from policies |

### Remember:

```text
User → Person/application identity

Role → Permissions that can be assumed
```

---

# 8. Principle of Least Privilege

**Least privilege** means giving only the permissions required to perform a task.

Example:

If a Glue job only needs to:

```text
Read S3/raw/
Write S3/processed/
```

it should not receive unrestricted access to every AWS resource.

This improves security.

---

# 9. Amazon EC2

**Amazon EC2 (Elastic Compute Cloud)** provides virtual servers in the cloud.

You can use EC2 to run:

```text
Applications
Web servers
Scripts
Data processing workloads
Databases
```

Conceptually:

```text
AWS
 ↓
EC2 Instance
 ↓
Virtual Server
 ↓
Application
```

---

# 10. What is an EC2 Instance?

An **EC2 instance** is a virtual server running in AWS.

You can configure:

```text
CPU
Memory
Storage
Operating System
Networking
Security
```

---

# 11. Why is EC2 Used?

EC2 is useful when you need more control over the computing environment.

For example:

```text
Install software
Configure operating system
Run applications
Control server configuration
```

---

# 12. EC2 vs Lambda

| EC2 | Lambda |
|---|---|
| Virtual server | Serverless compute |
| You manage more of the environment | AWS manages the underlying infrastructure |
| Can run continuously | Runs in response to events/invocations |
| More control | Less infrastructure management |
| Suitable for long-running/custom workloads | Suitable for event-driven functions |

### Easy Memory Trick

```text
EC2 → Virtual Server

Lambda → Run a Function
```

---

# 13. AWS Lambda

**AWS Lambda** is a serverless compute service that runs code in response to events or requests.

Example:

```text
File uploaded to S3
        ↓
S3 Event
        ↓
Lambda
        ↓
Run code
```

Lambda is useful for:

```text
Event-driven processing
Lightweight automation
Triggering workflows
File processing
Notifications
```

---

# 14. Lambda in Data Engineering

Example:

```text
CSV uploaded to S3
        ↓
Lambda triggered
        ↓
Validate file
        ↓
Start Glue Job
```

Lambda is generally better suited to lightweight tasks than large-scale data processing.

---

# 15. Amazon RDS

**Amazon RDS (Relational Database Service)** is a managed relational database service.

It supports relational database engines such as:

```text
MySQL
PostgreSQL
MariaDB
Oracle
SQL Server
```

RDS handles much of the database infrastructure management for you.

---

# 16. Why is RDS Used?

RDS can be used when an application needs a relational database.

Examples:

```text
Application database
Customer information
Orders
Transactions
User accounts
```

---

# 17. RDS vs S3

| RDS | S3 |
|---|---|
| Managed relational database | Object storage |
| Stores structured relational data | Stores objects/files |
| Supports SQL queries | Not a traditional relational database |
| Used for application databases | Commonly used for Data Lakes |

### Easy Memory Trick

```text
RDS → Database

S3 → Files/Objects
```

---

# 18. RDS vs Redshift

| RDS | Redshift |
|---|---|
| Relational database service | Data warehouse |
| Mainly application/transactional workloads | Analytical workloads |
| OLTP use cases | OLAP use cases |
| Designed for application databases | Designed for analytics |

### Remember:

```text
RDS → Application database

Redshift → Analytics/Data Warehouse
```

---

# 19. Amazon VPC

**Amazon VPC (Virtual Private Cloud)** allows you to create a logically isolated network in AWS.

It controls how AWS resources communicate with each other and with external networks.

Conceptually:

```text
AWS
 ↓
VPC
 ├── Subnet
 ├── Route Table
 ├── Security Group
 └── Internet/NAT connectivity
```

---

# 20. What is a Subnet?

A **subnet** is a range of IP addresses within a VPC.

A VPC can contain multiple subnets.

Example:

```text
VPC
│
├── Public Subnet
│
└── Private Subnet
```

---

# 21. Public vs Private Subnet

### Public Subnet

A subnet whose resources can have a route to an Internet Gateway.

### Private Subnet

A subnet whose resources do not have a direct route to the internet through an Internet Gateway.

Example:

```text
VPC
│
├── Public Subnet
│     ↓
│   Internet Gateway
│
└── Private Subnet
      ↓
   Internal resources
```

---

# 22. Security Group

A **Security Group** acts as a virtual firewall for AWS resources such as EC2 instances.

It controls network traffic using rules.

Example:

```text
Allow
Port 443
HTTPS
```

---

# 23. Security Group vs IAM

These are different.

```text
IAM
→ Controls AWS API/resource permissions

Security Group
→ Controls network traffic
```

Example:

```text
IAM
→ Can this user access S3?

Security Group
→ Can this EC2 instance receive traffic on port 443?
```

---

# 24. Amazon CloudWatch

**Amazon CloudWatch** is used for monitoring AWS resources and applications.

It provides:

```text
Metrics
Logs
Alarms
Monitoring
```

Example:

```text
EC2
 ↓
CloudWatch
 ↓
CPU utilization
 ↓
Alarm
```

---

# 25. CloudWatch in Data Engineering

CloudWatch can help monitor:

```text
Glue jobs
Lambda functions
EC2 instances
Application logs
Pipeline failures
Resource utilization
```

Example:

```text
Pipeline
   ↓
Failure
   ↓
CloudWatch Logs
   ↓
Investigate error
```

---

# 26. AWS Glue

**AWS Glue** is a managed serverless data integration and ETL service.

It can be used for:

```text
Data ingestion
Data transformation
ETL
Data cataloging
PySpark processing
```

Typical flow:

```text
S3
 ↓
Glue
 ↓
Transform
 ↓
S3
```

You have already covered Glue in detail in:

```text
08-data-engineering
└── 03-aws-data-engineering.md
```

So you don't need to study it twice.

---

# 27. Amazon Athena

**Amazon Athena** is a serverless service that allows you to query data stored in S3 using SQL.

Example:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department;
```

Conceptually:

```text
S3
 ↓
Athena
 ↓
SQL
 ↓
Results
```

---

# 28. Amazon Redshift

**Amazon Redshift** is a cloud data warehouse designed for analytical workloads.

Example:

```text
S3
 ↓
ETL
 ↓
Redshift
 ↓
Analytics
```

Again, this is already covered in your Data Engineering preparation.

---

# 29. Important AWS Service Comparison

| Service | Purpose |
|---|---|
| S3 | Object storage |
| EC2 | Virtual servers |
| Lambda | Serverless compute |
| RDS | Managed relational database |
| VPC | Networking |
| IAM | Access control |
| CloudWatch | Monitoring |
| Glue | ETL/Data integration |
| Athena | SQL on S3 |
| Redshift | Data warehouse |

---

# 30. S3 vs EC2 vs Lambda

```text
S3
→ Store data

EC2
→ Run a virtual server

Lambda
→ Run event-driven code
```

---

# 31. S3 vs RDS vs Redshift

```text
S3
→ Object storage / Data Lake

RDS
→ Relational application database

Redshift
→ Analytical Data Warehouse
```

---

# 32. Glue vs Lambda

```text
Glue
→ Data integration and large-scale ETL

Lambda
→ Lightweight event-driven computation
```

Example:

```text
S3 File Upload
      ↓
Lambda
      ↓
Trigger Glue
      ↓
PySpark Transformation
```

---

# 33. IAM vs VPC

```text
IAM
→ Who can access what?

VPC
→ How do resources communicate over the network?
```

---

# 34. Basic AWS Data Engineering Architecture

```text
                 DATA SOURCES
                      ↓
             ┌────────────────┐
             │ API / Database │
             │ CSV / JSON     │
             └────────────────┘
                      ↓
                     S3
                  RAW DATA
                      ↓
                 Glue / PySpark
                      ↓
                     S3
               PROCESSED DATA
                   ↙       ↘
              Athena      Redshift
                ↓             ↓
             Analysis      BI/Reports
```

Security:

```text
IAM
 ↓
Control access
```

Monitoring:

```text
CloudWatch
 ↓
Logs + Metrics + Alarms
```

---

# 35. Common AWS Interview Questions

```text
1. What is AWS?

2. What is Amazon S3?

3. What is an S3 bucket?

4. What is an S3 object?

5. Why is S3 used in Data Engineering?

6. What is IAM?

7. What is an IAM policy?

8. What is an IAM role?

9. IAM User vs IAM Role?

10. What is the principle of least privilege?

11. What is EC2?

12. What is an EC2 instance?

13. Why is EC2 used?

14. EC2 vs Lambda?

15. What is AWS Lambda?

16. How can Lambda be used in Data Engineering?

17. What is Amazon RDS?

18. Why is RDS used?

19. RDS vs S3?

20. RDS vs Redshift?

21. What is a VPC?

22. What is a subnet?

23. Public subnet vs private subnet?

24. What is a Security Group?

25. IAM vs Security Group?

26. What is CloudWatch?

27. Why is CloudWatch used?

28. What is AWS Glue?

29. What is Amazon Athena?

30. What is Amazon Redshift?

31. S3 vs RDS vs Redshift?

32. Glue vs Lambda?

33. Explain a basic AWS data pipeline.

34. How would you secure an AWS data pipeline?

35. How would you monitor an AWS data pipeline?
```

---

# 36. ⭐ Most Important Questions

If you have limited time, prepare these first:

```text
1. What is S3?

2. What is an S3 bucket?

3. Why is S3 used as Data Lake storage?

4. What is IAM?

5. IAM User vs IAM Role?

6. What is the principle of least privilege?

7. What is EC2?

8. EC2 vs Lambda?

9. What is Lambda?

10. What is RDS?

11. RDS vs S3?

12. RDS vs Redshift?

13. What is VPC?

14. What is a subnet?

15. What is a Security Group?

16. IAM vs Security Group?

17. What is CloudWatch?

18. What is AWS Glue?

19. What is Athena?

20. What is Redshift?

21. Explain an AWS data pipeline.

22. How would you secure an AWS data pipeline?

23. How would you monitor an AWS data pipeline?
```

---

# 37. Quick Revision

```text
AWS
→ Cloud platform

S3
→ Object storage

BUCKET
→ Container for S3 objects

IAM
→ Access control

IAM POLICY
→ Defines permissions

IAM ROLE
→ Assumable identity with permissions

EC2
→ Virtual server

LAMBDA
→ Serverless event-driven compute

RDS
→ Managed relational database

VPC
→ Isolated AWS network

SUBNET
→ Network range inside a VPC

SECURITY GROUP
→ Virtual firewall

CLOUDWATCH
→ Monitoring, logs, metrics and alarms

GLUE
→ Serverless data integration / ETL

ATHENA
→ Serverless SQL queries on S3

REDSHIFT
→ Cloud Data Warehouse
```

---

# 38. Placement Priority

## ⭐⭐⭐⭐⭐ Must Know

```text
S3
IAM
IAM Roles
EC2
Lambda
RDS
VPC basics
Security Groups
CloudWatch
Glue
Athena
Redshift
Basic AWS Architecture
```

## ⭐⭐⭐⭐ Good to Know

```text
S3 Storage Classes
Public vs Private Subnets
Least Privilege
IAM vs Security Groups
Glue vs Lambda
RDS vs Redshift
```

> **For your placement preparation, don't go deep into AWS infrastructure. You mainly need to know what each core service does, when to use it, and how S3, Glue, Lambda, Athena, Redshift, IAM, and CloudWatch fit together in a data pipeline.**