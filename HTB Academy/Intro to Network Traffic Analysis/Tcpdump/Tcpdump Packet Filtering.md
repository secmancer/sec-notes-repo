**Tcpdump Notes: Filtering and Advanced Syntax Options**

- **Tcpdump Filtering Overview**:
    
    - Tcpdump allows for robust data parsing using packet filters, which can modify capture output.
    - Advanced filters help reduce the traffic printed to output or saved to file, conserving disk space and improving buffer processing.
    - Filters can be used to capture specific traffic, such as packets from a particular host or with specific TCP header bits set.
- **Common Tcpdump Filters**:
    
    - **host**: Filters traffic involving the designated host (bi-directional).
    - **src / dest**: Modifiers to specify source or destination host or port.
    - **net**: Filters traffic from or destined to the specified network (uses / notation).
    - **proto**: Filters for specific protocol types (e.g., ether, TCP, UDP, ICMP).
    - **port**: Bi-directional filter for traffic with the specified port as source or destination.
    - **portrange**: Specifies a range of ports (e.g., 0-1024).
    - **less / greater**: Filters based on packet or protocol option size.
    - **and / &&**: Concatenates two filters (e.g., src host AND port).
    - **or**: Matches either of two conditions.
    - **not**: Excludes specified criteria (e.g., not UDP).
- **Examples**:
    
    - **Host Filter**:
        
        - Syntax: `host [IP]`
        - Example: `sudo tcpdump -i eth0 host 172.16.146.2`
        - Use: Examines traffic involving a specific host or server.
    - **Source/Destination Filter**:
        
        - Syntax: `src/dst [host|net|port] [IP|Network Range|Port]`
        - Example: `sudo tcpdump -i eth0 src host 172.16.146.2`
        - Use: Filters packets sent from or to a specific host, port, or network range.
    - **Source with Port Filter**:
        
        - Example: `sudo tcpdump -i eth0 tcp src port 80`
        - Use: Filters traffic with source port 80 (HTTP), showing only one side of the conversation.
    - **Destination with Net Filter**:
        
        - Example: `sudo tcpdump -i eth0 dest net 172.16.146.0/24`
        - Use: Filters traffic destined for the specified network.

### Protocol Filter

**Command Syntax:**

- `sudo tcpdump -i [interface] [protocol]`

**Example:**

- Capture only UDP traffic:
    - `sudo tcpdump -i eth0 udp`

### Protocol Number Filter

**Command Syntax:**

- `sudo tcpdump -i [interface] proto [protocol number]`

**Example:**

- Capture traffic using protocol number 17 (UDP):
    - `sudo tcpdump -i eth0 proto 17`

### Port Filter

**Command Syntax:**

- `sudo tcpdump -i [interface] tcp/udp port [port number]`

**Example:**

- Capture TCP traffic on port 443 (HTTPS):
    - `sudo tcpdump -i eth0 tcp port 443`

### Port Range Filter

**Command Syntax:**

- `sudo tcpdump -i [interface] portrange [start port]-[end port]`

**Example:**

- Capture traffic on ports 0 to 1024:
    - `sudo tcpdump -i eth0 portrange 0-1024`

### Packet Size Filter

**Command Syntax:**

- `sudo tcpdump -i [interface] less/greater [size in bytes]`

**Example:**

- Capture packets smaller than 64 bytes:
    - `sudo tcpdump -i eth0 less 64`

### Pre-Capture Filters vs. Post-Capture Processing

**Pre-Capture Filters:**

- Applied during live capture to reduce data by filtering out unwanted traffic.
- Only packets matching the filter criteria are captured.
- Ideal for focused troubleshooting or when disk space is limited.
- **Downside:** Irreversible; discarded packets cannot be recovered.

**Post-Capture Processing:**

- Filters are applied after capturing, allowing for analysis of the entire file.
- Preserves all data for future analysis or re-filtering.
- Suitable for detailed investigations where retaining all data is important.
- **Downside:** Requires more storage and processing power.

### Interpreting Tips and Tricks

- **-S Switch:** Shows absolute sequence numbers, useful for matching logs from other tools.
- **Verbose Switches:**
    - **-v, -X, -e:** Increase the detail level of the output for deeper analysis.
    - **-c, -n, -s, -S, -q:** Modify or reduce the output data for specific needs.
- **-A Switch:** Displays only ASCII text from packets, simplifying the readability of human-readable content.
- **-l Switch:** Enables line-buffered output, useful for piping data to tools like grep for quick searches.

### Tcpdump Packet Filtering Examples

- **Reading a Capture with ASCII Output:** Use `sudo tcpdump -Ar telnet.pcap` to view packet contents with ASCII values, making human-readable content more accessible.
    
- **Piping a Capture to Grep:** Use `sudo tcpdump -Ar http.cap -l | grep 'mailto:*'` to search for email addresses in the capture file, quickly filtering the output.
    
- **Filtering TCP SYN Flags:** Use `sudo tcpdump -i eth0 'tcp[13] &2 != 0'` to find packets with the TCP SYN flag set, useful for identifying new TCP connections.
    

### Additional Resources

- **IP Protocol:** RFC 791
- **ICMP Protocol:** RFC 792
- **TCP Protocol:** RFC 793
- **UDP Protocol:** RFC 768
- **Wikipedia - RFC List:** Comprehensive list of protocols and their RFCs


### Questions
- What filter will allow me to see traffic coming from or destined to the host with an ip of 10.10.20.1?
	- 
- What filter will allow me to capture based on either of two options?
	- or
- True or False: TCPDump will resolve IPs to hostnames by default.
	- True
