# Process Synchronization

## 1. What is Process Synchronization?

**Process synchronization** is the coordination of multiple processes or threads so that they can safely access shared resources and produce correct results.

It is especially important when multiple processes/threads execute concurrently and access shared data.

```text
Process 1 ──┐
            ├──→ Shared Resource
Process 2 ──┘
                  ↓
            Synchronization
```

---

# 2. Why is Synchronization Needed?

Consider:

```text
count = 5
```

Two threads simultaneously execute:

```text
count = count + 1
```

The operation may involve:

```text
Read
↓
Add
↓
Write
```

Possible execution:

```text
Thread 1 → Read 5
Thread 2 → Read 5
Thread 1 → Write 6
Thread 2 → Write 6
```

Expected:

```text
7
```

Actual:

```text
6
```

This happens because both threads accessed shared data without proper coordination.

---

# 3. What is a Race Condition?

A **race condition** occurs when the result of a program depends on the timing or ordering of concurrent operations accessing shared data.

Example:

```text
Thread 1 ──┐
           ├──→ Shared Variable
Thread 2 ──┘
             ↓
       Race Condition
```

### Interview Answer

> A race condition occurs when multiple processes or threads access shared data concurrently and the final result depends on the order in which their operations execute.

---

# 4. What is a Critical Section?

A **critical section** is the part of a program where shared data or resources are accessed.

Example:

```text
Entry Section
      ↓
Critical Section
      ↓
Exit Section
      ↓
Remainder Section
```

The critical section needs appropriate synchronization so that concurrent execution does not produce incorrect results.

---

# 5. Critical Section Problem

The **critical-section problem** is the problem of designing a protocol so concurrent processes can safely execute their critical sections.

A good solution should satisfy three important requirements:

```text
1. Mutual Exclusion
2. Progress
3. Bounded Waiting
```

---

# 6. Mutual Exclusion

**Mutual exclusion** means that at most one process/thread can execute a particular critical section protecting the same shared resource at a time.

```text
Thread 1
   ↓
Critical Section
   ↓
Thread 2 must wait
```

This prevents simultaneous conflicting access.

---

# 7. Progress

**Progress** means that if no process is currently inside the critical section and some processes want to enter, the decision about who enters next should not be postponed indefinitely.

In simple terms:

> If the critical section is free, an eligible waiting process should eventually be allowed to enter.

---

# 8. Bounded Waiting

**Bounded waiting** means there should be a limit on how many times other processes can enter their critical sections after a process has requested entry.

This helps prevent **starvation**.

```text
Process P1 wants to enter
        ↓
Other processes repeatedly enter
        ↓
P1 waits forever ❌
```

A proper solution should prevent this kind of indefinite waiting.

---

# 9. Mutual Exclusion vs Synchronization

### Mutual Exclusion

> Ensures that only one thread/process at a time accesses a protected critical section.

### Synchronization

> Coordinates concurrent processes/threads so they access shared resources in the correct and safe manner.

Therefore:

```text
Mutual Exclusion
       ↓
One-at-a-time access

Synchronization
       ↓
Broader coordination
```

---

# 10. What is a Mutex?

**Mutex** stands for **Mutual Exclusion**.

A mutex is a synchronization mechanism used to protect a critical section by allowing only one thread to hold the lock at a time.

Example:

```text
Thread 1
   ↓
Lock Mutex
   ↓
Critical Section
   ↓
Unlock Mutex

Thread 2
   ↓
Wait
```

---

# 11. How Does a Mutex Work?

Basic flow:

```text
        Mutex
          ↓
     Is it available?
       /       \
     Yes        No
      ↓          ↓
   Lock it     Wait
      ↓
Critical Section
      ↓
   Unlock
```

Only one thread can own the mutex at a time.

---

# 12. What is a Semaphore?

A **semaphore** is a synchronization mechanism based on a counter used to coordinate access to shared resources or signal between concurrent execution flows.

A semaphore is commonly manipulated using operations conceptually called:

```text
wait()
signal()
```

These may also be called:

```text
P()
V()
```

or:

```text
down()
up()
```

depending on the terminology used.

---

# 13. Binary Semaphore

A **binary semaphore** has two logical states/count values:

```text
0
1
```

It can be used to control access to a resource that should have at most one active user at a time.

Conceptually:

```text
1 → Available
0 → Not available
```

---

# 14. Counting Semaphore

A **counting semaphore** can represent multiple available instances of a resource.

Example:

```text
3 printers available

Semaphore = 3
```

When a process uses one:

```text
3 → 2
```

When it releases one:

```text
2 → 3
```

This allows up to the configured number of processes/threads to access the resource concurrently.

---

# 15. Mutex vs Semaphore

| Mutex | Semaphore |
|---|---|
| Primarily used for mutual exclusion | Used for signaling and resource counting |
| Usually has ownership semantics | Generally does not have mutex-style ownership |
| One owner at a time | Counter can represent multiple resource instances |
| Commonly protects a critical section | Can coordinate access to multiple resources |
| Typically lock/unlock | Commonly wait/signal |

### Interview Answer

> A mutex is primarily an ownership-based mutual-exclusion mechanism, while a semaphore is a counter-based synchronization mechanism that can be used for signaling or controlling access to multiple resource instances.

---

# 16. What is a Monitor?

A **monitor** is a higher-level synchronization construct that encapsulates shared data, operations on that data, and synchronization rules.

Conceptually:

```text
Monitor
├── Shared Data
├── Operations
└── Synchronization
```

Only one thread/process can execute inside a monitor at a time under the classic monitor model.

Monitors can also use **condition variables** to allow threads to wait for particular conditions.

---

# 17. Mutex vs Monitor

| Mutex | Monitor |
|---|---|
| Low-level synchronization primitive | Higher-level synchronization construct |
| Explicit lock/unlock commonly used | Synchronization is integrated into the construct |
| Protects shared resource/critical section | Encapsulates shared data and operations |
| Easier to misuse if locking is manual | Can provide safer structured synchronization |

---

# 18. What is a Spinlock?

A **spinlock** is a lock where a thread repeatedly checks whether the lock has become available instead of immediately blocking.

Example:

```text
Thread
  ↓
Try Lock
  ↓
Unavailable
  ↓
Keep Checking
  ↓
Available
  ↓
Acquire
```

This is called **busy waiting**.

Spinlocks can be useful when the expected waiting time is very short, but wasting CPU cycles while spinning can be inefficient for long waits.

---

# 19. Spinlock vs Mutex

| Spinlock | Mutex |
|---|---|
| Thread repeatedly checks lock | Thread can block/wait |
| Uses CPU while spinning | Can give CPU to other work while waiting |
| Useful for very short waits in suitable environments | Better for longer waits |
| Can waste CPU if held too long | Avoids busy-waiting in typical blocking mutex implementations |

---

# 20. What is Busy Waiting?

**Busy waiting** occurs when a process/thread repeatedly checks a condition instead of blocking.

Example:

```text
while lock is unavailable:
    keep checking
```

The CPU is being used even though the thread is not doing useful work.

---

# 21. What is Starvation?

**Starvation** occurs when a process/thread waits for an excessively long or indefinite period because other processes/threads repeatedly get access to the required resource.

Example:

```text
P1 waiting
 ↓
P2 enters
 ↓
P3 enters
 ↓
P4 enters
 ↓
P1 still waiting
```

---

# 22. How Can Starvation Be Prevented?

Possible approaches include:

```text
Fair scheduling
First-come-first-served policies
Aging
Fair lock implementations
Bounded waiting
```

---

# 23. What is Deadlock?

A **deadlock** occurs when a set of processes/threads are permanently blocked because each is waiting for a resource or event that another member of the set is preventing from becoming available.

Example:

```text
Thread 1
holds Lock A
waits for Lock B

Thread 2
holds Lock B
waits for Lock A
```

```text
T1 → waits for T2
T2 → waits for T1
```

Deadlocks are covered in detail in:

```text
05-deadlocks.md
```

---

# 24. Race Condition vs Deadlock

| Race Condition | Deadlock |
|---|---|
| Result depends on execution timing/order | Processes/threads become stuck waiting |
| Can produce incorrect results | Prevents progress for involved processes |
| Usually caused by unsafe concurrent access | Caused by resource/waiting relationships |
| Synchronization can prevent many race conditions | Deadlock handling requires specific prevention/avoidance/detection techniques |

---

# 25. Deadlock vs Starvation

### Deadlock

```text
Processes wait for each other
↓
No progress
```

### Starvation

```text
One process waits excessively
↓
Other processes continue
```

### Interview Answer

> In deadlock, the involved processes cannot proceed because of a circular or otherwise blocking dependency. In starvation, a process waits indefinitely or excessively while other processes continue to make progress.

---

# 26. Producer-Consumer Problem

The **Producer-Consumer Problem** is a classic synchronization problem.

```text
Producer
   ↓
  Buffer
   ↓
Consumer
```

The producer adds items to the buffer, while the consumer removes items.

Problems:

```text
Producer must not add to a full buffer
Consumer must not remove from an empty buffer
Concurrent buffer access must be synchronized
```

---

# 27. Producer-Consumer Using Semaphores

For a bounded buffer, a common conceptual setup is:

```text
empty → number of empty slots
full  → number of filled slots
mutex → protects buffer access
```

Initially:

```text
empty = buffer size
full = 0
```

Producer conceptually:

```text
wait(empty)
wait(mutex)

add item

signal(mutex)
signal(full)
```

Consumer conceptually:

```text
wait(full)
wait(mutex)

remove item

signal(mutex)
signal(empty)
```

The exact implementation varies by language and OS.

---

# 28. Readers-Writers Problem

The **Readers-Writers Problem** deals with concurrent access to shared data.

Rules:

```text
Multiple readers
→ Can read simultaneously

Writer
→ Requires exclusive access
```

Example:

```text
Reader 1 ──┐
Reader 2 ──┼──→ Shared Data
Reader 3 ──┘
```

Multiple readers can often proceed together.

But:

```text
Writer
   ↓
Exclusive access
```

No conflicting readers/writers should access the protected data simultaneously.

---

# 29. Dining Philosophers Problem

The **Dining Philosophers Problem** is a classic synchronization problem used to illustrate issues such as:

```text
Deadlock
Starvation
Resource contention
Synchronization
```

Conceptually:

```text
P1 ─ Fork ─ P2
 |           |
Fork       Fork
 |           |
P5 ─ Fork ─ P3
      |
     P4
```

Each philosopher needs two forks to eat.

If every philosopher picks up one fork and waits for the other:

```text
P1 waits for P2's fork
P2 waits for P3's fork
P3 waits for P4's fork
...
```

A deadlock can occur.

---

# 30. What is Peterson's Solution?

**Peterson's algorithm** is a classic software solution to the critical-section problem for **two processes** under its traditional assumptions.

It uses shared variables such as:

```text
flag[]
turn
```

Its purpose is to provide:

```text
Mutual Exclusion
Progress
Bounded Waiting
```

It is mainly important as a theoretical OS interview topic rather than a modern general-purpose synchronization mechanism.

---

# 31. What are Atomic Operations?

An **atomic operation** is an operation that appears indivisible with respect to concurrent observers.

Example:

```text
Thread 1 → atomic increment
Thread 2 → atomic increment
```

The operation cannot be observed as a partially completed operation in the way a non-atomic read-modify-write sequence can.

Atomic operations are commonly used to implement synchronization primitives and lock-free algorithms.

---

# 32. What is Lock Contention?

**Lock contention** occurs when multiple threads frequently try to acquire the same lock and have to wait for one another.

```text
Thread 1 ──┐
Thread 2 ──┤
Thread 3 ──┼──→ Same Lock
Thread 4 ──┘
```

High contention can reduce performance.

---

# 33. How Can Lock Contention Be Reduced?

Common approaches include:

```text
Reduce time spent holding locks
Reduce unnecessary shared data
Use finer-grained locking when appropriate
Use suitable concurrent data structures
Avoid unnecessary synchronization
```

The correct strategy depends on the workload and system.

---

# 34. Important Scenario

### Question

Two threads update the same shared variable simultaneously. What problem can occur?

### Answer

> A race condition can occur if the update is not atomic or properly synchronized.

---

### Question

How would you solve it?

Possible solutions:

```text
Mutex
Semaphore
Atomic operation
Other appropriate synchronization mechanism
```

---

# 35. Important Scenario

### Question

A buffer has capacity 10. Multiple producers and consumers access it. What synchronization is required?

### Answer

You need to ensure:

```text
Producer
→ Cannot add when buffer is full

Consumer
→ Cannot remove when buffer is empty

Buffer operations
→ Must be protected from conflicting concurrent access
```

A classic solution uses:

```text
empty semaphore
full semaphore
mutex
```

---

# 36. Important Scenario

### Question

A thread acquires Lock A and waits for Lock B. Another thread acquires Lock B and waits for Lock A. What is the problem?

### Answer

> This is a deadlock caused by circular waiting.

```text
T1 → Lock A → waits for B
T2 → Lock B → waits for A
```

---

# 37. Important Scenario

### Question

Several threads continuously compete for a lock, and one thread rarely gets it. What problem might this indicate?

### Answer

> It may indicate starvation or unfair lock/scheduling behavior.

A fairer synchronization or scheduling policy may be needed.

---

# 38. Important Interview Questions

Prepare these especially well:

```text
1. What is process synchronization?

2. Why is synchronization needed?

3. What is a race condition?

4. Give an example of a race condition.

5. What is a critical section?

6. What is the critical-section problem?

7. What are the requirements of a critical-section solution?

8. What is mutual exclusion?

9. What is progress?

10. What is bounded waiting?

11. What is a mutex?

12. How does a mutex work?

13. What is a semaphore?

14. What is a binary semaphore?

15. What is a counting semaphore?

16. Mutex vs semaphore?

17. What is a monitor?

18. What is a spinlock?

19. Spinlock vs mutex?

20. What is busy waiting?

21. What is starvation?

22. How can starvation be prevented?

23. What is deadlock?

24. Race condition vs deadlock?

25. Deadlock vs starvation?

26. What is the Producer-Consumer problem?

27. How can semaphores solve Producer-Consumer?

28. What is the Readers-Writers problem?

29. What is the Dining Philosophers problem?

30. What is Peterson's solution?

31. What are atomic operations?

32. What is lock contention?

33. How can lock contention be reduced?

34. How would you synchronize access to a shared variable?

35. How would you synchronize a bounded buffer?
```

---

# 39. Quick Revision

```text
PROCESS SYNCHRONIZATION
→ Coordinate concurrent processes/threads

RACE CONDITION
→ Result depends on timing/order

CRITICAL SECTION
→ Code that accesses shared resource/data

MUTUAL EXCLUSION
→ Only one thread/process in protected critical section

PROGRESS
→ If critical section is free, selection should not be postponed indefinitely

BOUNDED WAITING
→ Prevent indefinite waiting for entry

MUTEX
→ Mutual exclusion lock
→ One owner at a time

SEMAPHORE
→ Counter-based synchronization/signaling

BINARY SEMAPHORE
→ 0 / 1

COUNTING SEMAPHORE
→ Multiple resource instances

MONITOR
→ Higher-level synchronization construct

SPINLOCK
→ Repeatedly checks lock
→ Busy waiting

STARVATION
→ Excessive/indefinite waiting while others progress

DEADLOCK
→ Processes/threads permanently blocked by waiting dependencies

PRODUCER-CONSUMER
→ Producer adds
→ Consumer removes
→ Buffer must be synchronized

READERS-WRITERS
→ Multiple readers can read
→ Writer requires exclusive access

DINING PHILOSOPHERS
→ Classic synchronization/resource-sharing problem

PETERSON'S SOLUTION
→ Classic two-process critical-section solution

ATOMIC OPERATION
→ Appears indivisible

LOCK CONTENTION
→ Multiple threads compete for same lock
```

---

# 40. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Race Condition
Critical Section
Mutual Exclusion
Progress
Bounded Waiting
Mutex
Semaphore
Binary vs Counting Semaphore
Mutex vs Semaphore
Synchronization
Deadlock vs Starvation
Producer-Consumer
Readers-Writers
```

## ⭐⭐⭐ Good to Know

```text
Monitor
Spinlock
Busy Waiting
Dining Philosophers
Peterson's Solution
Atomic Operations
Lock Contention
```

> **For placement interviews, focus deeply on Race Condition → Critical Section → Mutex → Semaphore → Producer-Consumer.** These form the core synchronization chain and are among the most useful concepts to understand before moving to **Deadlocks**.