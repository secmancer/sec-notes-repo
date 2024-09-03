### **IP Addressing and MAC Addresses**

- **MAC Address**: A unique identifier assigned to network interfaces for communication within the same local network. It's like an apartment number, identifying a specific device within a building (local network).
    
- **IP Address**: Used for identifying devices across different networks. It functions like a postal address, ensuring data is delivered to the correct location within or outside the network.
    

### **IPv4 Address Structure**

- **IPv4 Address**: Consists of a 32-bit number divided into four 8-bit octets. These are often shown in dotted-decimal notation (e.g., `192.168.10.39`).
    
- **Subnet Mask**: Defines which portion of the IP address is the network and which is the host. It's also a 32-bit number, similar to the IP address.
    

### **Subnetting**

- **Subnetting**: Involves dividing a network into smaller sub-networks to improve performance and security. This is done by modifying the subnet mask.
    
- **Example**:
    
    - **IP Address**: `192.168.10.39`
    - **Subnet Mask**: `255.255.255.0`
    - **CIDR Notation**: `192.168.10.39/24` (indicating that the first 24 bits are the network portion)

### **IPv4 Address Classes**

- **Class A**: `1.0.0.0` to `127.255.255.255`
    
    - **Default Subnet Mask**: `255.0.0.0`
    - **CIDR**: `/8`
- **Class B**: `128.0.0.0` to `191.255.255.255`
    
    - **Default Subnet Mask**: `255.255.0.0`
    - **CIDR**: `/16`
- **Class C**: `192.0.0.0` to `223.255.255.255`
    
    - **Default Subnet Mask**: `255.255.255.0`
    - **CIDR**: `/24`
- **Class D**: Used for multicast.
    
- **Class E**: Reserved for experimental use.
    

### **Network and Broadcast Addresses**

- **Network Address**: Identifies the entire network. For instance, `192.168.10.0` in the `192.168.10.0/24` network.
    
- **Broadcast Address**: Used to send data to all devices within a network. For example, `192.168.10.255` in the `192.168.10.0/24` network.
    

### **Binary and Decimal Representation**

- **Binary to Decimal Conversion**:
    
    - Example: `192` in binary is `11000000`. Calculation: `128 + 64 = 192`.
- **Subnet Mask Representation**:
    
    - For `255.255.255.0`, in binary: `11111111.11111111.11111111.00000000`.

### **CIDR Notation**

- **CIDR**: Replaces traditional IP classes and allows for more flexible subnetting. It shows the number of bits used for the network portion of the address.
    
- **Example**:
    
    - **IP Address**: `192.168.10.39`
    - **Subnet Mask**: `255.255.255.0` (or `/24` in CIDR notation)
