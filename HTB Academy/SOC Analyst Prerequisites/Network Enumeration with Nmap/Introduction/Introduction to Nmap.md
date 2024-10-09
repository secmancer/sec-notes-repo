### Nmap Overview
- **Definition**: Nmap (Network Mapper) is an open-source network analysis and security auditing tool written in C, C++, Python, and Lua.
- **Purpose**: It scans networks to identify available hosts, services, applications (including names and versions), and operating systems.


### Features
- **Security Auditing**: Evaluates security aspects of networks.
- **Penetration Testing**: Simulates attacks to test defenses.
- **Firewall and IDS Checking**: Assesses configurations of firewalls and intrusion detection systems.
- **Network Mapping**: Creates a map of network connections.
- **Response Analysis**: Evaluates how the network responds to different types of scans.
- **Open Ports Identification**: Identifies which ports are open on target hosts.
- **Vulnerability Assessment**: Assists in identifying vulnerabilities within the network.


### Nmap Architecture
- **Scan Types**: Nmap supports various scanning techniques, including:
    - Host discovery
    - Port scanning
    - Service enumeration and detection
    - OS detection
    - Scriptable interaction via the Nmap Scripting Engine (NSE)


### Syntax
- **Basic Command Structure**:
```
nmap <scan types> <options> <target>
```


### Scan Techniques
- **Types of Scans**: Nmap offers several scanning techniques:
    - **TCP Scans**:
        - `-sS`: TCP SYN scan (default)
        - `-sT`: TCP Connect scan
        - `-sA`: TCP ACK scan
        - `-sW`: TCP Window scan
        - `-sM`: TCP Maimon scan
    - **UDP Scan**:
        - `-sU`: UDP scan
    - **Null, FIN, and Xmas Scans**:
        - `-sN`: TCP Null scan
        - `-sF`: TCP FIN scan
        - `-sX`: TCP Xmas scan
    - **Idle Scan**:
        - `-sI <zombie host[:probeport]`: Idle scan
    - **SCTP Scans**:
        - `-sY`: SCTP INIT scan
        - `-sZ`: SCTP COOKIE-ECHO scan
    - **IP Protocol Scan**:
        - `-sO`: IP protocol scan
    - **FTP Bounce Scan**:
        - `-b <FTP relay host>`: FTP bounce scan


### TCP-SYN Scan Example
- **Description**: The TCP-SYN scan sends a packet with the SYN flag to scan ports without completing the TCP handshake.
    - **Responses**:
        - SYN-ACK: Port is open.
        - RST: Port is closed.
        - No response: Port is filtered (could be blocked by a firewall).


#### Example Command
- **Command**:
```
sudo nmap -sS localhost
```
- **Output**:
```
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-11 22:50 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000010s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
5432/tcp open  postgresql
5901/tcp open  vnc-1

Nmap done: 1 IP address (1 host up) scanned in 0.18 seconds
```
- **Interpretation**: The output indicates four open TCP ports (22, 80, 5432, 5901) along with their respective services.