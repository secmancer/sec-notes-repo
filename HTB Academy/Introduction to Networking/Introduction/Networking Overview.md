#### **Networking Basics**

- **Network Functionality**:
    
    - A network connects computers, allowing them to communicate with each other.
    - Networks involve various **topologies** (e.g., mesh, tree, star), **mediums** (e.g., Ethernet, fiber, coax, wireless), and **protocols** (e.g., TCP, UDP, IPX).
- **Security Importance**:
    
    - Understanding networking is crucial for security professionals. Network failures can be silent, leading to missed detections of security breaches or misconfigurations.

#### **Flat vs. Segmented Networks**

- **Flat Network**:
    
    - A large, flat network has all devices in the same network segment, which is operationally simple but poses security risks.
    - It’s akin to securing a house with a single lock on the door, leaving the network vulnerable to attackers.
- **Segmented Network**:
    
    - Breaking down a flat network into smaller segments with Access Control Lists (ACLs) adds security layers.
    - This is like building fences around the property with specific entry/exit points, making unauthorized access more noticeable and easier to detect.

#### **Network Segmentation Examples**

1. **Access Control Lists (ACLs)**:
    
    - **Analogy**: Fencing around the property, creating specific entry/exit points.
    - **Purpose**: Restrict traffic between segments. For example, preventing a printer network from communicating with servers over HTTP.
2. **Network Documentation**:
    
    - **Analogy**: Placing lights around the property to monitor all activity.
    - **Purpose**: Ensure visibility of network traffic, such as questioning why a printer network is communicating with the internet.
3. **Intrusion Detection Systems (IDS)**:
    
    - **Analogy**: Bushes around windows deter unauthorized entry.
    - **Purpose**: IDS like Suricata or Snort can detect and deter network scans, similar to questioning why a port scan originated from a printer network.

#### **Pentesting Oversight: Understanding Subnetting**

- **Subnetting Scenario**:
    
    - Most networks use a `/24` subnet (e.g., 255.255.255.0), where devices communicate as long as the first three octets of their IP address are the same (e.g., `192.168.1.xxx`).
    - A `/25` subnet splits this range in half, limiting communication to only the devices within the same half of the range.
- **Example**:
    
    - **Server Gateway**: `10.20.0.1/25`
        
    - **Domain Controller**: `10.20.0.10/25`
        
    - **Client Gateway**: `10.20.0.129/25`
        
    - **Client Workstation**: `10.20.0.200/25`
        
    - **Pentester IP**: `10.20.0.252/24` (incorrectly set gateway to `10.20.0.1`)
        
    - The Pentester could only communicate with Client Workstations and mistakenly thought the Domain Controller was offline, missing higher-value targets due to incorrect subnetting.
        

#### **Work From Home (WFH) Networking Example**

- **High-Level Diagram**:
    - The internet comprises many subdivided networks, such as "Home Network" and "Company Network."
    - When accessing a company website from a home network, data is exchanged via the company's network.
    - The **Fully Qualified Domain Name (FQDN)** (e.g., `www.hackthebox.eu`) specifies the website's address, while the **Uniform Resource Locator (URL)** (e.g., `https://www.hackthebox.eu/example?floor=2&office=dev&employee=17`) specifies the exact location and resource on the website.

#### **Network Design Considerations**

- **Segmented Networks**:
    - A secure network design involves multiple segments, each with specific security considerations:
        1. **DMZ (Demilitarized Zone)**: For web servers exposed to the internet, separating them from the internal network.
        2. **Workstations Network**: Should be separate from servers, with host-based firewalls preventing workstation-to-workstation communication.
        3. **Administration Network**: For switches and routers, preventing workstations from snooping on administrative communications.
        4. **IP Phones Network**: To isolate voice traffic, prioritize its performance, and prevent eavesdropping.
        5. **Printers Network**: Printers should be isolated due to their vulnerabilities, preventing them from interacting with workstations or accessing the internet.

#### **Fun Story: Printer Exploit**

- **Scenario**:
    
    - During a penetration test during COVID, the tester exploited a printer by placing a reverse shell in it.
    - The printer was shipped to the client with a phishing email, tricking staff into connecting it to the network.
    - The printer captured the domain administrator's credentials, providing the tester with unauthorized access.
- **Key Takeaways**:
    
    - **Proper Network Segmentation**: Could have prevented the printer from initiating connections to workstations or accessing the internet.
    - **Security Best Practices**: Isolating printers, applying least privilege, and monitoring unusual behavior can prevent such attacks.