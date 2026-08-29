# CN Basics and Network Models

## 1. What is a Computer Network?

A **computer network** is a collection of interconnected devices that communicate and share data and resources with each other.

Examples:

```text
Computers
Servers
Mobile Phones
Printers
Routers
Switches
```

A network allows devices to:

```text
Exchange Data
Share Resources
Access the Internet
Communicate with Each Other
```

---

# 2. Why Do We Need Computer Networks?

Computer networks are used for:

```text
Data Sharing
Resource Sharing
Communication
Internet Access
Centralized Management
Remote Access
```

Example:

```text
Computer A ──┐
Computer B ──┼──→ Network ──→ Server
Computer C ──┘
```

---

# 3. Types of Networks

The commonly discussed network types are:

```text
PAN
LAN
MAN
WAN
```

---

## 3.1 PAN

**PAN (Personal Area Network)** is a small network around an individual.

Example:

```text
Phone
  ↕
Bluetooth
  ↕
Earbuds
```

Typical range is very small.

---

## 3.2 LAN

**LAN (Local Area Network)** connects devices within a limited geographical area.

Examples:

```text
Home
Office
School
Computer Lab
```

Example:

```text
PC ──┐
PC ──┼── Switch ── Router
PC ──┘
```

---

## 3.3 MAN

**MAN (Metropolitan Area Network)** covers a larger area than a LAN, typically across a city or metropolitan region.

---

## 3.4 WAN

**WAN (Wide Area Network)** covers a large geographical area such as multiple cities, regions, or countries.

Example:

```text
Office A ─────┐
              │
Office B ── WAN ── Office C
              │
Office D ─────┘
```

The **Internet** is the largest example of an interconnected global network.

---

# 4. LAN vs WAN

| LAN | WAN |
|---|---|
| Smaller geographical area | Large geographical area |
| Usually higher local speed | Often involves longer-distance links |
| Lower latency within the local network | Generally higher latency |
| Common in homes/offices | Connects geographically separated networks |

---

# 5. Network Topology

**Network topology** describes how devices and connections are arranged in a network.

Common topologies:

```text
Bus
Star
Ring
Mesh
Tree
```

---

# 6. Bus Topology

In a **bus topology**, multiple devices share a common communication backbone.

```text
PC ── PC ── PC ── PC
       │
   Shared Bus
```

### Advantages

```text
Simple
Less cabling
```

### Disadvantages

```text
Backbone failure can affect the network
More difficult to troubleshoot as the network grows
```

---

# 7. Star Topology

In a **star topology**, all devices connect to a central device such as a switch.

```text
        PC
         |
PC ─── Switch ─── PC
         |
        PC
```

### Advantages

```text
Easy to manage
Easy to troubleshoot
Failure of one device's cable usually affects only that device
```

### Disadvantage

```text
Failure of the central device can affect connected devices
```

**Star topology is very common in modern Ethernet LANs.**

---

# 8. Ring Topology

In a **ring topology**, each device is connected to neighboring devices, forming a ring.

```text
PC ── PC
|      |
PC ── PC
```

Data can travel around the ring depending on the protocol/design.

---

# 9. Mesh Topology

In a **mesh topology**, devices have multiple interconnections.

### Full Mesh

Every device connects directly to every other device.

```text
A ───── B
|\     /|
| \   / |
|  \ /  |
|  / \  |
| /   \ |
C ───── D
```

### Advantage

```text
High redundancy
```

### Disadvantage

```text
High cost
Large number of connections
```

---

# 10. Tree Topology

A **tree topology** organizes devices in a hierarchical structure.

```text
          Core
         /    \
       SW1    SW2
      /  \    /  \
    PC1 PC2 PC3 PC4
```

It can be viewed as a combination of hierarchical star-like networks.

---

# 11. What is a Network Protocol?

A **network protocol** is a set of rules that defines how devices communicate over a network.

Examples:

```text
TCP
UDP
IP
HTTP
HTTPS
DNS
DHCP
FTP
SMTP
```

Protocols define things such as:

```text
How data is formatted
How data is transmitted
How devices identify information
How errors are handled
```

---

# 12. What is the OSI Model?

The **OSI (Open Systems Interconnection) model** is a conceptual seven-layer model used to understand how network communication works.

The seven layers are:

```text
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
```

### Easy Memory Trick

```text
A
P
S
T
N
D
P
```

**"All People Seem To Need Data Processing"**

---

# 13. OSI Layers

| Layer | Name | Main Responsibility |
|---|---|---|
| 7 | Application | Network services used by applications |
| 6 | Presentation | Data representation, encryption, compression |
| 5 | Session | Establishes/manages sessions |
| 4 | Transport | End-to-end delivery, reliability, flow control |
| 3 | Network | Logical addressing and routing |
| 2 | Data Link | Frames, MAC addressing, local delivery |
| 1 | Physical | Transmission of raw bits |

---

# 14. Physical Layer

The **Physical Layer** is responsible for transmitting raw bits over the physical medium.

It deals with:

```text
Bits
Cables
Signals
Connectors
Radio transmission
Physical interfaces
```

Data unit:

```text
Bits
```

---

# 15. Data Link Layer

The **Data Link Layer** provides communication between devices on the same local network/link.

Important concepts:

```text
Frames
MAC Addresses
Ethernet
Error Detection
Media Access Control
```

Data unit:

```text
Frame
```

A common device associated with this layer is:

```text
Switch
```

---

# 16. Network Layer

The **Network Layer** handles logical addressing and routing between networks.

Important concepts:

```text
IP Address
Routing
Packets
Routers
```

Data unit:

```text
Packet
```

Main protocol:

```text
IP
```

---

# 17. Transport Layer

The **Transport Layer** provides end-to-end communication between applications/processes.

Important concepts:

```text
TCP
UDP
Ports
Reliability
Flow Control
Congestion Control
Segmentation
```

Data units are commonly described as:

```text
TCP → Segment
UDP → Datagram
```

---

# 18. Session Layer

The **Session Layer** is responsible for establishing, managing, and terminating communication sessions between applications.

In modern TCP/IP implementations, session-related functions are often handled by application protocols and libraries rather than as a separate layer.

---

# 19. Presentation Layer

The **Presentation Layer** deals with how data is represented.

Commonly associated concepts include:

```text
Data Translation
Encryption/Decryption
Compression/Decompression
Character Encoding
```

Like the Session Layer, these responsibilities are often implemented within application-layer protocols/software in modern TCP/IP systems.

---

# 20. Application Layer

The **Application Layer** provides network services used directly by applications.

Examples:

```text
HTTP
HTTPS
DNS
FTP
SMTP
SSH
```

Important point:

> The Application Layer is not the application itself. It provides network protocols/services used by applications.

---

# 21. OSI Layer Data Units

A commonly used representation is:

```text
Application   → Data
Presentation  → Data
Session       → Data
Transport     → Segment / Datagram
Network       → Packet
Data Link     → Frame
Physical      → Bits
```

---

# 22. What is Encapsulation?

**Encapsulation** is the process of adding protocol information as data moves down the network layers before transmission.

Example:

```text
Application Data
      ↓
Transport Header + Data
      ↓
Network Header + Segment
      ↓
Data Link Header + Packet + Trailer
      ↓
Bits
```

Conceptually:

```text
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Bits
```

---

# 23. What is Decapsulation?

**Decapsulation** is the reverse process.

At the receiving device:

```text
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Application Data
```

Each layer processes and removes the information associated with its protocol.

---

# 24. What is the TCP/IP Model?

The **TCP/IP model** is the practical networking model associated with the Internet protocol suite.

A commonly used four-layer representation is:

```text
Application
Transport
Internet
Network Access
```

---

# 25. TCP/IP Layers

| TCP/IP Layer | Examples / Responsibilities |
|---|---|
| Application | HTTP, DNS, DHCP, SMTP, SSH |
| Transport | TCP, UDP |
| Internet | IP, ICMP |
| Network Access | Ethernet, Wi-Fi |

Some textbooks use a **five-layer Internet model** by separating the Link and Physical layers.

---

# 26. OSI vs TCP/IP

| OSI | TCP/IP |
|---|---|
| 7 layers | Commonly represented as 4 layers |
| Conceptual/reference model | Practical protocol suite/model |
| Session and Presentation are separate | Usually included in Application |
| Data Link and Physical are separate | Commonly combined as Network Access |

### Easy Mapping

```text
OSI                     TCP/IP

Application ───────┐
Presentation ──────┤
Session ───────────┤ → Application
Transport ───────────→ Transport
Network ─────────────→ Internet
Data Link ─────────┐
Physical ──────────┘ → Network Access
```

---

# 27. OSI Model vs TCP/IP Model — Interview Answer

> OSI is a seven-layer reference model used mainly to understand and standardize networking concepts, while TCP/IP represents the practical protocol architecture used by the Internet. OSI has separate Presentation and Session layers, whereas TCP/IP generally combines their responsibilities into the Application layer.

---

# 28. What is Bandwidth?

**Bandwidth** is the maximum rate at which a communication link can theoretically transmit data.

It is commonly measured in:

```text
bps
Kbps
Mbps
Gbps
```

Example:

```text
Bandwidth = 100 Mbps
```

This does **not** necessarily mean applications will always achieve 100 Mbps.

---

# 29. What is Latency?

**Latency** is the time taken for data to travel from one point to another.

It is commonly measured in:

```text
milliseconds (ms)
```

Example:

```text
Low latency → Faster response
High latency → More delay
```

---

# 30. Bandwidth vs Latency

| Bandwidth | Latency |
|---|---|
| Data-carrying capacity/rate | Delay |
| Measured in bits per second | Usually measured in time |
| Higher bandwidth can increase potential throughput | Lower latency improves responsiveness |

### Simple Example

Think of a road:

```text
Bandwidth → Number of vehicles the road can carry
Latency   → Time taken for one vehicle to reach destination
```

---

# 31. What is Throughput?

**Throughput** is the actual rate at which data is successfully transferred over a network.

```text
Bandwidth
→ Maximum theoretical capacity

Throughput
→ Actual achieved data rate
```

Throughput can be lower than bandwidth because of:

```text
Network congestion
Protocol overhead
Packet loss
Latency
Hardware limitations
```

---

# 32. Bandwidth vs Throughput

```text
Bandwidth
→ Maximum possible capacity

Throughput
→ Actual data transfer rate
```

Example:

```text
Link bandwidth = 100 Mbps
Actual throughput = 75 Mbps
```

---

# 33. What is a Packet?

A **packet** is a unit of data used at the network layer.

A packet generally contains:

```text
Header
Payload
```

The header contains information needed for network-layer delivery, such as source and destination IP addresses.

---

# 34. What is a Frame?

A **frame** is the data-link-layer unit used for transmission over a local link.

Conceptually:

```text
Frame
├── Header
├── Packet/Data
└── Trailer
```

Ethernet frames, for example, contain source and destination MAC addresses.

---

# 35. Packet vs Frame

| Packet | Frame |
|---|---|
| Network Layer | Data Link Layer |
| Contains IP addressing information | Contains MAC addressing information |
| Used for routing between networks | Used for local-link delivery |

---

# 36. What is a Port?

A **port number** identifies a communication endpoint associated with a process/service at the transport layer.

Examples:

```text
HTTP  → 80
HTTPS → 443
DNS   → 53
SSH   → 22
```

Ports help the OS deliver received transport-layer data to the appropriate application/process.

---

# 37. What is a Socket?

A **socket** is an endpoint used by applications for network communication.

Conceptually, a network connection can be identified using information such as:

```text
IP Address
Port
Protocol
```

Example:

```text
192.168.1.10 : 5000
```

---

# 38. Important Network Devices

### Hub

A **hub** sends incoming data to all connected ports.

```text
PC1 ──┐
PC2 ──┼── Hub
PC3 ──┘

Data from PC1
↓
PC2 + PC3 + ...
```

Hubs are largely obsolete in modern switched Ethernet networks.

---

### Switch

A **switch** forwards Ethernet frames based on MAC addresses.

```text
PC1 ──┐
PC2 ──┼── Switch
PC3 ──┘
```

A switch can learn which MAC address is reachable through which port.

---

### Router

A **router** forwards packets between different IP networks using routing information.

```text
LAN 1
  ↓
Router
  ↓
LAN 2
```

---

# 39. Hub vs Switch vs Router

| Hub | Switch | Router |
|---|---|---|
| Broadcasts incoming data to ports | Forwards frames based on MAC addresses | Routes packets between IP networks |
| Layer 1 | Mainly Layer 2 | Layer 3 |
| No MAC-learning forwarding table | Uses MAC address table | Uses routing table |
| Largely obsolete | Common in LANs | Connects different networks |

---

# 40. What is a MAC Address?

A **MAC (Media Access Control) address** is a link-layer address used to identify a network interface on a local network.

Example format:

```text
00:1A:2B:3C:4D:5E
```

It is used for local-link communication.

---

# 41. MAC Address vs IP Address

| MAC Address | IP Address |
|---|---|
| Link-layer address | Network-layer address |
| Used for local-link delivery | Used for communication/routing across networks |
| Associated with network interface | Assigned/configured for network connectivity |
| Ethernet commonly uses MAC addresses | IP networks use IP addresses |

### Easy Way to Remember

```text
MAC → Local network delivery
IP  → Network-to-network routing
```

---

# 42. What is a Client-Server Model?

In the **client-server model**, a client requests a service and a server provides it.

```text
Client
   ↓ Request
Server
   ↓ Response
Client
```

Example:

```text
Browser → Web Server
```

---

# 43. What is Peer-to-Peer (P2P)?

In a **peer-to-peer network**, devices can act as both clients and servers and communicate directly with one another.

```text
Peer A ↔ Peer B
   ↕       ↕
Peer C ↔ Peer D
```

---

# 44. Client-Server vs P2P

| Client-Server | P2P |
|---|---|
| Central server provides services | Peers can provide services to each other |
| Easier centralized management | More distributed |
| Server can become a bottleneck/single point of dependency | No single central server is necessarily required |

---

# 45. Most Important Interview Questions

Prepare these questions especially well:

```text
1. What is a computer network?

2. Why do we need computer networks?

3. What are PAN, LAN, MAN, and WAN?

4. LAN vs WAN?

5. What is network topology?

6. Explain Bus topology.

7. Explain Star topology.

8. Explain Ring topology.

9. Explain Mesh topology.

10. Which topology is commonly used in modern LANs?

11. What is a network protocol?

12. What is the OSI model?

13. Explain all 7 layers of OSI.

14. What is the function of the Physical Layer?

15. What is the function of the Data Link Layer?

16. What is the function of the Network Layer?

17. What is the function of the Transport Layer?

18. What is the function of the Session Layer?

19. What is the function of the Presentation Layer?

20. What is the function of the Application Layer?

21. What are the data units at different OSI layers?

22. What is encapsulation?

23. What is decapsulation?

24. What is the TCP/IP model?

25. Explain TCP/IP layers.

26. OSI vs TCP/IP?

27. What is bandwidth?

28. What is latency?

29. What is throughput?

30. Bandwidth vs throughput?

31. Bandwidth vs latency?

32. What is a packet?

33. What is a frame?

34. Packet vs frame?

35. What is a port?

36. What is a socket?

37. What is a hub?

38. What is a switch?

39. What is a router?

40. Hub vs switch vs router?

41. What is a MAC address?

42. MAC address vs IP address?

43. What is client-server architecture?

44. What is peer-to-peer networking?

45. Client-server vs P2P?
```

---

# 46. Most Important OSI Layers for Interviews

If the interviewer asks you to explain the OSI model, remember this:

```text
7. Application
   → HTTP, DNS, FTP, SMTP

6. Presentation
   → Translation, Encryption, Compression

5. Session
   → Session Management

4. Transport
   → TCP, UDP, Ports, Reliability

3. Network
   → IP, Routing, Packets

2. Data Link
   → MAC, Frames, Ethernet, Switches

1. Physical
   → Bits, Signals, Cables
```

### Easy Memory Trick

```text
All People Seem To Need Data Processing
```

```text
A → Application
P → Presentation
S → Session
T → Transport
N → Network
D → Data Link
P → Physical
```

---

# 47. Quick Revision

```text
NETWORK
→ Connected devices communicating with each other

PAN
→ Personal area

LAN
→ Local area

MAN
→ Metropolitan/city area

WAN
→ Wide geographical area

PROTOCOL
→ Rules for communication

OSI
→ 7-layer reference model

TCP/IP
→ Practical Internet protocol architecture

PHYSICAL
→ Bits/signals

DATA LINK
→ Frames/MAC

NETWORK
→ Packets/IP/routing

TRANSPORT
→ TCP/UDP/ports

APPLICATION
→ HTTP/DNS/FTP/etc.

ENCAPSULATION
→ Headers/trailers added while moving down layers

DECAPSULATION
→ Headers/trailers processed/removed while moving up layers

BANDWIDTH
→ Maximum capacity

LATENCY
→ Delay

THROUGHPUT
→ Actual achieved data rate

PACKET
→ Network-layer data unit

FRAME
→ Data-link-layer data unit

HUB
→ Broadcasts data to connected ports

SWITCH
→ Forwards frames using MAC addresses

ROUTER
→ Routes packets between IP networks

MAC
→ Link-layer address

IP
→ Network-layer address

PORT
→ Identifies transport-layer application endpoint

SOCKET
→ Network communication endpoint

CLIENT-SERVER
→ Client requests, server provides

P2P
→ Peers communicate/provide services to each other
```

---

# 48. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
OSI Model
All 7 OSI Layers
OSI vs TCP/IP
TCP/IP Model
Encapsulation and Decapsulation
TCP/IP Data Units
Bandwidth vs Latency vs Throughput
Packet vs Frame
MAC Address vs IP Address
Hub vs Switch vs Router
Port
Socket
LAN vs WAN
```

## ⭐⭐⭐ Good to Know

```text
PAN / MAN
Network Topologies
Client-Server vs P2P
Session Layer
Presentation Layer
```

> **For placement interviews, focus deeply on the OSI model, TCP/IP model, layer responsibilities, encapsulation, bandwidth/latency/throughput, packet vs frame, MAC vs IP, and Hub vs Switch vs Router. These concepts form the foundation for the remaining Computer Networks topics.**