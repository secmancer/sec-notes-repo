### Introduction
- In the previous section, we discussed how HTTP requests are sent and processed. However, one major drawback of HTTP is that all data is transmitted in clear-text, making it vulnerable to Man-in-the-Middle (MiTM) attacks, where third parties can intercept and view the data being transferred.
- To address this issue, the [HTTPS (HTTP Secure) protocol](https://tools.ietf.org/html/rfc2660) was developed, encrypting all communications to prevent unauthorized access.
- As a result, HTTPS has become the dominant protocol for secure web communications, with HTTP being phased out. In the near future, most web browsers will no longer allow access to HTTP websites.

### HTTPS Overview
- If we examine an HTTP request, we can clearly see the risks associated with not enforcing secure communication between a web browser and a web application.
- For example, login credentials sent over an unencrypted connection would be transmitted in plain text, making it easy for attackers on the same network (such as those using public Wi-Fi) to intercept and misuse these credentials.
- On the other hand, when using HTTPS, data is encrypted, making it extremely difficult for attackers to capture sensitive information like credentials or any other personal data.
- For instance, when visiting a website like Google over HTTPS, all communications are encrypted, ensuring data privacy and security.

> **Note:** Although the data transferred through the HTTPS protocol may be encrypted, the request may still reveal the visited URL if it contacted a clear-text DNS server. For this reason, it is recommended to utilize encrypted DNS servers (e.g. 8.8.8.8 or 1.1.1.1), or utilize a VPN service to ensure all traffic is properly encrypted.



### HTTPS Flow
- If we type `http://` instead of `https://` when visiting a website that enforces HTTPS, the browser first tries to connect over the unencrypted HTTP protocol on port `80`.
- The web server detects this and responds with a `301 Moved Permanently` status code, redirecting the client to port `443`, which is used for secure HTTPS communication.
- After the redirect, the client (web browser) sends a "client hello" packet, which contains information about the client, like the preferred encryption algorithms and supported protocols.
- The server then responds with a "server hello" message and sends its SSL/TLS certificate.
- The client verifies the certificate, and if everything is in order, it sends its own certificate.
- A key exchange is performed, which ensures that both the client and server agree on secure encryption parameters.
- Once the handshake is successfully completed, encrypted communication begins, ensuring confidentiality and integrity for all transferred data.
- This high-level overview covers the key concepts of the HTTPS protocol and the TLS handshake process.

> **Note:** Depending on the circumstances, an attacker may be able to perform an HTTP downgrade attack, which downgrades HTTPS communication to HTTP, making the data transferred in clear-text. This is done by setting up a Man-In-The-Middle (MITM) proxy to transfer all traffic through the attacker's host without the user's knowledge. However, most modern browsers, servers, and web applications protect against this attack.


### cURL for HTTPS
- cURL should automatically handle all HTTPS communication standards and perform a secure handshake.
- Then, encrypt and decrypt data automatically. 
- However, if we ever contact a website with an invalid SSL certificate or an outdated one, then cURL by default would not proceed with the communication to protect against the earlier mentioned MITM attacks.
```shell-session
secmancer@htb[/htb]$ curl https://inlanefreight.com

curl: (60) SSL certificate problem: Invalid certificate chain
More details here: https://curl.haxx.se/docs/sslcerts.html
...SNIP...
```
- Modern web browsers would do the same, warning the user against visiting a website with an invalid SSL certificate.
- We may face such an issue when testing a local web application or with a web application hosted for practice purposes, as such web applications may not yet have implemented a valid SSL certificate. 
- To skip the certificate check with cURL, we can use the `-k` flag.
```shell-session
secmancer@htb[/htb]$ curl -k https://inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```
- As we can see, the request went through this time, and we received the response data.