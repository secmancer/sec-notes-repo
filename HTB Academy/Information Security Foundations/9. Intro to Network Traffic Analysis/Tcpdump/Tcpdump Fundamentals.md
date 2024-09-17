**Overview:**
- **Tcpdump**: A command-line packet sniffer for capturing and interpreting data frames from a file or network interface.
- **Compatibility**: Designed for Unix-like systems; Windows had a port called WinDump (now unsupported).
- **Use Case**: Ideal for network traffic analysis without requiring a GUI.



**Functionality:**
- **Libraries**: Utilizes `pcap` and `libpcap` for capturing packets.
- **Promiscuous Mode**: Allows capturing of packets not specifically addressed to the host.

**Installation and Verification:**
- **Locate Tcpdump**:
```
which tcpdump
```
- Typically found in `/usr/sbin/tcpdump`.
- **Install Tcpdump** (if not installed):
```
sudo apt install tcpdump
```
**Check Version**:
```
sudo tcpdump --version
```
Example output: `tcpdump version 4.9.3`, `libpcap version 1.9.1`, `OpenSSL 1.1.1f`
**Basic Commands and Options:**
- **List Interfaces**:
```
sudo tcpdump -D
```
- Lists available network interfaces.
**Capture Traffic on a Specific Interface**:
```
sudo tcpdump -i eth0
```
**Disable Name Resolution**:
```
sudo tcpdump -i eth0 -nn
```
**Include Ethernet Header**:
```
sudo tcpdump -i eth0 -e
```
**Display Packet Contents in Hex and ASCII**:
```
sudo tcpdump -i eth0 -X
```
**Combine Options for Detailed Output**:
```
sudo tcpdump -i eth0 -nnvXX
```



**Usage Examples:**
- **Listing Available Interfaces**:
```
sudo tcpdump -D
```
Example output includes interfaces like `eth0`, `lo`, `bluetooth0`, etc.
**Capturing Traffic**:
```
sudo tcpdump -i eth0
```
**Detailed Output with Headers**:
```
sudo tcpdump -i eth0 -e
```
**Hex and ASCII Output**:
```
sudo tcpdump -i eth0 -X
```



**Man Pages:**
- Access complete list of switches and options:
```
man tcpdump
```


**Additional Notes:**
- Tcpdump is a powerful tool but can be complex due to its numerous functions and filters.
- Requires root or administrator privileges, often via `sudo`.
- On Windows, consider using a Linux distribution via Windows Subsystem for Linux (WSL) for similar functionality.



**Usage Tips:**
- Familiarize yourself with basic switches and options to make efficient use of Tcpdump.
- Combine switches to tailor the output to specific needs (e.g., `-nnvXX` for detailed packet info).



## Questions
- Utilizing the output shown in question-1.png, who is the server in this communication? (IP Address)
	- 174.143.213.184
- Were absolute or relative sequence numbers used during the capture? (see question-1.zip to answer)
	- Relative
- If I wish to start a capture without hostname resolution, verbose output, showing contents in ASCII and hex, and grab the first 100 packets; what are the switches used? please answer in the order the switches are asked for in the question.
	- -nvXc 100
- Given the capture file at /tmp/capture.pcap, what tcpdump command will enable you to read from the capture and show the output contents in Hex and ASCII? (Please use best practices when using switches)
	- sudo tcpdump -Xr /tmp/capture.pcap
- What TCPDump switch will increase the verbosity of our output? ( Include the - with the proper switch )
	- -v
- What built in terminal help reference can tell us more about TCPDump?
	- man
- What TCPDump switch will let me write my output to a file?
	- -w