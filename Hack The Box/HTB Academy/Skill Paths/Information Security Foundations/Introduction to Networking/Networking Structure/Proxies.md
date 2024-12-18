### Proxies
- **Different views on proxies**:
    - **Security Professionals** focus on HTTP proxies (e.g., BurpSuite) and **SOCKS/SSH Proxies** for pivoting (e.g., Chisel, ptunnel).
    - **Web Developers** use proxies like Cloudflare or ModSecurity to block malicious traffic.
    - **Average People** may think proxies are used to change locations for services like Netflix.
    - **Law Enforcement** associates proxies with illegal activity.
- A **proxy** acts as a mediator between a device and the network, inspecting traffic, while a **gateway** just passes traffic without inspecting it.
- **Misconception**: People often confuse **VPNs** with proxies because both change an IP address, but a VPN isn't technically a proxy.
- **Proxies generally operate at Layer 7** of the OSI model and key types include:
    - **Dedicated/Forward Proxy**
    - **Reverse Proxy**
    - **Transparent Proxy**



### Dedicated Proxy / Forward Proxy
![image](https://academy.hackthebox.com/storage/modules/34/redesigned/forward_proxy.png)
- **Forward Proxy** is what most people imagine a proxy to be, where a client makes a request, and the proxy carries it out on behalf of the client.
- In a **corporate network**, sensitive computers might be restricted from direct Internet access and must go through a proxy or web filter to access websites. This provides a strong defense against malware by requiring it to either bypass the web filter or be proxy-aware, which is unlikely for most malware.
- **Web browsers** like Internet Explorer, Edge, and Chrome follow "System Proxy" settings by default, making them **proxy-aware**. Malware using WinSock (Windows API) will likely be proxy-aware as well. However, **Firefox** does not use WinSock, making it less likely for malware to exploit the proxy settings without explicitly targeting Firefox.
- **Malware can use DNS** as a command-and-control (C2) mechanism, but monitoring DNS traffic (e.g., with Sysmon) can catch this early.
- **Burp Suite** is an example of a **Forward Proxy** used to forward HTTP requests but can also be configured as a **reverse proxy** or **transparent proxy**, showcasing its flexibility as an HTTP proxy tool.



### Reverse Proxy
![image](https://academy.hackthebox.com/storage/modules/34/redesigned/reverse_proxy.png)
- A **Reverse Proxy** filters incoming requests, unlike a **Forward Proxy**, which filters outgoing ones. Its primary goal is to forward traffic to a closed-off network.
- **Cloudflare** is a popular Reverse Proxy service used by organizations to filter and mitigate DDoS attacks and control traffic sent to their web servers.
- **Penetration Testers** use Reverse Proxies on infected endpoints to forward traffic back to the attacker, allowing them to bypass firewalls and evade logging systems like **Intrusion Detection Systems** (IDS).
- **ModSecurity**, a Web Application Firewall (WAF), is another type of Reverse Proxy that inspects and blocks malicious web requests. Cloudflare can also act as a WAF but requires decrypting HTTPS traffic, which some organizations may avoid for security reasons.



### (Non-) Transparent Proxy
- Proxy services can operate **transparently** or **non-transparently**.
- In a **transparent proxy**, the client is unaware of its existence. The proxy intercepts requests and acts as a substitute, while appearing as the communication partner to the outside.
- In a **non-transparent proxy**, the client must be aware of the proxy and configure software to route traffic through it. Without this configuration, communication is typically blocked, as the proxy is the only path to external networks.