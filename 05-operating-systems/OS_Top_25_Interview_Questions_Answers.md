# Operating Systems – Top 25 Interview Questions & Answers
## System Engineer / Fresher Interview Preparation
### Infosys SE / Capgemini Exceller Focus

---

## 🟢 BASIC LEVEL

### 1. What is an Operating System?

**Answer:**

An Operating System (OS) is system software that acts as an interface between the user/applications and computer hardware.

It manages resources such as CPU, memory, files, and input/output devices and provides services required to run applications.

**Examples:** Windows, Linux, macOS, Android.

**Interview follow-up:** What are the main functions of an OS?

---

### 2. What are the main functions of an Operating System?

**Answer:**

The major functions of an OS are:

1. **Process Management** – Creates, schedules, and terminates processes.
2. **Memory Management** – Allocates and deallocates memory to processes.
3. **File Management** – Creates, reads, writes, and manages files and directories.
4. **Device Management** – Controls hardware devices through device drivers.
5. **Security** – Controls access to system resources.
6. **Resource Management** – Allocates CPU, memory, and other resources efficiently.

---

### 3. What is a Program and what is a Process?

**Answer:**

A **program** is a passive set of instructions stored on a disk.

A **process** is a program that is currently executing.

**Example:**

A `.exe` file stored on the computer is a program. When we open it and it starts executing, the OS creates a process.

**Simple difference:**

| Program | Process |
|---|---|
| Passive | Active |
| Stored on disk | Loaded into memory |
| Does not have execution state | Has execution state |

---

### 4. What is a Process?

**Answer:**

A process is a program that is currently being executed.

When a program starts execution, the operating system creates a process and assigns resources such as memory, CPU time, and other required resources.

The OS maintains information about a process using a **Process Control Block (PCB)**.

**Example:**

When we open a web browser, the operating system creates processes to execute it.

---

### 5. What are the different states of a Process?

**Answer:**

The common process states are:

1. **New** – The process is being created.
2. **Ready** – The process is waiting to get CPU time.
3. **Running** – The process is currently executing.
4. **Waiting/Blocked** – The process is waiting for an event or I/O operation.
5. **Terminated** – The process has completed execution.

**Typical flow:**

`New → Ready → Running → Waiting → Ready → Running → Terminated`

---

### 6. What is a Process Control Block (PCB)?

**Answer:**

A Process Control Block (PCB) is a data structure maintained by the operating system to store information about a process.

It generally contains:

- Process ID (PID)
- Process state
- Program counter
- CPU registers
- CPU scheduling information
- Memory management information
- I/O status information

**Why is it important?**

During context switching, the OS saves the current process information in its PCB and loads the information of another process.

---

### 7. What is a Thread?

**Answer:**

A thread is the smallest unit of CPU execution within a process.

A process can contain multiple threads, and threads belonging to the same process can share resources such as memory and files.

**Example:**

A web browser may use different threads for handling user input, loading web pages, and background tasks.

---

### 8. What is the difference between a Process and a Thread?

**Answer:**

| Process | Thread |
|---|---|
| Independent execution unit | Execution unit within a process |
| Has its own address space | Shares address space with other threads of the process |
| More expensive to create | Cheaper to create |
| Inter-process communication is comparatively complex | Communication is easier through shared memory |
| Context switching is generally more expensive | Thread switching is generally lighter |

**Interview point:**

Threads are useful when multiple tasks need to execute concurrently within the same application.

---

## 🟡 MEDIUM LEVEL

### 9. What is Multithreading?

**Answer:**

Multithreading is the execution of multiple threads within a single process.

It allows an application to perform multiple tasks concurrently.

**Advantages:**

- Better responsiveness
- Better CPU utilization
- Faster execution for suitable tasks
- Resource sharing between threads

**Disadvantages:**

- Synchronization problems
- Race conditions
- Debugging can be difficult
- Incorrect synchronization can cause deadlocks

---

### 10. What is Context Switching?

**Answer:**

Context switching is the process of saving the state of a currently running process or thread and loading the saved state of another process or thread.

The OS performs context switching when it changes the CPU from one execution unit to another.

**Example:**

If Process A is running and the scheduler decides to run Process B, the OS saves Process A's state and loads Process B's state.

**Important point:**

Context switching introduces overhead because saving and restoring execution state takes CPU time.

---

### 11. What is CPU Scheduling?

**Answer:**

CPU scheduling is the process of selecting a process from the ready queue and assigning the CPU to it.

The main goal is to use the CPU efficiently and provide good performance.

Common objectives include:

- High CPU utilization
- High throughput
- Low waiting time
- Low turnaround time
- Low response time

---

### 12. What are the different CPU Scheduling Algorithms?

**Answer:**

Important CPU scheduling algorithms include:

### FCFS – First Come First Serve

Processes are executed in the order in which they arrive.

**Advantage:** Simple.

**Disadvantage:** Can cause the convoy effect and high waiting time.

### SJF – Shortest Job First

The process with the shortest CPU burst is selected first.

**Advantage:** Gives minimum average waiting time when burst times are known.

**Disadvantage:** Long processes may suffer starvation.

### SRTF – Shortest Remaining Time First

It is the preemptive version of SJF. The process with the shortest remaining execution time gets the CPU.

### Round Robin

Each process gets a fixed time slice called a **time quantum**.

It is commonly used in time-sharing systems.

### Priority Scheduling

The process with the highest priority is selected first.

A disadvantage can be starvation of low-priority processes.

---

### 13. What is the difference between Preemptive and Non-Preemptive Scheduling?

**Answer:**

### Preemptive Scheduling

The OS can take the CPU away from a running process and assign it to another process.

**Examples:**
- Round Robin
- SRTF
- Preemptive Priority Scheduling

### Non-Preemptive Scheduling

Once a process gets the CPU, it keeps it until it finishes or voluntarily enters a waiting state.

**Examples:**
- FCFS
- Non-preemptive SJF
- Non-preemptive Priority Scheduling

**Simple difference:**

Preemptive → OS can interrupt a running process.

Non-preemptive → OS normally waits until the process releases the CPU.

---

### 14. What is Starvation?

**Answer:**

Starvation occurs when a process waits for a very long time because other processes continuously receive the required resource or CPU time.

**Example:**

In priority scheduling, if high-priority processes continuously arrive, a low-priority process may keep waiting.

**Solution:**

Aging can be used to reduce starvation.

---

### 15. What is Aging?

**Answer:**

Aging is a technique used to prevent starvation.

In aging, the priority of a process is gradually increased as it waits for a long time.

**Example:**

If a low-priority process waits for a long time, the OS can gradually increase its priority so that it eventually gets CPU time.

---

## 🔴 DEADLOCK

### 16. What is Deadlock?

**Answer:**

Deadlock is a situation where two or more processes are permanently waiting for resources held by each other, so none of them can continue.

**Simple example:**

- Process A holds Resource 1 and waits for Resource 2.
- Process B holds Resource 2 and waits for Resource 1.

Both processes keep waiting.

---

### 17. What are the four necessary conditions for Deadlock?

**Answer:**

Four conditions must exist for deadlock:

### 1. Mutual Exclusion

A resource can be used by only one process at a time.

### 2. Hold and Wait

A process holds at least one resource while waiting for another resource.

### 3. No Preemption

A resource cannot be forcibly taken from a process.

### 4. Circular Wait

A circular chain exists where each process is waiting for a resource held by the next process.

**Important:**

If at least one of these conditions is prevented, deadlock can be prevented.

---

### 18. What is the difference between Deadlock and Starvation?

**Answer:**

| Deadlock | Starvation |
|---|---|
| Processes wait for each other | A process waits because others keep getting resources |
| Usually involves circular waiting | Usually caused by unfair scheduling/resource allocation |
| Multiple processes can be stuck | Usually one or more processes are continuously delayed |
| Processes cannot proceed | The process may eventually proceed |

**Example:**

Deadlock → A waits for B and B waits for A.

Starvation → A continuously gets skipped because higher-priority processes keep getting CPU time.

---

### 19. How can an Operating System handle Deadlock?

**Answer:**

There are four major approaches:

### 1. Deadlock Prevention

Prevent at least one of the four necessary conditions from occurring.

### 2. Deadlock Avoidance

The OS checks whether allocating a resource will keep the system in a safe state.

**Example:** Banker's Algorithm.

### 3. Deadlock Detection

The OS allows deadlocks to occur and periodically checks whether a deadlock exists.

### 4. Deadlock Recovery

After detecting deadlock, the OS takes action such as terminating processes or taking resources back.

---

### 20. What is the Banker's Algorithm?

**Answer:**

Banker's Algorithm is a deadlock avoidance algorithm.

Before allocating resources, it checks whether the allocation will leave the system in a **safe state**.

If the system remains safe, the resource can be allocated. Otherwise, the request may be delayed.

**Simple idea:**

The algorithm tries to ensure that all processes can eventually finish without causing a deadlock.

---

## 🔵 MEMORY MANAGEMENT

### 21. What is Virtual Memory?

**Answer:**

Virtual memory is a memory management technique that allows a system to use part of secondary storage as an extension of RAM.

It allows programs to run even when their entire required memory cannot fit into physical RAM at the same time.

Virtual memory is commonly implemented using **paging**.

**Advantage:**

It allows larger programs or more processes to run than physical RAM alone might permit.

---

### 22. What is Paging?

**Answer:**

Paging is a memory management technique in which:

- Logical memory is divided into fixed-size **pages**.
- Physical memory is divided into fixed-size **frames**.
- Pages are loaded into available frames.

A **page table** is used to map pages to physical frames.

**Example:**

If a process has 4 pages and physical memory has available frames, those pages do not necessarily need to occupy consecutive physical memory locations.

**Advantage:**

Paging helps eliminate external fragmentation.

---

### 23. What is a Page Fault?

**Answer:**

A page fault occurs when a process tries to access a page that is not currently present in physical memory.

The OS then:

1. Detects the page fault.
2. Finds the required page on secondary storage.
3. Loads the page into an available frame.
4. Updates the page table.
5. Resumes execution.

**Important:**

A page fault is not necessarily an error. It is a normal part of virtual memory management.

---

### 24. What is the difference between Paging and Segmentation?

**Answer:**

| Paging | Segmentation |
|---|---|
| Memory is divided into fixed-size pages | Memory is divided into variable-size segments |
| Based mainly on physical memory management | Based on logical program structure |
| Page size is fixed | Segment size can vary |
| Helps avoid external fragmentation | Can suffer from external fragmentation |
| Uses page tables | Uses segment tables |

**Example of segments:**

A program can logically have:

- Code segment
- Data segment
- Stack segment

---

### 25. What is Fragmentation?

**Answer:**

Fragmentation means inefficient use of memory because available memory is divided or allocated in a way that makes some space unusable.

There are two major types:

### Internal Fragmentation

Unused space exists **inside** an allocated memory block.

**Example:**

If a process needs 18 KB but receives a 20 KB fixed-size block, 2 KB is wasted inside the allocated block.

### External Fragmentation

Free memory exists, but it is divided into many small non-contiguous blocks.

**Example:**

There may be enough total free memory to satisfy a request, but the free memory is not available as one sufficiently large contiguous block.

---

# ⭐ IMPORTANT DIFFERENCES TO PREPARE

## 1. Program vs Process

Program = passive instructions.

Process = program currently executing.

## 2. Process vs Thread

Process = independent execution unit with its own address space.

Thread = lightweight execution unit within a process.

## 3. Preemptive vs Non-Preemptive

Preemptive = OS can interrupt a running process.

Non-preemptive = process normally keeps CPU until it finishes or blocks.

## 4. Deadlock vs Starvation

Deadlock = processes are stuck waiting for each other.

Starvation = a process waits for an unfairly long time because other processes keep getting resources.

## 5. Paging vs Segmentation

Paging = fixed-size memory blocks.

Segmentation = variable-size logical blocks.

## 6. Internal vs External Fragmentation

Internal = wasted space inside allocated memory.

External = free space scattered between allocated blocks.

## 7. Mutex vs Semaphore

Mutex = synchronization mechanism generally used for mutual exclusion.

Semaphore = synchronization mechanism that can control access to a resource using a counter.

---

# 🎯 TOP 15 QUESTIONS TO PRIORITIZE

If you have limited preparation time, master these first:

1. What is an Operating System?
2. Process vs Thread
3. Process States
4. PCB
5. Context Switching
6. CPU Scheduling
7. FCFS
8. SJF
9. Round Robin
10. Preemptive vs Non-Preemptive Scheduling
11. Deadlock
12. Four Conditions of Deadlock
13. Starvation and Aging
14. Virtual Memory
15. Paging and Page Fault

---

# 💡 HOW TO ANSWER OS QUESTIONS IN AN INTERVIEW

Use this simple structure:

**Definition → Explanation → Example → Difference/Advantage**

For example:

**Interviewer:** What is a process?

**Good answer:**

> "A process is a program that is currently being executed. When a program starts execution, the operating system creates a process and assigns resources such as memory and CPU time to it. For example, when I open a browser, the operating system creates processes to execute it. The OS maintains information about the process using a Process Control Block."

This style is better than giving a textbook definition only.

---

# ⚠️ IMPORTANT FOR INFOSYS / CAPGEMINI

Do not memorize these answers word-for-word.

You should be able to explain each concept in your own words.

The interviewer may ask follow-up questions such as:

- Why is it required?
- How does it work?
- Give a real-world example.
- What is the difference?
- What happens internally?
- What are its advantages and disadvantages?

Prepare to answer the **"why" and "how"**, not just the definition.

---

# ✅ FINAL PREPARATION TARGET

For a System Engineer fresher interview, you should be able to:

- Explain processes and threads clearly.
- Explain CPU scheduling algorithms.
- Explain deadlock and its four conditions.
- Explain starvation and aging.
- Explain virtual memory and paging.
- Explain page faults.
- Explain fragmentation.
- Compare common OS concepts.
- Solve basic CPU scheduling problems if asked.
- Give simple real-world examples.

**Goal: Understand → Explain → Give Example → Handle Follow-up**
