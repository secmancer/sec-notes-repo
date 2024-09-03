**Common Terminology**

|**Network Type**|**Definition**|
|---|---|
|**Wide Area Network (WAN)**|Internet|
|**Local Area Network (LAN)**|Internal Networks (e.g., Home or Office)|
|**Wireless Local Area Network (WLAN)**|Internal Networks accessible over Wi-Fi|
|**Virtual Private Network (VPN)**|Connects multiple network sites to one LAN|

**WAN**

- The WAN, commonly referred to as the Internet, connects multiple LANs together, forming a vast network.
- **WAN Address:** The address accessed by the Internet, often seen in routers.
- Large organizations may have an internal WAN (Intranet, Airgap Network) that is isolated from the broader Internet.
- **WAN Specific Routing Protocols:** BGP (Border Gateway Protocol) is a common example, often used outside the RFC 1918 IP ranges (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16).

**LAN / WLAN**

- **LAN:** A network within a limited area like a home or office, typically using IP addresses designated for local use (RFC 1918).
- **WLAN:** A LAN that uses wireless communication, introducing security concerns related to data transmission without cables.

**VPN**

- **Site-To-Site VPN:** Connects entire network ranges over the Internet using routers or firewalls, often joining multiple company locations.
- **Remote Access VPN:** Creates a virtual interface on the client’s machine, simulating a direct connection to a remote network. Examples include OpenVPN for labs like Hack The Box.
    - **Split-Tunnel VPN:** Routes only specific traffic through the VPN, ideal for privacy but less secure for corporate use as malware detection can be bypassed.
- **SSL VPN:** A web browser-based VPN, streaming applications or desktop sessions directly. HackTheBox's Pwnbox is a practical example.

**Book Terms**

|**Network Type**|**Definition**|
|---|---|
|**Global Area Network (GAN)**|Global network (e.g., the Internet)|
|**Metropolitan Area Network (MAN)**|Regional network (e.g., multiple LANs)|
|**Wireless Personal Area Network (WPAN)**|Personal network (e.g., Bluetooth)|

**GAN**

- **Global Area Network (GAN):** Spans worldwide, including the Internet and international corporate networks, utilizing undersea cables or satellite transmissions.

**MAN**

- **Metropolitan Area Network (MAN):** Connects several LANs within a geographic area, often using high-performance connections like fiber optics. Typically involves a regional network, such as a city's infrastructure.

**PAN / WPAN**

- **Personal Area Network (PAN):** A network connecting personal devices, usually via cables.
- **Wireless Personal Area Network (WPAN):** Wireless connectivity over short distances, primarily using Bluetooth. WPANs like Piconet are often employed in smart homes with IoT devices, utilizing protocols such as ZigBee or Z-Wave.