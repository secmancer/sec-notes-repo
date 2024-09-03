### HTTPS Overview

- **HTTPS (HyperText Transfer Protocol Secure)**: An extension of HTTP that encrypts data to prevent interception and tampering.
    
- **Advantages**:
    
    - Encrypts data to protect it from being viewed or altered by third parties.
    - Ensures that communications between a web browser and a web server are secure.
- **Identification**:
    
    - Websites using HTTPS are identified by `https://` in the URL (e.g., `https://www.google.com`).
    - A lock icon in the address bar indicates a secure connection.
- **Potential Issues**:
    
    - Even with HTTPS, if the DNS request is made to a non-encrypted DNS server, the URL being visited may still be visible. Using encrypted DNS servers (e.g., 8.8.8.8 or 1.1.1.1) or a VPN can help ensure privacy.
- **HTTPS Flow**:
    
    1. **Initial Request**: Typing `http://` for a website that enforces HTTPS results in a redirection to HTTPS (port 443).
    2. **Handshake Process**:
        - Browser sends a "client hello" packet.
        - Server replies with "server hello" and exchanges SSL certificates.
        - Both client and server verify the certificates and establish an encrypted connection.
    3. **Secure Communication**: After the handshake, normal HTTP communication occurs, but data is encrypted.
- **Attacks**:
    
    - **HTTP Downgrade Attack**: An attacker may force a connection to use HTTP instead of HTTPS, exposing data. Modern browsers and servers often include protections against such attacks.

### cURL for HTTPS

- **Automatic Handling**:
    
    - cURL manages HTTPS communications, including secure handshakes and encryption.
- **Handling Invalid SSL Certificates**:
    
    - By default, cURL will not proceed with requests to sites with invalid SSL certificates to protect against potential Man-in-the-Middle (MITM) attacks.
        - Example error: "SSL certificate problem: Invalid certificate chain."
- **Skipping Certificate Verification**:
    
    - For testing purposes or when dealing with local applications with invalid SSL certificates, use the `-k` flag to bypass certificate checks.