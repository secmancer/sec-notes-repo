- **Purpose:** Refresher on networking concepts and standard protocols encountered during traffic captures.
- **Importance:**
    - Essential for capturing and analyzing network traffic effectively.
    - A strong understanding of network flow, ports, and protocols is critical for accurate traffic analysis.
- **Recommendation:**
    - If unfamiliar with terms or concepts, complete the _Introduction to Networking_ module for foundational knowledge.


![[Screenshot_20240917_100539.png]]

**Purpose:** Compare the OSI model and TCP/IP model, which represent how communication between networked computers is handled.



#### **Model Traits Comparison:**

|Trait|OSI|TCP/IP|
|---|---|---|
|**Layers**|Seven|Four|
|**Flexibility**|Strict|Loose|
|**Dependency**|Protocol-independent & generic|Based on common communication protocols|


#### **Key Observations:**
- **Segmentation:**
    - OSI model has more layers, dividing functions into smaller chunks.
    - TCP/IP model is more blended with fewer layers.
- **Layer Functions:**
    - **OSI Layers 1-4:** Focus on data transport between hosts, including physical transmission and protocol management.
    - **OSI Layers 5-7:** Handle the interpretation, management, and presentation of data to the end-user.
    - **TCP/IP Layer 4:** Covers OSI layers 5-7.
    - **TCP/IP Layer 3:** Handles transport (like OSI layer 4).
    - **TCP/IP Layer 2 (Internet Layer):** Aligns with OSI’s network layer (Layer 3).
    - **TCP/IP Layer 1 (Link Layer):** Covers OSI layers 1 and 2.


#### **Protocol Data Unit (PDU):**
- **PDU**: A data packet containing control information and encapsulated data from each layer.
- Understanding PDUs in both models is crucial for analyzing traffic in theory and practice.

![[Screenshot_20240917_101015.png]]

**Encapsulation Concept:**
- As data moves down the protocol stack, each layer encapsulates the data from the previous layer by wrapping it in a new "bubble."
- This process involves adding a header with essential information specific to that layer.



**Information in the Encapsulation Header:**
    - Data from the previous layer.
    - Operational flags.
    - Options needed for communication negotiation.
    - Source and destination IP addresses.
    - Ports for communication.
    - Protocols from transport and application layers.



**Purpose of Encapsulation:**
- Encapsulation ensures that the necessary information for routing, transport, and application-specific data handling is included at each step of the data transmission process.


![[Screenshot_20240917_101230.png]]

- **PDU in Wireshark:**
    - Wireshark displays the Protocol Data Unit (PDU) in reverse order compared to how it was encapsulated.
    - The **Packet Details pane** in Wireshark shows the layers unwrapping, starting from the innermost application data to the outermost network layers.
- **Addressing Mechanisms:**
    - Addressing mechanisms are crucial for ensuring that packets are delivered to the correct hosts across a network.
- **MAC Addressing:**
    - Every logical or physical network interface has a unique **Media Access Control (MAC) address**.
    - A **MAC address** is a 48-bit (6-octet) address represented in hexadecimal.
    - Example: `00:1A:2B:3C:4D:5E`.
    - The MAC address uniquely identifies the device on a local network.

![[Screenshot_20240917_101415.png]]

- **MAC Addressing (Layer 2):**
    - MAC addressing operates at **Layer 2** (Data-Link Layer).
    - It enables **host-to-host communication** within a **broadcast domain** (local network).
    - If Layer 2 traffic crosses a **Layer 3 interface** (router), the PDU is forwarded to the router.
    - The router examines the **Layer 3 address** (IP address) to determine the next hop.
    - The **Layer 2 encapsulation** is stripped, and a new MAC address is added, corresponding to the next network device.
- **IP Addressing (Layer 3):**
    - The **Internet Protocol (IP)** enables data transmission **across networks**.
    - IP handles routing, encapsulating data, and fragmentation/reassembly of datagrams.
    - **IP is connectionless** and relies on upper-layer protocols like TCP for reliability.
    - There are two primary IP versions: **IPv4** and **IPv6**.
- **IPv4:**
    - **IPv4** is the most widely used addressing standard.
    - It is responsible for routing packets beyond the local network to remote hosts.


![[Addressing.png]]

- **IPv4 Addressing:**
    - IPv4 is a **32-bit** address made up of four **octets**, represented in decimal (e.g., `192.168.86.243`).
    - Each octet ranges from **0 to 255**.
    - IPv4 addresses are found at **Layer 3** (Network Layer) in the OSI model and **Layer 2** (Internet Layer) in the TCP/IP model.
    - IPv4 is crucial for routing data beyond local networks but is limited by the number of available addresses.
- **IPv6 Addressing:**
    - Developed due to the exhaustion of IPv4 addresses.
    - IPv6 uses a **128-bit** address made up of **16 octets**, represented in **hexadecimal**.
    - IPv6 provides a significantly larger address space, solving the limitations faced with IPv4.
    - Example of a shortened IPv6 address: `2001:0db8:85a3::8a2e:0370:7334`.



**IPv6 Benefits**:
- Larger address space
- Improved support for **Multicasting** (one-to-many)
- **Global addressing** for each device
- **IPSec** built-in security
- Simplified packet headers for faster processing



**IPv6 Addressing Types**:
- **Unicast**: Address for a single interface (host-to-host).
- **Anycast**: Address shared by multiple interfaces; only one receives the packet (useful for load balancing).
- **Multicast**: Address for multiple interfaces, all of which receive the packet (one-to-many).
- **Broadcast**: Not used in IPv6; replaced by multicast.


**Adoption of IPv6**: As of writing, the global adoption rate is about **40%**.



**Transport Layer Functions**:
- Directs **application data** through encapsulation to lower layers (IP, MAC).
- Responsible for reassembling data upon reaching the destination.



**TCP vs. UDP**:
- **TCP** (Transmission Control Protocol):
    - **Connection-oriented**, ensures reliable data delivery.
    - Uses a **three-way handshake** to establish connections.
    - Utilizes **sequence and acknowledgment numbers** for error-checking and reordering packets.
    - Slower due to **overhead**, but guarantees data integrity.
    - Used in applications where **reliability** is critical (e.g., SSH, file transfers).
- **UDP** (User Datagram Protocol):
	- **Connectionless**, sends packets without acknowledgment.
	- **Faster**, but less reliable.
	- Best for applications prioritizing **speed** over accuracy (e.g., video streaming, DNS queries).




**Example Scenarios**:
- **TCP**: Used in critical data exchanges where data loss is unacceptable (e.g., password changes over SSH).
- **UDP**: Used in applications like video streaming where missing small data fragments (e.g., a pixel) is tolerable.



**Purpose**: The **three-way handshake** establishes a reliable TCP session between a client and a server.



**TCP Flags**: Utilizes **SYN** (synchronization) and **ACK** (acknowledgment) flags.



#### Steps of the Handshake:
1. **Client sends SYN**:
    - A packet with the **SYN flag** is sent to the server.
    - This initiates synchronization for the sequence number and negotiates options like **window size** and **maximum segment size**.
2. **Server responds with SYN/ACK**:
    - The server sends a packet with **SYN and ACK** flags set.
    - Acknowledges the client's SYN and includes any necessary TCP options.
3. **Client sends ACK**:
    - The client sends a final packet with the **ACK flag**, confirming the negotiation.
    - The session is now established between the client and server.


**Graceful shutdown**: TCP uses the **FIN** flag to signal the end of data transfer and initiate session termination.



#### Steps of Session Teardown:
1. **FIN, ACK**:
    - The client sends a **FIN and ACK** to signal the end of data transmission.
2. **Server sends FIN**:
    - The server acknowledges the client’s FIN and sends its own **FIN** to signal the session's closure from its end.
3. **Client sends final ACK**:
    - The client acknowledges the server's FIN, completing the termination process.

- **Termination packet pattern**:
    - **FIN, ACK → FIN, ACK → ACK** indicates a properly terminated TCP session.



## Questions
- How many layers does the OSI model have?
	- 7
- How many layers are there in the TCP/IP model?
	- 4
- True or False: Routers operate at layer 2 of the OSI model?
	- False
- What addressing mechanism is used at the Link Layer of the TCP/IP model?
	- Mac-Address
- At what layer of the OSI model is a PDU encapsulated into a packet? ( the number )
	- 3
- What addressing mechanism utilizes a 32-bit address?
	- IPv4
- What Transport layer protocol is connection oriented?
	- TCP
- What Transport Layer protocol is considered unreliable?
	- UDP
- TCP's three-way handshake consists of 3 packets: 1.Syn, 2.Syn & ACK, 3. _? What is the final packet of the handshake?
	- ACK