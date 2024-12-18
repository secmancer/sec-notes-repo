### Introduction
- **Cisco IOS**: The operating system for Cisco network devices (e.g., routers, switches) that provides essential features for managing and operating networks.
    - **Key Features**:
        - Support for IPv6
        - Quality of Service (QoS)
        - Security features (encryption, authentication)
        - Virtualization features (VPLS, VRF)
- **Management Methods**: Cisco IOS can be managed through the command line interface (CLI) or a graphical user interface (GUI).
- **Password Types**: Cisco IOS uses different passwords for various purposes, important for device security.
- **Encryption Mechanics**: Understanding Cisco IOS encryption is crucial, with recommended external resources for further study.
- **Remote Access**: Cisco IOS devices can be configured for SSH or Telnet, and they respond with a `User Access Verification` message for identification.

| **Protocol Type** | **Description** |
| --- | --- |
| `Routing protocols` | Such as [OSPF](https://en.wikipedia.org/wiki/Open_Shortest_Path_First) and [BGP](https://en.wikipedia.org/wiki/Border_Gateway_Protocol) are used to route data packets on a network. |
| `Switching protocols` | Such as [VLAN Trunking Protocol](https://en.wikipedia.org/wiki/VLAN_Trunking_Protocol) (`VTP`) and [Spanning Tree Protocol](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol) (`STP`) is used to configure and manage switches on a network. |
| `Network services` | Such as [Dynamic Host Configuration Protocol](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) (`DHCP`) are used to automatically provide clients on the network with IP addresses and other network configurations. |
| `Security features` | Such as [Access Control Lists](https://en.wikipedia.org/wiki/Access-control_list) (`ACLs`), which are used to control access to network resources and prevent security threats. |

| **Password Type** | **Description** |
| --- | --- |
| `User` | The [user](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/security/s1/sec-s1-cr-book/sec-cr-t2.html#wp2992613898) password is used for logging in to Cisco IOS. It is used to restrict access to the network device and its features. |
| `Enable Password` | The [enable password](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/security/d1/sec-d1-cr-book/sec-cr-e1.html#wp3884449514) is used to enter "enable" mode. The "enable" mode is the mode where you have access to advanced functions and settings. |
| `Secret` | The [secret](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/security/s1/sec-s1-cr-book/sec-cr-s1.html#wp2622423174) is a password to secure access to certain functions and services. It is often used to restrict access to remote management tools and services. |
| `Enable Secret` | The [enable secret](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/security/d1/sec-d1-cr-book/sec-cr-e1.html#wp3438133060) is an extra-secure password used to secure access to "enable" mode, and they are stored encrypted to provide additional protection. |

```shell-session
secmancer@htb[/htb]$ telnet 10.129.10.2

Trying 10.129.10.2...
Connected to 10.129.10.2.
Escape character is '^]'.


User Access Verification

Password:
```



### VLANs
- **Scenario**: A startup, XQ, hires a network administrator to design a network with one switch and router due to budget constraints. The network will support web and database servers, with staff from various departments.
- **Security Concerns**: The administrator considers potential insider attacks, particularly those exploiting broadcast traffic like `broadcast storms`.
- **Solution**: To address this, the network administrator implements `Virtual Local Area Networks` (VLANs) to logically segment the network, effectively turning the single switch into multiple mini-switches.
- **VLAN Definition**: A VLAN is a logical grouping of network endpoints on specific switch ports, creating separate broadcast domains. It allows network segmentation without being tied to physical locations.
- **Benefits**: VLANs allow network segmentation by factors such as department or function, ensuring that broadcast traffic in one VLAN does not reach other VLANs. Each VLAN also requires its own subnet, aiding in network management and security.
- **Benefits of VLANs**:
    - **Better Organization**: VLANs allow network administrators to group endpoints by common attributes, such as departments or functions, for a more structured network.
    - **Increased Security**: VLAN segmentation helps isolate traffic, preventing unauthorized users from sniffing network packets from other VLANs.
    - **Simplified Administration**: Network management is easier as administrators don’t need to worry about the physical locations of devices.
    - **Increased Performance**: Reducing broadcast traffic in each VLAN frees up bandwidth, allowing more efficient use of the network.
- **VLAN IDs/Numbers**: Cisco switches support VLAN IDs from 1 to 4094:
    - **VLAN 1**: Default VLAN, cannot be altered or deleted.
    - **Normal-Range VLANs**: IDs 1-1005, where IDs 1002-1005 are reserved for Token Ring and FDDI VLANs.
    - **Extended-Range VLANs**: IDs 1006-4094, which are not stored in the `vlan.dat` file.
- **VLAN Database**: VLANs 2-1001 are saved in the `vlan.dat` file and can have parameters such as:
    - **Name**: Identifies the VLAN.
    - **Type**: Defines the VLAN's behavior.
    - **State**: Shows whether the VLAN is active or inactive.
    - **Maximum Transmission Unit (MTU)**: Defines the maximum packet size.

| **Department** | **VLAN ID** | **Subnet** |
| :-: | :-: | :-: |
| `Servers` | `VLAN 10` | `192.168.1.0/24` |
| `C-Level` | `VLAN 20` | `192.168.2.0/24` |
| `Finance` | `VLAN 30` | `192.168.3.0/24` |
| `HR` | `VLAN 40` | `192.168.4.0/24` |
| `Marketing` | `VLAN 50` | `192.168.5.0/24` |
| `Support` | `VLAN 60` | `192.168.6.0/24` |



### VLAN Memberships
- **VLAN Assignment Methods**:
    - **Static VLAN Assignment**: The most common and simplest method where each port is manually assigned to a VLAN through the switch's network operating system. This is done for each switch separately, and the endpoints connected to these ports are unaware of the VLANs.
    - **Dynamic VLAN Assignment**: This method automatically determines an endpoint's VLAN membership based on its MAC address or other protocols. The administrator registers the MAC addresses in a centralized VLAN management service like the VLAN Membership Policy Server (VMPS). The switch then queries the VMPS to assign the appropriate VLAN based on the MAC address. While dynamic VLANs offer flexibility, they increase administrative complexity.
- **Security Considerations**:
    - **Static VLANs**: More secure because each port is permanently assigned to a specific VLAN, and this association does not change unless manually altered.
    - **Dynamic VLANs**: Less secure due to the potential for MAC address spoofing. An attacker could use tools like [macchanger](https://github.com/alobbs/macchanger) to spoof the MAC address of legitimate devices and gain access to their VLANs, allowing them to sniff traffic.



### Access and Trunk Ports
- **Access Ports**:
    - An **access port** is assigned to a single VLAN (or sometimes two, with one for voice traffic) and can carry traffic for that specific VLAN only.
    - Any traffic arriving on an access port is automatically associated with the VLAN to which the port is assigned.
    - These ports are typically used to connect devices like computers or printers, which do not need to be aware of the VLAN structure.
- **Trunk Ports**:
    - A **trunk port** can carry traffic from multiple VLANs at the same time.
    - Trunk ports are used to connect switches or switches to routers, allowing the traffic from several VLANs to be transmitted between devices.
    - Trunk links utilize **VLAN tagging** (e.g., IEEE 802.1Q) to distinguish the VLANs and maintain traffic segregation across the trunk.



### VLAN Identification
- Standard `802.3` `Ethernet` frames do not contain `VLAN` information; therefore, switches and other `VLAN`\-enabled devices need a mechanism to keep track of all the `VLAN` information associated with a packet while traversing `VLAN`\-enabled devices. 
- Two main `trunking methods` are utilized to achieve this, `ISL` and `IEEE 802.1Q`.



### Inter-Switch Link (ISL)
- `Inter-Switch Link` (`ISL`) is a Cisco-proprietary protocol used for trunking between `VLAN`\-enabled devices. 
- Although `ISL` is one of the first `trunking methods` (predating `802.1Q`), it is deprecated and not as widely used in modern Cisco switches (and routers).
- Instead, most only support the widely adopted `802.1Q`. `ISL` encapsulated the entire `Ethernet` frame, including the original `Ethernet` header and the `VLAN` tag, adding its 26-byte header and 4-byte trailer.



### IEEE 802.1Q
- **IEEE 802.1Q Specification**:
    - Developed in 1998 by the **Institute of Electrical and Electronics Engineers (IEEE)**, the **802.1Q** specification ensures interoperability of VLAN technologies across different network equipment vendors.
    - The specification modified the standard **Ethernet frame format** by adding two key fields: `TPID` (Tag Protocol Identifier) and `TCI` (Tag Control Information), which together form the **802.1Q-tagged Ethernet frame**.
- **VLAN Tagging**:
    - **Tag Protocol Identifier (TPID)**: A 16-bit field always set to `0x8100`, marking the Ethernet frame as an **802.1Q-tagged** frame.
    - **Tag Control Information (TCI)**: A 16-bit field containing three subfields:
        - **Priority Code Point (PCP)**: Used for Quality of Service (QoS) to define the priority of the frame.
        - **Drop Eligible Indicator (DEI)**: Indicates if the frame is eligible to be dropped in case of network congestion (formerly Canonical Format Indicator).
        - **VLAN Identifier (VID)**: A 12-bit field (low-order bits of TCI) that identifies the specific **VLAN**. It allows for **4096 VLANs** (from 1 to 4094) due to the 12-bit size of the field (reserving 0 and 4095).
- **Double Tagging**:
    - The practice of adding multiple **802.1Q** tags to a single Ethernet frame is called **Double Tagging**, introduced by the **802.1ad** standard. This allows for nested VLAN tags, useful in cases like service provider networks.
- **VLAN Tagging and Untagging**:
    - **VLAN Tagging**: The process of adding VLAN information (i.e., the VID) to an Ethernet frame header using **802.1Q**.
    - **VLAN Untagging**: The process of removing the VLAN tag from an Ethernet frame before forwarding it to a device or port. This occurs when the packet reaches its destination switch port, which is part of a specific VLAN.

![8023_Legacy_8021Q_Ethernet_Frames.png](https://academy.hackthebox.com/storage/modules/34/8023_Legacy_8021Q_Ethernet_Frames.png)


### VLAN-Capable NICs
- Some `network interface cards` (`NICs`) attached to computers/servers support `VLAN tagging`. 
- Let us see how we can assign a `VLAN` ID to a `NIC` using Linux and Windows.




### Assigning NICs a VLAN in Linux
- In Linux, creating a `VLAN` is done by creating an interface on top of another, called a `parent` interface. 
- This `VLAN` interface will tag packets with the assigned `VLAN` ID while returning packets will be untagged.
- To assign a network adapter a `VLAN` in Linux, many tools can be used, such as [ip](https://man7.org/linux/man-pages/man8/ip.8.html), [nmcli](https://linux.die.net/man/1/nmcli), and [vconfig](https://linux.die.net/man/8/vconfig) (deprecated).
- However, first, we need to ensure that the Kernel has the [802.1Q](https://elixir.bootlin.com/linux/v6.4.7/source/net/8021q/vlan.c) module loaded.
```shell-session
secmancer@htb[/htb]$ sudo modprobe 8021q
```
- Subsequently, we can use `lsmod` to make sure `8021q` was loaded successfully.
```shell-session
secmancer@htb[/htb]$ lsmod | grep 8021

8021q                  40960  0
garp                   16384  1 8021q
mrp                    20480  1 8021q
```

- Now, we need to find the name of the physical `Ethernet` interface that we will create the `VLAN` interface on top of, which is `eth0`.
```shell-session
secmancer@htb[/htb]$ ip a

<SNIP>
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether a6:ba:3b:08:3a:36 brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname ens3
    inet 94.2X.5X.72/22 brd 94.237.51.255 scope global dynamic eth0
       valid_lft 83489sec preferred_lft 83489sec
    inet6 fe80::a4ba:3bff:fe08:3a36/64 scope link 
       valid_lft forever preferred_lft forever
```

- Then, we will use `vconfig` to create a new interface that is a member of the desired `VLAN`, `20`, for example, on top of `eth0`.
```shell-session
secmancer@htb[/htb]$ sudo vconfig add eth0 20

Warning: vconfig is deprecated and might be removed in the future, please migrate to ip(route2) as soon as possible!
```
- To use `ip` instead, we can do this instead.
```shell-session
sudo ip link add link eth0 name eth0.20 type vlan id 20
```
- Either of these commands will make a new interface called `eth0.20@eth0`.
```shell-session
secmancer@htb[/htb]$ ip a

<SNIP>
4: eth0.20@eth0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether a6:ba:3b:08:3a:36 brd ff:ff:ff:ff:ff:ff
```
- Then, based on the `subnet` assigned to the addresses with `VLAN 20` within the local network, we need to assign the interface an IP address and then start it.
```shell-session
secmancer@htb[/htb]$ sudo ip addr add 192.168.1.1/24 dev eth0.20
secmancer@htb[/htb]$ sudo ip link set up eth0.20
```
- At last, we can check whether the interface has changed states to up.
```shell-session
secmancer@htb[/htb]$ ip a | grep eth0.20

4: eth0.20@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    inet 192.168.1.1/24 scope global eth0.20
```



### Assigning NICs a VLAN in Windows
- On Windows, to assign a `VLAN` for a physical network adapter that supports `VLAN tagging`, first we need to open `Device Manager`.
![Windows_Device_Manager.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager.png)
- Then we need to click on `Properties` for the `Ethernet interface` we want to assign to a `VLAN`.
![Windows_Device_Manager_Adapter_Properties.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager_Adapter_Properties.png)
- Within `Advanced`, there will be a `VLAN ID` property to which we can assign a value. 
- After clicking `OK`, if the adapter supports assigning a `VLAN`, it will be set; otherwise, the window will close, and no `VLAN` tag will be added to any packets originating from this host.
![Windows_Device_Manager_Adapter_Properties_VLAN_ID.png](https://academy.hackthebox.com/storage/modules/34/Windows_Device_Manager_Adapter_Properties_VLAN_ID.png)
- Instead of relying on the GUI, we can use `PowerShell`. 
- First, let us get the names of all the available physical network adapters using the [Get-NetAdapter](https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapter?view=windowsserver2022-ps) Cmdlet.
```powershell-session
PS C:\> Get-NetAdapter | Format-Table -AutoSize

Name                                           InterfaceDescription                                                          ifIndex Status             MacAddress              LinkSpeed
----                                           --------------------                                                          ------- ------             ----------              ---------
VirtualBox Host-Only Network  VirtualBox Host-Only Ethernet Adapter                                        20 Up                    0A-00-27-10-42-15       1 Gbps
Ethernet 2                                 ASIX AX88772B USB2.0 to Fast Ethernet Adapter                            55 Up                    90-EB-78-14-21-7F    100 Mbps
Bluetooth Network Connection  Bluetooth Device (Personal Area Network)                                   18 Disconnected   38-41-25-E8-DE-2D        3 Mbps
Wi-Fi                                         Intel(R) Wireless-AC 9560 160MHz                                                12 Disconnected   8E-36-6A-7A-BA-6A 866.7 Mbps
```
- Previously, we used `Device Manager` to assign `Ethernet 2` to `VLAN 10`; to retrieve the `VLAN` ID of the interface, we can use the [Get-NetAdapaterAdvancedProperty](https://learn.microsoft.com/en-us/powershell/module/netadapter/get-netadapteradvancedproperty?view=windowsserver2022-ps) Cmdlet with the `-DisplayName` flag along with `vlan id`.
```powershell-session
PS C:\> Get-NetAdapterAdvancedProperty -DisplayName "vlan id"

Name                      DisplayName                    DisplayValue                   RegistryKeyword RegistryValue
----                      -----------                    ------------                   --------------- -------------
Ethernet 2                VLAN ID                        10                                     VLAN_ID               {10}
```
- We can also set the `VLAN` ID of a physical network address using the [Set-NetAdapter](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps) Cmdlet along with the [VlanID](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps#-vlanid) flag; this powerful Cmdlet can also be used to customize other properties of interfaces such as [MAC addresses](https://learn.microsoft.com/en-us/powershell/module/netadapter/set-netadapter?view=windowsserver2022-ps#-macaddress).
```powershell-session
PS C:\> Set-NetAdapter -Name "Ethernet 2" -VlanID 10
```

- However, remember that this operation only succeeds if the network interface supports this functionality; otherwise, `PowerShell` will throw an error indicating that the interface does not support it.



### Analyzing VLAN Tagged Traffic
- We can identify and analyze `VLAN` tagged traffic on a network with `Wireshark` using the [vlan](https://www.wireshark.org/docs/dfref/v/vlan.html) filter. For example, when analyzing a network packet dump, we can inspect packets with `802.1Q` tagging using the filter `vlan`.
![Wireshark_VLAN_Filter.png](https://academy.hackthebox.com/storage/modules/34/Wireshark_VLAN_Filter.png)
- Moreover, we can search for packets with a specific `VLAN` ID; for example, to search for packets having `VLAN 10`, we can use the filter `vlan.id == 10`.
![Wireshark_VLAN_ID_Filter.png](https://academy.hackthebox.com/storage/modules/34/Wireshark_VLAN_ID_Filter.png)
- Additionally, to enumerate the used `VLAN` IDs from a packet dump, we can utilize tshark.
```shell-session
secmancer@htb[/htb]$ tshark -r "The Ultimate PCAP v20221220.pcapng" -T fields -e vlan.id | sort -n -u

1
2
3
7
10
20
30
40
50
60
70
80
90
121
125
224
```



### Security Implications and VLAN Attacks
- Regardless of improving a network's security posture, adversaries can still circumvent the defensive mechanisms put forth by `VLANs`. 
- Although in modern switched networks, the utilization of `VLANs` brings numerous advantages (such as simplified network maintenance and improved performance), it also introduces potential security risks, leading to various `VLAN` attacks. 
- It is essential to grasp the underlying methodologies of these attacks and implement practical mitigation approaches to safeguard networks.



### VLAN Hopping
- `VLAN hopping` attacks enable traffic from one `VLAN` to be seen by another `VLAN` without the aid of a router. 
- It exploits Cisco's `Dynamic Trunking Protocol` (`DTP`), a protocol used to automatically negotiate the formation of a `trunk link` between two Cisco devices. 
- An adversary needs to configure a host to mimic/act like a switch to take advantage of the automatic trunking port feature enabled by default on most switch ports. 
- To exploit `VLAN hopping`, an adversary must be able to physically connect with a switch port that has `DTP` enabled. 
- The adversary can abuse this connection by configuring a host connected to the switch on that specific port to spoof `802.1Q` signaling and the `DTP` packets. 
- If successful, the switch will eventually establish a `trunk link` with the adversary's host, exposing the network packets, not only for a specific `VLAN`.
- We can use tools such as [Yersinia](https://linux.die.net/man/8/yersinia) to perform `VLAN hopping` attacks.

![Yersinia_DTP_Attack.png](https://academy.hackthebox.com/storage/modules/34/Yersinia_DTP_Attack.png)



### Double-tagging VLAN Hopping
- The `double-tagging VLAN hopping attack` is an increasingly more sophisticated attack against `VLANs`. 
- Although `VLAN double-tagging` is a legitimate practice that entities such as `Internet Service Providers` (`ISPs`) utilize (they can use their `VLANs` internally while carrying traffic from clients that are already `VLAN tagged`), adversaries can also attempt to abuse it. 
- In a `double-tagging VLAN hopping attack`, an adversary embeds a hidden `802.1Q` tag inside an `Ethernet` frame that already has an `802.1Q` tag, allowing the frame to go to a different `VLAN`, which the original `802.1Q` tag did not specify.
- An adversary can carry out this attack following three steps. Bare in mind that this attack only works if the adversary is connected to a port residing in the same `VLAN` as the `native VLAN` of the trunk port:
	1. The adversary sends a `double-tagged 802.1Q` `Ethernet` frame to the switch with the outer header having the `VLAN` ID of the adversary, which is the same as the native `VLAN` of the trunk port. 
	2. Assume that the native `VLAN` is `VLAN 10` and that `VLAN 30` is the `VLAN` the adversary wants to reach, where the victim resides.
	3. The outer 4-byte `802.1Q` tag arrives on the switch, and it is seen to be destined for `VLAN 10`, the native `VLAN`. 
	4. After removing the `VLAN 10` tag, the frame is forwarded on all `VLAN 10` ports. On the trunk port, the `VLAN 10` tag is stripped (removed), and the packet is not re-tagged because it is part of the native `VLAN`. 
	5. However, the `VLAN 30` tag is still intact (not stripped), and the first switch has not inspected it.
	6. Subsequently, the switch will look only at the inner `802.1Q` tag that the adversary sent, and it decides that the frame must be forwarded for `VLAN 30`, which is the adversary's chosen `VLAN`. 
	7. Now, the second switch will either send the frame to the victim port directly or flood it, depending on whether there is an existing MAC address table entry for the victim host.
- [Scapy](https://scapy.readthedocs.io/en/latest/usage.html#vlan-hopping) allows carrying out the `double-tagging VLAN hopping attack`, in addition to `Yersinia`.
![Yersinia_Double_Tagging_VLAN_Hopping_Attack.png](https://academy.hackthebox.com/storage/modules/34/Yersinia_Double_Tagging_VLAN_Hopping_Attack.png)



### VXLAN
- **Limitations of Traditional Layer 2 Networks**:
    - Traditional Layer 2 networks, while suitable for small to medium-sized environments, struggle with scalability in large data centers and cloud service providers. **VLANs**, with their 12-bit **VLAN Identifier (VID)**, support only up to **4094 VLANs**, which is insufficient for the extensive segmentation required by large data centers.
    - Additionally, networks relying on the **IEEE 802.1D Spanning Tree Protocol (STP)** face challenges with **link blocking** to prevent network loops, which reduces the number of active paths and hinders network resiliency. While STP ensures a loop-free topology, it deactivates redundant links, affecting the efficiency and flexibility of **Layer 2** networks, particularly in virtualized environments.
    - The need for efficient **Layer 2** scaling and **multipathing** in virtualized environments further highlights the limitations of traditional Layer 2 protocols, such as STP.
- **VXLAN (Virtual eXtensible Local Area Network)**:
    - **VXLAN** (as introduced by **RFC 7348**) provides a solution to the scaling issues and limitations of traditional **Layer 2** networks. It is a **Layer 2 overlay protocol** that operates over an existing **Layer 3 network**, enabling the extension of **Layer 2** networks across large data centers and even between geographically distributed locations.
    - **Key Features of VXLAN**:
        - **VXLAN Network Identifier (VNI)**: A **24-bit identifier** that uniquely identifies a **VXLAN segment**. This allows for the creation of up to **16 million VXLAN segments** within a single administrative domain, far surpassing the scalability limitations of traditional VLANs.
        - **VXLAN Segments**: Each **VXLAN segment** is treated as a distinct Layer 2 network, ensuring that only virtual machines (VMs) within the same VXLAN segment can communicate with each other, maintaining network isolation and security.
        - **Overlays on Layer 3**: VXLAN operates over existing **Layer 3 infrastructure**, facilitating the **seamless extension of Layer 2 networks** across data centers. This enables the creation of flexible, scalable **virtualized networks** capable of handling the demands of modern cloud environments.
        - **Multi-Tenant Support**: VXLAN supports multi-tenancy by providing isolation between tenants’ traffic, a critical feature in data centers hosting virtual machines or containers from different organizations.
- **Benefits of VXLAN**:
    - **Scalability**: The ability to create up to **16 million VXLAN segments** supports the large-scale segmentation required in data centers, overcoming the 4094 VLAN limit.
    - **Efficient Resource Allocation**: VXLAN enables the seamless allocation and movement of computing, networking, and storage resources across geographically dispersed data centers, enhancing efficiency in virtualized environments.
    - **Network Flexibility**: By creating **Layer 2 overlays** on a **Layer 3 network**, VXLAN removes the constraints of traditional **Layer 2** protocols, such as STP, and enables **multipathing** for better resilience and performance.



### Cisco Discovery Protocol
- Cisco Discovery Protocol (CDP) is a layer-2 network protocol from Cisco that is used by Cisco devices such as routers, switches, and bridges to gather information about other directly connected Cisco devices. 
- This information can be used to discover and track the network's topology and help manage and troubleshoot the network.
- This protocol is usually enabled in Cisco devices, but it can be disabled if it is not needed or if it should be disabled for security reasons.



### CDP Network Traffic
```shell-session
22:14:11.563654 CDPv2, ttl: 180s, checksum: 0xebc1 (incorrect -> 0x8b71), length: 180
        Device-ID (0x01), length: 14 bytes: 'router.inlanefreight.loc'
        Addresses (0x02), length: 8 bytes:
                IPv4 (0x01), length: 4: 10.129.100.1
        Port-ID (0x03), length: 9 bytes: 'Ethernet0/0'
        Capability (0x04), length: 4: (0x00000010): Router
        Version String (0x05), length: 27 bytes: 'Cisco IOS Software, C880 Software'
        Platform (0x06), length: 26 bytes: 'Cisco 881 (MPC8300) processor'
```
- The shown message contains information about the device itself, such as the device name, IP address, port name, and functionality of the router, as well as information about the operating system and hardware platform of the device. 
- Besides, we can see in the first line from the `CDPv2` that we are dealing with the `Cisco Discovery Protocol`.
- For comparison, we can look at another protocol called Spanning Tree Protocol (`STP`). 
- The `STP` is a network protocol that ensures no loops in a network with multiple connections between switches. 
- There are no loops, and it prevents data packets from circulating in a loop and congesting the network.



### STP Network Traffic
```shell-session
22:14:11.563654 STP 802.1w, Rapid STP, Flags [Learn, Forward], bridge-id 8001.00:11:22:33:44:55.8000, length 43
        root-id 8001.AA:AA:AA:AA:AA:AA, cost 0, port-id 8001, message-age 0.00s, max-age 20.00s, hello-time 2.00s, forward-delay 15.00s
```
- In this example, we see that an `STP` message was sent containing information about the root switch, the MAC address of the root switch, the ID of the port over which the message was sent, and other configuration parameters such as the maximum aging time, hello time, and forward delay.