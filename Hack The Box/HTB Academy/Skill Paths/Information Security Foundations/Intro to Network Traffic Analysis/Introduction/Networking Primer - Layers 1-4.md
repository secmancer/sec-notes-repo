### Introduction
- **Networking Refresher**: Understanding standard protocols and network flow is essential for capturing and analyzing traffic.
- **Core Concepts**: Knowing ports, protocols, and typical network flow is critical for accurate traffic dissection.


### OSI / TCP-IP Models
- #### Networking Models

![image](https://academy.hackthebox.com/storage/modules/81/net_models4.png)

- Above is a great view of the Open Systems Interconnect (`OSI`) model and the Transmission Control Protocol - Internet Protocol (`TCP-IP`) model side by side. 
- The models are a graphical representation of how communication is handled between networked computers.
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
	- Encapsulation: a layer will wrap data from the previous layer.
	- This bubble adds the necessary information of that layer into the header of the PDU. 
	- This information can vary by level, but it includes what is held by the previous layer, operational flags, any options required to negotiate communications, the source and destination IP addresses, ports, transport, and application layer protocols.
- #### PDU Packet Breakdown

![image](https://academy.hackthebox.com/storage/modules/81/pdu-wireshark.png)

- Above shows us the makeup of a PDU side by side with a packet breakout from Wireshark's Packet Details pane, which is in reverse order when viewed in Wireshark.
- This is because it is in the order that it was unencapsulated.


### MAC-Addressing
- Every logical/physical interface on the host has  Media Access Control (`MAC`) address.
	- 48-bit address in a hexadecimal format. One is shown next to the red arrow.
- MAC-addressing is utilized in Layer 2.
	- Remember: Layer 2 is the data-link or link-layer depending on which model you look at communications between hosts. 
- This works through host-to-host communication within a broadcast domain. 
- If layer two traffic needs to cross a layer three interface, that PDU is sent to the layer three egress interface, and it is routed to the correct network. 
- At layer two, this looks as though the PDU is addressed to the router interface, and the router will take the layer three address into account when determining where to send it next. 
- Once it makes a choice, it strips the encapsulation at layer two and replaces it with new information that indicates the next physical address in the route.
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)



### IP Addressing
- Internet Protocol (IP) intends to get data from one host to another across network boundaries, responsible for routing packets, encapsulating the data, along with the fragmentation/reassembly of datagrams when reaching the destination host.
- IP is a connectionless protocol with no assurance that any data will reach the intended destination.
	- Therefore, for more reliability, IP needs to rely on something like TCP to get around this problem.
- Two versions of IP: IPv4 (current, common standard) and IPv6 (intended successor).


### IPv4
	- Most common addressing mechanism.
	- Example shown below by the green arrow.
	- Made up of a 32-bit four octet number, represented in decimal format.
	- Each octet is represented by a number from 0 to 255.
- When looking at a PDU, we find addresses in both layer 3 (Network) and layer 2 (Internet) in the TCP-IP model.
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)


### IPv6
- We have quickly starting to run out of IPv4 addresses. So, two things were done to solve this problem.
	- Implement variable-length subnet masks (VLSM) and Classless Inter-Domain Routing (CIDR).
		- Allows us to redefine usable addresses in how they are assigned to users.
	- Creation and continued development of IPv6.
- Much larger address space is provided.
	- 128-bit address 16 octets in hexadecimal format.
	- Shorten example shown with the blue arrow.
- Better support for Multicasting, which allows for sending traffic from one to many.
	- Overall allows for easier processing/moving from connection to connection
	- No reassigning required.
![image](https://academy.hackthebox.com/storage/modules/81/Addressing.png)
- Below is a table with several IPv6 types of addresses is given below.

| **Type**    | **Description**                                                                |
| ----------- | ------------------------------------------------------------------------------ |
| `Unicast`   | Addresses for a single interface.                                              |
| `Anycast`   | Addresses for multiple interfaces, where only one of them receives the packet. |
| `Multicast` | Addresses for multiple interfaces, where all of them receive the same packet.  |
| `Broadcast` | Does not exist and is realized with multicast addresses.                       |

- Remember: Unicast traffic is host to host while Multicast is one to many, and Anycast is one to many in a group of only one that can answer the packet.
- Even with its advantages over IPv4, the adoption of IPv6 has been slow to catch on.
- #### Adoption of IPv6
	- At the time of writing, according to statistics published by Google, the adoption rate is only around 40 percent globally.
![image](https://academy.hackthebox.com/storage/modules/81/ipv6-adoption.png)



###  Transport Mechanisms: TCP and UDP
- Transport layer has several ways to ensure seamless delivery of data from source to destination.
	- Application data from higher layers traverse down the stack to the Transport layer.
- This layer directs the way traffic is encapsulated and thrown into the lower layer protocols, like IP and MAC.
- Once reaching its destination, the Transport layers reassembles the encapsulated data back into the correct order with help from the Network/Internet layer protocols.
- To accomplish this, we have two protocols: Transmission Control (`TCP`) and User Datagram Protocol (`UDP`).

| **Characteristic** | **TCP** | **UDP** |
| --- | --- | --- |
| `Transmission` | Connection-oriented | Connectionless. Fire and forget. |
| `Connection Establishment` | TCP uses a three-way handshake to ensure that a connection is established. | UDP does not ensure the destination is listening. |
| `Data Delivery` | Stream-based conversations | packet by packet, the source does not care if the destination is active |
| `Receipt of data` | Sequence and Acknowledgement numbers are utilized to account for data. | UDP does not care. |
| `Speed` | TCP has more overhead and is slower because of its built-in functions. | UDP is fast but unreliable. |

### TCP vs. UDP
- #### TCP
	- Reliable protocol that ensures all packets get to where they need to go
	- Great for applications that need reliable data transfer
	- Connection establishment
- #### UDP
	- Protocol that is fine with some dropped packets along the way
	- Great for applications that need fast data transfer
	- Single packets



### TCP 3-Way Handshake
- This is used by TCP to ensure reliable communication between the client and server, using **SYN** (synchronization) and **ACK** (acknowledgment) flags to do so.
- #### Process
	1. Client Sends SYN
		- Initiate connection with a synchronization packet with negotiable options:
			- Sequence number, window size, maximum segment size
	 2. Server Responds with SYN-ACK
		- Acknowledge the SYN packet sent from the client
		- Include its own sequence number and any required TCP option changes
	3. Client Sends ACK
		- Acknowledge the server's response
		- This completes the handshake, hence completes the connection.
- #### Example
	- **Practical Relevance**: Understanding this process helps recognize handshake patterns in packet captures later in the module.
	- When examining this output, we can see the start of our handshake on line one. 
	- Looking at the information highlighted in the `red box`, we can see our initial Syn flag is set. If we look at the port numbers underlined in `green`, we can see two numbers, `57678` and `80`. 
	- The first number is the random high port number in use by the client, and the second is the well-known port for HTTP used by the server to listen for incoming web request connections. 
	- In line 2, we can see the server's response to the client with an `SYN / ACK` packet sent to the same ports. 
	- On line 3, we can see the client acknowledge the server's synchronization packet to establish the connection.
	- Packet 4 shows us that the HTTP request was sent, and a session is established to stream the data for the image requested. We can see as the stream continues that TCP sends acknowledgments for each chunk of data sent. This is an example of typical TCP communication.
	- We have seen how a session is established with TCP; now, let us examine how a session is concluded.
![image](https://academy.hackthebox.com/storage/modules/81/three-way-handshake.png)


### TCP Session Teardown
![image](https://academy.hackthebox.com/storage/modules/81/session-teardown.png)
- In the image above, a set of packets similar to our three-way handshake visible at the end of the output. 
- This is how TCP gracefully shuts connections. Another flag we will see with TCP is the `FIN` flag. It is used for signaling that the data transfer is finished and the sender is requesting termination of the connection. 
- The client acknowledges the receipt of the data and then sends a `FIN` and `ACK` to begin session termination. 
- The server responds with an acknowledgment of the FIN and sends back its own FIN. 
- Finally, the client acknowledges the session is complete and closes the connection. Before session termination, we should see a packet pattern of:
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