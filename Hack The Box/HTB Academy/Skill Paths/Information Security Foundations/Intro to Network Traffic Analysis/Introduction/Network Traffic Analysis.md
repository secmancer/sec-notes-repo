### Introduction
- **Characterizing network traffic** to identify common ports and protocols.
- **Establishing a baseline** for network behavior to detect deviations.
- **Monitoring and responding to threats** effectively by identifying anomalies early.
- **Facilitating compliance** with security guidelines.
- **Detecting advanced threats** as attackers adapt tactics to bypass defenses.
- **Supporting proactive defense** by leveraging NTA to pinpoint and address potential threats.****

|                                                                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Collecting` real-time traffic within the network to analyze upcoming threats.                                                                                                                     |
| `Setting` a baseline for day-to-day network communications.                                                                                                                                        |
| `Identifying` and analyzing traffic from non-standard ports, suspicious hosts, and issues with networking protocols such as HTTP errors, problems with TCP, or other networking misconfigurations. |
| `Detecting` malware on the wire, such as ransomware, exploits, and non-standard interactions.                                                                                                      |
| NTA is also useful when investigating past incidents and during threat hunting.                                                                                                                    |
- Picture a threat actor infiltrating our network, relying on communication with our infrastructure via various ports and protocols.
- Detecting malicious traffic requires understanding typical network traffic patterns within our environment.
- Identifying unusual traffic, such as `SYN` packets on uncommon ports, often indicates a `port scan` or other suspicious activity.
- Effective analysis of such traffic requires specialized skills and knowledge.



### Required Skills and Knowledge
- The skills we are about to list and describe require theoretical and practical knowledge acquired over time. 
- We do not have to know everything by heart, but we should know what to look for when certain aspects of the content seem unfamiliar. 
- This applies not only to NTA but also to most other topics we will deal with in cybersecurity.
- #### TCP/IP Stack & OSI Model
	- This understanding will ensure we grasp how networking traffic and the host applications interact.
- #### Basic Network Concepts
	- Understanding what types of traffic we will see at each level includes an understanding of the individual layers that make up the TCP/IP and OSI model and the concepts of switching and routing. If we tap a network on a backbone link, we will see much more traffic than usual, and it will be vastly different from what we find tapping an office switch.
- #### Common Ports and Protocols
	- Identifying standard ports and protocols quickly and having a functional understanding of how they communicate will ensure we can identify potentially malicious or malformed network traffic.
- #### Concepts of IP Packets and the Sublayers
	- Foundational knowledge of how TCP and UDP communicate will, at a minimum, ensure we understand what we see or are searching for. TCP, for example, is stream-oriented and allows us to follow a conversation between hosts easily. UDP is quick but not concerned with completeness, so it would be harder to recreate something from this packet type.
- #### Protocol Transport Encapsulation
	- Each layer will encapsulate the previous. Being able to read or dissect when this encapsulation changes will help us move through data quicker. It is easy to see hints based on encapsulation headers.

### Environment and Equipment
- The list below contains many different tools and equipment types that can be utilized to perform network traffic analysis. Each will provide a different way to capture or dissect the traffic. Some offer ways to copy and capture, while others read and ingest. 
- This module will explore just a few of these ([Wireshark](https://www.wireshark.org/) and [tcpdump](https://www.tcpdump.org/) mostly). Keep in mind these tools are not strictly geared for admins. Many of these can be used for malicious reasons as well.
- #### Common Traffic Analysis Tools

| **Tool** | **Description** |
| --- | --- |
| `tcpdump` | [tcpdump](https://www.tcpdump.org/) is a command-line utility that, with the aid of LibPcap, captures and interprets network traffic from a network interface or capture file. |
| `Tshark` | [TShark](https://www.wireshark.org/docs/man-pages/tshark.html) is a network packet analyzer much like TCPDump. It will capture packets from a live network or read and decode from a file. It is the command-line variant of Wireshark. |
| `Wireshark` | [Wireshark](https://www.wireshark.org/) is a graphical network traffic analyzer. It captures and decodes frames off the wire and allows for an in-depth look into the environment. It can run many different dissectors against the traffic to characterize the protocols and applications and provide insight into what is happening. |
| `NGrep` | [NGrep](https://github.com/jpr5/ngrep) is a pattern-matching tool built to serve a similar function as grep for Linux distributions. The big difference is that it works with network traffic packets. NGrep understands how to read live traffic or traffic from a PCAP file and utilize regex expressions and BPF syntax. This tool shines best when used to debug traffic from protocols like HTTP and FTP. |
| `tcpick` | [tcpick](http://tcpick.sourceforge.net/index.php?p=home.inc) is a command-line packet sniffer that specializes in tracking and reassembling TCP streams. The functionality to read a stream and reassemble it back to a file with tcpick is excellent. |
| `Network Taps` | Taps ([Gigamon](https://www.gigamon.com/), [Niagra-taps](https://www.niagaranetworks.com/products/network-tap)) are devices capable of taking copies of network traffic and sending them to another place for analysis. These can be in-line or out of band. They can actively capture and analyze the traffic directly or passively by putting the original packet back on the wire as if nothing had changed. |
| `Networking Span Ports` | [Span Ports](https://en.wikipedia.org/wiki/Port_mirroring) are a way to copy frames from layer two or three networking devices during egress or ingress processing and send them to a collection point. Often a port is mirrored to send those copies to a log server. |
| `Elastic Stack` | The [Elastic Stack](https://www.elastic.co/elastic-stack) is a culmination of tools that can take data from many sources, ingest the data, and visualize it, to enable searching and analysis of it. |
| `SIEMS` | `SIEMS` (such as [Splunk](https://www.splunk.com/en_us)) are a central point in which data is analyzed and visualized. Alerting, forensic analysis, and day-to-day checks against the traffic are all use cases for a SIEM. |
| and others. |  |

---

### BPF Syntax
- **Berkeley Packet Filter (BPF) Syntax**: A shared syntax among many tools for filtering and decoding network traffic.
- **Functionality**: Provides a raw interface to read and write data from the Data-Link layer.
- **Importance**: Key for filtering and decoding network packets effectively.
- **Usage**: Understanding BPF syntax helps in setting up effective filters within modules.
- **Resources**: Refer to the [Wikipedia article on BPF](https://en.wikipedia.org/wiki/Berkeley_Packet_Filter) or [IBM's BPF guide](https://www.ibm.com/docs/en/qsip/7.4?topic=queries-berkeley-packet-filters) for more information.


### Performing Network Traffic Analysis
- **Analysis Methods**: Can range from live traffic monitoring in the console to capturing data with taps for SIEM ingestion and pcap analysis for tactics and techniques.
- **Network Connection**: Passive listening requires connection to the target network segment, especially in switched environments with VLANs.
- **VLAN-Specific Capture**: To capture traffic from a VLAN, the capture device must be on the same network.
- **Traffic Access**: Tools like network taps, span ports, and port mirroring enable capturing traffic across specific links regardless of network segment or destination.

### NTA Workflow
- Traffic analysis is not an exact science. NTA can be a very dynamic process and is not a direct loop. 
- It is greatly influenced by what we are looking for (network errors vs. malicious actions) and where we have visibility into our network. 
- Performing traffic analysis can distill down to a few basic tenants.

![image](https://academy.hackthebox.com/storage/modules/81/workflow.png)
- #### 1\. Ingest Traffic
	- Once we have decided on our placement, begin capturing traffic. Utilize capture filters if we already have an idea of what we are looking for.
- #### 2\. Reduce Noise by Filtering
	- Capturing traffic of a link, especially one in a production environment, can be extremely noisy. Once we complete the initial capture, an attempt to filter out unnecessary traffic from our view can make analysis easier. (Broadcast and Multicast traffic, for example.)
- #### 3\. Analyze and Explore
	- Now is the time to start carving out data pertinent to the issue we are chasing down. Look at specific hosts, protocols, even things as specific as flags set in the TCP header. The following questions will help us:
		1. Is the traffic encrypted or plain text? Should it be?
		2. Can we see users attempting to access resources to which they should not have access?
		3. Are different hosts talking to each other that typically do not?
- #### 4\. Detect and Alert
	1. Are we seeing any errors? Is a device not responding that should be?
	2. Use our analysis to decide if what we see is benign or potentially malicious.
	3. Other tools like IDS and IPS can come in handy at this point. They can run heuristics and signatures against the traffic to determine if anything within is potentially malicious.
- #### 5\. Fix and Monitor
	- Fix and monitor is not a part of the loop but should be included in any workflow we perform. If we make a change or fix an issue, we should continue to monitor the source for a time to determine if the issue has been resolved.