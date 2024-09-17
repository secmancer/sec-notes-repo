Wireshark is a free and open-source network traffic analyzer with a graphical interface, offering advanced packet inspection capabilities. It is multi-platform and supports various interface types, including WiFi, USB, and Bluetooth. It can save traffic in multiple formats and provides detailed insights into network traffic.



#### Features and Capabilities:
- **Deep Packet Inspection**: Supports hundreds of different protocols.
- **Graphical and TTY Interfaces**: Provides both GUI and command-line options.
- **Cross-Platform**: Compatible with most operating systems.
- **Protocol Support**: Includes Ethernet, IEEE 802.11, PPP/HDLC, ATM, Bluetooth, USB, Token Ring, Frame Relay, FDDI, and more.
- **Decryption Capabilities**: Supports IPsec, ISAKMP, Kerberos, SNMPv3, SSL/TLS, WEP, WPA/WPA2, etc.


#### Requirements for Use:
**Windows:**
- **Universal C Runtime**: Included with Windows 10 and Windows Server 2019; otherwise, install KB2999226 or KB3118401.
- **Processor**: Any modern 64-bit AMD64/x86-64 or 32-bit x86.
- **RAM**: 500 MB available; larger capture files require more RAM.
- **Disk Space**: 500 MB available; additional space for capture files.
- **Display**: 1280 × 1024 or higher resolution recommended; supports HiDPI/Retina resolutions.
- **Network Card**:
    - **Ethernet**: Any supported Windows network card.
    - **802.11**: Special equipment may be required for raw capture.
**Linux:**
- **Compatibility**: Runs on most UNIX and UNIX-like platforms, including Linux and BSD variants.
- **Package Availability**: Binary packages available for most distributions.
- **Validation**: Use the following command to check if the package is installed:
```
dpkg -l | grep wireshark
```
or
```
rpm -qa | grep wireshark
```



#### Installation:
- **Windows**: Download from [wireshark.org](https://www.wireshark.org), validate the hash, and install.
- **Linux**: Use package managers like `apt`, `yum`, or `dnf` depending on your distribution.



#### Locating Wireshark
To check if Wireshark is installed and find its location, use the following command:
```
which wireshark
```
If Wireshark is not found, it is often located in `/usr/sbin/wireshark`.



#### Installing Wireshark on Linux
If Wireshark is not installed, you can install it using your package manager. For Debian-based distributions (like Ubuntu), use:
```
sudo apt install wireshark
```





### TShark vs. Wireshark (Terminal vs. GUI)
#### Overview
- **TShark**: A terminal-based tool based on Wireshark. It shares many of Wireshark’s features and syntax, making it suitable for environments without a graphical desktop. TShark is ideal for scripting and automation, as it can easily pass capture data to other command-line tools.
- **Wireshark**: A graphical interface for network traffic capture and analysis. It provides a rich set of features for detailed inspection and is best used in environments with a desktop interface for a full-featured experience.



#### Basic TShark Switches

| Switch Command   | Result                                                                     |
| ---------------- | -------------------------------------------------------------------------- |
| `-D`             | Display available interfaces for capture and exit.                         |
| `-L`             | List Link-layer mediums available for capture and exit. (e.g., ethernet)   |
| `-i`             | Choose an interface to capture from. (e.g., `-i eth0`)                     |
| `-f`             | Apply a packet filter in libpcap syntax during capture.                    |
| `-c`             | Capture a specific number of packets, then exit. Defines a stop condition. |
| `-a`             | Define an autostop condition (duration, file size, or packet count).       |
| `-r (pcap-file)` | Read from a capture file.                                                  |
| `-W (pcap-file)` | Write to a file using the pcapng format.                                   |
| `-P`             | Print packet summary while writing to a file. (`-W` required)              |
| `-x`             | Add Hex and ASCII output to the capture.                                   |
| `-h`             | Display the help menu.                                                     |


#### Additional Resources
To see the full list of switches you can utilize, refer to the TShark help menu:
```
tshark -h
```



### TShark Basic Usage
#### Locating TShark
- **Find TShark**:
```
secmancer@htb[/htb]$ which tshark
```
- **List Available Interfaces**:
```
secmancer@htb[/htb]$ tshark -D
```



#### Basic Capture Commands
- **Capture Packets**:
```
secmancer@htb[/htb]$ tshark -i 1 -w /tmp/test.pcap
```
- `-i 1`: Specify the interface to capture from (interface number `1` in this example).
- `-w /tmp/test.pcap`: Write captured packets to the specified file (`/tmp/test.pcap`).
- **Example Output**:
```
Capturing on 'Wi-Fi: en0'
484
```




#### Using Filters and Analyzing Captures
- **Filters**: TShark can apply filters for protocols, hosts, ports, and dissect individual fields from packets, similar to TCPDump. Filters use BPF (Berkeley Packet Filter) syntax.
- **Read from a Capture File**:
```
secmancer@htb[/htb]$ tshark -r /tmp/test.pcap
```
- `-r /tmp/test.pcap`: Read packets from the specified file.
- **Print Packet Summaries While Writing**:
```
secmancer@htb[/htb]$ tshark -w /tmp/test.pcap -P
```
- `-P`: Print packet summaries while writing out to a file. (Requires `-w` to specify the output file).



### Applying Filters with TShark
**Example Command**
- **Capture Traffic from a Specific Host**:
```
sudo tshark -i eth0 -f "host 172.16.146.2"
```

#### Sample Output
- **Captured Packets**:
```
Capturing on 'eth0'
    1 0.000000000 172.16.146.2 → 172.16.146.1 DNS 70 Standard query 0x0804 A github.com
    2 0.258861645 172.16.146.1 → 172.16.146.2 DNS 86 Standard query response 0x0804 A github.com A 140.82.113.4
    3 0.259866711 172.16.146.2 → 140.82.113.4 TCP 74 48256 → 443 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM=1 TSval=1321417850 TSecr=0 WS=128
    4 0.299681376 140.82.113.4 → 172.16.146.2 TCP 74 443 → 48256 [SYN, ACK] Seq=0 Ack=1 Win=65535 Len=0 MSS=1436 SACK_PERM=1 TSval=3885991869 TSecr=1321417850 WS=1024
    5 0.299771728 172.16.146.2 → 140.82.113.4 TCP 66 48256 → 443 [ACK] Seq=1 Ack=1 Win=64256 Len=0 TSval=1321417889 TSecr=3885991869
    6 0.306888828 172.16.146.2 → 140.82.113.4 TLSv1 579 Client Hello
    7 0.347570701 140.82.113.4 → 172.16.146.2 TLSv1.3 2785 Server Hello, Change Cipher Spec, Application Data, Application Data, Application Data, Application Data
    8 0.347653593 172.16.146.2 → 140.82.113.4 TCP 66 48256 → 443 [ACK] Seq=514 Ack=2720 Win=63488 Len=0 TSval=1321417937 TSecr=3885991916
    9 0.358887130 172.16.146.2 → 140.82.113.4 TLSv1.3 130 Change Cipher Spec, Application Data
   10 0.359781588 172.16.146.2 → 140.82.113.4 TLSv1.3 236 Application Data
   11 0.360037927 172.16.146.2 → 140.82.113.4 TLSv1.3 758 Application Data
   12 0.360482668 172.16.146.2 → 140.82.113.4 TLSv1.3 258 Application Data
   13 0.397331368 140.82.113.4 → 172.16.146.2 TLSv1.3 145 Application Data
```


#### Notes on Filters
- **Using `-f`**:
    - The `-f` flag allows the application of BPF (Berkeley Packet Filter) syntax filters to the capture.
    - In the example, the filter `host 172.16.146.2` was used to capture traffic involving the specified host.
- **Filter Options**:
    - TShark supports various filters recognized by Wireshark, allowing for detailed traffic inspection and analysis.


### Termshark
**Overview**:
- Termshark is a Text-based User Interface (TUI) application that provides a Wireshark-like interface within your terminal window.


**Getting Termshark**:
- **Website**: [Termshark](https://github.com/gcla/termshark)
- **Installation**:
    - **Build from Source**: Clone the repository from GitHub.
    - **Stable Releases**: Download a stable release from [Termshark Releases](https://github.com/gcla/termshark/releases), extract the file, and start using it.


**Starting Termshark**:
- Similar to TShark or tcpdump, you can specify an interface, filters, and other settings from the terminal.
- The Termshark window will appear once it detects traffic according to the capture filter. If it doesn't show up immediately, wait for traffic to trigger its display.



**Navigating Termshark**:
- Refer to the Termshark help and user interface guide provided on the Termshark website or repository for detailed navigation and usage instructions.



### Wireshark GUI Walkthrough
**Overview**: Wireshark provides a detailed graphical interface for packet capture and analysis, organized into three main panes and offering various features and controls.



**Three Main Panes**:
1. **Packet List (Orange)**:
    - **Description**: Displays a summary line for each packet.
    - **Default Columns**:
        - **Number**: Order in which packets arrived.
        - **Time**: Timestamp in Unix time format.
        - **Source**: Source IP address.
        - **Destination**: Destination IP address.
        - **Protocol**: Protocol used (e.g., TCP, UDP, DNS).
        - **Information**: Details about the packet, which varies depending on the protocol (e.g., DNS query type).
2. **Packet Details (Blue)**:
    - **Description**: Provides a detailed breakdown of the packet, showing various protocols and encapsulation layers.
    - **Display**: Information is shown in reverse OSI model order, with lower layers at the top and higher layers at the bottom.
3. **Packet Bytes (Green)**:
    - **Description**: Shows packet contents in ASCII or hexadecimal format.
    - **Highlighting**: Selection in the Packet Details pane will highlight corresponding bytes in this window.
    - **Format**: Each line shows data offset, sixteen hexadecimal bytes, and sixteen ASCII bytes. Non-printable bytes are displayed as periods.



**Other Notable Features**:
- **Control Points**: Various options and radial buttons in the Wireshark interface allow modifications to the view and packet analysis.
- **Capture and Display Filters**: Options available to refine packet captures and views. Changing capture options will restart the trace.



**Starting a Capture**:
1. **Steps**: Initiate capture through the Wireshark interface as shown in the provided steps or GIF.
2. **Restart on Options Change**: Note that any change to capture options will restart the trace.


### The Basics
**The Toolbar**:
- **Description**: The Toolbar is a central feature in Wireshark for managing various functions and settings.
- **Functions**:
    - **Start and Stop Captures**: Begin or halt the packet capture process.
    - **Change Interfaces**: Select different network interfaces for capturing data.
    - **Open and Save Files**: Manage capture files, including opening existing files and saving new ones.
    - **Apply Filters**: Set and modify capture and display filters.
    - **Analysis Add-ins**: Access additional tools and features for advanced analysis.



**How to Save a Capture**:
1. **Saving Method**:
    - **Option 1**: Go to `File` in the menu bar and select `Save`.
    - **Option 2**: Use the Toolbar's file option to choose the save location and format.
2. **Formats**:
    - **Default Format**: `.pcap` (Packet Capture) is commonly used and suitable for most scenarios.
    - **Other Formats**: Wireshark supports multiple capture file formats, so choose the appropriate format based on your needs.



**Capture and Display Filters**:
- **Capture Filters**: Applied before starting the capture. They use BPF (Berkeley Packet Filter) syntax and will drop any traffic not explicitly meeting the criteria. Useful for narrowing down the data written to disk.
- **Display Filters**: Applied during or after capture. They use Wireshark’s proprietary syntax and allow for detailed analysis of captured packets. Useful for filtering data after capture to focus on specific traffic.



**Handling Large Captures**:
- Wireshark may struggle with large captures, taking time to apply filters and perform analysis. For very large `.pcap` files, consider breaking them into smaller chunks to improve performance.



**Capture Filters**:
- **Usage**: Set before starting the capture.
- **Syntax**: Similar to TCPDump using BPF syntax.




**Common Capture Filters**:

|Filter|Result|
|---|---|
|`host x.x.x.x`|Capture only traffic related to a specific host.|
|`net x.x.x.x/24`|Capture traffic to/from a specific network (subnet mask specified).|
|`src net x.x.x.x/24`|Capture traffic from a specified network.|
|`dst net x.x.x.x/24`|Capture traffic to a specified network.|
|`port #`|Capture traffic on a specific port.|
|`not port #`|Capture all traffic except that on the specified port.|
|`port # and #`|Capture traffic on both specified ports.|
|`portrange x-x`|Capture traffic on all ports within the specified range.|
|`ip / ether / tcp`|Capture traffic for specific protocol headers.|
|`broadcast / multicast / unicast`|Capture specific types of traffic: broadcast, multicast, or unicast.|


**Applying Capture Filters**:
1. Click the capture radial at the top of the Wireshark window.
2. Select `Capture Filters` from the drop-down.
3. Modify or add filters as needed.
4. Click `Options` from the capture radial, and select or type the desired filter under `Capture filter for selected interfaces`.


**Display Filters**:
- **Usage**: Applied during or after the capture to refine the view of the data.




**Common Display Filters**:

|Filter|Result|
|---|---|
|`ip.addr == x.x.x.x`|Display traffic related to a specific host (OR statement).|
|`ip.addr == x.x.x.x/24`|Display traffic for a specific network (OR statement).|
|`ip.src == x.x.x.x`|Display traffic from a specific source host.|
|`ip.dst == x.x.x.x`|Display traffic to a specific destination host.|
|`dns / tcp / ftp / arp / ip`|Filter traffic by specific protocols.|
|`tcp.port == x`|Filter by a specific TCP port.|
|`tcp.port / udp.port != x`|Capture all traffic except the specified port.|
|`and / or / not`|Logical operators to combine or exclude filters.|


**Applying Display Filters**:
1. In the main Wireshark capture window, use the bookmark in the Toolbar or type the filter directly into the text field.
2. If the field turns green, the filter syntax is correct.



**Note**:
- **Capture Filters vs. Display Filters**: Capture filters drop traffic that doesn't meet criteria before saving, while display filters reprocess captured data to show only what matches the filter. Ports can be used for different purposes, so filtering by port is not the same as filtering by protocol.


## Questions
- True or False: Wireshark can run on both Windows and Linux.\
	- True
- Which Pane allows a user to see a summary of each packet grabbed during the capture?
	- Packet List
- Which pane provides you insight into the traffic you captured and displays it in both ASCII and Hex?
	- Packet Bytes
- What switch is used with TShark to list possible interfaces to capture on?
	- -D
- What switch allows us to apply filters in TShark?
	- -f
- Is a capture filter applied before the capture starts or after? (answer before or after)
	- before