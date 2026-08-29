# Routing and Network Layer

## 1. What is the Network Layer?

The **Network Layer** is Layer 3 of the OSI model.

Its main responsibility is to deliver packets from a source network to a destination network.

Main concepts:

```text
IP Addressing
Routing
Packet Forwarding
Routers
Routing Tables
ICMP
```

Data unit:

```text
Packet
```

---

# 2. Main Functions of the Network Layer

The Network Layer mainly handles:

```text
Logical Addressing
Routing
Packet Forwarding
Path Selection
Packet Fragmentation in IPv4
Error/Diagnostic Messaging through ICMP
```

---

# 3. What is Routing?

**Routing** is the process of determining the path that packets should take from the source network to the destination network.

Example:

```text
PC A
 ↓
Router 1
 ↓
Router 2
 ↓
Router 3
 ↓
PC B
```

Routing decides:

```text
Which path should the packet take?
```

---

# 4. What is Forwarding?

**Forwarding** is the process of moving a packet from an incoming interface to the appropriate outgoing interface.

Example:

```text
Packet arrives
      ↓
Router checks destination IP
      ↓
Looks at routing information
      ↓
Selects outgoing interface
      ↓
Forwards packet
```

---

# 5. Routing vs Forwarding

This is an important interview question.

| Routing | Forwarding |
|---|---|
| Determines the path | Moves the packet along that path |
| Control-plane function | Data-plane function |
| Builds/maintains routing information | Uses routing information |
| Can involve routing protocols | Happens for individual packets |

### Simple Memory Trick

```text
Routing
→ "Which path?"

Forwarding
→ "Send it where?"
```

---

# 6. What is a Router?

A **router** is a Layer-3 device that connects different IP networks and forwards packets based on destination IP addresses and routing information.

Example:

```text
Network A
   |
Router
   |
Network B
```

A router can have multiple interfaces connected to different networks.

---

# 7. What is a Routing Table?

A **routing table** contains information used by a router to determine where packets should be forwarded.

A simplified routing table may look like:

```text
Destination       Next Hop       Interface

192.168.1.0/24    Direct         eth0
10.0.0.0/8        192.168.1.1    eth1
0.0.0.0/0         192.168.1.254  eth2
```

Important fields can include:

```text
Destination Network
Prefix Length
Next Hop
Outgoing Interface
Metric
```

---

# 8. What is a Next Hop?

The **next hop** is the next router/device to which a packet should be sent on its journey toward the destination.

Example:

```text
Source
  ↓
Router A
  ↓
Router B
  ↓
Router C
  ↓
Destination
```

From Router A's perspective:

```text
Next Hop → Router B
```

---

# 9. What is an Outgoing Interface?

The **outgoing interface** is the router interface through which a packet should leave the router.

Example:

```text
Router

eth0 → Network A
eth1 → Network B
eth2 → Network C
```

If the destination is in Network B:

```text
Packet → eth1
```

---

# 10. How Does a Router Forward a Packet?

Suppose:

```text
Source:
192.168.1.10

Destination:
10.10.10.20
```

The router:

```text
1. Receives the packet
        ↓
2. Reads destination IP
        ↓
3. Searches routing table
        ↓
4. Finds the best matching route
        ↓
5. Determines next hop/outgoing interface
        ↓
6. Forwards the packet
```

---

# 11. Longest Prefix Match

When multiple routes match a destination IP, routers generally choose the route with the **longest matching prefix**.

Example:

```text
10.0.0.0/8
10.1.0.0/16
10.1.2.0/24
```

Destination:

```text
10.1.2.50
```

All three routes can match.

The router chooses:

```text
10.1.2.0/24
```

because `/24` is the most specific match.

### Interview Answer

> Longest prefix match means selecting the routing-table entry with the most specific matching network prefix.

---

# 12. What is a Default Route?

A **default route** is used when no more specific route matches the destination.

For IPv4:

```text
0.0.0.0/0
```

For IPv6:

```text
::/0
```

Example:

```text
Destination not found
        ↓
Default Route
        ↓
Default Gateway / Next Hop
```

---

# 13. What is a Static Route?

A **static route** is manually configured by a network administrator.

Example:

```text
Network:
10.10.0.0/16

Next Hop:
192.168.1.1
```

### Advantages

```text
Simple for small networks
Predictable
No routing-protocol overhead
```

### Disadvantages

```text
Manual configuration
Harder to maintain in large networks
Does not automatically adapt to topology changes
```

---

# 14. What is Dynamic Routing?

In **dynamic routing**, routers learn and update routes using routing protocols.

Examples:

```text
RIP
OSPF
EIGRP
BGP
```

Advantages:

```text
Automatic route learning
Adapts to topology changes
Useful for larger networks
```

---

# 15. Static vs Dynamic Routing

| Static Routing | Dynamic Routing |
|---|---|
| Manually configured | Learned using routing protocols |
| Simple for small networks | Better for larger networks |
| No routing-protocol overhead | Has protocol overhead |
| Does not automatically adapt | Can adapt to topology changes |
| Predictable | More dynamic |

---

# 16. What is a Routing Protocol?

A **routing protocol** allows routers to exchange information so they can learn paths to destination networks.

Examples:

```text
RIP
OSPF
EIGRP
BGP
```

Routing protocols help routers build and maintain routing information.

---

# 17. Types of Routing Protocols

Routing protocols can be broadly classified into:

```text
Distance Vector
Link State
Path Vector
```

---

# 18. Distance Vector Routing

In **Distance Vector** routing, routers learn routes based on information received from neighboring routers.

A router generally considers:

```text
Destination
Distance / Metric
Next Hop
```

Example:

```text
Router A
   ↓
Router B
   ↓
Router C
```

Router A can learn about networks reachable through Router B.

Example protocol:

```text
RIP
```

---

# 19. Link-State Routing

In **Link-State** routing, routers build a more complete view of the network topology and calculate paths using that information.

A common example:

```text
OSPF
```

Conceptually:

```text
Routers exchange link-state information
        ↓
Build topology database
        ↓
Calculate shortest/best paths
        ↓
Build routing table
```

---

# 20. Distance Vector vs Link State

| Distance Vector | Link State |
|---|---|
| Learns routes from neighbors | Builds topology view |
| Simpler concept | More complex |
| Typically less topology information | More topology information |
| Example: RIP | Example: OSPF |

---

# 21. What is RIP?

**RIP (Routing Information Protocol)** is a distance-vector routing protocol.

A traditional RIP metric is:

```text
Hop Count
```

Maximum usable hop count:

```text
15
```

A hop count of:

```text
16
```

is considered unreachable in RIP.

RIP is mainly useful as an interview concept and is not typically the preferred protocol for modern large enterprise networks.

---

# 22. What is OSPF?

**OSPF (Open Shortest Path First)** is a link-state Interior Gateway Protocol.

It uses a cost-based metric and calculates paths using the network topology.

Important concepts:

```text
Link State
Cost
Shortest Path First
Areas
```

---

# 23. What is BGP?

**BGP (Border Gateway Protocol)** is the major routing protocol used to exchange routing information between autonomous systems on the Internet.

It is a:

```text
Path Vector Protocol
```

BGP is especially important for:

```text
Internet routing
Inter-AS routing
Large-scale network connectivity
```

---

# 24. Interior vs Exterior Gateway Protocols

Routing protocols can also be categorized based on where they operate.

### IGP

**Interior Gateway Protocols** are used for routing within an autonomous system.

Examples:

```text
RIP
OSPF
EIGRP
```

### EGP

**Exterior Gateway Protocol** refers to routing between autonomous systems.

The modern Internet uses:

```text
BGP
```

for inter-domain routing.

---

# 25. What is an Autonomous System?

An **Autonomous System (AS)** is a network or group of networks operated under a common routing policy.

Each AS is identified by an:

```text
ASN
→ Autonomous System Number
```

BGP is used to exchange routing information between autonomous systems.

---

# 26. IGP vs BGP

| IGP | BGP |
|---|---|
| Used within an AS | Used primarily between ASes |
| Examples: OSPF, RIP, EIGRP | BGP |
| Focuses on internal network paths | Uses policy and path attributes for inter-domain routing |

---

# 27. What is a Routing Metric?

A **routing metric** is a value used to evaluate or compare routes.

Different protocols use different metrics.

Examples:

```text
RIP → Hop Count
OSPF → Cost
```

A router uses the relevant metric and protocol rules to select routes.

---

# 28. What is Hop Count?

A **hop** generally represents one router traversal.

Example:

```text
Host
 ↓
Router 1  → Hop 1
 ↓
Router 2  → Hop 2
 ↓
Router 3  → Hop 3
 ↓
Destination
```

Hop count is the traditional metric used by RIP.

---

# 29. What is ICMP?

**ICMP (Internet Control Message Protocol)** is used for network-layer control, diagnostic, and error-reporting messages.

Examples:

```text
Destination Unreachable
Time Exceeded
Echo Request
Echo Reply
```

---

# 30. What is Ping?

`ping` commonly uses:

```text
ICMP Echo Request
ICMP Echo Reply
```

Example:

```text
Host A
  |
  | Echo Request
  ↓
Host B
  |
  | Echo Reply
  ↓
Host A
```

Ping helps test:

```text
Reachability
Round-trip time
Basic network connectivity
```

---

# 31. What is Traceroute?

`traceroute` (called `tracert` on Windows) helps discover the sequence of routers/hops along a path.

It relies on mechanisms involving:

```text
TTL / Hop Limit
ICMP responses
```

Conceptually:

```text
Source
 ↓
Router 1
 ↓
Router 2
 ↓
Router 3
 ↓
Destination
```

It helps identify where delays or connectivity problems may occur.

---

# 32. What is TTL?

**TTL (Time To Live)** is an IPv4 header field.

It is decremented by routers as the packet is forwarded.

Example:

```text
TTL = 5

Router 1 → 4
Router 2 → 3
Router 3 → 2
Router 4 → 1
...
```

If TTL reaches zero, the packet is discarded and an ICMP Time Exceeded message may be generated.

The main purpose is to prevent packets from circulating indefinitely due to routing loops.

---

# 33. What is Hop Limit in IPv6?

IPv6 uses:

```text
Hop Limit
```

instead of the IPv4:

```text
TTL
```

The concept is similar:

```text
Each router
→ Decrements Hop Limit
```

When it reaches zero, the packet is discarded.

---

# 34. TTL vs Hop Limit

| IPv4 | IPv6 |
|---|---|
| TTL | Hop Limit |
| Decremented by routers | Decremented by routers |
| Prevents indefinite looping | Prevents indefinite looping |

---

# 35. What is Packet Fragmentation?

Fragmentation occurs when a packet is larger than the maximum packet size supported by a link.

This maximum size is called:

```text
MTU
→ Maximum Transmission Unit
```

IPv4 routers can fragment packets when permitted.

IPv6 routers do **not** fragment packets during forwarding; the source is expected to use Path MTU Discovery, and fragmentation is handled by the source using the IPv6 Fragment extension header when needed.

---

# 36. What is MTU?

**MTU (Maximum Transmission Unit)** is the largest IP packet size that can normally be transmitted over a particular link without fragmentation at that layer.

A common Ethernet MTU is:

```text
1500 bytes
```

The actual MTU depends on the network technology and configuration.

---

# 37. What is Path MTU Discovery?

**Path MTU Discovery (PMTUD)** determines the largest packet size that can travel along a path without fragmentation.

Conceptually:

```text
Source
 ↓
Router
 ↓
Router
 ↓
Destination

Find smallest supported MTU
        ↓
Use appropriate packet size
```

This helps avoid fragmentation.

---

# 38. IPv4 vs IPv6 Fragmentation

```text
IPv4
→ Routers may fragment packets

IPv6
→ Routers do not fragment packets
→ Source handles fragmentation if required
```

This is an important interview difference.

---

# 39. What Happens When a Packet Cannot Reach Its Destination?

A router or host may generate an ICMP error message, depending on the situation.

Example:

```text
Destination unreachable
```

Possible causes include:

```text
No route
Network unreachable
Host unreachable
Port unreachable
```

---

# 40. What is a Routing Loop?

A **routing loop** occurs when packets continuously circulate among routers instead of reaching their destination.

Example:

```text
Router A
   ↓
Router B
   ↓
Router C
   ↓
Router A
   ↓
Router B
   ↓
...
```

TTL/Hop Limit prevents such packets from circulating forever.

---

# 41. What is the Control Plane?

The **control plane** is responsible for making routing decisions and maintaining routing information.

Examples:

```text
OSPF
BGP
RIP
Routing table calculation
```

Conceptually:

```text
Control Plane
      ↓
Build routing information
      ↓
Data Plane uses it
```

---

# 42. What is the Data Plane?

The **data plane** is responsible for forwarding packets based on the forwarding/routing information.

Example:

```text
Packet
 ↓
Destination IP
 ↓
Forwarding lookup
 ↓
Outgoing Interface
 ↓
Packet sent
```

---

# 43. Control Plane vs Data Plane

| Control Plane | Data Plane |
|---|---|
| Determines routes | Forwards packets |
| Builds routing information | Uses forwarding information |
| Uses routing protocols | Handles packet forwarding |
| OSPF/BGP/RIP | Packet forwarding |

### Easy Memory Trick

```text
Control Plane
→ Decides

Data Plane
→ Delivers
```

---

# 44. What is Unicast Routing?

**Unicast routing** sends a packet from one source to one destination.

```text
A ─────→ B
```

Most ordinary IP traffic is unicast.

---

# 45. What is Multicast Routing?

**Multicast** sends traffic from one source to a group of interested receivers.

```text
        ┌── B
A ──────┼── C
        └── D
```

Multicast is useful when the same content needs to be delivered to multiple receivers.

---

# 46. What is Anycast?

With **anycast**, the same address can be assigned to multiple locations/interfaces, and routing directs the traffic to an appropriate destination, often the nearest according to routing.

Example:

```text
             Server A
            /
Client → Anycast Address
            \
             Server B
```

The routing system selects one suitable instance.

---

# 47. Important Interview Questions

```text
1. What is the Network Layer?

2. What are the main functions of the Network Layer?

3. What is routing?

4. What is forwarding?

5. Routing vs forwarding?

6. What is a router?

7. What is a routing table?

8. What is a next hop?

9. What is an outgoing interface?

10. How does a router forward a packet?

11. What is longest prefix match?

12. Why is longest prefix match important?

13. What is a default route?

14. What is a static route?

15. What is dynamic routing?

16. Static vs dynamic routing?

17. What is a routing protocol?

18. What are distance-vector protocols?

19. What are link-state protocols?

20. Distance vector vs link state?

21. What is RIP?

22. What is OSPF?

23. What is BGP?

24. What is an autonomous system?

25. What is an ASN?

26. IGP vs BGP?

27. What is a routing metric?

28. What is hop count?

29. What is ICMP?

30. How does ping work?

31. What is traceroute?

32. What is TTL?

33. What is IPv6 Hop Limit?

34. TTL vs Hop Limit?

35. What is MTU?

36. What is packet fragmentation?

37. IPv4 vs IPv6 fragmentation?

38. What is Path MTU Discovery?

39. What is a routing loop?

40. How does TTL help prevent routing loops?

41. What is the control plane?

42. What is the data plane?

43. Control plane vs data plane?

44. What is unicast?

45. What is multicast?

46. What is anycast?
```

---

# 48. Most Important Comparisons

## Routing vs Forwarding

```text
Routing
→ Determines the path
→ Control plane

Forwarding
→ Sends packets to the next destination
→ Data plane
```

---

## Static vs Dynamic Routing

```text
Static
→ Manually configured
→ Simple
→ No automatic adaptation

Dynamic
→ Learned through routing protocols
→ Automatically adapts
→ Better for larger networks
```

---

## Distance Vector vs Link State

```text
Distance Vector
→ Learns from neighbors
→ Example: RIP

Link State
→ Builds topology view
→ Example: OSPF
```

---

## RIP vs OSPF vs BGP

```text
RIP
→ Distance Vector
→ Hop Count
→ IGP

OSPF
→ Link State
→ Cost
→ IGP

BGP
→ Path Vector
→ Inter-domain routing
```

---

## IPv4 TTL vs IPv6 Hop Limit

```text
IPv4
→ TTL

IPv6
→ Hop Limit

Both
→ Decrement at routers
→ Help prevent indefinite packet loops
```

---

## Control Plane vs Data Plane

```text
Control Plane
→ Decides routes

Data Plane
→ Forwards packets
```

---

# 49. Quick Revision

```text
NETWORK LAYER
→ Layer 3
→ IP
→ Routing
→ Forwarding
→ Packets

ROUTING
→ Determines path

FORWARDING
→ Moves packet to outgoing interface

ROUTER
→ Connects IP networks

ROUTING TABLE
→ Contains route information

NEXT HOP
→ Next router/device

LONGEST PREFIX MATCH
→ Most specific matching route

DEFAULT ROUTE
→ 0.0.0.0/0
→ Used when no more specific route matches

STATIC ROUTING
→ Manually configured

DYNAMIC ROUTING
→ Learned through routing protocols

RIP
→ Distance Vector
→ Hop Count

OSPF
→ Link State
→ Cost

BGP
→ Path Vector
→ Inter-AS routing

ICMP
→ Error reporting and diagnostics

PING
→ ICMP Echo Request/Reply

TRACEROUTE
→ Shows path/hops

TTL
→ IPv4
→ Prevents indefinite looping

HOP LIMIT
→ IPv6 equivalent concept

MTU
→ Maximum Transmission Unit

FRAGMENTATION
→ Breaking a packet into smaller pieces

CONTROL PLANE
→ Makes routing decisions

DATA PLANE
→ Forwards packets

UNICAST
→ One-to-one

MULTICAST
→ One-to-many group

ANYCAST
→ One appropriate destination from multiple instances
```

---

# 50. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Network Layer
Routing vs Forwarding
Router
Routing Table
Longest Prefix Match
Default Route
Static vs Dynamic Routing
RIP
OSPF
BGP
Routing Metrics
ICMP
Ping
Traceroute
TTL
MTU
IPv4 vs IPv6 Fragmentation
Control Plane vs Data Plane
```

## ⭐⭐⭐ Good to Know

```text
Distance Vector
Link State
Autonomous System
ASN
Unicast
Multicast
Anycast
Path MTU Discovery
Routing Loops
```

> **For placement interviews, focus deeply on Routing → Routing Table → Longest Prefix Match → Static/Dynamic Routing → RIP/OSPF/BGP → ICMP → Ping/Traceroute → TTL → MTU/Fragmentation → Control Plane vs Data Plane.**