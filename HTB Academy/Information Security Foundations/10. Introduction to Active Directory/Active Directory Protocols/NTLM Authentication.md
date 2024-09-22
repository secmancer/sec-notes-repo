Here’s a concise set of notes based on the provided text:

---

### Active Directory Authentication Methods

Active Directory (AD) supports several authentication protocols beyond Kerberos and LDAP, including LM, NTLM, NTLMv1, and NTLMv2. These can be used or abused by applications and services in AD environments.

#### **Hash Protocol Comparison**:
- **NTLM**: Symmetric key cryptography, no mutual authentication, uses a random number, Domain Controller (DC) involved.
- **NTLMv1**: Symmetric key cryptography, no mutual authentication, MD4 hash with a random number, DC involved.
- **NTLMv2**: Symmetric key cryptography, no mutual authentication, MD4 hash with a random number, DC involved.
- **Kerberos**: Uses both symmetric and asymmetric cryptography, mutual authentication, encrypted ticket (DES, MD5), relies on DC/Key Distribution Center (KDC).

---

### **LM Hash (LAN Manager)**
- **Introduction**: Oldest Windows password storage mechanism; debuted in 1987.
- **Hashing Process**: 
  - Passwords split into two 7-character chunks.
  - Each chunk is encrypted using DES keys and the string `KGS!@#$%`.
  - Weak due to limited character set (69 characters) and being case insensitive.
  - Easy to crack using modern tools like Hashcat, especially since passwords under 7 characters result in the same second half of the hash.
- **Storage**: Stored in the SAM database on Windows hosts and NTDS.DIT on DCs.
- **Vulnerabilities**: Disabled by default in Windows Vista/Server 2008 due to weak security.
- **Example LM Hash**: `299bd128c1101fd6`.

---

### **NT Hash (NTLM)**
- **Introduction**: Modern password hash used in Windows systems.
- **Protocol**: Challenge-response authentication using three messages (NEGOTIATE_MESSAGE, CHALLENGE_MESSAGE, AUTHENTICATE_MESSAGE).
- **Hashing Process**: 
  - MD4 hash of the little-endian UTF-16 password value (MD4(UTF-16-LE(password))).
  - Stronger than LM hash but still vulnerable to brute-force attacks.
- **Example NTLM Hash**: `b4b9b02e6f09a9bd760f388b67351e2b`.

---

### **NTLMv1 (Net-NTLMv1)**
- **Challenge/Response Mechanism**: Uses NT and LM hash; vulnerable to offline cracking.
- **Hashing Process**: 
  - Server sends an 8-byte random challenge.
  - Client responds with a 24-byte response.
  - Response is created using DES encryption on chunks of the hash.
- **Example NTLMv1 Hash**: `338d08f8e26de93300000000000000000000000000000000`.

---

### **NTLMv2 (Net-NTLMv2)**
- **Improvements Over NTLMv1**: Hardened against certain attacks, includes client-generated challenge.
- **Hashing Process**:
  - Server sends an 8-byte challenge.
  - Client generates a 16-byte HMAC-MD5 hash of the challenge and credentials.
  - Additional response includes a client challenge with the current time, random values, and domain name.
- **Example NTLMv2 Hash**: `08ca45b7d7ea58ee:88dcbe4446168966a153a0064958dac6`.

---

### **Domain Cached Credentials (MSCache2)**
- **Purpose**: Used to authenticate when a domain-joined machine cannot communicate with the DC.
- **Storage**: Cached credentials stored in the registry (`HKEY_LOCAL_MACHINE\SECURITY\Cache`).
- **Hashing Process**: Very slow to crack and not usable in pass-the-hash attacks.
- **Example DCC2 Hash**: `$DCC2$10240#bjones#e4e938d12fe5974dc42a90120bd9c90f`.

---

### **Attacks & Vulnerabilities**:
- **Pass-the-hash (PtH)**: An attacker can authenticate with just the NTLM hash without needing the plaintext password.
- **Offline Cracking**: LM and NTLM hashes are susceptible to brute-force and dictionary attacks, especially with powerful GPUs.
- **NTLM Relay**: NTLM authentication can be relayed to another system to gain unauthorized access.

---

### **Recommendations**:
- **Disable LM Hashes**: Group Policy can disable LM hashes to prevent their use.
- **Use Kerberos**: Kerberos is the preferred protocol wherever possible due to its mutual authentication and stronger cryptography.

---


![[ntlm_auth.png]]


## Questions
- What Hashing protocol is capable of symmetric and asymmetric cryptography?
	- Kerberos
- NTLM uses three messages to authenticate; Negotiate, Challenge, and <__>. What is the missing message? (fill in the blank)
	- authenticate
- How many hashes does the Domain Cached Credentials mechanism save to a host by default?
	- 10