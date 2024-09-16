### Subnetting Notes



**Subnetting Overview**
- **Subnetting** is the process of dividing an IPv4 address range into smaller segments called subnets.
- A **subnet** is a logical segment of a network that uses IP addresses with the same network address. Think of it as a labeled entrance on a large building corridor.



**Components of Subnetting**
- **Network Address**
- **Broadcast Address**
- **First Host**
- **Last Host**
- **Number of Hosts**



**Example**
- **IPv4 Address:** 192.168.12.160
- **Subnet Mask:** 255.255.255.192
- **CIDR:** 192.168.12.160/26



**Network & Host Parts**
- An IP address is divided into network and host parts.
    - **Network Part:** Defined by the subnet mask, which uses 1-bits to determine the main network.
    - **Host Part:** Defined by the remaining bits that can change to identify hosts within the subnet.



**Example Breakdown**
1. **IPv4 Address:** 192.168.12.160
    - Binary: `11000000.10101000.00001100.10100000`
2. **Subnet Mask:** 255.255.255.192
    - Binary: `11111111.11111111.11111111.11000000`



**Subnet Calculations**
- **Network Address:** Set host bits to 0.
    - Result: 192.168.12.128
- **Broadcast Address:** Set host bits to 1.
    - Result: 192.168.12.191
- **Host Range:** 192.168.12.129 to 192.168.12.190
- **Total Hosts:** 64 - 2 (network & broadcast) = 62 usable addresses.



**Subnetting into Smaller Networks**
- To divide the subnet into smaller subnets, extend the subnet mask. For instance, dividing into 4 subnets requires a subnet mask of /28.



**Expanded Subnet Mask**
- **Original Subnet Mask:** /26
- **New Subnet Mask:** /28
    - **Subnet Mask in Decimal:** 255.255.255.240



**Subnet Details**
- **Each Subnet Size:** 16 addresses
- **Subnets Created:**
    1. **Subnet 1:** 192.168.12.128/28
        - Network: 192.168.12.128
        - First Host: 192.168.12.129
        - Last Host: 192.168.12.142
        - Broadcast: 192.168.12.143
    2. **Subnet 2:** 192.168.12.144/28
        - Network: 192.168.12.144
        - First Host: 192.168.12.145
        - Last Host: 192.168.12.158
        - Broadcast: 192.168.12.159
    3. **Subnet 3:** 192.168.12.160/28
        - Network: 192.168.12.160
        - First Host: 192.168.12.161
        - Last Host: 192.168.12.174
        - Broadcast: 192.168.12.175
    4. **Subnet 4:** 192.168.12.176/28
        - Network: 192.168.12.176
        - First Host: 192.168.12.177
        - Last Host: 192.168.12.190
        - Broadcast: 192.168.12.191



**Mental Subnetting**
- **Network Address / Subnet Size:** Identifies which octet changes.
    - Example: **/25** means only the fourth octet changes.
- **Modulo Operation:** Used to calculate size of subnets.
    - Example: For /25, `(25 % 8) = 1`. Usable IP addresses are `2^(8-1) = 128`.



**IP Address Ranges**
- For a /25 subnet:
    - **Range 1:** 192.168.1.0 - 192.168.1.127
        - Usable: 192.168.1.1 - 192.168.1.126
    - **Range 2:** 192.168.1.128 - 192.168.1.255
        - Usable: 192.168.1.129 - 192.168.1.254


## Questions
- Submit the decimal representation of the subnet mask from the following CIDR: 10.200.20.0/27
	- 255.255.255.224
- Submit the broadcast address of the following CIDR: 10.200.20.0/27
	- 10.200.20.31
- Split the network 10.200.20.0/27 into 4 subnets and submit the network address of the 3rd subnet as the answer.
	- 10.200.20.16
- Split the network 10.200.20.0/27 into 4 subnets and submit the broadcast address of the 2nd subnet as the answer.
	- 10.200.20.15