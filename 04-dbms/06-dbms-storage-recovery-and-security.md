# DBMS Recovery and Security — Important Interview Topics

## 1. What is Database Recovery?

Database recovery is the process of restoring the database to a consistent state after a failure.

Failures can occur because of:

- System crash
- Power failure
- Transaction failure
- Hardware failure
- Software failure

---

## 2. What is the Purpose of Recovery?

The main purpose is to:

- Prevent loss of committed data
- Remove the effects of failed transactions
- Restore database consistency

Example:

```text
Transaction starts
      ↓
Data is modified
      ↓
System crashes
      ↓
Recovery
      ↓
Database restored to a consistent state
```

---

## 3. What are UNDO and REDO?

### UNDO

`UNDO` removes the effects of a transaction that should not be preserved.

Example:

```text
Transaction changes A: 100 → 200
Transaction fails
        ↓
UNDO
        ↓
A = 100
```

### REDO

`REDO` reapplies changes that should be preserved, typically for committed work whose effects were not yet fully reflected in the database after a failure.

Example:

```text
Transaction commits
        ↓
System crashes before all changes reach disk
        ↓
REDO
        ↓
Committed changes restored
```

### Easy way to remember

```text
UNDO → Remove unwanted changes

REDO → Reapply required changes
```

---

# 4. What is a Log?

A **log** records information about database transactions and their changes.

Conceptually:

```text
Transaction T1
    ↓
Change A: 100 → 200
    ↓
Log record
```

The DBMS can use the log during recovery.

---

# 5. What is Database Backup?

A **backup** is a copy of database data kept so that the database can be restored after data loss or corruption.

Common backup concepts include:

- Full backup
- Incremental backup
- Differential backup

For placement interviews, understand the basic purpose rather than memorizing implementation details.

---

# 6. What is Database Security?

Database security protects database data from:

- Unauthorized access
- Unauthorized modification
- Data theft
- Accidental misuse

Important security concepts are:

```text
Authentication
Authorization
Privileges
Roles
Access control
```

---

# 7. Authentication vs Authorization

### Authentication

Authentication verifies **who the user is**.

Example:

```text
Username + Password
        ↓
Identity verified
```

### Authorization

Authorization determines **what the user is allowed to do**.

Example:

```text
User authenticated
        ↓
Can SELECT?
Can INSERT?
Can UPDATE?
Can DELETE?
```

### Interview Answer

> Authentication verifies the identity of a user, while authorization determines what that authenticated user is permitted to access or perform.

---

# 8. What are Database Privileges?

Privileges are permissions given to users or roles.

Common privileges include:

```text
SELECT
INSERT
UPDATE
DELETE
```

Example:

```sql
GRANT SELECT
ON employees
TO analyst;
```

This allows the specified user/role to perform `SELECT` according to the DBMS's privilege model.

---

# 9. What is GRANT?

`GRANT` is used to provide privileges to a user or role.

Example:

```sql
GRANT SELECT, INSERT
ON employees
TO analyst;
```

---

# 10. What is REVOKE?

`REVOKE` is used to remove previously granted privileges.

Example:

```sql
REVOKE INSERT
ON employees
FROM analyst;
```

---

# 11. GRANT vs REVOKE

| GRANT | REVOKE |
|---|---|
| Gives permissions | Removes permissions |
| Used to provide access | Used to withdraw access |

---

# 12. What is SQL Injection?

**SQL injection** is a security vulnerability where untrusted input is manipulated so that it changes the intended SQL query.

Unsafe application pattern:

```text
User Input
    ↓
String concatenated directly into SQL
    ↓
Potentially altered SQL query
```

The main protection is to use:

- Parameterized queries
- Prepared statements
- Proper input handling
- Appropriate database privileges

### Interview Answer

> SQL injection occurs when untrusted input is improperly incorporated into SQL statements, allowing the input to alter the intended query. Parameterized queries or prepared statements are a primary defense.

---

# 13. Why Should Least Privilege Be Used?

**Least privilege** means giving users only the permissions they actually need.

Example:

```text
Reporting user
→ SELECT only
```

Instead of:

```text
Reporting user
→ SELECT
→ INSERT
→ UPDATE
→ DELETE
```

This reduces the potential impact of unauthorized or accidental actions.

---

# 14. What are Roles?

A **role** is a collection of permissions that can be assigned to users.

Conceptually:

```text
Role: Analyst
      ↓
SELECT
      ↓
User 1
User 2
User 3
```

Roles make permission management easier.

---

# 15. Most Important Interview Questions

## Q1. What is database recovery?

> Database recovery is the process of restoring the database to a consistent state after a failure.

## Q2. What is the difference between UNDO and REDO?

> UNDO removes changes that should not be preserved, while REDO reapplies changes that should be preserved.

## Q3. What is a database log?

> A database log records transaction-related changes and is used to help the DBMS recover from failures.

## Q4. What is a database backup?

> A backup is a copy of database data that can be used to restore the database after data loss or corruption.

## Q5. What is database security?

> Database security protects database information from unauthorized access, modification, or misuse.

## Q6. Authentication vs authorization?

> Authentication verifies who the user is, while authorization determines what the user is allowed to do.

## Q7. What are GRANT and REVOKE?

> `GRANT` gives privileges, while `REVOKE` removes privileges.

## Q8. What is SQL injection?

> SQL injection is a vulnerability where untrusted input can alter the intended SQL query. Parameterized queries and prepared statements are common defenses.

## Q9. What is the principle of least privilege?

> It means giving each user or application only the permissions necessary to perform its required tasks.

## Q10. What is a database role?

> A role is a collection of privileges that can be assigned to users, making permission management easier.

---

# 16. One-Minute Revision

```text
RECOVERY
→ Restore database consistency after failure

UNDO
→ Remove unwanted transaction changes

REDO
→ Reapply required/committed changes

LOG
→ Records transaction changes for recovery

BACKUP
→ Copy of data used for restoration

SECURITY
→ Protect database from unauthorized access

AUTHENTICATION
→ Who are you?

AUTHORIZATION
→ What can you do?

GRANT
→ Give permission

REVOKE
→ Remove permission

ROLE
→ Collection of permissions

LEAST PRIVILEGE
→ Give only required permissions

SQL INJECTION
→ Malicious/untrusted input changes SQL
→ Use parameterized queries/prepared statements
```

# 17. Placement Priority

For DBMS placements, these are the **only topics from this file you need to prepare seriously**:

```text
⭐⭐⭐⭐⭐
1. Authentication vs Authorization
2. SQL Injection
3. GRANT and REVOKE
4. Database Recovery
5. UNDO vs REDO

⭐⭐⭐⭐
6. Database Backup
7. Database Logs
8. Roles
9. Least Privilege
```

You can **skip deep internal recovery algorithms, detailed storage architecture, RAID, shadow paging, and advanced database security** unless a particular company/job description specifically requires them.