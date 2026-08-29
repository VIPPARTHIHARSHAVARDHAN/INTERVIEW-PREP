# Physical and Data Link Layer

## 1. What is the Physical Layer?

The **Physical Layer** is the first layer of the OSI model.

It is responsible for transmitting raw bits over a physical communication medium.

```text
Physical Layer
      ↓
     Bits
      ↓
Signals / Medium
```

It deals with:

```text
Bits
Electrical signals
Optical signals
Radio signals
Cables
Connectors
Physical interfaces
Transmission media
```

---

# 2. What is the Data Link Layer?

The **Data Link Layer** is the second layer of the OSI model.

It is responsible for reliable communication over a **single local link/network segment**.

Main responsibilities include:

```text
Framing
MAC Addressing
Error Detection
Media Access Control
Local delivery
```

Data unit:

```text
Frame
```

---

# 3. Physical Layer vs Data Link Layer

| Physical Layer | Data Link Layer |
|---|---|
| Layer 1 | Layer 2 |
| Transmits raw bits | Transmits frames |
| Deals with signals and physical media | Deals with local-link communication |
| No frame-level addressing | Uses MAC addresses |
| Cables, radio, connectors | Ethernet, MAC, framing, error detection |

---

# 4. What is a Bit?

A **bit** is the basic unit of digital data.

It can have two logical values:

```text
0
1
```

At the Physical Layer, these bits are represented and transmitted using physical signals.

---

# 5. Transmission Media

Transmission media are the paths through which signals travel.

They are broadly divided into:

```text
Wired
Wireless
```

---

## 5.1 Wired Media

Examples:

```text
Twisted Pair Cable
Coaxial Cable
Fiber Optic Cable
```

---

## 5.2 Wireless Media

Examples:

```text
Wi-Fi
Radio
Microwave
Infrared
```

---

# 6. Twisted Pair Cable

Twisted-pair cables contain pairs of insulated copper wires twisted together.

Common types:

```text
UTP → Unshielded Twisted Pair
STP → Shielded Twisted Pair
```

Used commonly in:

```text
Ethernet LANs
```

---

# 7. Fiber Optic Cable

Fiber optic cables transmit data using light through optical fiber.

### Advantages

```text
Very high bandwidth
Long-distance transmission
Low electromagnetic interference
```

### Disadvantages

```text
More expensive/complex installation
More delicate than ordinary copper cabling
```

---

# 8. Wireless Transmission

Wireless communication transmits signals without a physical cable.

Examples:

```text
Wi-Fi
Bluetooth
Cellular Networks
Microwave Links
```

---

# 9. What is a Frame?

A **frame** is the data unit of the Data Link Layer.

Conceptually:

```text
┌────────┬──────────────┬─────────┐
│ Header │ Data/Payload │ Trailer │
└────────┴──────────────┴─────────┘
```

A frame can contain information such as:

```text
Source MAC Address
Destination MAC Address
Payload
Error-detection information
```

The exact structure depends on the link-layer protocol.

---

# 10. What is Framing?

**Framing** is the process of dividing a stream of data into manageable units called frames.

Example:

```text
Continuous Data
       ↓
┌───────┐ ┌───────┐ ┌───────┐
│Frame 1│ │Frame 2│ │Frame 3│
└───────┘ └───────┘ └───────┘
```

Framing allows the receiver to identify the boundaries of individual data-link-layer units.

---

# 11. What is a MAC Address?

**MAC (Media Access Control) address** is a link-layer address associated with a network interface.

A commonly seen Ethernet MAC address is written as:

```text
00:1A:2B:3C:4D:5E
```

MAC addresses are used for communication on the local network/link.

---

# 12. MAC Address vs IP Address

| MAC Address | IP Address |
|---|---|
| Data Link Layer | Network Layer |
| Used for local-link delivery | Used for communication across networks |
| Associated with network interface | Used as a logical network address |
| Used in frames | Used in packets |

### Easy Memory Trick

```text
MAC → Local delivery
IP  → Network-to-network delivery
```

---

# 13. What is Ethernet?

**Ethernet** is a widely used family of technologies for wired local-area networking.

It defines things such as:

```text
Frame format
MAC addressing
Physical transmission characteristics
Link operation
```

Ethernet commonly operates across:

```text
Physical Layer
Data Link Layer
```

---

# 14. What is a Switch?

A **network switch** connects devices within a LAN and forwards Ethernet frames based primarily on MAC addresses.

Example:

```text
PC1 ──┐
PC2 ──┼── Switch
PC3 ──┘
```

The switch maintains a **MAC address table** to determine which port should receive a frame.

---

# 15. How Does a Switch Learn MAC Addresses?

Suppose:

```text
PC1 → Switch
```

The switch receives a frame from PC1.

It can learn:

```text
PC1's MAC → Incoming Switch Port
```

The switch stores this information in its MAC address table.

Example:

```text
MAC Address       Port

AA:AA:AA:AA:AA:AA → 1
BB:BB:BB:BB:BB:BB → 2
CC:CC:CC:CC:CC:CC → 3
```

---

# 16. What Happens When a Switch Receives a Frame?

Conceptually:

```text
Frame arrives
      ↓
Read source MAC
      ↓
Learn/update source MAC → incoming port
      ↓
Read destination MAC
      ↓
Is destination known?
    /        \
  Yes         No
   ↓           ↓
Forward     Flood
to port      frame
```

If the destination MAC is unknown, the switch generally floods the frame within the relevant VLAN, excluding the incoming port.

---

# 17. What is Flooding?

**Flooding** means sending a frame out multiple ports when the destination is unknown or when a broadcast needs to be delivered.

Example:

```text
        Switch
       /   |   \
     PC1  PC2  PC3

Unknown destination
       ↓
  Send to multiple ports
```

The incoming port is not normally sent the same frame back.

---

# 18. What is a Broadcast Frame?

A **broadcast frame** is intended for all devices on the local Layer-2 broadcast domain.

The Ethernet broadcast MAC address is:

```text
FF:FF:FF:FF:FF:FF
```

Switches generally forward broadcasts to ports in the same VLAN/broadcast domain.

---

# 19. What is a Collision Domain?

A **collision domain** is a portion of a network in which simultaneous transmissions can potentially interfere with each other.

In modern switched full-duplex Ethernet:

```text
Each switch port
     ↓
Separate collision domain
```

Collisions are largely eliminated in full-duplex switched Ethernet.

---

# 20. What is a Broadcast Domain?

A **broadcast domain** is the set of devices that receive a Layer-2 broadcast.

A typical router separates broadcast domains.

Example:

```text
Broadcast Domain 1
PC1 ── Switch ── PC2
          |
        Router
          |
PC3 ── Switch ── PC4
Broadcast Domain 2
```

---

# 21. Collision Domain vs Broadcast Domain

| Collision Domain | Broadcast Domain |
|---|---|
| Area where Layer-2 transmission collisions can potentially occur | Area over which Layer-2 broadcasts are propagated |
| Switches can divide collision domains | Routers divide broadcast domains |
| Modern full-duplex switched Ethernet largely eliminates collisions | Broadcasts remain within the Layer-2 broadcast domain/VLAN |

---

# 22. Hub

A **hub** is a Layer-1 device that repeats incoming signals out its other ports.

```text
PC1 ──┐
PC2 ──┼── Hub
PC3 ──┘
```

If PC1 sends data:

```text
PC1
 ↓
Hub
 ↓
PC2 + PC3 + other ports
```

The hub does not make forwarding decisions based on MAC addresses.

---

# 23. Hub vs Switch

| Hub | Switch |
|---|---|
| Layer 1 | Mainly Layer 2 |
| Repeats signals | Forwards frames |
| Sends traffic to other ports | Can forward based on MAC address |
| One shared collision domain in typical hub Ethernet | Each full-duplex switch port is its own collision domain |
| Largely obsolete | Common in modern LANs |

---

# 24. What is a Bridge?

A **bridge** is a Layer-2 device that connects network segments and forwards frames based on MAC addresses.

Modern switches essentially provide multi-port bridging functionality.

```text
Segment A ── Bridge ── Segment B
```

---

# 25. Switch vs Bridge

| Bridge | Switch |
|---|---|
| Layer 2 | Mainly Layer 2 |
| Traditionally fewer ports | Usually many ports |
| Forwards using MAC addresses | Forwards using MAC addresses |
| Older/common conceptual device | Common modern implementation |

### Interview Answer

> A switch can be viewed as a high-port-count, hardware-based evolution of a bridge.

---

# 26. What is Error Detection?

Error detection allows the receiver to determine whether transmitted data was corrupted.

Common techniques include:

```text
Parity
Checksum
CRC
```

---

# 27. Parity Bit

A **parity bit** is an extra bit added to data to help detect certain transmission errors.

Two common forms:

```text
Even Parity
Odd Parity
```

### Even Parity

The total number of 1s, including the parity bit, should be even.

Example:

```text
Data = 1011

Number of 1s = 3

Even parity bit = 1

Result = 10111
```

Now the total number of 1s is:

```text
4 → Even
```

---

# 28. Limitation of Parity

Parity can detect many single-bit errors, but it cannot reliably detect all error patterns.

For example, an even number of bit flips can preserve the expected parity.

Therefore:

```text
Parity
→ Simple
→ Limited error detection
```

---

# 29. Checksum

A **checksum** is calculated from data and transmitted along with it.

The receiver recalculates/checks the value to detect corruption.

Conceptually:

```text
Sender
Data
 ↓
Calculate Checksum
 ↓
Data + Checksum
 ↓
Receiver
 ↓
Recalculate / Verify
```

Checksums are used in several networking protocols, although exact checksum algorithms vary.

---

# 30. CRC

**CRC (Cyclic Redundancy Check)** is a powerful error-detection technique based on polynomial arithmetic over binary data.

Conceptually:

```text
Data
 ↓
CRC Calculation
 ↓
CRC Value
 ↓
Transmit
 ↓
Receiver verifies
```

CRC is widely used in data-link technologies such as Ethernet.

---

# 31. Parity vs Checksum vs CRC

| Method | Complexity | Error Detection |
|---|---|---|
| Parity | Low | Limited |
| Checksum | Moderate | Better than simple parity for many errors |
| CRC | Higher | Very strong for many common transmission-error patterns |

---

# 32. What is CSMA/CD?

**CSMA/CD (Carrier Sense Multiple Access with Collision Detection)** is a medium-access mechanism historically used with **shared, half-duplex Ethernet**.

The basic idea:

```text
Listen before transmitting
        ↓
Transmit
        ↓
Detect collision
        ↓
Stop transmission
        ↓
Wait using backoff
        ↓
Try again
```

---

# 33. Why is CSMA/CD Not Normally Used in Modern Switched Ethernet?

Modern Ethernet LANs commonly use:

```text
Switches
+
Full-duplex links
```

In full-duplex Ethernet:

```text
Transmit and receive simultaneously
```

There is no shared medium requiring collision detection in the traditional sense.

Therefore:

> CSMA/CD is mainly a historical/legacy Ethernet concept for shared half-duplex networks.

---

# 34. What is CSMA/CA?

**CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)** is associated with wireless LANs such as Wi-Fi.

Wireless devices attempt to reduce the probability of collisions because detecting collisions while transmitting is difficult in the same way as wired Ethernet.

Conceptually:

```text
Listen
 ↓
Wait if channel is busy
 ↓
Random backoff
 ↓
Transmit
```

---

# 35. CSMA/CD vs CSMA/CA

| CSMA/CD | CSMA/CA |
|---|---|
| Traditionally used in shared Ethernet | Used in wireless LANs such as Wi-Fi |
| Collision Detection | Collision Avoidance |
| Detects collisions after transmission begins | Attempts to reduce collision probability |
| Mainly legacy/shared half-duplex Ethernet concept | Relevant to Wi-Fi |

---

# 36. What is Flow Control at the Data Link Layer?

Flow control prevents a fast sender from overwhelming a slower receiver.

Conceptually:

```text
Fast Sender
     ↓
Flow Control
     ↓
Slow Receiver
```

Common conceptual techniques include:

```text
Stop-and-Wait
Sliding Window
```

The exact mechanisms depend on the protocol.

---

# 37. Stop-and-Wait

In **Stop-and-Wait**, the sender sends one frame and waits for an acknowledgment before sending the next frame.

```text
Sender                 Receiver

Frame 1  ───────────────→
         ←──────────── ACK

Frame 2  ───────────────→
         ←──────────── ACK
```

### Advantage

```text
Simple
```

### Disadvantage

```text
Poor efficiency on high-latency links
```

---

# 38. Sliding Window

**Sliding Window** allows multiple frames to be transmitted before acknowledgments are received.

```text
Frame 1 ─────→
Frame 2 ─────→
Frame 3 ─────→
Frame 4 ─────→
```

This improves link utilization compared with basic Stop-and-Wait.

Sliding-window concepts are important in networking, though the exact implementation differs between protocols.

---

# 39. What is ARP?

**ARP (Address Resolution Protocol)** is used in IPv4 networks to discover the MAC address associated with an IPv4 address on the local network.

Example:

```text
IP Address
192.168.1.10
     ↓
    ARP
     ↓
MAC Address
AA:BB:CC:DD:EE:FF
```

---

# 40. How Does ARP Work?

Suppose:

```text
Host A wants to communicate with
192.168.1.10
```

but does not know the destination MAC address.

### Step 1 — ARP Request

Host A broadcasts:

```text
Who has 192.168.1.10?
```

### Step 2 — ARP Reply

The device owning that IP replies with its MAC address.

```text
192.168.1.10
      ↓
AA:BB:CC:DD:EE:FF
```

### Step 3

Host A can now construct a frame using the destination MAC address.

---

# 41. Is ARP Used for IPv6?

No.

IPv6 uses:

```text
Neighbor Discovery Protocol (NDP)
```

which operates using ICMPv6.

---

# 42. ARP vs DNS

These are completely different:

```text
ARP
→ IPv4 address → MAC address
```

```text
DNS
→ Domain name → IP address
```

Example:

```text
ARP:
192.168.1.10 → AA:BB:CC:DD:EE:FF

DNS:
google.com → IP address
```

---

# 43. What is Error Detection vs Error Correction?

### Error Detection

Determines whether data was corrupted.

Examples:

```text
Parity
Checksum
CRC
```

### Error Correction

Attempts to recover or reconstruct the correct data.

Conceptually:

```text
Error Detection
→ "Something is wrong."

Error Correction
→ "Something is wrong, and we can recover the data."
```

---

# 44. Important Interview Questions

Prepare these especially well:

```text
1. What is the Physical Layer?

2. What is the Data Link Layer?

3. Physical Layer vs Data Link Layer?

4. What is a bit?

5. What are transmission media?

6. Wired vs wireless transmission?

7. What is twisted-pair cable?

8. UTP vs STP?

9. What is fiber optic cable?

10. What is a frame?

11. What is framing?

12. What is a MAC address?

13. What is Ethernet?

14. What is a switch?

15. How does a switch learn MAC addresses?

16. What happens when a switch receives a frame?

17. What is flooding?

18. What is a broadcast frame?

19. What is a collision domain?

20. What is a broadcast domain?

21. Collision domain vs broadcast domain?

22. What is a hub?

23. Hub vs switch?

24. What is a bridge?

25. Bridge vs switch?

26. What is error detection?

27. What is parity?

28. What is checksum?

29. What is CRC?

30. Parity vs checksum vs CRC?

31. What is CSMA/CD?

32. Why is CSMA/CD not normally used in modern switched Ethernet?

33. What is CSMA/CA?

34. CSMA/CD vs CSMA/CA?

35. What is ARP?

36. How does ARP work?

37. ARP vs DNS?

38. Is ARP used in IPv6?

39. What is flow control?

40. What is Stop-and-Wait?

41. What is Sliding Window?

42. What is error detection vs error correction?
```

---

# 45. Most Important Comparisons

## Physical Layer vs Data Link Layer

```text
Physical
→ Bits
→ Signals
→ Cables / Radio

Data Link
→ Frames
→ MAC addresses
→ Local-link delivery
```

---

## Hub vs Switch

```text
Hub
→ Layer 1
→ Repeats signals

Switch
→ Layer 2
→ Forwards frames using MAC addresses
```

---

## Switch vs Router

```text
Switch
→ Mainly Layer 2
→ MAC addresses
→ Connects devices within LANs

Router
→ Layer 3
→ IP addresses
→ Connects different networks
```

---

## MAC vs IP

```text
MAC
→ Link-layer address
→ Local delivery

IP
→ Network-layer address
→ Routing between networks
```

---

## Collision Domain vs Broadcast Domain

```text
Collision Domain
→ Area where collisions can potentially occur

Broadcast Domain
→ Area that receives Layer-2 broadcasts
```

---

## CSMA/CD vs CSMA/CA

```text
CSMA/CD
→ Legacy/shared Ethernet
→ Collision Detection

CSMA/CA
→ Wi-Fi
→ Collision Avoidance
```

---

## ARP vs DNS

```text
ARP
→ IPv4 → MAC

DNS
→ Domain Name → IP
```

---

# 46. Quick Revision

```text
PHYSICAL LAYER
→ Layer 1
→ Bits
→ Signals
→ Physical media

DATA LINK LAYER
→ Layer 2
→ Frames
→ MAC addresses
→ Local-link communication

FRAME
→ Data Link Layer data unit

MAC
→ Link-layer address

ETHERNET
→ Common LAN technology

HUB
→ Layer 1
→ Repeats signals

SWITCH
→ Layer 2
→ Forwards frames using MAC addresses

BRIDGE
→ Layer 2
→ Connects LAN segments

COLLISION DOMAIN
→ Area where collisions can potentially occur

BROADCAST DOMAIN
→ Area receiving Layer-2 broadcasts

ARP
→ IPv4 address → MAC address

PARITY
→ Simple error detection

CHECKSUM
→ Error detection using calculated value

CRC
→ Strong error-detection technique

CSMA/CD
→ Legacy shared Ethernet
→ Detect collisions

CSMA/CA
→ Wireless LAN
→ Avoid collisions

STOP-AND-WAIT
→ Send one frame, wait for ACK

SLIDING WINDOW
→ Multiple frames can be in flight
```

---

# 47. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Physical Layer vs Data Link Layer
Frames and Framing
MAC Address
Ethernet
Switch
How a Switch Learns MAC Addresses
Hub vs Switch
Switch vs Router
ARP
MAC vs IP
Collision Domain
Broadcast Domain
CRC
CSMA/CD
CSMA/CA
```

## ⭐⭐⭐ Good to Know

```text
Transmission Media
UTP vs STP
Fiber Optic
Bridge
Parity
Checksum
Stop-and-Wait
Sliding Window
Error Detection vs Error Correction
```

> **For placement interviews, focus deeply on Frames → MAC Address → Ethernet → Switch → ARP → Collision/Broadcast Domains → Hub vs Switch → CRC → CSMA/CD/CSMA/CA.** These are the highest-value concepts from the Physical and Data Link Layers.