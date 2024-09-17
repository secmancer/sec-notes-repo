#### HTTP (Hypertext Transfer Protocol)
- **Overview**: A stateless Application Layer protocol used since 1990.
- **Function**: Transfers data in clear text between a client and server over TCP.
- **Ports**: Typically uses ports 80 or 8000. Can be modified to use other ports or even UDP.



#### HTTP Methods
- **HEAD**: Requests a response similar to GET but without the message body. Useful for acquiring server information.
- **GET**: Requests information and content from the server (e.g., `GET http://example.com/index.html`)
- **POST**: Submits information to a server (e.g., form submissions). Action varies based on server response codes.
- **PUT**: Creates or updates an object at a given URI. New data replaces existing data.
- **DELETE**: Removes the object at the specified URI.
- **TRACE**: For remote server diagnosis; echoes the same request sent.
- **OPTIONS**: Gathers information on supported HTTP methods of the server.
- **CONNECT**: Used for tunneling over HTTP, often with proxies or firewalls (e.g., SSL tunnels).
- **Required Methods**: GET and HEAD must always be supported.
- **Optional Methods**: TRACE, OPTIONS, DELETE, PUT, and POST are optional.


#### HTTPS (HTTP Secure)
- **Overview**: An extension of HTTP that uses TLS/SSL for secure communications.
- **Ports**: Uses ports 443 and 8443 instead of the standard port 80.
- **Function**: Encrypts data to prevent Man-in-the-Middle attacks and ensures data security.



#### TLS Handshake via HTTPS
1. **Client and Server Hello**: Exchange initial hello messages to agree on parameters.
2. **Cryptographic Parameters**: Exchange cryptographic information to establish a premaster secret.
3. **Certificates**: Exchange x.509 certificates for authentication.
4. **Master Secret**: Generate a master secret from the premaster secret and random values.
5. **Security Parameters**: Issue negotiated security parameters.
6. **Verification**: Ensure the handshake occurred without tampering.


#### FTP (File Transfer Protocol)
- **Overview**: Application Layer protocol for data transfer between devices.
- **Ports**: Uses ports 20 for data transfer and 21 for command control.
- **Modes**:
    - **Active Mode**: Server listens for data port connection from the client.
    - **Passive Mode**: Client requests a port from the server for data transfer, useful for firewalls/NATs.



#### FTP Commands
- **USER**: Specifies the user to log in as.
- **PASS**: Sends the password for the user.
- **PORT**: Changes the data port used (active mode).
- **PASV**: Switches to passive mode.
- **LIST**: Displays files in the current directory.
- **CWD**: Changes the working directory.
- **PWD**: Prints the current directory.
- **SIZE**: Returns the size of a specified file.
- **RETR**: Retrieves a file from the server.
- **QUIT**: Ends the session.



#### SMB (Server Message Block)
- **Overview**: Protocol for sharing resources (e.g., printers, files) over networks.
- **Ports**: Traditionally uses ports 137, 138 (NetBIOS over UDP), 139 (NetBIOS over TCP), and 445 (direct TCP transport).
- **Connection**: Requires user authentication and performs standard TCP functions like three-way handshake.



#### SMB Traffic Analysis
- **TCP Handshake**: Each SMB session starts with a TCP handshake.
- **Port Usage**: Typically utilizes port 445 for SMB traffic.
- **Common Issues**: Multiple authentication failures can indicate unauthorized access attempts.


### References
- **HTTP**: RFC 2616
- **HTTPS**: RFC 2246
- **FTP**: RFC 959


## Questions
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