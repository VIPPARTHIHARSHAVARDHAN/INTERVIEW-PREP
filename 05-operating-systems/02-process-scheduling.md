# Process Scheduling

## 1. What is Process Scheduling?

**Process scheduling** is the mechanism used by the operating system to select a process from the ready queue and allocate the CPU to it.

```text
Ready Queue
    ↓
Scheduler
    ↓
Selected Process
    ↓
CPU
```

The main goal is to use the CPU efficiently while providing good response and fairness.

---

# 2. Why is CPU Scheduling Needed?

Usually, multiple processes are ready to execute, but a CPU core can execute only one thread at a time.

```text
P1 ─┐
P2 ─┤
P3 ─┼──→ Scheduler → CPU
P4 ─┘
```

The scheduler decides **which process should run next**.

---

# 3. What is the Ready Queue?

The **ready queue** contains processes that are ready to execute but are waiting for CPU allocation.

```text
Ready Queue:

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

# 4. What is a CPU Scheduler?

The **CPU scheduler** selects a process/thread from the ready queue and gives it the opportunity to run on the CPU.

### Interview Answer

> The CPU scheduler selects a runnable process or thread from the ready queue according to a scheduling policy.

---

# 5. What is Preemptive Scheduling?

In **preemptive scheduling**, the operating system can interrupt a running process and allocate the CPU to another runnable process.

Example:

```text
P1 running
   ↓
Timer / higher-priority event
   ↓
P1 paused
   ↓
P2 runs
```

Common examples:

```text
Round Robin
Shortest Remaining Time First
Preemptive Priority Scheduling
```

---

# 6. What is Non-Preemptive Scheduling?

In **non-preemptive scheduling**, once a process gets the CPU, it normally keeps it until it finishes or blocks/waits.

Example:

```text
P1 runs
   ↓
P1 completes / blocks
   ↓
P2 runs
```

Common examples:

```text
FCFS
Non-Preemptive SJF
Non-Preemptive Priority
```

---

# 7. Preemptive vs Non-Preemptive

| Preemptive | Non-Preemptive |
|---|---|
| OS can interrupt a running process | Running process normally keeps CPU until completion/block |
| Better responsiveness | Simpler |
| More context-switch overhead | Usually less context-switch overhead |
| Useful for interactive systems | Suitable for simpler workloads |

---

# 8. Important Scheduling Criteria

The most important CPU scheduling metrics are:

### 1. CPU Utilization

Percentage of time the CPU is busy.

```text
Higher CPU utilization → generally better
```

---

### 2. Throughput

Number of processes completed per unit of time.

```text
Higher throughput → generally better
```

---

### 3. Turnaround Time

Total time from process arrival/submission until its completion.

```text
Turnaround Time
= Completion Time - Arrival Time
```

---

### 4. Waiting Time

Time a process spends waiting in the ready queue.

For the standard scheduling model:

```text
Waiting Time
= Turnaround Time - Burst Time
```

---

### 5. Response Time

Time from when a process arrives until it first gets CPU service.

```text
Response Time
= First CPU Start Time - Arrival Time
```

---

# 9. Turnaround vs Waiting vs Response Time

| Metric | Meaning |
|---|---|
| Turnaround Time | Arrival → Completion |
| Waiting Time | Time waiting in ready queue |
| Response Time | Arrival → First CPU execution |

### Easy Memory Trick

```text
Turnaround
→ When did it finish?

Waiting
→ How long did it wait?

Response
→ How quickly did it first respond?
```

---

# 10. FCFS Scheduling

**FCFS (First Come, First Served)** executes processes in the order they arrive.

```text
Arrival:

P1 → P2 → P3

Execution:

P1 → P2 → P3
```

It is generally **non-preemptive**.

---

## Example

Suppose:

```text
Process    Burst Time
P1         5
P2         3
P3         2
```

Execution:

```text
| P1 | P2 | P3 |
0    5    8    10
```

---

## Advantages

```text
Simple
Easy to implement
Fair according to arrival order
```

## Disadvantages

```text
Can cause large waiting times
Poor response for short jobs behind long jobs
Convoy effect
```

---

# 11. What is Convoy Effect?

The **convoy effect** occurs when a long-running process holds the CPU and many shorter processes wait behind it.

Example:

```text
Long process
     ↓
████████████████

Short processes
     ↓
waiting waiting waiting
```

This is commonly associated with FCFS scheduling.

---

# 12. SJF Scheduling

**SJF (Shortest Job First)** selects the process with the shortest CPU burst time.

Example:

```text
P1 → 8
P2 → 3
P3 → 5
P4 → 2
```

Order:

```text
P4 → P2 → P3 → P1
```

Standard SJF is **non-preemptive**.

---

# 13. Why is SJF Important?

SJF is important because, under the standard assumptions used in scheduling theory, it minimizes the **average waiting time** when the required CPU burst times are known.

### Problem

The OS generally does not know the exact future CPU burst time of a process.

Therefore, practical systems must estimate or use other scheduling strategies.

---

# 14. SRTF Scheduling

**SRTF (Shortest Remaining Time First)** is the preemptive version of SJF.

The scheduler selects the process with the **shortest remaining CPU time**.

Example:

```text
P1 running
   ↓
P2 arrives with shorter remaining time
   ↓
P1 is preempted
   ↓
P2 runs
```

---

# 15. SJF vs SRTF

| SJF | SRTF |
|---|---|
| Usually non-preemptive | Preemptive |
| Uses shortest burst time | Uses shortest remaining time |
| Running process normally isn't interrupted | Running process can be interrupted |
| Lower context-switch overhead | More context-switch overhead |

---

# 16. Priority Scheduling

In **Priority Scheduling**, each process is assigned a priority and the scheduler chooses according to that priority.

Example:

```text
P1 → Priority 3
P2 → Priority 1
P3 → Priority 2
```

If lower number means higher priority:

```text
P2 → P3 → P1
```

> Always check how the system defines priority; some systems use higher numbers for higher priority.

Priority scheduling can be:

```text
Preemptive
or
Non-Preemptive
```

---

# 17. Problem with Priority Scheduling

A low-priority process may wait for a very long time.

This is called **starvation**.

Example:

```text
High-priority processes keep arriving
          ↓
Low-priority process keeps waiting
          ↓
Starvation
```

---

# 18. What is Aging?

**Aging** gradually increases the priority of a process that has been waiting for a long time.

Example:

```text
Low priority
     ↓
waits
     ↓
priority improves
     ↓
eventually gets CPU
```

### Purpose

```text
Prevent starvation
```

---

# 19. Round Robin Scheduling

**Round Robin (RR)** is a preemptive scheduling algorithm commonly associated with time-sharing systems.

Each process gets a fixed **time quantum**.

Example:

```text
Time Quantum = 2

P1 → P2 → P3 → P1 → P2 → ...
```

---

# 20. How Round Robin Works

Suppose:

```text
Time Quantum = 2

P1 = 5
P2 = 3
P3 = 4
```

The CPU gives each process up to one time quantum at a time:

```text
P1 → 2 units
P2 → 2 units
P3 → 2 units
P1 → 2 units
...
```

If a process finishes before its quantum expires, the CPU moves to the next process.

---

# 21. What is Time Quantum?

The **time quantum** is the maximum amount of CPU time given to a process during one turn in Round Robin scheduling.

```text
Process
   ↓
CPU
   ↓
Time Quantum expires
   ↓
Next process
```

---

# 22. What Happens if Time Quantum is Too Small?

A very small time quantum can cause:

```text
Many context switches
↓
More overhead
↓
Less CPU time for useful work
```

---

# 23. What Happens if Time Quantum is Too Large?

If the time quantum becomes very large, Round Robin can behave more like FCFS.

```text
Very large quantum
        ↓
Processes run for long periods
        ↓
Less responsive
        ↓
Closer to FCFS behavior
```

---

# 24. Round Robin Advantages

```text
Good response time
Fair CPU sharing
Suitable for interactive/time-sharing workloads
Prevents one process from monopolizing CPU for too long
```

---

# 25. Round Robin Disadvantages

```text
Context-switch overhead
Performance depends on time quantum
Too-small quantum → excessive switching
Too-large quantum → approaches FCFS behavior
```

---

# 26. FCFS vs SJF vs Priority vs Round Robin

| Algorithm | Preemptive? | Main Idea |
|---|---|---|
| FCFS | Usually No | First arrival runs first |
| SJF | No | Shortest burst first |
| SRTF | Yes | Shortest remaining time first |
| Priority | Can be either | Highest-priority process first |
| Round Robin | Yes | Each process gets a time quantum |

---

# 27. Which Scheduling Algorithm Gives Minimum Average Waiting Time?

> Under the standard theoretical assumptions and known CPU burst times, **SJF** gives the minimum average waiting time.

Its preemptive counterpart is:

```text
SRTF
```

---

# 28. Which Scheduling Algorithm is Best for Time-Sharing Systems?

> **Round Robin** is commonly used as a basic example for time-sharing because each runnable process receives a time quantum.

---

# 29. What is Starvation?

**Starvation** occurs when a process waits indefinitely or for an unreasonably long time because other processes continually receive the resources/CPU it needs.

Commonly associated with:

```text
Priority Scheduling
SJF/SRTF in certain workloads
```

---

# 30. Starvation vs Deadlock

| Starvation | Deadlock |
|---|---|
| A process waits indefinitely for a resource/CPU opportunity | Processes are stuck waiting on each other/resources |
| Other processes may continue executing | A set of processes cannot make progress |
| Can occur due to unfair scheduling | Requires specific deadlock conditions |

---

# 31. What is Dispatcher?

The **dispatcher** gives control of the CPU to the process selected by the scheduler.

Its work includes things such as:

```text
Context switching
Switching to user mode when appropriate
Starting/resuming the selected process
```

---

# 32. Scheduler vs Dispatcher

| Scheduler | Dispatcher |
|---|---|
| Decides which process should run | Transfers CPU control to selected process |
| Makes scheduling decision | Carries out the switch |
| Selects process | Starts/resumes selected process |

---

# 33. What is Dispatch Latency?

**Dispatch latency** is the time required for the system to stop one process and start executing another selected process.

```text
P1
 ↓
Switch
 ↓
P2
```

The time involved in the switch contributes to dispatch latency.

---

# 34. Scheduling Numerical Problems

Placement interviews may give you:

```text
Process
Arrival Time
Burst Time
Priority
Time Quantum
```

and ask you to calculate:

```text
Gantt Chart
Completion Time
Turnaround Time
Waiting Time
Response Time
Average Waiting Time
Average Turnaround Time
```

---

# 35. Important Formulas

### Completion Time

The time at which a process finishes.

```text
CT = Completion Time
```

---

### Turnaround Time

```text
TAT = CT - AT
```

Where:

```text
CT = Completion Time
AT = Arrival Time
```

---

### Waiting Time

```text
WT = TAT - BT
```

Where:

```text
TAT = Turnaround Time
BT  = Burst Time
```

---

### Response Time

```text
RT = First Start Time - Arrival Time
```

---

### Average Waiting Time

```text
Average WT
= Sum of all Waiting Times / Number of Processes
```

---

### Average Turnaround Time

```text
Average TAT
= Sum of all Turnaround Times / Number of Processes
```

---

# 36. Simple FCFS Numerical Example

Given:

```text
Process    Arrival Time    Burst Time

P1         0               5
P2         1               3
P3         2               2
```

FCFS order:

```text
P1 → P2 → P3
```

Gantt chart:

```text
|   P1   |  P2  | P3 |
0        5      8    10
```

Completion times:

```text
P1 = 5
P2 = 8
P3 = 10
```

Turnaround:

```text
P1 = 5 - 0 = 5
P2 = 8 - 1 = 7
P3 = 10 - 2 = 8
```

Waiting:

```text
P1 = 5 - 5 = 0
P2 = 7 - 3 = 4
P3 = 8 - 2 = 6
```

Average waiting time:

```text
(0 + 4 + 6) / 3
= 10 / 3
≈ 3.33
```

---

# 37. Most Important Interview Questions

Prepare these questions especially well:

```text
1. What is process scheduling?

2. Why is CPU scheduling needed?

3. What is a ready queue?

4. What is a CPU scheduler?

5. What is preemptive scheduling?

6. What is non-preemptive scheduling?

7. Preemptive vs non-preemptive scheduling?

8. What is FCFS?

9. Advantages and disadvantages of FCFS?

10. What is convoy effect?

11. What is SJF?

12. Why does SJF minimize average waiting time?

13. What is SRTF?

14. SJF vs SRTF?

15. What is Priority Scheduling?

16. What is starvation?

17. What is aging?

18. How does aging solve starvation?

19. What is Round Robin?

20. What is a time quantum?

21. What happens if the time quantum is too small?

22. What happens if the time quantum is too large?

23. Which scheduling algorithm is suitable for time-sharing?

24. What is a dispatcher?

25. Scheduler vs dispatcher?

26. What is dispatch latency?

27. What is turnaround time?

28. What is waiting time?

29. What is response time?

30. How do you solve CPU scheduling numerical problems?
```

---

# 38. Quick Revision

```text
CPU SCHEDULING
→ Select a runnable process/thread for CPU

READY QUEUE
→ Runnable processes waiting for CPU

PREEMPTIVE
→ OS can interrupt running process

NON-PREEMPTIVE
→ Process normally runs until completion/block

FCFS
→ First Come First Served
→ Simple
→ Can cause convoy effect

SJF
→ Shortest Job First
→ Minimum average waiting time under standard assumptions
→ Usually non-preemptive

SRTF
→ Shortest Remaining Time First
→ Preemptive SJF

PRIORITY
→ Highest-priority process selected according to priority rule
→ Can cause starvation

AGING
→ Gradually increases waiting process priority
→ Helps prevent starvation

ROUND ROBIN
→ Each process gets time quantum
→ Preemptive
→ Good for time-sharing

SMALL QUANTUM
→ More context switches

LARGE QUANTUM
→ Can approach FCFS

TURNAROUND TIME
→ CT - AT

WAITING TIME
→ TAT - BT

RESPONSE TIME
→ First Start Time - AT

SCHEDULER
→ Decides who runs

DISPATCHER
→ Gives CPU to selected process

DISPATCH LATENCY
→ Time involved in switching to selected process
```

---

# 39. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Process scheduling basics
Preemptive vs non-preemptive
FCFS
SJF
SRTF
Priority Scheduling
Round Robin
Time Quantum
Starvation
Aging
Convoy Effect
Turnaround Time
Waiting Time
Response Time
Gantt Chart problems
Scheduling numerical questions
```

## ⭐⭐⭐ Good to Know

```text
Scheduler vs Dispatcher
Dispatch Latency
Detailed scheduling implementation
```

> **For placement interviews, numerical scheduling problems are worth practicing.** You should be able to take Arrival Time, Burst Time, Priority, and Time Quantum and quickly construct the Gantt chart and calculate CT, TAT, WT, RT, and their averages.