### HTTP
- Hypertext Transfer Protocol (`HTTP`): stateless Application Layer protocol that has been in use since 1990. 
	- Enables the transfer of clear text data between a client and server over TCP. 
- The client would send an HTTP request to the server, asking for a resource.
- A session is established, and the server responds with the requested media, like a HTML page, images, hyperlinks, or video file. 
- Utilizes ports 80 or 8000 over TCP during normal operations, but could use alternate ports or even UDP in some case.



### HTTP Methods
- To do various operations, we have several methods available with HTTP, some being either `required` or `optional`.
- Required methods include GET and HEAD, while every other method are only optional implementations.
- This can be useful in many applications. For example, if we can allow a client to get a resource, but not able to modify, add, or delete anything from the server.
- A table of HTTP methods is shown below.
- For more information on HTTP as a protocol or how it operates, see `RFC:2616`.

| **Method** | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `HEAD`     | `required` is a safe method that requests a response from the server similar to a Get request except that the message body is not included. It is a great way to acquire more information about the server and its operational status.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `GET`      | `required` Get is the most common method used. It requests information and content from the server. For example, `GET http://10.1.1.1/Webserver/index.html` requests the index.html page from the server based on our supplied URI.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `POST`     | `optional` Post is a way to submit information to a server based on the fields in the request. For example, submitting a message to a Facebook post or website forum is a POST action. The actual action taken can vary based on the server, and we should pay attention to the response codes sent back to validate the action.                                                                                                                                                                                                                                                                                                                                          |
| `PUT`      | `optional` Put will take the data appended to the message and place it under the requested URI. If an item does not exist there already, it will create one with the supplied data. If an object already exists, the new PUT will be considered the most up-to-date, and the object will be modified to match. The easiest way to visualize the differences between PUT and POST is to think of it like this; PUT will create or update an object at the URI supplied, while POST will create child entities at the provided URI. The action taken can be compared with the difference between creating a new file vs. writing comments about that file on the same page. |
| `DELETE`   | `optional` Delete does as the name implies. It will remove the object at the given URI.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `TRACE`    | `optional` Allows for remote server diagnosis. The remote server will echo the same request that was sent in its response if the TRACE method is enabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `OPTIONS`  | `optional` The Options method can gather information on the supported HTTP methods the server recognizes. This way, we can determine the requirements for interacting with a specific resource or server without actually requesting data or objects from it.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `CONNECT`  | `optional` Connect is reserved for use with Proxies or other security devices like firewalls. Connect allows for tunneling over HTTP. (`SSL tunnels`)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |


### HTTPS
- HTTP Secure (`HTTPS`): modification of HTTP to where it uses the Transport Layer Security (`TLS`) or Secure Sockets Layer (`SSL`) for data security.
- TLS is used to encrypt the communications from the client to the server.
	- Can wrap regular HTTP traffic within TLS to allow encryption of our entire conversation.
	- Otherwise, we will be vulnerable to attacks like Man-in-the-Middle or other reconnaissance/hijacking attempts
-  Allows for security for applications like search engines, bank applications, and others.
- HTTPS uses ports 443 and 8443



### TLS Handshake Via HTTPS
- The client initiates a session with the server on port 443, signaling the use of HTTPS.
- A TLS ClientHello is sent to begin the TLS handshake after the TCP session is established.
- The TLS handshake involves agreeing on parameters like session identifier, certificates, compression algorithm, cipher spec, session resumability, and a shared 48-byte master secret.
- After the handshake, all communication occurs over the secured TLS connection, with data appearing as TLS Application Data.
- The TLS handshake steps:
    1. Exchange hello messages to agree on connection parameters.
    2. Exchange cryptographic parameters for a premaster secret.
    3. Exchange x.509 certificates for authentication.
    4. Generate a master secret and security parameters.
    5. Apply negotiated parameters to the TLS record layer.
    6. Verify handshake integrity to ensure no tampering.
- HTTPS secures communication using HTTP over TLS. For detailed specifications, refer to RFC:2246.
![image](https://academy.hackthebox.com/storage/modules/81/https.png)




### FTP
- File Transfer Protocol (`FTP`): Application Layer protocol enabling quick data transfer between devices
	- Utilized as a CLI tool, web browser, or a GUI tool like FileZilla.
- Insecure protocol, so most use more secure protocols like SFTP to do the same functions.
	- Most browsers have phased out support for FTP as of 2020 anyways.
- Unique protocol as it uses multiple ports at a time, rather than a single link.
	- Uses TCP ports 20 and 21.
	- Port 20: data transfer
	- Port 21: issuing commands controlling the session
- Supports user authentication, along with anonymous access if configured to.
- Runs in one of two modes: `active` or `passive`.
	- **Active**: default mode
		- Server listens for a control command port from the client, containing what port to use for data transfer
	- **Passive**: selectable mode
		- Enables for access to FTP servers located behind firewalls
		- Can also allow for a NAT-enabled link to make direct TCP connections impossible.



### FTP Command & Response Example
![image](https://academy.hackthebox.com/storage/modules/81/ftp-example.png)
- The image above shows several examples of requests issued over the FTP command channel `green arrows`, and the responses sent back from the FTP server `blue arrows`. This is all pretty standard stuff. For a list of each command and what it is doing, check out the table below.




### FTP Commands
- This is not an exhaustive list of the possible FTP control commands that could be seen. These can vary based on the FTP application or shell in use. For more information on FTP, see `RFC:959`.

| **Command** | **Description** |
| --- | --- |
| `USER` | specifies the user to log in as. |
| `PASS` | sends the password for the user attempting to log in. |
| `PORT` | when in active mode, this will change the data port used. |
| `PASV` | switches the connection to the server from active mode to passive. |
| `LIST` | displays a list of the files in the current directory. |
| `CWD` | will change the current working directory to one specified. |
| `PWD` | prints out the directory you are currently working in. |
| `SIZE` | will return the size of a file specified. |
| `RETR` | retrieves the file from the FTP server. |
| `QUIT` | ends the session. |





### SMB
- Server Message Block (`SMB`): protocol most seen in Windows enterprise environments.
	- Enables sharing resources between hosts over common networking architectures. 
	- Connection-oriented protocol that requires user authentication from the host to the resource.
	- This ensures the user has correct permissions to use that resource or perform actions. 
	- Previously, SMB utilized NetBIOS as its transport mechanism over UDP ports 137 and 138.
	- With modern changes, SMB now supports direct TCP transport over port 445, NetBIOS over TCP port 139, and even the QUIC protocol.
- As a user, SMB provides us easy and convenient access to resources like printers, shared drives, authentication servers, and more.
- This makes it very attractive to potential attackers as well.
- Like any other application that uses TCP as its transport mechanism, it will perform standard functions like the three-way handshake and acknowledging received packets.
- #### SMB On The Wire
![image](https://academy.hackthebox.com/storage/modules/81/smb-actions.png)
- **TCP Handshake**
    - Observes a TCP handshake occurring each time a session is established (_orange boxes_).
- **Source and Destination Ports**
    - Port 445 is utilized, indicating **SMB traffic over TCP** (_blue box_).
- **SMB Communication Details**
    - The info field (_green boxes_) reveals the nature of SMB communication.
    - Example: **Many errors** in the SMB communication, which warrant deeper investigation.
- **Authentication Failures**
    - **Normal behavior**: One or two auth failures from a user.
    - **Anomalous behavior**: Clusters of repeated auth failures may signal:
        - Unauthorized access attempts.
        - Possible credential theft by attackers.
- **Attacker Tactics**
    - Use stolen credentials to:
        - Move laterally within the network.
        - Access resources typically denied to the user.
- **SMB Use Cases**
    - Common: File-share access between servers and hosts.
    - **Unusual Behavior**:
        - A host accessing file shares on other hosts.
        - Requires attention to **who** is requesting connections, **where**, and **what actions** are performed.