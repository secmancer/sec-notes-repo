### IP Addressing and Subnetting

**1. Media Access Control (MAC) Address**:
- **Purpose**: Identifies each host within a local network.
- **Limitation**: MAC addresses alone cannot be used to establish connections between different networks.



**2. Internet Protocol (IP) Address**:
- **Purpose**: Used for addressing on the Internet or any network. Ensures data delivery to the correct destination.
- **Address Structure**:
    - **IPv4**: 32-bit address divided into 4 octets (8-bit groups), represented in dotted-decimal notation.
    - **IPv6**: 128-bit address, represented in hexadecimal notation.

**3. Address Representation**:
- **IPv4**:
    - **Example**: `192.168.10.39`
    - **Binary Notation**:
        - Octet 1: `11000000` (192)
        - Octet 2: `10101000` (168)
        - Octet 3: `00001010` (10)
        - Octet 4: `00100111` (39)
    - **Decimal Representation**: `192.168.10.39`
- **IPv6**: Uses hexadecimal representation with 8 groups of 4 hexadecimal digits.



**4. IPv4 Address Classes**:
- **Class A**: `1.0.0.0` to `127.255.255.255`
    - **Subnet Mask**: `255.0.0.0`
    - **CIDR**: `/8`
- **Class B**: `128.0.0.0` to `191.255.255.255`
    - **Subnet Mask**: `255.255.0.0`
    - **CIDR**: `/16`
- **Class C**: `192.0.0.0` to `223.255.255.255`
    - **Subnet Mask**: `255.255.255.0`
    - **CIDR**: `/24`
- **Class D**: `224.0.0.0` to `239.255.255.255` (Multicast)
- **Class E**: `240.0.0.0` to `255.255.255.255` (Reserved)



**5. Subnet Mask**:
- **Purpose**: Determines which part of the IP address refers to the network and which part refers to the host.
- **Example**:
    - **Subnet Mask**: `255.255.255.0`
    - **CIDR Notation**: `/24`



**6. Network and Broadcast Addresses**:
- **Network Address**: Identifies the network segment.
- **Broadcast Address**: Sends data to all devices within the network segment.
- **Default Gateway**: Router IP address used to connect different networks and manage addresses.



**7. CIDR (Classless Inter-Domain Routing)**:
- **Purpose**: Replaces the old class-based system, allowing for flexible subnetting.
- **CIDR Notation**: Indicates the number of bits used for the network portion of the address.
    - **Example**: `192.168.10.39/24` (where `/24` represents the subnet mask `255.255.255.0`).



**8. Binary System**:
- **Description**: A number system using only two digits, 0 and 1.
- **IPv4 Address Calculation**:
    - **Example Address**: `192.168.10.39`
    - **Binary Calculation**: Convert each octet from decimal to binary.