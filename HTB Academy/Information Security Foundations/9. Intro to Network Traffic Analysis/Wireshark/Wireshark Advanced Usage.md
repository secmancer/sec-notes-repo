Wireshark offers advanced capabilities through various plugins and tools for detailed network analysis. Here’s a breakdown of some advanced features:



#### **Plugins and Advanced Analysis**
1. **Statistics Tab**
    - Provides detailed reports on network traffic.
    - Offers insights into:
        - Top talkers in the network.
        - Traffic breakdown by IP and protocol.
2. **Analyze Tab**
    - Contains tools for:
        - Following TCP streams.
        - Filtering and analyzing specific conversations.
        - Creating new packet filters.
        - Reviewing expert information about the traffic.



#### **Following TCP Streams**
- **Purpose:** Reconstruct and view entire TCP conversations.
- **Steps:**
    1. Right-click on a packet in the desired stream.
    2. Select `Follow` → `TCP Stream`.
    3. A new window will open with the reconstructed TCP conversation.
- **Alternative Method:** Use the filter `tcp.stream eq #` to find and track specific TCP streams.
    



#### **Extracting Data and Files**
- **Purpose:** Recover files and data from captured streams.
- **Requirements:** Must capture the entire conversation to accurately reconstruct files.
- **Steps:**
    1. Stop the capture.
    2. Navigate to `File` → `Export` and select the protocol format (e.g., DICOM, HTTP, SMB).
- **FTP Data Extraction:**
    - FTP uses TCP (port 20 for data, port 21 for control).
    - **Filters:**
        - `ftp`: Displays all FTP protocol data.
        - `ftp.request.command`: Shows commands sent over port 21, such as login details.
        - `ftp-data`: Displays data transferred over port 20.


    **Steps to Extract FTP Data:**
    1. Apply the `ftp` filter to view FTP traffic.
    2. Use `ftp.request.command` to identify file transfers and related commands.
    3. Filter for `ftp-data`, follow the TCP stream, and save the data as raw files.
    4. Verify and validate the extracted files by checking their types.


## Questions
- Which plugin tab can provide us with a way to view conversation metadata and even protocol breakdowns for the entire PCAP file?
	- Statistics
- What plugin tab will allow me to accomplish tasks such as applying filters, following streams, and viewing expert info?
	- Analyze
- What stream oriented Transport protocol enables us to follow and rebuild conversations and the included data?
	- TCP
- True or False: Wireshark can extract files from HTTP traffic.
	- True
- True or False: The ftp-data filter will show us any data sent over TCP port 21.
	- False