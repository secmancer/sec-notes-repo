### MAC Address Overview
- **MAC Address (Media Access Control):** A unique 48-bit (6 octets) address assigned to each network interface, represented in hexadecimal format.
- **Formats:**
    - **DE:AD:BE:EF:13:37**
    - **DE-AD-BE-EF-13-37**
    - **DEAD.BEEF.1337**

#### MAC Address Representation

|Representation|1st Octet|2nd Octet|3rd Octet|4th Octet|5th Octet|6th Octet|
|---|---|---|---|---|---|---|
|Binary|1101 1110|1010 1101|1011 1110|1110 1111|0001 0011|0011 0111|
|Hex|DE|AD|BE|EF|13|37|

#### MAC Address Components
- **Organization Unique Identifier (OUI):** The first 3 bytes (24 bits) assigned by IEEE to manufacturers.
- **Individual Address Part:** The last 3 bytes (24 bits) assigned by the manufacturer, ensuring uniqueness.

### Address Types
- **Unicast:**
    - Identified by the last bit of the first octet being 0.
    - Packet is delivered to a specific host.
- **Multicast:**
    - Identified by the last bit of the first octet being 1.
    - Packet is sent to multiple hosts on the network.
- **Broadcast:**
    - All bits of the MAC address set to 1 (FF:FF:FF:FF:FF).
    - Packet is sent to all devices in the network.

#### Special MAC Address Ranges
- **Local Range:**
    - `02:00:00:00:00:00`
    - `06:00:00:00:00:00`
    - `0A:00:00:00:00:00`
    - `0E:00:00:00:00:00`
- **Global OUI vs. Locally Administrated:**
    - **Global OUI:** Identified by the second last bit of the first octet being 0.
    - **Locally Administrated:** Identified by the second last bit of the first octet being 1.

### Address Resolution Protocol (ARP)
- **Purpose:** Resolves IP addresses to MAC addresses within a LAN.
- **Process:**
    1. **ARP Request:** Broadcast to the network asking for the MAC address corresponding to an IP address.
    2. **ARP Reply:** The device with the matching IP address responds with its MAC address.

#### ARP Packet Example

| Time  | Source IP     | Destination IP | ARP Operation | Source MAC     | Target MAC |
| ----- | ------------- | -------------- | ------------- | -------------- | ---------- |
| 0.000 | 10.129.12.100 | 10.129.12.255  | Request       | -              | -          |
| 0.015 | 10.129.12.101 | 10.129.12.100  | Reply         | AA:AA:AA:AA:AA | -          |
| 0.030 | 10.129.12.102 | 10.129.12.255  | Request       | -              | -          |
| 0.045 | 10.129.12.103 | 10.129.12.102  | Reply         | BB:BB:BB:BB:BB | -          |

### Security Considerations
- **MAC Spoofing:** Changing a MAC address to mimic another device.
- **MAC Flooding:** Overloading a switch's MAC address table to disrupt network function.
- **MAC Address Filtering:** Exploiting networks that use MAC address-based access control.

#### ARP Attacks
- **ARP Spoofing (ARP Poisoning):** Associating a malicious MAC address with an IP address to intercept or manipulate traffic.

#### ARP Spoofing Example

|Time|Source IP|Destination IP|ARP Operation|Source MAC|Target MAC|
|---|---|---|---|---|---|
|0.000|10.129.12.100|10.129.12.101|Reply|AA:AA:AA:AA:AA|-|
|0.015|10.129.12.100|10.129.12.255|Request|-|-|
|0.030|10.129.12.101|10.129.12.100|Reply|BB:BB:BB:BB:BB|-|
|0.045|10.129.12.100|10.129.12.101|Reply|AA:AA:AA:AA:AA|-|

- **Protection Measures:**
    - Use secure network protocols (e.g., IPSec, SSL).
    - Implement security measures (e.g., firewalls, intrusion detection systems).