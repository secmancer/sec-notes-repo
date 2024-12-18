### Introduction
- A **network** allows two computers to communicate and can involve various **topologies** (mesh, tree, star), **mediums** (ethernet, fiber, coax, wireless), and **protocols** (TCP, UDP, IPX).
- Understanding networking is crucial for security professionals because network failures can be silent, leading to missed issues.
- **Flat networks** are simple to set up but lack security. They are like a house with just a lock on the door. By breaking networks into smaller segments and controlling communication, we add security layers, slowing down attackers.
    - **Example No. 1:** Creating smaller networks and using **Access Control Lists (ACLs)** is like putting a fence around a property with controlled entry points, making suspicious activity easy to spot.
    - **Example No. 2:** Mapping and documenting each network's purpose is like placing lights around a property to spot unusual activity, such as a printer talking to the internet.
    - **Example No. 3:** Using **Intrusion Detection Systems (IDS)** like Suricata or Snort is like having bushes around windows to deter intruders, helping detect unauthorized activities like port scans originating from unusual sources.
- While these ideas may seem obvious, implementing them is challenging in a **flat /24 network** where devices like printers may easily communicate in ways that are difficult to monitor or restrict.



### Story Time - A Pentesters Oversight
- **/24 subnets** are commonly used in networks, allowing communication between devices that share the first three octets of their IP addresses (e.g., 192.168.1.xxx).
- Changing the subnet mask to **/25** divides the network into two halves, restricting devices to communicate only within their half of the network (e.g., 10.20.0.1/25 and 10.20.0.129/25).
- A **Penetration Tester** (Pentester) may mistakenly assume a **Domain Controller** is offline if it's on a different subnet, leading to confusion. For example:
    - Server Gateway: 10.20.0.1/25
    - Domain Controller: 10.20.0.10/25
    - Client Gateway: 10.20.0.129/25
    - Client Workstation: 10.20.0.200/25
    - Pentester IP: 10.20.0.252/24 (Set Gateway to 10.20.0.1)
- In this case, the Pentester may only access the **Client Network** (e.g., stealing passwords from workstations) without reaching higher-value targets like database servers due to lack of understanding about the subnet.



### Basic Information
- Let us look at the following high-level diagram of how a Work From Home setup may work.
![[net_overview_png.png]]
- **The internet** is composed of many subdivided networks, such as the `Home Network` and `Company Network`. This can be compared to sending packages or mail between two locations.
- When visiting a company’s website from the `Home Network`, data is exchanged with the website on the `Company Network`. The website address entered in the browser is a **URL** (Uniform Resource Locator) or **FQDN** (Fully Qualified Domain Name).
- The difference between **URL** and **FQDN**:
    - **FQDN** (e.g., `www.hackthebox.eu`) specifies the address of the "building."
    - **URL** (e.g., `https://www.hackthebox.eu/example?floor=2&office=dev&employee=17`) specifies the "floor," "office," "mailbox," and the recipient.
- We know the **address** (FQDN), but not the **exact location**. The **post office** (the router) determines the correct route to forward the packet.
- The **router** in the `Home Network` forwards the packet to the **main post office** (the ISP), which checks the **Domain Name Service (DNS)** to get the exact **IP address** of the destination.
- The packet is sent to the web server, which responds with data for the website and sends it back through the ISP and the `Home Network` router to the user’s IP address.



### Extra Points
- **Company Network Design** should consist of multiple separate networks for better security and management:
    1. **Web Server in a DMZ**: The web server should be placed in a **Demilitarized Zone (DMZ)** to protect it from direct internal network access, reducing the risk of compromise. This zone allows for stronger network protections between the server and other internal devices.
    2. **Workstations on Separate Network**: Workstations should be isolated from each other on different networks. Ideally, **Host-Based Firewall** rules should prevent workstations from communicating with each other to avoid risks like **spoofing** or **man-in-the-middle** attacks when connected to servers.
    3. **Switch and Router on Administration Network**: The switch and router should be placed on a dedicated **Administration Network** to prevent unauthorized monitoring and attacks. This configuration helps avoid **man-in-the-middle** attacks via malicious **OSPF** advertisements on the internal network.
    4. **IP Phones on Separate Network**: **IP Phones** should have their own network to prevent eavesdropping and allow administrators to prioritize traffic for low-latency communications, ensuring high-quality voice calls without delays.
    5. **Printers on Separate Network**: **Printers** should be isolated in their own network due to security risks, such as **NTLMv2** authentication that can expose passwords, and because printers store sensitive data. Keeping them isolated prevents exploitation and enhances security.



### Fun Story
- The scenario highlights the importance of designing secure network architectures and implementing proper segmentation to prevent attacks. In this case, the attack was successful due to several network security shortcomings. If the client had followed best practices for network security, this attack might have been prevented. Here are the key lessons:
	1. **Printer Should Be Isolated from the Internet**: Printers should not have direct access to the internet, as they can be vulnerable to exploitation. Placing printers on isolated, segmented networks would reduce their exposure to external threats.
	2. **Workstations Should Not Have Direct Access to Printers Over Port 445**: Port 445, commonly used for Windows file-sharing (SMB), should not be accessible from workstations to printers or any devices that do not require it. This would prevent remote exploitation of vulnerabilities like those associated with SMB.
	3. **Prevent Printers from Initiating Connections to Workstations**: Printers should not have the ability to initiate connections to workstations. This helps prevent the device from acting as a pivot point for attacks or from harvesting credentials. Instead, workstations should initiate communication with printers in a controlled manner.
	4. **Secure Communications for Printer/Scanner Devices**: In some cases, printers or multi-functional devices that need to communicate with a mail server (for scanning documents) should be restricted to only the necessary services and ports. These devices should not have unnecessary network access or the ability to communicate with other sensitive internal systems.
- By segmenting networks, implementing firewalls, and configuring devices with the principle of least privilege, organizations can limit the opportunities for attackers to exploit vulnerabilities in devices like printers, ensuring better overall network security.