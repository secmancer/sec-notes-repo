### Introduction
- **Networking Refresher**: Understanding standard protocols and network flow is essential for capturing and analyzing traffic.
- **Core Concepts**: Knowing ports, protocols, and typical network flow is critical for accurate traffic dissection.
- **Recommendation**: Beginners should complete the [Introduction to Networking](https://academy.hackthebox.com/course/preview/introduction-to-networking) module for foundational knowledge.

### OSI / TCP-IP Models
- #### Networking Models

![image](https://academy.hackthebox.com/storage/modules/81/net_models4.png)

- The image above gives a great view of the Open Systems Interconnect (`OSI`) model and the Transmission Control Protocol - Internet Protocol (`TCP-IP`) model side by side. 
- The models are a graphical representation of how communication is handled between networked computers. Let's take a second to compare the two:
- #### Model Traits Comparison.
	- **OSI vs. TCP-IP Models**:
	    - OSI is segmented into more layers, offering detailed functional chunks.
	    - TCP-IP is more practical and flexible, with four broader layers.
	- **Layer Breakdown**:
	    - OSI layers 1-4 focus on data transport between hosts.
	    - OSI layers 5-7 manage data interpretation, presentation, and end-user interaction.
	    - TCP-IP blends OSI layers, with its four layers roughly aligning as:
	        - TCP-IP layer 4 = OSI layers 5-7.
	        - TCP-IP layer 3 = OSI transport layer.
	        - TCP-IP layer 2 = OSI network layer.
	        - TCP-IP layer 1 = OSI layers 1-2 (link and physical).
	- **Protocol Data Units (PDUs)**: Understanding PDUs is essential for analyzing theoretical and real-world data encapsulation at each layer.

| Trait | OSI | TCP-IP |
| --- | --- | --- |
| Layers | Seven | Four |
| Flexibility | Strict | Loose |
| Dependency | Protocol independent & generic | Based on common communication protocols |

- #### PDU Example
![image](https://academy.hackthebox.com/storage/modules/81/net_models_pdu2.png)
	- When inspecting a PDU, we need to keep the idea of encapsulation in mind. 
	- As our data moves down the protocol stack, each layer will wrap the previous layers' data in a new bubble we call encapsulation.
	- This bubble adds the necessary information of that layer into the header of the PDU. 
	- This information can vary by level, but it includes what is held by the previous layer, operational flags, any options required to negotiate communications, the source and destination IP addresses, ports, transport, and application layer protocols.
- #### PDU Packet Breakdown

![image](https://academy.hackthebox.com/storage/modules/81/pdu-wireshark.png)

- The image above shows us the makeup of a PDU side by side with a packet breakout from Wireshark's Packet Details pane. 
- Please take note that when we see the breakout in Wireshark, it is in reverse order. 
- Wireshark shows us the PDU in reverse because it is in the order that it was unencapsulated.


### Addressing Mechanisms
- Now that we have gone over the basic concepts driving networking behavior let us take some time to discuss the addressing mechanisms that enable the delivery of our packets to the correct hosts. We will begin with Media Access Control addresses first.
- #### MAC-Addressing
	- Each logical or physical interface attached to a host has a Media Access Control (`MAC`) address. This address is a 48-bit `six octet` address represented in hexadecimal format. If we look at the image below, we can see an example of one by the `red` arrow.
	- MAC-addressing is utilized in Layer two ( `the data-link or link-layer depending on which model you look at` ) communications between hosts. 
	- This works through host-to-host communication within a broadcast domain. If layer two traffic needs to cross a layer three interface, that PDU is sent to the layer three egress interface, and it is routed to the correct network. 
	- At layer two, this looks as though the PDU is addressed to the router interface, and the router will take the layer three address into account when determining where to send it next. 
	- Once it makes a choice, it strips the encapsulation at layer two and replaces it with new information that indicates the next physical address in the route.
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)



### IP Addressing
- The Internet Protocol (`IP`) was developed to deliver data from one host to another across network boundaries. IP is responsible for routing packets, the encapsulation of data, and fragmentation and reassembly of datagrams when they reach the destination host. 
- By nature, IP is a connectionless protocol that provides no assurances that data will reach its intended recipient. For the reliability and validation of data delivery, IP relies on upper-layer protocols such as TCP. 
- Currently, there exist two main versions of IP. IPv4, which is the current dominant standard, and IPv6, which is intended to be the successor of IPv4.
- #### IPv4
	- The most common addressing mechanism most are familiar with is the Internet Protocol address version 4 (`IPv4`). IPv4 addressing is the core method of routing packets across networks to hosts located outside our immediate vicinity. The image below shows us an example of an IPv4 address by the `green` arrow.
	- An IPv4 address is made up of a 32-bit `four octet` number represented in decimal format. In our example, we can see the address `192.168.86.243`. 
	- Each octet of an IP address can be represented by a number ranging from `0` to `255`. When examining a PDU, we will find IP addresses in layer three (`Network`) of the OSI model and layer two (`internet`) of the TCP-IP model. 
	- We will not deep dive into IPv4 here, but for the sake of this module, understand what these addresses are, what they do for us, and at which layer they are used.
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)
- #### IPv6
	- After a little over a decade of utilizing IPv4, it was determined that we had quickly exhausted the pool of usable IP addresses. With such large chunks sectioned off for special use or private addressing, the world had quickly used up the available space. To help solve this issue, two things were done. 
	- The first was implementing variable-length subnet masks (`VLSM`) and Classless Inter-Domain Routing (`CIDR`). This allowed us to redefine the useable IP addresses in the v4 format changing how addresses were assigned to users. The second was the creation and continued development of `IPv6` as a successor to IPv4.
	- IPv6 provides us a much larger address space that can be utilized for any networked purpose. IPv6 is a 128-bit address `16 octets` represented in Hexadecimal format. We can see an example of a shortened IPv6 address in the image below by the blue arrow.
	- Along with a much larger address space, IPv6 provides: Better support for Multicasting (sending traffic from one to many) Global addressing per device Security within the protocol in the form of IPSec Simplified Packet headers allow for easier processing and move from connection to connection without being re-assigned an address.
	- IPv6 uses four main types of addresses within its schema:
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)
- #### IPv6 Addressing Types

| **Type**    | **Description**                                                                |
| ----------- | ------------------------------------------------------------------------------ |
| `Unicast`   | Addresses for a single interface.                                              |
| `Anycast`   | Addresses for multiple interfaces, where only one of them receives the packet. |
| `Multicast` | Addresses for multiple interfaces, where all of them receive the same packet.  |
| `Broadcast` | Does not exist and is realized with multicast addresses.                       |

- When thinking about each address type, it is helpful to remember that Unicast traffic is host to host, while Multicast is one to many, and Anycast is one to many in a group where only one will answer the packet. (think load balancing).
- Even with its current state providing many advantages over IPv4, the adoption of IPv6 has been slow to catch on.
- #### Adoption of IPv6

![image](https://academy.hackthebox.com/storage/modules/81/ipv6-adoption.png)

- At the time of writing, according to statistics published by Google, the adoption rate is only around 40 percent globally.



### TCP / UDP, Transport Mechanisms
- The Transport Layer has several mechanisms to help ensure the seamless delivery of data from source to destination. 
- Think about the Transport layer as a control hub. Application data from the higher layers have to traverse down the stack to the Transport layer. 
- This layer directs how the traffic will be encapsulated and thrown to the lower layer protocols ( IP and MAC ). Once the data reaches its intended recipient, the Transport layer, working with the Network / Internet layer protocols, is responsible for reassembling the encapsulated data back in the correct order. 
- The two mechanisms used to accomplish this task are the Transmission Control (`TCP`) and the User Datagram Protocol (`UDP`).
	- #### TCP vs. UDP
	- Let us take a second to examine these two protocols side by side.

| **Characteristic** | **TCP** | **UDP** |
| --- | --- | --- |
| `Transmission` | Connection-oriented | Connectionless. Fire and forget. |
| `Connection Establishment` | TCP uses a three-way handshake to ensure that a connection is established. | UDP does not ensure the destination is listening. |
| `Data Delivery` | Stream-based conversations | packet by packet, the source does not care if the destination is active |
| `Receipt of data` | Sequence and Acknowledgement numbers are utilized to account for data. | UDP does not care. |
| `Speed` | TCP has more overhead and is slower because of its built-in functions. | UDP is fast but unreliable. |
- **TCP vs. UDP**:
    - **TCP**: Reliable protocol with error checking and data acknowledgment; ensures completeness over speed.
    - **UDP**: Faster, "fire-and-forget" protocol, prioritizing speed over reliability.
- **TCP Characteristics**:
    - Used for applications requiring reliable data transfer, e.g., SSH.
    - Ensures data integrity by acknowledging packets and preventing partial fragments from being processed.
    - Example: Prevents errors in critical commands like `sudo passwd user`.
- **UDP Characteristics**:
    - Suited for speed-critical applications like video streaming or DNS queries.
    - Dropped packets do not cause major issues (e.g., minor video glitches or reissued DNS requests).
    - No acknowledgment or response, making it lightweight but less reliable.
- **Connection Behavior**: TCP traffic involves connection establishment, whereas UDP traffic consists of single packets without acknowledgment.
- #### TCP Three-way Handshake
	- **TCP Session Establishment**:
	    - Uses a **three-way handshake** to ensure reliable communication between client and server.
	    - Relies on **SYN** (synchronization) and **ACK** (acknowledgment) flags in the TCP header.
	- **Three-Way Handshake Process**:
	    1. **Client Sends SYN**:
	        - Initiates connection with a synchronization packet containing negotiable options like sequence number, window size, and maximum segment size.
	    2. **Server Responds with SYN-ACK**:
	        - Acknowledges the client's SYN packet and includes its own sequence number and any required TCP option changes.
	    3. **Client Sends ACK**:
	        - Acknowledges the server's response, completing the handshake and establishing the session.
	- **Practical Relevance**: Understanding this process helps recognize handshake patterns in packet captures later in the module.
- When examining this output, we can see the start of our handshake on line one. Looking at the information highlighted in the `red box`, we can see our initial Syn flag is set. If we look at the port numbers underlined in `green`, we can see two numbers, `57678` and `80`. 
- The first number is the random high port number in use by the client, and the second is the well-known port for HTTP used by the server to listen for incoming web request connections. In line 2, we can see the server's response to the client with an `SYN / ACK` packet sent to the same ports. On line 3, we can see the client acknowledge the server's synchronization packet to establish the connection.
- Packet 4 shows us that the HTTP request was sent, and a session is established to stream the data for the image requested. We can see as the stream continues that TCP sends acknowledgments for each chunk of data sent. This is an example of typical TCP communication.
- We have seen how a session is established with TCP; now, let us examine how a session is concluded.

![image](https://academy.hackthebox.com/storage/modules/81/three-way-handshake.png)
- #### TCP Session Teardown
![image](https://academy.hackthebox.com/storage/modules/81/session-teardown.png)

- In the image above, a set of packets similar to our three-way handshake visible at the end of the output. This is how TCP gracefully shuts connections. Another flag we will see with TCP is the `FIN` flag. It is used for signaling that the data transfer is finished and the sender is requesting termination of the connection. The client acknowledges the receipt of the data and then sends a `FIN` and `ACK` to begin session termination. The server responds with an acknowledgment of the FIN and sends back its own FIN. Finally, the client acknowledges the session is complete and closes the connection. Before session termination, we should see a packet pattern of:
	1. `FIN, ACK`
	2. `FIN, ACK`,
	3. `ACK`
- If we look at the image above detailing a session, we will see that this is the case. An output similar to this is considered an adequately terminated connection.


### Questions
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