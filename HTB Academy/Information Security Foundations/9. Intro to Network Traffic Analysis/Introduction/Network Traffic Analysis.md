NTA involves examining network traffic to:
- Identify common ports and protocols used.
- Establish a baseline for normal traffic.
- Detect and respond to threats.
- Ensure better insight into network activity.


**Benefits:**
- Helps identify anomalies and security threats early.
- Aids in meeting security guidelines.
- Provides insight when attackers use legitimate credentials or blend in with allowed tools.
- Useful in real-time threat detection, incident investigation, and threat hunting.



**Common Use Cases:**
- Collecting real-time traffic for threat analysis.
- Establishing a baseline of regular network communication.
- Detecting unusual traffic on non-standard ports, suspicious hosts, or misconfigurations.
- Identifying malware, ransomware, and other threats in network traffic.



**Example Scenario:**
- A threat actor must interact with network infrastructure to breach it.
- Recognizing deviations from typical network traffic helps narrow down malicious activities (e.g., detecting many SYN packets on rarely used ports might indicate a port scan).


### **Required Skills and Knowledge for NTA**
1. **TCP/IP Stack & OSI Model:**
    - Understanding networking traffic and its interaction with host applications.
2. **Basic Network Concepts:**
    - Familiarity with traffic at each layer of the TCP/IP and OSI models.
    - Knowledge of switching, routing, and backbone links versus office switches.
3. **Common Ports and Protocols:**
    - Recognizing standard ports and understanding how they communicate to spot potential threats.
4. **IP Packets and Sublayers:**
    - Understanding TCP (stream-oriented) and UDP (quick, not concerned with completeness) for effective analysis.
5. **Protocol Transport Encapsulation:**
    - Ability to read and dissect encapsulated layers for faster data analysis.


### **Common Traffic Analysis Tools**
1. **tcpdump:**
    - Command-line tool that captures and interprets network traffic with the help of LibPcap.
2. **TShark:**
    - Command-line version of Wireshark for live packet capturing and reading from files.
3. **Wireshark:**
    - Graphical tool for analyzing captured network traffic in-depth with various protocol dissectors.
4. **NGrep:**
    - Similar to grep but for network traffic; works with PCAP files and live traffic using regex and BPF syntax.
5. **tcpick:**
    - Specializes in reassembling TCP streams into files.
6. **Network Taps:**
    - Devices (e.g., Gigamon) that copy network traffic for analysis, either inline or out-of-band.
7. **Networking Span Ports:**
    - Copy frames during ingress/egress to send them to a collection point.
8. **Elastic Stack:**
    - Toolset for data ingestion, visualization, and analysis.
9. **SIEMs (e.g., Splunk):**
    - Centralized systems for analyzing and visualizing traffic, useful for alerting and forensic analysis.



### **BPF Syntax:**
- **Berkeley Packet Filter (BPF):**
    - Common syntax used for filtering and decoding in many NTA tools (e.g., tcpdump, Wireshark).



### **Performing Network Traffic Analysis:**
- **Capture and Monitoring:**
    - NTA can be as simple as watching live traffic or as complex as ingesting traffic in a SIEM.
    - Must be connected to the specific network segment (e.g., VLAN) to monitor effectively.
    - Tools like network taps and span ports allow capturing traffic from specific links.



### **NTA Workflow:**
- **Dynamic Process:**
    - NTA is influenced by what is being analyzed (errors vs. malicious activity).
    - The process depends on visibility across the network.


![[workflow.png]]


**Ingest Traffic:**
- Start capturing traffic after deciding where to place the capture point.
- Use capture filters if specific traffic is targeted (e.g., filter by IP, protocol).




**Reduce Noise by Filtering:**
- Production environments generate a lot of traffic (noisy).
- Filter out unnecessary traffic like broadcast and multicast to focus on relevant data.



**Analyze and Explore:**
- Look into specific hosts, protocols, or flags in headers to isolate useful information.
- Key questions to ask during analysis:
    - Is the traffic encrypted? Should it be?
    - Are users trying to access unauthorized resources?
    - Are unexpected hosts communicating?




**Detect the Root Issue:**
- Identify errors or missing responses from devices.
- Analyze whether the traffic is benign or malicious.
- Tools like IDS/IPS can help by checking heuristics and signatures.



**Fix and Monitor:**
- After fixing issues, monitor the source for a while to ensure the problem is resolved.