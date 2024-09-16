- **HTTPS Overview**
    - **Drawbacks of HTTP**: Data is transferred in clear-text, making it vulnerable to Man-in-the-Middle (MiTM) attacks.
    - **HTTPS**: Solves this by encrypting communications, protecting sensitive data from interception.
    - **Browser Indicators**: HTTPS websites can be identified by the `https://` prefix in URLs and a lock icon in the browser address bar.
    - **Encryption**: HTTPS encrypts traffic, but DNS requests may still be visible if a clear-text DNS server is used. Encrypted DNS servers (e.g., 8.8.8.8) or VPNs are recommended for full encryption.

- **Example of HTTP vs HTTPS**
    - **HTTP Login Request**: Credentials can be easily captured in clear-text.
    - **HTTPS Traffic**: Appears as an encrypted stream, making data capture difficult.


- **HTTPS Flow**
    - **Redirection**: If HTTP is used, the server redirects the client to HTTPS (port 443) using a `301 Moved Permanently` response.
    - **Handshake Process**:
        - Client sends a "client hello" to the server.
        - Server responds with "server hello" and exchanges SSL certificates.
        - After verifying the certificates, the client initiates an encrypted handshake.
        - Once the handshake is complete, encrypted HTTP communication proceeds.


- **Vulnerabilities**
    - **HTTP Downgrade Attacks**: An attacker could downgrade HTTPS to HTTP using a MiTM proxy, but modern browsers and servers have protections against this.


- **Using cURL with HTTPS**
    - **Default Behavior**: cURL automatically handles HTTPS, performing secure handshakes and encryption.
    - **SSL Certificate Errors**: If a website has an invalid SSL certificate, cURL will block the request for security reasons.
        - **Example**: `curl: (60) SSL certificate problem: Invalid certificate chain`


    - **Bypassing SSL Check**: The `-k` flag in cURL can be used to bypass SSL certificate verification, which is useful for local or test web applications without valid certificates.
        - Example: `curl -k https://example.com`