### Debrief
- Aside from Kerberos and LDAP, Active Directory uses several other authentication methods which can be used (and abused) by applications and services in AD. 
	- These include LM, NTLM, NTLMv1, and NTLMv2. LM and NTLM here are the hash names, and NTLMv1 and NTLMv2 are authentication protocols that utilize the LM or NT hash. 
	- There are a ton of hash and protocols for us to use, which are listed below.
	- Kerberos is often the authentication protocol of choice wherever possible. It is essential to understand the difference between the hash types and the protocols that use them.
- #### Hash Protocol Comparison

| **Hash/Protocol** | **Cryptographic technique**                          | **Mutual Authentication** | **Message Type**                | **Trusted Third Party**                         |
| ----------------- | ---------------------------------------------------- | ------------------------- | ------------------------------- | ----------------------------------------------- |
| `NTLM`            | Symmetric key cryptography                           | No                        | Random number                   | Domain Controller                               |
| `NTLMv1`          | Symmetric key cryptography                           | No                        | MD4 hash, random number         | Domain Controller                               |
| `NTLMv2`          | Symmetric key cryptography                           | No                        | MD4 hash, random number         | Domain Controller                               |
| `Kerberos`        | Symmetric key cryptography & asymmetric cryptography | Yes                       | Encrypted ticket using DES, MD5 | Domain Controller/Key Distribution Center (KDC) |



## LM
- **LAN Manager (LM) hashes** were the first password storage mechanism used by Windows, debuting in **1987** on the **OS/2** operating system.
- If **LM hashes** are in use, they are stored in the **SAM** database on Windows hosts and the **NTDS.DIT** database on **Domain Controllers**.
- Due to significant weaknesses in the **LM hashing algorithm**, it has been **disabled by default** since **Windows Vista/Server 2008**, but it may still be found in environments with older systems.
- **LM hashes** are limited to **14 characters** and are **not case sensitive**—passwords are converted to uppercase before hashing, reducing the keyspace to only **69 characters**, making them easier to crack with tools like **Hashcat**.
- Passwords longer than 14 characters are split into **two 7-character chunks** and padded with **NULL characters** if shorter.
- For each chunk, **two DES keys** are generated and encrypted using the string `KGS!@#$%`, producing two **8-byte ciphertexts** that are concatenated to form the **LM hash**.
- The process allows attackers to brute-force **seven characters** twice instead of cracking all fourteen, making LM hashes relatively fast to crack using **GPU-based tools**.
- If a password is **seven characters or less**, the second half of the LM hash is always the same, which can be determined visually without tools like **Hashcat**.
- **Group Policy** can be configured to **disable LM hashes** on password changes, enhancing security: [Network Security: Do not store LAN Manager hash value on next password change](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/network-security-do-not-store-lan-manager-hash-value-on-next-password-change).
- **Note:** Older versions of Windows (such as **NT4**, **2000**, **2003**, and **XP**) stored both **LM** and **NTLM hashes** by default, adding another layer of potential vulnerability for attackers.



## NTHash (NTLM)
- `NT LAN Manager` (NTLM) hashes are used on modern Windows systems. 
- It is a challenge-response authentication protocol and uses three messages to authenticate: a client first sends a `NEGOTIATE_MESSAGE` to the server, whose response is a `CHALLENGE_MESSAGE` to verify the client's identity. 
- Lastly, the client responds with an `AUTHENTICATE_MESSAGE`. 
- These hashes are stored locally in the SAM database or the NTDS.DIT database file on a Domain Controller. 
- The protocol has two hashed password values to choose from to perform authentication: the LM hash (as discussed above) and the NT hash, which is the MD4 hash of the little-endian UTF-16 value of the password. 
- The algorithm can be visualized as: `MD4(UTF-16-LE(password))`.
- #### NTLM Authentication Request
![image](https://academy.hackthebox.com/storage/modules/74/ntlm_auth.png)
- Even though they are considerably stronger than LM hashes (supporting the entire Unicode character set of 65,536 characters), they can still be brute-forced offline relatively quickly using a tool such as Hashcat. GPU attacks have shown that the entire NTLM 8 character keyspace can be brute-forced in under `3 hours`. 
- Longer NTLM hashes can be more challenging to crack depending on the password chosen, and even long passwords (15+ characters) can be cracked using an offline dictionary attack combined with rules. 
- NTLM is also vulnerable to the pass-the-hash attack, which means an attacker can use just the NTLM hash (after obtaining via another successful attack) to authenticate to target systems where the user is a local admin without needing to know the cleartext value of the password.
- An NT hash takes the form of `b4b9b02e6f09a9bd760f388b67351e2b`, which is the second half of the full NTLM hash.

```shell-session
Rachel:500:aad3c435b514a4eeaad3b935b51304fe:e46b9e548fa0d122de7f59fb6d48eaa2:::
```

- Looking at the hash above, we can break the NTLM hash down into its individual parts:
- `Rachel` is the username
- `500` is the Relative Identifier (RID). 500 is the known RID for the `administrator` account
- `aad3c435b514a4eeaad3b935b51304fe` is the LM hash and, if LM hashes are disabled on the system, can not be used for anything
- `e46b9e548fa0d122de7f59fb6d48eaa2` is the NT hash. 
- This hash can either be cracked offline to reveal the cleartext value (depending on the length/strength of the password) or used for a pass-the-hash attack. Below is an example of a successful pass-the-hash attack using the [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec) tool.

```shell-session
secmancer@htb[/htb]$ crackmapexec smb 10.129.41.19 -u rachel -H e46b9e548fa0d122de7f59fb6d48eaa2

SMB         10.129.43.9     445    DC01      [*] Windows 10.0 Build 17763 (name:DC01) (domain:INLANEFREIGHT.LOCAL) (signing:True) (SMBv1:False)
SMB         10.129.43.9     445    DC01      [+] INLANEFREIGHT.LOCAL\rachel:e46b9e548fa0d122de7f59fb6d48eaa2 (Pwn3d!)
```

- Now that we understand the capabilities and structure of NTLM let's examine the progression of the protocol through NTLMv1 and NTLMv2.
- **Note:** Neither LANMAN nor NTLM uses a salt.



## NTLMv1 (Net-NTLMv1)
- The NTLM protocol performs a challenge/response between a server and client using the NT hash. 
- NTLMv1 uses both the NT and the LM hash, which can make it easier to "crack" offline after capturing a hash using a tool such as [Responder](https://github.com/lgandx/Responder) or via an [NTLM relay attack](https://byt3bl33d3r.github.io/practical-guide-to-ntlm-relaying-in-2017-aka-getting-a-foothold-in-under-5-minutes.html) (both of which are out of scope for this module and will be covered in later modules on Lateral Movement). 
- The protocol is used for network authentication, and the Net-NTLMv1 hash itself is created from a challenge/response algorithm. 
- The server sends the client an 8-byte random number (challenge), and the client returns a 24-byte response. 
- These hashes can NOT be used for pass-the-hash attacks.
- #### V1 Challenge & Response Algorithm

```shell-session
C = 8-byte server challenge, random
K1 | K2 | K3 = LM/NT-hash | 5-bytes-0
response = DES(K1,C) | DES(K2,C) | DES(K3,C)
```

- An example of a full NTLMv1 hash looks like is shown below.
- #### NTLMv1 Hash Example

```shell-session
u4-netntlm::kNS:338d08f8e26de93300000000000000000000000000000000:9526fb8c23a90751cdd619b6cea564742e1e4bf33006ba41:cb8086049ec4736c
```

- NTLMv1 was the building block for modern NTLM authentication. 
- Like any protocol, it has flaws and is susceptible to cracking and other attacks. 
- Now let us move on and take a look at NTLMv2 and see how it improves on the foundation that version one set.



## NTLMv2 (Net-NTLMv2)
- The NTLMv2 protocol was first introduced in Windows NT 4.0 SP4 and was created as a stronger alternative to NTLMv1. 
- It has been the default in Windows since Server 2000. 
- It is hardened against certain spoofing attacks that NTLMv1 is susceptible to. 
- NTLMv2 sends two responses to the 8-byte challenge received by the server. 
- These responses contain a 16-byte HMAC-MD5 hash of the challenge, a randomly generated challenge from the client, and an HMAC-MD5 hash of the user's credentials. 
- A second response is sent, using a variable-length client challenge including the current time, an 8-byte random value, and the domain name.
- #### V2 Challenge & Response Algorithm

```shell-session
SC = 8-byte server challenge, random
CC = 8-byte client challenge, random
CC* = (X, time, CC2, domain name)
v2-Hash = HMAC-MD5(NT-Hash, user name, domain name)
LMv2 = HMAC-MD5(v2-Hash, SC, CC)
NTv2 = HMAC-MD5(v2-Hash, SC, CC*)
response = LMv2 | CC | NTv2 | CC*
```

- An example of an NTLMv2 hash is shown below.
- #### NTLMv2 Hash Example

```shell-session
admin::N46iSNekpT:08ca45b7d7ea58ee:88dcbe4446168966a153a0064958dac6:5c7830315c7830310000000000000b45c67103d07d7b95acd12ffa11230e0000000052920b85f78d013c31cdb3b92f5d765c783030
```

- We can see that developers improved upon v1 by making NTLMv2 harder to crack and giving it a more robust algorithm made up of multiple stages.
- We have one more authentication mechanism to discuss before moving on. 
- This method is of note to us because it does not require a persistent network connection to work.



## Domain Cached Credentials (MSCache2)
- In an AD environment, the authentication methods mentioned in this section and the previous require the host we are trying to access to communicate with the "brains" of the network, the Domain Controller. 
- Microsoft developed the [MS Cache v1 and v2](https://webstersprodigy.net/2014/02/03/mscash-hash-primer-for-pentesters/) algorithm (also known as `Domain Cached Credentials` (DCC) to solve the potential issue of a domain-joined host being unable to communicate with a domain controller (i.e., due to a network outage or other technical issue) and, hence, NTLM/Kerberos authentication not working to access the host in question. 
- Hosts save the last `ten` hashes for any domain users that successfully log into the machine in the `HKEY_LOCAL_MACHINE\SECURITY\Cache` registry key. 
- These hashes cannot be used in pass-the-hash attacks. 
- Furthermore, the hash is very slow to crack with a tool such as Hashcat, even when using an extremely powerful GPU cracking rig, so attempts to crack these hashes typically need to be extremely targeted or rely on a very weak password in use. 
- These hashes can be obtained by an attacker or pentester after gaining local admin access to a host and have the following format: `$DCC2$10240#bjones#e4e938d12fe5974dc42a90120bd9c90f`. I
- It is vital as penetration testers that we understand the varying types of hashes that we may encounter while assessing an AD environment, their strengths, weaknesses, how they can be abused (cracking to cleartext, pass-the-hash, or relayed), and when an attack may be futile (i.e., spending days attempting to crack a set of Domain Cached Credentials).



## Moving On
- Now that we have covered authentication protocols and associated password hashes let's look at users and groups in Active Directory, which are typically the most important target for penetration testers and attackers alike. 
- They can have varying privileges and be used to move laterally in an environment or gain access to protected resources.



## Questions
- What Hashing protocol is capable of symmetric and asymmetric cryptography?
	- Kerberos
- NTLM uses three messages to authenticate; Negotiate, Challenge, and blank. What is the missing message? (fill in the blank)
	- authenticate
- How many hashes does the Domain Cached Credentials mechanism saved to a host by default?
	- 10