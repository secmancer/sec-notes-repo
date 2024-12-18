### Introduction
- **TCP** and **UDP** are both protocols for data transmission on the Internet, with TCP used for important data (e.g., web pages, emails) and UDP for real-time data (e.g., streaming, online gaming).
- **TCP** is connection-oriented, ensuring reliable data transmission with error recovery, but it is slower due to the need for retransmissions in case of errors.
- **UDP** is connectionless, prioritizing speed over reliability. It does not verify if data is complete or error-free, leading to potential data loss but faster transmission.

### IP Packet
- An [Internet Protocol](https://en.wikipedia.org/wiki/Internet_Protocol) (`IP`) packet is the data area used by the network layer of the [Open Systems Interconnection](https://en.wikipedia.org/wiki/OSI_model) (`OSI`) model to transmit data from one computer to another. It consists of a header and the payload, the actual payload data.
- We can also think of the IP packet as a letter sent in an envelope. 
- The envelope contains the header, which includes information on the sender and the recipient, as well as instructions for routing the letter, i.e., via which post offices the letter should be sent. 
- The letter itself is the payload, the actual payload data.
- #### IP header
	- The header of an IP packet contains several fields that have important information.

| **Field** | **Description** |
| --- | --- |
| `Version` | Indicates which version of the IP protocol is being used |
| `Internet Header Length` | Indicates the size of the header in 32-bit words |
| `Class of Service` | Means how important the transmission of the data is |
| `Total length` | Specifies the total length of the packet in bytes |
| `Identification (ID)` | Is used to identify fragments of the packet when fragmented into smaller parts |
| `Flags` | Used to indicate fragmentation |
| `Fragment Offset` | Indicates where the current fragment is placed in the packet |
| `Time to Live` | Specifies how long the packet may remain on the network |
| `Protocol` | Specifies which protocol is used to transmit the data, such as TCP or UDP |
| `Checksum` | Is used to detect errors in the header |
| `Source/Destination` | Indicate where the packet was sent from and where it is being sent to |
| `Options` | Contain optional information for routing |
| `Padding` | Pads the packet to a full word length |

- We may see a computer with multiple IP addresses in different networks. 
- Here we should pay attention to the `IP ID` field. 
- It is used to identify fragments of an IP packet when fragmented into smaller parts. 
- It is a `16-bit` field with a unique number ranging from `0-65535`.
- If a computer has multiple IP addresses, the `IP ID` field will be different for each packet sent from the computer but very similar.
- #### Network Sniffing
```shell-session
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1337
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1338
IP 10.129.1.100.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1339
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1340
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1341
IP 10.129.2.200.5060 > 10.129.1.1.5060: SIP, length: 1329, id 1342
```
- We can see from the output that two different IP addresses are sending packets to IP address 10.129.1.1. 
- However, from the `IP ID`, we can see that the packets are continuous. 
- This strongly indicates that the two IP addresses belong to the same host in the network.
- #### IP Record-Route Field
	- The `Record-Route field` in the IP header also records the route to a destination device. 
	- When the destination device sends back the `ICMP Echo Reply` packet, the IP addresses of all devices that pass through the packet are listed in the `Record-Route field` of the IP header.
```shell-session
secmancer@htb[/htb]$ ping -c 1 -R 10.129.143.158

PING 10.129.143.158 (10.129.143.158) 56(124) bytes of data.
64 bytes from 10.129.143.158: icmp_seq=1 ttl=63 time=11.7 ms
RR: 10.10.14.38
        10.129.0.1
        10.129.143.158
        10.129.143.158
        10.10.14.1
        10.10.14.38


--- 10.129.143.158 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 11.688/11.688/11.688/0.000 ms
```
- The output indicates that a `ping` request was sent and a response was received from the destination device and also shows the `Record-Route field` in the IP header of the `ICMP Echo Request` packet. 
- The Record Route field contains the IP addresses of all devices that passed through the `ICMP Echo Request` packet on the way to the destination device.

|  |  |  |
| --- | --- | --- |
| 10.10.14.38 | 10.129.0.1 | 10.129.143.158 |
| 10.129.143.158 | 10.10.14.1 | 10.10.14.38 |

- The `traceroute` tool can also be used to trace the route to a destination more accurately, which uses the TCP timeout method to determine when the route has been fully traced.
	1. We send a TCP SYN packet to the destination device with a TTL of 1 in the IP header.
	    When the TCP SYN packet with a TTL greater than 1 reaches a router, the value of the TTL is decreased by 1, and the packet is forwarded to the next device. If the TCP SYN packet with a TTL of 1 reaches a router, the packet is dropped, and the router sends an ICMP Time-Exceeded packet back to us.
	2. We receive the ICMP Time-Exceeded packet and note the IP address of the router that sent the packet.
	3. After that, we send another TCP SYN packet to the destination, increasing the TTL by 1.
- The process repeats until the TCP SYN packet reaches the destination host and receives a `TCP SYN/ACK` or a `TCP RST` response from the target. 
- Once we receive a response from the destination device, we know that we have traced the route to the destination and ended the traceroute process.
- #### IP Payload
	- The payload (also referred to as `IP Data`) is the actual payload of the packet. It contains the data from various protocols, such as TCP or UDP, that are being transmitted, just like the contents of the letter in the envelope.



### TCP
- **TCP packets**, or **segments**, consist of headers and payloads, with the headers containing important information.
- **Header fields** include:
    - **Source port**: the sending computer
    - **Destination port**: the receiving computer
    - **Sequence number**: the order of data sent
    - **Acknowledgment number**: confirms successful data receipt
    - **Control flags**: indicate message status (e.g., end of message, acknowledgment, or request for data retransmission)
    - **Window size**: the amount of data the receiver can handle
    - **Checksum**: detects errors in the packet
    - **Urgent Pointer**: alerts the receiver to important data in the payload
- **Payload**: the actual data being transmitted, similar to the content of a conversation.



### UDP
- **UDP** transfers **datagrams** (small data packets) between hosts without establishing a connection beforehand, making it a connectionless protocol.
- When using **traceroute** with UDP, a **Destination Unreachable** or **Port Unreachable** message is returned when the UDP datagram reaches the target device.
- **UDP packets** are typically sent with **traceroute** on **Unix hosts**.



### Blind Spoofing
- **Blind spoofing** is a data manipulation attack where an attacker sends false information to a network without receiving responses from the target devices.
- It involves manipulating the **IP header** to indicate false source and destination addresses, including the **Initial Sequence Number (ISN)**, which specifies the sequence number of the first TCP packet in a connection.
- The attacker may send a **TCP packet** with false details, tricking the target host into establishing a connection without receiving the actual connection request.
- This attack is used to disrupt network connections, monitor traffic, or intercept information sent between network devices.