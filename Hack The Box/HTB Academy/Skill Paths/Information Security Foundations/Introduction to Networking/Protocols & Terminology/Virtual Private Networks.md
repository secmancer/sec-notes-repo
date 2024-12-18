### Introduction
- **VPN (Virtual Private Network)** provides a secure, encrypted connection between a remote device and a private network, allowing access to the network's resources.
- VPNs are commonly used by administrators to manage internal servers remotely while ensuring secure access, especially when servers are restricted to local network access.
- VPNs use encryption to create a secure tunnel for data transfer, making it difficult for attackers to intercept sensitive information.
- VPNs enable remote access to a private network from anywhere with an internet connection, making it useful for employees working from home or traveling.
- VPNs are cost-effective compared to dedicated connections like leased lines and can connect multiple remote locations into a single private network.
- VPNs typically use **TCP/1723** for PPTP connections and **UDP/500** for IKEv1/IKEv2 connections, and rely on the **ESP** protocol for encryption and authentication.

| **Requirement**  | **Description**                                                                                                                                                         |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `VPN Client`     | This is installed on the remote device and is used to establish and maintain a VPN connection with the VPN server. For example, this could be an OpenVPN client.        |
| `VPN Server`     | This is a computer or network device responsible for accepting VPN connections from VPN clients and routing traffic between the VPN clients and the private network.    |
| `Encryption`     | VPN connections are encrypted using a variety of encryption algorithms and protocols, such as AES and IPsec, to secure the connection and protect the transmitted data. |
| `Authentication` | The VPN server and client must authenticate each other using a shared secret, certificate, or another authentication method to establish a secure connection.           |



### IPsec
- **IPsec (Internet Protocol Security)** is a widely-used network security protocol that provides encryption and authentication for internet communications by encrypting data and verifying packet integrity.
- It uses two protocols for security:
    - **Authentication Header (AH)**: Ensures integrity and authenticity of IP packets without encryption, using a cryptographic checksum.
    - **Encapsulating Security Payload (ESP)**: Encrypts the data payload and optionally adds authentication for IP packets.
- IPsec operates in two modes, providing flexibility for different network configurations.
- For IPsec VPN traffic, firewalls need to allow specific protocols (AH and ESP) to enable secure communication between VPN clients and servers, preventing interception and tampering.

| **Mode** | **Description** |
| --- | --- |
| `Transport Mode` | In this mode, IPsec encrypts and authenticates the data payload of each IP packet but does not encrypt the IP header. This is typically used to secure end-to-end communication between two hosts. |
| `Tunnel Mode` | With this mode, IPsec encrypts and authenticates the entire IP packet, including the IP header. This is typically used to create a VPN tunnel between two networks. |

| **Protocol**                             | **Port**    | **Description**                                                                                                                                                                                                                                                                                          |
| ---------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Internet Protocol` (`IP`)               | `UDP/50-51` | This is the primary protocol that provides the foundation for all internet communication. It is used to route packets of data between the VPN client and the VPN server.                                                                                                                                 |
| `Internet Key Exchange` (`IKE`)          | `UDP/500`   | IKE is a protocol that is used to establish and maintain secure communication between the VPN client and the VPN server. It is based on the Diffie-Hellman key exchange algorithm, and it is used to negotiate and establish shared secret keys that can be used to encrypt and decrypt the VPN traffic. |
| `Encapsulating Security Payload` (`ESP`) | `UDP/4500`  | ESP is also a protocol that provides encryption and authentication for IP datagrams. It is used to encrypt the VPN traffic between the VPN client and the VPN server, using the keys that were negotiated with IKE.                                                                                      |



### PPTP
- **Point-to-Point Tunneling Protocol (PPTP)** is a VPN protocol that creates secure tunnels between clients and servers, encapsulating transmitted data. 
- It was originally an extension of the Point-to-Point Protocol (PPP) and is supported by many operating systems.
- Due to known vulnerabilities, PPTP is no longer considered secure. 
- It supports tunneling protocols like IP, IPX, and NetBEUI but has been largely replaced by more secure protocols such as L2TP/IPsec, IPsec/IKEv2, and OpenVPN.
- PPTP’s authentication method, MSCHAPv2, uses outdated DES encryption, which can be easily cracked, leading to a significant decline in its use since 2012.