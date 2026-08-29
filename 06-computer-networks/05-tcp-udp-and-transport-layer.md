# TCP, UDP and Transport Layer

## 1. What is the Transport Layer?

The **Transport Layer** is Layer 4 of the OSI model.

It provides **end-to-end communication between applications/processes** running on different devices.

Main concepts:

```text
TCP
UDP
Port Numbers
Segmentation
Reliability
Flow Control
Congestion Control
Connection Management
```

Data units:

```text
TCP → Segment
UDP → Datagram
```

---

# 2. Main Functions of the Transport Layer

The Transport Layer is responsible for:

```text
Process-to-process communication
Port addressing
Segmentation and reassembly
Reliability
Flow control
Congestion control
Connection management
Error detection
```

Not every transport protocol provides all of these features.

---

# 3. Host-to-Host vs Process-to-Process Communication

The Network Layer mainly handles:

```text
Host-to-host delivery
```

The Transport Layer handles:

```text
Process-to-process delivery
```

Example:

```text
Computer A
   ↓
Network Layer
   ↓
Computer B
   ↓
Transport Layer
   ↓
Correct application/process
```

The Transport Layer uses **port numbers** to identify the destination application/process.

---

# 4. What is a Port Number?

A **port number** identifies a transport-layer communication endpoint associated with an application or service.

Port numbers are:

```text
16 bits
```

Therefore, the range is:

```text
0 to 65535
```

Examples:

```text
HTTP  → 80
HTTPS → 443
SSH   → 22
DNS   → 53
FTP   → 21
```

---

# 5. Port Number Ranges

Port numbers are commonly divided into:

```text
0–1023
→ Well-known ports

1024–49151
→ Registered ports

49152–65535
→ Dynamic / Private ports
```

The exact use of a port depends on the application and operating system.

---

# 6. What is a Socket?

A **socket** is a communication endpoint used by an application for network communication.

A socket is commonly associated with:

```text
IP Address
Port Number
Transport Protocol
```

Example:

```text
192.168.1.10 : 5000
```

Conceptually:

```text
IP Address → Which host?
Port       → Which application/process?
```

---

# 7. TCP

**TCP (Transmission Control Protocol)** is a connection-oriented and reliable transport protocol.

TCP provides mechanisms for:

```text
Reliable delivery
Ordered delivery
Error detection
Flow control
Congestion control
Retransmission
Connection management
```

TCP is commonly used when reliable, ordered delivery is important.

Examples:

```text
HTTP/HTTPS
SSH
FTP
```

---

# 8. UDP

**UDP (User Datagram Protocol)** is a connectionless transport protocol.

UDP provides:

```text
Port-based multiplexing
Checksum-based error detection
Datagram delivery
```

It does **not** provide TCP-style:

```text
Reliable delivery
Ordered delivery
Retransmission
Connection establishment
Flow control
Congestion control
```

UDP is useful when low overhead and application-controlled behavior are preferred.

Examples include:

```text
DNS
DHCP
Streaming/real-time applications
Online gaming
VoIP
```

The exact protocol used by an application depends on its design.

---

# 9. TCP vs UDP

This is one of the **most important Computer Networks interview questions**.

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable delivery | No TCP-style reliability guarantee |
| Ordered delivery | No ordering guarantee |
| Retransmission | No built-in retransmission |
| Flow control | No TCP-style flow control |
| Congestion control | No TCP-style congestion control |
| More protocol overhead | Lower overhead |
| Stream-oriented | Datagram-oriented |

### Easy Memory Trick

```text
TCP
→ Reliable + Ordered

UDP
→ Simple + Low Overhead
```

---

# 10. Why is TCP Reliable?

TCP provides reliability using mechanisms such as:

```text
Sequence Numbers
Acknowledgments
Retransmissions
Checksum
```

Example:

```text
Sender
  |
  | Segment 1
  ↓
Receiver
  |
  | ACK
  ↓
Sender
```

If data is lost:

```text
Segment
   ↓
Lost
   ↓
No appropriate ACK
   ↓
Retransmission
```

---

# 11. What is a Sequence Number?

A **sequence number** helps TCP identify the position of bytes in the data stream.

It helps TCP:

```text
Maintain ordering
Detect missing data
Identify duplicate data
Support retransmission
```

Example concept:

```text
Data:
A B C D E

Sequence information
↓
A → position
B → position
C → position
...
```

TCP sequence numbers are based on **bytes**, not simply packet/segment numbers.

---

# 12. What is an Acknowledgment?

An **ACK (Acknowledgment)** tells the sender what data has been received/what byte is expected next.

Conceptually:

```text
Sender
  |
  | Data
  ↓
Receiver
  |
  | ACK
  ↓
Sender
```

TCP acknowledgments are generally **cumulative**.

For example, an ACK value can indicate:

```text
"I have received everything up to this point and expect this next byte."
```

---

# 13. What is Retransmission?

If TCP determines that data was lost, it can retransmit the missing data.

Loss can be inferred through mechanisms such as:

```text
Timeout
Duplicate ACK patterns
```

Conceptually:

```text
Sender
  |
  | Segment
  X
  | Lost
  |
  | Retransmit
  ↓
Receiver
```

---

# 14. What is TCP Connection?

TCP is **connection-oriented**.

Before normal application data is exchanged, TCP establishes a connection between the endpoints.

The standard connection establishment process uses the:

```text
Three-Way Handshake
```

---

# 15. TCP Three-Way Handshake

The three messages are:

```text
SYN
SYN-ACK
ACK
```

Example:

```text
Client                         Server

   | -------- SYN ----------> |
   |                          |
   | <------ SYN + ACK ------- |
   |                          |
   | -------- ACK ----------> |
   |                          |
        Connection Established
```

---

# 16. What is SYN?

**SYN** is a TCP flag used to initiate a connection and synchronize sequence-number state.

```text
Client
  |
  | SYN
  ↓
Server
```

---

# 17. What is SYN-ACK?

The server responds with:

```text
SYN + ACK
```

This indicates that the server:

```text
Acknowledges the client's SYN
+
Requests synchronization in the reverse direction
```

---

# 18. What is the Final ACK?

The client sends:

```text
ACK
```

This completes the standard three-way handshake.

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

Then application data can be exchanged.

---

# 19. Why Does TCP Need a Three-Way Handshake?

The handshake allows both sides to:

```text
Establish connection state
Synchronize sequence numbers
Confirm that both directions are reachable
```

### Interview Answer

> TCP uses a three-way handshake to establish connection state and synchronize sequence numbers between the two endpoints before normal data transfer.

---

# 20. TCP Connection Termination

TCP commonly uses a **four-segment exchange** to close a connection gracefully.

Typical flow:

```text
Client                         Server

   | -------- FIN -----------> |
   | <--------- ACK ---------- |
   | <--------- FIN ---------- |
   | -------- ACK -----------> |
```

This allows each direction of the TCP connection to be closed independently.

---

# 21. What is FIN?

**FIN** is a TCP flag used to indicate that a side has finished sending data.

Example:

```text
Client
  |
  | FIN
  ↓
Server
```

---

# 22. TCP Flags

Important TCP flags include:

```text
SYN
ACK
FIN
RST
PSH
URG
```

For placement interviews, focus mainly on:

```text
SYN
ACK
FIN
RST
```

---

# 23. What is RST?

**RST (Reset)** is used to immediately terminate/reset a TCP connection or reject an invalid/unexpected connection attempt.

Example situations can include:

```text
Connection to a closed port
Invalid connection state
Abrupt termination
```

---

# 24. TCP Header

A simplified TCP segment looks like:

```text
┌──────────────────────────────────┐
│ Source Port | Destination Port  │
├──────────────────────────────────┤
│ Sequence Number                  │
├──────────────────────────────────┤
│ Acknowledgment Number            │
├──────────────────────────────────┤
│ Flags | Window Size              │
├──────────────────────────────────┤
│ Checksum | Urgent Pointer        │
├──────────────────────────────────┤
│ Options                          │
├──────────────────────────────────┤
│ Data                             │
└──────────────────────────────────┘
```

Important fields:

```text
Source Port
Destination Port
Sequence Number
Acknowledgment Number
Flags
Window Size
Checksum
```

---

# 25. What is TCP Window Size?

TCP uses a **receive window** to implement flow control.

It tells the sender approximately how much additional data the receiver is currently prepared to accept without overflowing its receive buffer.

Conceptually:

```text
Fast Sender
     ↓
Receive Window
     ↓
Receiver
```

---

# 26. What is Flow Control?

**Flow control** prevents a sender from overwhelming the receiver.

Example:

```text
Sender → Very Fast
Receiver → Slower
```

Without flow control:

```text
Receiver Buffer
████████████████
     Overflow
```

TCP uses the receiver's advertised window to regulate how much unacknowledged data can be in flight.

---

# 27. What is Congestion Control?

**Congestion control** prevents the sender from overwhelming the **network**.

Important difference:

```text
Flow Control
→ Protects receiver

Congestion Control
→ Protects network
```

---

# 28. Flow Control vs Congestion Control

| Flow Control | Congestion Control |
|---|---|
| Protects receiver | Helps prevent network overload |
| Based on receiver capacity | Based on network conditions |
| Uses receive window | Uses congestion-control mechanisms |
| Receiver-oriented | Network-oriented |

### Easy Memory Trick

```text
Flow Control
→ "Can the receiver handle this?"

Congestion Control
→ "Can the network handle this?"
```

---

# 29. TCP Congestion Control

TCP dynamically adjusts its sending behavior based on network conditions.

Important concepts include:

```text
Congestion Window (cwnd)
Slow Start
Congestion Avoidance
Fast Retransmit
Fast Recovery
```

Different TCP implementations use different congestion-control algorithms.

For placement interviews, understand the concepts rather than memorizing every implementation.

---

# 30. What is Congestion Window?

The **congestion window (`cwnd`)** limits how much data TCP can have in flight based on its estimate of network capacity/congestion.

Conceptually:

```text
Sending Rate
     ↑
     |
   cwnd
     |
Network
```

The sender's effective amount of in-flight data is influenced by both:

```text
cwnd
+
Receiver's advertised window
```

---

# 31. What is Slow Start?

Despite its name, TCP **Slow Start** can increase the congestion window rapidly at the beginning of a connection.

Conceptually:

```text
cwnd
 ↑
 |       *
 |     *
 |   *
 | *
 +----------------→ Time
```

The goal is to discover available network capacity without immediately sending an excessive amount of traffic.

---

# 32. What is Congestion Avoidance?

After the congestion window reaches an appropriate threshold, TCP generally transitions to a more conservative growth phase.

Conceptually:

```text
Slow Start
     ↓
Congestion Avoidance
```

The exact behavior depends on the TCP congestion-control algorithm.

---

# 33. What is UDP Header?

UDP has a very small header.

```text
┌──────────────────────────────────┐
│ Source Port | Destination Port  │
├──────────────────────────────────┤
│ Length       | Checksum          │
├──────────────────────────────────┤
│ Data                             │
└──────────────────────────────────┘
```

UDP header size:

```text
8 bytes
```

Important fields:

```text
Source Port
Destination Port
Length
Checksum
```

---

# 34. TCP Header Size

The TCP header has:

```text
Minimum → 20 bytes
```

It can be larger when options are included.

This is one reason TCP has more overhead than UDP.

---

# 35. TCP vs UDP Header Size

```text
TCP
→ Minimum 20 bytes

UDP
→ 8 bytes
```

Therefore:

```text
UDP → Lower header overhead
TCP → More control information
```

---

# 36. Does UDP Have Error Detection?

Yes.

UDP has a:

```text
Checksum
```

which provides error detection.

However, UDP does not provide TCP-style:

```text
Retransmission
Ordering
Reliability
Flow control
Congestion control
```

---

# 37. Is UDP Faster Than TCP?

A better interview answer is:

> UDP generally has lower protocol overhead and does not require TCP's connection establishment, reliability, retransmission, and ordering mechanisms. Therefore, applications using UDP can have lower overhead and latency in suitable situations. It is not correct to say that UDP is always faster than TCP.

---

# 38. When Should TCP Be Used?

TCP is appropriate when the application requires:

```text
Reliable delivery
Ordered data
Retransmission
Connection-oriented communication
```

Examples:

```text
Web traffic
SSH
File transfer
Email protocols
```

---

# 39. When Should UDP Be Used?

UDP can be appropriate when:

```text
Low overhead is important
Timeliness is more important than retransmission
The application can handle loss/reordering itself
Connection setup should be avoided
```

Examples:

```text
DNS
DHCP
Real-time applications
Online gaming
VoIP
```

---

# 40. TCP and UDP Are Both Transport Protocols

Both operate at:

```text
OSI Layer 4
```

Conceptually:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Data Link
     ↓
Physical
```

---

# 41. Multiplexing and Demultiplexing

The Transport Layer allows multiple applications to communicate simultaneously using port numbers.

Example:

```text
Browser ───── Port 50001 ──┐
SSH ───────── Port 50002 ──┼── Network
DNS Client ── Port 50003 ──┘
```

At the receiver:

```text
Incoming Segment
       ↓
Destination Port
       ↓
Correct Application
```

This is called:

```text
Multiplexing / Demultiplexing
```

---

# 42. TCP Connection Identification

A TCP connection is commonly identified by a combination of:

```text
Source IP
Source Port
Destination IP
Destination Port
```

This is commonly called the:

```text
4-tuple
```

Example:

```text
192.168.1.10 : 50000
        ↓
93.184.216.34 : 443
```

The transport protocol is TCP.

---

# 43. What is a TCP Connection?

A TCP connection is a logical communication relationship between two endpoints.

Example:

```text
Client
192.168.1.10:50000
       |
       | TCP
       |
Server
93.184.216.34:443
```

TCP maintains state for this communication.

---

# 44. What is Connection-Oriented Communication?

Connection-oriented communication establishes state before normal data transfer.

TCP:

```text
Connection establishment
        ↓
Data transfer
        ↓
Connection termination
```

UDP:

```text
No TCP-style connection establishment
        ↓
Datagrams can be sent
```

---

# 45. What is Connectionless Communication?

A connectionless protocol sends independent datagrams without establishing a TCP-style connection first.

UDP is:

```text
Connectionless
```

Example:

```text
Sender
  |
  | Datagram
  ↓
Receiver
```

---

# 46. Important Interview Questions

```text
1. What is the Transport Layer?

2. What are the main functions of the Transport Layer?

3. TCP vs UDP?

4. What is TCP?

5. What is UDP?

6. Why is TCP reliable?

7. Why is UDP called connectionless?

8. What is a port number?

9. What is the range of port numbers?

10. What is a socket?

11. What is process-to-process communication?

12. What is multiplexing and demultiplexing?

13. What is a TCP segment?

14. What is a UDP datagram?

15. What is the TCP three-way handshake?

16. Explain SYN, SYN-ACK, and ACK.

17. Why does TCP use a three-way handshake?

18. What is TCP connection termination?

19. Why does TCP commonly use four segments for graceful termination?

20. What is FIN?

21. What is RST?

22. What is a sequence number?

23. What is an acknowledgment number?

24. How does TCP provide reliability?

25. What is retransmission?

26. What is flow control?

27. What is congestion control?

28. Flow control vs congestion control?

29. What is a receive window?

30. What is congestion window?

31. What is TCP Slow Start?

32. What is Congestion Avoidance?

33. What is the TCP header?

34. What is the UDP header?

35. What is the minimum TCP header size?

36. What is the UDP header size?

37. Why does UDP have lower overhead than TCP?

38. Does UDP provide error detection?

39. Is UDP always faster than TCP?

40. When should TCP be used?

41. When should UDP be used?

42. What is the TCP 4-tuple?

43. What is connection-oriented communication?

44. What is connectionless communication?
```

---

# 47. Most Important Comparisons

## TCP vs UDP

```text
TCP
→ Connection-oriented
→ Reliable
→ Ordered
→ Retransmission
→ Flow control
→ Congestion control
→ More overhead

UDP
→ Connectionless
→ No TCP-style reliability
→ No ordering guarantee
→ No retransmission
→ No TCP-style flow control
→ No TCP-style congestion control
→ Lower overhead
```

---

## Flow Control vs Congestion Control

```text
Flow Control
→ Protects receiver

Congestion Control
→ Helps protect network
```

---

## TCP vs IP

```text
TCP
→ Transport Layer
→ Process-to-process communication
→ Reliability and ordering

IP
→ Network Layer
→ Host/network addressing
→ Routing and packet delivery
```

---

## Port vs IP Address

```text
IP Address
→ Identifies network-layer destination/interface

Port
→ Identifies transport-layer application endpoint
```

Think:

```text
IP   → Which machine/network?
Port → Which application?
```

---

## TCP Segment vs UDP Datagram

```text
TCP
→ Segment
→ Reliable, ordered byte stream

UDP
→ Datagram
→ Independent message-oriented delivery
```

---

# 48. Quick Revision

```text
TRANSPORT LAYER
→ Layer 4
→ Process-to-process communication

TCP
→ Connection-oriented
→ Reliable
→ Ordered
→ Retransmission
→ Flow control
→ Congestion control

UDP
→ Connectionless
→ Lower overhead
→ No TCP-style reliability
→ No ordering guarantee

PORT
→ Identifies application/process endpoint
→ 0–65535

SOCKET
→ Communication endpoint

TCP HANDSHAKE
→ SYN
→ SYN-ACK
→ ACK

TCP TERMINATION
→ FIN
→ ACK
→ FIN
→ ACK

SEQUENCE NUMBER
→ Tracks byte positions

ACK
→ Indicates received data / next expected byte

FLOW CONTROL
→ Protects receiver

CONGESTION CONTROL
→ Helps prevent network overload

RECEIVE WINDOW
→ Receiver capacity advertised to sender

CONGESTION WINDOW
→ Sender's congestion-controlled in-flight limit

TCP HEADER
→ Minimum 20 bytes

UDP HEADER
→ 8 bytes

MULTIPLEXING
→ Multiple applications use network simultaneously

DEMULTIPLEXING
→ Incoming data delivered to correct application

TCP 4-TUPLE
→ Source IP
→ Source Port
→ Destination IP
→ Destination Port
```

---

# 49. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Transport Layer
TCP vs UDP
TCP Reliability
TCP Three-Way Handshake
SYN / SYN-ACK / ACK
TCP Connection Termination
FIN / RST
Sequence Numbers
Acknowledgments
Retransmission
Flow Control
Congestion Control
TCP vs UDP Header
Ports
Sockets
Multiplexing / Demultiplexing
```

## ⭐⭐⭐ Good to Know

```text
TCP Congestion Window
Slow Start
Congestion Avoidance
TCP 4-Tuple
TCP Header Fields
UDP Header Fields
Connection-Oriented vs Connectionless
```

> **For placement interviews, focus deeply on TCP vs UDP, the three-way handshake, TCP reliability, sequence numbers, ACKs, retransmission, flow control vs congestion control, ports, sockets, and connection termination. These are the highest-value Transport Layer concepts.**