### MAC Addresses

- **Format:** MAC addresses are 48-bit addresses represented as hexadecimal numbers, typically displayed in formats like `DE:AD:BE:EF:13:37`, `DE-AD-BE-EF-13-37`, or `DEAD.BEEF.1337`.
    
- **Structure:**
    
    - **Organization Unique Identifier (OUI):** The first 24 bits (3 bytes) identify the manufacturer.
    - **Individual Address Part (NIC):** The last 24 bits (3 bytes) are assigned by the manufacturer to ensure uniqueness.
- **Address Types:**
    
    - **Unicast:** Addressing a single specific device.
    - **Multicast:** Addressing a group of devices on the local network.
    - **Broadcast:** Addressing all devices on the local network.
- **Special Ranges:**
    
    - **Local Range:** Reserved MAC addresses for special purposes.
    - **Global OUI vs. Locally Administered:** Identified by the second-to-last bit in the first octet; global OUIs are IEEE-assigned, while locally administered addresses are set by users.

### ARP (Address Resolution Protocol)

- **Purpose:** Resolves IP addresses to MAC addresses on a local network to facilitate communication.
    
- **Request and Reply:**
    
    - **ARP Request:** Broadcasts a request for the MAC address corresponding to an IP address.
    - **ARP Reply:** Provides the MAC address for the requested IP address.
- **Vulnerabilities:**
    
    - **ARP Spoofing/Cache Poisoning:** An attacker sends false ARP messages to associate their MAC address with another device's IP address, potentially intercepting or altering traffic.

### Security Measures

- **Against ARP Spoofing:**
    - Implementing secure protocols (e.g., IPSec, SSL).
    - Using firewalls and intrusion detection systems.
    - Network segmentation and monitoring.