**Overview**
- **Network Basics**: A network allows two computers to communicate. Understanding networks is crucial for security professionals because network failures can be silent and easily missed.



**Network Elements**
- **Topologies**: Mesh, tree, star
- **Mediums**: Ethernet, fiber, coaxial, wireless
- **Protocols**: TCP, UDP, IPX



**Network Design Considerations**
- **Flat Network**: Easy to set up and operationally reliable but lacks security. It's similar to a house with just a lock on the door—secure only in the simplest sense.
- **Segmented Network**: Adding layers of defense by creating smaller networks and managing their communication. This approach increases security, making it harder for attackers to move quickly and silently across the network.



**Examples of Network Segmentation**
1. **Access Control Lists (ACLs)**:
    - **Analogy**: Like placing a fence around a property with specific entry and exit points.
    - **Purpose**: Detect suspicious activity. Example: Why is the printer network communicating with the servers over HTTP?
2. **Network Documentation**:
    - **Analogy**: Like placing lights around the property to monitor all activity.
    - **Purpose**: Ensure visibility and detect unusual behavior. Example: Why is the printer network accessing the internet?
3. **Intrusion Detection Systems (IDS)**:
    - **Analogy**: Like having bushes around windows to deter unauthorized access.
    - **Purpose**: Detect network scans and other malicious activities. Example: Why is there a port scan originating from the printer network?



**Challenges in Flat Networks**
- **Restrictions**: Implementing security measures like ACLs and IDS can be difficult in a flat network, where devices like printers are given broad access through DHCP.



**Story Time - Pentester's Oversight**
- **Subnet Mask Issue**: Many penetration testers use a /24 subnet mask (255.255.255.0) without checking. This allows communication between devices with the same first three octets of the IP address (e.g., 192.168.1.xxx).
- **Subnetting Example**:
    - **/25 Subnet Mask**: Divides the network into two halves, restricting communication to devices on the same half.
    - **Scenario**:
        - Server Gateway: 10.20.0.1/25
        - Domain Controller: 10.20.0.10/25
        - Client Gateway: 10.20.0.129/25
        - Client Workstation: 10.20.0.200/25
        - Pentester IP: 10.20.0.252/24 (with gateway set to 10.20.0.1)
    - **Mistake**: The pentester, with a /24 subnet, was unable to reach high-value targets on a different /25 subnet. They could only access the client network and missed higher-value targets like database servers due to a lack of understanding of subnetting.




**Basic Network Communication**
- **Work From Home Setup**: Illustrates communication between a "Home Network" and a "Company Network."
- **Networking Analogy**: Similar to sending mail or packages:
    - **FQDN (Fully Qualified Domain Name)**: Specifies the exact address of a website (e.g., `www.hackthebox.eu`).
    - **URL (Uniform Resource Locator)**: Specifies more detailed address components (e.g., `https://www.hackthebox.eu/example?floor=2&office=dev&employee=17`).



**Network Communication Process**
1. **Address Resolution**:
    - The **router** (post office) sends packets to the **ISP** (main post office).
    - **ISP** uses DNS (address register) to resolve the IP address.
    - **Packet Routing**: Packet is forwarded to the destination using its IP address.
2. **Response**:
    - The web server sends back the requested data to the **router** of the "Company Network."
    - The router then delivers the data to the original sender (home network).


![[Screenshot_20240916_095209.png]]


**Network Security Layers**
- **DMZ (Demilitarized Zone)**:
    - **Purpose**: Isolate public-facing services (e.g., web servers) from internal networks.
    - **Benefit**: Adds a layer of protection between the web server and internal systems.
- **Workstations**:
    - **Separate Network**: Helps prevent attacks like spoofing or man-in-the-middle if they are on a separate network from servers.
    - **Host-Based Firewalls**: Ideally should prevent workstation-to-workstation communication.
- **Administration Network**:
    - **Purpose**: Isolate critical network infrastructure like switches and routers from regular workstations.
    - **Security**: Prevents unauthorized access and eavesdropping on administrative communications.
- **IP Phones**:
    - **Separate Network**: Ensures voice traffic is prioritized and isolated to reduce latency.
    - **Security**: Prevents unauthorized access and eavesdropping.
- **Printers**:
    - **Separate Network**: Difficult to secure due to potential vulnerabilities.
    - **Security Issues**: Printers can be targets for attacks and may expose sensitive information.



**Fun Story - Physical Penetration Test**
- **Scenario**:
    - A printer was used as a vector for a remote access attack.
    - Exploited printer shipped to a company during COVID.
    - The printer was connected, and the domain administrator's credentials were compromised.

**Lessons Learned**
1. **Secure Printers**:
    - **Prevent Internet Access**: Printers should not communicate with external networks.
    - **Restrict Communication**: Limit access between workstations and printers.
    - **Control Initiation of Connections**: Printers should not initiate connections to workstations.
2. **Network Design**:
    - Proper segmentation and security controls could prevent similar attacks.
    - Implementing a layered security approach can significantly enhance network defenses.