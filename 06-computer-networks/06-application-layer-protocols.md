# Application Layer Protocols

## 1. What is the Application Layer?

The **Application Layer** is Layer 7 of the OSI model.

It provides network services directly to applications and users.

Common Application Layer protocols:

```text
HTTP
HTTPS
DNS
DHCP
FTP
SMTP
POP3
IMAP
SSH
Telnet
```

> In the TCP/IP model, these application-level protocols are generally grouped into the Application Layer.

---

# 2. HTTP

**HTTP (HyperText Transfer Protocol)** is used for communication between web clients and web servers.

Example:

```text
Browser
   ↓
HTTP Request
   ↓
Web Server
   ↓
HTTP Response
   ↓
Browser
```

HTTP commonly uses:

```text
TCP Port 80
```

---

# 3. HTTPS

**HTTPS (HTTP Secure)** is HTTP communication protected using **TLS**.

Commonly:

```text
HTTPS → TCP Port 443
```

HTTPS provides:

```text
Encryption
Authentication
Data integrity
```

Basic flow:

```text
Browser
   ↓
TLS-secured HTTP
   ↓
Web Server
```

---

# 4. HTTP vs HTTPS

| HTTP | HTTPS |
|---|---|
| Not protected by TLS | Protected by TLS |
| Commonly port 80 | Commonly port 443 |
| Data can be exposed if sent without other protection | Provides encrypted communication |
| Less secure for sensitive web traffic | Used for secure web communication |

### Interview Answer

> HTTPS is HTTP secured using TLS, providing encryption, authentication, and integrity for communication between the client and server.

---

# 5. HTTP Request

When a browser requests a resource, it sends an HTTP request.

Example:

```text
GET /index.html HTTP/1.1
Host: example.com
```

An HTTP request can contain:

```text
Request Method
URL/Path
Headers
Body (when applicable)
```

---

# 6. HTTP Methods

Important HTTP methods:

```text
GET
POST
PUT
PATCH
DELETE
```

### GET

Used to retrieve a resource.

```text
GET /users
```

### POST

Commonly used to submit data or create a resource.

```text
POST /users
```

### PUT

Commonly used to replace/update a resource representation.

```text
PUT /users/10
```

### PATCH

Used for a partial update.

```text
PATCH /users/10
```

### DELETE

Used to delete a resource.

```text
DELETE /users/10
```

---

# 7. HTTP Response

A server sends an HTTP response to the client.

Example:

```text
HTTP/1.1 200 OK

Hello World
```

An HTTP response contains:

```text
Status Code
Headers
Body (when applicable)
```

---

# 8. HTTP Status Codes

Status codes are grouped into categories:

```text
1xx → Informational
2xx → Success
3xx → Redirection
4xx → Client Error
5xx → Server Error
```

Important examples:

```text
200 → OK
201 → Created
301 → Moved Permanently
302 → Found
304 → Not Modified
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
500 → Internal Server Error
502 → Bad Gateway
503 → Service Unavailable
```

---

# 9. Important HTTP Status Codes

## 200 OK

The request was successfully processed.

```text
Client → Request
Server → 200 OK
```

## 201 Created

A new resource was successfully created.

## 400 Bad Request

The server cannot process the request because the request is invalid.

## 401 Unauthorized

Authentication is required or has failed.

## 403 Forbidden

The server understood the request but refuses to authorize access.

## 404 Not Found

The requested resource was not found.

## 500 Internal Server Error

The server encountered an unexpected internal error.

---

# 10. HTTP Headers

Headers carry additional information about a request or response.

Examples:

```text
Content-Type
Content-Length
Authorization
User-Agent
Accept
Cookie
Cache-Control
```

Example:

```text
Content-Type: application/json
```

This indicates that the body contains JSON data.

---

# 11. HTTP Statelessness

HTTP is traditionally considered a **stateless protocol**.

This means the protocol itself does not inherently maintain application session state between independent requests.

Example:

```text
Request 1
Request 2
Request 3
```

Each request can be handled independently unless additional mechanisms are used to maintain state.

State can be maintained using:

```text
Cookies
Sessions
Tokens
```

---

# 12. What is a Cookie?

A **cookie** is small data stored by the browser and associated with a website/domain.

Cookies can be used for:

```text
Session identification
Preferences
Authentication state
Tracking
```

Example:

```text
Browser
   ↓
Cookie
   ↓
Server recognizes session
```

---

# 13. DNS

**DNS (Domain Name System)** translates domain names into IP addresses and provides other name-related information.

Example:

```text
www.example.com
       ↓
      DNS
       ↓
93.184.216.34
```

DNS commonly uses:

```text
UDP Port 53
```

TCP Port 53 is also used in cases such as larger responses and zone transfers.

---

# 14. Why Do We Need DNS?

Humans prefer:

```text
google.com
```

instead of:

```text
142.250.x.x
```

DNS provides a naming system that maps domain names to IP addresses and other records.

---

# 15. How DNS Resolution Works

Simplified process:

```text
User enters:
www.example.com

        ↓

DNS Resolver
        ↓
DNS Servers
        ↓
IP Address
        ↓
Browser connects to server
```

---

# 16. DNS Records

Important DNS record types:

```text
A
AAAA
CNAME
MX
NS
TXT
```

### A Record

Maps a hostname to an IPv4 address.

```text
example.com
    ↓
192.168.1.10
```

### AAAA Record

Maps a hostname to an IPv6 address.

### CNAME

Creates an alias from one hostname to another hostname.

### MX

Specifies mail-exchange servers for a domain.

### NS

Identifies authoritative name servers for a domain.

### TXT

Stores arbitrary text used for purposes such as verification and email-related policies.

---

# 17. DNS Recursive vs Iterative Query

### Recursive

The client asks a recursive resolver to obtain the final answer.

```text
Client
  ↓
Resolver
  ↓
DNS hierarchy
  ↓
Resolver returns answer
```

### Iterative

A DNS server gives the best information/referral it has, and the requester continues the lookup.

---

# 18. DNS Caching

DNS responses can be cached.

Example:

```text
Client
  ↓
DNS Resolver
  ↓
Cached Answer
```

Caching reduces:

```text
Lookup time
Network traffic
Load on DNS infrastructure
```

DNS records have a:

```text
TTL
```

that controls how long a cached response may normally be retained.

---

# 19. DHCP

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration to clients.

It can provide:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

DHCP commonly uses:

```text
UDP
Server → Port 67
Client → Port 68
```

---

# 20. DHCP DORA

The standard DHCP address-assignment sequence is:

```text
D → Discover
O → Offer
R → Request
A → Acknowledgment
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

# 21. FTP

**FTP (File Transfer Protocol)** is used for transferring files.

Traditional FTP uses:

```text
TCP
Control → Port 21
Data    → Port 20 in traditional active mode
```

FTP supports operations such as:

```text
Upload
Download
Directory operations
File management
```

FTP itself does not provide encryption for credentials/data.

Secure alternatives include:

```text
FTPS
SFTP
```

> SFTP is a file-transfer protocol that runs over SSH; it is not simply "secure FTP."

---

# 22. SMTP

**SMTP (Simple Mail Transfer Protocol)** is used for sending email.

It is commonly used for:

```text
Mail submission
Mail transfer between mail servers
```

Common ports include:

```text
25  → SMTP relay
587 → Message submission
465 → SMTP over TLS commonly used for submission
```

---

# 23. POP3

**POP3 (Post Office Protocol version 3)** is used to retrieve email from a mail server.

Common ports:

```text
110  → POP3
995  → POP3 over TLS
```

POP3 traditionally focuses on downloading messages to the client.

---

# 24. IMAP

**IMAP (Internet Message Access Protocol)** is used to access and manage email stored on a mail server.

Common ports:

```text
143  → IMAP
993  → IMAP over TLS
```

IMAP is useful when the same mailbox needs to be synchronized across multiple devices.

---

# 25. SMTP vs POP3 vs IMAP

| Protocol | Main Purpose |
|---|---|
| SMTP | Send/relay email |
| POP3 | Retrieve/download email |
| IMAP | Access and synchronize email on server |

### Easy Memory Trick

```text
SMTP → Send
POP3 → Download
IMAP → Sync/Manage
```

---

# 26. SSH

**SSH (Secure Shell)** provides secure remote access and command execution over a network.

Common port:

```text
TCP 22
```

SSH provides:

```text
Encryption
Authentication
Integrity
Secure remote access
```

Example:

```text
Local Computer
      ↓
    SSH
      ↓
Remote Server
```

---

# 27. Telnet

**Telnet** provides remote terminal access but does not provide the encryption/security that SSH provides.

Common port:

```text
TCP 23
```

Because Telnet sends communication without modern cryptographic protection, **SSH is preferred for secure remote administration**.

---

# 28. SSH vs Telnet

| SSH | Telnet |
|---|---|
| Secure | Not encrypted |
| Commonly TCP 22 | Commonly TCP 23 |
| Provides encryption | No encryption |
| Used for secure remote administration | Mostly legacy/testing use |

---

# 29. HTTP vs FTP

| HTTP | FTP |
|---|---|
| Web communication | File transfer |
| Commonly TCP 80 / HTTPS 443 | TCP 21 control |
| Request/response model | Dedicated control/data mechanisms |
| Used by browsers and web applications | Used for file transfer |

---

# 30. DNS vs DHCP

These are frequently confused.

### DNS

```text
Name
 ↓
IP Address / Other DNS information
```

### DHCP

```text
Network configuration
 ↓
IP + Gateway + DNS + etc.
```

### Easy Memory Trick

```text
DNS → "What IP belongs to this name?"

DHCP → "Give this device network configuration."
```

---

# 31. Application Protocols and Transport Protocols

Different application protocols use different transport mechanisms.

Examples:

```text
HTTP  → TCP
HTTPS → TCP
SSH   → TCP
FTP   → TCP
SMTP  → TCP
IMAP  → TCP
POP3  → TCP

DNS   → Usually UDP, can use TCP
DHCP  → UDP
```

Modern protocols can also use newer transports. For example:

```text
HTTP/3 → QUIC → UDP
```

So don't memorize the rule as:

```text
"All HTTP uses TCP."
```

That is not true for HTTP/3.

---

# 32. What is QUIC?

**QUIC** is a modern transport protocol built over UDP.

It provides transport features such as:

```text
Reliable delivery
Stream multiplexing
Connection establishment
Encryption integration
```

HTTP/3 runs over:

```text
HTTP/3
   ↓
QUIC
   ↓
UDP
   ↓
IP
```

This is an important modern interview concept.

---

# 33. HTTP/1.1 vs HTTP/2 vs HTTP/3

### HTTP/1.1

Traditionally uses:

```text
TCP
```

### HTTP/2

Also commonly uses:

```text
TCP
```

It introduces features such as:

```text
Multiplexing
Header compression
Binary framing
```

### HTTP/3

Uses:

```text
QUIC
 ↓
UDP
```

It provides:

```text
Multiplexed streams
Modern connection establishment
TLS integration
```

---

# 34. Important Port Numbers

| Protocol | Port | Transport |
|---|---:|---|
| FTP | 21 | TCP |
| SSH | 22 | TCP |
| Telnet | 23 | TCP |
| SMTP | 25 | TCP |
| DNS | 53 | UDP/TCP |
| DHCP Server | 67 | UDP |
| DHCP Client | 68 | UDP |
| HTTP | 80 | TCP |
| POP3 | 110 | TCP |
| IMAP | 143 | TCP |
| HTTPS | 443 | TCP |
| IMAP over TLS | 993 | TCP |
| POP3 over TLS | 995 | TCP |

> These are common/default ports. A service can be configured to use a different port.

---

# 35. What Happens When You Enter a URL in a Browser?

This is a **very important interview question**.

Suppose you enter:

```text
https://example.com
```

A simplified sequence is:

```text
1. Browser parses the URL
        ↓
2. DNS resolution finds the server IP
        ↓
3. Transport connection is established
   (TCP for typical HTTPS/HTTP/1.1 or HTTP/2)
        ↓
4. TLS handshake occurs
        ↓
5. Browser sends HTTP request
        ↓
6. Server processes request
        ↓
7. Server sends HTTP response
        ↓
8. Browser renders the content
```

For HTTP/3:

```text
DNS
 ↓
QUIC over UDP
 ↓
TLS integrated with QUIC
 ↓
HTTP/3
```

---

# 36. Important Application Layer Questions

```text
1. What is the Application Layer?

2. What are common Application Layer protocols?

3. What is HTTP?

4. What is HTTPS?

5. HTTP vs HTTPS?

6. What is TLS?

7. What are HTTP methods?

8. GET vs POST?

9. PUT vs PATCH?

10. What is an HTTP status code?

11. Explain 200, 201, 301, 400, 401, 403, 404 and 500.

12. What are HTTP headers?

13. Is HTTP stateful or stateless?

14. What is a cookie?

15. What is DNS?

16. Why is DNS required?

17. How does DNS resolution work?

18. What are A and AAAA records?

19. What is a CNAME record?

20. What is an MX record?

21. What is DNS caching?

22. What is DNS TTL?

23. Recursive vs iterative DNS query?

24. What is DHCP?

25. What is DHCP DORA?

26. What are DHCP ports 67 and 68?

27. What is FTP?

28. What are FTP control and data connections?

29. What is SMTP?

30. What is POP3?

31. What is IMAP?

32. SMTP vs POP3 vs IMAP?

33. What is SSH?

34. What is Telnet?

35. SSH vs Telnet?

36. What is QUIC?

37. What is HTTP/3?

38. HTTP/2 vs HTTP/3?

39. Which transport protocol does DNS use?

40. Which transport protocol does DHCP use?

41. Which protocols commonly use TCP?

42. What happens when you enter a URL in a browser?
```

---

# 37. Most Important Comparisons

## HTTP vs HTTPS

```text
HTTP
→ Web communication
→ Commonly port 80
→ No TLS protection

HTTPS
→ HTTP + TLS
→ Commonly port 443
→ Encryption + authentication + integrity
```

---

## DNS vs DHCP

```text
DNS
→ Resolves names
→ Commonly UDP/TCP 53

DHCP
→ Provides network configuration
→ UDP 67/68
```

---

## SMTP vs POP3 vs IMAP

```text
SMTP
→ Send/relay email

POP3
→ Retrieve/download email

IMAP
→ Access/synchronize email
```

---

## SSH vs Telnet

```text
SSH
→ Secure remote access
→ TCP 22

Telnet
→ Unencrypted remote access
→ TCP 23
```

---

## HTTP/2 vs HTTP/3

```text
HTTP/2
→ Usually TCP
→ Multiplexing
→ Header compression

HTTP/3
→ QUIC
→ UDP
→ Multiplexing
→ TLS integrated with QUIC
```

---

# 38. Quick Revision

```text
APPLICATION LAYER
→ Layer 7
→ Provides network services to applications

HTTP
→ Web communication
→ Port 80 commonly

HTTPS
→ HTTP + TLS
→ Port 443 commonly

GET
→ Retrieve

POST
→ Submit/create

PUT
→ Replace/update

PATCH
→ Partial update

DELETE
→ Delete

200
→ OK

201
→ Created

400
→ Bad Request

401
→ Authentication required/failed

403
→ Forbidden

404
→ Not Found

500
→ Internal Server Error

DNS
→ Domain name resolution
→ Port 53
→ Usually UDP, can use TCP

A
→ IPv4 address

AAAA
→ IPv6 address

CNAME
→ Hostname alias

MX
→ Mail server

DHCP
→ Automatic network configuration
→ UDP 67/68

DORA
→ Discover
→ Offer
→ Request
→ Acknowledge

FTP
→ File transfer
→ TCP 21 control

SMTP
→ Email sending/relay

POP3
→ Email retrieval

IMAP
→ Email access/synchronization

SSH
→ Secure remote access
→ TCP 22

TELNET
→ Remote access
→ TCP 23
→ No encryption

QUIC
→ Transport protocol over UDP

HTTP/3
→ HTTP over QUIC
→ UDP
```

---

# 39. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
Application Layer
HTTP
HTTPS
HTTP vs HTTPS
HTTP Methods
HTTP Status Codes
DNS
DNS Resolution
DNS Records
DNS vs DHCP
DHCP + DORA
SMTP
POP3
IMAP
SSH
Telnet
Important Port Numbers
URL/Browser Request Flow
```

## ⭐⭐⭐ Good to Know

```text
HTTP Headers
Cookies
DNS Caching
DNS Recursive vs Iterative
FTP
QUIC
HTTP/2
HTTP/3
```

> **For placement interviews, focus deeply on HTTP/HTTPS, HTTP methods and status codes, DNS, DHCP, email protocols, SSH/Telnet, important port numbers, and what happens when you enter a URL in a browser. These are the highest-value Application Layer concepts.**