**Internet Protocols Overview**

Internet protocols are standardized rules and guidelines defined in RFCs that ensure devices on a network communicate consistently and reliably. They establish the format and structure of data being transmitted between devices connected via wired or wireless channels. The two main connection types used are Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).



### Transmission Control Protocol (TCP)
- **Definition**: A connection-oriented protocol that establishes a virtual connection before transmitting data using a Three-Way-Handshake. The connection is maintained until data transfer is complete.
- **Example**: When a web browser requests a webpage, TCP ensures that the HTML code is reliably transferred from the server to the browser.
- **Characteristics**: Reliable but slower due to overhead for establishing and maintaining the connection.



**Common TCP Protocols**:
- **Telnet** (Port 23): Remote login service
- **Secure Shell (SSH)** (Port 22): Secure remote login service
- **Simple Network Management Protocol (SNMP)** (Ports 161-162): Manage network devices
- **Hyper Text Transfer Protocol (HTTP)** (Port 80): Transfer webpages
- **Hyper Text Transfer Protocol Secure (HTTPS)** (Port 443): Transfer secure webpages
- **Domain Name System (DNS)** (Port 53): Lookup domain names
- **File Transfer Protocol (FTP)** (Ports 20-21): Transfer files
- **Trivial File Transfer Protocol (TFTP)** (Port 69): Transfer files
- **Network Time Protocol (NTP)** (Port 123): Synchronize computer clocks
- **Simple Mail Transfer Protocol (SMTP)** (Port 25): Email transfer
- **Post Office Protocol (POP3)** (Port 110): Retrieve emails
- **Internet Message Access Protocol (IMAP)** (Port 143): Access emails
- **Server Message Block (SMB)** (Port 445): Transfer files
- **Network File System (NFS)** (Ports 111, 2049): Mount remote systems
- **Bootstrap Protocol (BOOTP)** (Ports 67, 68): Bootstrap computers
- **Kerberos** (Port 88): Authentication and authorization
- **Lightweight Directory Access Protocol (LDAP)** (Port 389): Directory services
- **Remote Authentication Dial-In User Service (RADIUS)** (Ports 1812, 1813): Authentication and authorization
- **Dynamic Host Configuration Protocol (DHCP)** (Ports 67, 68): Configure IP addresses
- **Remote Desktop Protocol (RDP)** (Port 3389): Remote desktop access
- **Network News Transfer Protocol (NNTP)** (Port 119): Access newsgroups
- **Remote Procedure Call (RPC)** (Ports 135, 137-139): Call remote procedures
- **Identification Protocol (Ident)** (Port 113): Identify user processes
- **Internet Control Message Protocol (ICMP)** (Ports 0-255): Troubleshoot network issues
- **Internet Group Management Protocol (IGMP)** (Ports 0-255): Multicasting
- **Oracle DB Listener** (Ports 1521/1526): Oracle database listener
- **Ingres Lock** (Port 1524): Ingres database
- **Squid Web Proxy** (Port 3128): Caching and forwarding HTTP proxy
- **Secure Copy Protocol (SCP)** (Port 22): Securely copy files
- **Session Initiation Protocol (SIP)** (Port 5060): VoIP sessions
- **Simple Object Access Protocol (SOAP)** (Ports 80, 443): Web services
- **Secure Socket Layer (SSL)** (Port 443): Securely transfer files
- **TCP Wrappers (TCPW)** (Port 113): Access control
- **Internet Security Association and Key Management Protocol (ISAKMP)** (Port 500): VPN connections
- **Microsoft SQL Server** (Port 1433): SQL Server client connections
- **Kerberized Internet Negotiation of Keys (KINK)** (Port 892): Authentication and authorization
- **Open Shortest Path First (OSPF)** (Port 89): Routing
- **Point-to-Point Tunneling Protocol (PPTP)** (Port 1723): Create VPNs
- **Remote Execution (REXEC)** (Port 512): Execute commands on remote computers
- **Remote Login (RLOGIN)** (Port 513): Start interactive shell sessions on remote computers
- **X Window System (X11)** (Port 6000): GUI for networked computers
- **Relational Database Management System (DB2)** (Port 50000): Store, retrieve, manage data



### User Datagram Protocol (UDP)
- **Definition**: A connectionless protocol that sends data packets without establishing a virtual connection or checking for receipt.
- **Example**: Video streaming services use UDP to transmit video data, tolerating some data loss in favor of faster transmission.
- **Characteristics**: Faster but less reliable compared to TCP.



**Common UDP Protocols**:
- **Domain Name System (DNS)** (Port 53): Resolve domain names to IP addresses
- **Trivial File Transfer Protocol (TFTP)** (Port 69): Transfer files
- **Network Time Protocol (NTP)** (Port 123): Synchronize clocks
- **Simple Network Management Protocol (SNMP)** (Port 161): Manage network devices
- **Routing Information Protocol (RIP)** (Port 520): Exchange routing information
- **Internet Key Exchange (IKE)** (Port 500): Establish VPN connections
- **Bootstrap Protocol (BOOTP)** (Port 68): Bootstrap hosts
- **Dynamic Host Configuration Protocol (DHCP)** (Port 67): Assign IP addresses
- **Telnet** (Port 23): Text-based remote access
- **MySQL** (Port 3306): Database management system
- **Terminal Server (TS)** (Port 3389): Remote access protocol
- **NetBIOS Name** (Port 137): Resolve NetBIOS names on LAN
- **Microsoft SQL Server** (Port 1434): SQL Server Browser service
- **Universal Plug and Play (UPnP)** (Port 1900): Device discovery
- **PostgreSQL** (Port 5432): Object-relational database management system
- **Virtual Network Computing (VNC)** (Port 5900): Graphical desktop sharing
- **X Window System (X11)** (Ports 6000-6063): GUI on Unix-like systems
- **Syslog** (Port 514): Collect and store log messages
- **Internet Relay Chat (IRC)** (Port 194): Real-time text messaging
- **OpenPGP** (Port 11371): Encrypting and signing communications
- **Internet Protocol Security (IPsec)** (Port 500): Secure communication
- **X Display Manager Control Protocol (XDMCP)** (Port 177): Remote log in to X11


### Internet Control Message Protocol (ICMP)
- **Definition**: Used for error reporting and status information in network communication.
- **Requests**: Messages sent to request information or actions, e.g., ping requests.
- **Messages**: Can be requests or replies, such as error messages, time exceeded, and destination unreachable.

**ICMP Versions**:
- **ICMPv4**: For IPv4, widely used.
- **ICMPv6**: For IPv6, with additional functionality.

**ICMP Request Types**:
- **Echo Request**: Tests network reachability.
- **Timestamp Request**: Determines time on a remote device.
- **Address Mask Request**: Requests the subnet mask of a device.

**ICMP Message Types**:
- **Echo Reply**: Response to an echo request.
- **Destination Unreachable**: Packet delivery failure.
- **Redirect**: Inform of a better router.
- **Time Exceeded**: Packet took too long.
- **Parameter Problem**: Header issue.
- **Source Quench**: Too many packets received.

**Time-To-Live (TTL)**:
- **Purpose**: Limits packet lifetime, prevents infinite routing loops.
- **Usage**: Determines hops and approximate distance.
- **Default Values**: Windows (128), macOS/Linux (64), Solaris (255).



### Voice over Internet Protocol (VoIP)
- **Definition**: Transmits voice and multimedia communications over the internet.
- **Common Ports**:
    - **SIP (Session Initiation Protocol)**: TCP/5060, TCP/5061
    - **H.323**: TCP/1720 (less common)

**SIP Methods**:
- **INVITE**: Initiates a session.
- **ACK**: Confirms receipt of an INVITE.
- **BYE**: Terminates a session.
- **CANCEL**: Cancels an INVITE request.
- **REGISTER**: Registers a user agent.
- **OPTIONS**: Requests server/user capabilities.


**Information Disclosure**:
- SIP OPTIONS requests can enumerate users or gather server capabilities. Configuration files like `SEPxxxx.cnf` in Cisco Unified Communications Manager provide details for IP Phones.