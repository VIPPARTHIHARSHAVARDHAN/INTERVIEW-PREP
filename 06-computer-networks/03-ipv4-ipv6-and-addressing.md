# IPv4, IPv6 and Addressing

## 1. What is an IP Address?

An **IP (Internet Protocol) address** is a logical address assigned to a network interface so that devices can be identified and packets can be delivered across IP networks.

Example:

```text
192.168.1.10
```

IP addresses operate at the **Network Layer (Layer 3)** of the OSI model.

---

# 2. Why Do We Need IP Addresses?

IP addresses help identify:

```text
Source Device
Destination Device
Network
Host
```

When a packet travels across networks:

```text
Source
  ↓
Router
  ↓
Router
  ↓
Destination
```

Routers use IP addressing and routing information to decide where packets should go.

---

# 3. IPv4

**IPv4 (Internet Protocol version 4)** is a widely used version of the Internet Protocol.

IPv4 uses:

```text
32 bits
```

Example:

```text
192.168.1.10
```

An IPv4 address contains **4 octets**, with each octet representing 8 bits.

```text
192 . 168 . 1 . 10
 ↓     ↓    ↓    ↓
 8     8    8    8 bits

Total = 32 bits
```

---

# 4. IPv4 Address Range

Each IPv4 octet contains 8 bits.

Therefore, each octet can represent:

```text
0 to 255
```

Example:

```text
0.0.0.0
to
255.255.255.255
```

The total number of possible IPv4 addresses is:

```text
2^32
= 4,294,967,296
```

---

# 5. Binary Representation of IPv4

An IPv4 address is ultimately represented as 32 bits.

Example:

```text
192.168.1.10
```

can be represented in binary as:

```text
11000000.10101000.00000001.00001010
```

Each group contains 8 bits.

---

# 6. Network Part and Host Part

An IP address can be divided into:

```text
Network Part
+
Host Part
```

Example:

```text
192.168.1.10/24
```

Here:

```text
First 24 bits → Network
Remaining 8 bits → Host
```

So conceptually:

```text
192.168.1 | 10
Network   | Host
```

The exact boundary is determined by the subnet mask or prefix length.

---

# 7. What is a Subnet Mask?

A **subnet mask** identifies which portion of an IPv4 address represents the network and which portion represents the host.

Example:

```text
IP Address:
192.168.1.10

Subnet Mask:
255.255.255.0
```

Binary:

```text
IP:
11000000.10101000.00000001.00001010

Mask:
11111111.11111111.11111111.00000000
```

The `1`s represent the network portion.

The `0`s represent the host portion.

```text
Network              Host
11111111.11111111.11111111.00000000
```

---

# 8. What is CIDR?

**CIDR (Classless Inter-Domain Routing)** represents an IP network using a prefix length.

Example:

```text
192.168.1.0/24
```

The `/24` means:

```text
24 bits → Network prefix
8 bits  → Host portion
```

Common examples:

```text
/8
/16
/24
/25
/26
/27
/28
/30
```

---

# 9. CIDR Example

Consider:

```text
192.168.1.0/24
```

Total bits:

```text
32
```

Network bits:

```text
24
```

Host bits:

```text
32 - 24 = 8
```

Therefore:

```text
2^8 = 256
```

addresses exist in the block.

In a typical traditional IPv4 subnet, two addresses are reserved for:

```text
Network Address
Broadcast Address
```

So:

```text
Usable host addresses = 256 - 2 = 254
```

---

# 10. What is Subnetting?

**Subnetting** is the process of dividing a larger IP network into smaller logical networks called subnets.

Example:

```text
Large Network
     ↓
 ┌───┼───┐
 ↓   ↓   ↓
Subnet 1
Subnet 2
Subnet 3
```

Subnetting helps with:

```text
Efficient IP address usage
Network organization
Traffic isolation
Network management
```

---

# 11. Simple Subnetting Example

Suppose:

```text
192.168.1.0/24
```

is divided into:

```text
/26
```

Network bits:

```text
26
```

Host bits:

```text
32 - 26 = 6
```

Number of addresses per subnet:

```text
2^6 = 64
```

Therefore, the `/24` network can be divided into:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

Each subnet contains 64 addresses.

Typically:

```text
62 usable host addresses
```

because one address is used as the network address and one as the broadcast address.

---

# 12. Private IPv4 Addresses

Private IP addresses are intended for use inside private networks.

The main private IPv4 ranges are:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

Examples:

```text
10.0.0.5
172.16.10.20
192.168.1.10
```

Private IP addresses are not directly routable across the public Internet.

---

# 13. Public IP Address

A **public IP address** is an address used for communication across the public Internet.

Example:

```text
Internet
   ↓
Public IP
   ↓
Router / Network
```

Public addresses must be globally coordinated to avoid conflicts.

---

# 14. Public vs Private IP

| Public IP | Private IP |
|---|---|
| Used on public Internet | Used inside private networks |
| Globally unique/routable | Can be reused in different private networks |
| Assigned through Internet addressing systems/ISPs | Commonly assigned by local network configuration such as DHCP |
| Can be reachable from the Internet when routing/firewall rules allow | Normally not directly Internet-routable |

---

# 15. Static IP Address

A **static IP address** is manually or persistently configured so that it normally remains the same.

Common uses:

```text
Servers
Network devices
Printers
Infrastructure
```

Example:

```text
Server → 192.168.1.100
```

---

# 16. Dynamic IP Address

A **dynamic IP address** is assigned automatically and may change over time.

A common protocol used for automatic IPv4 address configuration is:

```text
DHCP
```

Example:

```text
Device
  ↓
DHCP
  ↓
IP Address
Subnet Mask
Default Gateway
DNS Server
```

---

# 17. Static vs Dynamic IP

| Static IP | Dynamic IP |
|---|---|
| Usually remains fixed | May change |
| Often manually configured or reserved | Commonly assigned using DHCP |
| Useful for servers/infrastructure | Common for client devices |
| Requires deliberate configuration | Easier to manage automatically |

---

# 18. What is DHCP?

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration information to clients.

It can provide:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

---

# 19. DHCP DORA Process

A common IPv4 DHCP exchange is called **DORA**:

```text
D → Discover
O → Offer
R → Request
A → Acknowledge
```

Flow:

```text
Client
  |
  | DHCP Discover
  ↓
Server
  |
  | DHCP Offer
  ↓
Client
  |
  | DHCP Request
  ↓
Server
  |
  | DHCP ACK
  ↓
Client
```

---

# 20. What is a Default Gateway?

A **default gateway** is the router or Layer-3 device a host uses to reach destinations outside its local subnet.

Example:

```text
PC
IP:      192.168.1.10
Gateway: 192.168.1.1
```

If the destination is outside the local network:

```text
PC
 ↓
Default Gateway
 ↓
Other Networks
```

---

# 21. Local vs Remote Destination

Suppose:

```text
PC:
192.168.1.10/24

Destination:
192.168.1.20
```

Both are in:

```text
192.168.1.0/24
```

So the destination is local.

But if:

```text
Destination:
8.8.8.8
```

it is outside the local subnet.

The host sends the packet toward its:

```text
Default Gateway
```

---

# 22. What is NAT?

**NAT (Network Address Translation)** translates IP addresses as packets pass between networks.

It is commonly used to allow multiple private IPv4 hosts to share one public IPv4 address.

Example:

```text
Private Network

192.168.1.10 ──┐
192.168.1.11 ──┼── Router/NAT ── Public Internet
192.168.1.12 ──┘
```

The router performs address translation between the private network and the public side.

---

# 23. Why is NAT Important?

One major reason NAT became widely used is IPv4 address scarcity.

For example:

```text
Private Devices
       ↓
     NAT
       ↓
One/Few Public IPv4 Addresses
       ↓
Internet
```

NAT also provides a form of address hiding, but it should **not** be considered a replacement for a firewall or a complete security mechanism.

---

# 24. IPv6

**IPv6 (Internet Protocol version 6)** was developed to address limitations of IPv4, especially the shortage of IPv4 addresses.

IPv6 uses:

```text
128 bits
```

Example:

```text
2001:db8:1234:5678:abcd:ef01:2345:6789
```

---

# 25. IPv6 Address Format

IPv6 addresses are written in hexadecimal.

They contain:

```text
8 groups
```

Each group contains:

```text
16 bits
```

Therefore:

```text
8 × 16 = 128 bits
```

Example:

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

---

# 26. IPv6 Address Compression

IPv6 allows leading zeros within a group to be removed.

Example:

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

can become:

```text
2001:db8:0:0:0:ff00:42:8329
```

A consecutive sequence of all-zero groups can also be replaced by:

```text
::
```

So the address can be written as:

```text
2001:db8::ff00:42:8329
```

Important rule:

> `::` can be used only once in an IPv6 address.

---

# 27. IPv4 vs IPv6

| IPv4 | IPv6 |
|---|---|
| 32-bit address | 128-bit address |
| Decimal notation | Hexadecimal notation |
| Example: `192.168.1.10` | Example: `2001:db8::1` |
| Smaller address space | Extremely large address space |
| Uses broadcast | Does not use broadcast |
| ARP is used for address resolution | NDP is used |
| NAT is widely used | NAT is generally less central to addressing |

---

# 28. Why Was IPv6 Introduced?

The main reason was:

```text
IPv4 address exhaustion
```

IPv6 provides:

```text
Much larger address space
```

It also introduces improvements such as:

```text
Simplified base header
Autoconfiguration mechanisms
Multicast/anycast support
No IPv4-style broadcast
```

---

# 29. IPv6 Address Types

Important IPv6 address categories include:

```text
Unicast
Multicast
Anycast
```

---

## 29.1 Unicast

A **unicast** address identifies a single interface.

```text
Sender ─────→ One Destination
```

---

## 29.2 Multicast

A **multicast** address identifies a group of interfaces.

```text
Sender
  ↓
 ┌───┬───┬───┐
 ↓   ↓   ↓
Host Host Host
```

---

## 29.3 Anycast

An **anycast** address is assigned to multiple interfaces, and traffic is delivered to the nearest or best destination according to routing.

```text
        ┌── Server A
Client ─┼── Server B
        └── Server C

→ Routing selects an appropriate/nearest instance
```

---

# 30. Does IPv6 Have Broadcast?

No.

IPv6 does **not** use broadcast.

Instead, IPv6 uses:

```text
Multicast
```

for many functions that used broadcast in IPv4.

---

# 31. What is NDP?

**NDP (Neighbor Discovery Protocol)** is used by IPv6 nodes for functions such as:

```text
Neighbor discovery
Router discovery
Address resolution
Duplicate Address Detection
```

NDP operates through:

```text
ICMPv6
```

---

# 32. ARP vs NDP

| ARP | NDP |
|---|---|
| Used with IPv4 | Used with IPv6 |
| Resolves IPv4 address to MAC address | Provides IPv6 neighbor/address-resolution functions |
| Uses ARP messages | Uses ICMPv6 messages |
| Uses local broadcast for ARP requests | Uses IPv6 multicast mechanisms |

---

# 33. What is Loopback Address?

A loopback address refers to the local host itself.

IPv4:

```text
127.0.0.1
```

IPv6:

```text
::1
```

Example:

```text
Application
    ↓
127.0.0.1
    ↓
Same Computer
```

It is commonly used for testing local network software.

---

# 34. What is APIPA?

**APIPA (Automatic Private IP Addressing)** is an IPv4 mechanism used by some systems when a DHCP server cannot provide an address.

The IPv4 link-local range is:

```text
169.254.0.0/16
```

Example:

```text
169.254.x.x
```

This is intended for local-link communication rather than normal Internet routing.

---

# 35. What is a Link-Local Address?

A link-local address is intended for communication on the local network/link.

IPv4:

```text
169.254.0.0/16
```

IPv6 link-local addresses use:

```text
FE80::/10
```

IPv6 link-local addresses are important for local-network operation and neighbor/router discovery.

---

# 36. What is Subnetting Used For?

Subnetting can help:

```text
Divide large networks
Reduce unnecessary broadcast scope
Organize departments
Improve address utilization
Control network boundaries
```

Example:

```text
Company Network
      ↓
 ┌────┼────┐
 ↓    ↓    ↓
HR   IT   Sales
```

Each department can have its own subnet.

---

# 37. What is CIDR Notation?

CIDR notation uses:

```text
IP Address / Prefix Length
```

Example:

```text
192.168.10.0/24
```

Here:

```text
/24
```

means the first 24 bits identify the network prefix.

---

# 38. Important CIDR Values

| CIDR | Host Bits | Addresses |
|---|---:|---:|
| `/24` | 8 | 256 |
| `/25` | 7 | 128 |
| `/26` | 6 | 64 |
| `/27` | 5 | 32 |
| `/28` | 4 | 16 |
| `/29` | 3 | 8 |
| `/30` | 2 | 4 |

For traditional IPv4 subnets, usable host addresses are usually:

```text
Total addresses - 2
```

because of the network and broadcast addresses.

There are exceptions and special cases, so don't blindly apply `-2` to every IPv4 prefix.

---

# 39. Classful IPv4 Addressing

Older IPv4 networking used classes:

```text
Class A
Class B
Class C
Class D
Class E
```

Traditional ranges:

```text
Class A → 1–126
Class B → 128–191
Class C → 192–223
Class D → 224–239
Class E → 240–255
```

Class D was used for multicast.

Class E was reserved/experimental.

---

# 40. Is Classful Addressing Important?

For modern networking:

```text
CIDR
```

is more important than traditional classful addressing.

However, interviewers may still ask:

```text
What are Class A, B, C?
Why was classful addressing replaced?
```

### Interview Answer

> Classful addressing divided IPv4 addresses into fixed classes with predefined network sizes. It was inefficient because organizations often received blocks larger or smaller than needed. CIDR introduced flexible prefix lengths and improved address allocation and routing efficiency.

---

# 41. Special IPv4 Addresses

Some important IPv4 addresses/ranges:

```text
127.0.0.0/8
→ Loopback

169.254.0.0/16
→ Link-local / APIPA

10.0.0.0/8
→ Private

172.16.0.0/12
→ Private

192.168.0.0/16
→ Private

255.255.255.255
→ Limited broadcast
```

---

# 42. Network Address

The **network address** identifies the subnet itself.

Example:

```text
192.168.1.0/24
```

Network address:

```text
192.168.1.0
```

Host addresses are within the subnet's range.

---

# 43. Broadcast Address

The **broadcast address** is used in IPv4 to send a packet to all hosts in a subnet.

For:

```text
192.168.1.0/24
```

the broadcast address is:

```text
192.168.1.255
```

---

# 44. Network Address vs Broadcast Address

For a typical `/24` subnet:

```text
192.168.1.0   → Network Address

192.168.1.1
      ↓
  Host Addresses
      ↓
192.168.1.254

192.168.1.255 → Broadcast Address
```

---

# 45. Important Interview Questions

```text
1. What is an IP address?

2. What is IPv4?

3. Why does IPv4 use 32 bits?

4. What is an octet?

5. What is the range of an IPv4 octet?

6. How many IPv4 addresses are possible?

7. What is the difference between network and host portions?

8. What is a subnet mask?

9. What is CIDR?

10. What does /24 mean?

11. What is subnetting?

12. Why is subnetting used?

13. How many addresses are in a /24 subnet?

14. How many usable hosts are normally in a /24 subnet?

15. What are private IP addresses?

16. What are the private IPv4 ranges?

17. Public IP vs private IP?

18. Static IP vs dynamic IP?

19. What is DHCP?

20. Explain the DHCP DORA process.

21. What is a default gateway?

22. What is NAT?

23. Why is NAT used?

24. What is IPv6?

25. Why was IPv6 introduced?

26. How many bits does IPv6 use?

27. Why does IPv6 use hexadecimal notation?

28. How is IPv6 address compression done?

29. IPv4 vs IPv6?

30. Does IPv6 support broadcast?

31. What is multicast?

32. What is anycast?

33. What is NDP?

34. ARP vs NDP?

35. What is a loopback address?

36. What is APIPA?

37. What is a link-local address?

38. What is the difference between a network address and broadcast address?

39. What is classful addressing?

40. Class A vs Class B vs Class C?

41. Why was classful addressing replaced by CIDR?

42. What happens when a device wants to communicate with a device outside its subnet?
```

---

# 46. Most Important Comparisons

## IPv4 vs IPv6

```text
IPv4
→ 32-bit
→ Decimal
→ Broadcast supported
→ ARP
→ Limited address space

IPv6
→ 128-bit
→ Hexadecimal
→ No broadcast
→ NDP
→ Huge address space
```

---

## Public IP vs Private IP

```text
Public
→ Internet-facing/routable
→ Globally coordinated

Private
→ Internal networks
→ Reusable across different private networks
```

---

## Static IP vs Dynamic IP

```text
Static
→ Usually fixed
→ Manual/reserved configuration

Dynamic
→ Assigned automatically
→ Can change
→ DHCP commonly used
```

---

## IP vs MAC

```text
IP
→ Layer 3
→ Logical/network addressing
→ Routing

MAC
→ Layer 2
→ Local-link addressing
```

---

## ARP vs NDP

```text
ARP
→ IPv4
→ Address resolution

NDP
→ IPv6
→ Neighbor/router discovery and address-resolution functions
```

---

# 47. Quick Revision

```text
IP ADDRESS
→ Logical network-layer address

IPv4
→ 32 bits
→ Decimal
→ 4 octets

IPv6
→ 128 bits
→ Hexadecimal
→ 8 groups

SUBNET MASK
→ Separates network and host portions

CIDR
→ IP/prefix notation
→ Example: 192.168.1.0/24

SUBNETTING
→ Dividing a network into smaller networks

PRIVATE IPv4
→ 10.0.0.0/8
→ 172.16.0.0/12
→ 192.168.0.0/16

PUBLIC IP
→ Publicly routable address

DHCP
→ Automatically provides network configuration

DORA
→ Discover → Offer → Request → Acknowledge

DEFAULT GATEWAY
→ Router used to reach outside the local subnet

NAT
→ Translates IP addresses between network contexts
→ Commonly allows private IPv4 hosts to share public IPv4 addresses

ARP
→ IPv4 address → MAC address

NDP
→ IPv6 neighbor/router discovery functions

LOOPBACK
→ IPv4: 127.0.0.1
→ IPv6: ::1

IPv4 LINK-LOCAL
→ 169.254.0.0/16

IPv6 LINK-LOCAL
→ FE80::/10

NETWORK ADDRESS
→ Identifies subnet

BROADCAST ADDRESS
→ Reaches all hosts in an IPv4 subnet

UNICAST
→ One destination

MULTICAST
→ Group of destinations

ANYCAST
→ One appropriate/nearest destination from a group
```

---

# 48. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
IPv4
IPv6
IPv4 vs IPv6
IP Address
Private vs Public IP
Static vs Dynamic IP
Subnet Mask
CIDR
Subnetting
Default Gateway
NAT
DHCP + DORA
ARP vs NDP
Network Address
Broadcast Address
Loopback Address
```

## ⭐⭐⭐ Good to Know

```text
IPv6 Address Compression
IPv6 Unicast/Multicast/Anycast
Link-Local Addresses
APIPA
Classful Addressing
Class A/B/C
```

> **For placement interviews, focus deeply on IPv4 addressing, subnetting, CIDR, private/public IPs, DHCP, NAT, IPv4 vs IPv6, default gateway, and ARP/NDP. These are the highest-value concepts from IP addressing.**