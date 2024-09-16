### TCP vs. UDP
- **Transmission Control Protocol (TCP)**:
    - Connection-oriented, reliable protocol.
    - Ensures all data is received and errors are corrected.
    - Slower due to error recovery, used for transmitting web pages, emails, etc.
- **User Datagram Protocol (UDP)**:
    - Connectionless, faster but less reliable.
    - Used for real-time data transmission (e.g., video streaming, online gaming).
    - No guarantee of data delivery or error correction.


### IP Packet Overview
- **IP Packet**:
    - Used to transmit data across networks.
    - Consists of two parts: header and payload.
    - Header contains routing information, and payload contains actual data.

#### **IP Header Fields**:
- **Version**: Indicates IP version used (e.g., IPv4 or IPv6).
- **Internet Header Length**: Size of the header in 32-bit words.
- **Class of Service**: Specifies the priority of the data.
- **Total Length**: Size of the entire packet in bytes.
- **ID**: Identifies fragments of the packet.
- **Flags**: For fragmentation purposes.
- **Fragment Offset**: Position of the fragment in the original packet.
- **Time to Live (TTL)**: How long the packet can stay on the network.
- **Protocol**: Defines the protocol used (e.g., TCP or UDP).
- **Checksum**: Detects errors in the header.
- **Source/Destination Addresses**: Specify sender and receiver IPs.
- **Options**: Contains optional routing info.
- **Padding**: Ensures the packet is a full word length.


### Network Sniffing (TCP/UDP Connections)
- **TCPdump Example**:  
    Identifying traffic from multiple IPs:
    - IP ID field shows packet sequence.
    - Example: Two IP addresses sending packets to the same target with sequential IDs suggests the same host.


### IP Record-Route Field
- **Ping Example with `-R`**:
    - Shows the route to a destination by listing all intermediate devices' IPs.
    - Example:  
        `ping -c 1 -R 10.129.143.158`  
        Displays route: `10.10.14.38 > 10.129.0.1 > 10.129.143.158`.
- **Traceroute**:
    
    - Traces the route to a destination by sending TCP SYN packets with increasing TTL.
    - Receives ICMP Time-Exceeded packets to trace each hop.



### TCP vs. UDP Packet Structure
- **TCP Packets**:
    - Divided into a header (source/destination ports, sequence numbers, etc.) and payload (actual data).
    - TCP control flags (e.g., SYN, ACK) manage communication states.
- **UDP Packets**:
    
    - Connectionless, sends datagrams directly to the target host.
    - Commonly used in `traceroute` on Unix systems.


### Blind Spoofing Attack
- **Blind Spoofing**:
    - Attack technique where an attacker manipulates IP header fields (e.g., source/destination ports, Initial Sequence Number) without seeing responses from the target.
    - Commonly used to disrupt connections or monitor network traffic.