### Transmission Control Protocol (TCP)

- **Connection-oriented**: Establishes a connection before transmitting data.
- **Three-Way Handshake**: Method for establishing a connection.
- **Reliable but slower**: Ensures data integrity and order but with more overhead.

#### Common TCP Protocols:

- **Telnet (23)**: Remote login service.
- **SSH (22)**: Secure remote login.
- **HTTP (80)**: Transfer of webpages.
- **HTTPS (443)**: Secure transfer of webpages.
- **FTP (20-21)**: File transfer.
- **SMTP (25)**: Email transfer.
- **IMAP (143)**: Access emails.
- **NFS (111, 2049)**: Network file system.
- **RDP (3389)**: Remote desktop access.

### User Datagram Protocol (UDP)

- **Connectionless**: Sends data without establishing a connection.
- **Faster but less reliable**: No guarantee of data delivery.

#### Common UDP Protocols:

- **DNS (53)**: Domain name resolution.
- **TFTP (69)**: File transfer.
- **NTP (123)**: Synchronize computer clocks.
- **RIP (520)**: Routing information exchange.
- **DHCP (67)**: Assign IP addresses dynamically.
- **UDP Port 1900**: Universal Plug and Play (UPnP).

### Internet Control Message Protocol (ICMP)

- **Error reporting and status**: Communicates errors and status updates between devices.
- **Versions**: ICMPv4 (for IPv4) and ICMPv6 (for IPv6).
- **Key Requests and Messages**:
    - **Echo Request/Reply**: Tests connectivity.
    - **Destination Unreachable**: Indicates packet delivery failure.
    - **Time Exceeded**: Packet lifetime expired.
    - **TTL (Time-To-Live)**: Limits packet lifetime to prevent infinite loops.

### Voice over Internet Protocol (VoIP)

- **Transmits voice and multimedia**: Uses broadband internet instead of traditional phone lines.
- **Common Ports**:
    - **SIP (5060, 5061)**: Signaling protocol for real-time communication.
    - **H.323 (1720)**: Protocol for multimedia communication.
- **SIP Methods**:
    - **INVITE**: Initiates a session.
    - **ACK**: Confirms receipt of an INVITE request.
    - **BYE**: Terminates a session.
    - **OPTIONS**: Requests information about capabilities.

### Additional Considerations:

- **Enumeration via SIP**: Possible to discover user information or perform attacks.
- **Cisco SEPxxxx.cnf File**: Configuration file for Cisco IP Phones with settings and parameters.