# Computer Networks – Important Interview Questions

This file contains the **most important and frequently asked Computer Networks interview questions**.

If you are short on time before an interview, prioritize the questions marked with ⭐⭐⭐⭐⭐.

---

# 1. Computer Networks Basics

### ⭐⭐⭐⭐⭐ 1. What is a Computer Network?

A **computer network** is a collection of interconnected devices that communicate and share data and resources with each other.

Examples:

```text
Computers
Servers
Routers
Switches
Printers
Mobile Devices
```

---

### ⭐⭐⭐⭐⭐ 2. What are the different types of networks?

Common types:

```text
PAN → Personal Area Network
LAN → Local Area Network
MAN → Metropolitan Area Network
WAN → Wide Area Network
```

---

### ⭐⭐⭐⭐⭐ 3. What is the difference between LAN and WAN?

```text
LAN
→ Smaller geographical area
→ Usually faster
→ Example: Office/Home network

WAN
→ Large geographical area
→ Connects multiple networks
→ Example: Internet
```

---

### ⭐⭐⭐⭐⭐ 4. What is a protocol?

A **protocol** is a set of rules that defines how devices communicate over a network.

Examples:

```text
HTTP
TCP
IP
DNS
FTP
SMTP
```

---

# 2. OSI and TCP/IP Models

### ⭐⭐⭐⭐⭐ 5. What is the OSI model?

The **OSI (Open Systems Interconnection) model** is a conceptual seven-layer model used to understand network communication.

```text
7 → Application
6 → Presentation
5 → Session
4 → Transport
3 → Network
2 → Data Link
1 → Physical
```

---

### ⭐⭐⭐⭐⭐ 6. Explain all seven layers of the OSI model.

```text
Application
→ Network services to applications

Presentation
→ Data representation, encryption, compression

Session
→ Session establishment and management

Transport
→ End-to-end/process communication

Network
→ Routing and logical addressing

Data Link
→ Frames and MAC-based local delivery

Physical
→ Transmission of raw bits
```

---

### ⭐⭐⭐⭐⭐ 7. What is the TCP/IP model?

The TCP/IP model is the practical protocol architecture used by the Internet.

Common four-layer representation:

```text
Application
Transport
Internet
Network Access
```

---

### ⭐⭐⭐⭐⭐ 8. OSI vs TCP/IP model?

| OSI | TCP/IP |
|---|---|
| 7 layers | Commonly represented as 4 layers |
| Conceptual/reference model | Practical Internet protocol architecture |
| Developed by ISO | Developed around DARPA/Internet protocols |
| Session and Presentation are separate | Generally included in Application layer |

---

### ⭐⭐⭐⭐⭐ 9. What are the devices associated with different network layers?

Common interview mapping:

```text
Physical
→ Hub / Repeater

Data Link
→ Switch / Bridge

Network
→ Router

Transport
→ Usually implemented in end hosts
```

> Modern networking devices can operate across multiple layers, so this is a simplified interview mapping.

---

# 3. Physical and Data Link Layer

### ⭐⭐⭐⭐ 10. What is a MAC address?

A **MAC address** is a link-layer address used to identify a network interface on a local network.

Common Ethernet MAC addresses are:

```text
48 bits
```

Example:

```text
00:1A:2B:3C:4D:5E
```

---

### ⭐⭐⭐⭐⭐ 11. MAC address vs IP address?

```text
MAC Address
→ Data Link Layer
→ Local/link-level addressing

IP Address
→ Network Layer
→ Logical addressing and routing
```

---

### ⭐⭐⭐⭐⭐ 12. What is a switch?

A **switch** connects devices within a local network and forwards Ethernet frames based primarily on MAC addresses.

```text
Computer A ─┐
Computer B ─┼── Switch
Computer C ─┘
```

---

### ⭐⭐⭐⭐⭐ 13. What is a router?

A **router** connects different IP networks and forwards packets based on destination IP addresses and routing information.

```text
LAN
 ↓
Router
 ↓
Internet
```

---

### ⭐⭐⭐⭐⭐ 14. Switch vs Router?

| Switch | Router |
|---|---|
| Mainly operates at Layer 2 | Mainly operates at Layer 3 |
| Uses MAC addresses | Uses IP addresses |
| Connects devices within networks | Connects different networks |
| Forwards frames | Forwards packets |

---

### ⭐⭐⭐⭐ 15. What is a hub?

A **hub** is a Layer 1 device that repeats incoming signals to other ports.

It does not intelligently forward traffic based on MAC addresses.

---

### ⭐⭐⭐⭐ 16. Hub vs Switch?

```text
Hub
→ Broadcasts/repeats traffic to ports

Switch
→ Learns MAC addresses
→ Forwards frames toward the appropriate port
```

---

### ⭐⭐⭐⭐ 17. What is ARP?

**ARP (Address Resolution Protocol)** is used in IPv4 local networks to determine the MAC address associated with an IPv4 address.

Example:

```text
IP Address
   ↓
ARP
   ↓
MAC Address
```

---

### ⭐⭐⭐⭐⭐ 18. What is a broadcast?

A broadcast is communication intended for all hosts within the relevant broadcast domain.

Example:

```text
Sender
 ↓
All hosts in broadcast domain
```

---

### ⭐⭐⭐⭐ 19. What is a collision domain?

A **collision domain** is a network segment where simultaneous transmissions can potentially interfere with each other in technologies where collisions are possible.

Modern switched full-duplex Ethernet largely eliminates collisions on individual switch links.

---

### ⭐⭐⭐⭐ 20. What is a broadcast domain?

A **broadcast domain** is the set of devices that receive a Layer 2 broadcast.

Routers normally separate broadcast domains.

---

# 4. IP Addressing

### ⭐⭐⭐⭐⭐ 21. What is an IP address?

An **IP address** is a logical network-layer address used to identify an interface and support communication across IP networks.

---

### ⭐⭐⭐⭐⭐ 22. What is IPv4?

IPv4 uses:

```text
32-bit addresses
```

Example:

```text
192.168.1.10
```

---

### ⭐⭐⭐⭐⭐ 23. What is IPv6?

IPv6 uses:

```text
128-bit addresses
```

Example:

```text
2001:db8::1
```

---

### ⭐⭐⭐⭐⭐ 24. IPv4 vs IPv6?

| IPv4 | IPv6 |
|---|---|
| 32-bit | 128-bit |
| Dotted decimal notation | Hexadecimal notation |
| Smaller address space | Much larger address space |
| Uses ARP for IPv4 address resolution | Uses Neighbor Discovery |
| Broadcast supported | No broadcast; multicast/anycast are used |

---

### ⭐⭐⭐⭐⭐ 25. What is a private IP address?

Private IPv4 addresses are used inside private networks and are not directly routable on the public Internet.

Ranges:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

---

### ⭐⭐⭐⭐⭐ 26. What is a public IP address?

A public IP address is an address that can be routed on the public Internet, subject to Internet routing and allocation policies.

---

### ⭐⭐⭐⭐⭐ 27. What is localhost?

`localhost` refers to the local machine.

IPv4 loopback:

```text
127.0.0.1
```

IPv6 loopback:

```text
::1
```

---

### ⭐⭐⭐⭐⭐ 28. What is subnetting?

**Subnetting** divides an IP network into smaller logical networks called subnets.

Benefits include:

```text
Efficient address usage
Network organization
Traffic isolation
Routing control
```

---

### ⭐⭐⭐⭐⭐ 29. What is a subnet mask?

A subnet mask indicates which part of an IPv4 address represents the network prefix and which part represents host bits.

Example:

```text
IP:
192.168.1.10

Mask:
255.255.255.0

CIDR:
192.168.1.10/24
```

---

### ⭐⭐⭐⭐⭐ 30. What is CIDR?

**CIDR (Classless Inter-Domain Routing)** represents an IP network using a prefix length.

Example:

```text
192.168.1.0/24
```

Here:

```text
/24
→ First 24 bits are the network prefix
```

---

### ⭐⭐⭐⭐ 31. What is a default gateway?

A **default gateway** is the router/interface a host uses to reach destinations outside its local IP network.

```text
Computer
   ↓
Default Gateway
   ↓
Other Network
```

---

### ⭐⭐⭐⭐ 32. What is NAT?

**NAT (Network Address Translation)** modifies IP addressing information as packets pass through a network device.

A common use is allowing multiple private hosts to share a public IPv4 address.

```text
Private Network
      ↓
     NAT
      ↓
Public Internet
```

---

# 5. Routing and Network Layer

### ⭐⭐⭐⭐⭐ 33. What is routing?

Routing is the process of determining paths for packets to travel from a source network toward a destination network.

---

### ⭐⭐⭐⭐⭐ 34. What is a routing table?

A routing table contains information used by a router to determine where packets should be forwarded.

Conceptually:

```text
Destination Network
        ↓
Next Hop / Interface
```

---

### ⭐⭐⭐⭐⭐ 35. What is the difference between routing and forwarding?

```text
Routing
→ Determines the path / builds routing information

Forwarding
→ Sends each packet to the appropriate next hop/interface
```

---

### ⭐⭐⭐⭐ 36. What is a routing protocol?

A routing protocol allows routers to exchange information and determine routes.

Examples:

```text
RIP
OSPF
BGP
```

---

### ⭐⭐⭐⭐⭐ 37. What is the difference between RIP, OSPF and BGP?

```text
RIP
→ Distance-vector
→ Uses hop count

OSPF
→ Link-state
→ Commonly used within an autonomous system

BGP
→ Path-vector
→ Used for inter-domain routing
```

For placements, know the basic purpose rather than every protocol detail.

---

### ⭐⭐⭐⭐ 38. What is TTL?

**TTL (Time To Live)** is an IP header field that limits how long a packet can remain in a routed network.

In IPv4, routers decrement TTL as the packet is forwarded.

When it reaches zero, the packet is discarded.

This helps prevent packets from circulating indefinitely.

---

### ⭐⭐⭐⭐⭐ 39. What is ICMP?

**ICMP (Internet Control Message Protocol)** is used for network-layer control, diagnostics, and error reporting.

Examples:

```text
Ping
Traceroute-related messages
Destination Unreachable
Time Exceeded
```

---

### ⭐⭐⭐⭐⭐ 40. What is ping?

`ping` commonly uses ICMP Echo Request and Echo Reply messages to test reachability and measure round-trip time.

```text
Host A
  ↓
ICMP Echo Request
  ↓
Host B
  ↓
ICMP Echo Reply
  ↓
Host A
```

---

### ⭐⭐⭐⭐⭐ 41. What is traceroute?

`traceroute`/`tracert` is used to discover the sequence of network hops toward a destination.

It commonly works by manipulating TTL/hop-limit values and observing router responses.

---

# 6. Transport Layer

### ⭐⭐⭐⭐⭐ 42. What is the Transport Layer?

The Transport Layer provides communication between processes/applications running on different hosts.

Main concepts:

```text
TCP
UDP
Ports
Reliability
Flow Control
Congestion Control
```

---

### ⭐⭐⭐⭐⭐ 43. TCP vs UDP?

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable delivery | No TCP-style reliability |
| Ordered byte stream | Datagram-oriented |
| Retransmission | No built-in retransmission |
| Flow control | No TCP-style flow control |
| Congestion control | No TCP-style congestion control |
| More overhead | Lower overhead |

---

### ⭐⭐⭐⭐⭐ 44. Why is TCP reliable?

TCP provides reliability using mechanisms such as:

```text
Sequence Numbers
Acknowledgments
Retransmissions
Checksums
```

---

### ⭐⭐⭐⭐⭐ 45. What is a TCP three-way handshake?

```text
Client                    Server

  | -------- SYN --------> |
  | <------ SYN-ACK ------ |
  | -------- ACK --------> |
```

It establishes TCP connection state and synchronizes sequence-number state between the endpoints.

---

### ⭐⭐⭐⭐⭐ 46. Why does TCP use a three-way handshake?

It allows both sides to:

```text
Establish connection state
Synchronize sequence numbers
Confirm bidirectional reachability
```

---

### ⭐⭐⭐⭐⭐ 47. What are SYN, ACK and FIN?

```text
SYN
→ Used to initiate/synchronize a TCP connection

ACK
→ Acknowledges received data/control information

FIN
→ Indicates a side has finished sending data
```

---

### ⭐⭐⭐⭐ 48. What is TCP connection termination?

A graceful TCP close commonly involves:

```text
FIN
ACK
FIN
ACK
```

Each direction of the connection is closed independently.

---

### ⭐⭐⭐⭐⭐ 49. What is a port number?

A port number identifies a transport-layer endpoint associated with an application/process.

Range:

```text
0–65535
```

---

### ⭐⭐⭐⭐⭐ 50. What is a socket?

A socket is a communication endpoint used by an application.

Conceptually:

```text
IP Address + Port + Transport Protocol
```

---

### ⭐⭐⭐⭐⭐ 51. What is flow control?

Flow control prevents a sender from overwhelming the receiver.

```text
Sender
  ↓
Receiver Capacity
  ↓
Controlled Sending
```

---

### ⭐⭐⭐⭐⭐ 52. What is congestion control?

Congestion control adjusts sending behavior to help prevent excessive network congestion.

---

### ⭐⭐⭐⭐⭐ 53. Flow control vs congestion control?

```text
Flow Control
→ Protects receiver

Congestion Control
→ Helps protect network from overload
```

---

# 7. Application Layer

### ⭐⭐⭐⭐⭐ 54. What is HTTP?

**HTTP** is an application-layer protocol used for communication between web clients and servers.

Common port:

```text
80
```

---

### ⭐⭐⭐⭐⭐ 55. What is HTTPS?

HTTPS is HTTP secured using **TLS**.

Common port:

```text
443
```

It provides:

```text
Encryption
Authentication
Integrity
```

---

### ⭐⭐⭐⭐⭐ 56. HTTP vs HTTPS?

```text
HTTP
→ No TLS protection
→ Commonly port 80

HTTPS
→ HTTP + TLS
→ Commonly port 443
→ Secure communication
```

---

### ⭐⭐⭐⭐⭐ 57. What is DNS?

**DNS (Domain Name System)** translates domain names into IP addresses and provides other DNS information.

Example:

```text
google.com
     ↓
DNS
     ↓
IP Address
```

---

### ⭐⭐⭐⭐⭐ 58. What are important DNS records?

```text
A
→ IPv4 address

AAAA
→ IPv6 address

CNAME
→ Alias

MX
→ Mail server

NS
→ Name server

TXT
→ Text/policy/verification information
```

---

### ⭐⭐⭐⭐⭐ 59. How does DNS resolution work?

Simplified:

```text
Browser
   ↓
DNS Resolver
   ↓
DNS hierarchy
   ↓
IP Address
   ↓
Server connection
```

---

### ⭐⭐⭐⭐⭐ 60. What is DHCP?

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration to clients.

It can provide:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

---

### ⭐⭐⭐⭐⭐ 61. What is DHCP DORA?

```text
D → Discover
O → Offer
R → Request
A → Acknowledgment
```

---

### ⭐⭐⭐⭐⭐ 62. What are the common DHCP ports?

```text
Server → UDP 67
Client → UDP 68
```

---

### ⭐⭐⭐⭐ 63. What is FTP?

**FTP** is a protocol used for file transfer.

Traditional FTP uses:

```text
TCP 21 → Control
TCP 20 → Data in traditional active mode
```

---

### ⭐⭐⭐⭐ 64. What is SMTP?

**SMTP** is used primarily for sending/submitting and relaying email.

Common ports:

```text
25
587
465
```

---

### ⭐⭐⭐⭐ 65. POP3 vs IMAP?

```text
POP3
→ Primarily retrieves/downloads mail

IMAP
→ Accesses and synchronizes mail on the server
```

---

### ⭐⭐⭐⭐ 66. What is SSH?

**SSH** provides secure remote access and command execution.

Common port:

```text
TCP 22
```

---

### ⭐⭐⭐⭐ 67. SSH vs Telnet?

```text
SSH
→ Encrypted
→ TCP 22

Telnet
→ Not encrypted
→ TCP 23
```

---

# 8. URL and Web Communication

### ⭐⭐⭐⭐⭐ 68. What happens when you enter a URL in a browser?

Example:

```text
https://example.com
```

Simplified flow:

```text
URL entered
     ↓
DNS resolution
     ↓
Find server IP
     ↓
Transport connection
     ↓
TLS handshake
     ↓
HTTP request
     ↓
Server response
     ↓
Browser renders page
```

For HTTP/3:

```text
DNS
 ↓
QUIC over UDP
 ↓
HTTP/3
```

---

### ⭐⭐⭐⭐ 69. What is HTTP statelessness?

HTTP is traditionally considered stateless because the protocol does not inherently maintain application session state between independent requests.

State can be maintained using:

```text
Cookies
Sessions
Tokens
```

---

# 9. Network Security

### ⭐⭐⭐⭐⭐ 70. What is the CIA Triad?

```text
C → Confidentiality
I → Integrity
A → Availability
```

```text
Confidentiality
→ Prevent unauthorized access

Integrity
→ Prevent unauthorized modification

Availability
→ Keep systems/services accessible
```

---

### ⭐⭐⭐⭐⭐ 71. Authentication vs Authorization?

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

### ⭐⭐⭐⭐⭐ 72. Encryption vs Hashing?

```text
Encryption
→ Reversible with appropriate key
→ Used for confidentiality

Hashing
→ One-way transformation
→ Used for integrity/password-related applications
```

---

### ⭐⭐⭐⭐⭐ 73. Symmetric vs Asymmetric encryption?

```text
Symmetric
→ Same secret key
→ Faster
→ AES

Asymmetric
→ Public + Private key
→ RSA/ECC
```

---

### ⭐⭐⭐⭐⭐ 74. What is a firewall?

A firewall controls network traffic according to configured security rules.

It can filter based on:

```text
IP
Port
Protocol
Connection state
Application characteristics
```

---

### ⭐⭐⭐⭐⭐ 75. IDS vs IPS?

```text
IDS
→ Detects suspicious activity
→ Alerts

IPS
→ Detects suspicious activity
→ Can block/prevent it
```

---

### ⭐⭐⭐⭐⭐ 76. What is a VPN?

A VPN creates a protected communication path over an untrusted network.

```text
Device
   ↓
Protected Tunnel
   ↓
VPN Server
```

---

# 10. Common Network Attacks

### ⭐⭐⭐⭐⭐ 77. What is a Man-in-the-Middle attack?

An attacker positions themselves between two communicating parties to intercept or potentially manipulate communication.

```text
Client
   ↓
Attacker
   ↓
Server
```

---

### ⭐⭐⭐⭐⭐ 78. What is phishing?

Phishing is a social-engineering attack that tricks users into revealing sensitive information or performing an unwanted action.

---

### ⭐⭐⭐⭐⭐ 79. What is spoofing?

Spoofing means falsifying or impersonating an identity/source.

Examples:

```text
IP Spoofing
MAC Spoofing
DNS Spoofing
Email Spoofing
```

---

### ⭐⭐⭐⭐⭐ 80. What is DoS?

**Denial of Service** attempts to make a service unavailable to legitimate users.

---

### ⭐⭐⭐⭐⭐ 81. What is DDoS?

**Distributed Denial of Service** uses many distributed systems to attack a target and make its service unavailable.

---

### ⭐⭐⭐⭐⭐ 82. DoS vs DDoS?

```text
DoS
→ Attack from one/limited source

DDoS
→ Attack from many distributed sources
```

---

### ⭐⭐⭐⭐ 83. What is ARP spoofing?

An attacker sends forged ARP information to associate their MAC address with another IP address, such as the gateway.

This can enable:

```text
Traffic interception
Traffic modification
Denial of service
```

---

### ⭐⭐⭐⭐ 84. What is DNS spoofing?

DNS spoofing involves causing a domain name to resolve to an unintended or malicious destination.

---

### ⭐⭐⭐⭐ 85. What is a brute-force attack?

A brute-force attack attempts many possible credentials until a valid one is found.

---

### ⭐⭐⭐⭐ 86. What is a replay attack?

A replay attack captures valid communication and retransmits it later in an attempt to make it accepted again.

---

### ⭐⭐⭐⭐⭐ 87. What is SQL Injection?

SQL Injection occurs when untrusted input is improperly incorporated into SQL queries, allowing an attacker to alter the intended query.

Prevention:

```text
Parameterized Queries
Prepared Statements
Input Validation
Least Privilege
```

---

### ⭐⭐⭐⭐⭐ 88. What is XSS?

**Cross-Site Scripting (XSS)** occurs when malicious script content executes in a victim's browser through a vulnerable web application.

---

### ⭐⭐⭐⭐⭐ 89. What is CSRF?

**Cross-Site Request Forgery (CSRF)** tricks a user's browser into sending an unwanted authenticated request to a website.

---

### ⭐⭐⭐⭐⭐ 90. XSS vs CSRF?

```text
XSS
→ Malicious script executes in the browser

CSRF
→ Tricks authenticated browser into sending an unwanted request
```

---

# 11. Frequently Asked Scenario Questions

### ⭐⭐⭐⭐⭐ 91. How would you troubleshoot if a website is not opening?

A good troubleshooting sequence:

```text
1. Check network connection
2. Check DNS resolution
3. Check IP connectivity
4. Check routing
5. Check port connectivity
6. Check HTTP/HTTPS response
7. Check firewall/security rules
8. Check server/application availability
```

Useful tools:

```text
ping
nslookup / dig
traceroute / tracert
curl
```

---

### ⭐⭐⭐⭐⭐ 92. A website works using an IP address but not using its domain name. What could be wrong?

Likely investigate:

```text
DNS resolution
DNS records
DNS cache
DNS configuration
```

---

### ⭐⭐⭐⭐⭐ 93. You can ping a server but cannot open the website. What could be wrong?

Possible causes:

```text
Web server unavailable
Port 80/443 blocked
Firewall rules
Application failure
Incorrect service configuration
TLS problems
```

Important point:

```text
Ping working
≠
HTTP/HTTPS working
```

They use different protocols and services.

---

### ⭐⭐⭐⭐⭐ 94. Why can two computers in the same network communicate without a router?

If both hosts are in the same IP subnet, they can communicate directly at the local network layer after resolving the destination MAC address.

A router is needed when communicating with another IP network.

---

### ⭐⭐⭐⭐⭐ 95. What happens when two devices are in different networks?

Conceptually:

```text
Device A
   ↓
Default Gateway
   ↓
Router(s)
   ↓
Destination Network
   ↓
Device B
```

---

### ⭐⭐⭐⭐⭐ 96. Why do we need a default gateway?

The default gateway provides the next-hop router used when the destination is outside the host's local subnet.

---

### ⭐⭐⭐⭐⭐ 97. Why is DNS usually UDP?

DNS commonly uses UDP because it has:

```text
Low overhead
No connection establishment
Fast request/response communication
```

TCP is also used when required, such as for some larger responses and zone transfers.

---

### ⭐⭐⭐⭐⭐ 98. Why does HTTP/3 use UDP?

HTTP/3 uses **QUIC**, which runs over UDP.

QUIC provides transport features such as:

```text
Reliable delivery
Stream multiplexing
Connection management
TLS integration
```

while avoiding some limitations of traditional TCP-based HTTP transport.

---

### ⭐⭐⭐⭐⭐ 99. Why is TCP called reliable but UDP unreliable?

TCP provides:

```text
Acknowledgments
Sequence numbers
Retransmissions
Ordering
Flow control
Congestion control
```

UDP does not provide TCP-style reliability and ordering mechanisms.

---

### ⭐⭐⭐⭐⭐ 100. Which is better: TCP or UDP?

There is no universally better protocol.

```text
TCP
→ When reliable, ordered delivery is important

UDP
→ When low overhead/timeliness is important and the application can tolerate or handle loss
```

The correct choice depends on the application requirements.

---

# 12. Rapid-Fire Interview Questions

These are useful for **last-minute revision**.

```text
101. What is a MAC address?
102. What is an IP address?
103. What is a subnet mask?
104. What is CIDR?
105. What is a default gateway?
106. What is NAT?
107. What is ARP?
108. What is ICMP?
109. What is TTL?
110. What is a routing table?
111. What is a routing protocol?
112. RIP vs OSPF vs BGP?
113. What is a port?
114. What is a socket?
115. What is a TCP segment?
116. What is a UDP datagram?
117. What is a sequence number?
118. What is an ACK?
119. What is flow control?
120. What is congestion control?
121. What is the TCP three-way handshake?
122. What is TCP connection termination?
123. What is DNS?
124. What is DHCP?
125. What is DHCP DORA?
126. What is HTTP?
127. What is HTTPS?
128. What is TLS?
129. What is FTP?
130. What is SMTP?
131. What is POP3?
132. What is IMAP?
133. What is SSH?
134. What is Telnet?
135. What is a firewall?
136. What is IDS?
137. What is IPS?
138. What is a VPN?
139. What is MITM?
140. What is phishing?
141. What is spoofing?
142. What is DoS?
143. What is DDoS?
144. What is SQL Injection?
145. What is XSS?
146. What is CSRF?
147. What happens when you enter a URL?
148. HTTP vs HTTPS?
149. TCP vs UDP?
150. Switch vs Router?
```

---

# 13. Top 30 Questions to Never Skip

If you have **very little time**, prepare these first:

```text
1. ⭐⭐⭐⭐⭐ What is the OSI model?

2. ⭐⭐⭐⭐⭐ Explain all seven OSI layers.

3. ⭐⭐⭐⭐⭐ OSI vs TCP/IP?

4. ⭐⭐⭐⭐⭐ TCP vs UDP?

5. ⭐⭐⭐⭐⭐ What is the TCP three-way handshake?

6. ⭐⭐⭐⭐⭐ Why does TCP use a three-way handshake?

7. ⭐⭐⭐⭐⭐ How does TCP provide reliability?

8. ⭐⭐⭐⭐⭐ What are sequence numbers and ACKs?

9. ⭐⭐⭐⭐⭐ Flow control vs congestion control?

10. ⭐⭐⭐⭐⭐ What is a port?

11. ⭐⭐⭐⭐⭐ What is a socket?

12. ⭐⭐⭐⭐⭐ MAC address vs IP address?

13. ⭐⭐⭐⭐⭐ Switch vs Router?

14. ⭐⭐⭐⭐⭐ What is ARP?

15. ⭐⭐⭐⭐⭐ What is an IP address?

16. ⭐⭐⭐⭐⭐ IPv4 vs IPv6?

17. ⭐⭐⭐⭐⭐ What is subnetting?

18. ⭐⭐⭐⭐⭐ What is CIDR?

19. ⭐⭐⭐⭐⭐ What is a default gateway?

20. ⭐⭐⭐⭐⭐ What is NAT?

21. ⭐⭐⭐⭐⭐ What is routing?

22. ⭐⭐⭐⭐⭐ What is DNS?

23. ⭐⭐⭐⭐⭐ How does DNS resolution work?

24. ⭐⭐⭐⭐⭐ What is DHCP and DORA?

25. ⭐⭐⭐⭐⭐ HTTP vs HTTPS?

26. ⭐⭐⭐⭐⭐ What happens when you enter a URL?

27. ⭐⭐⭐⭐⭐ Authentication vs Authorization?

28. ⭐⭐⭐⭐⭐ Encryption vs Hashing?

29. ⭐⭐⭐⭐⭐ What is a firewall?

30. ⭐⭐⭐⭐⭐ DoS vs DDoS?
```

---

# 14. Final One-Page Revision

```text
OSI
→ 7 layers

TCP/IP
→ Application
→ Transport
→ Internet
→ Network Access

MAC
→ Layer 2
→ Local network addressing

IP
→ Layer 3
→ Logical addressing/routing

SWITCH
→ Mainly Layer 2
→ MAC address
→ Frames

ROUTER
→ Mainly Layer 3
→ IP address
→ Packets

ARP
→ IPv4 address → MAC address

IPv4
→ 32-bit

IPv6
→ 128-bit

SUBNETTING
→ Divide network into smaller networks

CIDR
→ /24, /16, etc.

DEFAULT GATEWAY
→ Router for outside local subnet

NAT
→ Translates IP addressing

ICMP
→ Diagnostics/control

PING
→ ICMP Echo

TRACEROUTE
→ Discover path/hops

TCP
→ Reliable
→ Ordered
→ Connection-oriented

UDP
→ Connectionless
→ Lower overhead

TCP HANDSHAKE
→ SYN
→ SYN-ACK
→ ACK

TCP CLOSE
→ FIN / ACK exchange

PORT
→ Application/process endpoint
→ 0–65535

DNS
→ Domain name resolution
→ Port 53

DHCP
→ Network configuration
→ UDP 67/68
→ DORA

HTTP
→ Web
→ Port 80 commonly

HTTPS
→ HTTP + TLS
→ Port 443 commonly

FTP
→ File transfer
→ TCP

SMTP
→ Send/relay email

POP3
→ Retrieve email

IMAP
→ Synchronize/access email

SSH
→ Secure remote access
→ TCP 22

TELNET
→ Remote access
→ TCP 23
→ Not encrypted

FIREWALL
→ Controls traffic

IDS
→ Detect

IPS
→ Detect + Prevent

VPN
→ Protected tunnel

CIA
→ Confidentiality
→ Integrity
→ Availability

AUTHENTICATION
→ Who are you?

AUTHORIZATION
→ What can you do?

ENCRYPTION
→ Confidentiality

HASHING
→ One-way transformation

MITM
→ Intercept communication

PHISHING
→ Trick users

SPOOFING
→ Fake identity/source

DoS
→ Deny service

DDoS
→ Distributed DoS

SQL INJECTION
→ Manipulate SQL through unsafe input

XSS
→ Malicious script in browser

CSRF
→ Unwanted authenticated request
```

---

# 15. Interview Preparation Priority

## 🔥 Priority 1 — Must Know

```text
OSI Model
TCP/IP Model
TCP vs UDP
TCP Three-Way Handshake
TCP Reliability
Sequence Numbers
ACK
Flow Control
Congestion Control
IP Addressing
IPv4 vs IPv6
MAC vs IP
Switch vs Router
ARP
Subnetting
CIDR
Default Gateway
NAT
Routing
DNS
DHCP + DORA
HTTP vs HTTPS
URL Request Flow
Ports
Sockets
```

## 🔥 Priority 2 — Very Important

```text
ICMP
Ping
Traceroute
RIP / OSPF / BGP basics
HTTP Methods
HTTP Status Codes
FTP
SMTP
POP3
IMAP
SSH
Firewall
CIA Triad
Authentication vs Authorization
Encryption vs Hashing
Symmetric vs Asymmetric Encryption
IDS vs IPS
VPN
```

## 🔥 Priority 3 — Good to Know

```text
HTTP/2
HTTP/3
QUIC
DNS Records
DNS Caching
ARP Spoofing
DNS Spoofing
MITM
Phishing
DoS/DDoS
SQL Injection
XSS
CSRF
Replay Attack
Session Hijacking
```

> **If you prepare the Priority 1 topics thoroughly and can explain the Top 30 questions confidently, you will have covered the core Computer Networks concepts most commonly tested in software placement interviews.**