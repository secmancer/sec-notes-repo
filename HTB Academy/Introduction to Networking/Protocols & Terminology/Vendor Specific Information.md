### **Cisco IOS Overview**

**Cisco IOS** is the operating system used in Cisco routers and switches, providing features for network management and operation. Key features include:

- **IPv6 Support**: Handling next-generation IP addresses.
- **Quality of Service (QoS)**: Ensuring priority for critical network traffic.
- **Security Features**: Including encryption and authentication mechanisms.
- **Virtualization**: Features like VPLS and VRF for network segmentation and management.

**Management Methods**:

- **Command Line Interface (CLI)**: Common for direct configuration and troubleshooting.
- **Graphical User Interface (GUI)**: Available in some Cisco devices for easier management.

### **VLANs (Virtual Local Area Networks)**

**Purpose**:

- **Segmentation**: Divide a single physical network into multiple logical networks to improve security and performance.
- **Broadcast Domains**: Each VLAN is a separate broadcast domain, reducing broadcast traffic and improving network efficiency.

**Example VLAN Configuration**:

- **Servers**: VLAN 10, 192.168.1.0/24
- **C-Level**: VLAN 20, 192.168.2.0/24
- **Finance**: VLAN 30, 192.168.3.0/24
- **HR**: VLAN 40, 192.168.4.0/24
- **Marketing**: VLAN 50, 192.168.5.0/24
- **Support**: VLAN 60, 192.168.6.0/24

**Types of Ports**:

- **Access Ports**: Assigned to a single VLAN, carry traffic for that VLAN only.
- **Trunk Ports**: Carry traffic for multiple VLANs, typically used to connect switches or switches to routers.

**Trunking Methods**:

- **ISL (Inter-Switch Link)**: Cisco-proprietary, deprecated.
- **IEEE 802.1Q**: Standard protocol for VLAN tagging, widely used.

### **VLAN Tagging**

**802.1Q Tagging**:

- **TPID (Tag Protocol Identifier)**: 0x8100, marks the frame as VLAN-tagged.
- **TCI (Tag Control Information)**: Contains Priority code point (PCP), Drop eligible indicator (DEI), and VLAN Identifier (VID).

**Creating VLANs**:

- **Linux**:
    - Load 802.1Q module: `sudo modprobe 8021q`
    - Create VLAN: `sudo ip link add link eth0 name eth0.20 type vlan id 20`
    - Assign IP: `sudo ip addr add 192.168.1.1/24 dev eth0.20`
- **Windows**:
    - Use Device Manager or PowerShell (`Set-NetAdapter -Name "Ethernet 2" -VlanID 10`).

### **Analyzing VLAN Traffic**

**Wireshark**:

- Use filters to inspect VLAN-tagged packets:
    - `vlan` for general VLAN traffic.
    - `vlan.id == 10` to filter by specific VLAN ID.

**Tshark**:

- Enumerate VLAN IDs from a packet capture: `tshark -r "file.pcap" -T fields -e vlan.id | sort -n -u`

### **VLAN Security and Attacks**

**VLAN Hopping**:

- **Standard VLAN Hopping**: Exploits Dynamic Trunking Protocol (DTP) to gain access to multiple VLANs.
- **Double-Tagging VLAN Hopping**: Embeds a second VLAN tag in a frame to bypass VLAN restrictions.

**Mitigations**:

- Disable DTP on switch ports that don’t require trunking.
- Implement strong VLAN configurations and monitor for abnormal traffic patterns.