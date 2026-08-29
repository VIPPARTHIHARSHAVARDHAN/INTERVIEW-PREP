# File Systems and Disk Management

## 1. What is a File System?

A **file system** is the method used by an operating system to organize, store, name, and access files on storage devices.

It manages:

```text
Files
Directories
File metadata
Storage allocation
Free space
File access
```

Examples of file systems:

```text
NTFS
FAT32
exFAT
ext4
APFS
```

---

# 2. What is a File?

A **file** is a named collection of related data stored on secondary storage.

Examples:

```text
resume.pdf
photo.jpg
program.py
data.txt
```

The OS provides mechanisms to:

```text
Create
Open
Read
Write
Close
Delete
```

files.

---

# 3. File Attributes

A file can have metadata such as:

```text
Name
Type
Size
Location
Owner
Permissions
Creation/modification information
```

The exact attributes depend on the operating system and file system.

---

# 4. Basic File Operations

Common file operations include:

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

Example:

```text
Open file
   ↓
Read / Write
   ↓
Close file
```

---

# 5. What is a Directory?

A **directory** is a structure used by the file system to organize and locate files and other directories.

Example:

```text
Project/
├── main.py
├── data.txt
└── images/
    ├── a.jpg
    └── b.jpg
```

---

# 6. File Path

A **path** specifies the location of a file or directory.

### Absolute Path

Specifies the complete location.

```text
/home/user/project/data.txt
```

### Relative Path

Specifies the location relative to the current directory.

```text
project/data.txt
```

---

# 7. File Access Methods

The major file access methods are:

```text
Sequential Access
Direct/Random Access
Indexed Access
```

---

# 8. Sequential Access

In **sequential access**, data is accessed in order from the beginning toward the end.

```text
Record 1
   ↓
Record 2
   ↓
Record 3
   ↓
Record 4
```

Example:

```text
Reading a text file from beginning to end
```

---

# 9. Direct / Random Access

In **direct access**, the system can access a particular location without reading all previous data.

Example:

```text
File

Block 0
Block 1
Block 2
Block 3
Block 4

        ↓
Directly access Block 3
```

This is useful when applications need to access specific records or blocks.

---

# 10. Indexed Access

**Indexed access** uses an index to locate data efficiently.

Conceptually:

```text
Index
├── Record A → Location 100
├── Record B → Location 500
└── Record C → Location 900
```

The index helps locate the required data without scanning everything sequentially.

---

# 11. File Allocation

The OS must determine where file data is stored on disk.

Important file-allocation methods are:

```text
Contiguous Allocation
Linked Allocation
Indexed Allocation
```

---

# 12. Contiguous Allocation

In **contiguous allocation**, the blocks of a file are stored next to each other.

Example:

```text
File A:

[10][11][12][13][14]
```

### Advantages

```text
Fast sequential access
Fast direct access
Simple
```

### Disadvantages

```text
External fragmentation
File growth can be difficult
```

---

# 13. Linked Allocation

In **linked allocation**, each file block contains a pointer to the next block.

Example:

```text
Block 5 → Block 19 → Block 8 → Block 25
```

The blocks do not need to be physically adjacent.

### Advantages

```text
No external fragmentation caused by requiring contiguous file blocks
Easy file growth
```

### Disadvantages

```text
Poorer random access
Pointer overhead
A damaged pointer can affect traversal
```

---

# 14. Indexed Allocation

In **indexed allocation**, an index block contains pointers to the blocks belonging to a file.

Example:

```text
Index Block
├── → Block 7
├── → Block 14
├── → Block 22
└── → Block 31
```

### Advantages

```text
Supports direct access
File blocks need not be contiguous
```

### Disadvantages

```text
Index-block overhead
Large files may require additional indexing structures
```

---

# 15. Contiguous vs Linked vs Indexed Allocation

| Feature | Contiguous | Linked | Indexed |
|---|---|---|---|
| Blocks adjacent | Yes | No | No |
| Sequential access | Fast | Good | Good |
| Direct access | Fast | Poor | Good |
| File growth | Difficult | Easy | Easier |
| External fragmentation | Possible | Avoided for file placement | Avoided for file placement |
| Pointer/index overhead | Low | High | Index overhead |

---

# 16. What is an Inode?

An **inode** is a data structure used by Unix-like file systems such as ext4 to store metadata about a file and information used to locate its data blocks.

It can contain information such as:

```text
File type
Permissions
Owner
File size
Timestamps
Links
Pointers/extent information for file data
```

The filename itself is generally stored in a directory entry that refers to the inode.

---

# 17. What is a File Descriptor?

A **file descriptor** is a small integer used by a process to refer to an open file or another I/O resource in Unix-like systems.

Common standard descriptors:

```text
0 → stdin
1 → stdout
2 → stderr
```

Example:

```text
Program
  ↓
File Descriptor
  ↓
Open File
  ↓
File System
```

---

# 18. Inode vs File Descriptor

| Inode | File Descriptor |
|---|---|
| File-system data structure | Process-level handle/reference |
| Stores file metadata and data-location information | Used by a process to access an open file/resource |
| Exists as part of the file system | Created/managed as part of opening a resource |
| Not simply the filename | Usually represented to the process by a small integer |

### Interview Answer

> An inode stores file metadata and information needed to locate file data, while a file descriptor is a process-level identifier used to access an open file or I/O resource.

---

# 19. Hard Link

A **hard link** is another directory entry referring to the same underlying file inode on Unix-like file systems.

Example:

```text
file1 ──┐
        ├──→ Same inode → Data
file2 ──┘
```

Both names refer to the same underlying file.

---

# 20. Symbolic Link

A **symbolic link** is a special file that stores a path/reference to another file or directory.

Example:

```text
link
 ↓
/home/user/file.txt
```

If the target is removed, the symbolic link can become broken.

---

# 21. Hard Link vs Symbolic Link

| Hard Link | Symbolic Link |
|---|---|
| Refers to the same inode | Refers to a path/target |
| Usually cannot cross file-system boundaries | Can generally cross file-system boundaries |
| Usually cannot link directories in normal user usage | Can point to directories |
| Remains valid if another filename is removed | Can become dangling if target disappears |

---

# 22. What is Disk Management?

**Disk management** involves managing storage devices and how data is physically or logically organized on them.

The OS manages:

```text
Disk space
Disk partitions
Disk scheduling
Free space
Storage allocation
I/O requests
```

---

# 23. Disk Structure

A traditional magnetic hard disk contains:

```text
Platters
Tracks
Sectors
```

Conceptually:

```text
Platter
 ├── Track
 │    ├── Sector
 │    ├── Sector
 │    └── Sector
```

Modern SSDs do not use physical tracks and sectors in the same mechanical way, but operating systems still expose block-oriented storage interfaces.

---

# 24. HDD vs SSD

### HDD

Hard Disk Drive uses:

```text
Rotating magnetic platters
Mechanical read/write head
```

Disk access can involve mechanical movement.

### SSD

Solid-State Drive uses:

```text
Flash memory
No mechanical read/write head
```

SSDs generally provide much lower access latency than HDDs.

---

# 25. Disk Access Time

For a traditional HDD, access time is commonly discussed in terms of:

```text
Seek Time
Rotational Latency
Transfer Time
```

### Seek Time

Time required to move the disk head to the required track.

### Rotational Latency

Time waiting for the required sector to rotate under the head.

### Transfer Time

Time required to transfer the data.

Conceptually:

```text
Disk Access Time
≈ Seek Time
 + Rotational Latency
 + Transfer Time
```

---

# 26. Disk Scheduling

When multiple disk I/O requests are waiting, the OS can choose the order in which requests are serviced.

This is called **disk scheduling**.

Main algorithms:

```text
FCFS
SSTF
SCAN
C-SCAN
```

---

# 27. FCFS Disk Scheduling

**FCFS (First-Come, First-Served)** services requests in the order they arrive.

Example:

```text
Requests:

98 → 183 → 37 → 122
```

The disk services them in exactly that order.

### Advantages

```text
Simple
Fair in arrival order
```

### Disadvantages

```text
Can cause large head movement
Poor average performance
```

---

# 28. SSTF Disk Scheduling

**SSTF (Shortest Seek Time First)** selects the request closest to the current disk-head position.

Example:

```text
Current head = 50

Requests:
20, 55, 90

Closest = 55
```

So:

```text
50 → 55
```

### Advantage

Usually reduces average seek time compared with FCFS.

### Disadvantage

A far-away request may wait for a long time, causing **starvation**.

---

# 29. SCAN Disk Scheduling

**SCAN** moves the disk head in one direction, servicing requests along the way, then reverses direction.

It is often called the **elevator algorithm**.

Example:

```text
→ → → → →
Service requests
       ↓
← ← ← ← ←
Service requests
```

The behavior resembles an elevator moving through floors.

---

# 30. C-SCAN Disk Scheduling

**C-SCAN (Circular SCAN)** services requests in one direction only.

When the head reaches the end:

```text
End
 ↓
Return to beginning
 ↓
Continue in same direction
```

Conceptually:

```text
→ → → → →
          ↓
          ↘
←──────────
   jump
→ → → → →
```

This can provide more uniform waiting times than SCAN for some workloads.

---

# 31. SCAN vs C-SCAN

| SCAN | C-SCAN |
|---|---|
| Services requests in both directions | Services requests in one direction |
| Reverses direction at an end | Returns to beginning and continues |
| Elevator-like movement | Circular movement |
| Waiting time can vary by position | More uniform waiting time in many cases |

---

# 32. Disk Scheduling Comparison

| Algorithm | Main Idea | Main Issue |
|---|---|---|
| FCFS | Arrival order | High head movement |
| SSTF | Closest request first | Possible starvation |
| SCAN | Move both directions | More movement than ideal in some cases |
| C-SCAN | One direction, then wrap around | Extra return movement |

---

# 33. Important: Disk Scheduling and SSDs

Traditional disk-scheduling algorithms are primarily designed around the mechanical movement of HDD heads.

For SSDs:

```text
No mechanical seek
No rotational latency
```

Therefore, the performance considerations are different, although I/O scheduling can still matter for system behavior.

---

# 34. What is Free Space Management?

The file system must keep track of unused disk blocks.

Common techniques include:

```text
Bitmaps / Bit vectors
Free lists
Grouping
Counting
```

For placement interviews, the most important concept is usually the **bitmap**.

---

# 35. Bitmap

A bitmap uses one bit or a small representation to indicate whether a block is free or allocated.

Example:

```text
Block:  0 1 2 3 4 5 6 7
Status: 1 0 1 1 0 0 1 0
```

Depending on the convention:

```text
1 → allocated
0 → free
```

or the reverse.

The convention depends on the implementation.

---

# 36. What is Disk Formatting?

Formatting prepares a storage medium or partition for use with a file system.

Two common concepts are:

```text
Low-level formatting
Logical/high-level formatting
```

Modern storage devices typically perform much of the low-level preparation during manufacturing, while users commonly perform logical formatting to create a file-system structure.

---

# 37. What is Mounting?

**Mounting** makes a file system accessible at a directory in the operating system's namespace.

Example:

```text
Storage Device
      ↓
File System
      ↓
Mount Point
      ↓
/mnt/data
```

After mounting, applications can access files through the mounted path.

---

# 38. What is a Mount Point?

A **mount point** is the directory where a file system is attached and made accessible.

Example:

```text
/mnt/data
```

The mounted file system becomes accessible through this directory.

---

# 39. Important Interview Scenario

### Question

A process wants to read a file. What happens conceptually?

### Answer

```text
Process
  ↓
System Call
  ↓
File Descriptor / Open File
  ↓
File System
  ↓
Storage I/O
  ↓
Data returned to process
```

The exact path can involve caches, device drivers, and other kernel components.

---

# 40. Important Interview Scenario

### Question

Why is SSTF better than FCFS in many cases?

### Answer

> SSTF chooses the request with the shortest seek distance from the current head position, so it often reduces total head movement and average seek time compared with FCFS.

However:

> SSTF can cause starvation for requests that remain far from the current head position.

---

# 41. Important Interview Scenario

### Question

Why is SCAN called the Elevator Algorithm?

### Answer

> Because the disk head moves in one direction while servicing requests, then reverses direction, similar to an elevator serving floors in both directions.

---

# 42. Important Interview Scenario

### Question

What is the difference between a hard link and a symbolic link?

### Answer

> A hard link refers to the same underlying inode as the original file, while a symbolic link refers to another path. A symbolic link can become dangling when its target is removed.

---

# 43. Important Interview Questions

Prepare these especially well:

```text
1. What is a file system?

2. What is a file?

3. What are file attributes?

4. What are basic file operations?

5. What is a directory?

6. What is an absolute path?

7. What is a relative path?

8. What are sequential, direct, and indexed file access methods?

9. What is file allocation?

10. What is contiguous allocation?

11. What is linked allocation?

12. What is indexed allocation?

13. Contiguous vs linked vs indexed allocation?

14. What is an inode?

15. What is a file descriptor?

16. Inode vs file descriptor?

17. What is a hard link?

18. What is a symbolic link?

19. Hard link vs symbolic link?

20. What is disk management?

21. What is the difference between HDD and SSD?

22. What is seek time?

23. What is rotational latency?

24. What is transfer time?

25. What is disk scheduling?

26. What is FCFS disk scheduling?

27. What is SSTF?

28. What is SCAN?

29. What is C-SCAN?

30. SCAN vs C-SCAN?

31. Which disk scheduling algorithm can cause starvation?

32. Why is SCAN called the elevator algorithm?

33. Why are traditional disk scheduling algorithms less relevant to SSDs?

34. What is free-space management?

35. What is a bitmap?

36. What is disk formatting?

37. What is mounting?

38. What is a mount point?

39. Solve a disk-scheduling numerical problem.
```

---

# 44. Quick Revision

```text
FILE SYSTEM
→ Organizes and manages files on storage

FILE
→ Named collection of data

DIRECTORY
→ Organizes files/directories

SEQUENTIAL ACCESS
→ Access in order

DIRECT ACCESS
→ Jump directly to a location

CONTIGUOUS ALLOCATION
→ File blocks stored together

LINKED ALLOCATION
→ Each block points to next block

INDEXED ALLOCATION
→ Index block stores pointers to file blocks

INODE
→ File metadata + data-location information

FILE DESCRIPTOR
→ Process-level handle for an open file/resource

HARD LINK
→ Another directory entry for same inode

SYMBOLIC LINK
→ Link to another path

HDD
→ Mechanical storage

SSD
→ Flash-based storage

SEEK TIME
→ Move head to required track

ROTATIONAL LATENCY
→ Wait for required sector

DISK SCHEDULING
→ Decide order of disk requests

FCFS
→ Arrival order

SSTF
→ Closest request first

SCAN
→ Move in both directions

C-SCAN
→ Move in one direction and wrap around

BITMAP
→ Tracks free/allocated blocks

MOUNTING
→ Makes file system accessible through a directory
```

---

# 45. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
File System
File Operations
Directories and Paths
File Allocation
Contiguous vs Linked vs Indexed Allocation
Inode
File Descriptor
Hard Link vs Symbolic Link
HDD vs SSD
Disk Scheduling
FCFS
SSTF
SCAN
C-SCAN
Seek Time
Rotational Latency
```

## ⭐⭐⭐ Good to Know

```text
Indexed Access
Free-Space Management
Bitmap
Mounting
Mount Point
Disk Formatting
```

> **For placement interviews, focus deeply on File Allocation → Inode → File Descriptor → Hard vs Symbolic Links → Disk Scheduling → FCFS/SSTF/SCAN/C-SCAN.** These are the highest-value topics in this file.