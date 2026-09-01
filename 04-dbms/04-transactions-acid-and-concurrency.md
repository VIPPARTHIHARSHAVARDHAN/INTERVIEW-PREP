# Transactions, ACID and Concurrency

## 1. What is a Transaction?

A **transaction** is a sequence of one or more database operations that are treated as a single logical unit of work.

A transaction can contain operations such as:

```sql
INSERT
UPDATE
DELETE
SELECT
```

Example: transferring ₹1000 from Account A to Account B.

```text
1. Deduct ₹1000 from Account A
2. Add ₹1000 to Account B
```

Both operations should be treated as one transaction.

If the first operation succeeds but the second fails, the database should undo the first operation.

---

# 2. Simple Transaction Example

Suppose:

```text
Account A = ₹5000
Account B = ₹3000
```

Transfer ₹1000 from A to B:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

After the transaction:

```text
Account A = ₹4000
Account B = ₹4000
```

---

# 3. What is COMMIT?

`COMMIT` permanently saves the changes made by the current transaction.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

COMMIT;
```

After `COMMIT`, the changes become permanent according to the database's transaction semantics.

---

# 4. What is ROLLBACK?

`ROLLBACK` undoes changes made by the current transaction that have not been committed.

Example:

```sql
BEGIN;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

ROLLBACK;
```

The update is undone.

---

# 5. COMMIT vs ROLLBACK

| COMMIT | ROLLBACK |
|---|---|
| Saves transaction changes | Undoes uncommitted transaction changes |
| Makes changes permanent | Returns data to the previous transactionally consistent state |
| Used when transaction succeeds | Used when transaction fails or must be cancelled |

### Memory Trick

```text
COMMIT   → Save
ROLLBACK → Undo
```

---

# 6. What is ACID?

**ACID** represents four important properties of database transactions:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

These properties help ensure reliable transaction processing.

---

# 7. What is Atomicity?

**Atomicity** means a transaction is treated as an all-or-nothing unit.

Either:

```text
All operations succeed
```

or:

```text
None of the transaction's changes are applied
```

Example:

```text
Transfer ₹1000

Step 1:
A → -₹1000

Step 2:
B → +₹1000
```

If Step 2 fails, Step 1 should also be undone.

```text
Transaction succeeds
→ Both changes applied

Transaction fails
→ Changes rolled back
```

### Interview Definition

> Atomicity ensures that a transaction's operations are treated as one unit: either the transaction completes successfully, or its changes are rolled back.

---

# 8. What is Consistency?

**Consistency** means a successful transaction takes the database from one valid state to another valid state while respecting defined integrity rules and constraints.

Example:

Suppose:

```text
Account A = ₹5000
Account B = ₹3000
```

Total:

```text
₹8000
```

After transferring ₹1000:

```text
A = ₹4000
B = ₹4000
```

Total remains:

```text
₹8000
```

The transaction should preserve the applicable database rules.

### Interview Definition

> Consistency ensures that a transaction preserves database integrity constraints and moves the database from one valid state to another valid state.

---

# 9. What is Isolation?

**Isolation** means concurrent transactions should not improperly interfere with each other.

Example:

```text
Transaction T1
Transaction T2
```

If both execute at the same time, the database's isolation mechanisms control what changes each transaction can see and how their operations interact.

The goal is to prevent incorrect results caused by unsafe concurrent execution.

---

# 10. What is Durability?

**Durability** means that once a transaction has been successfully committed, its changes survive subsequent failures such as a system crash, subject to the database system's recovery guarantees.

Example:

```text
UPDATE
   ↓
COMMIT
   ↓
System crashes
   ↓
Database recovers
   ↓
Committed change remains
```

### Interview Definition

> Durability ensures that committed transaction changes are preserved even if a system failure occurs afterward.

---

# 11. ACID Summary

| Property | Meaning |
|---|---|
| Atomicity | All-or-nothing transaction |
| Consistency | Preserves database rules/integrity |
| Isolation | Concurrent transactions do not improperly interfere |
| Durability | Committed changes survive failures |

### Easy Memory Trick

```text
A → All or Nothing
C → Correct/Valid State
I → Transactions are Isolated
D → Data Survives Commit
```

---

# 12. Why is Concurrency Needed?

**Concurrency** means multiple transactions can execute during overlapping periods.

Example:

```text
T1 → Updating Account A
T2 → Reading Account B
T3 → Updating Account C
```

Databases need concurrency because many users can access the database at the same time.

Without proper concurrency control, transactions may interfere and produce incorrect results.

---

# 13. What is Concurrency Control?

**Concurrency control** is the set of techniques used by a DBMS to manage simultaneous transactions while maintaining correctness and isolation.

It aims to ensure that concurrent execution produces acceptable results according to the database's isolation guarantees.

Common techniques include:

```text
Locking
MVCC
Timestamp-based techniques
```

---

# 14. What is a Schedule?

A **schedule** is the order in which operations from multiple transactions are executed.

Suppose:

```text
T1:
Read(A)
Write(A)

T2:
Read(A)
Write(A)
```

A schedule determines how these operations are interleaved.

Example:

```text
T1: Read(A)
T2: Read(A)
T1: Write(A)
T2: Write(A)
```

---

# 15. What is a Serial Schedule?

In a **serial schedule**, transactions execute one after another without interleaving their operations.

Example:

```text
T1:
Read
Write
Commit

Then

T2:
Read
Write
Commit
```

Conceptually:

```text
T1 → T2
```

or:

```text
T2 → T1
```

---

# 16. What is a Concurrent Schedule?

In a concurrent schedule, operations from multiple transactions are interleaved.

Example:

```text
T1: Read(A)
T2: Read(B)
T1: Write(A)
T2: Write(B)
```

Concurrency can improve resource utilization and throughput, but it requires concurrency control.

---

# 17. Serial vs Concurrent Schedule

| Serial Schedule | Concurrent Schedule |
|---|---|
| Transactions execute one after another | Operations may be interleaved |
| Simpler to reason about | Can improve concurrency |
| No interleaving | Interleaving occurs |
| Usually less concurrency | Higher concurrency |

---

# 18. What is Serializability?

**Serializability** is a correctness criterion for concurrent schedules.

A concurrent schedule is serializable if its effect is equivalent to some serial execution of the same transactions.

Example:

```text
Concurrent Schedule
        ↓
Equivalent to
        ↓
T1 → T2
```

If it produces the same relevant final result as a valid serial order, it is considered serializable.

---

# 19. Why is Serializability Important?

Without proper concurrency control:

```text
T1 + T2
   ↓
Incorrect interleaving
   ↓
Incorrect database result
```

Serializability helps ensure that concurrent execution remains correct by requiring equivalence to an appropriate serial execution.

---

# 20. What is Conflict Serializability?

A schedule is **conflict-serializable** if it can be transformed into a serial schedule by swapping non-conflicting operations.

Two operations conflict when:

- They belong to different transactions.
- They access the same data item.
- At least one of them is a write.

Conflicting pairs include:

```text
Read-Write
Write-Read
Write-Write
```

A:

```text
Read-Read
```

pair does not conflict.

---

# 21. What is a Conflict?

Two operations conflict when:

```text
1. They belong to different transactions
2. They access the same data item
3. At least one operation is a write
```

Example:

```text
T1: Read(A)
T2: Write(A)
```

These operations conflict.

Another example:

```text
T1: Write(A)
T2: Write(A)
```

They also conflict.

But:

```text
T1: Read(A)
T2: Read(A)
```

do not conflict.

---

# 22. Conflict Types

The important conflict pairs are:

```text
Read → Write
Write → Read
Write → Write
```

Not a conflict:

```text
Read → Read
```

### Memory Trick

```text
Same data + different transactions + at least one WRITE
= Conflict
```

---

# 23. What is a Precedence Graph?

A **precedence graph**, also called a serialization graph, is used to analyze conflict serializability.

Basic process:

```text
1. Create one node for each transaction.
2. Look for conflicting operations.
3. Add a directed edge based on their order.
4. Check for cycles.
```

---

# 24. Precedence Graph Example

Suppose:

```text
T1: Read(A)
T1: Write(A)

T2: Read(A)
T2: Write(A)
```

Schedule:

```text
T1: Read(A)
T2: Read(A)
T1: Write(A)
T2: Write(A)
```

There is a conflict between:

```text
T1 Write(A)
T2 Read(A)
```

and:

```text
T1 Write(A)
T2 Write(A)
```

This can create:

```text
T1 → T2
```

If the graph has no cycle, the schedule is conflict-serializable.

---

# 25. Cycle Rule

For a precedence graph:

```text
No cycle
→ Conflict-serializable

Cycle
→ Not conflict-serializable
```

This is one of the most important rules for interview questions.

---

# 26. What are Concurrency Problems?

Important concurrency problems include:

1. Dirty Read
2. Non-Repeatable Read
3. Phantom Read
4. Lost Update

These are frequently asked in interviews.

---

# 27. What is a Dirty Read?

A **dirty read** occurs when one transaction reads data written by another transaction before that other transaction commits.

Example:

```text
T1:
UPDATE balance = 5000 → 4000

T2:
READ balance = 4000

T1:
ROLLBACK
```

T2 read:

```text
4000
```

but T1 later rolled back the change.

Therefore, T2 read data that was never committed.

```text
T1 writes
   ↓
T2 reads
   ↓
T1 rolls back
```

This is a dirty read.

---

# 28. What is a Non-Repeatable Read?

A **non-repeatable read** occurs when a transaction reads the same row twice and gets different values because another committed transaction modified that row between the two reads.

Example:

```text
T1:
READ balance → 5000

T2:
UPDATE balance → 4000
COMMIT

T1:
READ balance → 4000
```

T1 read the same row twice but obtained different values.

---

# 29. What is a Phantom Read?

A **phantom read** occurs when a transaction repeats a query that returns a set of rows and finds a different set because another committed transaction inserted, deleted, or otherwise changed rows that satisfy the query condition.

Example:

```text
T1:
SELECT * FROM employees
WHERE salary > 50000;

→ 5 rows
```

Then:

```text
T2:
INSERT a new employee with salary = 60000
COMMIT
```

T1 executes the same query again:

```text
→ 6 rows
```

The newly appearing row is a phantom.

---

# 30. What is a Lost Update?

A **lost update** occurs when concurrent transactions read and update the same data item and one transaction's update overwrites another transaction's update.

Example:

Initial value:

```text
balance = 1000
```

Two transactions read:

```text
T1 reads 1000
T2 reads 1000
```

T1 calculates:

```text
1000 + 100 = 1100
```

T2 calculates:

```text
1000 + 200 = 1200
```

If T1 writes 1100 and then T2 writes 1200:

```text
Final value = 1200
```

T1's update has effectively been lost.

---

# 31. Dirty Read vs Non-Repeatable Read vs Phantom Read

| Problem | Main Issue |
|---|---|
| Dirty Read | Reads uncommitted data |
| Non-Repeatable Read | Same row gives different values |
| Phantom Read | Same query returns different set of rows |
| Lost Update | One update overwrites another |

### Easy Memory Trick

```text
Dirty
→ Uncommitted data

Non-repeatable
→ Same row, different value

Phantom
→ Same query, different rows

Lost Update
→ One update gets overwritten
```

---

# 32. What is a Lock?

A **lock** is a concurrency-control mechanism used to regulate access to data by transactions.

It can prevent incompatible operations from occurring simultaneously.

The two fundamental lock modes are:

```text
Shared Lock
Exclusive Lock
```

---

# 33. What is a Shared Lock?

A **shared lock (S-lock)** is generally used for reading.

Multiple transactions can hold compatible shared locks on the same data item simultaneously.

Conceptually:

```text
T1 → S-lock(A)
T2 → S-lock(A)
```

Both may read A.

But a shared lock is incompatible with an exclusive lock on the same item.

---

# 34. What is an Exclusive Lock?

An **exclusive lock (X-lock)** is used when a transaction needs to modify a data item.

An exclusive lock prevents incompatible concurrent access.

Conceptually:

```text
T1 → X-lock(A)
```

Another transaction cannot obtain a conflicting lock on A until the relevant lock is released.

---

# 35. Shared Lock vs Exclusive Lock

| Shared Lock | Exclusive Lock |
|---|---|
| Mainly used for reading | Used for modification |
| Multiple compatible shared locks can coexist | Conflicts with shared and exclusive locks |
| Does not allow conflicting writes | Prevents conflicting access |

---

# 36. Lock Compatibility

A simplified compatibility table is:

| Existing / Requested | Shared | Exclusive |
|---|---:|---:|
| Shared | Yes | No |
| Exclusive | No | No |

Therefore:

```text
S + S → Compatible

S + X → Not compatible

X + X → Not compatible
```

---

# 37. What is Two-Phase Locking (2PL)?

**Two-Phase Locking (2PL)** is a concurrency-control protocol with two phases:

```text
1. Growing Phase
2. Shrinking Phase
```

---

# 38. Growing Phase

During the growing phase:

```text
Transaction can acquire locks
Transaction cannot release locks
```

Example:

```text
Lock(A)
Lock(B)
Lock(C)
```

No locks are released yet.

---

# 39. Shrinking Phase

During the shrinking phase:

```text
Transaction can release locks
Transaction cannot acquire new locks
```

Example:

```text
Unlock(C)
Unlock(B)
Unlock(A)
```

Once the transaction starts releasing locks, it cannot obtain new locks under basic 2PL.

---

# 40. 2PL Structure

```text
        GROWING PHASE
        ↓
    Acquire Locks
        ↓
   Lock(A), Lock(B)
        ↓
    Lock Point
        ↓
       SHRINKING PHASE
        ↓
    Release Locks
        ↓
    Unlock(B), Unlock(A)
```

---

# 41. What Does 2PL Guarantee?

Basic 2PL guarantees **conflict serializability** under the standard locking model.

However, basic 2PL does not by itself guarantee freedom from deadlocks.

---

# 42. What is Strict Two-Phase Locking?

In **Strict 2PL**, exclusive locks are held until the transaction commits or aborts.

This helps prevent certain cascading rollback problems and simplifies recovery.

Conceptually:

```text
Acquire locks
      ↓
Perform operations
      ↓
Commit / Abort
      ↓
Release exclusive locks
```

---

# 43. Basic 2PL vs Strict 2PL

| Basic 2PL | Strict 2PL |
|---|---|
| Has growing and shrinking phases | Also follows 2PL principles |
| Locks can be released before commit depending on protocol | Exclusive locks are held until commit/abort |
| Guarantees conflict serializability | Helps provide stronger recovery properties |
| Can still have deadlocks | Can still have deadlocks |

---

# 44. What is Deadlock?

A **deadlock** occurs when two or more transactions wait for each other indefinitely.

Example:

```text
T1 holds Lock(A)
T2 holds Lock(B)

T1 waits for B
T2 waits for A
```

Diagram:

```text
T1 → waiting for T2
T2 → waiting for T1
```

Neither can proceed.

---

# 45. Deadlock Example

```text
T1:
Lock(A)
Wait for B

T2:
Lock(B)
Wait for A
```

Result:

```text
T1 waits for T2
T2 waits for T1
```

This creates a cycle and therefore a deadlock.

---

# 46. How Can Deadlocks Be Handled?

Common approaches include:

### Prevention

Design the locking protocol so deadlocks cannot occur.

Examples include:

```text
Lock ordering
Wait-die
Wound-wait
```

### Detection

Allow deadlocks to occur, then detect them using techniques such as a wait-for graph.

### Recovery

After detecting a deadlock, abort/rollback one or more transactions to break the cycle.

---

# 47. What is a Wait-For Graph?

A **wait-for graph** represents transactions waiting for other transactions.

Example:

```text
T1 → T2
```

means:

```text
T1 is waiting for T2
```

If the graph contains a cycle:

```text
T1 → T2
↑       ↓
└───────┘
```

there is a deadlock in the standard lock-wait model.

---

# 48. Deadlock vs Starvation

### Deadlock

Transactions are waiting for each other and none can proceed.

```text
T1 waits for T2
T2 waits for T1
```

### Starvation

A transaction waits for an excessively long time because other transactions repeatedly get the resources or priority it needs.

### Difference

```text
Deadlock
→ Circular waiting

Starvation
→ Indefinite/unfair waiting
```

---

# 49. What is a Transaction State?

A transaction can move through several states.

Common states include:

```text
Active
Partially Committed
Committed
Failed
Aborted
```

---

# 50. Active State

The transaction is currently executing.

Example:

```text
BEGIN
UPDATE
UPDATE
...
```

The transaction is active.

---

# 51. Partially Committed State

The transaction has executed its final statement, but the system has not yet completed the steps required to guarantee that the transaction can be considered fully committed.

---

# 52. Committed State

The transaction has successfully completed and its changes have been committed.

```text
Transaction
    ↓
COMMIT
    ↓
Committed
```

---

# 53. Failed State

The transaction cannot continue because of an error, system failure, or another condition.

Example:

```text
T1
 ↓
Error
 ↓
Failed
```

---

# 54. Aborted State

The transaction has been rolled back and its effects have been undone.

After abort, a transaction may:

```text
Restart
```

or:

```text
Terminate
```

depending on the system and application.

---

# 55. Transaction State Diagram

```text
              +----------------+
              |     Active     |
              +----------------+
                |            |
                |            |
          Last statement    Error
                |            |
                ↓            ↓
      +----------------+   +--------+
      | Partially      |   | Failed |
      | Committed      |   +--------+
      +----------------+       |
                |              |
          Commit succeeds      |
                |              |
                ↓              ↓
        +-------------+    +---------+
        |  Committed  |    | Aborted |
        +-------------+    +---------+
```

---

# 56. What is a Transaction Log?

A **transaction log** records information about database changes and transaction activity so the DBMS can support recovery.

Conceptually:

```text
Transaction
    ↓
Log records
    ↓
Commit / Abort
    ↓
Recovery if required
```

Logs are an important part of recovery and durability mechanisms.

---

# 57. What is Write-Ahead Logging (WAL)?

**Write-Ahead Logging** is a recovery technique in which required log information is written to stable storage before the corresponding database changes are considered safely persisted.

Simple idea:

```text
Write log
   ↓
Write data
```

not:

```text
Write data
   ↓
Write log
```

The log allows the DBMS to recover from failures.

---

# 58. What is a Checkpoint?

A **checkpoint** is a recovery mechanism that records a known point in the database's processing so that crash recovery does not necessarily need to process the entire history from the beginning.

Conceptually:

```text
Transactions
   ↓
Checkpoint
   ↓
More transactions
   ↓
Crash
   ↓
Recovery starts from a useful recent point
```

---

# 59. What is Recoverability?

A schedule is **recoverable** when a transaction does not commit before the transactions whose changes it has read have committed.

Example:

```text
T1 writes A
T2 reads A
T1 commits
T2 commits
```

This is recoverable.

But:

```text
T1 writes A
T2 reads A
T2 commits
T1 rolls back
```

is not recoverable because T2 committed after reading data from T1 before T1 committed.

---

# 60. What is Cascading Rollback?

A **cascading rollback** can occur when one transaction reads uncommitted data written by another transaction, and the first transaction later rolls back.

Example:

```text
T1 writes A
T2 reads A
T1 rolls back
```

T2 may now need to roll back because it used T1's uncommitted value.

```text
T1 rollback
     ↓
T2 rollback
```

This is called cascading rollback.

---

# 61. What is a Cascadeless Schedule?

In a **cascadeless schedule**, a transaction reads a data item only after the transaction that wrote that item has committed.

Example:

```text
T1 writes A
T1 commits
T2 reads A
```

Therefore, if T1 later does not roll back, T2 does not need to cascade its rollback due to that read.

---

# 62. Recoverable vs Cascadeless

```text
Recoverable
→ A transaction commits only after transactions whose values it read have committed.

Cascadeless
→ Transactions read only committed values.
```

A cascadeless schedule is recoverable.

---

# 63. What are Isolation Levels?

SQL databases provide transaction isolation levels that control the visibility and concurrency behavior of transactions.

The commonly standardized levels are:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

Some DBMSs also provide additional levels or implement these levels with DBMS-specific behavior.

---

# 64. READ UNCOMMITTED

At this isolation level, a transaction may be allowed to read data written by another transaction before that transaction commits.

Therefore, dirty reads can occur.

```text
Dirty Read → Possible
```

It provides weak isolation and potentially higher concurrency.

---

# 65. READ COMMITTED

A transaction generally sees only data committed before its read, so dirty reads are prevented.

However, another transaction may commit changes between two reads of the same row.

Therefore:

```text
Dirty Read → Prevented
Non-repeatable Read → Can occur
```

---

# 66. REPEATABLE READ

This level provides stronger guarantees for repeated reads of the same rows.

In the SQL standard, it prevents dirty and non-repeatable reads, while phantom behavior can still be possible.

However, exact behavior can vary between DBMS implementations.

For interview purposes:

```text
Dirty Read → Prevented
Non-repeatable Read → Prevented
Phantom Read → May occur
```

---

# 67. SERIALIZABLE

**SERIALIZABLE** provides the strongest standard isolation level.

Its goal is to make concurrent execution behave like some serial execution.

Conceptually:

```text
Concurrent execution
       ↓
Equivalent to
       ↓
Serial execution
```

It provides the strongest standard isolation guarantees but can reduce concurrency and increase waiting/conflicts.

---

# 68. Isolation Levels Summary

For the standard anomaly model:

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|---|---|---|---|
| READ UNCOMMITTED | Possible | Possible | Possible |
| READ COMMITTED | Prevented | Possible | Possible |
| REPEATABLE READ | Prevented | Prevented | May be possible |
| SERIALIZABLE | Prevented | Prevented | Prevented |

**Important:** Actual DBMS behavior can differ, especially for `REPEATABLE READ`, because implementations may use different locking or MVCC mechanisms.

---

# 69. Isolation Levels Memory Trick

```text
READ UNCOMMITTED
→ Weakest

READ COMMITTED
→ No Dirty Reads

REPEATABLE READ
→ No Dirty + No Non-Repeatable Reads

SERIALIZABLE
→ Strongest standard isolation
```

---

# 70. What is MVCC?

**MVCC (Multi-Version Concurrency Control)** allows the database to maintain multiple versions of data so that readers and writers can often operate concurrently without directly blocking each other.

Conceptually:

```text
Data
 ↓
Multiple Versions
 ↓
Transaction reads appropriate version
```

MVCC implementations differ between database systems.

---

# 71. Locking vs MVCC

| Locking | MVCC |
|---|---|
| Uses locks to control access | Uses multiple versions of data |
| Can cause readers/writers to wait depending on lock compatibility | Readers can often access an appropriate committed version |
| Widely used in concurrency control | Widely used in modern DBMSs |
| Exact behavior depends on DBMS | Exact behavior depends on DBMS |

---

# 72. What is Optimistic Concurrency Control?

**Optimistic concurrency control** assumes conflicts are relatively uncommon.

A transaction can execute without aggressively locking every resource and checks for conflicts before committing.

Conceptually:

```text
Read / Execute
      ↓
Validate
      ↓
No conflict?
   ↙       ↘
 Yes       No
 ↓          ↓
Commit     Abort/Retry
```

---

# 73. What is Pessimistic Concurrency Control?

**Pessimistic concurrency control** assumes conflicts may occur and uses mechanisms such as locks to prevent unsafe concurrent access.

Conceptually:

```text
Acquire lock
     ↓
Perform operation
     ↓
Release lock
```

---

# 74. Optimistic vs Pessimistic Concurrency Control

| Optimistic | Pessimistic |
|---|---|
| Assumes conflicts are relatively rare | Assumes conflicts are likely |
| Checks for conflicts later | Prevents conflicts using mechanisms such as locks |
| Can require retry/rollback | Can cause waiting/blocking |
| Useful in low-conflict workloads | Useful when conflicts are common |

---

# 75. What is Atomicity vs Consistency?

This is a common interview question.

### Atomicity

Deals with:

```text
All operations or none
```

### Consistency

Deals with:

```text
Valid state → Valid state
```

Example:

```text
Atomicity:
If transfer fails, undo all its changes.

Consistency:
The transaction must preserve database constraints and integrity rules.
```

---

# 76. What is Isolation vs Consistency?

### Isolation

Deals mainly with:

```text
Interaction between concurrent transactions
```

### Consistency

Deals mainly with:

```text
Maintaining valid database states and integrity rules
```

---

# 77. What is Durability vs Atomicity?

### Atomicity

```text
Failed transaction
→ Changes are undone
```

### Durability

```text
Committed transaction
→ Changes survive failures
```

### Easy Memory

```text
Atomicity → Failed transaction doesn't partially apply

Durability → Successful transaction doesn't disappear
```

---

# 78. Frequently Asked Interview Questions

## Q1. What is a transaction?

### Answer

> A transaction is a sequence of database operations treated as one logical unit of work.

---

## Q2. What does ACID stand for?

### Answer

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

---

## Q3. Explain Atomicity.

### Answer

> Atomicity ensures that a transaction is treated as an all-or-nothing unit. If it fails, its applicable changes are rolled back.

---

## Q4. Explain Consistency.

### Answer

> Consistency ensures that a successful transaction preserves database integrity rules and moves the database from one valid state to another.

---

## Q5. Explain Isolation.

### Answer

> Isolation controls how concurrent transactions interact so that their operations do not improperly interfere with one another.

---

## Q6. Explain Durability.

### Answer

> Durability ensures that committed transaction changes survive subsequent system failures according to the DBMS's recovery guarantees.

---

## Q7. What is COMMIT?

### Answer

> COMMIT permanently saves the changes made by the transaction.

---

## Q8. What is ROLLBACK?

### Answer

> ROLLBACK undoes uncommitted changes made by the current transaction.

---

## Q9. What is concurrency control?

### Answer

> Concurrency control manages simultaneous transactions while maintaining correctness and the required isolation guarantees.

---

## Q10. What is serializability?

### Answer

> Serializability is a correctness criterion where a concurrent schedule produces an effect equivalent to some serial execution of the transactions.

---

## Q11. What is a serial schedule?

### Answer

> A serial schedule executes transactions one after another without interleaving their operations.

---

## Q12. What is a concurrent schedule?

### Answer

> A concurrent schedule allows operations from multiple transactions to be interleaved.

---

## Q13. What is conflict serializability?

### Answer

> A schedule is conflict-serializable if it can be transformed into a serial schedule by swapping non-conflicting operations.

---

## Q14. What is a dirty read?

### Answer

> A dirty read occurs when a transaction reads data written by another transaction before that transaction commits.

---

## Q15. What is a non-repeatable read?

### Answer

> A non-repeatable read occurs when the same row is read twice by a transaction and the value differs because another committed transaction modified it between the reads.

---

## Q16. What is a phantom read?

### Answer

> A phantom read occurs when repeating a query returns a different set of rows because another transaction changed rows that satisfy the query condition.

---

## Q17. What is a lost update?

### Answer

> A lost update occurs when one transaction's update is overwritten by another concurrent transaction's update.

---

## Q18. What is a shared lock?

### Answer

> A shared lock is generally used for reading and allows compatible shared locks to coexist while preventing conflicting exclusive access.

---

## Q19. What is an exclusive lock?

### Answer

> An exclusive lock is used for modifying data and prevents conflicting concurrent access to that data item.

---

## Q20. What is 2PL?

### Answer

> Two-Phase Locking is a concurrency-control protocol with a growing phase, where locks are acquired, and a shrinking phase, where locks are released. Basic 2PL guarantees conflict serializability.

---

## Q21. What is deadlock?

### Answer

> A deadlock occurs when transactions wait for each other in a cycle and none can proceed.

---

## Q22. How can deadlocks be handled?

### Answer

> Deadlocks can be prevented, detected, or recovered from by aborting one or more transactions. Lock ordering and wait-for graphs are common concepts used in deadlock handling.

---

## Q23. What is starvation?

### Answer

> Starvation occurs when a transaction waits for an excessively long time because other transactions repeatedly receive the resources or priority it needs.

---

## Q24. What are isolation levels?

### Answer

The commonly standardized isolation levels are:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

---

## Q25. Which is the strongest standard isolation level?

### Answer

> SERIALIZABLE is the strongest standard SQL isolation level.

---

## Q26. Which isolation level allows dirty reads?

### Answer

> READ UNCOMMITTED can allow dirty reads.

---

## Q27. Which isolation level prevents dirty reads but may allow non-repeatable reads?

### Answer

> READ COMMITTED.

---

## Q28. What is MVCC?

### Answer

> MVCC, or Multi-Version Concurrency Control, maintains multiple versions of data so transactions can often read an appropriate version while other transactions modify newer versions.

---

## Q29. What is a transaction log?

### Answer

> A transaction log records transaction and data-change information used to support recovery and durability.

---

## Q30. What is Write-Ahead Logging?

### Answer

> Write-Ahead Logging requires the necessary log information to be persisted before the corresponding database changes are considered safely persisted.

---

# 79. Scenario-Based Interview Questions

## Scenario 1: Bank Transfer

A transaction transfers ₹500 from Account A to Account B.

The amount is deducted from A, but adding it to B fails.

### Question

Which ACID property is most directly involved?

### Answer

**Atomicity.**

The transaction should not leave only half of the transfer applied.

---

## Scenario 2: Reading Uncommitted Data

```text
T1:
UPDATE salary = 60000

T2:
READ salary = 60000

T1:
ROLLBACK
```

### Question

What problem occurred?

### Answer

**Dirty read.**

T2 read a value that T1 had not committed.

---

## Scenario 3: Same Row, Different Value

```text
T1:
SELECT balance → 5000

T2:
UPDATE balance → 4000
COMMIT

T1:
SELECT balance → 4000
```

### Question

What problem occurred?

### Answer

**Non-repeatable read.**

---

## Scenario 4: New Row Appears

```text
T1:
SELECT * FROM employees
WHERE salary > 50000;

→ 5 rows

T2:
INSERT employee with salary = 60000
COMMIT

T1:
SELECT * FROM employees
WHERE salary > 50000;

→ 6 rows
```

### Question

What problem occurred?

### Answer

**Phantom read.**

---

## Scenario 5: Two Transactions Wait for Each Other

```text
T1:
Locks A
Waits for B

T2:
Locks B
Waits for A
```

### Question

What is this?

### Answer

**Deadlock.**

---

## Scenario 6: Composite Schedule

Suppose a precedence graph contains:

```text
T1 → T2
T2 → T3
T1 → T3
```

### Question

Is there a cycle?

### Answer

No.

Therefore, based on the precedence graph, the schedule is conflict-serializable.

---

## Scenario 7: Cyclic Graph

Suppose:

```text
T1 → T2
T2 → T1
```

### Question

What does this indicate?

### Answer

There is a cycle.

Therefore, the schedule is **not conflict-serializable**.

If this is a wait-for graph representing lock waits, the cycle indicates a deadlock.

---

# 80. Most Important Differences

## ACID vs Concurrency Control

```text
ACID
→ Properties of reliable transactions

Concurrency Control
→ Techniques for managing simultaneous transactions
```

---

## Serial vs Serializable

```text
Serial
→ Actually executes transactions one after another

Serializable
→ Concurrent schedule behaves equivalently to a serial schedule
```

---

## Deadlock vs Lost Update

```text
Deadlock
→ Transactions wait for each other

Lost Update
→ One transaction's update overwrites another
```

---

## Dirty Read vs Non-Repeatable Read

```text
Dirty Read
→ Reads uncommitted data

Non-Repeatable Read
→ Same row produces different committed values across reads
```

---

## Non-Repeatable Read vs Phantom Read

```text
Non-Repeatable Read
→ Existing row's value changes

Phantom Read
→ Result set changes because matching rows appear/disappear
```

---

# 81. Quick Revision Sheet

```text
TRANSACTION
───────────
Sequence of database operations
treated as one logical unit


ACID
────
A → Atomicity
    All or nothing

C → Consistency
    Valid state → Valid state

I → Isolation
    Controls concurrent interaction

D → Durability
    Committed changes survive failures


COMMANDS
────────
COMMIT
→ Save transaction

ROLLBACK
→ Undo uncommitted changes


CONCURRENCY
───────────
Multiple transactions execute
during overlapping periods


SCHEDULE
────────
Order/interleaving of transaction operations


SERIAL
──────
Transactions execute one after another


SERIALIZABLE
────────────
Concurrent schedule behaves like
some serial schedule


CONFLICT
────────
Same data
+
Different transactions
+
At least one WRITE


CONFLICT TYPES
──────────────
Read-Write
Write-Read
Write-Write


CONCURRENCY PROBLEMS
────────────────────
Dirty Read
→ Uncommitted data

Non-Repeatable Read
→ Same row, different value

Phantom Read
→ Same query, different rows

Lost Update
→ One update overwritten


LOCKS
─────
S-lock
→ Shared / Read

X-lock
→ Exclusive / Write


2PL
───
Growing
→ Acquire locks

Shrinking
→ Release locks


DEADLOCK
────────
Circular waiting


ISOLATION LEVELS
────────────────
READ UNCOMMITTED
→ Dirty reads possible

READ COMMITTED
→ Dirty reads prevented

REPEATABLE READ
→ Dirty + non-repeatable reads prevented
   under the standard model

SERIALIZABLE
→ Strongest standard isolation level


RECOVERY
────────
Transaction Log
→ Recovery information

WAL
→ Log before corresponding data persistence

Checkpoint
→ Useful recovery point
```

# 82. Final Interview Priority

If you have limited time, prepare these topics first:

```text
⭐⭐⭐⭐⭐
1. What is a transaction?
2. ACID properties
3. COMMIT and ROLLBACK
4. Concurrency control
5. Serial vs concurrent schedule
6. Serializability
7. Dirty read
8. Non-repeatable read
9. Phantom read
10. Lost update
11. Shared vs exclusive locks
12. Two-Phase Locking
13. Deadlock
14. Isolation levels
15. READ COMMITTED vs REPEATABLE READ vs SERIALIZABLE

⭐⭐⭐⭐
16. Conflict serializability
17. Precedence graph
18. Recoverable schedules
19. Cascading rollback
20. Cascadeless schedules
21. MVCC

⭐⭐⭐
22. Transaction states
23. Transaction log
24. Write-Ahead Logging
25. Checkpoints
26. Optimistic vs pessimistic concurrency control
27. Wait-for graph
28. Starvation
```

# 83. One-Minute Interview Revision

```text
Transaction
→ One logical unit of work

ACID
→ Atomicity
→ Consistency
→ Isolation
→ Durability

COMMIT
→ Save

ROLLBACK
→ Undo uncommitted changes

Concurrency
→ Multiple transactions overlap

Serial
→ One transaction at a time

Serializable
→ Concurrent result equivalent to serial execution

Dirty Read
→ Read uncommitted data

Non-Repeatable Read
→ Same row, different value

Phantom Read
→ Same query, different rows

Lost Update
→ One update overwrites another

S-Lock
→ Read

X-Lock
→ Write

2PL
→ Growing + Shrinking

Deadlock
→ Circular waiting

Isolation Levels
→ Read Uncommitted
→ Read Committed
→ Repeatable Read
→ Serializable

MVCC
→ Multiple versions of data
```

# 84. Key Interview Takeaway

The most important chain to understand is:

```text
TRANSACTIONS
     ↓
ACID
     ↓
Reliable Database Operations
     ↓
CONCURRENT TRANSACTIONS
     ↓
Concurrency Problems
     ↓
Dirty Read
Non-Repeatable Read
Phantom Read
Lost Update
     ↓
Concurrency Control
     ↓
Locks / 2PL / MVCC
     ↓
Serializability
     ↓
Deadlocks & Recovery
     ↓
Isolation Levels
```

If you can explain this chain and solve simple transaction/schedule scenarios, you are well prepared for the transactions, ACID, and concurrency portion of a typical DBMS interview.