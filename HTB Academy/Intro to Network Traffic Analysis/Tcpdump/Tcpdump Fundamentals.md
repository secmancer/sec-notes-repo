### Tcpdump Overview

- **Tcpdump**: A command-line packet sniffer that captures and interprets data frames from a file or network interface.
- **Compatibility**: Built for Unix-like operating systems with a Windows counterpart called WinDump, though support for WinDump has ceased.
- **Usability**: It doesn't require a GUI, making it usable through terminal or remote connections like SSH. Requires root or admin privileges.
- **Libraries**: Utilizes `pcap` and `libpcap` for capturing network traffic and interfaces in promiscuous mode.

### Key Features and Commands

- **Location & Installation**:
    
    - Check if Tcpdump is installed: `which tcpdump`
    - Install Tcpdump (if necessary): `sudo apt install tcpdump`
    - Validate installation: `sudo tcpdump --version`
- **Basic Capture Options**:
    
    - **-D**: Display available interfaces.
    - **-i [interface]**: Select an interface to capture from (e.g., `-i eth0`).
    - **-n**: Do not resolve hostnames.
    - **-nn**: Do not resolve hostnames or well-known ports.
    - **-e**: Capture Ethernet headers along with data.
    - **-X**: Show packet contents in both hex and ASCII.
    - **-v, -vv, -vvv**: Increase verbosity of output.
    - **-c [number]**: Capture a specific number of packets.
    - **-s [size]**: Define how much of a packet to capture.
    - **-S**: Use absolute sequence numbers.
    - **-q**: Print less protocol information.
    - **-r [file]**: Read from a file.
    - **-w [file]**: Write capture data to a file.
- **Using Tcpdump**:
    
    - **Listing Available Interfaces**: `sudo tcpdump -D`
    - **Selecting an Interface**: `sudo tcpdump -i eth0`
    - **Disable Name Resolution**: `sudo tcpdump -i eth0 -nn`
    - **Include Ethernet Header**: `sudo tcpdump -i eth0 -e`
    - **Include ASCII and Hex Output**: `sudo tcpdump -i eth0 -X`

### Additional Resources

- **Man Page**: Access the full list of Tcpdump switches with `man tcpdump`.

### Notes on Windows Compatibility

- **WinDump**: The Windows port of Tcpdump is no longer supported.
- **Alternative**: Running a Linux distribution through Windows Subsystem for Linux (WSL) is recommended to use Tcpdump on Windows systems.


### Questions
- Utilizing the output shown in question-1.png, who is the server in this communication? (IP Address)
	- 174.143.213.184
- Were absolute or relative sequence numbers used during the capture? (see question-1.zip to answer)
	- Relative
- If I wish to start a capture without hostname resolution, verbose output, showing contents in ASCII and hex, and grab the first 100 packets; what are the switches used? please answer in the order the switches are asked for in the question.
	-  -nvXc 100
- Given the capture file at /tmp/capture.pcap, what tcpdump command will enable you to read from the capture and show the output contents in Hex and ASCII? (Please use best practices when using switches)
	- sudo tcpdump -Xr /tmp/capture.pcap
- What TCPDump switch will increase the verbosity of our output? ( Include the - with the proper switch )
	- -v
- What built in terminal help reference can tell us more about TCPDump?
	- man
- What TCPDump switch will let me write my output to a file?
	- -w