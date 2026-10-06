# Computer Networks – Top 25 Interview Questions & Answers
## System Engineer / Fresher Interview Preparation
### Infosys SE / Capgemini Exceller Focus

---

## 🟢 BASIC LEVEL

### 1. What is a Computer Network?

**Answer:**

A computer network is a group of interconnected devices that communicate with each other and share data and resources.

Devices can communicate using wired or wireless connections and follow communication protocols.

**Examples:**
- Computers connected in an office
- Mobile phones connected through Wi-Fi
- Servers communicating over the Internet

**Interview follow-up:** What are the advantages of computer networks?

---

### 2. What are the main types of Computer Networks?

**Answer:**

Common types are:

- **PAN (Personal Area Network)** – Small network around a person, such as Bluetooth devices.
- **LAN (Local Area Network)** – Network within a small area such as a home, office, or college.
- **MAN (Metropolitan Area Network)** – Covers a city or large campus.
- **WAN (Wide Area Network)** – Covers large geographical areas. The Internet is the largest example.

**Easy order:**

`PAN → LAN → MAN → WAN`

---

### 3. What is a Protocol?

**Answer:**

A protocol is a set of rules that defines how devices communicate and exchange data over a network.

Protocols define things such as:

- How data is formatted
- How data is transmitted
- How devices identify each other
- How errors are handled

**Examples:**

HTTP, HTTPS, TCP, UDP, IP, DNS, FTP.

---

### 4. What is the OSI Model?

**Answer:**

The OSI (Open Systems Interconnection) model is a conceptual framework that divides network communication into seven layers.

The seven layers are:

1. **Physical**
2. **Data Link**
3. **Network**
4. **Transport**
5. **Session**
6. **Presentation**
7. **Application**

**Mnemonic:**

> Please Do Not Throw Sausage Pizza Away

**Interview point:**

The OSI model helps us understand and troubleshoot how data travels through a network.

---

### 5. Explain the seven layers of the OSI Model.

**Answer:**

### 1. Physical Layer

Transmits raw bits over the physical medium.

**Examples:** Cables, signals, connectors.

### 2. Data Link Layer

Provides node-to-node communication and handles MAC addressing and frame delivery.

**Example:** Ethernet.

### 3. Network Layer

Responsible for logical addressing and routing packets between networks.

**Example:** IP.

### 4. Transport Layer

Provides end-to-end communication and controls reliability, flow, and segmentation.

**Examples:** TCP, UDP.

### 5. Session Layer

Establishes, manages, and terminates communication sessions.

### 6. Presentation Layer

Handles data translation, encryption/decryption, and compression.

### 7. Application Layer

Provides network services directly to applications.

**Examples:** HTTP, DNS, FTP, SMTP.

---

### 6. What is the TCP/IP Model?

**Answer:**

The TCP/IP model is the practical networking model used by the Internet.

Its commonly described four layers are:

1. **Network Access / Link Layer**
2. **Internet Layer**
3. **Transport Layer**
4. **Application Layer**

Examples:

- Network Access → Ethernet, Wi-Fi
- Internet → IP
- Transport → TCP, UDP
- Application → HTTP, DNS, SMTP

---

### 7. What is the difference between OSI and TCP/IP models?

**Answer:**

| OSI | TCP/IP |
|---|---|
| Seven layers | Commonly represented using four layers |
| Conceptual/reference model | Practical Internet protocol suite |
| Developed by ISO | Developed around DARPA/Internet protocols |
| Session and Presentation are separate | Their functions are generally included in Application |
| Transport and Network are separate | Transport and Internet are separate |

**Interview point:**

OSI is mainly useful for understanding networking concepts, while TCP/IP represents the protocols used in real-world Internet communication.

---

### 8. What is an IP Address?

**Answer:**

An IP address is a logical address assigned to a device or network interface so that it can be identified and reached over an IP network.

There are two major versions:

### IPv4

Uses 32 bits.

Example:

`192.168.1.10`

### IPv6

Uses 128 bits.

Example:

`2001:db8::1`

**Why is it required?**

It helps devices identify the source and destination of network communication.

---

## 🟡 MEDIUM LEVEL

### 9. What is the difference between IPv4 and IPv6?

**Answer:**

| IPv4 | IPv6 |
|---|---|
| 32-bit address | 128-bit address |
| Smaller address space | Much larger address space |
| Written in decimal notation | Written in hexadecimal notation |
| Example: 192.168.1.1 | Example: 2001:db8::1 |
| Uses broadcast | Does not use traditional broadcast |
| Address exhaustion is a concern | Provides a vastly larger address space |

**Important point:**

IPv6 was introduced mainly to provide a much larger address space and improve modern Internet addressing.

---

### 10. What is the difference between MAC Address and IP Address?

**Answer:**

A **MAC address** is a hardware/link-layer address associated with a network interface.

An **IP address** is a logical network-layer address used for communication across networks.

| MAC Address | IP Address |
|---|---|
| Data Link Layer | Network Layer |
| Used for local network delivery | Used for routing between networks |
| Typically associated with a network interface | Can change depending on network configuration |
| Example: `00:1A:2B:3C:4D:5E` | Example: `192.168.1.10` |

**Simple example:**

IP helps determine where a device is on the network, while MAC helps identify the interface for local delivery.

---

### 11. What is a Port Number?

**Answer:**

A port number is a logical number used by the transport layer to identify a specific application or service on a device.

A combination such as:

`IP Address + Port Number`

helps identify a network endpoint.

**Common ports:**

- HTTP → 80
- HTTPS → 443
- FTP → 21
- SSH → 22
- DNS → 53

**Example:**

When a browser connects to an HTTPS server, it normally communicates with port 443.

---

### 12. What is TCP?

**Answer:**

TCP (Transmission Control Protocol) is a connection-oriented transport-layer protocol that provides reliable and ordered delivery of data.

Important characteristics:

- Connection-oriented
- Reliable delivery
- Ordered data
- Error detection/recovery mechanisms
- Flow control
- Congestion control

TCP is useful when reliable delivery is important.

**Examples:**

Web traffic using HTTP/HTTPS, file transfers, and many application protocols can use TCP.

---

### 13. What is UDP?

**Answer:**

UDP (User Datagram Protocol) is a connectionless transport-layer protocol that provides a lightweight way to send datagrams without TCP's connection setup and reliability mechanisms.

Characteristics:

- Connectionless
- Low overhead
- No guarantee of delivery
- No guarantee of ordering
- Faster for applications that can tolerate some loss

**Examples:**

DNS commonly uses UDP for many queries, and real-time applications such as streaming or online gaming may use UDP where low latency is important.

---

### 14. What is the difference between TCP and UDP?

**Answer:**

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable delivery | No built-in delivery guarantee |
| Ordered delivery | No built-in ordering guarantee |
| Higher overhead | Lower overhead |
| Uses flow and congestion control | Does not provide TCP-style flow/congestion control |
| Suitable when reliability is important | Suitable when low overhead/latency is important |

**Interview example:**

If an application cannot tolerate missing or reordered data, TCP is often preferred.

If low latency is more important and the application can handle loss itself, UDP may be preferred.

---

### 15. What is the TCP Three-Way Handshake?

**Answer:**

The TCP three-way handshake establishes a TCP connection between a client and server.

The steps are:

### Step 1: SYN

The client sends a SYN packet to request a connection.

### Step 2: SYN-ACK

The server responds with SYN-ACK.

### Step 3: ACK

The client sends an ACK.

After this exchange, the TCP connection is established and data transfer can begin.

**Simple flow:**

`Client → SYN → Server`

`Client ← SYN-ACK ← Server`

`Client → ACK → Server`

---

### 16. What is HTTP?

**Answer:**

HTTP (Hypertext Transfer Protocol) is an application-layer protocol used to transfer web resources between clients and servers.

It follows a request-response model.

**Example:**

A browser sends:

`GET /index.html`

The server processes the request and sends a response.

Common HTTP methods include:

- GET
- POST
- PUT
- PATCH
- DELETE

---

### 17. What is HTTPS?

**Answer:**

HTTPS is HTTP carried over a secure TLS connection.

It provides:

- Encryption
- Authentication of the server
- Protection against tampering in transit

HTTPS normally uses port **443**.

**Simple difference:**

HTTP → Communication is not protected by TLS.

HTTPS → HTTP communication is protected using TLS.

---

### 18. What is DNS?

**Answer:**

DNS (Domain Name System) translates human-readable domain names into IP addresses and supports other name-related records.

**Example:**

When we enter:

`www.example.com`

the DNS system can help determine the IP address associated with that domain.

This allows users to use domain names instead of remembering IP addresses.

**Simple analogy:**

DNS is like the Internet's phone directory.

---

### 19. What happens when you enter a URL in a browser?

**Answer:**

A simplified sequence is:

1. The browser parses the URL.
2. It determines whether it already has relevant cached information.
3. If needed, DNS resolution obtains the server's IP address.
4. The client establishes the required network connection.
5. For HTTPS, a TLS handshake is performed.
6. The browser sends an HTTP request.
7. The server processes the request.
8. The server sends an HTTP response.
9. The browser receives the resources and renders the page.

**Interview point:**

This question can test DNS, TCP/IP, TLS, HTTP, and browser fundamentals together.

---

### 20. What is DHCP?

**Answer:**

DHCP (Dynamic Host Configuration Protocol) automatically provides network configuration information to devices.

It can assign:

- IP address
- Subnet mask
- Default gateway
- DNS server information

Without DHCP, network settings would often need to be configured manually.

**Common process:**

`Discover → Offer → Request → Acknowledge`

This is often remembered as **DORA**.

---

## 🔴 IMPORTANT NETWORKING CONCEPTS

### 21. What is the difference between a Hub, Switch, and Router?

**Answer:**

### Hub

A hub sends incoming data to all connected ports.

It operates at the **Physical Layer**.

### Switch

A switch forwards Ethernet frames based on MAC addresses.

It primarily operates at the **Data Link Layer**.

### Router

A router forwards packets between different networks using IP addressing and routing information.

It primarily operates at the **Network Layer**.

| Device | Main Function | Typical Layer |
|---|---|---|
| Hub | Broadcasts incoming signals to ports | Physical |
| Switch | Forwards frames using MAC addresses | Data Link |
| Router | Connects and routes between networks | Network |

---

### 22. What is a Subnet Mask?

**Answer:**

A subnet mask is used with IPv4 addresses to determine which portion represents the network and which portion represents the host.

**Example:**

`192.168.1.10/24`

The `/24` indicates that the first 24 bits represent the network prefix.

A common subnet mask for `/24` is:

`255.255.255.0`

**Why is subnetting used?**

- Efficient IP address usage
- Network organization
- Smaller broadcast domains
- Better network management

---

### 23. What is the difference between Unicast, Broadcast, and Multicast?

**Answer:**

### Unicast

One sender communicates with one receiver.

**Example:**

A client communicating with one web server.

### Broadcast

One sender communicates with all applicable devices on a local broadcast domain.

**Example:**

An IPv4 broadcast message on a local network.

### Multicast

One sender communicates with a group of interested receivers.

**Example:**

A multicast application sending data to subscribed hosts.

**Simple:**

`Unicast → One-to-One`

`Broadcast → One-to-All`

`Multicast → One-to-Many (selected group)`

---

### 24. What is the difference between Flow Control and Congestion Control?

**Answer:**

### Flow Control

Flow control prevents a fast sender from overwhelming a slower receiver.

It focuses on the **receiver's capacity**.

### Congestion Control

Congestion control prevents excessive traffic from overwhelming the network.

It focuses on the **network's capacity**.

**Simple difference:**

Flow Control → Protects the receiver.

Congestion Control → Protects the network.

---

### 25. What is a Firewall?

**Answer:**

A firewall is a security mechanism that monitors and controls network traffic according to defined rules.

It can allow or block traffic based on factors such as:

- Source/destination IP
- Port
- Protocol
- Connection state
- Other security rules, depending on the firewall

**Example:**

A firewall can block incoming connections to a server port that should not be publicly accessible.

**Important point:**

A firewall is a security control; it is not the same thing as antivirus software.

---

# ⭐ MUST-KNOW DIFFERENCES

Before the interview, make sure you can clearly explain:

1. OSI vs TCP/IP
2. TCP vs UDP
3. IPv4 vs IPv6
4. MAC Address vs IP Address
5. HTTP vs HTTPS
6. Hub vs Switch vs Router
7. Flow Control vs Congestion Control
8. Unicast vs Broadcast vs Multicast
9. LAN vs WAN
10. DNS vs DHCP

---

# 🎯 HIGH-PRIORITY QUESTIONS

If you have limited time, prepare these first:

1. What is a Computer Network?
2. OSI Model
3. Seven OSI layers
4. TCP/IP Model
5. OSI vs TCP/IP
6. TCP vs UDP
7. TCP Three-Way Handshake
8. IP Address
9. IPv4 vs IPv6
10. MAC vs IP
11. Port Number
12. HTTP vs HTTPS
13. DNS
14. DHCP
15. What happens when you enter a URL?
16. Hub vs Switch vs Router
17. Subnet Mask
18. Firewall
19. Flow Control vs Congestion Control
20. Unicast vs Broadcast vs Multicast

---

# 💡 HOW TO ANSWER CN QUESTIONS IN AN INTERVIEW

Use this structure:

**Definition → Explanation → Example → Difference/Use case**

### Example

**Interviewer:** What is TCP?

**Good answer:**

> "TCP stands for Transmission Control Protocol. It is a connection-oriented transport-layer protocol that provides reliable and ordered delivery of data. Before transferring data, TCP establishes a connection using a three-way handshake. It also provides mechanisms for flow and congestion control. TCP is useful for applications where reliable delivery is important."

Then be ready for:

- How is TCP different from UDP?
- What is the three-way handshake?
- Why does TCP need a connection?
- What is flow control?
- What is congestion control?

---

# ⚠️ IMPORTANT FOR INFOSYS / CAPGEMINI

Do not memorize answers word-for-word.

The interviewer may ask:

- Why is it required?
- How does it work?
- Give an example.
- What is the difference?
- What happens internally?
- Which protocol would you choose and why?

You should understand the concept well enough to explain it in your own words.

---

# ✅ FINAL PREPARATION TARGET

For a System Engineer fresher interview, you should be able to:

- Explain the OSI model and all seven layers.
- Explain the TCP/IP model.
- Compare TCP and UDP.
- Explain the TCP three-way handshake.
- Explain IP and MAC addresses.
- Explain IPv4 and IPv6.
- Explain DNS and DHCP.
- Explain HTTP and HTTPS.
- Explain what happens when a URL is entered.
- Differentiate hub, switch, and router.
- Explain ports and common port numbers.
- Explain subnet masks at a basic level.
- Explain unicast, broadcast, and multicast.
- Explain flow control and congestion control.
- Explain the basic purpose of a firewall.

**Goal: Understand → Explain → Give Example → Handle Follow-up**
