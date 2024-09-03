### TCP vs. UDP

- **TCP (Transmission Control Protocol)**
    
    - **Connection-Oriented**: Establishes a connection before transmitting data, ensuring reliable delivery.
    - **Reliability**: Guarantees that all data sent is received correctly. If data is lost or corrupted, TCP handles retransmissions.
    - **Use Cases**: Ideal for applications where data integrity is crucial, such as web browsing, email, and file transfers.
- **UDP (User Datagram Protocol)**
    
    - **Connectionless**: Sends data without establishing a connection or ensuring delivery.
    - **Speed**: Faster than TCP due to the lack of connection setup and error recovery.
    - **Use Cases**: Suitable for real-time applications where speed is more important than reliability, such as streaming, gaming, and VoIP.

### IP Packet Structure

- **IP Packet**: Consists of a header and a payload. The header contains routing and control information, while the payload carries the actual data.
- **IP Header Fields**:
    - **Version**: Protocol version (IPv4 or IPv6).
    - **Internet Header Length (IHL)**: Length of the header in 32-bit words.
    - **Class of Service (ToS)**: Priority level of the packet.
    - **Total Length**: Total length of the packet, including header and payload.
    - **Identification**: Unique ID for fragment reassembly.
    - **Flags**: Indicate fragmentation.
    - **Fragment Offset**: Position of the fragment in the original packet.
    - **Time to Live (TTL)**: Limits the packet’s lifespan to prevent endless looping.
    - **Protocol**: Specifies the protocol used (TCP, UDP, etc.).
    - **Checksum**: Error-checking for the header.
    - **Source/Destination Address**: IP addresses of the sender and receiver.
    - **Options**: Optional fields for various control features.
    - **Padding**: Ensures the header is a multiple of 32 bits.

### IP Header Analysis

- **IP ID Field**: Unique identifier for packet fragments. Essential for reassembling fragmented packets.
    
- **Record-Route Field**: Records the route taken by a packet. Useful for tracing the path of packets through the network.
    

### Network Sniffing

- **Example**: `TCPdump` output shows packets from different IP addresses with continuous IP IDs, indicating packets from the same host.

### Traceroute

- **Method**: Uses TTL values to discover the path packets take to reach a destination. Each router decrements the TTL, sending back an ICMP Time-Exceeded message if TTL reaches zero.

### IP Payload

- **TCP Payload**: Contains data from applications. The TCP header includes fields for sequence numbers, acknowledgment, control flags, window size, checksum, and urgent pointer.
    
- **UDP Payload**: Contains datagrams sent directly to the target host without connection setup.
    

### Blind Spoofing

- **Definition**: Attack where false data is sent without seeing responses from the target. Manipulates IP header fields to disrupt or intercept network traffic. Commonly used to break or monitor network connections.