### HTTP (Hypertext Transfer Protocol)

- **Purpose**: Transfers data in clear text between a client and server over TCP.
- **Ports**: Standard ports are 80 and 8000; it can use other ports or even UDP in exceptional cases.
- **Methods**:
    - **GET**: Requests information from the server.
    - **POST**: Submits data to the server.
    - **PUT**: Updates or creates resources at the specified URI.
    - **DELETE**: Removes resources at the specified URI.
    - **HEAD**: Requests the headers of a resource.
    - **TRACE**: Diagnoses the path to the server.
    - **OPTIONS**: Lists supported methods by the server.
    - **CONNECT**: Establishes a tunnel for secure communication.
- **RFC**: RFC 2616 for detailed specifications.

### HTTPS (Hypertext Transfer Protocol Secure)

- **Purpose**: Secures HTTP traffic using Transport Layer Security (TLS) or Secure Sockets Layer (SSL).
- **Ports**: Standard ports are 443 and 8443.
- **TLS Handshake**:
    - Establishes encryption parameters and authenticates both parties.
    - Ensures data integrity and secure communication.
- **RFC**: RFC 2246 for detailed TLS specifications.

### FTP (File Transfer Protocol)

- **Purpose**: Transfers files between devices; can be used through command-line, web browsers, or graphical clients.
- **Ports**: Uses port 20 for data transfer and port 21 for command control.
- **Modes**:
    - **Active Mode**: Server listens for data transfer on a port specified by the client.
    - **Passive Mode**: Client initiates the data connection to the server's specified port, useful for clients behind firewalls or NAT.
- **Commands**:
    - **USER**: Specifies the user for login.
    - **PASS**: Sends the password.
    - **PORT**: Specifies the data port in active mode.
    - **PASV**: Switches to passive mode.
    - **LIST**: Lists files in the current directory.
    - **RETR**: Retrieves a file.
- **RFC**: RFC 959 for detailed specifications.

### SMB (Server Message Block)

- **Purpose**: Shares resources like files and printers over a network.
- **Ports**:
    - TCP port 445 for direct transport.
    - UDP ports 137 and 138 for NetBIOS.
    - TCP port 139 for NetBIOS over TCP.
- **Features**:
    - Connection-oriented, requires authentication.
    - Allows access to shared resources, often used in Windows environments.
- **Traffic**: Commonly uses TCP for communication and performs a handshake like other TCP-based protocols.

### Questions
- What is the default operational mode method used by FTP?
	- active
- FTP utilizes what two ports for command and data transfer? (separate the two numbers with a space)
	- 20 21
- Does SMB utilize TCP or UDP as its transport layer protocol?
	- TCP
- SMB has moved to using what TCP port?
	- 445
- Hypertext Transfer Protocol uses what well known TCP port number?
	- 80
- What HTTP method is used to request information and content from the webserver?
	- GET
- What web based protocol uses TLS as a security measure?
	- HTTPS
- True or False: when utilizing HTTPS, all data sent across the session will appear as TLS Application data?
	- True