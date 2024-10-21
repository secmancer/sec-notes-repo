### Nmap Scanning Overview
**Purpose**: Understanding the functionality and performance of Nmap is crucial for effective scanning and interpretation of results.

#### Objectives:
- Identify if the target is alive.
- Gather detailed information about the system, including:
  - Open ports and associated services
  - Service versions
  - Information provided by services
  - Operating system

### Port States
Nmap can report six different states for scanned ports:

| State            | Description                                                                                                         |
|------------------|---------------------------------------------------------------------------------------------------------------------|
| **open**         | Connection to the scanned port established (TCP, UDP, or SCTP).                                                  |
| **closed**       | RST flag received; indicates the port is closed. This method also checks if the target is alive.                  |
| **filtered**     | Nmap cannot determine if the port is open or closed due to lack of response or error code from the target.        |
| **unfiltered**   | Port is accessible, but its state (open or closed) cannot be determined; occurs during TCP-ACK scans.            |
| **open|filtered** | No response received; indicates a firewall or packet filter may be protecting the port.                            |
| **closed|filtered**| Indicates that it was impossible to determine if the port is closed or filtered; occurs in IP ID idle scans.     |

### Discovering Open TCP Ports
- **Default Behavior**: Nmap scans the top 1000 TCP ports using SYN scan (-sS) when run as root. Otherwise, it uses TCP connect scan (-sT).
- **Port Scanning Options**:
  - Individual ports: `-p 22,25,80,139,445`
  - Port range: `-p 22-445`
  - Top ports: `--top-ports=10`
  - All ports: `-p -`
  - Fast scan: `-F`

#### Example of Scanning Top 10 TCP Ports
```bash
sudo nmap 10.129.2.28 --top-ports=10
```
- **Output Example**:
  ```
  PORT     STATE    SERVICE
  21/tcp   closed   ftp
  22/tcp   open     ssh
  23/tcp   closed   telnet
  25/tcp   open     smtp
  80/tcp   open     http
  110/tcp  open     pop3
  139/tcp  filtered netbios-ssn
  443/tcp  closed   https
  445/tcp  filtered microsoft-ds
  3389/tcp closed   ms-wbt-server
  ```

### Packet Tracing with Nmap
To view packet transmission, disable ICMP, DNS resolution, and ARP ping:

```bash
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```
- **SENT**: Shows packets sent to the target.
- **RCVD**: Shows packets received from the target.

### Connect Scan
- **Method**: Uses TCP three-way handshake to check port status.
- **Characteristics**:
  - Highly accurate but not stealthy.
  - Logs connections, making it easily detectable by IDS/IPS.
  - Useful when the target host has a firewall allowing outgoing packets.
- **Example Command**:
```bash
sudo nmap 10.129.2.28 -p 443 --packet-trace --disable-arp-ping -Pn -n --reason -sT
```
- **Output Example**:
  ```
  PORT    STATE SERVICE REASON
  443/tcp open  https   syn-ack
  ```

### Filtered Ports
- A filtered port indicates the target is blocking packets (often due to firewall rules).
- When a packet is dropped, Nmap waits and retries by default (10 retries).

#### Example of Scanning a Filtered Port
```bash
sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn
```
- **Output Example**:
  ```
  PORT    STATE    SERVICE
  139/tcp filtered netbios-ssn
  ```

## Questions
- Find all TCP ports on your target. Submit the total number of found TCP ports as the answer.
	- 7
- Enumerate the hostname of your target and submit it as the answer. (case-sensitive)
	- NIX-NMAP-DEFAULT