# OS Important Interview Questions

> **Purpose:** This file is for quick revision before placements. If you prepare the questions below properly, you can cover the **main and frequently asked Operating System interview topics** without revising every detail again.

---

# 1. OS Basics

### 1. What is an Operating System?

> An Operating System is system software that acts as an interface between the user/applications and computer hardware and manages system resources.

### 2. What are the main functions of an OS?

```text
Process Management
Memory Management
File Management
I/O Management
Resource Management
Security and Protection
```

### 3. What are the main types of Operating Systems?

```text
Batch OS
Time-Sharing OS
Multiprogramming OS
Multiprocessing OS
Distributed OS
Real-Time OS
```

### 4. What is a kernel?

> The kernel is the core part of an operating system that manages hardware resources and provides essential services to programs.

### 5. What is the difference between kernel and OS?

> The OS is the complete system software, while the kernel is its core component responsible for low-level resource management.

### 6. What is user mode and kernel mode?

> User mode restricts applications from directly accessing critical hardware/resources, while kernel mode provides the OS with privileged access.

```text
User Mode
   ↓
System Call
   ↓
Kernel Mode
   ↓
Hardware
```

### 7. What is a system call?

> A system call is the mechanism through which a user-level program requests a service from the operating system kernel.

Examples:

```text
open()
read()
write()
fork()
exec()
wait()
```

### 8. What is a context switch?

> A context switch occurs when the CPU switches from executing one process/thread to another by saving the current execution state and restoring another.

---

# 2. Processes

### 9. What is a process?

> A process is a program in execution.

### 10. Program vs Process?

| Program | Process |
|---|---|
| Passive set of instructions | Program currently executing |
| Stored on storage | Requires memory/resources |
| No execution state | Has execution state |

### 11. What is a Process Control Block (PCB)?

A **PCB** is a data structure maintained by the OS for each process.

It can contain:

```text
Process ID
Process State
Program Counter
CPU Registers
Scheduling Information
Memory Management Information
I/O Information
```

### 12. What are the common process states?

```text
New
Ready
Running
Waiting/Blocked
Terminated
```

Typical flow:

```text
New
 ↓
Ready
 ↓
Running
 ↓
Waiting
 ↓
Ready
 ↓
Running
 ↓
Terminated
```

### 13. Process vs Thread?

| Process | Thread |
|---|---|
| Independent execution unit with its own process resources/address space | Execution unit within a process |
| More expensive to create/switch | Usually cheaper to create/switch |
| Processes generally have separate address spaces | Threads of the same process share its address space |
| Communication generally requires IPC | Communication through shared process memory is easier |

### 14. What is IPC?

**IPC (Inter-Process Communication)** allows processes to communicate and coordinate.

Common IPC mechanisms:

```text
Pipes
Message Queues
Shared Memory
Sockets
Signals
```

### 15. Shared Memory vs Message Passing?

| Shared Memory | Message Passing |
|---|---|
| Processes communicate through shared memory | Processes exchange messages |
| Very fast after setup | Can involve more communication overhead |
| Requires synchronization | Synchronization is often integrated into communication mechanism |
| Suitable for large amounts of shared data | Useful for structured communication |

### 16. What is `fork()`?

On Unix-like systems, `fork()` creates a new process by duplicating the calling process's execution context according to OS semantics.

```text
Parent Process
      ↓
    fork()
    /   \
Parent  Child
```

### 17. What is `exec()`?

The `exec` family replaces the current process image with a new program.

A common pattern is:

```text
fork()
  ↓
child
  ↓
exec()
  ↓
new program
```

### 18. What is a zombie process?

A **zombie process** is a child process that has terminated but whose parent has not yet collected its termination status.

### 19. What is an orphan process?

An **orphan process** is a child process whose original parent has terminated before the child.

---

# 3. CPU Scheduling

### 20. What is CPU scheduling?

> CPU scheduling is the process of selecting a ready process/thread to execute on the CPU.

### 21. What are common CPU scheduling algorithms?

```text
FCFS
SJF
SRTF
Round Robin
Priority Scheduling
Multilevel Queue
Multilevel Feedback Queue
```

### 22. What is FCFS?

**First-Come, First-Served** executes processes in the order they arrive.

```text
P1 → P2 → P3 → P4
```

### 23. What is SJF?

**Shortest Job First** selects the process with the smallest CPU burst.

### 24. What is SRTF?

**Shortest Remaining Time First** is the preemptive version of SJF.

The process with the shortest remaining CPU burst gets the CPU.

### 25. What is Round Robin?

Round Robin assigns each process a fixed **time quantum** in circular order.

```text
P1 → P2 → P3
↑           ↓
└───────────┘
```

### 26. What is time quantum?

> Time quantum is the maximum amount of CPU time allocated to a process during one turn in Round Robin scheduling.

### 27. What happens if the time quantum is too small?

```text
Very frequent context switches
↓
Higher overhead
```

### 28. What happens if the time quantum is too large?

Round Robin can approach the behavior of FCFS.

### 29. What is preemptive scheduling?

> In preemptive scheduling, the OS can interrupt a running process and allocate the CPU to another process.

### 30. What is non-preemptive scheduling?

> In non-preemptive scheduling, a running process generally keeps the CPU until it terminates, blocks, or otherwise voluntarily yields it.

### 31. What is starvation in CPU scheduling?

> Starvation occurs when a process waits for an excessively long time because other processes keep getting selected.

### 32. What is aging?

> Aging gradually increases the priority of waiting processes to reduce starvation.

### 33. What is turnaround time?

```text
Turnaround Time =
Completion Time - Arrival Time
```

### 34. What is waiting time?

> Waiting time is the total time a process spends waiting in the ready queue.

For the standard scheduling model:

```text
Waiting Time =
Turnaround Time - Burst Time
```

### 35. What is response time?

```text
Response Time =
First CPU Start Time - Arrival Time
```

### 36. Which scheduling algorithm can cause starvation?

Common examples:

```text
SJF
SRTF
Priority Scheduling
```

depending on workload and implementation.

---

# 4. Threads and Concurrency

### 37. What is a thread?

> A thread is an execution unit within a process.

### 38. Why are threads used?

```text
Responsiveness
Concurrency
Resource sharing
Lower overhead than separate processes in many cases
```

### 39. User-level vs Kernel-level threads?

| User-Level Threads | Kernel-Level Threads |
|---|---|
| Managed by user-space library/runtime | Managed/scheduled by OS kernel |
| Kernel may not directly know each user thread | Kernel is aware of kernel threads |
| Fast management can be possible | More OS involvement |
| Blocking behavior depends on threading model | OS can schedule threads individually |

### 40. What is concurrency?

> Concurrency means multiple tasks make progress during overlapping periods of time.

### 41. What is parallelism?

> Parallelism means multiple tasks actually execute simultaneously, typically on multiple CPU cores.

### 42. Concurrency vs Parallelism?

```text
Concurrency
→ Dealing with multiple tasks during overlapping time

Parallelism
→ Executing multiple tasks at the same time
```

---

# 5. Process Synchronization

### 43. What is process synchronization?

> Process synchronization coordinates concurrent processes/threads so that shared resources are accessed safely and operations occur correctly.

### 44. What is a race condition?

> A race condition occurs when the result depends on the timing/order of concurrent operations accessing shared data.

Example:

```text
Thread 1 ──┐
           ├──→ Shared Variable
Thread 2 ──┘
```

### 45. What is a critical section?

> A critical section is the part of a program where shared data or resources are accessed and therefore requires appropriate synchronization.

### 46. What are the requirements of a critical-section solution?

```text
Mutual Exclusion
Progress
Bounded Waiting
```

### 47. What is mutual exclusion?

> Mutual exclusion ensures that only one process/thread at a time enters a particular protected critical section.

### 48. What is a mutex?

> A mutex is a synchronization mechanism used to provide mutual exclusion, typically allowing one thread to hold a lock at a time.

### 49. What is a semaphore?

> A semaphore is a counter-based synchronization mechanism used for signaling or controlling access to resources.

### 50. Binary vs Counting Semaphore?

| Binary Semaphore | Counting Semaphore |
|---|---|
| Represents two logical states/count levels | Can represent multiple available resources |
| Often used for simple synchronization | Useful for resource pools |
| Conceptually 0/1 | Can have values greater than 1 |

### 51. Mutex vs Semaphore?

> A mutex is primarily an ownership-based mutual-exclusion mechanism, while a semaphore is a counter-based synchronization mechanism used for signaling or controlling resource availability.

### 52. What is busy waiting?

> Busy waiting occurs when a thread repeatedly checks a condition instead of blocking and therefore continues consuming CPU time.

### 53. What is starvation?

> Starvation occurs when a process/thread waits for an excessively long or indefinite period while others continue to make progress.

### 54. What are classic synchronization problems?

```text
Producer-Consumer
Readers-Writers
Dining Philosophers
```

---

# 6. Deadlocks

### 55. What is deadlock?

> Deadlock is a situation where a set of processes/threads are permanently blocked because each is waiting for resources or events that cannot become available due to the other processes in the set.

### 56. What are the four necessary conditions for deadlock?

```text
1. Mutual Exclusion
2. Hold and Wait
3. No Preemption
4. Circular Wait
```

### 57. What is Hold and Wait?

> A process holds at least one resource while waiting for another resource.

### 58. What is No Preemption?

> A resource cannot simply be forcibly taken from a process holding it; it must be released according to the resource's rules.

### 59. What is Circular Wait?

> A circular chain exists where each process waits for a resource held by another process in the chain.

```text
P1 → P2 → P3 → P1
```

### 60. How can deadlock be prevented?

Prevent at least one of the four necessary conditions.

Examples:

```text
Prevent Hold and Wait
Prevent Circular Wait
Allow preemption where possible
Make resources shareable where appropriate
```

### 61. What is deadlock avoidance?

> Deadlock avoidance dynamically evaluates resource-allocation decisions and grants requests only when the resulting state remains safe.

### 62. What is Banker's Algorithm?

> Banker's Algorithm is a deadlock-avoidance algorithm that checks whether resource allocation leaves the system in a safe state.

### 63. What is a safe state?

> A safe state is a state in which there exists a sequence allowing all processes to obtain the resources they need and complete.

### 64. What is an unsafe state?

> An unsafe state is a state from which the system cannot guarantee a safe completion sequence.

Important:

```text
Unsafe ≠ necessarily deadlocked
```

### 65. Deadlock prevention vs avoidance?

| Prevention | Avoidance |
|---|---|
| Breaks at least one necessary condition | Dynamically checks resource allocation |
| Uses restrictions/rules | Uses current resource information |
| Prevents deadlock structurally | Keeps system in a safe state |

### 66. Deadlock vs Starvation?

> In deadlock, the involved processes cannot proceed because of blocking dependencies. In starvation, one process waits excessively while other processes may continue.

### 67. Deadlock vs Livelock?

> In deadlock, processes are stuck waiting. In livelock, processes remain active but repeatedly respond to each other without making useful progress.

---

# 7. Memory Management

### 68. What is memory management?

> Memory management is the OS function responsible for allocating, tracking, protecting, and managing memory used by processes.

### 69. Logical/Virtual address vs Physical address?

> A logical/virtual address is an address used by a process, while a physical address identifies an actual location in physical memory.

```text
CPU
 ↓
Virtual Address
 ↓
MMU
 ↓
Physical Address
 ↓
RAM
```

### 70. What is the MMU?

> MMU (Memory Management Unit) is hardware that translates virtual addresses into physical addresses.

### 71. What is paging?

> Paging divides virtual memory into fixed-size pages and physical memory into equally sized frames.

### 72. What is a page?

> A page is a fixed-size block of virtual memory.

### 73. What is a frame?

> A frame is a fixed-size block of physical memory.

### 74. What is a page table?

> A page table stores mappings between virtual pages and physical frames.

### 75. What is fragmentation?

Two major types:

```text
Internal Fragmentation
External Fragmentation
```

### 76. Internal vs External Fragmentation?

> Internal fragmentation is unused space inside an allocated block, while external fragmentation is free space scattered between allocated blocks.

### 77. What is virtual memory?

> Virtual memory allows processes to use a virtual address space larger than the physical RAM currently available by keeping only needed portions in RAM and other portions in secondary storage.

### 78. What is demand paging?

> Demand paging loads a page into physical memory only when it is needed.

### 79. What is a page fault?

> A page fault occurs when a process accesses a virtual page that is not currently present in physical memory.

### 80. Is a page fault an error?

> Not necessarily. In a virtual-memory system using demand paging, page faults are normal events that cause the OS to bring required pages into memory.

### 81. What is page replacement?

> Page replacement selects a page to remove from physical memory when a required page needs to be loaded and no free frame is available.

### 82. What is LRU?

> LRU (Least Recently Used) replaces the page that has not been used for the longest time.

### 83. What is FIFO page replacement?

> FIFO replaces the page that has been in memory the longest.

### 84. What is Optimal page replacement?

> Optimal replacement removes the page whose next use is farthest in the future.

It is mainly a theoretical benchmark because the future reference sequence is not normally known.

### 85. What is Belady's anomaly?

> Belady's anomaly is a situation where increasing the number of page frames can increase the number of page faults, notably with FIFO.

### 86. What is thrashing?

> Thrashing occurs when the system spends excessive time handling page faults and moving pages between memory and storage instead of doing useful work.

### 87. What is a TLB?

> TLB (Translation Lookaside Buffer) is a small, fast cache that stores recent virtual-page-to-physical-frame translations.

### 88. TLB miss vs Page fault?

> A TLB miss means the translation is not found in the TLB; the page may still be in RAM. A page fault means the required page is not currently in physical memory.

---

# 8. File Systems

### 89. What is a file system?

> A file system is the structure and set of methods used by an OS to organize, store, locate, and manage files on storage.

### 90. What are common file operations?

```text
Create
Open
Read
Write
Seek
Close
Delete
Rename
```

### 91. What is a directory?

> A directory organizes and helps locate files and other directories.

### 92. What is file allocation?

The main allocation methods are:

```text
Contiguous Allocation
Linked Allocation
Indexed Allocation
```

### 93. Contiguous vs Linked vs Indexed Allocation?

| Contiguous | Linked | Indexed |
|---|---|---|
| Blocks stored together | Blocks can be scattered and linked | Index block points to file blocks |
| Fast access | Good sequential access | Good direct access |
| File growth can be difficult | Easy growth | Supports non-contiguous blocks |
| External fragmentation possible | No requirement for contiguous blocks | No requirement for contiguous blocks |

### 94. What is an inode?

> An inode is a Unix-like file-system data structure containing file metadata and information used to locate its data.

### 95. What is a file descriptor?

> A file descriptor is a process-level identifier used by Unix-like systems to refer to an open file or other I/O resource.

### 96. Inode vs File Descriptor?

> An inode is a file-system structure containing metadata and data-location information, while a file descriptor is a process-level handle for accessing an open resource.

### 97. Hard link vs Symbolic link?

> A hard link is another directory entry referring to the same inode, while a symbolic link refers to another path.

---

# 9. Disk Management

### 98. What is disk scheduling?

> Disk scheduling determines the order in which pending disk I/O requests are serviced.

### 99. What is FCFS disk scheduling?

> Services disk requests in arrival order.

### 100. What is SSTF?

> SSTF (Shortest Seek Time First) selects the request closest to the current disk-head position.

### 101. What is SCAN?

> SCAN moves the disk head in one direction while servicing requests, then reverses direction.

It is also called the:

```text
Elevator Algorithm
```

### 102. What is C-SCAN?

> C-SCAN services requests in one direction and, after reaching the end, returns to the beginning and continues in the same direction.

### 103. SCAN vs C-SCAN?

```text
SCAN
→ Services in both directions

C-SCAN
→ Services in one direction
→ Returns to beginning
→ Continues in same direction
```

### 104. What is seek time?

> Seek time is the time required for an HDD's read/write head to move to the required track.

### 105. What is rotational latency?

> Rotational latency is the time spent waiting for the required sector to rotate under the disk head.

---

# 10. Most Important Scenario-Based Questions

## 106. Two threads update the same variable simultaneously. What can happen?

> A race condition can occur if the update is not atomic or properly synchronized.

### How do you solve it?

```text
Mutex
Semaphore
Atomic operation
Other appropriate synchronization mechanism
```

---

## 107. Two threads acquire locks in opposite order. What can happen?

Example:

```text
T1:
Lock A
Wait for B

T2:
Lock B
Wait for A
```

> This can cause deadlock.

### Solution

Use a consistent global lock order:

```text
A → B
```

---

## 108. A process has a high priority but never gets CPU time. What problem could this indicate?

> It may indicate starvation caused by scheduling behavior or unfair resource allocation.

---

## 109. A system is spending most of its time handling page faults. What is happening?

> The system may be experiencing thrashing.

---

## 110. A required page is not present in RAM. What happens?

```text
Page Fault
   ↓
OS handles fault
   ↓
Find required page
   ↓
Load page into RAM
   ↓
Update page table
   ↓
Resume execution
```

---

## 111. Why can increasing the number of frames sometimes increase page faults?

> This can happen due to Belady's anomaly with certain page-replacement algorithms such as FIFO.

---

## 112. Why is SSTF better than FCFS in many cases?

> SSTF often reduces total head movement by selecting the closest pending request, improving average seek time. However, it can cause starvation for far-away requests.

---

## 113. Why is Round Robin suitable for time-sharing systems?

> Round Robin gives each ready process a time slice, allowing multiple processes to receive CPU time fairly and improving responsiveness.

---

## 114. What happens if Round Robin's time quantum is very small?

```text
More context switches
↓
Higher overhead
```

---

## 115. What happens if Round Robin's time quantum is very large?

> It approaches FCFS behavior.

---

# 11. Most Important Comparisons

### Process vs Thread

```text
Process
→ Independent execution unit
→ Separate address space

Thread
→ Execution unit within process
→ Threads share process address space
```

### Program vs Process

```text
Program
→ Passive code

Process
→ Program in execution
```

### Mutex vs Semaphore

```text
Mutex
→ Mutual exclusion
→ Ownership-based

Semaphore
→ Counter-based
→ Signaling/resource counting
```

### Paging vs Segmentation

```text
Paging
→ Fixed-size pages

Segmentation
→ Variable-size logical segments
```

### Internal vs External Fragmentation

```text
Internal
→ Waste inside allocated block

External
→ Free space scattered outside allocated blocks
```

### Deadlock vs Starvation

```text
Deadlock
→ Involved processes are stuck

Starvation
→ One process waits excessively while others progress
```

### Concurrency vs Parallelism

```text
Concurrency
→ Tasks make progress during overlapping periods

Parallelism
→ Tasks execute simultaneously
```

### TLB Miss vs Page Fault

```text
TLB Miss
→ Translation not in TLB

Page Fault
→ Page not in RAM
```

### Prevention vs Avoidance

```text
Prevention
→ Break a necessary condition

Avoidance
→ Maintain a safe state
```

---

# 12. Numerical Problems You Should Prepare

For OS placements, also practice basic numerical problems from:

```text
1. FCFS CPU Scheduling

2. SJF CPU Scheduling

3. SRTF CPU Scheduling

4. Round Robin Scheduling

5. Priority Scheduling

6. Waiting Time

7. Turnaround Time

8. Response Time

9. Page Replacement
   → FIFO
   → LRU
   → Optimal

10. Page Number / Offset Calculation

11. Banker's Algorithm

12. Disk Scheduling
   → FCFS
   → SSTF
   → SCAN
   → C-SCAN
```

---

# 13. Final OS Revision Checklist

Before an interview, make sure you can explain these without looking at notes:

```text
✓ What is an Operating System?

✓ Kernel and System Calls

✓ User Mode vs Kernel Mode

✓ Process and PCB

✓ Process States

✓ Process vs Thread

✓ IPC

✓ fork() and exec()

✓ Zombie vs Orphan

✓ CPU Scheduling

✓ FCFS

✓ SJF

✓ SRTF

✓ Round Robin

✓ Priority Scheduling

✓ Preemptive vs Non-Preemptive

✓ Waiting / Turnaround / Response Time

✓ Starvation and Aging

✓ Concurrency vs Parallelism

✓ Race Condition

✓ Critical Section

✓ Mutual Exclusion

✓ Mutex

✓ Semaphore

✓ Producer-Consumer

✓ Readers-Writers

✓ Deadlock

✓ Four Deadlock Conditions

✓ Deadlock Prevention

✓ Deadlock Avoidance

✓ Banker's Algorithm

✓ Safe vs Unsafe State

✓ Deadlock vs Starvation

✓ Deadlock vs Livelock

✓ Memory Management

✓ Logical vs Physical Address

✓ MMU

✓ Paging

✓ Page vs Frame

✓ Page Table

✓ Fragmentation

✓ Virtual Memory

✓ Demand Paging

✓ Page Fault

✓ Page Replacement

✓ FIFO / LRU / Optimal

✓ Belady's Anomaly

✓ Thrashing

✓ TLB

✓ File System

✓ File Allocation

✓ Inode

✓ File Descriptor

✓ Hard Link vs Symbolic Link

✓ Disk Scheduling

✓ FCFS / SSTF / SCAN / C-SCAN

✓ Seek Time

✓ Rotational Latency

✓ Basic OS Numerical Problems
```

---

# 14. Last-Minute Priority

If you have **very little time before the interview**, prioritize in this order:

## ⭐⭐⭐⭐⭐ Highest Priority

```text
1. Process vs Thread

2. Process States and PCB

3. Context Switching

4. CPU Scheduling
   → FCFS
   → SJF
   → SRTF
   → Round Robin
   → Priority

5. Waiting Time / Turnaround Time / Response Time

6. Race Condition

7. Critical Section

8. Mutex vs Semaphore

9. Deadlock
   → Four Conditions
   → Prevention
   → Avoidance
   → Banker's Algorithm

10. Paging

11. Virtual Memory

12. Page Fault

13. Page Replacement
   → FIFO
   → LRU
   → Optimal

14. TLB

15. Thrashing
```

## ⭐⭐⭐ Important

```text
16. IPC

17. fork() and exec()

18. Zombie vs Orphan

19. Starvation and Aging

20. Concurrency vs Parallelism

21. Fragmentation

22. File Allocation

23. Inode vs File Descriptor

24. Hard Link vs Symbolic Link

25. Disk Scheduling
```

## ⭐⭐ Basic Awareness

```text
26. Segmentation

27. Swapping

28. Working Set

29. Mounting

30. Disk Formatting
```

> **Placement strategy:** Don't try to memorize every OS definition. Be able to **explain the concept in simple words, compare related concepts, draw the basic flow, and solve the common numerical/scenario-based questions.** That is usually much more useful in an interview than memorizing textbook paragraphs.