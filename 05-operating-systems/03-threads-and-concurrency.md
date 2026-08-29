# Threads and Concurrency

## 1. What is a Thread?

A **thread** is the smallest unit of execution within a process that can be scheduled by the operating system.

A process can contain one or more threads.

```text
Process
├── Thread 1
├── Thread 2
└── Thread 3
```

Threads belonging to the same process generally share:

```text
Code
Data
Heap
Open resources
```

Each thread generally has its own:

```text
Stack
Program Counter
CPU Registers
Execution state
```

---

# 2. Why are Threads Used?

Threads allow a process to perform multiple tasks concurrently.

Example:

```text
Browser Process
├── UI Thread
├── Network Thread
├── Rendering Thread
└── Background Thread
```

### Main advantages

- Better responsiveness
- Resource sharing
- Lower overhead than creating separate processes
- Can take advantage of multiple CPU cores
- Useful for concurrent tasks

---

# 3. Process vs Thread

| Process | Thread |
|---|---|
| Independent execution environment | Execution unit within a process |
| Has its own address space | Threads of the same process share address space |
| More expensive to create/manage | Generally cheaper to create/manage |
| Communication can require IPC | Shared memory makes communication easier |
| Better isolation | Less isolation |
| Context switching can be relatively expensive | Thread switching can be relatively cheaper |

### Interview Answer

> A process is an independent execution environment, while a thread is an execution unit within a process. Threads of the same process share resources such as code, data, and heap.

---

# 4. Single-Threaded vs Multithreaded Process

## Single-Threaded Process

A process contains one thread.

```text
Process
└── Thread
```

## Multithreaded Process

A process contains multiple threads.

```text
Process
├── Thread 1
├── Thread 2
└── Thread 3
```

---

# 5. What is Multithreading?

**Multithreading** is the execution or management of multiple threads within a single process.

Example:

```text
Application
│
├── Thread 1 → Task A
├── Thread 2 → Task B
└── Thread 3 → Task C
```

The threads share the process's resources while maintaining separate execution states.

---

# 6. Advantages of Multithreading

### 1. Responsiveness

One thread can continue handling user interaction while another performs a longer task.

```text
UI Thread
   ↓
remains responsive

Worker Thread
   ↓
performs background task
```

---

### 2. Resource Sharing

Threads within the same process can share:

```text
Code
Data
Heap
```

This makes communication easier than between separate processes in many cases.

---

### 3. Economy

Creating and managing threads is generally less expensive than creating separate processes.

---

### 4. Parallelism

On a multicore CPU, multiple threads can execute simultaneously.

```text
Core 1 → Thread 1
Core 2 → Thread 2
Core 3 → Thread 3
```

---

# 7. User-Level Threads

User-level threads are managed primarily by a user-space threading library/runtime rather than directly by the kernel for every thread operation.

```text
Application
    ↓
User-level Thread Library
    ↓
OS
```

### Advantages

```text
Fast thread operations
Less kernel involvement
Flexible management
```

### Disadvantages

Depending on the implementation, a blocking system call by one user-level thread may block the entire process, and the kernel may not schedule the user-level threads independently.

---

# 8. Kernel-Level Threads

Kernel-level threads are managed and scheduled by the operating system kernel.

```text
Application
    ↓
Kernel
    ↓
Threads
```

### Advantages

- Kernel can schedule threads individually
- Blocking of one thread need not block all threads in the process, depending on the operation and OS
- Can support parallel execution across multiple cores

### Disadvantages

- More overhead than purely user-space thread management
- Requires kernel involvement

---

# 9. User-Level vs Kernel-Level Threads

| User-Level Threads | Kernel-Level Threads |
|---|---|
| Managed mainly in user space | Managed by kernel |
| Fast management | More management overhead |
| Kernel may not know each user thread | Kernel knows/schedules kernel threads |
| Blocking behavior depends on runtime/OS design | Kernel can schedule individual threads |
| Parallelism depends on implementation | Supports true parallel execution of threads across cores |

---

# 10. What is Concurrency?

**Concurrency** means multiple tasks can make progress during overlapping periods of time.

It does **not necessarily mean** that tasks execute at exactly the same instant.

Example on a single CPU core:

```text
Time →

Task A: ███     ███
Task B:    ███     ███
```

The CPU switches between tasks, allowing both to make progress.

---

# 11. What is Parallelism?

**Parallelism** means multiple tasks are actually executing at the same time using multiple execution resources.

Example:

```text
Core 1 → Task A
Core 2 → Task B
```

---

# 12. Concurrency vs Parallelism

| Concurrency | Parallelism |
|---|---|
| Multiple tasks make overlapping progress | Multiple tasks execute simultaneously |
| Can occur on a single core | Usually requires multiple execution resources |
| Focuses on managing multiple tasks | Focuses on simultaneous execution |
| Does not require multiple cores | Commonly uses multiple cores |

### Interview Answer

> Concurrency means multiple tasks can make progress during overlapping periods, while parallelism means multiple tasks are actually executed at the same time.

---

# 13. Is Concurrency Possible on a Single-Core CPU?

**Yes.**

A single CPU core can switch between tasks rapidly.

```text
Task A
  ↓
Task B
  ↓
Task A
  ↓
Task C
```

This creates concurrent progress even though only one task executes at a particular instant on that core.

---

# 14. Is Parallelism Possible on a Single-Core CPU?

True simultaneous execution of independent tasks is **not possible on a single CPU core**.

Parallel execution requires multiple execution resources, such as multiple CPU cores.

---

# 15. What is Multicore Processing?

A multicore processor contains multiple CPU cores.

Example:

```text
CPU
├── Core 1
├── Core 2
├── Core 3
└── Core 4
```

Different runnable threads can execute simultaneously on different cores.

---

# 16. Concurrency and Multithreading

Multithreading is commonly used to implement concurrent applications.

Example:

```text
Application
├── Thread 1 → Download
├── Thread 2 → Process data
└── Thread 3 → Update UI
```

These threads may:

```text
Run concurrently on one core
```

or:

```text
Run in parallel on multiple cores
```

---

# 17. What is a Race Condition?

A **race condition** occurs when the result of a program depends on the timing or ordering of concurrent operations accessing shared state.

Example:

```text
Shared variable:
count = 10

Thread 1 → reads count
Thread 2 → reads count

Both modify count

Final result may be incorrect
```

The problem occurs because operations that should be coordinated are interleaved unexpectedly.

---

# 18. Simple Race Condition Example

Suppose:

```text
count = 0
```

Two threads execute:

```text
count = count + 1
```

This operation may conceptually involve:

```text
Read
Add
Write
```

Possible interleaving:

```text
Thread 1 → Read 0
Thread 2 → Read 0
Thread 1 → Write 1
Thread 2 → Write 1
```

Expected:

```text
2
```

Actual:

```text
1
```

This is a race condition.

---

# 19. What is Shared Data?

**Shared data** is data that can be accessed by multiple threads or processes.

Examples:

```text
Shared variable
Shared memory
File
Database record
Global data structure
```

Shared data requires appropriate synchronization when concurrent access can cause incorrect results.

---

# 20. What is Synchronization?

**Synchronization** is the coordination of concurrent processes/threads to ensure correct access to shared resources and prevent inconsistent results.

Example:

```text
Thread 1 ──┐
           ├──→ Shared Resource
Thread 2 ──┘
             ↑
        Synchronization
```

Important synchronization mechanisms include:

```text
Mutex
Semaphore
Monitor
Locks
```

Detailed synchronization concepts are covered in:

```text
04-process-synchronization.md
```

---

# 21. What is a Critical Section?

A **critical section** is a part of a program where shared data or resources are accessed and therefore may require synchronization.

Example:

```text
Thread
  ↓
Enter Critical Section
  ↓
Access Shared Data
  ↓
Leave Critical Section
```

Only an appropriate number of threads should be allowed into a critical section according to the resource's requirements.

---

# 22. What is a Mutex?

A **mutex (mutual exclusion lock)** is a synchronization mechanism used to ensure that only one thread at a time owns a protected critical section/resource.

Example:

```text
Thread 1
   ↓
Lock
   ↓
Critical Section
   ↓
Unlock

Thread 2
   ↓
Wait
```

---

# 23. What is a Semaphore?

A **semaphore** is a synchronization mechanism based on a counter that can control access to shared resources.

Two common forms are:

```text
Binary Semaphore
Counting Semaphore
```

A counting semaphore can allow a limited number of threads to access a resource concurrently.

---

# 24. Mutex vs Semaphore

| Mutex | Semaphore |
|---|---|
| Primarily provides mutual exclusion | Coordinates access using a counter |
| Usually has ownership semantics | Generally does not have mutex-style ownership |
| Commonly protects one critical section/resource | Can manage multiple instances of a resource |
| Typically locked/unlocked by the owning thread | Wait/signal operations control the semaphore count |

### Easy Interview Answer

> A mutex is primarily used for mutual exclusion and ownership-based locking, while a semaphore is a signaling/counting mechanism that can control access to one or more resource instances.

---

# 25. What is Thread Synchronization?

Thread synchronization ensures that multiple threads access shared resources safely and in the required order.

Without synchronization:

```text
Thread 1 ──┐
           ├──→ Shared Data
Thread 2 ──┘
       ↓
Race Condition
```

With synchronization:

```text
Thread 1
   ↓
Lock
   ↓
Shared Data
   ↓
Unlock
   ↓
Thread 2
```

---

# 26. What is Thread Safety?

A piece of code is **thread-safe** when it behaves correctly when accessed concurrently by multiple threads according to its intended contract.

Thread safety may involve:

```text
Locks
Atomic operations
Immutable data
Thread-local data
Proper synchronization
```

---

# 27. What is Deadlock in Multithreading?

A **deadlock** occurs when two or more threads/processes are permanently blocked because each is waiting for a resource held by another.

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

# 28. Race Condition vs Deadlock

| Race Condition | Deadlock |
|---|---|
| Result depends on timing/order | Threads/processes become stuck waiting |
| Can produce incorrect results | Prevents progress for involved participants |
| Caused by unsafe concurrent access | Caused by circular/resource waiting conditions |
| Synchronization can prevent it | Deadlock prevention/avoidance/detection can address it |

---

# 29. What is Thread Starvation?

Thread starvation occurs when a thread waits for a resource or CPU opportunity for an excessively long time because other threads continually receive access.

Example:

```text
Thread A
   ↓
Waiting

Thread B/C/D
   ↓
Keep getting resource

Thread A
   ↓
Still waiting
```

---

# 30. Starvation vs Deadlock

### Starvation

```text
One thread waits
Other threads continue
```

### Deadlock

```text
Threads wait on each other
No progress for the involved set
```

---

# 31. What is Context Switching Between Threads?

When the CPU switches from one thread to another, the OS/runtime may save the current thread's execution state and restore another thread's state.

```text
Thread A
   ↓
Save state
   ↓
Load Thread B state
   ↓
Thread B
```

Threads in the same process generally share an address space, so thread switching can have different costs from switching between separate processes, depending on the OS and architecture.

---

# 32. What Happens When Multiple Threads Access the Same Variable?

It depends on the operation and synchronization.

### Safe case

If access is properly synchronized:

```text
Thread 1
   ↓
Lock
   ↓
Update
   ↓
Unlock
```

### Unsafe case

Without appropriate synchronization:

```text
Thread 1 ──┐
           ├──→ Shared Variable
Thread 2 ──┘
             ↓
       Race Condition
```

---

# 33. Why Can Multithreading Improve Performance?

Multithreading can improve performance when:

```text
Tasks can overlap
Tasks spend time waiting for I/O
Multiple CPU cores are available
Work can be divided effectively
```

But multithreading does **not automatically** make every program faster.

Overhead can come from:

```text
Thread creation
Context switching
Synchronization
Lock contention
Communication
```

---

# 34. Concurrency vs Parallelism: Interview Scenario

### Question

A program uses four threads on a single-core CPU. Are the threads executing in parallel?

### Answer

> No. The CPU core can execute only one thread at a time, although the threads can make concurrent progress through context switching.

### Question

What if the same four threads run on four CPU cores?

### Answer

> They may execute in parallel if the operating system schedules them on separate available cores and the workload allows it.

---

# 35. Important Interview Questions

Prepare these particularly well:

```text
1. What is a thread?

2. Why are threads used?

3. Process vs thread?

4. What is multithreading?

5. What are the advantages of multithreading?

6. What is a single-threaded process?

7. What is a multithreaded process?

8. User-level vs kernel-level threads?

9. What are the advantages/disadvantages of user-level threads?

10. What are the advantages/disadvantages of kernel-level threads?

11. What is concurrency?

12. What is parallelism?

13. Concurrency vs parallelism?

14. Can concurrency happen on a single-core CPU?

15. Can parallelism happen on a single-core CPU?

16. What is a race condition?

17. Give an example of a race condition.

18. What is shared data?

19. What is synchronization?

20. What is a critical section?

21. What is a mutex?

22. What is a semaphore?

23. Mutex vs semaphore?

24. What is thread safety?

25. What is thread starvation?

26. Starvation vs deadlock?

27. What is thread context switching?

28. Does multithreading always improve performance?

29. How can multithreading improve performance?

30. What happens when multiple threads access shared data?
```

---

# 36. Quick Revision

```text
THREAD
→ Unit of execution within a process

PROCESS
→ Independent execution environment

MULTITHREADING
→ Multiple threads within a process

USER-LEVEL THREAD
→ Managed mainly in user space

KERNEL-LEVEL THREAD
→ Managed/scheduled by kernel

CONCURRENCY
→ Multiple tasks make overlapping progress

PARALLELISM
→ Multiple tasks execute simultaneously

SINGLE CORE
→ Can provide concurrency
→ Cannot provide true simultaneous parallel execution

MULTICORE
→ Can execute multiple threads in parallel

RACE CONDITION
→ Result depends on concurrent timing/order

SYNCHRONIZATION
→ Coordinates concurrent access

CRITICAL SECTION
→ Code accessing shared resource/data

MUTEX
→ Mutual exclusion
→ One owner at a time

SEMAPHORE
→ Counter-based synchronization/signaling

THREAD SAFETY
→ Correct behavior under concurrent access

STARVATION
→ Thread waits excessively while others continue

DEADLOCK
→ Threads/processes wait in a cycle and cannot progress

CONTEXT SWITCH
→ Save one execution state
→ Load another
```

---

# 37. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Thread
Process vs Thread
Multithreading
User-level vs Kernel-level threads
Concurrency
Parallelism
Concurrency vs Parallelism
Race Condition
Critical Section
Synchronization
Mutex
Semaphore
Mutex vs Semaphore
Thread Safety
Starvation
Deadlock vs Starvation
```

## ⭐⭐⭐ Good to Know

```text
Thread context switching
Multicore processing
Thread performance overhead
Detailed thread implementation
```

> **For placement interviews, focus deeply on Process vs Thread, User vs Kernel Threads, Concurrency vs Parallelism, Race Conditions, Critical Sections, Mutexes, and Semaphores.** These concepts also connect directly to the next file on **Process Synchronization**.