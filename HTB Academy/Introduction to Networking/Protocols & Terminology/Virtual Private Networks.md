### VPN Overview

- **Purpose**: VPNs create a secure and encrypted connection between a remote device and a private network, allowing remote access to internal resources.
- **Usage**: Commonly used for remote administration, secure access for employees working from different locations, and connecting multiple remote sites.
- **Ports**:
    - **TCP/1723**: Used for PPTP VPN connections.
    - **UDP/500**: Used for IKEv1 and IKEv2 VPN connections.

### IPsec (Internet Protocol Security)

- **Function**: Provides encryption and authentication for IP communications.
- **Protocols**:
    - **Authentication Header (AH)**: Provides packet integrity and authentication but no encryption.
    - **Encapsulating Security Payload (ESP)**: Provides encryption and optional authentication for IP packets.
- **Modes**:
    - **Transport Mode**: Encrypts and authenticates the payload but not the header; used for end-to-end communication.
    - **Tunnel Mode**: Encrypts and authenticates the entire packet; used for VPN tunnels between networks.
- **Ports**:
    - **UDP/500**: For IKE.
    - **UDP/4500**: For ESP.

### PPTP (Point-to-Point Tunneling Protocol)

- **Function**: Encapsulates data within a secure tunnel between VPN clients and servers.
- **History**: An extension of PPP, PPTP was once widely used but is now considered insecure due to vulnerabilities in its authentication and encryption methods.
- **Current Status**: Replaced by more secure protocols like L2TP/IPsec, IPsec/IKEv2, and OpenVPN.