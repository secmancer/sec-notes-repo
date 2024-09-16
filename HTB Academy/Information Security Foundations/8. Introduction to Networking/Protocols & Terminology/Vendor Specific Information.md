### Cisco IOS Overview
**Cisco IOS** is the operating system for Cisco network devices like routers and switches. It offers essential features and services to manage and operate network hardware.

**Key Features:**
- **Support for IPv6:** Enables handling of IPv6 traffic and addresses.
- **Quality of Service (QoS):** Manages network traffic to ensure optimal performance for different types of data.
- **Security Features:** Includes encryption and authentication to secure network communications.
- **Virtualization Features:** Supports Virtual Private LAN Service (VPLS) and Virtual Routing and Forwarding (VRF) for network segmentation and isolation.

**Management Methods:**
- **Command Line Interface (CLI):** The primary and most commonly used method for managing Cisco IOS.
- **Graphical User Interface (GUI):** Provides an alternative way to manage IOS, depending on the network device and hardware.

**Supported Protocols and Services:**
Cisco IOS supports a range of network protocols and services necessary for network operation, enhancing its functionality and flexibility in various network environments.

![[Screenshot_20240916_120357.png]]

In Cisco IOS, different types of passwords are used for various purposes, for example:

![[Screenshot_20240916_120430.png]]


### Cisco IOS Configuration and Access

**Encryption Mechanics:**
- **Recommendation:** Review provided external resources to understand the encryption mechanics used in Cisco IOS.

**Remote Access:**
- **Protocols Supported:** Cisco IOS devices can be configured for SSH or Telnet, allowing remote access.
- **Identification:** You can determine that a device is running Cisco IOS based on the response received. For example, it responds with the "User Access Verification" message.

**Example Telnet Access:**
```
secmancer@htb[/htb]$ telnet 10.129.10.2

Trying 10.129.10.2...
Connected to 10.129.10.2.
Escape character is '^]'.

User Access Verification

Password:
```
- **Access Prompt:** The device will prompt for a password after connecting, indicating it is a Cisco IOS device.


### VLANs Overview

**Scenario:** A startup named XQ needs to set up a network with budget constraints, allowing only one switch and router. The network administrator decides to use VLANs to segment the network for security and efficiency.


What is a VLAN?
- Definition: A Virtual Local Area Network (VLAN) is a logical grouping of network endpoints connected to specific ports on a switch. It segments networks by creating logical broadcast domains that can span multiple physical LAN segments.
- Purpose: VLANs allow network segmentation based on team, function, department, or application, independent of physical location. Broadcast packets within a VLAN do not reach endpoints in other VLANs.



**Example VLAN Configuration for XQ:**

| Department | VLAN ID | Subnet         |
| ---------- | ------- | -------------- |
| Servers    | VLAN 10 | 192.168.1.0/24 |
| C-Level    | VLAN 20 | 192.168.2.0/24 |
| Finance    | VLAN 30 | 192.168.3.0/24 |
| HR         | VLAN 40 | 192.168.4.0/24 |
| Marketing  | VLAN 50 | 192.168.5.0/24 |
| Support    | VLAN 60 | 192.168.6.0/24 |



**Benefits of VLANs:**
- **Better Organization:** Grouping endpoints based on common attributes (e.g., department).
- **Increased Security:** Prevents unauthorized access to network packets in other VLANs.
- **Simplified Administration:** Independence from physical locations of endpoints.
- **Increased Performance:** Reduced broadcast traffic, leading to more available bandwidth.



**Cisco VLAN IDs:**
- **ID Range:** 1-4094 (0 and 4095 are reserved and cannot be used).
    - **Normal-Range VLANs:** IDs 1-1005. VLAN 1 is the default and cannot be altered or deleted.
    - **Reserved VLANs:** IDs 1002-1005 for Token Ring and Fiber Distributed Data Interface (FDDI) VLANs.
    - **Extended-Range VLANs:** IDs 1006-4094.
- **Configuration Storage:**
    - **Normal-Range VLANs:** Customizations saved in the VLAN database (vlan.dat file).
    - **Extended-Range VLANs:** Customizations not saved.
- **VLAN Parameters (IDs 2-1001):** Can include name, type, state, and maximum transmission unit (MTU).


### VLAN Memberships
**Static vs. Dynamic VLAN Assignment:**
- **Static VLAN Assignment:**
    - **Method:** Manually assign each port on the switch to a VLAN.
    - **Administration:** Must be done for each switch individually.
    - **Endpoints:** Unaware of VLAN existence.
    - **Security:** More secure since ports are permanently assigned to specific VLANs unless changed manually.
- **Dynamic VLAN Assignment:**
    - **Method:** Automatically assigns VLAN membership based on MAC addresses or protocols.
    - **Centralized Management:** Uses a service/database like VLAN Membership Policy Server (VMPS).
    - **Security Risks:** Potential for attackers to spoof MAC addresses and gain unauthorized VLAN access using tools like macchanger.
    - **Administrative Overhead:** Increases due to the need for centralized management and potential security risks.

### Access and Trunk Ports
- **Access Ports:**
    - **Function:** Belong to and carry traffic for only one VLAN (or two, if one is for voice traffic).
    - **Traffic Handling:** Assumes any traffic arriving on the port belongs to the VLAN assigned to that port.
- **Trunk Ports:**
    - **Function:** Can carry traffic for multiple VLANs simultaneously.
    - **Usage:** Connects two trunk ports on different switches (or a switch and a router) to allow the transport of multiple VLANs across switches.

### VLAN Identification
- **Standard Ethernet Frames:** Do not contain VLAN information.
- **Mechanism:** VLAN-enabled devices use trunking methods to track VLAN information as packets traverse devices.

**Trunking Methods:**
- **Inter-Switch Link (ISL):**
    - **Type:** Cisco-proprietary protocol for trunking.
    - **Encapsulation:** Encapsulates the entire Ethernet frame, including the original header and VLAN tag, adding a 26-byte header and 4-byte trailer.
    - **Usage:** Deprecated and less common in modern switches; replaced by the more widely supported IEEE 802.1Q.
- **IEEE 802.1Q:**
    - **Type:** Widely adopted trunking method.
    - **Encapsulation:** Inserts a 4-byte VLAN tag into the Ethernet frame, without altering the original Ethernet header.


### IEEE 802.1Q Overview
**Purpose:**
- Developed by IEEE in 1998 to ensure interoperability of VLAN technologies across different network equipment vendors.

**VLAN-Compliant 802.1Q Ethernet Frame:**
- **Modification:** IEEE 802.1Q specification modified the 802.3 Ethernet frame format by adding a VLAN tag.
- **Fields Added:**
    - **Tag Protocol Identifier (TPID):** A 16-bit field set to `0x8100` to identify the frame as 802.1Q-tagged.
    - **Tag Control Information (TCI):** A 16-bit field consisting of:
        - **Priority Code Point (PCP):** Used for Quality of Service (QoS).
        - **Drop Eligible Indicator (DEI):** Indicates frames eligible to be dropped under congestion (formerly Canonical Format Indicator (CFI)).
        - **VLAN Identifier (VID):** 12-bit field identifying the VLAN.

**VLAN Identifier (VID):**
- **Capacity:** 12 bits allow for 4096 VLAN IDs (0 and 4095 are reserved, so 4094 usable VLANs).
- **Double Tagging:** The practice of inserting multiple 802.1Q tags in a single packet, introduced by 802.1ad.

**VLAN Tagging and Untagging:**
- **Tagging:** The process of inserting VLAN information into an 802.1Q Ethernet header.
- **Untagging:** The process of removing VLAN information from an 802.1Q-tagged Ethernet frame and forwarding the packet to the intended destination ports.

**Visual Representation:**
- **802.3 Legacy vs. 802.1Q Ethernet Frames:** The 802.1Q frame includes additional fields compared to legacy 802.3 Ethernet frames.

![[8023_Legacy_8021Q_Ethernet_Frames.jpg]]



### VLANs: Key Concepts and Configuration
**1. VLAN Tags and Fields:**
- **Tag Protocol Identifier (TPID):**
    - 16-bit field set to `0x8100` to identify the frame as an 802.1Q-tagged frame.
- **Tag Control Information (TCI):**
    - 16-bit field containing:
        - **Priority Code Point (PCP):** Used for QoS.
        - **Drop Eligible Indicator (DEI):** Indicates frames eligible for dropping under congestion (formerly CFI).
        - **VLAN Identifier (VID):**
            - 12-bit field for VLAN ID.
            - Allows for 4096 VLAN IDs (0 and 4095 are reserved), so 4094 usable VLANs.
- **Double Tagging:** Inserting multiple 802.1Q tags within a single packet (introduced by 802.1ad).

**2. VLAN Tagging and Untagging:**
- **Tagging:** Inserting VLAN information into an 802.1Q Ethernet header.
- **Untagging:** Removing VLAN information from an 802.1Q-tagged Ethernet frame before forwarding it.

**3. VLAN-Capable NICs:**
**Linux:**
- **Ensure Kernel Module is Loaded:**
    - Command: `sudo modprobe 8021q`
    - Verify with: `lsmod | grep 8021`
- **Create VLAN Interface:**
    - Find physical interface: `ip a`
    - Create VLAN interface:
        - Using `vconfig` (deprecated): `sudo vconfig add eth0 20`
        - Using `ip`: `sudo ip link add link eth0 name eth0.20 type vlan id 20`
    - Assign IP and start interface:
        - `sudo ip addr add 192.168.1.1/24 dev eth0.20`
        - `sudo ip link set up eth0.20`
    - Verify interface status: `ip a | grep eth0.20`

**Windows:**
- **Via Device Manager:**
    - Open Device Manager.
    - Access properties of the Ethernet adapter.
    - Set VLAN ID under Advanced settings.
- **Via PowerShell:**
    - List NICs: `Get-NetAdapter | Format-Table -AutoSize`
    - Retrieve VLAN ID: `Get-NetAdapterAdvancedProperty -DisplayName "vlan id"`
    - Set VLAN ID: `Set-NetAdapter -Name "Ethernet 2" -VlanID 10`
    - Note: Operation succeeds only if the NIC supports VLAN tagging.

**4. Analyzing VLAN Tagged Traffic:**
- **Wireshark:**
    - Use filter `vlan` to inspect VLAN tagged packets.
    - Filter for specific VLAN ID: `vlan.id == 10`
- **Tshark:**
    - Enumerate VLAN IDs from a packet dump:
        - `tshark -r "The Ultimate PCAP v20221220.pcapng" -T fields -e vlan.id | sort -n -u`



### Security Implications and VLAN Attacks
#### VLAN Hopping
- **VLAN Hopping Overview**:
    - **Definition**: An attack that allows traffic from one VLAN to be seen by another VLAN without a router.
    - **Exploitation Method**: Utilizes Cisco's Dynamic Trunking Protocol (DTP), which automatically negotiates trunk links between Cisco devices.
    - **Attack Mechanism**:
        - The attacker configures a host to mimic a switch and connects to a switch port with DTP enabled.
        - The host sends 802.1Q signaling and DTP packets to establish a trunk link, exposing traffic from multiple VLANs.
- **Tools for VLAN Hopping**:
    - **Yersinia**: A tool that can be used to perform VLAN hopping attacks.



#### Double-Tagging VLAN Hopping
- **Double-Tagging Overview**:
    - **Definition**: An advanced VLAN hopping attack where two 802.1Q tags are used within a single Ethernet frame.
    - **Attack Steps**:
        1. **Send Double-Tagged Frame**: The attacker sends a frame with an outer VLAN tag (matching the native VLAN of the trunk port) and an inner VLAN tag (target VLAN).
        2. **Frame Processing**: The switch processes the outer tag, removing it and forwarding the frame based on the native VLAN. The inner tag is not removed and is used for further forwarding.
        3. **Forwarding**: The frame is forwarded based on the inner tag to the target VLAN.
- **Tools for Double-Tagging**:
    - **Scapy**: A tool that can also be used to execute double-tagging VLAN hopping attacks.



#### VXLAN (Virtual eXtensible Local Area Network)
- **VXLAN Overview**:
    - **Definition**: A Layer 2 overlay network protocol that operates over a Layer 3 network, designed to extend Layer 2 networks across large data centers.
    - **Primary Benefits**:
        - Scales Layer 2 networks across large and multi-tenant environments.
        - Supports up to 16 million VXLAN segments using a 24-bit VXLAN Network Identifier (VNI).
    - **Addressing Issues**:
        - Overcomes limitations of traditional Layer 2 networks like STP, which can block links and reduce efficiency.



#### Cisco Discovery Protocol (CDP)
- **CDP Overview**:
    - **Definition**: A Layer 2 protocol used by Cisco devices to gather information about other directly connected Cisco devices.
    - **Information Provided**:
        - Device-ID, IP address, port name, device capabilities, and OS/hardware platform information.
    - **Example**:
        - **CDP Packet**: Contains details like device name, IP address, port ID, and software/hardware details.



#### Spanning Tree Protocol (STP)
- **STP Overview**:
    - **Definition**: A network protocol that prevents loops in a network with multiple connections between switches.
    - **Functionality**:
        - Ensures no loops occur, preventing data packets from circulating endlessly and causing network congestion.
    - **Example**:
        - **STP Packet**: Contains information about the root switch, port ID, and configuration parameters like maximum aging time, hello time, and forward delay.