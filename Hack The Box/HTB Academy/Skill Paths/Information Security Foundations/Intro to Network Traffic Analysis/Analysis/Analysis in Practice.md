### Introduction
- The previous section covered network traffic analysis, its dependencies, and importance.
- This section will outline a workflow for performing traffic analysis and introduce key components.
- Traffic analysis is not an exact science; it is dynamic and varies based on what we're investigating (e.g., errors vs. malicious activity) and network visibility.
- The analysis process can be broken down into fundamental principles, though.


## Descriptive Analysis
- Descriptive analysis is crucial for identifying data set characteristics, detecting errors, and identifying outliers.
- Key steps in descriptive analysis:
    1. **Identify the issue** – Is it a suspected breach or a networking issue?
    2. **Define scope and goals** – What are we looking for, and which time period?
        - Example: Multiple hosts downloading malicious files from bad.example.com in the last 48 hours + 2 hours.
        - Supporting info: Filenames/types like 'superbad.exe' or 'new-crypto-miner.exe'.
    3. **Define targets** – Network, hosts, or protocols involved.
        - Scope: 192.168.100.0/24 network, HTTP and FTP protocols.
- Descriptive analysis helps clarify these components and ensures a structured approach to network analysis.


## Diagnostic Analysis
- Diagnostic analysis focuses on understanding the causes, effects, and interactions of conditions through correlations and interpretation.
- Key steps in diagnostic analysis:
    1. **Capture network traffic** – Use a link with access to the 192.168.100.0/24 network to capture live traffic, pulling PCAP/netflow data from the SIEM for historical data.
    2. **Identify required network traffic components (filtering)** – Filter out irrelevant traffic, focusing on HTTP and FTP from the subnet, with GET requests for suspected executables.
    3. **Understand captured network traffic** – Analyze filtered traffic to identify files transferred (e.g., `ftp-data`) and GET requests matching filenames, helping track transfers and internal network activity.
- By capturing, filtering, and analyzing traffic, we validate the cause of the issue through diagnostic analysis, examining events and interactions.


## Predictive Analysis
- Predictive analysis uses historical and current data to create models for future probabilities, identifying trends and deviations to anticipate future occurrences.
- Key steps in predictive analysis:
    1. **Note-taking and mind mapping** – Document all findings, including traffic timeframes, suspicious hosts, and packet-level details, such as conversations containing the targeted files.
    2. **Summary of the analysis** – Summarize findings in detail for decision-making, helping superiors decide on quarantine or further incident response.
- By evaluating data against baselines and identifying markers of potential threats (like malicious signatures), predictive analysis helps ensure appropriate actions are taken in response.


## Prescriptive Analysis
- Prescriptive analysis focuses on determining the actions needed to eliminate or prevent future issues.
- Steps for prescriptive analysis:
    1. **Identify the issue** – Suspected breach or networking issue?
    2. **Define scope and goal** – Identify hosts downloading malicious files (e.g., ‘superbad.exe’ and ‘new-crypto-miner.exe’) within the last 48 hours + 2 hours.
    3. **Define targets** – 192.168.100.0/24 network, HTTP and FTP protocols.
    4. **Capture network traffic** – Use access to capture live traffic, extract PCAP/netflow data from the SIEM.
    5. **Filter network traffic** – Remove irrelevant traffic, focusing on HTTP/FTP with GET requests for suspected files.
    6. **Analyze captured traffic** – Identify and filter files transferred, examining HTTP and FTP requests to reconstruct and trace activity.
    7. **Note-taking and mind mapping** – Document all findings, including timestamps, packet numbers, and suspicious hosts.
    8. **Summary of findings** – Clearly summarize findings, providing detailed reports for decision-making (e.g., quarantining hosts or further incident response).
- This process is often iterative, requiring revisiting and reanalyzing previous steps for larger, more complex incidents.


## Key Components of an Effective Analysis
- #### 1. Know your environment
	- **Know the environment** – Understanding the network topology, asset inventories, and network maps is essential for effective traffic analysis.
	- **Identify rogue hosts** – If unsure whether a host belongs to the network, compare it against asset inventories and network maps to determine if it is rogue.
	- **Centralized visibility** – Ensuring complete visibility into network traffic is critical for identifying unusual or suspicious activity.
- #### 2. Placement is Key
	- **Placement of capture tools** – Positioning capture tools as close to the source of the issue as possible ensures visibility into the relevant traffic.
	- **Inbound links** – Capturing traffic near inbound links helps identify external sources and get the full picture of the issue.
	- **Internal network issues** – If the problem is isolated to a single host, placing capture tools within the same network segment helps monitor internal traffic related to the issue.
- #### 3. Persistence
	- **Persistence** – The issue may not always be immediately visible and could occur sporadically, e.g., Command and Control (C2) communications occurring infrequently (e.g., once per hour or day).
	- **Importance of continuous monitoring** – If the issue is missed initially, further attacks could go unnoticed until a full-scale breach occurs, such as a ransomware attack.
	- **Perseverance** – Staying persistent in monitoring and investigation can help detect and prevent attacks that would otherwise go unnoticed.


## Analysis Approach
- **Standard Protocols First** – Start with common protocols like HTTP/S, FTP, email, TCP/UDP, SSH, RDP, Telnet, and clear out unnecessary traffic before moving on to more specific, less common protocols.
- **Identify Patterns** – Look for patterns like regular, daily check-ins or C2 profiles from specific hosts, as these can signal malicious activity.
- **Host-to-Host Traffic** – Be suspicious of host-to-host traffic, as typical setups rarely involve direct communication between user hosts.
- **Unique Events** – Pay attention to unusual or anomalous behavior like different User-Agent strings, random port usage, or deviations from expected traffic patterns.
- **Ask for Help** – Collaboration can help spot overlooked threats, especially when staring at data for extended periods.
- **Utilize Tools** – Use tools like tcpdump, Wireshark, Snort, Security Onion, Firewalls, and SIEMs to enrich traffic analysis and strengthen network defenses.