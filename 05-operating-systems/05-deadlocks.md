# Deadlocks

## 1. What is a Deadlock?

A **deadlock** is a situation where two or more processes/threads are permanently blocked because each is waiting for a resource or event that another process/thread is preventing from becoming available.

### Simple Example

```text
Process P1
holds Resource A
waits for Resource B

Process P2
holds Resource B
waits for Resource A
```

```text
P1 → A → waits for B
              ↑
              |
P2 → B → waits for A
```

Neither process can continue.

### Interview Answer

> Deadlock is a situation where a set of processes or threads are permanently blocked because each is waiting for a resource held by another process in the set.

---

# 2. Simple Real-Life Example

Imagine:

```text
Person A has Pen
Person B has Paper

A needs Paper to continue
B needs Pen to continue
```

```text
A → waits for Paper
B → waits for Pen
```

Neither gives up what they have.

This is similar to a deadlock in an operating system.

---

# 3. Resources in Deadlock

A resource is something a process needs to execute.

Examples:

```text
CPU
Memory
Files
Printers
I/O devices
Locks
Database resources
```

A process may:

```text
Request Resource
       ↓
Use Resource
       ↓
Release Resource
```

---

# 4. How Does Deadlock Occur?

A typical sequence is:

```text
P1 requests A
P1 gets A

P2 requests B
P2 gets B

P1 requests B
P1 waits

P2 requests A
P2 waits
```

Now:

```text
P1 waits for P2
P2 waits for P1
```

Deadlock occurs.

---

# 5. Four Necessary Conditions for Deadlock

A deadlock can occur only when **all four Coffman conditions** hold simultaneously:

```text
1. Mutual Exclusion
2. Hold and Wait
3. No Preemption
4. Circular Wait
```

These four conditions are extremely important for interviews.

---

# 6. Mutual Exclusion

**Mutual exclusion** means at least one resource is non-shareable and can be held by only one process at a time.

Example:

```text
Printer
   ↓
P1 is using it
   ↓
P2 must wait
```

The resource cannot be simultaneously allocated to both processes.

---

# 7. Hold and Wait

**Hold and Wait** means a process is holding at least one resource while waiting to acquire additional resources.

Example:

```text
P1
holds A
  +
waits for B
```

---

# 8. No Preemption

**No Preemption** means a resource cannot simply be forcibly taken away from a process holding it; the process must release it voluntarily or according to the resource's rules.

Example:

```text
P1 holds A
P2 wants A

OS cannot forcibly take A
        ↓
P2 waits
```

---

# 9. Circular Wait

**Circular Wait** means there is a circular chain of processes where each process waits for a resource held by the next process.

Example:

```text
P1 waits for P2
P2 waits for P3
P3 waits for P1
```

```text
P1 → P2 → P3
↑           ↓
└───────────┘
```

---

# 10. Easy Way to Remember the Four Conditions

Remember:

```text
M H N C
```

```text
M → Mutual Exclusion
H → Hold and Wait
N → No Preemption
C → Circular Wait
```

Or:

> **"My Hungry Neighbor Circles"**

The exact mnemonic is less important than remembering all four conditions.

---

# 11. Why are the Four Conditions Important?

The four conditions are important because:

> **If at least one of the four necessary conditions is prevented, deadlock cannot occur under the corresponding model.**

This gives us the basic idea behind **deadlock prevention**.

```text
Break one condition
        ↓
Prevent deadlock
```

---

# 12. Resource Allocation Graph

A **Resource Allocation Graph (RAG)** is used to represent processes, resources, requests, and allocations.

We use:

```text
Circle → Process
Square → Resource
```

Example:

```text
P1 → R1
```

means:

```text
P1 is requesting R1
```

While:

```text
R1 → P1
```

means:

```text
R1 is allocated to P1
```

---

# 13. Resource Allocation Graph Example

Consider:

```text
R1 → P1 → R2
↑           ↓
└── P2 ←────┘
```

A cycle can indicate a possible deadlock.

For a system where each resource type has **only one instance**, a cycle in the resource-allocation graph indicates deadlock.

With multiple instances of resource types, a cycle alone does **not necessarily** prove deadlock.

---

# 14. Deadlock Prevention

**Deadlock prevention** ensures that at least one of the four necessary deadlock conditions is never allowed to hold.

```text
Deadlock Conditions
        ↓
Prevent at least one
        ↓
No Deadlock
```

Examples:

```text
Prevent Hold and Wait
Prevent Circular Wait
Allow Preemption where possible
Make resources shareable where appropriate
```

---

# 15. Preventing Mutual Exclusion

If a resource can safely be made shareable, mutual exclusion can be reduced or eliminated for that resource.

However, some resources are inherently non-shareable.

Example:

```text
Printer
```

You cannot simply allow multiple processes to perform conflicting physical operations simultaneously.

Therefore, this condition cannot always be eliminated.

---

# 16. Preventing Hold and Wait

Require a process to request all resources it needs before it begins execution.

Example:

```text
P1 needs:
A + B

Request A and B together
        ↓
Then execute
```

This prevents:

```text
Hold A
while waiting for B
```

### Disadvantage

```text
Resources may remain unused
↓
Lower resource utilization
```

---

# 17. Preventing No Preemption

If a process requests a resource that cannot immediately be granted, the system may require it to release resources it currently holds, where safe and feasible.

Example:

```text
P1 holds A
P1 requests B

B unavailable
     ↓
Release A
     ↓
Try again later
```

This approach is not applicable to every resource.

---

# 18. Preventing Circular Wait

Impose a fixed ordering on resource types.

Example:

```text
R1 < R2 < R3
```

Processes must request resources in increasing order.

Correct:

```text
R1 → R2 → R3
```

Incorrect:

```text
R3 → R1
```

This prevents circular wait.

---

# 19. Deadlock Avoidance

**Deadlock avoidance** dynamically examines resource allocation requests and grants them only if doing so keeps the system in a **safe state**.

The most famous algorithm is:

```text
Banker's Algorithm
```

---

# 20. Prevention vs Avoidance

| Prevention | Avoidance |
|---|---|
| Ensures at least one deadlock condition cannot hold | Dynamically checks whether allocation is safe |
| Uses restrictions/rules | Makes decisions based on current state |
| Deadlock is structurally prevented | Allocation is granted only when safe |
| Can reduce flexibility/resource utilization | Requires additional information about resource needs |

### Easy Interview Answer

> Deadlock prevention breaks at least one necessary deadlock condition, while deadlock avoidance checks resource allocation decisions dynamically to ensure the system remains in a safe state.

---

# 21. What is a Safe State?

A system is in a **safe state** if there exists some order in which all processes can obtain the resources they need and finish without causing deadlock.

This order is called a:

```text
Safe Sequence
```

Example:

```text
P2 → P1 → P3
```

If such an order exists, the system is safe.

---

# 22. What is an Unsafe State?

An **unsafe state** is a state from which the system cannot guarantee that all processes can complete without deadlock.

Important:

```text
Unsafe ≠ necessarily already deadlocked
```

An unsafe state means deadlock **may become possible**.

---

# 23. Safe vs Unsafe vs Deadlocked

```text
Safe
 ↓
Completion can be guaranteed with some safe sequence

Unsafe
 ↓
No guaranteed safe sequence

Deadlocked
 ↓
Processes are already stuck
```

Therefore:

> Every deadlocked state is unsafe, but every unsafe state is not necessarily already deadlocked.

---

# 24. Banker's Algorithm

The **Banker's Algorithm** is a deadlock-avoidance algorithm.

It checks whether granting a resource request leaves the system in a safe state.

Conceptually:

```text
Process requests resources
        ↓
Pretend to allocate
        ↓
Check safe state
     /       \
   Safe      Unsafe
    ↓           ↓
 Grant       Don't grant
```

---

# 25. Why is it Called Banker's Algorithm?

It is based on an analogy with a bank.

A bank has:

```text
Limited resources
```

It gives loans only if it can still satisfy all customers' maximum possible requirements without reaching an unsafe state.

Similarly, the OS allocates resources only if the resulting state remains safe.

---

# 26. Important Banker's Algorithm Terms

You should know these terms:

```text
Available
Maximum
Allocation
Need
```

The important relationship is:

```text
Need = Maximum - Allocation
```

---

# 27. Available

**Available** represents the number of currently available instances of each resource type.

Example:

```text
Available:
A = 3
B = 2
C = 1
```

---

# 28. Maximum

**Maximum** represents the maximum number of resources of each type that a process may need.

Example:

```text
P1:
Maximum = [3, 2, 2]
```

---

# 29. Allocation

**Allocation** represents the resources currently allocated to a process.

Example:

```text
P1:
Allocation = [1, 1, 0]
```

---

# 30. Need

**Need** represents the remaining resources that a process may still require to complete.

Formula:

```text
Need = Maximum - Allocation
```

Example:

```text
Maximum    = [3, 2, 2]
Allocation = [1, 1, 0]

Need       = [2, 1, 2]
```

---

# 31. Deadlock Detection

**Deadlock detection** allows deadlock to occur and then checks whether a deadlock exists.

```text
Allow allocations
       ↓
System operates
       ↓
Run detection algorithm
       ↓
Deadlock?
```

If detected, the OS can attempt recovery.

---

# 32. Prevention vs Avoidance vs Detection

| Technique | Main Idea |
|---|---|
| Prevention | Break at least one necessary condition |
| Avoidance | Grant requests only if state remains safe |
| Detection | Allow deadlock and detect it afterward |
| Recovery | Take action after detecting deadlock |

This comparison is frequently asked in interviews.

---

# 33. Deadlock Recovery

After detecting deadlock, the OS can attempt recovery.

Common approaches include:

```text
Terminate processes
Preempt resources
Rollback/restart processes where supported
```

---

# 34. Process Termination for Recovery

One recovery strategy is to terminate one or more processes involved in the deadlock.

Example:

```text
P1 ↔ P2 ↔ P3
     ↓
Terminate P2
     ↓
Resources released
     ↓
Others may continue
```

The choice should consider factors such as:

```text
Priority
Resources held
Work already completed
Cost of restarting
```

---

# 35. Resource Preemption for Recovery

The system may take a resource from one process and give it to another, when the resource and application semantics permit safe preemption.

```text
P1 holds Resource A
       ↓
Preempt A
       ↓
Give A to P2
```

Challenges include:

```text
Selecting victim
Rollback
Starvation
Consistency
```

---

# 36. Deadlock vs Livelock

### Deadlock

Processes are blocked and make no progress.

```text
P1 waits
P2 waits
```

### Livelock

Processes remain active and keep changing state, but still make no useful progress.

```text
P1 → changes action
P2 → changes action
P1 → changes again
P2 → changes again
```

### Interview Answer

> In deadlock, processes are stuck waiting. In livelock, processes remain active but continuously respond to each other without making useful progress.

---

# 37. Deadlock vs Starvation

| Deadlock | Starvation |
|---|---|
| Processes are stuck due to waiting dependencies | A process waits excessively while others continue |
| Involved processes cannot make progress | Other processes may continue making progress |
| Often involves circular waiting | Can result from unfair scheduling/resource allocation |
| Requires deadlock handling | Fairness/aging can help address it |

---

# 38. Deadlock Example with Locks

Consider:

```text
Thread 1:
lock(A)
lock(B)

Thread 2:
lock(B)
lock(A)
```

Possible execution:

```text
Thread 1 → locks A
Thread 2 → locks B

Thread 1 → waits for B
Thread 2 → waits for A
```

Result:

```text
Deadlock
```

### Solution

Acquire locks in the same global order:

```text
A → B
```

Both threads follow:

```text
lock(A)
lock(B)
```

This prevents circular wait.

---

# 39. How Can Deadlock Be Prevented in Locking Code?

Common techniques:

```text
1. Acquire locks in a consistent global order.

2. Avoid holding locks longer than necessary.

3. Use timeout-based or try-lock mechanisms where appropriate.

4. Avoid unnecessary nested locks.

5. Release locks reliably.
```

The exact technique depends on the programming environment.

---

# 40. Important Interview Scenario

### Question

Two threads acquire two locks in opposite order. What problem can occur?

### Answer

> A deadlock can occur due to circular waiting.

```text
T1:
Lock A → waits for B

T2:
Lock B → waits for A
```

### Solution

Use a consistent lock ordering:

```text
A → B
```

---

# 41. Important Interview Scenario

### Question

Can a cycle in a Resource Allocation Graph always mean deadlock?

### Answer

> No. If every resource type has a single instance, a cycle indicates deadlock. With multiple instances of resource types, a cycle may indicate the possibility of deadlock but does not by itself prove deadlock.

---

# 42. Important Interview Scenario

### Question

Is every unsafe state a deadlock?

### Answer

> No. An unsafe state means the system cannot guarantee a safe completion sequence, but the system may not be deadlocked yet.

---

# 43. Important Interview Questions

Prepare these especially well:

```text
1. What is deadlock?

2. Give a real-life example of deadlock.

3. How does deadlock occur?

4. What are the four necessary conditions for deadlock?

5. What is mutual exclusion?

6. What is hold and wait?

7. What is no preemption?

8. What is circular wait?

9. What is a Resource Allocation Graph?

10. Can a cycle in a Resource Allocation Graph always indicate deadlock?

11. What is deadlock prevention?

12. How can deadlock be prevented?

13. What is deadlock avoidance?

14. Prevention vs avoidance?

15. What is a safe state?

16. What is an unsafe state?

17. Safe state vs unsafe state?

18. Is every unsafe state a deadlock?

19. What is Banker's Algorithm?

20. Why is Banker's Algorithm used?

21. What are Available, Maximum, Allocation, and Need?

22. What is the formula for Need?

23. What is a safe sequence?

24. What is deadlock detection?

25. What is deadlock recovery?

26. Prevention vs avoidance vs detection?

27. How can processes be terminated to recover from deadlock?

28. What is resource preemption?

29. Deadlock vs starvation?

30. Deadlock vs livelock?

31. How can deadlock occur with mutexes/locks?

32. How can lock-based deadlock be prevented?

33. Solve a Banker's Algorithm problem.

34. Identify deadlock from a resource-allocation scenario.
```

---

# 44. Quick Revision

```text
DEADLOCK
→ Processes/threads permanently wait
→ No progress for involved processes

FOUR CONDITIONS
→ Mutual Exclusion
→ Hold and Wait
→ No Preemption
→ Circular Wait

RESOURCE ALLOCATION GRAPH
→ Represents processes/resources
→ Single-instance cycle → deadlock

PREVENTION
→ Break at least one necessary condition

AVOIDANCE
→ Keep system in a safe state

BANKER'S ALGORITHM
→ Deadlock avoidance

SAFE STATE
→ Has a safe sequence

UNSAFE STATE
→ No guaranteed safe sequence
→ Not necessarily deadlocked

DETECTION
→ Detect deadlock after allowing allocations

RECOVERY
→ Terminate processes
→ Preempt resources
→ Rollback/restart where applicable

DEADLOCK
→ Stuck waiting

STARVATION
→ One process waits excessively
→ Others continue

LIVELOCK
→ Processes remain active
→ No useful progress

NEED
→ Maximum - Allocation
```

---

# 45. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Deadlock definition
Four necessary conditions
Mutual Exclusion
Hold and Wait
No Preemption
Circular Wait
Resource Allocation Graph
Deadlock Prevention
Deadlock Avoidance
Safe vs Unsafe State
Banker's Algorithm
Prevention vs Avoidance vs Detection
Deadlock vs Starvation
Deadlock vs Livelock
Deadlock with locks
Deadlock prevention using lock ordering
```

## ⭐⭐⭐ Good to Know

```text
Deadlock detection
Deadlock recovery
Resource preemption
Banker's Algorithm numerical problems
```

> **For placement interviews, the highest-priority topics are the four deadlock conditions, prevention vs avoidance, safe/unsafe states, Banker's Algorithm, and deadlock scenarios involving locks.**