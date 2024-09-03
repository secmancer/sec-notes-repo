### **IPv6 Overview**

- **Address Length**: IPv6 addresses are 128 bits long, compared to 32 bits for IPv4.
- **Address Space**: IPv6 offers a vastly larger address space, approximately 3.4×10383.4 \times 10^{38}3.4×1038 addresses, compared to about 4.3 billion in IPv4.
- **Address Notation**: IPv6 addresses are represented in hexadecimal format, separated by colons (:), while IPv4 addresses are in dotted-decimal format.
- **Dynamic Addressing**: IPv6 supports Stateless Address Autoconfiguration (SLAAC) and DHCPv6, whereas IPv4 uses DHCP.
- **IPsec**: In IPv6, IPsec (Internet Protocol Security) is mandatory, enhancing security.
- **Data Package Size**: IPv6 supports data packets up to 4 GB, whereas IPv4 supports a maximum of 64 KB.

### **Types of IPv6 Addresses**

1. **Unicast**: Identifies a single interface. Packets sent to a unicast address are delivered to the specific interface.
2. **Anycast**: Assigned to multiple interfaces, but only the nearest (as defined by the routing protocol) interface receives the packet.
3. **Multicast**: Sent to multiple interfaces, where all interfaces receive the packet.
4. **Broadcast**: Not used in IPv6; broadcast functionality is achieved using multicast.

### **IPv6 Address Format**

- **Full IPv6 Address**: Represented in eight 16-bit blocks, separated by colons (e.g., `fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64`).
- **Short IPv6 Address**: Leading zeros in each block can be omitted, and consecutive blocks of zeros can be replaced with double colons (::) (e.g., `fe80::dd80:b1a9:6687:2d3b/64`).

### **Address Prefixes**

- **Network Prefix**: Identifies the network part of the address. Common prefix lengths are /32, /48, /56, and /64.
- **Interface Identifier**: The host part, often derived from the MAC address and converted to a 64-bit format.

### **Hexadecimal Representation**

Hexadecimal (hex) is used to represent IPv6 addresses. It simplifies binary representation, as each hex digit represents four binary digits (bits). For example:

- **Decimal 1-15**: Represented as `1-F` in hex.
- **Binary**: Each byte is represented as two hex digits.

**Example Conversion:**

- **IPv4 Address (192.168.12.160)**
    
    - **Binary**: 11000000.10101000.00001100.10100000
    - **Hex**: C0.A8.0C.A0
- **IPv6 Address (fe80:0000:0000:0000:dd80:b1a9:6687:2d3b)**
    
    - **Binary**: Each group of 4 hex digits (e.g., fe80) represents 16 bits.
    - **Hexadecimal**: Directly used for representation, with each group separated by colons.

### **IPv6 Address Shortening Rules (RFC 5952)**

1. **Lowercase**: All letters in the address should be lowercase.
2. **Omit Leading Zeros**: Leading zeros in each block should be omitted.
3. **Use of Double Colons (::)**: One or more consecutive blocks of zeros can be replaced by `::`. This can be used only once in an address.