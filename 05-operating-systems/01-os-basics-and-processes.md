# OS Basics and Processes

## 1. What is an Operating System?

An **Operating System (OS)** is system software that acts as an interface between the user/applications and computer hardware.

It manages resources such as:

- CPU
- Memory
- Files
- Input/Output devices
- Processes
- Security and access

### Simple view

```text
User / Applications
        ↓
Operating System
        ↓
Hardware
```

### Examples

```text
Windows
Linux
macOS
Android
iOS
```

---

# 2. What are the Main Functions of an OS?

The major responsibilities of an OS are:

```text
Process Management
Memory Management
File Management
Device Management
Security
Resource Management
```

### Interview Answer

> An operating system manages hardware and software resources and provides services to application programs.

---

# 3. What is the Kernel?

The **kernel** is the core part of an operating system that runs with high privileges and manages hardware resources.

It handles tasks such as:

- CPU/process management
- Memory management
- Device management
- System calls
- Protection

```text
Applications
     ↓
System Calls
     ↓
Kernel
     ↓
Hardware
```

### Interview Question

**Q: What is the difference between OS and Kernel?**

> The OS is the complete system software that provides an environment for applications and manages resources. The kernel is the core component of the OS that directly manages system resources and hardware access.

---

# 4. User Mode vs Kernel Mode

Modern operating systems use different privilege levels to protect the system.

## User Mode

Applications normally run in **user mode**.

They have restricted access to:

- Hardware
- Kernel memory
- Privileged CPU instructions

## Kernel Mode

The kernel runs in **kernel mode** and has privileged access to system resources.

### Comparison

| User Mode | Kernel Mode |
|---|---|
| Restricted privileges | High privileges |
| Applications normally run here | Kernel runs here |
| Cannot directly perform privileged operations | Can perform privileged operations |
| Failure is generally isolated to the application | Kernel failure can affect the whole system |

---

# 5. What is a System Call?

A **system call** is a mechanism through which a user-level program requests a service from the operating system kernel.

Example:

```text
Application
    ↓
System Call
    ↓
Kernel
    ↓
Requested operation
```

Examples of operations commonly exposed through system calls:

```text
Create process
Open file
Read file
Write file
Allocate/manage resources
```

---

# 6. Why are System Calls Needed?

Applications cannot directly perform many privileged operations.

For example:

```text
Application
    ↓
"I want to read this file"
    ↓
System Call
    ↓
Kernel checks permissions
    ↓
File system / device operation
    ↓
Result returned
```

This provides controlled access to system resources.

---

# 7. What is a Process?

A **process** is a program in execution.

A program is a passive set of instructions stored somewhere, while a process is an active execution instance.

Example:

```text
Program:
    calculator.exe

When executed:
    ↓
Process is created
```

### Process contains things such as:

- Program code
- Data
- Stack
- Heap
- CPU/register state
- Process-related OS information

---

# 8. Program vs Process

| Program | Process |
|---|---|
| Passive | Active |
| Stored instructions | Program currently executing |
| Does not have execution state by itself | Has execution state |
| Can exist without running | Exists while executing |

### Easy Interview Answer

> A program is a passive set of instructions, whereas a process is a program in execution with its own execution state and resources.

---

# 9. Process States

A process generally moves through different states during its lifetime.

Common states:

```text
New
 ↓
Ready
 ↓
Running
 ↓
Terminated
```

A running process may also move to:

```text
Running
   ↓
Waiting / Blocked
   ↓
Ready
```

### Main States

### New

The process is being created.

### Ready

The process is ready to run but is waiting for CPU time.

### Running

The CPU is executing the process.

### Waiting / Blocked

The process is waiting for an event, such as I/O completion.

### Terminated

The process has finished execution.

---

# 10. Process State Diagram

```text
             admitted
   NEW ----------------→ READY
                           |
                           | scheduler dispatch
                           ↓
                        RUNNING
                       /   |   \
                      /    |    \
             I/O wait     |     | exit
                    ↓      |     ↓
                 WAITING   |  TERMINATED
                    |      |
                    |      | preemption
                    ↓      |
                  READY ←---
```

---

# 11. What is a PCB?

**PCB (Process Control Block)** is an OS data structure that stores information about a process.

A PCB may contain:

```text
Process ID
Process State
Program Counter
CPU Registers
CPU Scheduling Information
Memory Management Information
Accounting Information
I/O Status Information
```

### Simple representation

```text
PCB
├── Process ID
├── Process State
├── Program Counter
├── CPU Registers
├── Scheduling Information
├── Memory Information
└── I/O Information
```

---

# 12. What is Process ID (PID)?

A **PID** is a unique identifier assigned to a process by the operating system.

Example:

```text
Process
   ↓
PID = 1524
```

The OS uses the PID to identify and manage the process.

---

# 13. What is a Context Switch?

A **context switch** occurs when the CPU switches from one process/thread to another and the OS saves the current execution state and restores the state of the next one.

Example:

```text
Process P1 running
       ↓
Save P1 context
       ↓
Load P2 context
       ↓
Process P2 running
```

The saved state can include:

```text
Program Counter
CPU Registers
Process state
Other execution-related information
```

---

# 14. Why is Context Switching Needed?

Suppose multiple processes need the CPU:

```text
P1 → P2 → P3 → P1 → ...
```

The CPU cannot execute all of them at exactly the same instant on a single core.

The OS switches between them so that each gets CPU time.

---

# 15. Is Context Switching Free?

**No.**

Context switching introduces overhead because the OS needs to:

```text
Save current state
↓
Select/load next state
↓
Resume execution
```

During the switch, useful application work is generally not being performed.

---

# 16. What is a Thread?

A **thread** is the smallest unit of CPU execution/scheduling within a process in common OS terminology.

A process can contain multiple threads.

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
```

while each thread has its own:

```text
Stack
Registers / execution state
Program Counter
```

---

# 17. Process vs Thread

| Process | Thread |
|---|---|
| Independent execution unit | Execution unit within a process |
| Has its own address space | Threads in same process share address space |
| More expensive to create/manage | Generally cheaper to create/manage |
| Communication can require IPC mechanisms | Communication through shared memory is easier |
| Failure is generally more isolated | A faulty thread can affect its process |

### Interview Answer

> A process is an independent execution environment, while a thread is an execution unit within a process. Threads of the same process share resources such as code, data, and heap.

---

# 18. What is IPC?

**IPC (Inter-Process Communication)** refers to mechanisms that allow processes to communicate and coordinate with each other.

Common IPC mechanisms include:

```text
Pipes
Message Queues
Shared Memory
Sockets
Signals
```

---

# 19. Why is IPC Needed?

Processes normally have separate address spaces.

Therefore, they need controlled mechanisms to exchange information.

Example:

```text
Process A
    ↓
   IPC
    ↓
Process B
```

---

# 20. What is Multiprogramming?

**Multiprogramming** keeps multiple programs in memory so that the CPU can switch to another ready program when one is waiting, for example for I/O.

Goal:

```text
Keep CPU busy
```

---

# 21. What is Multitasking?

**Multitasking** allows multiple tasks to make progress by sharing CPU time.

Example:

```text
Browser
Music Player
VS Code
Terminal
```

The OS schedules CPU time among runnable tasks.

---

# 22. Multiprogramming vs Multitasking

| Multiprogramming | Multitasking |
|---|---|
| Multiple programs kept available for execution | Multiple tasks share CPU time |
| Focuses on keeping CPU utilized | Focuses on responsive concurrent task execution |
| Switching often occurs when a running program waits | Scheduling can use time slices/preemption |

---

# 23. What is Multiprocessing?

**Multiprocessing** means using multiple CPU cores/processors to execute tasks concurrently.

Example:

```text
CPU
├── Core 1 → Process A
├── Core 2 → Process B
├── Core 3 → Process C
└── Core 4 → Process D
```

---

# 24. Concurrency vs Parallelism

## Concurrency

Multiple tasks make progress during overlapping time periods.

```text
Time →
A: ███     ███
B:    ███     ███
```

## Parallelism

Multiple tasks execute literally at the same time on different CPU cores.

```text
Core 1 → Task A
Core 2 → Task B
```

### Interview Answer

> Concurrency is about managing multiple tasks that overlap in progress, while parallelism means executing multiple tasks at the same time using multiple execution resources.

---

# 25. What is a Scheduler?

A **scheduler** is an OS component that selects which ready process/thread should run next.

Conceptually:

```text
Ready Queue
   ↓
Scheduler
   ↓
Selected Process
   ↓
CPU
```

Detailed scheduling algorithms are covered in:

```text
02-process-scheduling.md
```

---

# 26. What is a Dispatcher?

The **dispatcher** is responsible for giving control of the CPU to the process selected by the scheduler.

Conceptually:

```text
Scheduler
    ↓
Selects process
    ↓
Dispatcher
    ↓
CPU starts/resumes process
```

---

# 27. What is a Ready Queue?

The **ready queue** contains processes/threads that are ready to execute but are waiting for CPU allocation.

```text
READY QUEUE

P1
P2
P3
P4
 ↓
Scheduler
 ↓
CPU
```

---

# 28. What is a Blocking Operation?

A blocking operation causes the current process/thread to wait until some required event occurs.

Example:

```text
Process
   ↓
Requests I/O
   ↓
Waiting / Blocked
   ↓
I/O completes
   ↓
Ready
```

---

# 29. What Happens When a Process Makes an I/O Request?

A simplified flow is:

```text
Running
   ↓
I/O request
   ↓
Waiting / Blocked
   ↓
I/O completes
   ↓
Ready
   ↓
Scheduled
   ↓
Running
```

This allows another ready process to use the CPU while the first process waits for I/O.

---

# 30. What is a Process Creation?

When a process creates another process, the newly created process is called a **child process**, while the creator is commonly called the **parent process**.

```text
Parent Process
      |
      ↓
Child Process
```

The exact process-creation mechanisms and parent/child behavior depend on the operating system.

---

# 31. What is a Zombie Process?

A **zombie process** is a terminated child process whose exit status has not yet been collected by its parent, so the OS retains a small amount of process information for it.

Conceptually:

```text
Child finishes
     ↓
Child terminates
     ↓
Exit status remains
     ↓
Parent has not collected it
     ↓
Zombie
```

---

# 32. What is an Orphan Process?

An **orphan process** is a child process whose original parent terminates before the child.

The operating system then re-parents the child according to its process-management rules.

---

# 33. Zombie vs Orphan

| Zombie | Orphan |
|---|---|
| Child has already terminated | Child is still running |
| Parent has not collected exit status | Original parent has terminated |
| Small process-table information remains | Child is re-parented |

---

# 34. What is a Daemon/Service?

A **daemon** on Unix-like systems is a background process that provides a service, often without direct user interaction.

Examples include services responsible for:

```text
Networking
Logging
Scheduling
Web services
```

Windows uses the term **service** for its analogous background service mechanism.

---

# 35. What is Booting?

**Booting** is the process of starting a computer and loading the operating system.

Simplified flow:

```text
Power On
   ↓
Firmware
   ↓
Bootloader
   ↓
OS Kernel
   ↓
System Initialization
   ↓
Login / User Environment
```

You only need this basic understanding for most placement interviews.

---

# 36. Most Important Interview Questions from This File

Prepare these particularly well:

```text
1. What is an Operating System?

2. What are the main functions of an OS?

3. What is a kernel?

4. OS vs Kernel?

5. What is a system call?

6. User mode vs Kernel mode?

7. What is a process?

8. Program vs Process?

9. What are the states of a process?

10. What is PCB?

11. What is PID?

12. What is context switching?

13. Why is context switching expensive?

14. What is a thread?

15. Process vs Thread?

16. What is IPC?

17. Why is IPC required?

18. What is multitasking?

19. What is multiprogramming?

20. What is multiprocessing?

21. Concurrency vs Parallelism?

22. What is a scheduler?

23. What is a ready queue?

24. What happens when a process requests I/O?

25. What is a zombie process?

26. What is an orphan process?

27. Zombie vs Orphan?

28. What is booting?
```

---

# 37. Quick Revision

```text
OS
→ Manages hardware and software resources

KERNEL
→ Core of OS
→ Manages system resources

SYSTEM CALL
→ Application requests OS service

USER MODE
→ Restricted privileges

KERNEL MODE
→ Privileged execution

PROGRAM
→ Passive instructions

PROCESS
→ Program in execution

PCB
→ Stores process information

PID
→ Identifies a process

PROCESS STATES
→ New
→ Ready
→ Running
→ Waiting/Blocked
→ Terminated

CONTEXT SWITCH
→ Save current execution state
→ Load another process/thread state

THREAD
→ Unit of execution within a process

IPC
→ Communication between processes

MULTIPROGRAMMING
→ Multiple programs available in memory
→ Keep CPU utilized

MULTITASKING
→ Multiple tasks share CPU time

MULTIPROCESSING
→ Multiple processors/cores execute tasks

CONCURRENCY
→ Tasks make overlapping progress

PARALLELISM
→ Tasks execute simultaneously

SCHEDULER
→ Selects next runnable process/thread

ZOMBIE
→ Terminated child
→ Exit status not collected

ORPHAN
→ Running child whose original parent terminated
```

# 38. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
What is OS?
Functions of OS
Kernel
System calls
User mode vs kernel mode
Process
Program vs process
Process states
PCB
Context switching
Thread
Process vs thread
IPC
Concurrency vs parallelism
Zombie vs orphan
```

## ⭐⭐⭐ Good to Know

```text
Multiprogramming
Multitasking
Multiprocessing
Scheduler
Ready queue
I/O blocking
Booting
Daemon/service
```

> **For placements, focus deeply on the ⭐⭐⭐⭐⭐ section.** The remaining topics should be understood at a basic level rather than studied in excessive detail.