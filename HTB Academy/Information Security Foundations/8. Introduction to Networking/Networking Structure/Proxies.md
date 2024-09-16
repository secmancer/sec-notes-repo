### Proxies: Overview and Types
**Definition**: A proxy is a device or service that sits between a client and a server and acts as a mediator in the connection. It must be able to inspect the contents of the traffic it mediates. Without this ability, the device is a gateway, not a proxy.

**Common Misconceptions**:
- **Security Professionals**: Focus on HTTP Proxies (e.g., BurpSuite) and pivoting with SOCKS/SSH Proxies (e.g., Chisel, ptunnel, sshuttle).
- **Web Developers**: Use proxies like Cloudflare or ModSecurity to block malicious traffic.
- **Average Users**: Often confuse proxies with VPNs for obfuscating location and accessing restricted content (e.g., different Netflix catalogs).
- **Law Enforcement**: May associate proxies with illegal activities.

**Key Points**:
- **Average Misconception**: People might think a proxy is any IP address change, but this is often a misunderstanding. They may actually be using a VPN, which is different from a proxy.
- **Reminder**: Proxies typically operate at Layer 7 (Application Layer) of the OSI Model.

**Types of Proxies**:
1. **Dedicated Proxy / Forward Proxy**:
    - **Definition**: A Forward Proxy acts on behalf of a client making a request. The proxy server carries out the request to the destination server.
    - **Corporate Use**: In a corporate network, sensitive devices may access the internet only through a Forward Proxy, which helps in filtering and securing web traffic.
    - **Security Consideration**: Can prevent direct internet access and provide a defense against malware. Malware must bypass or be aware of the proxy, which can be challenging.
    - **Example**: Burp Suite is a versatile tool that can function as a Forward Proxy to forward HTTP requests and can also be configured as a Reverse Proxy or Transparent Proxy.
2. **Reverse Proxy**:
    - **Definition**: A Reverse Proxy appears as a regular server to the outside world but forwards requests to a backend server. It hides the actual server details from the client.
    - **Use**: Often used for load balancing, improving security, and handling requests for multiple servers.
3. **Transparent Proxy**:
    - **Definition**: A Transparent Proxy intercepts and forwards requests without altering or hiding the client's IP address. It is often used for content filtering and caching.
    - **Use**: Can be used for monitoring and filtering web traffic without requiring configuration changes on client devices.

**Additional Notes**:
- **Proxies vs. VPNs**: Proxies and VPNs both alter the apparent origin of traffic but serve different purposes. VPNs typically encrypt all traffic between the client and the VPN server, while proxies focus on specific protocols or applications.
- **Proxy Awareness**: Malware may need to be aware of the proxy settings, especially if the proxy is used by applications like Firefox, which uses libcurl, or system-wide settings handled by WinSock in other browsers.


### Forward Proxy
![[forward_proxy.png]]


### Reverse Proxy
**Definition**:
- A Reverse Proxy is the opposite of a Forward Proxy. Instead of filtering outgoing requests from clients, it filters incoming requests from the internet to an internal network.

**Common Goals**:
- **Filtering Incoming Traffic**: A Reverse Proxy is designed to listen on a public address and forward incoming traffic to a private or closed network. This helps manage and secure traffic flow into the network.

**Use Cases**:
1. **CloudFlare**:
    - **Purpose**: CloudFlare acts as a Reverse Proxy by filtering incoming web traffic before it reaches an organization's servers.
    - **Benefits**: Provides protection against Distributed Denial of Service (DDoS) attacks and helps in managing the volume and type of traffic that reaches the web servers.
2. **Penetration Testing**:
    - **Usage**: Penetration testers configure reverse proxies on compromised endpoints. The proxy listens on a port and forwards any connecting clients back to the attacker through the compromised system.
    - **Advantages**: Helps bypass firewalls, evade logging, and circumvent Intrusion Detection Systems (IDS). For example, if an attacker gains SSH access, the reverse proxy can forward web requests through the SSH tunnel to avoid detection.
3. **ModSecurity**:
    - **Purpose**: ModSecurity is a Web Application Firewall (WAF) that functions as a Reverse Proxy.
    - **Function**: Inspects incoming web requests for malicious content and blocks harmful requests. It can help protect web applications by filtering out potentially harmful data.
    - **Resources**: For more information, the ModSecurity Core Rule Set is a valuable resource for understanding how this WAF operates.



**Additional Considerations**:
- **HTTPS Traffic**: CloudFlare can also act as a WAF, but doing so requires decrypting HTTPS traffic, which may be a concern for some organizations due to privacy and security considerations.

![[reverse_proxy.png]]



### Transparent vs. Non-Transparent Proxy

**Transparent Proxy**:
- **Definition**: A transparent proxy operates without the client's knowledge. It intercepts communication requests from the client to the internet and acts as a mediator without requiring any special configuration on the client's part.
- **Function**:
    - Intercepts and forwards client requests as if they were made directly to the destination.
    - The client is unaware of the proxy’s existence.
- **Visibility**: The proxy is visible to the destination servers as the source of the request, not the original client.

**Non-Transparent Proxy**:
- **Definition**: A non-transparent proxy requires explicit configuration on the client side. The client must be aware of and configure the proxy settings to route traffic through the proxy server.
- **Function**:
    - Clients must configure their software or devices to direct traffic to the proxy.
    - Communication with the internet is only possible through the proxy if it is properly configured.
- **Visibility**: The proxy server must be explicitly configured, and clients know about its existence.

**Comparison**:
- **Transparent Proxy**:
    - **Client Awareness**: Not required.
    - **Configuration**: None needed on the client side.
    - **Use Cases**: Often used for content filtering, caching, and monitoring without altering client settings.
- **Non-Transparent Proxy**:
    - **Client Awareness**: Required.
    - **Configuration**: Must be set up on the client side.
    - **Use Cases**: Common in scenarios where explicit control and configuration of client traffic are needed, such as in corporate networks or specific application settings.