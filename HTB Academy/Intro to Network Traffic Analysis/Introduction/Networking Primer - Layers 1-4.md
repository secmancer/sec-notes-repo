#### OSI Model vs. TCP-IP Model

|**Trait**|**OSI Model**|**TCP-IP Model**|
|---|---|---|
|**Layers**|Seven|Four|
|**Flexibility**|Strict|Loose|
|**Dependency**|Protocol independent & generic|Based on common communication protocols|

- **OSI Model**: Segmented into seven layers. It provides a theoretical framework, detailing how communication is structured from physical transmission to data presentation.
    
    - **Layers 1-4**: Focus on data transportation, including physical medium, data framing, and transport management.
    - **Layers 5-7**: Handle data interpretation, management, and presentation.
- **TCP-IP Model**: More practical and flexible with four layers. It aligns closely with actual network operations.
    
    - **Layer 1**: Link Layer (combines OSI’s Layers 1 & 2)
    - **Layer 2**: Internet Layer (aligns with OSI’s Network Layer)
    - **Layer 3**: Transport Layer (aligns with OSI’s Transport Layer)
    - **Layer 4**: Application Layer (combines OSI’s Sessions, Presentation, and Application Layers)

### Protocol Data Units (PDUs)

- **Encapsulation**: Data from higher layers is wrapped with control information at each lower layer, forming a PDU. This includes layer-specific information such as headers and operational flags.
- **Wireshark Display**: PDUs are shown in reverse order as they are de-encapsulated during inspection.

### Addressing Mechanisms

#### MAC Addressing

- **MAC Address**: A 48-bit address used in Layer 2 (Data Link Layer) for local network communication.
- **Format**: Six octets in hexadecimal.
- **Function**: Used for direct communication within a broadcast domain. When crossing into Layer 3, routers use MAC addresses to forward packets, then replace the Layer 2 information with new details for the next hop.

#### IP Addressing

- **IPv4**:
    
    - **Format**: 32-bit address divided into four octets (e.g., 192.168.86.243).
    - **Usage**: Core method for routing packets across networks. Found in Layer 3 (Network Layer) in OSI and Layer 2 (Internet Layer) in TCP-IP.
- **IPv6**:
    
    - **Format**: 128-bit address divided into 16 octets (e.g., `2001:db8::1`).
    - **Advantages**: Larger address space, better multicast support, built-in security, and simplified headers.
    - **Address Types**:
        - **Unicast**: For a single interface.
        - **Anycast**: For multiple interfaces; one receives the packet.
        - **Multicast**: For multiple interfaces; all receive the packet.
        - **Broadcast**: Not used in IPv6; multicast serves similar purposes.

#### Adoption of IPv6

- **Current Adoption**: Around 40% globally, as of the latest statistics.

### TCP vs. UDP

|**Characteristic**|**TCP**|**UDP**|
|---|---|---|
|**Transmission**|Connection-oriented|Connectionless|
|**Connection Establishment**|Uses a three-way handshake|No connection establishment|
|**Data Delivery**|Stream-based|Packet-based|
|**Receipt of Data**|Acknowledged and sequenced|No acknowledgment or sequencing|
|**Speed**|Slower due to overhead|Faster, but less reliable|

- **TCP**: Reliable, connection-oriented protocol with error checking and acknowledgment. Suitable for applications needing complete data, like SSH.
- **UDP**: Fast, connectionless protocol suitable for applications where speed is crucial and minor data loss is acceptable, like streaming or DNS queries.

### TCP Three-Way Handshake

1. **SYN**: Client sends a SYN packet to initiate a connection.
2. **SYN-ACK**: Server responds with SYN-ACK to acknowledge and synchronize.
3. **ACK**: Client responds with an ACK, completing the handshake and establishing the connection.

**Packet Flow Example**:

- SYN: Client → Server
- SYN-ACK: Server → Client
- ACK: Client → Server

### TCP Session Teardown

1. **FIN, ACK**: Client sends FIN to signal the end of data transfer.
2. **FIN, ACK**: Server acknowledges and sends its own FIN.
3. **ACK**: Client acknowledges the server’s FIN, completing the connection termination.

**Packet Flow Example**:

- FIN, ACK: Client → Server
- FIN, ACK: Server → Client
- ACK: Client → Server

![[Screenshot_20240820_153403.png]]

![[Screenshot_20240820_154715.png]]

![[Screenshot_20240820_154734.png]]

![[Screenshot_20240820_154742.png]]

![[Screenshot_20240820_154748.png]]
![[Screenshot_20240820_154754.png]]

### Questions
- How many layers does the OSI model have?
	- 7
- How many layers are there in the TCP/IP model?
	- 4
- True or False: Routers operate at layer 2 of the OSI model?
	- False
- What addressing mechanism is used at the Link Layer of the TCP/IP model?
	- Mac-Address
- At what layer of the OSI model is a PDU encapsulated into a packet? ( the number )
	- 3
- What addressing mechanism utilizes a 32-bit address?
	- IPv4
- What Transport layer protocol is connection oriented?
	- TCP
- What Transport Layer protocol is considered unreliable?
- TCP's three-way handshake consists of 3 packets: 1.Syn, 2.Syn & ACK, 3. _? What is the final packet of the handshake?
	- ACK