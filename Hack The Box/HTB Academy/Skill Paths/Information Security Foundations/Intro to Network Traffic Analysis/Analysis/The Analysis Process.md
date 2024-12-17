### Introduction
- Network Traffic Analysis (NTA) is a dynamic process, influenced by multiple factors like tools, permissions, and network visibility, with the idea of establishing a repeatable framework that can be applied to traffic analysis consistently.
- It's a detailed examination of network events/processes.
	- Goal: determine their origin, impact, and potential risks.
	- Finding deviations from what is considered normal network behavior, like unauthorized remote communications in an easy and timely fashion.
	- Helps gives us visibility into our network, making it a crucial tool for our network defense. 
	- Aids with troubleshooting the network.
- Advanced implementations may also have IDS/IPS, firewalls, and centralized logging solutions to automate these alerts.
- Even with automation, a human aspect to the oversight is still needed to ensure nothing is glanced over, as computers can really only go so far.



### Analysis and Capturing Methods
- Two methods for traffic analysis: **active** and **passive**.
	- **Passive**: Simply look over and get data from the network without any packet interaction.
		- Tools: network taps, port mirroring, packet capture
	- **Active**: Direct intervention with the network, often through packet interaction
		- Tools: IDS, firewalls, custom traffic monitoring tools with filters/rule sets
- Now with our capturing methods laid out, we also have two options for analysis we can use.
	- **Post-Capture**: Captured traffic gets stored and analyzed after collection
		- Tools: Wireshark, SIEMS, tcpdump
	- **Real-Time**: Analyze traffic as it's flowing through the network'
		- Tools: IDS/IPS, Splunk, ELK Stack

| Method      | Dependencies                                                                                   | Example Tools                                    |
| ----------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| **Passive** | - Network tap/port mirroring- Packet capture devices- Storage for packet data                  | Wireshark, tcpdump, Snort, Security Onion, SIEMs |
| **Active**  | - In-line devices (IDS, firewalls, probes)- Filtering rules and policies- Real-time processing | IDS/IPS, Firewalls, Splunk, ELK Stack            |



### Traffic Capture Dependencies

| **Dependencies** | **Passive** | **Active** | **Description** |
| --- | --- | --- | --- |
| `Permission` | `☑` | `☑` | Depending on the organization we are working in, capturing data can be against policy or even against the law in some sensitive areas like healthcare or banking. Be sure always to obtain permission in writing from someone with the proper authority to grant it to you. We may style ourselves as hackers, but we want to stay in the light legally and ethically. |
| `Mirrored Port` | `☑` | ☐ | A switch or router network interface configured to copy data from other sources to that specific interface, along with the capability to place your NIC into promiscuous mode. Having packets copied to our port allows us to inspect any traffic destined to the other links we could normally not have visibility over. Since VLANs and switch ports will not forward traffic outside of their broadcast domain, we have to be connected to the segment or have that traffic copied to our specific port. When dealing with wireless, passive can be a bit more complicated. We must be connected to the SSID we wish to capture traffic off of. Just passively listening to the airwaves around us will present us with many SSID broadcast advertisements, but not much else. |
| `Capture Tool` | `☑` | `☑` | A way to ingest the traffic. A computer with access to tools like TCPDump, Wireshark, Netminer, or others is sufficient. Keep in mind that when dealing with PCAP data, these files can get pretty large quickly. Each time we apply a filter to it in tools like Wireshark, it causes the application to parse that data again. This can be a resource-intensive process, so make sure the host has abundant resources. |
| `In-line Placement` | ☐ | `☑` | Placing a Tap in-line requires a topology change for the network you are working in. The source and destination hosts will not notice a difference in the traffic, but for the sake of routing and switching, it will be an invisible next hop the traffic passes through on its way to the destination. |
| `Network Tap or Host With Multiple NIC's` | ☐ | `☑` | A computer with two NIC's, or a device such as a Network Tap is required to allow the data we are inspecting to flow still. Think of it as adding another router in the middle of a link. To actively capture the traffic, we will be duplicating data directly from the sources. The best placement for a tap is in a layer three link between switched segments. It allows for the capture of any traffic routing outside of the local network. A switched port or VLAN segmentation does not filter our view here. |
| `Storage and Processing Power` | `☑` | `☑` | You will need plenty of storage space and processing power for traffic capture off a tap. Much more traffic is traversing a layer three link than just inside a switched LAN. Think of it like this; When we passively capture traffic inside a LAN, it's like pouring water into a cup from a water fountain. It's a steady stream but manageable. Actively grabbing traffic from a routed link is more like using a water hose to fill up a teacup. There is a lot more pressure behind the flow, and it can be a lot for the host to process and store. |
- **Understanding network traffic baselines** is a critical recommendation for effective traffic analysis.
- **Without a baseline**, analyzing captured data becomes time-consuming and overwhelming, as every conversation must be examined to filter out known-good traffic.
- **With a baseline**, normal traffic can be quickly filtered out, allowing focus on outliers or suspicious activity.
- **Tools like Wireshark’s “top talkers”** help identify unusual data patterns, such as peer-to-peer communication on ports like 8080 or 445, which may indicate potential issues.
- **Faster visibility** into network traffic reduces damage from intrusions, making baseline understanding essential for spotting abnormal behavior efficiently.