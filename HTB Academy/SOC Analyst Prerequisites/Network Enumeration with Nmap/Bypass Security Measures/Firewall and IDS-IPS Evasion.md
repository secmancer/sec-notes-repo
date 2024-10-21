### Nmap Firewall and IDS/IPS Evasion Techniques

#### **1. Overview**
- Nmap provides multiple methods to evade **firewalls** and **IDS/IPS** systems:
  - **Packet fragmentation**: Breaking up packets to avoid detection.
  - **Decoys**: Masking the real scan by simulating multiple source IPs.
  - **Custom scan techniques** (e.g., SYN, ACK) to bypass specific security mechanisms.

#### **2. Firewalls**
- **Function**: A firewall monitors and controls incoming/outgoing network traffic based on predefined security rules.
- **Packet handling**: 
  - Firewalls decide whether to **pass**, **ignore** (drop), or **block** (reject) packets.
  - **Dropped packets**: No response is sent back (host silently ignores the packet).
  - **Rejected packets**: Returned with an **RST flag** or **ICMP error codes**.
  
  Common ICMP error codes:
  - **Net Unreachable**
  - **Net Prohibited**
  - **Host Unreachable**
  - **Host Prohibited**
  - **Port Unreachable**
  - **Protocol Unreachable**

#### **3. IDS/IPS (Intrusion Detection and Prevention Systems)**
- **IDS**: Monitors the network for potential attacks, analyzing and reporting suspicious activities.
- **IPS**: Acts after detection, preventing the attack by blocking or mitigating the potential threat.
  - IDS/IPS typically rely on **pattern matching** or **signature detection**.
  - Example: If an IDS detects a port scan, an IPS might block further scanning attempts.

#### **4. TCP ACK Scans for Firewall and IDS/IPS Evasion**
- **TCP ACK scans (-sA)** are more difficult for firewalls and IDS/IPS to filter compared to **SYN scans (-sS)** or **Connect scans (-sT)**.
  - **SYN scan (-sS)**: Sends a packet with a SYN flag to initiate a connection. Firewalls typically block these.
  - **ACK scan (-sA)**: Sends only an ACK flag, simulating part of an established connection, making it harder for firewalls to detect.
  
  **Why ACK Scans Work**:
  - **Firewalls** usually block incoming **SYN** flags from external networks, but **ACK** flags are often passed through since they appear to be part of an already established connection.
  - The response to an ACK scan reveals whether a port is **filtered** (no response) or **unfiltered** (RST response).

#### **5. Example Scans and Results**

- **SYN Scan Example (-sS)**:
  - Command: `sudo nmap 10.129.2.28 -p 21,22,25 -sS -Pn -n --disable-arp-ping --packet-trace`
  - Results:
    - **Port 21 (FTP)**: Filtered (no response).
    - **Port 22 (SSH)**: Open (SYN-ACK response).
    - **Port 25 (SMTP)**: Filtered (no response).
  - Explanation: The firewall or IDS/IPS allows the connection to **port 22** but blocks **ports 21 and 25**.

- **ACK Scan Example (-sA)**:
  - Command: `sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace`
  - Results:
    - **Port 21 (FTP)**: Filtered (no response).
    - **Port 22 (SSH)**: Unfiltered (RST response).
    - **Port 25 (SMTP)**: Filtered (no response).
  - Explanation: The **ACK scan** shows **port 22** is **unfiltered** (RST flag), while **ports 21 and 25** are filtered, meaning the firewall is blocking them.

#### **6. Key Nmap Scan Options for Evasion**
| **Option**                  | **Description**                                                     |
|-----------------------------|---------------------------------------------------------------------|
| `-sS`                       | Performs a **SYN scan**.                                            |
| `-sA`                       | Performs an **ACK scan**.                                           |
| `-Pn`                       | Disables ICMP Echo requests (ping), useful for avoiding ping blocks.|
| `-n`                        | Disables DNS resolution, increasing speed and avoiding DNS detection.|
| `--disable-arp-ping`        | Disables ARP ping (useful for evading network discovery mechanisms).|
| `--packet-trace`            | Displays all packets sent and received during the scan.             |

#### **7. SYN vs ACK Scan Results**
- **SYN Scan (-sS)**:
  - Detects whether a port is **open** (SYN-ACK) or **filtered** (no response).
- **ACK Scan (-sA)**:
  - Useful for determining whether a port is **filtered** or **unfiltered** (based on RST response).

#### **8. Summary of Scan Responses**
- **SYN Scan (-sS)**: Firewall attempts to establish a connection if port is open, sending **SYN-ACK**.
- **ACK Scan (-sA)**: Host responds with **RST** if the port is unfiltered, indicating the port's state (open/closed).

#### **9. Additional Considerations**
- Use **ACK scans** for stealthy detection in environments with firewalls and IDS/IPS.
- SYN scans are more direct but may trigger IDS/IPS alarms if firewalls are in place.
  
### Nmap Techniques to Detect IDS/IPS

#### **1. IDS (Intrusion Detection System)**
- **Purpose**: Monitors traffic and alerts administrators to potential attacks.
- **Function**: **Passive** monitoring of network connections for suspicious patterns (e.g., port scans, unusual traffic).
- **Action**: The administrator decides how to respond (e.g., block IPs or take manual action).

#### **2. IPS (Intrusion Prevention System)**
- **Purpose**: Works alongside IDS, but actively **prevents attacks** by taking automated actions.
- **Function**: **Active** security system that blocks or restricts traffic deemed suspicious, based on predefined rules.

#### **3. Challenges in Detecting IDS/IPS**
- Detection of IDS/IPS is difficult because these systems **passively monitor** network traffic.
- When IDS/IPS detects suspicious activity, such as an aggressive scan, the administrator may block the IP address or take defensive measures.
  
#### **4. Methods to Detect IDS/IPS Presence**
1. **Single Host Scan**: 
   - Use a **single VPS** to scan the target network.
   - If the VPS IP is **blocked** after scanning, this indicates potential IDS/IPS action.
   - Continue scanning with a different VPS if the initial host is blocked.

2. **Aggressive Scanning of a Specific Port**:
   - If the network reacts to aggressive scanning (e.g., by blocking the IP), it may have **IDS/IPS protection**.
   - Test different scan techniques to gauge how the network responds.

#### **5. Decoy Scans**
- **Purpose**: Mask the true origin of the scan by using **decoy IP addresses**.
- **How it works**:
  - Nmap inserts random **decoy IPs** in the packet headers.
  - The real IP address is hidden among the decoys, making it harder for the IDS/IPS to trace the actual attacker.
  - **Important**: The decoy IPs must be active (alive), or the target may block the request due to **SYN-flooding** prevention mechanisms.
  
- **Example Command**: `nmap -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5`
  - **-D RND:5**: Generates 5 random decoy IP addresses.
  
#### **6. Testing Firewall Rules with Decoys**
- **Goal**: Test if firewalls or IDS/IPS systems block specific subnets or regions.
- Use the **-S** option to specify a source IP address manually.
- Example command:
  - `nmap -n -Pn -p 445 -O -S 10.129.2.200 -e tun0`
  - **-S**: Scans using a different source IP.
  - **-e tun0**: Sends requests through a specified network interface.

#### **7. DNS Proxying for Evasion**
- By default, Nmap performs **reverse DNS resolution**. DNS queries often pass through firewalls.
- Use Nmap’s **--dns-server** option to specify trusted DNS servers, especially useful when scanning from within a **DMZ** (Demilitarized Zone).
- You can also use **TCP port 53** as a source port to evade certain IDS/IPS filtering mechanisms.
  
- **Example**:  
  - Use **--source-port 53** to scan from a DNS port that may be trusted by firewalls.
  - Command: `nmap -p 50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53`
  - This technique can exploit weaker IDS/IPS configurations for trusted ports.

#### **8. SYN Scans from Filtered Ports**
- Scanning through a **filtered port** helps determine how strict the firewall is.
- If SYN packets from a trusted port like **port 53** (DNS) bypass the firewall, the system may trust traffic from that port.
  
- **Example**:
  - `nmap -p50000 -sS -Pn -n --disable-arp-ping --packet-trace`
  - A SYN scan with **port 53** as the source port may trick the firewall into allowing the connection.

#### **9. Detecting and Bypassing Firewall Rules**
- If a port appears filtered, using different source IPs or trusted ports may yield better results.
- IDS/IPS may not filter traffic from **trusted ports** like DNS (port 53), allowing for evasion.

#### **10. Key Nmap Options for IDS/IPS Detection and Evasion**
| **Option**                  | **Description**                                             |
|-----------------------------|-------------------------------------------------------------|
| `-D RND:5`                  | Generates 5 random decoy IP addresses to hide the real IP.  |
| `-S <IP>`                   | Sets a different source IP address.                         |
| `--source-port <port>`       | Sends traffic through a trusted port (e.g., port 53 for DNS).|
| `--dns-server <ns>`          | Specifies DNS servers for reverse DNS resolution.           |
| `-e <interface>`             | Uses the specified network interface (e.g., `tun0`).        |

#### **11. Firewall and IDS/IPS Detection Workflow**
1. **Initial Scan**: Conduct an initial scan with a single VPS to gauge the target’s defenses.
2. **Detection**: If your IP is blocked, switch to a new VPS or use decoys to hide your identity.
3. **Evasion Techniques**:
   - Use decoy IPs or change source IP addresses.
   - Use trusted ports like **port 53** to bypass IDS/IPS filtering.
   - Use **DNS proxying** to route queries through trusted DNS servers.
4. **Quiet Scanning**: Avoid aggressive scans; keep interactions as stealthy as possible to avoid detection.

#### **12. Practical Example - SYN Scan from DNS Port**
- **Scenario**: Scanning a filtered port (50000) from **port 53** to evade detection.
- **Command**:  
  - `nmap -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53`
  - The scan succeeded because **port 53** is trusted by the target's firewall.

For more details on IDS/IPS evasion techniques, refer to [Nmap Evasion Documentation](https://nmap.org).