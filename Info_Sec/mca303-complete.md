# MCA-303 Information Security – Complete Study Material
## 3rd Semester MCA – End Semester Exam Preparation

> **Preparation Strategy (2–3 Days):** This comprehensive guide integrates material from all prescribed textbooks. Study sequentially, focusing on diagrams, equations, and marked sections.

---

## UNIT I – Introduction to Information Security & Basics of Cryptography

### 1.1 Basic Security Concepts

**Information Security** protects information assets from threats and vulnerabilities using the **CIA Triad**:

- **Confidentiality** – Data accessible only to authorized entities
- **Integrity** – Data cannot be modified undetectably
- **Availability** – Systems accessible when needed

**Extended Security Goals:**
- **Authentication** – Verifying identity of users/systems
- **Authorization** – Defining access permissions
- **Non-repudiation** – Sender cannot deny transmission
- **Accountability** – Actions traceable to responsible parties

### 1.2 Security Attacks – Classification & Analysis

#### 1.2.1 Attack Classifications (Stallings)

**Passive Attacks:**
- Eavesdropping, traffic analysis
- Do not modify data
- Difficult to detect; focus on prevention

**Active Attacks:**
- Masquerade, replay, modification, denial of service
- Modify data or create false data
- Difficult to prevent; focus on detection

#### 1.2.2 Motives Behind Attacks

1. **Financial gain** – Fraud, ransomware, data theft
2. **Espionage** – Corporate/military intelligence
3. **Hacktivism** – Political or social agenda
4. **Personal gain** – Fame, challenge, revenge

#### 1.2.3 Vulnerabilities and Threats

- **Vulnerability:** Weakness in system design, implementation, or operation
- **Threat:** Circumstance that could exploit vulnerability
- **Attack:** Assault on system security derived from threat
- **Risk:** Potential for loss when threat exploits vulnerability

**Risk Assessment Formula (conceptual):**
\[ \text{Risk} = \text{Threat} \times \text{Vulnerability} \times \text{Impact} \]

### 1.3 Defense Strategies (Five-Layer Approach)

1. **Prevention** – Block attacks before occurrence
   - Strong authentication, encryption, input validation, patching
2. **Detection** – Identify attacks in progress
   - IDS/IPS, SIEM, log monitoring, anomaly detection
3. **Response** – Contain and mitigate damage
   - Incident response plans, isolation, credential revocation
4. **Recovery** – Restore normal operations
   - Backups, disaster recovery, system rebuilds
5. **Forensics** – Investigate and learn from incidents
   - Evidence collection, chain of custody, root cause analysis

### 1.4 Types of Security Attacks

#### 1.4.1 Denial of Service (DoS) and Distributed DoS (DDoS)

**Objective:** Overwhelm system resources to make service unavailable

**DoS Types:**
- **Flooding attacks:** ICMP flood, UDP flood, HTTP flood
- **Protocol attacks:** TCP SYN flood, ping of death
- **Application layer attacks:** Slowloris, HTTP POST flood

**TCP SYN Flood Mechanism:**

```text
Attacker              Target Server
   |                      |
   |--SYN-------------->  | (allocate resources)
   |<---SYN+ACK---------- | (wait for ACK)
   |  (no ACK sent)       | (connection half-open)
   |--SYN (new)-------->  | (allocate more)
   |--SYN (new)-------->  | (repeat until exhaustion)
   
Result: Server backlog queue full, legitimate users denied
```

**DDoS Characteristics:**
- Uses botnet (network of compromised machines)
- Amplification attacks (e.g., DNS amplification, NTP amplification)
- Harder to trace and block

**Defense Mechanisms:**
- **SYN cookies** – Stateless connection tracking
- **Rate limiting** – Throttle requests per source
- **Traffic filtering** – Block malicious patterns
- **Over-provisioning** – Excess bandwidth/resources
- **DDoS mitigation services** – Cloudflare, Akamai

#### 1.4.2 Session Hijacking and Spoofing

**Session Hijacking:**
Attacker takes over legitimate user's active session by stealing session identifier (cookie/token).

**Attack Vectors:**
- Cross-Site Scripting (XSS)
- Session sniffing on unencrypted HTTP
- Man-in-the-Middle (MitM) attacks
- Session fixation

**Session Hijacking Flow:**

```text
User                Web Server              Attacker
  |                      |                      |
  |--Login-------------> |                      |
  |<-SessionID=ABC123--- |                      |
  |                      |                      |
  |                      |<--Sniff/Steal--------|
  |                      |   SessionID=ABC123   |
  |                      |                      |
  |                      |<--Request (fake)-----|
  |                      |   Cookie: SessionID=ABC123
  |                      |--Grant Access------> |
```

**IP Spoofing:**
Forging source IP address in packets to:
- Bypass IP-based authentication
- Launch reflection attacks
- Hide attacker identity

**Countermeasures:**
- Use **HTTPS** (TLS) for all sessions
- **Secure cookie flags:** HttpOnly, Secure, SameSite
- **Session regeneration** after authentication
- **IP binding** – tie session to client IP (with caveats)
- **Short timeouts** and re-authentication

#### 1.4.3 Phishing and Social Engineering

**Phishing:** Fraudulent attempt to obtain sensitive information by impersonating trusted entity.

**Types:**
- **Email phishing** – Mass emails mimicking banks, services
- **Spear phishing** – Targeted at specific individuals/organizations
- **Whaling** – Targeting high-level executives
- **Smishing** – SMS-based phishing
- **Vishing** – Voice/phone phishing

**Defense:**
- User awareness training
- Email authentication: **SPF**, **DKIM**, **DMARC**
- Anti-phishing filters
- Multi-factor authentication (MFA)
- URL inspection and domain verification

#### 1.4.4 Buffer Overflow Attack (Stallings - Software Security)

**Definition:** Writing more data to buffer than it can hold, overwriting adjacent memory.

**Classic Stack-Based Buffer Overflow:**

```text
Memory Layout (Stack grows downward):

High Address
+------------------+
| Return Address   | <-- Target for overwrite
+------------------+
| Saved Frame Ptr  |
+------------------+
| Local Variables  |
+------------------+
| Buffer[64]       | <-- Vulnerable buffer
+------------------+
Low Address

Attack: Input 100 bytes into Buffer[64]
→ Overflow overwrites Return Address
→ Redirect execution to attacker's shellcode
```

**Attack Equation:**
If buffer size = \( n \) bytes, input size = \( m \) bytes where \( m > n \):
\[ \text{Overflow} = m - n \text{ bytes overwrite adjacent memory} \]

**Real-World Example Code (Vulnerable):**

```c
void vulnerable_function(char *input) {
    char buffer[64];
    strcpy(buffer, input);  // No bounds checking!
}
```

If `input` is 100 bytes, overflow occurs.

**Types of Buffer Overflow:**
1. **Stack-based** – Overwrite return address
2. **Heap-based** – Corrupt heap metadata
3. **Integer overflow** – Arithmetic overflow leads to undersized buffer

**Defenses:**
- **Bounds checking** – Use safe functions (strncpy, snprintf)
- **Stack canaries** – Random value before return address
- **ASLR** – Address Space Layout Randomization
- **DEP/NX bit** – Non-executable stack/heap
- **Compiler protections** – Stack-smashing protection (-fstack-protector)

#### 1.4.5 Format String Attack

**Vulnerability:** User input used directly as format string in printf-family functions.

**Vulnerable Code:**

```c
printf(user_input);  // DANGEROUS!
```

**Attack Examples:**

```c
// Read stack memory:
user_input = "%x %x %x %x"  // Leaks stack values

// Write arbitrary memory:
user_input = "%n"  // Writes number of bytes output so far
```

**Format Specifiers Exploited:**
- `%x` – Read from stack
- `%s` – Read string from memory (can cause crash)
- `%n` – Write to memory (most dangerous)

**Defense:**

```c
printf("%s", user_input);  // SAFE - fixed format string
```

#### 1.4.6 SQL Injection (SQLI)

**Definition:** Inserting malicious SQL code into application queries.

**Vulnerable Code (Pseudo):**

```sql
query = "SELECT * FROM users WHERE username='" + userInput + "' 
         AND password='" + passInput + "'";
```

**Attack Example:**
```
userInput = "admin' --"
Resulting query:
SELECT * FROM users WHERE username='admin' --' AND password='...'
(Comment -- ignores rest, bypasses password check)
```

**Attack Types:**
1. **In-band (Classic)** – Results returned in same channel
2. **Inferential (Blind)** – No direct output, infer from behavior
3. **Out-of-band** – Data exfiltrated via different channel (DNS, HTTP)

**UNION-based Attack:**

```sql
' UNION SELECT table_name, column_name FROM information_schema.columns --
```

**Defense (OWASP Guidelines):**
- **Prepared statements (Parameterized queries):**

```sql
PreparedStatement ps = conn.prepareStatement(
    "SELECT * FROM users WHERE username=? AND password=?");
ps.setString(1, userInput);
ps.setString(2, passInput);
```

- **Stored procedures** (with proper parameterization)
- **Input validation** – Whitelist acceptable inputs
- **Least privilege** – Database accounts with minimal permissions
- **Web Application Firewall (WAF)**

#### 1.4.7 Malicious Software (Malware) – Detailed Classification

**Stallings Classification:**

**1. Needs Host Program:**
- **Virus** – Attaches to executable, replicates when host runs
- **Logic Bomb** – Triggers on specific condition (date, event)
- **Trojan Horse** – Appears legitimate, performs malicious actions
- **Backdoor** – Provides unauthorized access

**2. Independent:**
- **Worm** – Self-replicating, spreads via network
- **Zombie/Bot** – Compromised machine under remote control
- **Botnet** – Network of zombies controlled by botmaster

**Virus Types (by Target):**

1. **Parasitic Virus** – Attaches to executable files
2. **Memory-Resident Virus** – Loads into memory, infects programs run
3. **Boot Sector Virus** – Infects boot sector of disk
4. **Stealth Virus** – Hides from antivirus detection
5. **Polymorphic Virus** – Changes signature with each infection
6. **Metamorphic Virus** – Rewrites entire code structure
7. **Macro Virus** – Embedded in document macros (Word, Excel)

**Virus Life Cycle:**

```text
Dormant Phase → Propagation Phase → Triggering Phase → Execution Phase
     ↑                                                        |
     └────────────────────────────────────────────────────────┘
```

**Ransomware:**
- Encrypts victim's files
- Demands payment (usually cryptocurrency) for decryption key
- Examples: WannaCry, CryptoLocker, Petya

**Spyware/Adware:**
- Monitors user activity
- Collects personal information
- Displays unwanted advertisements

**Rootkit:**
- Hides presence of malware
- Operates at kernel level (kernel-mode rootkit)
- Very difficult to detect and remove

**Anti-Virus Evolution (Stallings - 4 Generations):**

**First Generation – Simple Scanners**
- Use virus signatures (unique byte patterns)
- Fast but only detect known viruses

**Second Generation – Heuristic Scanners**
- Detect suspicious code patterns
- Use checksums to detect file modifications
- More false positives

**Third Generation – Activity Traps**
- Memory-resident, monitor system calls
- Detect virus-like behavior in real-time

**Fourth Generation – Full-Featured Protection**
- Combination of techniques
- Sandbox execution, cloud analysis
- Behavioral analysis, machine learning

**Advanced Anti-Virus Techniques:**

1. **Generic Decryption:**
   - CPU emulation to decrypt and analyze before execution

2. **Digital Immune System (IBM):**
   - Distributed detection and analysis
   - Rapid signature updates

3. **Behavior-Blocking Software:**
   - Monitors dangerous actions (file access, registry changes)
   - Blocks or prompts before allowing

### 1.5 Data Protection, Response, Recovery & Forensics

**Data Protection Mechanisms:**
- **Encryption** – At rest and in transit
- **Access control** – RBAC, MAC, DAC
- **Data masking** – Hide sensitive data
- **Backup** – Regular, tested, off-site

**Incident Response Phases (NIST SP 800-61):**

1. **Preparation** – Plans, tools, training
2. **Detection & Analysis** – Identify and scope incident
3. **Containment, Eradication, Recovery**
   - Short-term containment (isolate)
   - Long-term containment (temporary fix)
   - Eradication (remove malware/vulnerability)
   - Recovery (restore to normal)
4. **Post-Incident Activity** – Lessons learned, improve

**Computer Forensics:**
- **Identification** – Recognize potential evidence
- **Preservation** – Prevent alteration
- **Collection** – Document and gather evidence
- **Examination** – Extract and analyze data
- **Analysis** – Draw conclusions
- **Presentation** – Report findings (legal/technical)

**Chain of Custody:** Documentation trail showing evidence handling from collection to court.

### 1.6 Basics of Cryptography

**Cryptography:** Science of secret writing to achieve:
- Confidentiality
- Authentication
- Integrity
- Non-repudiation

**Terminology:**
- **Plaintext (P)** – Original message
- **Ciphertext (C)** – Encrypted message
- **Encryption (E)** – Transform plaintext to ciphertext
- **Decryption (D)** – Transform ciphertext to plaintext
- **Key (K)** – Parameter controlling transformation
- **Cryptanalysis** – Breaking cryptographic security
- **Cryptology** – Cryptography + Cryptanalysis

#### 1.6.1 Symmetric Cipher Model

**Symmetric (Secret-Key) Cryptography:** Same key for encryption and decryption.

**Model Diagram:**

```text
          Plaintext P
               |
               v
        +-------------+
        | Encryption  |<------ Secret Key K
        |  E_K(P)     |
        +-------------+
               |
               v
          Ciphertext C
               |
      (Transmitted over
       insecure channel)
               |
               v
        +-------------+
        | Decryption  |<------ Secret Key K
        |  D_K(C)     |
        +-------------+
               |
               v
          Plaintext P
```

**Mathematical Notation:**
- Encryption: \( C = E_K(P) \)
- Decryption: \( P = D_K(C) \)
- Property: \( D_K(E_K(P)) = P \)

**Key Distribution Problem:** How to securely share secret key between parties?

**Requirements for Secure Use:**
1. Strong encryption algorithm \( E \)
2. Sender and receiver must obtain secret key securely
3. Key must remain secret

#### 1.6.2 Substitution Techniques

**Substitution Cipher:** Replace plaintext elements with ciphertext elements.

**1. Caesar Cipher (Shift Cipher):**

- **Encryption:** \( C = (P + k) \bmod 26 \)
- **Decryption:** \( P = (C - k) \bmod 26 \)

Where \( P, C \in \{0,1,...,25\} \) (A=0, B=1,..., Z=25), and \( k \) is shift key.

**Example (k=3):**
```
Plaintext:  HELLO
Shift by 3: KHOOR (Ciphertext)
```

**Security:** Only 25 possible keys – easily broken by brute force.

**2. Monoalphabetic Substitution:**

Arbitrary permutation of alphabet:
```
Plain:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Cipher: D K V Q F I B J W P E S C X H T Z Y R L G M E A O U
```

**Key space:** 26! ≈ \( 4 \times 10^{26} \) – large, but vulnerable to **frequency analysis**.

**Letter Frequency in English:**
E (12.7%), T (9.1%), A (8.2%), O (7.5%), I (7.0%), N (6.7%)...

**3. Playfair Cipher:**
- Uses 5×5 matrix of letters (I/J combined)
- Encrypts pairs of letters (digrams)
- More resistant to frequency analysis

**4. Polyalphabetic Ciphers (Vigenère):**

Uses keyword to vary substitution:

**Vigenère Encryption:**
\[ C_i = (P_i + K_i) \bmod 26 \]

Where \( K_i \) is \( i \)-th letter of repeating keyword.

**Example:**
```
Plaintext:  ATTACKATDAWN
Key:        LEMONLEMONLE
Ciphertext: LXFOPVEFRNHR
```

**Security:** More secure than monoalphabetic, but vulnerable to **Kasiski examination** and **Index of Coincidence** analysis.

**5. One-Time Pad (Vernam Cipher):**

- Random key same length as message, used only once
- \( C_i = (P_i + K_i) \bmod 26 \) or \( C = P \oplus K \) (binary)
- **Perfectly secure** (Shannon) if:
  - Key is truly random
  - Key length ≥ message length
  - Key used only once
  - Key kept secret

**Problem:** Key distribution and key length impractical for most applications.

#### 1.6.3 Transposition (Permutation) Techniques

**Transposition Cipher:** Rearrange order of plaintext characters; no substitution.

**Rail Fence Cipher (2 rails):**

```text
Plaintext: MEETMEAFTERTHETOGAPARTY

Arrangement:
M E M A T R H T G P R Y
 E T E F E T E O A A T

Ciphertext: MEMATRHTGPRYETEFETOAAT
```

**Columnar Transposition:**

Plaintext written in rows, read column by column using key order.

```text
Key:         4 3 1 2 5 6
Plaintext:   a t t a c k
             p o s t p o
             n e d u n t
             i l t o m o
             r r o w

Read by key order (1,2,3,4,5,6):
Ciphertext: TNSRR AOOWI POELR ATPTM ACTUO KTONW
```

**Product Cipher:** Combination of substitution and transposition (used in modern ciphers like DES).

#### 1.6.4 Confusion and Diffusion (Shannon's Principles)

**Claude Shannon (1949)** defined two key properties for secure ciphers:

**1. Confusion:**
- Relationship between ciphertext and key should be complex
- Each bit of ciphertext should depend on several parts of key
- **Achieved by:** Substitution operations (S-boxes)
- **Purpose:** Obscure relationship between key and ciphertext

**2. Diffusion:**
- Each bit of plaintext affects many bits of ciphertext
- Statistical structure of plaintext is dissipated
- **Achieved by:** Transposition/permutation operations (P-boxes)
- **Purpose:** Spread plaintext statistics throughout ciphertext

**In Modern Block Ciphers:**
- Multiple rounds alternate substitution and permutation
- DES: 16 rounds of substitution (S-boxes) + permutation
- AES: SubBytes (confusion) + ShiftRows/MixColumns (diffusion)

#### 1.6.5 Block and Stream Ciphers

**Block Cipher:**
- Processes plaintext in **fixed-size blocks** (e.g., 64, 128 bits)
- Each block encrypted independently (in ECB) or with chaining
- Examples: DES (64-bit), AES (128-bit), Blowfish

**Block Cipher Diagram:**

```text
Plaintext Block (n bits)
        |
        v
   +---------+
   | Encrypt |<---- Key K
   |  E_K    |
   +---------+
        |
        v
Ciphertext Block (n bits)
```

**Stream Cipher:**
- Encrypts data **one bit (or byte) at a time**
- Generates **keystream** from key
- Fast, less overhead
- Examples: RC4, ChaCha20, A5/1 (GSM)

**Stream Cipher Diagram:**

```text
Key K -----> Keystream Generator -----> k1, k2, k3, k4, ...
                                           |
Plaintext bits:                      p1, p2, p3, p4, ...
                                           |
                                           v
                                          XOR
                                           |
                                           v
Ciphertext bits:                     c1, c2, c3, c4, ...

Encryption: ci = pi ⊕ ki
Decryption: pi = ci ⊕ ki  (since (pi ⊕ ki) ⊕ ki = pi)
```

**Comparison:**

| Feature | Block Cipher | Stream Cipher |
|---------|--------------|---------------|
| Unit Size | Fixed block (64/128 bits) | Bit or byte |
| Speed | Slower | Faster |
| Error Propagation | Limited to block (in ECB) | Single bit |
| Use Case | File encryption, disk | Real-time (voice, video) |
| Examples | DES, AES, 3DES | RC4, ChaCha20 |

---

## UNIT II – Secret Key & Public Key Cryptography

### 2.1 Data Encryption Standard (DES)

**DES Specifications:**
- **Type:** Symmetric block cipher
- **Block size:** 64 bits
- **Key size:** 56 bits (64 bits with 8 parity bits)
- **Rounds:** 16 Feistel rounds
- **Structure:** Feistel network
- **Standard:** FIPS 46 (1977), withdrawn in 2005

#### 2.1.1 DES Algorithm Structure

**High-Level DES Flow:**

```text
64-bit Plaintext
      |
      v
Initial Permutation (IP)
      |
      v
Split into L0 (32 bits) | R0 (32 bits)
      |
      v
+---------------------------+
| Round 1                   |
| L1 = R0                   |
| R1 = L0 ⊕ F(R0, K1)       |
+---------------------------+
      |
      v
+---------------------------+
| Round 2                   |
| L2 = R1                   |
| R2 = L1 ⊕ F(R1, K2)       |
+---------------------------+
      |
      v
      ...
      |
      v
+---------------------------+
| Round 16                  |
| L16 = R15                 |
| R16 = L15 ⊕ F(R15, K16)   |
+---------------------------+
      |
      v
Swap: R16 | L16
      |
      v
Final Permutation (IP⁻¹)
      |
      v
64-bit Ciphertext
```

**Feistel Round Equations:**

For round \( i \) (where \( 1 \leq i \leq 16 \)):
\[
L_i = R_{i-1}
\]
\[
R_i = L_{i-1} \oplus F(R_{i-1}, K_i)
\]

Where:
- \( L_{i-1}, R_{i-1} \) – Left and right halves from previous round
- \( F \) – Feistel function
- \( K_i \) – 48-bit subkey for round \( i \)
- \( \oplus \) – XOR operation

**DES Feistel Function F:**

```text
R(i-1) (32 bits)
      |
      v
Expansion Permutation (E)
      |
      v
48 bits
      |
      v
    XOR <---- Ki (48-bit subkey)
      |
      v
48 bits
      |
      v
Split into 8 × 6-bit groups
      |
      v
+---------------------------+
| S-box 1 ... S-box 8       |
| (6 bits → 4 bits each)    |
+---------------------------+
      |
      v
32 bits
      |
      v
Permutation (P)
      |
      v
F(R(i-1), Ki) (32 bits)
```

**S-Boxes (Substitution Boxes):**
- 8 S-boxes, each with 6-bit input → 4-bit output
- Non-linear transformation (provides **confusion**)
- Each S-box is 4 rows × 16 columns table
- Outer bits (1st and 6th) select row
- Inner bits (2nd-5th) select column

**Example S-Box 1 (partial):**

```text
      Column (middle 4 bits: 0-15)
Row     0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15
(outer)
 0     14  4 13  1  2 15 11  8  3 10  6 12  5  9  0  7
 1      0 15  7  4 14  2 13  1 10  6 12 11  9  5  3  8
 ...
```

**Key Schedule:**
- 64-bit key → discard 8 parity bits → 56 bits
- Split into C0 (28 bits) and D0 (28 bits)
- For each round \( i \):
  - Left circular shift Ci-1 and Di-1 by 1 or 2 positions
  - Permuted Choice 2 (PC-2) selects 48 bits from 56 to form Ki

#### 2.1.2 Strength of DES

**Vulnerabilities:**
- **56-bit key** too small → brute force feasible
- **DES Cracker (EFF, 1998):** Broke DES in 56 hours
- **Distributed.net (2002):** Broke DES in ~22 hours

**Cryptanalysis Attacks:**
- **Differential Cryptanalysis** (Biham & Shamir, 1990)
- **Linear Cryptanalysis** (Matsui, 1993)

**Result:** DES considered insecure for sensitive data; replaced by 3DES and AES.

### 2.2 Block Cipher Design Principles (Stallings)

1. **Number of rounds:** More rounds = higher security (DES: 16, AES: 10/12/14)
2. **Function F:** Should be highly non-linear
3. **Key schedule:** Subkeys should be sufficiently different and independent
4. **Avalanche effect:** Small change in plaintext/key → large change in ciphertext
   - DES achieves full avalanche after 5 rounds

### 2.3 Block Cipher Modes of Operation

Block ciphers need **modes** to encrypt messages longer than block size.

Let:
- \( E_K \) = Block encryption function with key \( K \)
- \( D_K \) = Block decryption function with key \( K \)
- \( P_i \) = Plaintext block \( i \)
- \( C_i \) = Ciphertext block \( i \)
- \( IV \) = Initialization Vector

#### 2.3.1 Electronic Code Book (ECB)

**Encryption:** \( C_i = E_K(P_i) \)
**Decryption:** \( P_i = D_K(C_i) \)

**Diagram:**

```text
P1 --->[E_K]---> C1
P2 --->[E_K]---> C2
P3 --->[E_K]---> C3
```

**Characteristics:**
- **Simplest** mode
- Each block encrypted independently
- **Parallel** encryption/decryption possible
- **Weakness:** Identical plaintext blocks → identical ciphertext (patterns leak)
- **Use:** Not recommended except for single-block messages

#### 2.3.2 Cipher Block Chaining (CBC)

**Encryption:**
\[
C_1 = E_K(P_1 \oplus IV)
\]
\[
C_i = E_K(P_i \oplus C_{i-1}) \quad \text{for } i > 1
\]

**Decryption:**
\[
P_1 = D_K(C_1) \oplus IV
\]
\[
P_i = D_K(C_i) \oplus C_{i-1} \quad \text{for } i > 1
\]

**Diagram:**

```text
Encryption:
IV ⊕ P1 --->[E_K]---> C1 ⊕ P2 --->[E_K]---> C2 ⊕ P3 --->[E_K]---> C3

Decryption:
C1 --->[D_K]---> ⊕ IV = P1
C2 --->[D_K]---> ⊕ C1 = P2
C3 --->[D_K]---> ⊕ C2 = P3
```

**Characteristics:**
- Each ciphertext block depends on all previous plaintext blocks
- Identical plaintext blocks encrypted differently
- **Error propagation:** Error in \( C_i \) affects \( P_i \) and \( P_{i+1} \)
- Decryption can be **parallelized**, encryption cannot
- **IV** must be unpredictable
- **Use:** General-purpose encryption (TLS, disk encryption)

#### 2.3.3 Cipher Feedback (CFB)

Turns block cipher into **stream cipher**.

**s-bit CFB Encryption:**
\[
C_i = P_i \oplus \text{MSB}_s(E_K(\text{Shift Register}_i))
\]

**Characteristics:**
- Encrypts \( s \) bits at a time (typically \( s = 8 \) for byte)
- No need for padding
- Self-synchronizing (error recovery after block size)

#### 2.3.4 Output Feedback (OFB)

**Encryption:**
\[
O_i = E_K(O_{i-1}), \quad O_0 = IV
\]
\[
C_i = P_i \oplus O_i
\]

**Characteristics:**
- Generates keystream independent of plaintext/ciphertext
- **No error propagation** (bit error in \( C_i \) only affects \( P_i \))
- Encryption and decryption identical
- Keystream can be pre-computed

#### 2.3.5 Counter (CTR)

**Encryption:**
\[
C_i = P_i \oplus E_K(\text{Counter}_i)
\]

Where \( \text{Counter}_i = \text{Nonce} \parallel i \)

**Characteristics:**
- Each block uses unique counter value
- **Fully parallelizable** encryption and decryption
- **Random access** to any block
- No error propagation
- **Use:** Modern applications (IPsec ESP, GCM mode)

**Mode Comparison:**

| Mode | Encryption Parallel | Decryption Parallel | Error Propagation | Use Case |
|------|---------------------|---------------------|-------------------|----------|
| ECB  | Yes | Yes | One block | Not recommended |
| CBC  | No | Yes | Two blocks | General purpose |
| CFB  | No | Yes (limited) | Self-sync | Stream applications |
| OFB  | No (but pre-compute) | No | None | Stream, error-prone channels |
| CTR  | Yes | Yes | None | High-speed, random access |

### 2.4 Triple DES (3DES / TDEA)

**Purpose:** Increase effective key length to counter brute-force attacks on DES.

**3DES with Three Keys (K1, K2, K3):**

**Encryption:**
\[
C = E_{K3}(D_{K2}(E_{K1}(P)))
\]

**Decryption:**
\[
P = D_{K1}(E_{K2}(D_{K3}(C)))
\]

**Diagram:**

```text
Plaintext P
    |
    v
  [E_K1]
    |
    v
  [D_K2]
    |
    v
  [E_K3]
    |
    v
Ciphertext C
```

**Why Encrypt-Decrypt-Encrypt (EDE)?**
- If K1 = K2 = K3 = K, then 3DES reduces to single DES (backward compatible)

**3DES Key Options:**

1. **Three independent keys (Keying Option 1):**
   - Total: 168 bits (3 × 56)
   - Effective security: ~112 bits (meet-in-the-middle attack)

2. **Two keys (Keying Option 2):** K1 ≠ K2, K3 = K1
   - Total: 112 bits
   - Effective security: ~80 bits

3. **One key (Keying Option 3):** K1 = K2 = K3 (backward compatible DES)

**Strength:**
- More secure than DES
- Much slower (3× DES operations)
- Being phased out in favor of AES

**Vulnerabilities:**
- **Meet-in-the-middle attack** reduces effective key length
- Block size still 64 bits (smaller than AES's 128 bits)

**Standards:**
- NIST: Deprecated after 2023
- PCI DSS: Prohibited after 2024

### 2.5 Public Key Cryptography – Principles

**Asymmetric Cryptography:** Uses **two keys**:
- **Public key** (\( K_{pub} \)): Freely distributed
- **Private key** (\( K_{pri} \)): Kept secret

**Properties:**
1. Computationally infeasible to derive \( K_{pri} \) from \( K_{pub} \)
2. \( E_{K_{pub}}(P) = C \), \( D_{K_{pri}}(C) = P \)
3. Optionally (for signatures): \( E_{K_{pri}}(P) = C \), \( D_{K_{pub}}(C) = P \)

**Applications:**
1. **Encryption/Decryption:** Confidentiality
2. **Digital Signatures:** Authentication, integrity, non-repudiation
3. **Key Exchange:** Establish shared secret key

**Mathematical Basis:**
- **RSA:** Integer factorization problem
- **Diffie-Hellman, DSA:** Discrete logarithm problem
- **ECC:** Elliptic curve discrete logarithm problem

**Advantages:**
- No need for secure key distribution channel
- Supports digital signatures
- Enables key exchange over insecure channel

**Disadvantages:**
- **Much slower** than symmetric cryptography (100-1000× slower)
- Larger key sizes required
- Usually used in hybrid systems (public key for key exchange, symmetric for data)

### 2.6 RSA Algorithm (Rivest, Shamir, Adleman, 1978)

**Security Basis:** Difficulty of factoring large composite numbers.

#### 2.6.1 RSA Key Generation

**Steps:**

1. **Choose two large primes** \( p \) and \( q \) (typically 1024-2048 bits each)

2. **Compute modulus:**
   \[
   n = p \times q
   \]

3. **Compute Euler's totient function:**
   \[
   \varphi(n) = (p-1)(q-1)
   \]

4. **Choose public exponent** \( e \):
   - \( 1 < e < \varphi(n) \)
   - \( \gcd(e, \varphi(n)) = 1 \)
   - Common choice: \( e = 65537 = 2^{16} + 1 \) (fast encryption)

5. **Compute private exponent** \( d \):
   \[
   d \equiv e^{-1} \pmod{\varphi(n)}
   \]
   i.e., \( e \times d \equiv 1 \pmod{\varphi(n)} \)
   
   Use Extended Euclidean Algorithm to find \( d \).

**Public Key:** \( (e, n) \)
**Private Key:** \( (d, n) \)
**Keep secret:** \( p, q, \varphi(n), d \)

#### 2.6.2 RSA Encryption and Decryption

**Encryption (using public key):**
Given plaintext \( M \) where \( 0 \leq M < n \):
\[
C = M^e \bmod n
\]

**Decryption (using private key):**
\[
M = C^d \bmod n
\]

**Why it works (mathematical proof):**

By Euler's theorem: If \( \gcd(M, n) = 1 \), then
\[
M^{\varphi(n)} \equiv 1 \pmod{n}
\]

Since \( e \times d \equiv 1 \pmod{\varphi(n)} \), we have \( ed = 1 + k\varphi(n) \) for some integer \( k \).

Thus:
\[
C^d = (M^e)^d = M^{ed} = M^{1 + k\varphi(n)} = M \cdot (M^{\varphi(n)})^k \equiv M \cdot 1^k \equiv M \pmod{n}
\]

#### 2.6.3 RSA Example (Small Numbers)

**Key Generation:**

1. Choose \( p = 61, q = 53 \)
2. \( n = 61 \times 53 = 3233 \)
3. \( \varphi(n) = 60 \times 52 = 3120 \)
4. Choose \( e = 17 \) (since \( \gcd(17, 3120) = 1 \))
5. Compute \( d \): \( 17d \equiv 1 \pmod{3120} \)
   
   Using Extended Euclidean Algorithm: \( d = 2753 \)
   
   Verify: \( 17 \times 2753 = 46801 = 15 \times 3120 + 1 \)

**Public Key:** \( (17, 3233) \)
**Private Key:** \( (2753, 3233) \)

**Encryption:**
Let \( M = 123 \)
\[
C = 123^{17} \bmod 3233 = 855
\]

**Decryption:**
\[
M = 855^{2753} \bmod 3233 = 123 \checkmark
\]

#### 2.6.4 RSA for Digital Signatures

**Signing (using private key):**
\[
S = M^d \bmod n
\]

**Verification (using public key):**
\[
M' = S^e \bmod n
\]

If \( M' = M \), signature is valid.

**In Practice:**
Sign **hash** of message, not message itself:
\[
S = H(M)^d \bmod n
\]

#### 2.6.5 Security of RSA

**Key Lengths (NIST recommendations):**
- **1024 bits:** Deprecated
- **2048 bits:** Minimum for current use (equivalent to ~112-bit symmetric)
- **3072 bits:** Recommended for long-term (equivalent to ~128-bit symmetric)
- **4096 bits:** High security

**Attacks:**
1. **Factoring \( n \):** Best known - General Number Field Sieve (GNFS)
2. **Small exponent attack:** If \( e \) is small and message is short
3. **Timing attacks:** Exploit timing variations in modular exponentiation
4. **Chosen ciphertext attack:** Need proper padding (OAEP)

**Padding Schemes (Essential):**
- **PKCS#1 v1.5:** Older, has vulnerabilities
- **OAEP (Optimal Asymmetric Encryption Padding):** Recommended

### 2.7 Diffie-Hellman Key Exchange (1976)

**Purpose:** Establish shared secret key over public channel.

**Security Basis:** Discrete logarithm problem.

**Discrete Logarithm Problem:**
Given \( g, p, \) and \( y = g^x \bmod p \), find \( x \).
(Hard for large \( p \))

#### 2.7.1 Diffie-Hellman Protocol

**Public Parameters (agreed beforehand):**
- Large prime \( q \) (1024-3072 bits)
- Primitive root \( \alpha \) modulo \( q \)

**Steps:**

1. **Alice:**
   - Chooses secret \( X_A \), where \( 0 < X_A < q \)
   - Computes public value:
     \[
     Y_A = \alpha^{X_A} \bmod q
     \]
   - Sends \( Y_A \) to Bob

2. **Bob:**
   - Chooses secret \( X_B \), where \( 0 < X_B < q \)
   - Computes public value:
     \[
     Y_B = \alpha^{X_B} \bmod q
     \]
   - Sends \( Y_B \) to Alice

3. **Alice computes shared secret:**
   \[
   K = Y_B^{X_A} \bmod q = (\alpha^{X_B})^{X_A} = \alpha^{X_A X_B} \bmod q
   \]

4. **Bob computes shared secret:**
   \[
   K = Y_A^{X_B} \bmod q = (\alpha^{X_A})^{X_B} = \alpha^{X_A X_B} \bmod q
   \]

Both obtain **same shared secret** \( K \).

**Diagram:**

```text
Alice                           Bob
-----                           ---
Choose random XA              Choose random XB
Compute YA = α^XA mod q       Compute YB = α^XB mod q

       YA
    --------->
                                Compute K = YA^XB mod q
       YB                            = α^(XA·XB) mod q
    <---------

Compute K = YB^XA mod q
     = α^(XA·XB) mod q

Both now share secret K
```

#### 2.7.2 Diffie-Hellman Example

**Public parameters:**
- \( q = 23 \) (prime)
- \( \alpha = 5 \) (primitive root mod 23)

**Alice:**
- \( X_A = 6 \) (secret)
- \( Y_A = 5^6 \bmod 23 = 8 \)

**Bob:**
- \( X_B = 15 \) (secret)
- \( Y_B = 5^{15} \bmod 23 = 19 \)

**Shared Secret:**
- Alice: \( K = 19^6 \bmod 23 = 2 \)
- Bob: \( K = 8^{15} \bmod 23 = 2 \) ✓

**Attacker (Eve) knows:** \( q = 23, \alpha = 5, Y_A = 8, Y_B = 19 \)
**To find \( K \), needs to solve:** \( 5^x \equiv 8 \pmod{23} \) (discrete log – hard for large \( q \))

#### 2.7.3 Security and Limitations

**Vulnerability:**
- **Man-in-the-Middle (MitM) attack:** No authentication of parties

**Man-in-the-Middle Attack:**

```text
Alice          Attacker (Mallory)          Bob
  |                    |                     |
  |--YA------------>   |                     |
  |              [intercept, use YM1]        |
  |                    |---YM1------------>  |
  |                    |<--YM2------------|  |
  |<--YM2----------    |                     |
  |              [intercept]                 |
  
Alice shares KAM with Mallory
Bob shares KMB with Mallory
Mallory decrypts and re-encrypts all traffic
```

**Defense:**
- **Authenticated Diffie-Hellman:** Sign exchanged values with certificates (TLS)
- **Static Diffie-Hellman:** Long-term DH keys certified by CA

**Use Cases:**
- **TLS/SSL handshake** (DHE, ECDHE)
- **IPsec IKE** (Internet Key Exchange)
- **SSH** key exchange

### 2.8 Advanced Encryption Standard (AES) – Detailed

**AES (Rijndael):** Winner of NIST competition (2001), replaced DES.

**Specifications:**
- **Block size:** 128 bits (fixed)
- **Key sizes:** 128, 192, or 256 bits
- **Rounds:**
  - AES-128: 10 rounds
  - AES-192: 12 rounds
  - AES-256: 14 rounds
- **Structure:** Substitution-Permutation Network (not Feistel)

#### 2.8.1 AES State Representation

Data represented as **4×4 matrix of bytes** (called **State**):

```text
128-bit block (16 bytes):
b0 b1 b2 b3 b4 b5 b6 b7 b8 b9 b10 b11 b12 b13 b14 b15

Arranged in State matrix (column-major):
     Column 0  1  2  3
Row 0  [ b0  b4  b8  b12 ]
Row 1  [ b1  b5  b9  b13 ]
Row 2  [ b2  b6 b10  b14 ]
Row 3  [ b3  b7 b11  b15 ]
```

#### 2.8.2 AES Round Structure

**Initial Round:**
- AddRoundKey

**Main Rounds (9/11/13):**
1. SubBytes
2. ShiftRows
3. MixColumns
4. AddRoundKey

**Final Round:**
1. SubBytes
2. ShiftRows
3. AddRoundKey (no MixColumns)

**Overall Structure:**

```text
Plaintext (128 bits)
      |
      v
[ AddRoundKey ] (Round 0)
      |
+-----v--------------------+
| [ SubBytes ]             |
| [ ShiftRows ]            |  Repeat 9/11/13 times
| [ MixColumns ]           |
| [ AddRoundKey ]          |
+--------------------------+
      |
      v
[ SubBytes ]
[ ShiftRows ]
[ AddRoundKey ] (Final round, no MixColumns)
      |
      v
Ciphertext (128 bits)
```

#### 2.8.3 AES Transformations

**1. SubBytes (Substitution) – Provides Confusion**

Each byte in State replaced using **S-Box** (substitution box).

\[
\text{State}[i,j] = \text{S-Box}[\text{State}[i,j]]
\]

**S-Box properties:**
- Non-linear transformation
- Based on multiplicative inverse in GF(2^8) plus affine transformation
- Fixed 16×16 lookup table

**Example:**
If byte value is `0x53`:
- Row = 5, Column = 3
- S-Box[5,3] = `0xed`

**S-Box (partial):**

```text
     0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F
0   63 7C 77 7B F2 6B 6F C5 30 01 67 2B FE D7 AB 76
1   CA 82 C9 7D FA 59 47 F0 AD D4 A2 AF 9C A4 72 C0
...
5   ... ... ... ED ...
```

**2. ShiftRows (Permutation) – Provides Diffusion**

Cyclically shift each row of State to the left:
- **Row 0:** No shift
- **Row 1:** Shift 1 byte left
- **Row 2:** Shift 2 bytes left
- **Row 3:** Shift 3 bytes left

**Before:**

```text
s00 s01 s02 s03
s10 s11 s12 s13
s20 s21 s22 s23
s30 s31 s32 s33
```

**After ShiftRows:**

```text
s00 s01 s02 s03
s11 s12 s13 s10  (shifted left by 1)
s22 s23 s20 s21  (shifted left by 2)
s33 s30 s31 s32  (shifted left by 3)
```

**Purpose:** Ensures that bytes from each column are spread to different columns.

**3. MixColumns (Mixing) – Provides Diffusion**

Each **column** of State treated as polynomial over GF(2^8) and multiplied by fixed polynomial.

\[
\begin{bmatrix} s'_{0,c} \\ s'_{1,c} \\ s'_{2,c} \\ s'_{3,c} \end{bmatrix}
=
\begin{bmatrix} 02 & 03 & 01 & 01 \\ 01 & 02 & 03 & 01 \\ 01 & 01 & 02 & 03 \\ 03 & 01 & 01 & 02 \end{bmatrix}
\times
\begin{bmatrix} s_{0,c} \\ s_{1,c} \\ s_{2,c} \\ s_{3,c} \end{bmatrix}
\]

(in GF(2^8))

**Effect:** Each output byte is function of all 4 input bytes in column.

**Example (for one column):**
\[
s'_{0,c} = (02 \cdot s_{0,c}) \oplus (03 \cdot s_{1,c}) \oplus s_{2,c} \oplus s_{3,c}
\]

(Multiplication `02·x` and `03·x` in GF(2^8) using irreducible polynomial)

**4. AddRoundKey (Key Mixing)**

XOR State with round key:

\[
\text{State}[i,j] = \text{State}[i,j] \oplus \text{RoundKey}[i,j]
\]

**Properties:**
- Simple and fast (bitwise XOR)
- Reversible (XOR is self-inverse)
- Combines data with key

#### 2.8.4 AES Key Expansion

**Goal:** Expand 128/192/256-bit key into (Nr+1) round keys (128 bits each).

- AES-128: 10 rounds → 11 round keys (176 bytes)
- AES-192: 12 rounds → 13 round keys (208 bytes)
- AES-256: 14 rounds → 15 round keys (240 bytes)

**Process:**
1. Initial key copied to first round key
2. Generate subsequent words using:
   - XOR with previous word
   - Every Nk-th word: Apply RotWord, SubWord, XOR with round constant (Rcon)

**Key Expansion Function (simplified for AES-128):**

```text
W[0...3] = Initial Key (4 words)
For i = 4 to 43:
  If i mod 4 = 0:
    temp = SubWord(RotWord(W[i-1])) XOR Rcon[i/4]
    W[i] = W[i-4] XOR temp
  Else:
    W[i] = W[i-4] XOR W[i-1]
```

#### 2.8.5 AES Decryption

Each transformation has an inverse:
- **InvSubBytes:** Use inverse S-Box
- **InvShiftRows:** Shift right instead of left
- **InvMixColumns:** Multiply by inverse matrix
- **AddRoundKey:** Same (XOR is self-inverse)

**Decryption applies inverse operations in reverse order.**

#### 2.8.6 AES Security and Performance

**Security:**
- **No practical attacks** on full-round AES
- Best attack (biclique): Slightly better than brute force, impractical
- **Key recommendations:**
  - AES-128: Adequate for most applications
  - AES-256: Government/military, long-term secrets

**Performance:**
- **Hardware:** Very fast with AES-NI instructions (Intel/AMD CPUs)
- **Software:** Efficient implementation using table lookups
- Much faster than 3DES

**Comparison:**

| Cipher | Block Size | Key Size | Rounds | Status |
|--------|------------|----------|--------|--------|
| DES | 64 bits | 56 bits | 16 | Insecure (deprecated) |
| 3DES | 64 bits | 112/168 bits | 48 | Being phased out |
| AES-128 | 128 bits | 128 bits | 10 | Secure, recommended |
| AES-256 | 128 bits | 256 bits | 14 | High security |

---

## UNIT III – Hash Functions, Authentication, OS & DB Security

### 3.1 Cryptographic Hash Functions

**Hash Function \( H \):** Maps arbitrary-length input to fixed-length output.

\[
h = H(M)
\]

Where:
- \( M \) = Message (any length)
- \( h \) = Hash value / Message Digest (fixed length, e.g., 160, 256 bits)

#### 3.1.1 Properties of Cryptographic Hash Functions

**1. One-way (Pre-image Resistance):**
Given \( h \), computationally infeasible to find any \( M \) such that \( H(M) = h \).

**2. Second Pre-image Resistance (Weak Collision Resistance):**
Given \( M_1 \), computationally infeasible to find \( M_2 \neq M_1 \) such that \( H(M_1) = H(M_2) \).

**3. Collision Resistance (Strong Collision Resistance):**
Computationally infeasible to find any pair \( (M_1, M_2) \) where \( M_1 \neq M_2 \) and \( H(M_1) = H(M_2) \).

**Note:** Collision resistance ⇒ Second pre-image resistance ⇒ One-way

**4. Avalanche Effect:**
Small change in input causes significant change in output (≈50% bits flip).

#### 3.1.2 Applications of Hash Functions

1. **Message integrity:** Verify data not modified
2. **Digital signatures:** Sign hash instead of entire message
3. **Password storage:** Store \( H(\text{password}) \), not plaintext
4. **Key derivation:** Generate keys from passwords (PBKDF2, bcrypt)
5. **Proof-of-work:** Bitcoin mining
6. **File/data deduplication:** Identify unique content

#### 3.1.3 Secure Hash Algorithm (SHA) Family

**SHA-1:**
- Output: 160 bits
- **Status:** **Broken** – collision found (2017), deprecated
- Don't use for security

**SHA-2 Family (Widely Used):**
- **SHA-224:** 224-bit output
- **SHA-256:** 256-bit output (most common)
- **SHA-384:** 384-bit output
- **SHA-512:** 512-bit output
- **Structure:** Merkle-Damgård construction, based on Davies-Meyer compression

**SHA-256 Process:**

1. **Padding:** Append bits so length ≡ 448 (mod 512), then append 64-bit length
2. **Parse:** Divide into 512-bit blocks \( M_1, M_2, \ldots, M_N \)
3. **Initialize:** 8 hash values (H0-H7) from constants
4. **Process each block:**
   - 64 rounds of operations
   - Uses AND, OR, XOR, addition mod 2^32, rotation
5. **Output:** Concatenate final hash values

**SHA-256 Round Function (simplified):**

Uses:
- 64 constants \( K_0, \ldots, K_{63} \)
- 8 working variables \( a, b, c, d, e, f, g, h \)
- Logical functions: Ch, Maj, Σ0, Σ1

**SHA-3 (Keccak):**
- **Winner of NIST competition (2012)**
- **Different structure:** Sponge construction (not Merkle-Damgård)
- More resistant to length-extension attacks
- Variants: SHA3-224, SHA3-256, SHA3-384, SHA3-512

**Hash Function Comparison:**

| Algorithm | Output Size | Status | Use |
|-----------|-------------|--------|-----|
| MD5 | 128 bits | Broken | Don't use |
| SHA-1 | 160 bits | Broken | Legacy only |
| SHA-256 | 256 bits | Secure | Recommended |
| SHA-512 | 512 bits | Secure | High security |
| SHA-3 | Variable | Secure | Modern alternative |

### 3.2 Message Authentication Code (MAC)

**MAC:** Cryptographic checksum using secret key for **authentication** and **integrity**.

\[
\text{MAC} = C_K(M)
\]

Where:
- \( C \) = MAC algorithm
- \( K \) = Secret key (shared between sender and receiver)
- \( M \) = Message

**Process:**

```text
Sender                        Receiver
------                        --------
M, K --->[MAC]---> MAC        M, MAC, K
                   |                |
      Send M || MAC                 v
                            Compute MAC' = C_K(M)
                            Compare MAC' with MAC
                            If equal → authentic & unmodified
```

**Requirements:**
1. Knowing \( M \) and \( \text{MAC} \), infeasible to find \( K \)
2. Knowing \( M \) and \( \text{MAC} \), infeasible to construct valid \( \text{MAC}(M') \)

**MAC vs. Hash:**
- Hash: No key, only integrity (public verification)
- MAC: With key, integrity + authentication (only key holder can verify/create)

### 3.3 HMAC (Hash-based Message Authentication Code)

**HMAC (RFC 2104):** Constructs MAC using cryptographic hash function.

**Definition:**

\[
\text{HMAC}_K(M) = H\left((K^+ \oplus \text{opad}) \parallel H((K^+ \oplus \text{ipad}) \parallel M)\right)
\]

Where:
- \( H \) = Hash function (e.g., SHA-256)
- \( K^+ \) = Key padded to block size of \( H \)
- \( \text{ipad} \) = Inner padding (0x36 repeated)
- \( \text{opad} \) = Outer padding (0x5C repeated)
- \( \parallel \) = Concatenation
- \( \oplus \) = XOR

**Step-by-Step HMAC:**

1. **Pad key:** If \( |K| < \text{block size} \), pad with zeros; if \( |K| > \text{block size} \), hash \( K \) first
2. **Inner hash:**
   \[
   h_1 = H((K^+ \oplus \text{ipad}) \parallel M)
   \]
3. **Outer hash:**
   \[
   \text{HMAC} = H((K^+ \oplus \text{opad}) \parallel h_1)
   \]

**Example:** HMAC-SHA256 produces 256-bit MAC.

**Advantages:**
- Uses existing hash functions (easy to implement)
- Secure if underlying hash is secure
- Resistant to length-extension attacks

**Applications:**
- **TLS/SSL:** Integrity check in record protocol
- **IPsec:** Authentication in AH and ESP
- **JWT:** Signature algorithm (HS256 = HMAC-SHA256)

### 3.4 Digital Signatures

**Purpose:** Provide **authentication**, **integrity**, and **non-repudiation**.

**Analogy:** Digital equivalent of handwritten signature.

**Properties:**
1. **Authenticity:** Verifies sender's identity
2. **Integrity:** Ensures message not altered
3. **Non-repudiation:** Sender cannot deny sending

**Digital Signature Process:**

```text
Sender                                      Receiver
------                                      --------
M --->[Hash]---> h                          M, S
            |                               |
            v                               v
   [Encrypt with                       [Hash]---> h'
    private key]                       [Decrypt S with
            |                           sender's public key]
            v                               |
         S (signature)                      v
                                          h''
      Send M || S                     Compare h' and h''
                                      If equal → valid signature
```

**Mathematical Notation:**

**Signing:**
\[
S = \text{Sign}_{K_{pri}}(H(M))
\]

**Verification:**
\[
h' = H(M), \quad h'' = \text{Verify}_{K_{pub}}(S)
\]

If \( h' = h'' \), signature valid.

**With RSA:**
- **Sign:** \( S = H(M)^d \bmod n \)
- **Verify:** \( h'' = S^e \bmod n \), compare with \( h' = H(M) \)

**Properties vs. MAC:**

| Feature | MAC | Digital Signature |
|---------|-----|-------------------|
| Key Type | Symmetric (shared) | Asymmetric (public/private) |
| Authentication | Yes | Yes |
| Integrity | Yes | Yes |
| Non-repudiation | No | Yes |
| Performance | Fast | Slower |
| Key Distribution | Requires secure channel | Public key can be shared openly |

### 3.5 Digital Signature Algorithm (DSA)

**DSA (FIPS 186):** US government standard for digital signatures.

**Based on:** Discrete logarithm problem and ElGamal signatures.

#### 3.5.1 DSA Parameters

**Global Public-Key Parameters (shared by group):**
- \( p \) = Prime modulus (1024-3072 bits)
- \( q \) = Prime divisor of \( p-1 \) (160-256 bits)
- \( g \) = Generator, where \( g = h^{(p-1)/q} \bmod p \)

**User Keys:**
- **Private key:** \( x \) (random, \( 0 < x < q \))
- **Public key:** \( y = g^x \bmod p \)

#### 3.5.2 DSA Signature Generation

**To sign message \( M \):**

1. Compute hash: \( h = H(M) \) (typically SHA-256)

2. Choose random \( k \), where \( 0 < k < q \)

3. Compute:
   \[
   r = (g^k \bmod p) \bmod q
   \]

4. Compute:
   \[
   s = k^{-1}(h + xr) \bmod q
   \]

5. **Signature:** \( (r, s) \)

#### 3.5.3 DSA Signature Verification

**To verify signature \( (r, s) \) on message \( M \):**

1. Verify \( 0 < r < q \) and \( 0 < s < q \); else reject

2. Compute hash: \( h = H(M) \)

3. Compute:
   \[
   w = s^{-1} \bmod q
   \]

4. Compute:
   \[
   u_1 = hw \bmod q
   \]
   \[
   u_2 = rw \bmod q
   \]

5. Compute:
   \[
   v = \left((g^{u_1} y^{u_2}) \bmod p\right) \bmod q
   \]

6. **Accept if \( v = r \)**

**Why it works:** Mathematical properties of discrete logarithm and modular arithmetic ensure only holder of private key \( x \) can generate valid \( s \).

### 3.6 Authentication Protocols

**Purpose:** Verify identity of communicating parties.

#### 3.6.1 Challenge-Response Authentication

**Prevent replay attacks** by using fresh challenge.

**Protocol:**

```text
Alice                           Bob
  |                              |
  |<----Challenge (nonce)--------|
  |                              |
  |--Response (Encrypt/Sign)---->|
  |    challenge with key        |
                           Bob verifies response
```

**Symmetric version:**
- Response = \( E_K(\text{nonce}) \)

**Asymmetric version:**
- Response = \( \text{Sign}_{K_{pri}}(\text{nonce}) \)

### 3.7 Kerberos Authentication Service

**Kerberos:** Network authentication protocol using **symmetric cryptography** and **trusted third party**.

**Developed at MIT, used in:** Windows Active Directory, UNIX/Linux.

#### 3.7.1 Kerberos Architecture

**Entities:**
1. **Client (C):** User/workstation
2. **Application Server (V):** Service client wants to access
3. **Key Distribution Center (KDC):**
   - **Authentication Server (AS):** Verifies client identity
   - **Ticket Granting Server (TGS):** Issues service tickets

**Tickets:** Encrypted credentials with limited lifetime.

#### 3.7.2 Kerberos Protocol (Simplified)

**Phase 1: Authentication (Get TGT)**

1. **Client → AS:** Username
2. **AS → Client:**
   - **Ticket Granting Ticket (TGT):** Encrypted with TGS key
   - **Session key \( K_{C,TGS} \):** Encrypted with client's key (derived from password)

**Phase 2: Get Service Ticket**

3. **Client → TGS:**
   - TGT
   - Authenticator (encrypted with \( K_{C,TGS} \))
   - Requested service ID

4. **TGS → Client:**
   - **Service Ticket:** Encrypted with service key
   - **Session key \( K_{C,V} \):** Encrypted with \( K_{C,TGS} \)

**Phase 3: Access Service**

5. **Client → Server (V):**
   - Service Ticket
   - Authenticator (encrypted with \( K_{C,V} \))

6. **Server → Client:**
   - Confirmation (encrypted with \( K_{C,V} \)) – optional, for mutual authentication

**Kerberos Diagram:**

```text
Client (C)                AS                    TGS                  Server (V)
   |                       |                     |                      |
   |---Request TGT-------->|                     |                      |
   |<--TGT + KC,TGS--------|                     |                      |
   |                       |                     |                      |
   |---TGT + Request--------------------------->|                      |
   |<--Service Ticket + KC,V--------------------|                      |
   |                       |                     |                      |
   |---Service Ticket + Authenticator----------------------------------->|
   |<--Service Response (optional)--------------------------------------|
```

#### 3.7.3 Kerberos Security Features

- **Mutual authentication:** Both client and server verified
- **Replay protection:** Timestamps in authenticators (5-minute window)
- **Limited ticket lifetime:** Reduces exposure if ticket stolen
- **No passwords on network:** Only encrypted tickets
- **Single Sign-On (SSO):** One login, access multiple services

**Limitations:**
- **Requires synchronized clocks** (for timestamps)
- **Single point of failure:** KDC compromise affects all
- **Password guessing:** Offline attacks on initial response

### 3.8 Public Key Infrastructure (PKI) & X.509

**PKI:** Framework for managing digital certificates and public keys.

#### 3.8.1 PKI Components

1. **Certificate Authority (CA):** Issues and signs certificates
2. **Registration Authority (RA):** Verifies identity before issuance
3. **Certificate Repository:** Stores certificates (directory)
4. **Certificate Revocation List (CRL):** List of revoked certificates
5. **End Entities:** Users, servers requesting certificates

#### 3.8.2 X.509 Certificate

**X.509:** ITU-T standard for public key certificates.

**Certificate Fields (v3):**

```text
Certificate:
  Version: 3
  Serial Number: Unique ID
  Signature Algorithm: RSA-SHA256
  Issuer: CA name (DN)
  Validity:
    Not Before: Start date/time
    Not After: End date/time
  Subject: Certificate owner name (DN)
  Subject Public Key Info:
    Algorithm: RSA
    Public Key: (modulus, exponent)
  Extensions: (v3)
    - Key Usage
    - Extended Key Usage
    - Subject Alternative Name
  CA Digital Signature
```

**Distinguished Name (DN) Example:**
```
CN=www.example.com, O=Example Inc, L=New York, C=US
```

#### 3.8.3 Certificate Chain and Trust

**Chain of Trust:**

```text
Root CA (self-signed)
   |
   v
Intermediate CA (signed by Root)
   |
   v
End-Entity Certificate (signed by Intermediate)
```

**Verification Process:**
1. Check certificate validity period
2. Check certificate not revoked (CRL/OCSP)
3. Verify signature chain up to trusted root CA
4. Check domain name matches (for HTTPS)

### 3.9 Email Security

#### 3.9.1 Pretty Good Privacy (PGP)

**PGP (Phil Zimmermann, 1991):** Email encryption and signing.

**PGP Services:**
1. **Confidentiality:** Symmetric encryption (AES) with session key
2. **Authentication:** Digital signatures (RSA/DSA)
3. **Compression:** ZIP before encryption
4. **Email compatibility:** Radix-64 encoding

**PGP Encryption Process:**

```text
1. Compress message (ZIP)
2. Generate random session key
3. Encrypt message with session key (AES)
4. Encrypt session key with recipient's public key (RSA)
5. Concatenate encrypted session key + encrypted message
6. Convert to Radix-64 for email
```

**PGP Signing Process:**

```text
1. Hash message (SHA-256)
2. Encrypt hash with sender's private key (RSA) → signature
3. Prepend signature to message
```

**PGP Key Management:**
- **Web of Trust:** Decentralized, users sign each other's keys
- No centralized CA (unlike X.509)

#### 3.9.2 S/MIME (Secure/Multipurpose Internet Mail Extensions)

**S/MIME:** Email security standard using **X.509 certificates** and **hierarchical PKI**.

**Differences from PGP:**

| Feature | PGP | S/MIME |
|---------|-----|--------|
| Key Management | Web of trust | PKI / X.509 |
| Trust Model | Decentralized | Hierarchical CA |
| Adoption | Individual use | Enterprise |
| Standards Body | OpenPGP (RFC 4880) | IETF (RFC 8551) |

**S/MIME Functions:**
- **Enveloped Data:** Encryption (confidentiality)
- **Signed Data:** Digital signature (authentication, integrity)
- **Clear-Signed Data:** Signature, but message readable
- **Signed and Enveloped:** Both encryption and signature

### 3.10 Operating System Protection

#### 3.10.1 Memory and Address Protection

**Goals:**
- Isolate processes from each other
- Protect OS from user processes
- Prevent unauthorized memory access

**Techniques:**

**1. Base and Limit Registers:**

```text
Process P:
  Base = 0x1000
  Limit = 0x2000

Every memory access addr:
  If (addr < Base) OR (addr >= Base + Limit):
    Raise protection fault
  Else:
    Physical address = Base + addr
```

**Diagram:**

```text
Memory:
+-----------------+
| OS Kernel       | (protected)
+-----------------+ <-- Base (0x1000)
| Process P       |
| memory space    |
+-----------------+ <-- Base + Limit (0x3000)
| Other processes |
+-----------------+
```

**2. Segmentation:**
- Memory divided into logical segments (code, data, stack)
- Each segment has base, limit, and access rights (read/write/execute)

**3. Paging:**
- Virtual memory divided into fixed-size **pages**
- Physical memory divided into **frames**
- **Page table** maps virtual pages to physical frames
- Each page table entry (PTE) has **protection bits:**
  - Read, Write, Execute
  - User/Supervisor

**4. Virtual Memory:**
- Processes use virtual addresses
- MMU (Memory Management Unit) translates to physical addresses
- Provides isolation and protection

**5. User Mode vs. Kernel Mode:**
- **User mode:** Restricted instruction set, limited memory access
- **Kernel mode:** Full privileges
- **System calls:** Controlled transition from user to kernel mode

#### 3.10.2 File Protection Mechanisms

**1. Access Control Lists (ACLs):**

Each file/directory has list of (user/group, permissions):

```text
File: report.docx
ACL:
  alice: read, write
  bob: read
  admin_group: read, write, execute
```

**2. UNIX/Linux File Permissions:**

Three permission sets: **Owner, Group, Others**

Each set has: **Read (r), Write (w), Execute (x)**

**Example:**

```bash
-rw-r--r--  1 alice users 1024 Nov 30 report.txt
```

- Owner (alice): rw- (read, write)
- Group (users): r-- (read only)
- Others: r-- (read only)

**Permission Bits (Octal):**
- r = 4, w = 2, x = 1
- Example: `chmod 644 file` = rw-r--r--

**3. Capabilities:**
- Unforgeable tokens representing access rights
- Process must possess capability to access resource
- Difficult to revoke, but fine-grained control

**4. Role-Based Access Control (RBAC):**
- Permissions assigned to **roles**
- Users assigned to roles
- Simplifies management in large organizations

```text
Role: Manager
  Permissions: read_reports, write_reports, approve_budget

User alice → Role: Manager → Permissions
```

#### 3.10.3 User Authentication in OS

**Methods:**

**1. Password-Based:**
- User enters username + password
- System compares with stored hash
- **Salted hash:** \( H(\text{password} \parallel \text{salt}) \)
  - **Salt:** Random value prevents rainbow table attacks

**Password Storage (Linux):**
```
/etc/shadow:
alice:$6$saltvalue$hashedpassword:...
      ↑   ↑           ↑
    algorithm  salt   hash
```

**2. Token-Based:**
- **Physical token:** Smart card, USB token
- **One-Time Password (OTP):** Time-based (TOTP) or counter-based (HOTP)
- **Example:** Google Authenticator, RSA SecurID

**3. Biometric:**
- **Physiological:** Fingerprint, iris, face, hand geometry
- **Behavioral:** Typing pattern, gait, voice
- **Issues:** False acceptance rate (FAR), False rejection rate (FRR)

**4. Multi-Factor Authentication (MFA):**
Combination of:
- **Something you know** (password)
- **Something you have** (token, phone)
- **Something you are** (biometric)

### 3.11 Database Security

#### 3.11.1 Security Requirements

1. **Confidentiality:** Sensitive data protected from unauthorized disclosure
2. **Integrity:** Data accurate and consistent
3. **Availability:** Database accessible when needed
4. **Accountability:** Track who accesses/modifies data

#### 3.11.2 Reliability and Integrity

**ACID Properties (Transactions):**
- **Atomicity:** All or nothing
- **Consistency:** Database remains in valid state
- **Isolation:** Concurrent transactions don't interfere
- **Durability:** Committed changes persist

**Integrity Constraints:**
- **Entity integrity:** Primary key not null and unique
- **Referential integrity:** Foreign keys reference existing primary keys
- **Domain integrity:** Values within allowed range/type
- **User-defined integrity:** Business rules

**Concurrency Control:**
- **Locking:** Prevent simultaneous conflicting access
- **Two-Phase Locking (2PL)**
- **Timestamp ordering**

#### 3.11.3 Access Control in Databases

**SQL GRANT/REVOKE:**

```sql
GRANT SELECT, UPDATE ON employees TO alice;
REVOKE DELETE ON employees FROM bob;
```

**Privileges:**
- SELECT, INSERT, UPDATE, DELETE
- CREATE, ALTER, DROP (schema)
- EXECUTE (stored procedures)

**Views for Access Control:**
Create restricted view of table:

```sql
CREATE VIEW employee_public AS
  SELECT name, department FROM employees;
  
GRANT SELECT ON employee_public TO public;
```

Hides sensitive columns (salary, SSN).

#### 3.11.4 Sensitive Data & Inference

**Sensitive Data:**
- Personal Identifiable Information (PII)
- Financial data, health records
- Trade secrets

**Inference Problem:**
Attacker deduces sensitive information from non-sensitive data.

**Example:**
```sql
-- Non-sensitive queries:
SELECT AVG(salary) FROM employees WHERE department='Sales';
SELECT COUNT(*) FROM employees WHERE department='Sales';

-- If only one employee in Sales, can infer individual salary!
```

**Defenses:**
- **Query restriction:** Limit types of queries
- **Data perturbation:** Add noise to aggregate results
- **Auditing:** Track query patterns

#### 3.11.5 Multilevel Database Security

**Objective:** Support multiple **classification levels** within single database.

**Classification Levels (Example):**
- Unclassified (U)
- Confidential (C)
- Secret (S)
- Top Secret (TS)

**Bell-LaPadula Model (Confidentiality):**

**Rules:**
1. **Simple Security (No Read Up):**
   Subject at level \( L \) cannot read data at level > \( L \)

2. **Star Property (No Write Down):**
   Subject at level \( L \) cannot write data to level < \( L \)

**Purpose:** Prevent information leakage to lower levels.

**Biba Model (Integrity):**

**Rules:**
1. **No Read Down:** Subject cannot read lower integrity data (prevent contamination)
2. **No Write Up:** Subject cannot write to higher integrity (prevent corruption)

**Multilevel Relations:**
Each tuple and attribute can have different classification.

**Example:**

| Employee | Salary | Classification |
|----------|--------|----------------|
| Alice | 50000 | Unclassified |
| Bob | 80000 (S) | Secret (entire row) |
| Charlie | 60000 | Confidential (Salary) |

User with Confidential clearance:
- Can see Alice (Unclassified)
- Cannot see Bob (Secret)
- Can see Charlie's name, but salary shows as "Classified"

**Challenges:**
- **Polyinstantiation:** Multiple versions of same data at different levels
- **Covert channels:** Indirect information flow

---

## UNIT IV – IP Security, Web Security, IDS, and Firewalls

### 4.1 IP Security (IPsec)

**IPsec:** Suite of protocols providing security at **Network Layer (IP layer)**.

**Motivation:**
- Protects all traffic above IP (TCP, UDP, ICMP)
- Transparent to applications
- Enables **Virtual Private Networks (VPNs)**

#### 4.1.1 IPsec Services

1. **Confidentiality:** Encryption of IP payloads
2. **Integrity:** Detection of modification
3. **Authentication:** Verify source identity
4. **Anti-replay:** Prevent replay attacks

#### 4.1.2 IPsec Architecture Components

**1. Security Associations (SA):**
- **One-way** relationship between sender and receiver
- Identified by:
  - **SPI (Security Parameter Index):** Unique ID
  - **Destination IP**
  - **Security Protocol (AH or ESP)**

**SA Parameters:**
- Sequence number (for anti-replay)
- Anti-replay window
- AH/ESP algorithm and keys
- Lifetime

**Security Association Database (SAD):** Stores active SAs.

**2. Security Policy Database (SPD):**
- Rules determining IPsec processing for packets
- Actions: DISCARD, BYPASS, or PROTECT

**3. Key Management:**
- **Manual:** Static pre-shared keys
- **Automated:** **Internet Key Exchange (IKE)** protocol

#### 4.1.3 IPsec Protocols

**1. Authentication Header (AH):**
- Provides **integrity** and **authentication**
- **No confidentiality** (no encryption)
- Protects entire IP packet (including header)

**2. Encapsulating Security Payload (ESP):**
- Provides **confidentiality** (encryption)
- Optionally provides **integrity** and **authentication**
- Protects only payload (not original IP header in transport mode)

#### 4.1.4 IPsec Modes

**Transport Mode:**
- Protects **payload** only
- Original IP header remains
- Used for **end-to-end** communication (host-to-host)

**Tunnel Mode:**
- Protects **entire IP packet** (header + payload)
- New IP header added
- Used for **VPNs** (gateway-to-gateway, host-to-gateway)

**Diagrams:**

**AH Transport Mode:**

```text
Original Packet:
[ IP Header | TCP/UDP Header | Data ]

With AH:
[ IP Header | AH | TCP/UDP Header | Data ]
               ↑
          Authenticates everything after IP header
```

**AH Tunnel Mode:**

```text
Original Packet:
[ IP Hdr | TCP/UDP Hdr | Data ]

With AH Tunnel:
[ New IP Hdr | AH | Original IP Hdr | TCP/UDP Hdr | Data ]
                   ↑_____ Authenticates all of this _____↑
```

**ESP Transport Mode:**

```text
Original Packet:
[ IP Header | TCP/UDP Header | Data ]

With ESP:
[ IP Header | ESP Header | TCP/UDP Header | Data | ESP Trailer | ESP Auth ]
                          ↑___ Encrypted ___↑     ↑__Authenticated__↑
```

**ESP Tunnel Mode:**

```text
Original Packet:
[ IP Hdr | TCP/UDP Hdr | Data ]

With ESP Tunnel:
[ New IP Hdr | ESP Hdr | Orig IP Hdr | TCP/UDP Hdr | Data | ESP Trailer | ESP Auth ]
                        ↑_________ Encrypted _________↑     ↑___Authenticated___↑
```

#### 4.1.5 Authentication Header (AH) Details

**AH Header Format:**

```text
0                   1                   2                   3
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Next Header  |  Payload Len  |          RESERVED             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                 Security Parameters Index (SPI)               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Sequence Number                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
|             Integrity Check Value (ICV) - MAC                 |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

**Fields:**
- **Next Header:** Protocol of protected payload (TCP=6, UDP=17)
- **SPI:** Identifies SA
- **Sequence Number:** For anti-replay
- **ICV:** HMAC-SHA256 or HMAC-SHA1 over packet

#### 4.1.6 Encapsulating Security Payload (ESP) Details

**ESP Packet Structure:**

```text
[ ESP Header | Encrypted Payload | ESP Trailer | ESP Auth ]

ESP Header:
  - SPI
  - Sequence Number

Encrypted Payload:
  - (In tunnel mode: Original IP header)
  - TCP/UDP header + Data
  - Padding

ESP Trailer:
  - Pad Length
  - Next Header

ESP Auth (optional):
  - ICV (HMAC)
```

**Encryption Algorithms:**
- AES-CBC, AES-CTR, AES-GCM (most common)
- 3DES-CBC (legacy)

**Authentication Algorithms:**
- HMAC-SHA256, HMAC-SHA1

#### 4.1.7 Combining Security Associations

**Scenarios:**

1. **Single SA:**
   - AH or ESP alone

2. **Transport Adjacency:**
   - Both AH and ESP applied to same packet
   - Example: AH for authentication, ESP for encryption

3. **Iterated Tunneling:**
   - Multiple tunnel SAs applied (multi-hop VPN)

**Example: Transport + Tunnel:**

```text
Host A --[ESP transport]--> Security Gateway --[ESP tunnel]--> Host B
```

### 4.2 Internet Key Exchange (IKE)

**Purpose:** Automated key management and SA establishment for IPsec.

**IKE = ISAKMP + Oakley + SKEME**
- Uses **Diffie-Hellman** for key exchange
- Uses **digital certificates** for authentication

**IKE Phases:**

**Phase 1: Establish IKE SA (ISAKMP SA)**
- Authenticate peers
- Establish secure channel for Phase 2
- Modes: **Main Mode** (6 messages) or **Aggressive Mode** (3 messages)

**Phase 2: Negotiate IPsec SAs**
- Use IKE SA to securely negotiate AH/ESP SAs
- **Quick Mode**

**IKEv2 (RFC 7296):** Improved version, fewer messages.

### 4.3 Web Security Considerations

**Web Threats:**
1. **Eavesdropping:** Sniffing HTTP traffic (passwords, cookies)
2. **Man-in-the-Middle:** Intercept and modify
3. **Server impersonation:** Fake websites
4. **Client-side attacks:** XSS, CSRF, clickjacking
5. **Server-side attacks:** SQL injection, command injection

**Requirements:**
- **Confidentiality:** Encrypt HTTP traffic
- **Integrity:** Detect tampering
- **Server authentication:** Verify server identity
- **Client authentication:** (Optional) verify user

### 4.4 SSL/TLS (Secure Sockets Layer / Transport Layer Security)

**TLS:** Cryptographic protocol providing security for communications over networks.

**History:**
- SSL 2.0, 3.0 (Netscape, 1990s) – deprecated (insecure)
- **TLS 1.0** (1999) – based on SSL 3.0
- **TLS 1.1** (2006)
- **TLS 1.2** (2008) – widely used
- **TLS 1.3** (2018) – latest, faster, more secure

**Position in Protocol Stack:**

```text
Application Layer (HTTP, SMTP, FTP)
         |
         v
     TLS Layer
         |
         v
   Transport Layer (TCP)
         |
         v
  Network Layer (IP)
```

#### 4.4.1 TLS Architecture

**TLS consists of two layers:**

**1. TLS Handshake Protocol:**
- Authenticate server (and optionally client)
- Negotiate cipher suite and keys
- Establish secure session

**2. TLS Record Protocol:**
- Fragment, compress, encrypt, and authenticate data
- Provides confidentiality and integrity

#### 4.4.2 TLS Handshake (Simplified TLS 1.2)

```text
Client                                  Server
  |                                       |
  |---ClientHello------------------------>|
  |  (supported cipher suites, random)    |
  |                                       |
  |<--ServerHello-------------------------|
  |  (chosen cipher, random)              |
  |<--Certificate-------------------------|
  |  (server's X.509 cert with public key)|
  |<--ServerHelloDone---------------------|
  |                                       |
  |---ClientKeyExchange------------------>|
  |  (pre-master secret encrypted with    |
  |   server's public key, or DH params)  |
  |                                       |
  |---ChangeCipherSpec------------------->|
  |---Finished (encrypted)--------------->|
  |                                       |
  |<--ChangeCipherSpec--------------------|
  |<--Finished (encrypted)----------------|
  |                                       |
  |<====== Application Data =============>|
       (encrypted and authenticated)
```

**Steps:**

1. **ClientHello:**
   - TLS version, random number, supported cipher suites, compression

2. **ServerHello:**
   - Selected cipher suite, random number, session ID

3. **Certificate:**
   - Server's X.509 certificate (contains public key)

4. **ServerHelloDone**

5. **ClientKeyExchange:**
   - **RSA:** Client generates pre-master secret, encrypts with server's public key
   - **DHE/ECDHE:** Client sends DH public value

6. **Both sides derive keys:**
   - Master secret = PRF(pre-master secret, ClientRandom, ServerRandom)
   - Session keys (encryption, MAC) derived from master secret

7. **ChangeCipherSpec + Finished:**
   - Switch to negotiated cipher
   - Finished message (encrypted MAC of handshake) verifies key agreement

8. **Application Data:** Encrypted communication begins

#### 4.4.3 TLS Record Protocol

**Record Format:**

```text
[ Content Type | Version | Length | Payload ]
```

**Processing:**
1. **Fragment:** Break data into blocks (max 16 KB)
2. **Compress:** (Optional, rarely used due to CRIME attack)
3. **Add MAC:** HMAC for integrity
4. **Encrypt:** Symmetric cipher (AES)
5. **Add TLS header**

#### 4.4.4 Cipher Suites

**Format:** TLS_KeyExchange_WITH_Encryption_MAC

**Examples:**
- `TLS_RSA_WITH_AES_128_CBC_SHA256`
  - Key exchange: RSA
  - Encryption: AES-128-CBC
  - MAC: HMAC-SHA256

- `TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384`
  - Key exchange: ECDHE (Elliptic Curve Diffie-Hellman Ephemeral)
  - Authentication: RSA
  - Encryption+MAC: AES-256-GCM (authenticated encryption)

**Modern Best Practice:**
- Use **ECDHE** or **DHE** (forward secrecy)
- Use **AES-GCM** or **ChaCha20-Poly1305** (AEAD ciphers)
- Avoid RC4, MD5, SHA1

#### 4.4.5 TLS 1.3 Improvements

- **Faster handshake:** 1-RTT (round trip time) or 0-RTT
- **Removed weak algorithms:** RC4, SHA1, CBC mode
- **Forward secrecy mandatory:** Only ephemeral key exchange (ECDHE, DHE)
- **Encrypted handshake:** More handshake messages encrypted

### 4.5 Electronic Payment

**E-Payment Requirements:**
- **Confidentiality:** Card numbers, transaction details encrypted
- **Integrity:** Detect tampering
- **Authentication:** Verify cardholder and merchant
- **Non-repudiation:** Proof of transaction
- **Anonymity:** (Optional) Privacy for buyer

**Technologies:**
- **SSL/TLS:** Encrypt communication (HTTPS)
- **3-D Secure:** Additional authentication (Verified by Visa, Mastercard SecureCode)
- **Tokenization:** Replace card number with token
- **EMV chip cards:** Chip + PIN

**Payment Flow (Simplified):**

```text
Customer --> Merchant --> Payment Gateway --> Acquiring Bank --> Card Network --> Issuing Bank
```

### 4.6 Intrusion Detection Systems (IDS)

**Intrusion:** Unauthorized access or misuse of system.

**IDS:** Monitors system/network for signs of intrusion.

#### 4.6.1 IDS Types

**1. Host-based IDS (HIDS):**
- Monitors single host (logs, file integrity, system calls)
- Examples: OSSEC, Tripwire

**2. Network-based IDS (NIDS):**
- Monitors network traffic
- Examples: Snort, Suricata, Zeek (Bro)

#### 4.6.2 Detection Approaches

**1. Signature-Based (Misuse Detection):**
- Match traffic/behavior against known attack patterns (signatures)
- **Advantages:** Low false positives, fast
- **Disadvantages:** Cannot detect new/unknown attacks (zero-days)

**2. Anomaly-Based:**
- Build profile of normal behavior
- Detect deviations from normal
- **Types:**
  - **Statistical:** Threshold on metrics (login attempts, packet rate)
  - **Machine Learning:** Train models on normal behavior
- **Advantages:** Can detect novel attacks
- **Disadvantages:** Higher false positives

**3. Stateful Protocol Analysis:**
- Understand protocol state machines
- Detect protocol violations

#### 4.6.3 Intrusion Prevention System (IPS)

**IPS = IDS + Active Response**
- Can **block** malicious traffic inline
- Placement: Inline in network path (vs. IDS passive tap)

#### 4.6.4 Password Management

**Password Security Practices:**

1. **Strong Policies:**
   - Minimum length (12+ characters)
   - Complexity requirements (mix of character types)
   - No dictionary words, personal info

2. **Secure Storage:**
   - **Never store plaintext passwords**
   - Use **salted hashing:**
     \[
     H(\text{password} \parallel \text{salt})
     \]
   - **Slow hash functions:** bcrypt, scrypt, Argon2 (resist brute force)

3. **Account Lockout:**
   - Lock account after N failed attempts
   - Throttle login attempts

4. **Password Managers:**
   - Generate and store strong, unique passwords

5. **Multi-Factor Authentication:**
   - Add second factor (OTP, biometric)

**Common Attacks:**
- **Dictionary attack:** Try common passwords
- **Brute force:** Try all combinations
- **Rainbow tables:** Precomputed hashes (defeated by salt)
- **Credential stuffing:** Reuse leaked credentials

### 4.7 Firewalls

**Firewall:** Device that controls traffic between networks based on security policy.

**Functions:**
- Enforce access control policy
- Log traffic
- Centralized security management
- Network segmentation (DMZ)

#### 4.7.1 Firewall Characteristics

**Essential Properties:**
1. **All traffic** between inside and outside must pass through firewall
2. Only **authorized traffic** (per policy) is allowed
3. Firewall itself is **immune to penetration**

#### 4.7.2 Types of Firewalls

**1. Packet-Filtering Firewall (Stateless):**

- Operates at **Network and Transport layers**
- Filters based on:
  - Source/Destination IP
  - Source/Destination Port
  - Protocol (TCP, UDP, ICMP)
  - Flags (SYN, ACK, etc.)

**Diagram:**

```text
External Network --> [ Packet Filter ] --> Internal Network
                     Checks each packet
                     against rule list
```

**Example Rules:**

| Action | Src IP | Src Port | Dst IP | Dst Port | Protocol | Comment |
|--------|--------|----------|--------|----------|----------|---------|
| Allow | Any | Any | 192.168.1.10 | 80 | TCP | Allow HTTP to web server |
| Allow | 192.168.1.0/24 | Any | Any | Any | TCP | Allow outbound TCP from LAN |
| Deny | Any | Any | Any | Any | Any | Default deny |

**Advantages:**
- Simple, fast, low overhead

**Disadvantages:**
- No context/state (can't track connections)
- Vulnerable to IP spoofing, fragmentation attacks

**2. Stateful Inspection Firewall:**

- Maintains **connection state table**
- Tracks TCP connections (SYN, established, FIN)
- Understands sessions for UDP, ICMP

**State Table Example:**

| Src IP | Src Port | Dst IP | Dst Port | Protocol | State |
|--------|----------|--------|----------|----------|-------|
| 203.0.113.5 | 54321 | 192.168.1.10 | 80 | TCP | ESTABLISHED |
| 192.168.1.20 | 8080 | 198.51.100.7 | 443 | TCP | SYN_SENT |

**Advantages:**
- Context-aware (understands connections)
- Better security than stateless

**Disadvantages:**
- More resources (maintain state)
- Can be overwhelmed (state exhaustion attacks)

**3. Application-Level Gateway (Proxy Firewall):**

- Operates at **Application Layer**
- Acts as **intermediary** (proxy) between client and server
- Inspects application-layer data (HTTP headers, URLs, etc.)

**Diagram:**

```text
Client <---> [ Proxy Firewall ] <---> Server
             (terminates connections,
              inspects payload,
              initiates new connection)
```

**Types:**
- **HTTP Proxy:** Inspect web traffic, block URLs, malware scan
- **SMTP Proxy:** Email filtering, anti-spam
- **FTP Proxy**

**Advantages:**
- Deep inspection (application content)
- Hide internal IP addresses (NAT)
- Logging and caching

**Disadvantages:**
- Slower (terminates and reconstructs connections)
- Requires proxy for each protocol

**4. Circuit-Level Gateway:**

- Monitors **TCP handshakes** (session layer)
- Once connection established, data flows without inspection
- Example: SOCKS proxy

**5. Next-Generation Firewall (NGFW):**

Combines:
- Stateful inspection
- Application awareness
- **Intrusion Prevention System (IPS)**
- Deep Packet Inspection (DPI)
- User/identity awareness
- SSL/TLS inspection

#### 4.7.3 Firewall Placement

**1. Single Firewall (Simple):**

```text
Internet <----> [ Firewall ] <----> Internal Network
```

**2. DMZ (Demilitarized Zone) Architecture:**

```text
                     [ External Firewall ]
                              |
Internet <----------> DMZ (Public Servers: Web, Mail, DNS)
                              |
                     [ Internal Firewall ]
                              |
                      Internal Network
```

**DMZ Purpose:**
- Isolate public-facing servers from internal network
- If DMZ server compromised, internal network still protected

**3. Multi-Tier:**

- Multiple DMZs for different trust levels

#### 4.7.4 Firewall Configuration

**Policy Approaches:**

**1. Default-Deny (Whitelist):**
- Block everything by default
- Explicitly allow only necessary traffic
- **Recommended** for security

**Example:**
```
1. Allow HTTP to web server
2. Allow DNS queries to DNS server
3. Allow outbound HTTPS from LAN
4. DENY ALL (implicit)
```

**2. Default-Allow (Blacklist):**
- Allow everything by default
- Explicitly block known bad traffic
- **Not recommended** (reactive, misses new threats)

**Rule Ordering:**
- **First-match:** First matching rule applied (most firewalls)
- Rules processed top-to-bottom
- **Most specific rules first, general rules last**

**Best Practices:**
- **Principle of Least Privilege:** Minimum necessary access
- Regular rule review and cleanup
- Logging and monitoring
- Test changes before production
- Document all rules

### 4.8 Trusted Systems

**Trusted System:** Computing system that can be trusted to enforce security policy reliably.

**Characteristics:**

1. **Reference Monitor:**
   - Mediates all access to objects
   - **Properties:**
     - **Tamper-proof:** Cannot be modified
     - **Always invoked:** Cannot be bypassed
     - **Small enough to verify:** Formal analysis possible

2. **Security Kernel:**
   - Hardware, firmware, software implementing reference monitor
   - Core of Trusted Computing Base (TCB)

3. **Mandatory Access Control (MAC):**
   - System enforces access control (vs. Discretionary Access Control - DAC)
   - Based on security labels (classification levels)

4. **Security Policies:**
   - **Bell-LaPadula:** Confidentiality (military)
   - **Biba:** Integrity (commercial)
   - **Chinese Wall:** Conflict of interest

5. **Assurance:**
   - **Formal verification:** Mathematical proof of security properties
   - **Security evaluation:** Common Criteria (CC), EAL levels

**Trusted Computing Base (TCB):**
- All hardware, firmware, software responsible for enforcing security
- **Smaller TCB = easier to verify and trust**

**Security Evaluation:**
- **Common Criteria (ISO 15408):**
  - **EAL1:** Functionally tested
  - **EAL4:** Methodically designed, tested, reviewed
  - **EAL7:** Formally verified design and tested

**Use Cases:**
- Military systems (classified data)
- Critical infrastructure
- High-security environments

---

## Exam Preparation Guide

### Important Formulas & Equations Summary

**Unit I:**
- Caesar Cipher: \( C = (P + k) \bmod 26 \), \( P = (C - k) \bmod 26 \)
- Vigenère: \( C_i = (P_i + K_i) \bmod 26 \)
- Stream Cipher: \( c_i = p_i \oplus k_i \)

**Unit II:**
- DES Feistel: \( L_i = R_{i-1} \), \( R_i = L_{i-1} \oplus F(R_{i-1}, K_i) \)
- 3DES: \( C = E_{K3}(D_{K2}(E_{K1}(P))) \)
- RSA Key: \( n = p \times q \), \( \varphi(n) = (p-1)(q-1) \), \( ed \equiv 1 \pmod{\varphi(n)} \)
- RSA Encrypt: \( C = M^e \bmod n \)
- RSA Decrypt: \( M = C^d \bmod n \)
- Diffie-Hellman: \( Y_A = \alpha^{X_A} \bmod q \), \( K = Y_B^{X_A} \bmod q \)

**Unit III:**
- HMAC: \( \text{HMAC}_K(M) = H((K^+ \oplus \text{opad}) \parallel H((K^+ \oplus \text{ipad}) \parallel M)) \)
- Digital Signature: \( S = \text{Sign}_{K_{pri}}(H(M)) \)

### High-Yield Topics for Short Answer (Question 9)

1. Define: vulnerability, threat, attack, risk
2. Difference between DoS and DDoS
3. What is session hijacking?
4. Buffer overflow - diagram and defense
5. SQL injection example
6. Confusion vs diffusion
7. Block cipher vs stream cipher
8. DES key size and block size
9. Triple DES structure
10. RSA key generation steps
11. Diffie-Hellman purpose
12. Properties of hash functions
13. MAC vs digital signature
14. Kerberos components
15. X.509 certificate fields
16. PGP vs S/MIME
17. Memory protection techniques
18. UNIX file permissions
19. ACID properties
20. Bell-LaPadula rules
21. IPsec AH vs ESP
22. Transport vs tunnel mode
23. TLS handshake purpose
24. IDS types
25. Firewall types
26. DMZ architecture
27. Default-deny vs default-allow

### Expected Long Questions (10 marks)

**Unit I:**
1. Explain various security attacks (DoS, session hijacking, buffer overflow, SQL injection) with diagrams and defenses
2. Explain symmetric cipher model. Discuss substitution and transposition techniques with examples
3. Define confusion and diffusion. Explain block and stream ciphers

**Unit II:**
1. Explain DES algorithm structure with diagram. Discuss strength of DES
2. Explain block cipher modes of operation (ECB, CBC) with diagrams
3. Explain RSA algorithm: key generation, encryption, decryption with example
4. Explain Diffie-Hellman key exchange protocol with diagram and example
5. Explain AES structure: SubBytes, ShiftRows, MixColumns, AddRoundKey

**Unit III:**
1. Explain cryptographic hash functions, properties, and applications. Discuss SHA family
2. Explain HMAC construction and working with diagram
3. Explain digital signature process with diagram. Discuss DSA algorithm
4. Explain Kerberos authentication protocol with architecture diagram
5. Explain X.509 certificate structure and PKI components
6. Explain PGP working for email security
7. Explain memory protection and file protection mechanisms in OS
8. Explain database security: access control, integrity, multilevel security (Bell-LaPadula)

**Unit IV:**
1. Explain IPsec architecture: AH, ESP, transport mode, tunnel mode with diagrams
2. Explain TLS/SSL handshake protocol with diagram
3. Explain intrusion detection systems: types and detection approaches
4. Explain firewall types with diagrams. Discuss firewall placement (DMZ)
5. Explain trusted systems and reference monitor concept

### 3-Day Study Plan (Final Revision)

**Day 1:**
- Morning: Unit I (attacks, cryptography basics, substitution/transposition)
- Afternoon: Unit II (DES structure, modes, Triple DES)
- Evening: Practice diagrams (symmetric cipher, DES, modes, buffer overflow)

**Day 2:**
- Morning: Unit II (RSA, Diffie-Hellman, AES structure)
- Afternoon: Unit III (Hash, HMAC, digital signatures, Kerberos)
- Evening: Unit III (PKI, email security, OS/DB security)

**Day 3:**
- Morning: Unit IV (IPsec, TLS, IDS)
- Afternoon: Unit IV (Firewalls, trusted systems)
- Evening: **Rapid fire revision** – formulas, diagrams, short answers
- Practice writing: 5 long answers (one per unit + one mixed), 10 short answers

---

**Good Luck with Your Exam!**