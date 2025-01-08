### Notes on HyperText Transfer Protocol Secure (HTTPS)

---

### **1. What is HTTPS?**

- **HTTPS (HTTP Secure)**:
    
    - Encrypts all data transferred between a client and a server.
    - Prevents third parties from intercepting and reading sensitive data, such as login credentials.
    - Default port: **443**.
- **Advantages over HTTP**:
    
    - Prevents **Man-in-the-Middle (MITM)** attacks.
    - Secures sensitive information such as passwords, credit card numbers, and session tokens.
    - Ensures data integrity and authentication.

---

### **2. HTTP vs. HTTPS**

|**Feature**|**HTTP**|**HTTPS**|
|---|---|---|
|**Data Transfer**|Clear-text|Encrypted using SSL/TLS.|
|**Port**|80|443|
|**Security**|Vulnerable to MITM attacks.|Data is protected against MITM.|
|**Identification**|No lock icon in URL bar.|Displays a lock icon in URL bar.|

#### **Example Traffic**:

- **HTTP Request**:
    - Login credentials are visible in plain text.
- **HTTPS Request**:
    - Data appears as a single encrypted stream, making interception difficult.

---

### **3. Identifying HTTPS Websites**

- URLs start with `https://`.
- Lock icon appears in the browser’s address bar.

#### **Note**:

- DNS queries may still expose visited URLs if a **clear-text DNS server** is used.
- Use **encrypted DNS servers** (e.g., Google’s `8.8.8.8` or Cloudflare’s `1.1.1.1`) or a **VPN** for additional privacy.

---

### **4. HTTPS Communication Flow**

1. **Initial Request**:
    
    - Client sends an HTTP request (e.g., `http://example.com`).
    - Server responds with a `301 Moved Permanently` status, redirecting to HTTPS (e.g., `https://example.com`).
2. **TLS Handshake**:
    
    - **Client Hello**: The browser shares its capabilities (e.g., supported encryption methods).
    - **Server Hello**: The server responds with its SSL/TLS certificate and encryption options.
    - **Key Exchange**: Both parties exchange keys for encryption.
    - **Handshake**: Verifies encryption setup before starting secure communication.
3. **Encrypted Communication**:
    
    - Once the handshake is complete, all HTTP data is encrypted.

---

### **5. Potential Threats**

- **HTTP Downgrade Attack**:
    - A MITM proxy may force communication to downgrade from HTTPS to HTTP.
    - Modern browsers and servers mitigate this by enforcing **HSTS (HTTP Strict Transport Security)**.

---

### **6. Using cURL with HTTPS**

- **Default Behavior**:
    
    - cURL handles HTTPS automatically, including encryption, decryption, and secure handshakes.
- **Invalid SSL Certificates**:
    
    - By default, cURL stops communication with a server using an invalid SSL certificate to prevent MITM attacks.

#### **Example Error**:

```bash
curl: (60) SSL certificate problem: Invalid certificate chain
```

- **Skipping Certificate Checks**:
    - Use the `-k` flag to bypass SSL verification (use only in trusted environments):
        
        ```bash
        curl -k https://example.com
        ```
        

---

### **7. Key cURL Flags for HTTPS**

|**Flag**|**Description**|
|---|---|
|`-k`|Ignore SSL certificate verification.|
|`-s`|Silent mode (suppress unnecessary output).|
|`-O`|Save the response as a file (use the remote name).|
|`-o <file>`|Save the response with a custom filename.|

---

### **Key Takeaways**

1. HTTPS encrypts data, protecting against eavesdropping and MITM attacks.
2. Always ensure SSL certificates are valid for secure communication.
3. Use `cURL` effectively to interact with HTTPS websites, bypassing certificate checks when necessary (e.g., for local or testing environments).