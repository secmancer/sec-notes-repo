**Encryption Overview**
- Encryption is vital for securely transmitting data (e.g., payment info, emails) over the internet, protecting it from unauthorized access and manipulation.
- Cryptographic algorithms transform data into unreadable forms for unauthorized users, using either symmetric or asymmetric keys.
- Encryption's security depends on the method and key length; state-of-the-art methods are nearly impossible to crack.

### Symmetric Encryption
- Uses the same key for both encryption and decryption.
- The security risk arises if the key is shared or compromised.
- Widely used for encrypting large data volumes (e.g., AES, DES).
- **AES** is considered the most secure symmetric algorithm today.

### Asymmetric Encryption
- Employs two keys: a public key (for encryption) and a private key (for decryption).
- Examples include RSA, PGP, and ECC.
- **Advantages**:
    - No need for secure key exchange, as public keys can be shared openly.
    - Enables digital signatures for authentication.
- Common uses: SSL/TLS, VPNs, PKI, SSH.

### Data Encryption Standard (DES)
- A symmetric cipher using 64-bit blocks, with a 56-bit effective key length.
- Vulnerable to attacks due to shorter key length.
- **Triple DES (3DES)** is an enhanced version, using three rounds of encryption but is now considered outdated.

### Advanced Encryption Standard (AES)
- Successor to DES, AES uses key lengths of 128, 192, or 256 bits.
- Faster and more secure than DES, widely used in applications like WLAN, IPsec, SSH, and OpenSSL.

### Cipher Modes
Cipher modes define how block ciphers encrypt/decrypt data. Common modes include:
- **ECB (Electronic Code Book)**: Susceptible to attacks; not recommended.
- **CBC (Cipher Block Chaining)**: Common for disk encryption and emails; used by AES in TrueCrypt, VeraCrypt, TLS, and SSL.
- **CFB (Cipher Feedback)**: Suitable for real-time data streams (e.g., BitLocker).
- **OFB (Output Feedback)**: Used for real-time communication (e.g., SSH).
- **CTR (Counter)**: Fast, suitable for real-time streams (e.g., IPsec, BitLocker).
- **GCM (Galois/Counter)**: Protects confidentiality and integrity; used in wireless communication, VPNs.