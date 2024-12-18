### Introduction
- **Wireless networks** allow devices like laptops, smartphones, and tablets to communicate without physical connections, using **radio frequency (RF)** technology to transmit data between devices.
- Devices on the network have wireless adapters that convert data into RF signals, which are transmitted and received by other devices with their own adapters. The data is then converted back into a usable form.
- **WiFi** is commonly used for local area networks (LANs) with a range of a few hundred feet, while **WWANs** (using cellular technology like **3G, 4G LTE, 5G**) cover larger areas like cities or regions.
- To connect to a wireless network, devices must be within range and have the correct settings (e.g., network name and password). Once connected, devices can communicate with each other and access the internet.
- Communication in **WiFi networks** occurs over the **2.4 GHz** or **5 GHz** bands. Devices communicate with a **Wireless Access Point (WAP)**, which grants permission for data transmission. The data is sent as RF signals, received by wireless adapters, and processed by the appropriate applications.
- RF signal strength and range are influenced by factors like transmitter power, obstacles, and RF noise. To ensure reliable communication, WiFi networks use techniques such as **spread spectrum transmission** and **error correction**.



### WiFi Connection
- To connect to a WiFi network, the device must be configured with the correct **network settings**, such as the **SSID** (Service Set Identifier) and **password**.
- The device uses the **IEEE 802.11** wireless networking protocol, which defines how devices communicate with each other and **Wireless Access Points (WAPs)**. The device sends a **connection request frame** (or **association request**) to initiate the connection process.
- Once the device's wireless adapter is configured and the connection is established, it can communicate with the WAP, access other network devices, and use the Internet via the WAP, which acts as a gateway to the wired network.
- The **SSID** can be **hidden** by disabling broadcasting, making it unidentifiable by devices searching for the network. However, the **SSID** can still be found in the **authentication packet**.
- Additional protocols like **TCP/IP**, **DHCP**, and **WPA2** are used in WiFi networks for tasks such as assigning IP addresses, routing traffic, and providing security.
![[Screenshot_20241216_210424.png]]



### WEP Challenge-Response Handshake
- The **challenge-response handshake** is a process used in the **WEP** security protocol to establish a secure connection between a **WAP** and a client device, involving the exchange of packets for authentication.
- To protect against data corruption, **Cyclic Redundancy Check (CRC)** is used in WEP to verify the integrity of transmitted data. 
- The CRC value is calculated for each packet and checked at the destination device to ensure the data was transmitted correctly.
- If the CRC values match, the data is successfully transmitted; if they don't, the data is considered corrupted and needs retransmission.
- However, a **design flaw** in the CRC mechanism allows decryption of a single packet **without knowing the encryption key**, since the CRC is calculated using the **plaintext** data, not the encrypted data. 
- This enables attackers to determine the plaintext data in a packet, even if it is encrypted.
![[Screenshot_20241216_210504.png]]



### Security Features
- WiFi networks have several security features to protect against unauthorized access and ensure the privacy and integrity of data transmitted over the network.
- Some of the leading security features include but are not limited to:
	- Encryption
	- Access Control
	- Firewall
- #### Encryption
	- We can use various encryption algorithms to protect the confidentiality of data transmitted over wireless networks. 
	- The most common encryption algorithms in WiFi networks are [Wired Equivalent Privacy](https://en.wikipedia.org/wiki/Wired_Equivalent_Privacy) (`WEP`), [WiFi Protected Access 2](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access#WPA2) (`WPA2`), and [WiFi Protected Access 3](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access#WPA3) (`WPA3`).
- #### Access Control
	- WiFi networks are configured by default to allow authorized devices to join the network using specific authentication methods. 
	- However, these methods can be changed by requiring a password or a unique identifier (such as a MAC address) to identify authorized devices.
- #### Firewall
	- A firewall is a security system that controls incoming and outgoing network traffic based on predetermined security rules.
	- For example, WiFi routers often have built-in firewalls that can block incoming traffic from the Internet and protect against various types of cyber threats.



### Encryption Protocols
- [Wired Equivalent Privacy](https://en.wikipedia.org/wiki/Wired_Equivalent_Privacy) (`WEP`) and [WiFi Protected Access](https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access) (`WPA`) are encryption protocols that secure data transmitted over a WiFi network. 
- WPA can use different encryption algorithms, including [Advanced Encryption Standard](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) (`AES`).



### WEP
- **WEP** uses either a **40-bit** or **104-bit** key for data encryption, while **WPA with AES** uses a **128-bit** key, offering more robust encryption. However, WEP is considered insecure due to its vulnerabilities and incompatibility with newer devices and operating systems.
- **WEP** employs the **RC4 cipher** encryption algorithm, which is vulnerable to various attacks, allowing attackers to potentially decrypt data.
- **WEP uses a shared key** for both encryption and authentication. There are two versions:
    - **WEP-40/WEP-64**: Uses a **40-bit** secret key.
    - **WEP-104**: Uses a **104-bit** key and an **80-bit secret key**.
- The **Initialization Vector (IV)** in WEP is a small value included in the packet header, used to create unique keys for encryption. However, the **small size of the IV** allows attackers to brute-force it, trying every possible combination to determine the correct IV and decrypt the data, compromising network security.
![[Screenshot_20241216_210658.png]]



### WPA
- `WPA` provides the highest level of security and is not susceptible to the same types of attacks as WEP. In addition, WPA uses more secure authentication methods, such as a [Pre-Shared Key](https://en.wikipedia.org/wiki/Pre-shared_key) (`PSK`) or an 802.1X authentication server, which provide stronger protection against unauthorized access. 
- Although older devices may not support WPA is compatible with most devices and operating systems. 
- All wireless networks, especially in critical infrastructure like offices, should generally implement at least `WPA2` or even `WPA3` encryption.



### Authentication Protocols
- [Lightweight Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Lightweight_Extensible_Authentication_Protocol) (`LEAP`) and [Protected Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Protected_Extensible_Authentication_Protocol) (`PEAP`) are authentication protocols used to secure wireless networks to provide a secure method for authenticating devices on a wireless network and are often used in conjunction with WEP or WPA to provide an additional layer of security.
- LEAP and PEAP are both based on the [Extensible Authentication Protocol](https://en.wikipedia.org/wiki/Extensible_Authentication_Protocol) (`EAP`), a framework for authentication used in various networking contexts. However, one key difference between `LEAP` and `PEAP` is how they secure the authentication process.
- `LEAP` uses a `shared key` for authentication, which means that the `same key` is used for `encryption and authentication`.
- This can make it relatively easy for us to gain access to the network if the key is compromised.
- However, `PEAP` uses a more secure authentication method called tunneled [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (`TLS`). This method establishes a secure connection between the device and the WAP using a `digital certificate`, and an encrypted tunnel protects the authentication process. This provides more robust protection against unauthorized access and is more resistant to attacks.



### TACACS+
- In a wireless network, when a wireless access point (WAP) sends an authentication request to a [Terminal Access Controller Access-Control System Plus](https://www.ciscopress.com/articles/article.asp?p=422947&seqNum=4) (`TACACS+`) server, it is likely that the `entire request packet` will be encrypted to protect the confidentiality and integrity of the request.
- `TACACS+` is a protocol used to authenticate and authorize users accessing network devices, such as routers and switches. When a WAP sends an authentication request to a `TACACS+` server, the request typically includes the user's credentials and other information about the session.
- Encrypting the authentication request helps to ensure that this sensitive information is not visible to unauthorized parties who may be able to intercept the request. At the same time, it is being transmitted over the network. It also helps prevent tampering with the request or replacing it with a malicious request of their own.
- Several encryption methods may be used to encrypt the authentication request, such as `SSL`/`TLS` or `IPSec`. The specific encryption method used may depend on the configuration of the `TACACS+` server and the capabilities of the WAP.



### Disassociation Attack
- A [Disassociation Attack](https://www.makeuseof.com/what-are-disassociation-attacks/) is a type of `all` wireless network attack that aims to disrupt the communication between a WAP and its clients by sending disassociation frames to one or more clients.
- The WAP uses disassociation frames to disconnect a client from the network. When a WAP sends a disassociation frame to a client, the client will disconnect from the network and have to reconnect to continue using the network.
- We can launch the attack from `within` or `outside` the network depending on our location and network security measures. The purpose of this attack is to disrupt the communication between the WAP and its clients, causing the clients to disconnect and possibly causing inconvenience or disruption to the users. We can also use it as a precursor to other attacks, such as a MITM attack, by forcing the clients to reconnect to the network and potentially exposing them to further attacks.



### Wireless Hardening
- There are many different ways to protect wireless networks. However, some examples should be considered to increase wireless networks' security dramatically. These are the following, but not limited to:
	- Disabling broadcasting
	- WiFi Protected Access
	- MAC filtering
	- Deploying EAP-TLS
- #### Disabling Broadcasting
	- Disabling the broadcasting of the SSID is a security measure that can help harden a WAP by making it more difficult to discover and connect to the network. When the SSID is broadcasted, it is included in beacon frames regularly transmitted by the WAP to advertise the availability of the network. By disabling the broadcasting of the SSID, the WAP will not transmit beacon frames, and the network will not be visible to devices that are not already connected to the network.
- #### WPA
	- Again, WPA provides strong encryption and authentication for wireless communications, helping protect against unauthorized network access and sensitive data interception. WPA includes two main versions:
		1. WPA-Personal
		2. WPA-Enterprise
	- WPA-Personal, designed for home and small business networks, and WPA-Enterprise, designed for larger organizations and uses a centralized authentication server (e.g., RADIUS or TACACS+) to verify the identity of clients.
- #### MAC Filtering
	- MAC filtering is a security measure that allows a WAP to accept or reject connections from specific devices based on their MAC addresses. By configuring the WAP to accept connections only from devices with approved MAC addresses, it is possible to prevent unauthorized devices from connecting to the network.
- #### Deploying EAP-TLS
	- EAP-TLS is a security protocol used to authenticate and encrypt wireless communications. It uses digital certificates and PKI to verify the identity of clients and establish secure connections. Deploying EAP-TLS can help to harden a WAP by providing strong authentication and encryption for wireless communications, which can protect against unauthorized access to the network and the interception of sensitive data.