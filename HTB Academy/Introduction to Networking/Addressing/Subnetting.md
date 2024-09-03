### Subnetting Overview

1. **Subnet Mask**: Divides an IP address into network and host parts.
2. **CIDR Notation**: Indicates the number of bits used for the network portion (`/26`, `/28`, etc.).
3. **Network Address**: The first address in a subnet; all host bits are set to 0.
4. **Broadcast Address**: The last address in a subnet; all host bits are set to 1.
5. **First Host**: The first usable IP address in a subnet; network address + 1.
6. **Last Host**: The last usable IP address in a subnet; broadcast address - 1.
7. **Number of Hosts**: Calculated as 2number of host bits−22^{\text{number of host bits}} - 22number of host bits−2 (subtracting 2 for network and broadcast addresses).

### Example Calculation

For the IP address `192.168.12.160` with a subnet mask of `255.255.255.192` (CIDR `/26`):

1. **Subnet Mask**: `255.255.255.192` converts to `11111111.11111111.11111111.11000000` in binary.
2. **Network Address**:
    - Binary: `11000000.10101000.00001100.10100000` AND `11111111.11111111.11111111.11000000` = `11000000.10101000.00001100.10000000`
    - Decimal: `192.168.12.128`
3. **Broadcast Address**:
    - Binary: `11000000.10101000.00001100.10100000` OR `00000000.00000000.00000000.00111111` = `11000000.10101000.00001100.10111111`
    - Decimal: `192.168.12.191`
4. **First Host**: `192.168.12.129`
5. **Last Host**: `192.168.12.190`
6. **Number of Hosts**: 2(32−26)−2=64−2=622^{(32 - 26)} - 2 = 64 - 2 = 622(32−26)−2=64−2=62

### Subnetting into Smaller Networks

If you need to divide `192.168.12.128/26` into 4 subnets:

1. **Calculate New Subnet Mask**: `/26` expanded by 2 bits to `/28`.
    - New Subnet Mask: `255.255.255.240`
2. **Number of Hosts per New Subnet**: 2(32−28)−2=16−2=142^{(32 - 28)} - 2 = 16 - 2 = 142(32−28)−2=16−2=14
3. **Subnets**:
    - **Subnet 1**:
        - Network Address: `192.168.12.128/28`
        - First Host: `192.168.12.129`
        - Last Host: `192.168.12.142`
        - Broadcast Address: `192.168.12.143`
    - **Subnet 2**:
        - Network Address: `192.168.12.144/28`
        - First Host: `192.168.12.145`
        - Last Host: `192.168.12.158`
        - Broadcast Address: `192.168.12.159`
    - **Subnet 3**:
        - Network Address: `192.168.12.160/28`
        - First Host: `192.168.12.161`
        - Last Host: `192.168.12.174`
        - Broadcast Address: `192.168.12.175`
    - **Subnet 4**:
        - Network Address: `192.168.12.176/28`
        - First Host: `192.168.12.177`
        - Last Host: `192.168.12.190`
        - Broadcast Address: `192.168.12.191`

### Mental Subnetting Tips

- Remember powers of 2 for quick calculations.
- Use modulo operation to determine usable IP ranges within subnets.
- The calculation can be simplified using binary math and understanding the octet structure.

### Questions
- Submit the decimal representation of the subnet mask from the following CIDR: 10.200.20.0/27
	- 255.255.255.224
- Submit the broadcast address of the following CIDR: 10.200.20.0/27
	- 10.200.20.31
- Split the network 10.200.20.0/27 into 4 subnets and submit the network address of the 3rd subnet as the answer.
	- 10.200.20.16
- Split the network 10.200.20.0/27 into 4 subnets and submit the broadcast address of the 2nd subnet as the answer.
	- 10.200.20.15