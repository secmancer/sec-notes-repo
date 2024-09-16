### VPN Overview
- **Definition:** A Virtual Private Network (VPN) establishes a secure and encrypted connection between a private network and a remote device. This enables remote machines to access the private network's resources securely.
    
- **Example Use Case:** An administrator needs to manage internal servers from a remote location. VPN allows the administrator to connect to the VPN server over the internet, authenticate, and create an encrypted tunnel. The administrator is assigned a local IP address to manage the internal servers.
    
- **VPN Ports:**
    - **TCP/1723:** Point-to-Point Tunneling Protocol (PPTP)
    - **UDP/500:** IKEv1 and IKEv2
- **Benefits:**
    - **Encryption:** VPNs encrypt connections, making data transfer secure and reducing the risk of interception.
    - **Remote Access:** Employees can access the network from anywhere with an internet connection, useful for remote work.
    - **Cost-Effectiveness:** VPNs can be cheaper than leased lines or dedicated connections by utilizing public internet infrastructure.
    - **Connecting Remote Locations:** VPNs can link multiple remote locations into a single private network.


### VPN Components and Requirements

|**Requirement**|**Description**|
|---|---|
|**VPN Client**|Installed on the remote device to establish and maintain the VPN connection (e.g., OpenVPN client).|
|**VPN Server**|Accepts VPN connections from clients and routes traffic between them and the private network.|
|**Encryption**|Uses algorithms and protocols like AES and IPsec to secure the connection and protect transmitted data.|
|**Authentication**|VPN server and client authenticate each other using a shared secret, certificate, or other methods.|



### IPsec Overview
- **Definition:** Internet Protocol Security (IPsec) provides encryption and authentication for internet communications.
- **Components:**
    - **Authentication Header (AH):** Provides integrity and authenticity without encryption. Adds an authentication header to IP packets.
    - **Encapsulating Security Payload (ESP):** Provides encryption and optional authentication. Encrypts data payload and may add an authentication header.
- **Modes:**
    - **Transport Mode:** Encrypts and authenticates the data payload of each IP packet but not the IP header. Used for end-to-end communication between hosts.
    - **Tunnel Mode:** Encrypts and authenticates the entire IP packet, including the IP header. Used for creating VPN tunnels between networks.
- **Protocols and Ports:**
    - **Internet Protocol (IP):** UDP/50-51
    - **Internet Key Exchange (IKE):** UDP/500
    - **Encapsulating Security Payload (ESP):** UDP/4500


### PPTP Overview
- **Definition:** Point-to-Point Tunneling Protocol (PPTP) is used to create VPNs by establishing a secure tunnel between the client and server, encapsulating the data.
- **Limitations:**
    - **Security:** PPTP is considered insecure due to vulnerabilities and outdated encryption methods (MSCHAPv2 with DES).
    - **Replacement:** More secure protocols like L2TP/IPsec, IPsec/IKEv2, and OpenVPN have largely replaced PPTP since 2012.