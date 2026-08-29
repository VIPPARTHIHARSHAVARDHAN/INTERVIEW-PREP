# Network Security and Common Attacks

## 1. What is Network Security?

**Network Security** is the practice of protecting networks, devices, applications, and data from unauthorized access, misuse, attacks, and disruption.

Main goals:

```text
Confidentiality
Integrity
Availability
```

These three are commonly called the:

```text
CIA Triad
```

---

# 2. CIA Triad

## Confidentiality

Ensures that only authorized users can access information.

Example:

```text
Encryption
Access Control
Authentication
```

---

## Integrity

Ensures that data is not improperly modified or corrupted.

Example:

```text
Hashing
Digital Signatures
Checksums
```

---

## Availability

Ensures that systems and services remain accessible when needed.

Example:

```text
Redundancy
Backups
DDoS Protection
Failover
```

### Easy Memory Trick

```text
Confidentiality → Keep it secret

Integrity → Keep it correct

Availability → Keep it accessible
```

---

# 3. Authentication

**Authentication** verifies the identity of a user or system.

Example:

```text
Username + Password
        ↓
Authentication
        ↓
User Identity Verified
```

Other methods:

```text
OTP
Biometrics
Security Keys
Certificates
```

---

# 4. Authorization

**Authorization** determines what an authenticated user is allowed to access or perform.

Example:

```text
Authentication
→ Who are you?

Authorization
→ What are you allowed to do?
```

---

# 5. Authentication vs Authorization

| Authentication | Authorization |
|---|---|
| Verifies identity | Determines permissions |
| "Who are you?" | "What can you access?" |
| Happens before authorization | Usually follows authentication |
| Example: Password | Example: Admin permission |

### Example

```text
Login
 ↓
Authentication
 ↓
User identified as Harsha
 ↓
Authorization
 ↓
Can access permitted resources
```

---

# 6. Encryption

**Encryption** converts readable data (**plaintext**) into unreadable data (**ciphertext**) using a cryptographic method and key.

```text
Plaintext
   ↓
Encryption + Key
   ↓
Ciphertext
```

Decryption reverses the process:

```text
Ciphertext
   ↓
Decryption + Key
   ↓
Plaintext
```

Encryption primarily provides:

```text
Confidentiality
```

---

# 7. Symmetric Encryption

In **symmetric encryption**, the same secret key is used for encryption and decryption.

```text
Plaintext
   ↓
Secret Key
   ↓
Ciphertext
   ↓
Same Secret Key
   ↓
Plaintext
```

Example:

```text
AES
```

Advantages:

```text
Fast
Efficient for large amounts of data
```

Main challenge:

```text
How do both parties securely obtain/share the secret key?
```

---

# 8. Asymmetric Encryption

**Asymmetric cryptography** uses a key pair:

```text
Public Key
Private Key
```

The keys are mathematically related.

A common conceptual use:

```text
Public Key
→ Can be shared

Private Key
→ Must be kept secret
```

Examples of public-key cryptography include:

```text
RSA
ECC
```

---

# 9. Symmetric vs Asymmetric Encryption

| Symmetric | Asymmetric |
|---|---|
| Same secret key | Public/private key pair |
| Faster | Computationally more expensive |
| Good for bulk data encryption | Useful for key exchange/authentication/signatures |
| Example: AES | Examples: RSA, ECC |

---

# 10. Hashing

**Hashing** converts input data into a fixed-length hash value.

```text
Input
 ↓
Hash Function
 ↓
Hash
```

A cryptographic hash function is designed so that it is computationally difficult to reverse the hash into the original input.

Examples:

```text
SHA-256
SHA-3
```

Important:

```text
Encryption
→ Designed to be reversible with the appropriate key

Hashing
→ Designed as a one-way transformation
```

---

# 11. Hashing vs Encryption

| Hashing | Encryption |
|---|---|
| One-way transformation | Reversible with appropriate key |
| Used for integrity/password-related applications | Used for confidentiality |
| Produces a hash | Produces ciphertext |
| Example: SHA-256 | Example: AES |

> Passwords should generally be stored using a password-hashing/KDF scheme such as Argon2, bcrypt, or scrypt rather than plain SHA-256.

---

# 12. Digital Signature

A **digital signature** helps provide:

```text
Authentication
Integrity
Non-repudiation
```

Conceptually:

```text
Message
   ↓
Hash
   ↓
Sign using Private Key
   ↓
Digital Signature
```

The recipient can use the corresponding public key to verify the signature.

---

# 13. Digital Certificate

A **digital certificate** binds an identity/domain to a public key.

Certificates are commonly used in:

```text
HTTPS/TLS
```

A certificate is generally issued/signed by a:

```text
Certificate Authority (CA)
```

---

# 14. What is TLS?

**TLS (Transport Layer Security)** is a cryptographic protocol used to secure communication over networks.

TLS provides:

```text
Confidentiality
Integrity
Authentication
```

HTTPS commonly uses:

```text
HTTP
 ↓
TLS
 ↓
TCP
 ↓
IP
```

For HTTP/3:

```text
HTTP/3
 ↓
QUIC
 ↓
UDP
```

with TLS integrated into QUIC.

---

# 15. What is a Firewall?

A **firewall** controls network traffic based on security rules.

It can allow or block traffic based on things such as:

```text
Source IP
Destination IP
Port
Protocol
Connection state
Application characteristics
```

Example:

```text
Internet
   ↓
Firewall
   ↓
Internal Network
```

---

# 16. Firewall Example

Suppose a server should allow:

```text
HTTPS → Port 443
```

but block:

```text
Unwanted incoming traffic
```

A firewall can enforce rules such as:

```text
Allow TCP 443
Block other unauthorized inbound traffic
```

---

# 17. IDS

**IDS (Intrusion Detection System)** monitors activity and attempts to detect suspicious or malicious behavior.

Conceptually:

```text
Network Traffic
      ↓
     IDS
      ↓
Detect suspicious activity
      ↓
Alert
```

IDS is primarily:

```text
Detection
```

---

# 18. IPS

**IPS (Intrusion Prevention System)** can detect suspicious activity and take action to block or prevent it.

```text
Network Traffic
      ↓
     IPS
      ↓
Detect attack
      ↓
Block / Prevent
```

---

# 19. IDS vs IPS

| IDS | IPS |
|---|---|
| Detects suspicious activity | Detects and can block suspicious activity |
| Primarily alerts | Can actively prevent |
| Usually monitoring-oriented | Usually placed inline |

### Easy Memory Trick

```text
IDS → Detect

IPS → Detect + Prevent
```

---

# 20. What is a VPN?

A **VPN (Virtual Private Network)** creates a protected communication path over an untrusted network.

Conceptually:

```text
Device
  ↓
Encrypted Tunnel
  ↓
Internet
  ↓
VPN Server
```

VPN technologies can provide:

```text
Confidentiality
Authentication
Integrity
```

depending on the protocol and configuration.

---

# 21. What is a Man-in-the-Middle Attack?

A **Man-in-the-Middle (MITM)** attack occurs when an attacker gets between two communicating parties and attempts to intercept or manipulate their communication.

Conceptually:

```text
Client
  ↓
Attacker
  ↓
Server
```

Without proper protection:

```text
Client ←→ Attacker ←→ Server
```

TLS helps protect against MITM attacks when certificates and authentication are correctly validated.

---

# 22. What is Phishing?

**Phishing** is a social-engineering attack in which an attacker tricks users into revealing sensitive information or performing an unwanted action.

Example:

```text
Fake Email
    ↓
Fake Login Page
    ↓
User enters credentials
    ↓
Attacker obtains them
```

Phishing can target:

```text
Passwords
Banking information
OTP codes
Company credentials
Personal information
```

---

# 23. What is Spoofing?

**Spoofing** means impersonating or falsifying an identity/address/source.

Examples:

```text
IP Spoofing
MAC Spoofing
Email Spoofing
DNS Spoofing
```

The attacker attempts to make traffic or communication appear to originate from a trusted source.

---

# 24. IP Spoofing

In **IP spoofing**, an attacker modifies the source IP address in packets to make them appear to originate from another address.

Conceptually:

```text
Attacker
   ↓
Fake Source IP
   ↓
Victim
```

IP spoofing can be used in:

```text
Reflection attacks
DDoS attacks
Traffic manipulation
```

---

# 25. ARP Spoofing

ARP spoofing targets IPv4 local networks by sending forged ARP information.

Example:

```text
Victim
  ↓
Attacker claims:
"I am the gateway"
```

This can allow the attacker to position themselves between a victim and the gateway.

Possible consequences:

```text
Traffic interception
Traffic modification
Denial of service
```

---

# 26. DNS Spoofing

DNS spoofing involves providing false DNS information so that a domain name resolves to an unintended destination.

Example:

```text
User enters:
bank.com

DNS response manipulated
        ↓
Fake IP
        ↓
Attacker-controlled site
```

Proper DNS security mechanisms and HTTPS certificate validation can help reduce these risks.

---

# 27. DoS Attack

**DoS (Denial of Service)** attempts to make a service unavailable to legitimate users.

Conceptually:

```text
Attacker
   ↓↓↓↓↓↓↓
Server
   ↓
Resources exhausted
   ↓
Service unavailable
```

The attacker may exploit:

```text
Bandwidth
CPU
Memory
Connections
Application resources
```

---

# 28. DDoS Attack

**DDoS (Distributed Denial of Service)** is a DoS attack performed using many distributed systems.

```text
Device 1 ──┐
Device 2 ──┤
Device 3 ──┼──→ Target
Device 4 ──┤
Device 5 ──┘
```

Because traffic originates from many systems, mitigation can be more difficult.

---

# 29. DoS vs DDoS

| DoS | DDoS |
|---|---|
| Attack from one or relatively few sources | Distributed across many sources |
| Easier to identify/block in some cases | More difficult to distinguish from distributed traffic |
| Attempts to exhaust resources | Same goal using distributed sources |

---

# 30. Malware

**Malware** means malicious software designed to harm systems, steal information, disrupt operations, or gain unauthorized access.

Common categories:

```text
Virus
Worm
Trojan
Ransomware
Spyware
```

---

# 31. Virus

A **virus** is malicious code that typically attaches itself to a legitimate file/program and requires some form of user/system action to spread.

```text
Malicious File
      ↓
User/System Executes
      ↓
Virus Activates
```

---

# 32. Worm

A **worm** is malware capable of self-propagating across systems, often through network or software vulnerabilities.

```text
Computer A
    ↓
Computer B
    ↓
Computer C
    ↓
Computer D
```

A worm does not need to attach itself to another executable in the same way a traditional virus does.

---

# 33. Trojan

A **Trojan** is malicious software disguised as or delivered as something legitimate.

Example:

```text
Fake Application
      ↓
User Installs
      ↓
Malicious Activity
```

Unlike worms, Trojans do not inherently self-replicate.

---

# 34. Ransomware

**Ransomware** is malware that typically blocks access to data or systems, often by encrypting files, and demands payment.

Conceptually:

```text
Files
 ↓
Ransomware
 ↓
Encrypted Files
 ↓
Ransom Demand
```

---

# 35. Spyware

**Spyware** is software designed to secretly monitor or collect information about users or systems.

Examples of targeted information can include:

```text
Browsing activity
Credentials
Personal information
System activity
```

---

# 36. Brute Force Attack

A **brute-force attack** attempts to guess credentials by trying many possible passwords or combinations.

Conceptually:

```text
Password 1 → Wrong
Password 2 → Wrong
Password 3 → Wrong
...
Password N → ?
```

Defenses include:

```text
Strong passwords
Rate limiting
Account lockout
MFA
Monitoring
```

---

# 37. Dictionary Attack

A **dictionary attack** uses a list of likely/common passwords rather than trying every possible combination.

```text
password
123456
qwerty
welcome
admin
...
```

It is generally more efficient than blindly trying every possible character combination when users choose predictable passwords.

---

# 38. Replay Attack

A **replay attack** occurs when an attacker captures a valid communication and later retransmits it to try to make the system accept it again.

Conceptually:

```text
Valid Request
     ↓
Attacker captures it
     ↓
Later retransmits
     ↓
Server
```

Defenses can include:

```text
Nonces
Timestamps
Sequence numbers
Challenge-response mechanisms
```

---

# 39. Session Hijacking

**Session hijacking** occurs when an attacker obtains or takes control of a valid user's session.

Example:

```text
User
 ↓
Authenticated Session
 ↓
Session Identifier stolen
 ↓
Attacker uses session
```

Possible defenses:

```text
HTTPS/TLS
Secure cookies
HttpOnly cookies
Session expiration
Session rotation
MFA
```

---

# 40. SQL Injection

**SQL Injection** occurs when untrusted user input is improperly incorporated into SQL queries, allowing an attacker to alter the intended query.

Unsafe conceptual example:

```text
SELECT * FROM users
WHERE username = 'USER_INPUT';
```

If input is directly concatenated into SQL, an attacker may manipulate the query structure.

### Prevention

Use:

```text
Parameterized Queries
Prepared Statements
Input Validation
Least Privilege
```

The most important defense is:

```text
Parameterized Queries / Prepared Statements
```

---

# 41. Cross-Site Scripting (XSS)

**XSS** occurs when an attacker causes malicious script content to execute in another user's browser in the context of a vulnerable web application.

Example:

```text
Attacker Input
     ↓
Vulnerable Website
     ↓
Browser executes script
```

Possible defenses:

```text
Output Encoding
Input Validation
Content Security Policy
Safe templating
```

---

# 42. CSRF

**CSRF (Cross-Site Request Forgery)** tricks a user's browser into sending an unwanted authenticated request to a website where the user is already logged in.

Conceptually:

```text
User logged into bank
        ↓
Visits malicious website
        ↓
Browser sends unwanted request
        ↓
Bank
```

Defenses can include:

```text
CSRF Tokens
SameSite Cookies
Origin/Referer validation where appropriate
```

---

# 43. XSS vs CSRF

| XSS | CSRF |
|---|---|
| Malicious script executes in victim's browser | Tricks browser into sending unwanted request |
| Exploits insufficient output/input handling | Exploits trust in authenticated browser requests |
| Can steal/modify accessible browser data | Can perform actions using victim's authenticated session |
| Main defense: output encoding/CSP | Main defenses: CSRF tokens/SameSite cookies |

---

# 44. Common Network Attacks Summary

| Attack | Main Idea |
|---|---|
| MITM | Intercept/manipulate communication |
| Phishing | Trick users into revealing information |
| Spoofing | Impersonate/fake identity or source |
| ARP Spoofing | Forge ARP mappings |
| DNS Spoofing | Provide false DNS resolution |
| DoS | Make service unavailable |
| DDoS | Distributed DoS |
| Brute Force | Try many credentials |
| Dictionary Attack | Try common passwords |
| Replay | Reuse captured valid communication |
| Session Hijacking | Take over a valid session |
| SQL Injection | Manipulate database query through input |
| XSS | Execute malicious script in victim's browser |
| CSRF | Trick authenticated browser into unwanted action |
| Malware | Malicious software |

---

# 45. Important Security Terms

## Authentication

```text
Who are you?
```

## Authorization

```text
What are you allowed to do?
```

## Encryption

```text
Protect data confidentiality
```

## Hashing

```text
One-way transformation
```

## Firewall

```text
Control network traffic
```

## IDS

```text
Detect suspicious activity
```

## IPS

```text
Detect + prevent/block
```

---

# 46. Important Interview Questions

```text
1. What is network security?

2. What is the CIA Triad?

3. Explain confidentiality, integrity, and availability.

4. What is authentication?

5. What is authorization?

6. Authentication vs authorization?

7. What is encryption?

8. What is symmetric encryption?

9. What is asymmetric encryption?

10. Symmetric vs asymmetric encryption?

11. What is hashing?

12. Hashing vs encryption?

13. What is a digital signature?

14. What is a digital certificate?

15. What is TLS?

16. How does HTTPS provide security?

17. What is a firewall?

18. What is IDS?

19. What is IPS?

20. IDS vs IPS?

21. What is a VPN?

22. What is a Man-in-the-Middle attack?

23. What is phishing?

24. What is spoofing?

25. What is IP spoofing?

26. What is ARP spoofing?

27. What is DNS spoofing?

28. What is DoS?

29. What is DDoS?

30. DoS vs DDoS?

31. What is malware?

32. Virus vs worm?

33. What is a Trojan?

34. What is ransomware?

35. What is spyware?

36. What is a brute-force attack?

37. What is a dictionary attack?

38. What is a replay attack?

39. What is session hijacking?

40. What is SQL Injection?

41. How can SQL Injection be prevented?

42. What is XSS?

43. How can XSS be prevented?

44. What is CSRF?

45. XSS vs CSRF?

46. What is the difference between a firewall and IDS?

47. Why is HTTPS safer than HTTP?

48. How does TLS protect communication?

49. What is the difference between encryption, hashing, and encoding?

50. How can a network be protected against common attacks?
```

---

# 47. Most Important Comparisons

## Authentication vs Authorization

```text
Authentication
→ Who are you?

Authorization
→ What can you do?
```

---

## Encryption vs Hashing

```text
Encryption
→ Reversible with appropriate key
→ Confidentiality

Hashing
→ One-way transformation
→ Integrity/password-related uses
```

---

## Symmetric vs Asymmetric

```text
Symmetric
→ Same secret key
→ Fast
→ AES

Asymmetric
→ Public + Private key
→ RSA/ECC
→ Authentication/key exchange/signatures
```

---

## IDS vs IPS

```text
IDS
→ Detect + Alert

IPS
→ Detect + Block/Prevent
```

---

## DoS vs DDoS

```text
DoS
→ Single/limited source

DDoS
→ Many distributed sources
```

---

## XSS vs CSRF

```text
XSS
→ Malicious script executes in browser

CSRF
→ Browser is tricked into sending an unwanted authenticated request
```

---

# 48. Quick Revision

```text
NETWORK SECURITY
→ Protect network, systems, applications and data

CIA
→ Confidentiality
→ Integrity
→ Availability

AUTHENTICATION
→ Verify identity

AUTHORIZATION
→ Verify permissions

SYMMETRIC
→ Same secret key
→ AES

ASYMMETRIC
→ Public + Private key
→ RSA/ECC

HASHING
→ One-way transformation
→ SHA-256/SHA-3

DIGITAL SIGNATURE
→ Authentication + Integrity + Non-repudiation

CERTIFICATE
→ Binds identity/domain to public key

TLS
→ Secure network communication

FIREWALL
→ Controls traffic

IDS
→ Detects attacks

IPS
→ Detects + prevents

VPN
→ Protected communication tunnel

MITM
→ Intercept communication

PHISHING
→ Trick users

SPOOFING
→ Fake identity/source

ARP SPOOFING
→ Fake ARP mappings

DNS SPOOFING
→ Fake DNS response

DoS
→ Deny service

DDoS
→ Distributed DoS

MALWARE
→ Malicious software

VIRUS
→ Typically attaches to files/programs

WORM
→ Self-propagates

TROJAN
→ Disguised malicious software

RANSOMWARE
→ Locks/encrypts data for extortion

SPYWARE
→ Secret monitoring/collection

BRUTE FORCE
→ Try many passwords

DICTIONARY ATTACK
→ Try likely/common passwords

REPLAY
→ Reuse captured communication

SESSION HIJACKING
→ Take over valid session

SQL INJECTION
→ Manipulate SQL through unsafe input

XSS
→ Malicious script in browser

CSRF
→ Unwanted authenticated request
```

---

# 49. Placement Priority

## ⭐⭐⭐⭐⭐ Must Prepare

```text
CIA Triad
Authentication vs Authorization
Encryption
Symmetric vs Asymmetric Encryption
Hashing vs Encryption
TLS / HTTPS Security
Firewall
IDS vs IPS
VPN
MITM
Phishing
Spoofing
DoS vs DDoS
Brute Force
SQL Injection
XSS
CSRF
```

## ⭐⭐⭐ Good to Know

```text
Digital Signatures
Digital Certificates
ARP Spoofing
DNS Spoofing
Replay Attacks
Session Hijacking
Malware
Virus vs Worm vs Trojan
Ransomware
Spyware
Dictionary Attacks
```

> **For placement interviews, focus deeply on CIA Triad, authentication vs authorization, encryption, hashing, TLS/HTTPS, firewalls, IDS/IPS, MITM, phishing, spoofing, DoS/DDoS, SQL Injection, XSS, and CSRF. These are the highest-value Network Security concepts for typical software-placement interviews.**