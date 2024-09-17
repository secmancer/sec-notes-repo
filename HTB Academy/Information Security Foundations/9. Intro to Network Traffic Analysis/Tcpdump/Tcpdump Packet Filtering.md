**Overview:**
- **Tcpdump** provides efficient ways to parse and filter data from packet captures.
- **Advanced Filters** can be used to reduce the volume of captured data and optimize processing.

**Benefits of Advanced Filtering:**
- **Reduces Output:** Limits the amount of traffic displayed or saved to a file.
- **Efficient Use of Resources:** Decreases file size and helps buffer processing.

**Advanced Filtering Options:**
- **Specific Captures:** Target packets from specific hosts or with certain flags in the TCP header.
- **Standard Syntax Pairing:** Combine with basic Tcpdump options for more precise captures.

**Commonly Used Filters:**
- **Filters:** Not exhaustive but essential for quick setup and practical use.
- **Function:** Inspects packets and matches values in protocol headers.

**Recommendation:**
- Explore and experiment with different filter combinations to meet specific capture needs.

![[Screenshot_20240917_103615.png]]


#### Host Filter
- **Purpose**: To filter network traffic based on a specific IP address, checking for the IP in either the source or destination IP fields.
- **Syntax**:
```
host [IP]
```
- **Example Command**:
```
sudo tcpdump -i eth0 host 172.16.146.2
```
- **Output Example**:
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
14:50:53.072536 IP 172.16.146.2.48738 > ec2-52-31-199-148.eu-west-1.compute.amazonaws.com.https: Flags [P.], seq 3400465007:3400465044, ack 254421756, win 501, options [nop,nop,TS val 220968655 ecr 80852594], length 37
```
- **Use Case**: Useful for examining traffic involving a specific host or server to identify communication patterns and determine if they are legitimate. Can be combined with other filters for more detailed analysis.



#### Source/Destination Filter
- **Purpose**: To filter network traffic based on the source or destination host, network, or port.
- **Syntax**:
```
src [host|net|port] [IP|Network Range|Port]
dst [host|net|port] [IP|Network Range|Port]
```
- **Example Command for Source Host**:
```
sudo tcpdump -i eth0 src host 172.16.146.2
```
- **Example Command for Source Port**:
```
sudo tcpdump -i eth0 tcp src port 80
```
- **Example Command for Destination Network**:
```
sudo tcpdump -i eth0 dest net 172.16.146.0/24
```
**Output Examples**:
- **Source Host**:
```
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
14:53:36.199628 IP 172.16.146.2.48766 > ec2-52-31-199-148.eu-west-1.compute.amazonaws.com.https: Flags [P.], seq 1428378231:1428378268, ack 3778572066, win 501, options [nop,nop,TS val 221131782 ecr 80889856], length 37
```
- **Source Port**:
```
06:17:08.222534 IP 65.208.228.223.http > dialin-145-254-160-237.pools.arcor-ip.net.3372: Flags [S.], seq 290218379, ack 951057940, win 5840, options [mss 1380,nop,nop,sackOK], length 0
```
- **Use Case**: Allows for filtering based on specific traffic directions (source or destination). This can be extended to include ports and network ranges, aiding in pinpointing specific traffic patterns or anomalies.



#### Protocol Filter
- **Purpose**: To filter traffic based on the specific protocol, using either the common protocol name or its number.
- **Syntax**:
```
proto [protocol]
```
- **Example Command**:
```
sudo tcpdump -i eth0 proto 6  # For TCP (protocol number 6)
```
**Use Case**: Useful for analyzing specific types of traffic (e.g., TCP, UDP, ICMP) by filtering out other protocols.



### Protocol Filter
- **Syntax:** `tcpdump -i [interface] [protocol]`
- **Example:** To capture UDP packets:
```
sudo tcpdump -i eth0 udp
```
- **Output Example:**
```
06:17:09.864896 IP dialin-145-254-160-237.pools.arcor-ip.net.3009 > 145.253.2.203.domain: 35+ A? pagead2.googlesyndication.com. (47)
06:17:10.225414 IP 145.253.2.203.domain > dialin-145-254-160-237.pools.arcor-ip.net.3009: 35 4/0/0 CNAME pagead2.google.com., CNAME pagead.google.akadns.net., A 216.239.59.104, A 216.239.59.99 (146)
```



### Protocol Number Filter
- **Syntax:** `tcpdump -i [interface] proto [protocol number]`
- **Example:** To capture packets for protocol number 17 (UDP):
```
sudo tcpdump -i eth0 proto 17
```
- **Output Example:**
```
06:17:09.864896 IP dialin-145-254-160-237.pools.arcor-ip.net.3009 > 145.253.2.203.domain: 35+ A? pagead2.googlesyndication.com. (47)
06:17:10.225414 IP 145.253.2.203.domain > dialin-145-254-160-237.pools.arcor-ip.net.3009: 35 4/0/0 CNAME pagead2.google.com., CNAME pagead.google.akadns.net., A 216.239.59.104, A 216.239.59.99 (146)
```



### Port Filter
- **Syntax:** `tcpdump -i [interface] [protocol] port [port number]`
- **Example:** To capture TCP traffic on port 443:
```
sudo tcpdump -i eth0 tcp port 443
```
- **Output Example:**
```
06:17:07.311224 IP dialin-145-254-160-237.pools.arcor-ip.net.3372 > 65.208.228.223.http: Flags [S], seq 951057939, win 8760, options [mss 1460,nop,nop,sackOK], length 0
06:17:08.222534 IP 65.208.228.223.http > dialin-145-254-160-237.pools.arcor-ip.net.3372: Flags [S.], seq 290218379, ack 951057940, win 5840, options [mss 1380,nop,nop,sackOK], length 0
```



### Port Range Filter
- **Syntax:** `tcpdump -i [interface] portrange [range]`
- **Example:** To capture traffic on ports from 0 to 1024:
```
sudo tcpdump -i eth0 portrange 0-1024
```
- **Output Example:**
```
13:10:35.092477 IP 172.16.146.1.domain > 172.16.146.2.32824: 47775 1/0/0 CNAME autopush.prod.mozaws.net. (81)
13:10:35.093217 IP 172.16.146.2.48078 > 172.16.146.1.domain: 30234+ A? ocsp.pki.goog. (31)
```


### Less/Greater Filter
- **Syntax:** `tcpdump -i [interface] [less|greater] [size in bytes]`
- **Example:** To capture packets smaller than 64 bytes:
```
sudo tcpdump -i eth0 less 64
```
- **Output Example:**
```
06:17:07.311224 IP dialin-145-254-160-237.pools.arcor-ip.net.3372 > 65.208.228.223.http: Flags [S], seq 951057939, win 8760, options [mss 1460,nop,nop,sackOK], length 0
06:17:08.222534 IP 65.208.228.223.http > dialin-145-254-160-237.pools.arcor-ip.net.3372: Flags [S.], seq 290218379, ack 951057940, win 5840, options [mss 1380,nop,nop,sackOK], length 0
```


#### AND Filter
- **Purpose**: Captures packets that meet all specified criteria.
- **Syntax**: `and [requirement]`
- **Example**: `sudo tcpdump -i eth0 host 192.168.0.1 and port 23`
    - **Output**: Shows traffic from host `192.168.0.1` on port `23` only.
    - **Details**:
        - Captures packets with both conditions: source host `192.168.0.1` and port `23`.
        - Example output shows TCP traffic on port 23.



#### OR Filter
- **Purpose**: Captures packets that meet at least one of the specified criteria.
- **Syntax**: `or` or `|| [requirement]`
- **Example**: `sudo tcpdump -r sus.pcap icmp or host 172.16.146.1`
    - **Output**: Shows ICMP traffic or traffic related to host `172.16.146.1`.
    - **Details**:
        - Displays packets matching either the ICMP condition or the host condition.
        - Example output includes ARP and ICMP traffic.


#### NOT Filter
- **Purpose**: Excludes packets that meet the specified criterion.
- **Syntax**: `not` or `! [requirement]`
- **Example**: `sudo tcpdump -r sus.pcap not icmp`
    - **Output**: Excludes ICMP traffic.
    - **Details**:
        - Displays all packets except those with ICMP protocol.
        - Example output includes ARP and HTTPS traffic.


#### Pre-Capture Filters
- **Application**: Applied during the capture process.
- **Function**: Drops any traffic not matching the filter criteria.
- **Impact**: Reduces the amount of data captured, which can be useful for focusing on specific issues, such as troubleshooting network connectivity problems.
- **Caveat**: May remove potentially valuable data that could be needed later. Best used when searching for specific patterns or issues.



#### Post-Capture Processing
- **Application**: Applied after capturing data, when reading from a capture file.
- **Function**: Filters and removes unwanted data from the terminal output without modifying the original capture file.
- **Impact**: Allows investigation of data without altering the captured file, preserving potentially useful information. Filters can be adjusted or cleared by rerunning the command with different syntax.



### Interpreting Tips and Tricks
- **-S Switch**: Displays absolute sequence numbers in TCP packets, which can be very long. Useful for cross-referencing with other tools or logs.
- **-v, -X, -e Switches**: Increase the amount of data captured.
- **-c, -n, -s, -S, -q Switches**: Reduce or modify the amount of data written and seen.
- **-A Switch**: Shows only ASCII text after the packet line, which helps in identifying human-readable content quickly.
- **-l Switch**: Enables line buffering, allowing output to be piped directly to other tools like `grep` for real-time analysis.


### Tcpdump Packet Filtering
- **Command Example**: `sudo tcpdump -Ar telnet.pcap`
    - Displays packet details and ASCII text from a capture file.
- **Filtering with Grep**:
    - Command: `sudo tcpdump -Ar http.cap -l | grep 'mailto:*'`
    - Utilizes `-l` for line buffering and `grep` to search for specific keywords in the packet data.
- **TCP SYN Flag Filtering**:
    - Command: `sudo tcpdump -i eth0 'tcp[13] & 2 != 0'`
    - Filters packets with the TCP SYN flag set by examining specific bytes in the TCP header.


#### Pre-Capture Filters
\
- **Application**: Applied during the capture process.
- **Function**: Drops any traffic not matching the filter criteria.
- **Impact**: Reduces the amount of data captured, which can be useful for focusing on specific issues, such as troubleshooting network connectivity problems.
- **Caveat**: May remove potentially valuable data that could be needed later. Best used when searching for specific patterns or issues.



#### Post-Capture Processing
- **Application**: Applied after capturing data, when reading from a capture file.
- **Function**: Filters and removes unwanted data from the terminal output without modifying the original capture file.
- **Impact**: Allows investigation of data without altering the captured file, preserving potentially useful information. Filters can be adjusted or cleared by rerunning the command with different syntax.


### Interpreting Tips and Tricks
- **-S Switch**: Displays absolute sequence numbers in TCP packets, which can be very long. Useful for cross-referencing with other tools or logs.
- **-v, -X, -e Switches**: Increase the amount of data captured.
- **-c, -n, -s, -S, -q Switches**: Reduce or modify the amount of data written and seen.
- **-A Switch**: Shows only ASCII text after the packet line, which helps in identifying human-readable content quickly.
- **-l Switch**: Enables line buffering, allowing output to be piped directly to other tools like `grep` for real-time analysis.



### Tcpdump Packet Filtering
- **Command Example**: `sudo tcpdump -Ar telnet.pcap`
    - Displays packet details and ASCII text from a capture file.
- **Filtering with Grep**:
    - Command: `sudo tcpdump -Ar http.cap -l | grep 'mailto:*'`
    - Utilizes `-l` for line buffering and `grep` to search for specific keywords in the packet data.
- **TCP SYN Flag Filtering**:
    - Command: `sudo tcpdump -i eth0 'tcp[13] & 2 != 0'`
    - Filters packets with the TCP SYN flag set by examining specific bytes in the TCP header.



### Protocol RFC Links
- **IP Protocol**: RFC 791
- **ICMP Protocol**: RFC 792
- **TCP Protocol**: RFC 793
- **UDP Protocol**: RFC 768
- **RFC Quick Links**: [Wikipedia RFC List](https://en.wikipedia.org/wiki/Request_for_Comments)


## Questions
- What filter will allow me to see traffic coming from or destined to the host with an ip of 10.10.20.1?
	- insert answer here
- What filter will allow me to capture based on either of two options?
	- or
- True or False: TCPDump will resolve IPs to hostnames by default.
	- True