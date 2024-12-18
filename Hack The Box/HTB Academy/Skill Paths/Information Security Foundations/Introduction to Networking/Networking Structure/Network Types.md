### Introduction
- Each network is structured differently and can be set up individually. 
- For this reason, so-called `types` and `topologies` have been developed that can be used to categorize these networks. 
- When reading about all the types of networks, it can be a bit of information overload as some network types include the geographical range. 
- We rarely hear some of the terminologies in practice, so this section will be broken up into `Common Terms` and `Book Terms`. 
- Book terms are good to know, as there has been a single documented case of an email server failing to deliver emails longer than 500 miles but don't be expected to be able to recite them on demand unless you are studying for a networking exam.
![[Screenshot_20241111_155056.png]]



### WAN
- **WAN (Wide Area Network)** is often referred to as the Internet but is essentially a network of interconnected LANs (Local Area Networks).
- **WAN Address** is the public IP address used to access the Internet, while **LAN Address** refers to private IP addresses used within internal networks.
- Many large organizations have an **Internal WAN** (Intranet, Airgap Network), which is separate from the public internet.
- WANs are identified by using routing protocols like **BGP** and by IP schemas outside of **RFC 1918** (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16).



### LAN / WLAN
- **LANs (Local Area Networks)** and **WLANs (Wireless Local Area Networks)** typically use IP addresses from **RFC 1918** (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) for local use.
- In some cases, such as colleges or hotels, you may be assigned a **routable IP address** (internet-accessible) when joining their network, though this is less common.
- The main difference between LANs and WLANs is that WLANs use **wireless communication** instead of cables, with security being the primary distinction.



### VPN
- There are three main types of **Virtual Private Networks (VPNs)**, all aimed at making the user feel as if they are on a different network.
    - **Site-To-Site VPN**: Connects entire networks, typically using **routers** or **firewalls**, allowing multiple locations to communicate over the Internet as if they were local.
    - **Remote Access VPN**: Creates a virtual interface on the client's computer that behaves as if it’s on the client's network. Includes **Split-Tunnel VPN** (only specific networks route through the VPN) and is used by Hack The Box for access to labs.
    - **SSL VPN**: Operates within a web browser, streaming applications or desktops. A common example is the **HackTheBox Pwnbox**.
![[Screenshot_20241111_155144.png]]



### GAN
- A **Global Area Network (GAN)** refers to a worldwide network like the **Internet** but is not the only one.
- **International companies** maintain isolated networks spanning several **WANs**, connecting computers worldwide.
- **GANs** utilize **wide-area networks (WANs)** and are interconnected by **undersea cables** or **satellite transmission**.



### MAN
- A **Metropolitan Area Network (MAN)** connects several **LANs** in a geographical area, often linking company branches via leased lines.
- **High-performance routers** and **fiber-optic connections** are used, offering higher data throughput than the Internet and speeds comparable to communication within a **LAN**.
- **Network operators** provide the infrastructure for **MANs**, which can be integrated into **WANs** and **GANs** for wider, international connectivity.



### PAN / WPAN
- **Personal Area Network (PAN)** allows devices like smartphones, tablets, laptops, or desktops to connect for data exchange, typically using cables.
- **Wireless Personal Area Network (WPAN)** uses Bluetooth or Wireless USB technologies, with Bluetooth-based networks called **Piconet**. These networks are short-range, usually extending only a few meters.
- In the **Internet of Things (IoT)**, **WPANs** are used for low-data-rate communication in smart homes, with protocols like **Insteon**, **Z-Wave**, and **ZigBee** designed for home automation.