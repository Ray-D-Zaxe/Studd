# MCA-303 Information Security – Master Revision (Final)
## 3rd Semester MCA – End Semester Exam Preparation

> **Master Guide:** This file combines the comprehensive syllabus coverage of Version 2 with the deep step-by-step mechanisms of Version 3, plus an expanded IP Security section.

---

## UNIT I – Introduction to Information Security & Basics of Cryptography

### 1.1 Core Security Concepts
**Information Security** protects information assets from threats and vulnerabilities using the **CIA Triad**:
*   **Confidentiality:** Preserving authorized restrictions on access (e.g., encryption).
*   **Integrity:** Guarding against improper modification (e.g., hashing).
*   **Availability:** Ensuring timely and reliable access (e.g., redundancy).

**Extended Goals:** Authentication, Authorization, Non-repudiation, Accountability.

### 1.2 Security Architecture Models

#### 1.2.1 Active vs. Passive Attacks
*   **Passive Attacks (Monitoring):**
    *   **Goal:** Obtain info without affecting resources.
    *   **Types:** *Traffic Analysis* (observing pattern/volume), *Release of Message Contents*.
    *   **Defense:** **Prevention** (Encryption) is feasible; detection is hard.
*   **Active Attacks (Modification):**
    *   **Goal:** Alter system resources or operation.
    *   **Types:**
        *   *Masquerade:* Impersonation.
        *   *Replay:* Capture and retransmit.
        *   *Modification:* Altering data in transit.
        *   *DoS:* disrupting service.
    *   **Defense:** **Detection** and **Recovery** (hard to prevent completely).

### 1.3 Detailed Attack Mechanisms

#### 1.3.1 Buffer Overflow Attack (Step-by-Step)
**Concept:** Overwriting adjacent memory by exceeding buffer boundaries on the **Stack**.
**Steps:**
1.  **Vulnerability:** Program uses unsafe function like `strcpy(dest, src)` without checking length.
2.  **Payload Creation:** Attacker crafts a string containing:
    *   *Shellcode:* Malicious code (e.g., to spawn a shell).
    *   *NOP Sled:* Instructions to slide execution to shellcode.
    *   *New Return Address:* Pointer to the shellcode.
3.  **Overflow:** Input > Buffer Size. The "New Return Address" overwrites the **Saved Return Address** on the stack.
4.  **Control Hijack:** Function tries to `return` but jumps to the "New Return Address" (Shellcode).
5.  **Execution:** Shellcode executes with the program's privileges.

#### 1.3.2 SQL Injection (Step-by-Step)
**Concept:** Injecting malicious SQL via user input fields to manipulate the backend database.
**Steps:**
1.  **Input:** Attacker enters `admin' #` into a username field.
2.  **Query Construction:** App builds: `SELECT * FROM users WHERE name = 'admin' #' AND pass = '...'`
3.  **Interpretation:** The `'` closes the name string. The `#` comments out the rest (password check).
4.  **Bypass:** Database executes `SELECT * FROM users WHERE name = 'admin'`, logging the attacker in as admin.

#### 1.3.3 Other Attacks (Brief)
*   **DoS/DDoS:** Flooding (SYN Flood) or crashing service. Defense: SYN Cookies, Rate limiting.
*   **Session Hijacking:** Stealing Session ID (via XSS or sniffing) to impersonate user.
*   **Phishing:** Social engineering via email.
*   **Malware:** Virus (needs host), Worm (independent), Trojan (disguised), Ransomware (encrypts data).

### 1.4 Cryptography Basics
*   **Symmetric:** Same key for encryption/decryption (DES, AES). Fast. Key distribution problem.
*   **Asymmetric:** Public/Private key pair (RSA, ECC). Slow. Solves key distribution.
*   **Hash:** Fixed length digest (SHA-256). One-way. Integrity only.

---

## UNIT II – Secret Key & Public Key Cryptography

### 2.1 DES (Data Encryption Standard)
*   **Specs:** 64-bit block, 56-bit key, 16 rounds.
*   **Structure:** Feistel Network.

**Detailed Algorithm Steps:**
1.  **Initial Permutation (IP):** Shuffle 64-bit plaintext.
2.  **Split:** Divide into Left ($L_0$) and Right ($R_0$) 32-bit halves.
3.  **16 Rounds:** For $i = 1$ to $16$:
    *   $L_i = R_{i-1}$
    *   $R_i = L_{i-1} \oplus F(R_{i-1}, K_i)$
    *   **Function F:**
        1.  *Expand* $R_{i-1}$ to 48 bits.
        2.  *XOR* with 48-bit Subkey $K_i$.
        3.  *Substitute* using 8 S-Boxes (6 bits in -> 4 bits out). **(Confusion)**
        4.  *Permute* the 32-bit result. **(Diffusion)**
4.  **Final Swap:** Swap halves.
5.  **Inverse IP:** Final shuffle.

### 2.2 AES (Advanced Encryption Standard)
*   **Specs:** 128-bit block. Key: 128/192/256 bits. Rounds: 10/12/14.
*   **Structure:** SPN (Substitution-Permutation Network).

**Detailed Algorithm Steps (AES-128):**
1.  **AddRoundKey:** XOR State with Key 0.
2.  **9 Main Rounds:**
    *   **SubBytes:** Non-linear substitution using S-Box (1 byte -> 1 byte).
    *   **ShiftRows:** Cyclic shift (Row 0: 0, Row 1: 1, Row 2: 2, Row 3: 3 bytes).
    *   **MixColumns:** Matrix multiplication of columns (Diffusion).
    *   **AddRoundKey:** XOR with Round Key.
3.  **Final Round (10th):** SubBytes -> ShiftRows -> AddRoundKey (No MixColumns).

### 2.3 Block Cipher Modes
*   **ECB:** Parallel, pattern leakage. Bad.
*   **CBC:** Chained ($C_i = E(P_i \oplus C_{i-1})$). Needs IV. Secure.
*   **CTR:** Counter based. Parallel, random access.

### 2.4 RSA Algorithm
**Theory:** Integer factorization.

**Detailed Steps:**
1.  **Key Gen:**
    *   Select primes $p, q$. Compute $n = p \times q$ and $\phi(n) = (p-1)(q-1)$.
    *   Select $e$ (coprime to $\phi(n)$).
    *   Compute $d$ such that $d \times e \equiv 1 \pmod{\phi(n)}$.
    *   Public: $\{e, n\}$, Private: $\{d, n\}$.
2.  **Encryption:** $C = M^e \pmod n$.
3.  **Decryption:** $M = C^d \pmod n$.

### 2.5 Diffie-Hellman Key Exchange
**Theory:** Discrete Logarithm. Used to share secret over insecure channel.
**Mechanism:**
*   Global: Prime $q$, root $\alpha$.
*   Alice: Select private $X_A$, send $Y_A = \alpha^{X_A} \pmod q$.
*   Bob: Select private $X_B$, send $Y_B = \alpha^{X_B} \pmod q$.
*   **Shared Secret:** $K = (Y_B)^{X_A} \pmod q = (Y_A)^{X_B} \pmod q$.

---

## UNIT III – Integrity, Authentication & System Security

### 3.1 Digital Signatures
**Process:**
1.  **Sign:** Hash message $H(M)$. Encrypt Hash with **Sender's Private Key**.
2.  **Verify:** Decrypt Signature with **Sender's Public Key**. Compare with calculated $H(M)$.

### 3.2 Kerberos V5 (Detailed)
**Concept:** TTP-based auth (KDC). No password transmission.
**Steps:**
1.  **AS_REQ:** Client asks AS for TGT.
2.  **AS_REP:** AS sends $\{SessionKey_{C-TGS}\}$ encrypted with Client Pass, and **TGT** encrypted with TGS Key.
3.  **TGS_REQ:** Client sends TGT + Authenticator + Service ID to TGS.
4.  **TGS_REP:** TGS validates TGT. Sends **Service Ticket** (encrypted with Service Key) + $SessionKey_{C-Service}$.
5.  **AP_REQ:** Client sends Service Ticket + Authenticator to Service.
6.  **Access:** Service validates Ticket.

### 3.3 Database Security Models
*   **Inference:** Deducing sensitive data from aggregate queries.
*   **Bell-LaPadula (Confidentiality):**
    *   *No Read Up:* Can't read higher classification.
    *   *No Write Down:* Can't write to lower classification.
*   **Biba (Integrity):**
    *   *No Read Down:* Can't read lower integrity.
    *   *No Write Up:* Can't write to higher integrity.

---

## UNIT IV – IP Security, Web Security, IDS & Firewalls

### 4.1 IP Security (IPsec) – Deep Dive

**Definition:** A suite of protocols providing security (authentication, integrity, confidentiality) at the **IP Layer (Layer 3)**. It secures all traffic (TCP, UDP, ICMP) transparently.

#### 4.1.1 Security Associations (SA)
An SA is a logical connection describing *how* to protect traffic. It is **simplex** (one-way). Two-way communication requires two SAs.
**Key Parameters in SA:**
1.  **SPI (Security Parameter Index):** A 32-bit ID in the packet header that tells the receiver *which* SA to use to decrypt/validate this packet.
2.  **Sequence Number Counter:** 32-bit counter, incremented for each packet. Used for **Anti-Replay**.
3.  **Anti-Replay Window:** A sliding window (e.g., 64 packets) tracked by the receiver.
    *   *Mechanism:* If a received packet has a Sequence Number *lower* than the window (old) or *inside* the window but marked as received (duplicate), it is **discarded**.
    *   *Goal:* Prevents hackers from capturing valid packets and resending them later.
4.  **IP Destination Address:** Endpoint of the SA.
5.  **Protocol:** AH or ESP.

#### 4.1.2 IPsec Protocols (AH vs ESP)

**1. Authentication Header (AH):**
*   **Provides:** Data Origin Authentication, Integrity, Anti-Replay.
*   **Does NOT Provide:** Encryption (Confidentiality).
*   **Header Fields:** Next Header, Payload Length, Reserved, **SPI**, **Sequence Number**, **ICV** (Integrity Check Value - HMAC).
*   **Limitations:** Incompatible with NAT (Network Address Translation) because it hashes the IP header (including IP addresses which NAT changes).

**2. Encapsulating Security Payload (ESP):**
*   **Provides:** **Confidentiality (Encryption)**, Authentication, Integrity, Anti-Replay.
*   **Packet Structure:**
    *   *ESP Header:* SPI, Sequence Number.
    *   *Payload:* Encrypted Data.
    *   *ESP Trailer:* Padding, Next Header.
    *   *ESP Auth:* ICV (HMAC).
*   **NAT-Traversal:** Works better with NAT (especially with UDP encapsulation).

#### 4.1.3 IPsec Modes
*   **Transport Mode:** Protects **Payload Only**. Original IP header is visible. Used for Host-to-Host.
    *   `[Orig IP][ESP Header][TCP/Data][ESP Trailer]`
*   **Tunnel Mode:** Protects **Entire Packet**. Adds New IP Header. Used for VPN (Gateway-to-Gateway).
    *   `[New IP][ESP Header][Orig IP][TCP/Data][ESP Trailer]`

#### 4.1.4 Internet Key Exchange (IKE)
Automated protocol to negotiate keys and establish SAs. Uses Diffie-Hellman.

**Phase 1: IKE SA Establishment (Secure Channel)**
*   Goal: Create a secure management channel to negotiate Phase 2.
*   **Main Mode (6 messages):** Slower, safer. Hides identities (encrypted).
*   **Aggressive Mode (3 messages):** Faster. Identities sent in cleartext (vulnerable to sniffing).

**Phase 2: IPsec SA Establishment**
*   **Quick Mode:** Negotiates the actual keys for AH/ESP traffic using the Phase 1 channel. Generates key material (Keying Material).

### 4.2 Web Security (SSL/TLS)
**TLS 1.2 Handshake:**
1.  **ClientHello:** Random$_C$, CipherSuites.
2.  **ServerHello:** Random$_S$, Chosen Cipher.
3.  **Certificate:** Server's Public Key.
4.  **ClientKeyExchange:** Pre-Master Secret (PMS) encrypted with Server Public Key.
5.  **Key Gen:** Master Secret = $f(PMS, Random_C, Random_S)$.
6.  **Finished:** MAC checks.

### 4.3 IDS & Firewalls
*   **IDS:** Detects intrusions. **HIDS** (Host), **NIDS** (Network). Signature vs Anomaly based.
*   **Firewall Types:**
    *   *Packet Filter:* Source/Dest IP/Port. Stateless.
    *   *Stateful:* Tracks connection state (SYN, ESTABLISHED).
    *   *Application Proxy:* Inspects payload (e.g., HTTP URL).
    *   *Circuit Gateway:* Monitors handshake only.
*   **Placement:** **Screened Subnet (DMZ)** puts public servers between two firewalls (External & Internal) for isolation.

---
**Use this Master Revision file for your final 2-3 days of study. It covers the syllabus breadth and depth required.**