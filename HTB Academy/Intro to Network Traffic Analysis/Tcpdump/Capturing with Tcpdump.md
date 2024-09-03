#### Purpose:

- Familiarize with tcpdump and the terminal.
- Practice tcpdump basics: reading from/writing to files, using basic switches, and locating files in the terminal.
- Explore and practice different switches and functionalities within tcpdump.
- Analyze visible network traffic and understand its significance.

#### Context:

- This lab helps examine specific hosts and servers to understand interactions, identify backdoors, and detect potential breaches.
- Tcpdump can monitor and log communication from a server for packet analysis using various filters and patterns, covered in another section.

#### Scenario:

- As the new network administrator, your task is to capture network traffic to baseline and validate the Corporation's network.
- Start by capturing local broadcast domain traffic to ensure the capture device works properly.
- Ensure necessary tools and dependencies are installed and test your ability to capture and read traffic into a file.

### Tasks

#### Task #1: Validate Tcpdump Installation

- **Objective**: Ensure tcpdump is installed on your machine.
- **Command**: Use a Linux command to check if tcpdump is installed or search for tcpdump on Windows.
- **Answer**: To check for tcpdump, use the command: `which tcpdump`.

#### Task #2: Start a Capture

- **Objective**: Begin capturing network traffic.
- **Tip**: If unsure of available interfaces, use a tcpdump switch to list them.
- **Answer**: The switch to list all possible interfaces is `-D`.

#### Task #3: Utilize Basic Capture Filters

- **Objective**: Modify traffic capture output by adding verbosity, and displaying content in ASCII and Hex.
- **Challenge**: Disable name resolution and display relative sequence numbers.
- **Answer**:
    - Verbosity switch: `-v`
    - Display in ASCII and Hex: `-X`
    - Disable name resolution: `-n`
    - Display relative sequence numbers: `-S`

#### Task #4: Save a Capture to a .PCAP File

- **Objective**: Capture and save traffic to a .PCAP file for network baselining.
- **Note**: Capture filters will modify the output.
- **Answer**: Use the command `tcpdump -w filename.pcap`.

#### Task #5: Read the Capture from a .PCAP File

- **Objective**: Read a .PCAP file into tcpdump and modify the view to understand the network traffic.
- **Tip**: Disable hostname and port resolution for simplicity, and ensure TCP sequence/acknowledgment numbers are in absolute values.
- **Answer**: Use the command `tcpdump -r filename.pcap`.

#### Final Step:

- Answer the questions at the bottom of the section to test your understanding.'

### Questions
- What TCPDump switch will allow us to pipe the contents of a pcap file out to another function such as 'grep'?
	- -l
- True or False: The filter "port" looks at source and destination traffic.
	- True
- If we wished to filter out ICMP traffic from our capture, what filter could we use? ( word only, not symbol please.)
	- not icmp
- What command will show you where / if TCPDump is installed?
	- which tcpdump
- How do you start a capture with TCPDump to capture on eth0?
	- tcpdump -i eth0
- What switch will provide more verbosity in your output?
	- -v
- What switch will write your capture output to a .pcap file?
	- -w
- What switch will read a capture from a .pcap file?
	- -r
- What switch will show the contents of a capture in Hex and ASCII?
	- -X