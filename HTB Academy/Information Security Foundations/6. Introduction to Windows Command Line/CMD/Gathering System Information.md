#### Importance of Gathering System Information
- **Host enumeration** refers to collecting details about a system and its environment.
- This is a fundamental concept for both Systems Administrators (Blue Team) and Penetration Testers (Red Team).

#### Why is System Information Important?
- **Red Team** (Penetration Testers, Hackers, Red Team Operators):
    
    - Helps identify vulnerable services, misconfigurations, or machines that can be exploited.
    - Assists in understanding the network layout to craft targeted attacks.
- **Blue Team** (System Administrators, SOC Analysts):
    - Helps in diagnosing issues, securing systems, and maintaining network integrity.
    - Identifies potential weaknesses and ensures systems are properly configured.

#### Key Questions in System Enumeration:
1. **What information can we gather from the host?**
    - System hardware details (CPU, memory, disk space).
    - Network configuration and active connections.
    - Installed software and services running on the system.
    - User accounts and permissions.
2. **Why do we need this information?**
    - Provides insight into system vulnerabilities and misconfigurations.
    - Enables effective troubleshooting, security, and optimization of systems.
    - Forms a basis for understanding the environment before taking further action.
3. **How can we gather this information using Command Prompt?**
    - Using built-in Windows commands and tools like `systeminfo`, `ipconfig`, `netstat`, and `tasklist`.

#### General Methodology for Gathering System Information:
1. **Identify key areas of interest**: Focus on gathering details on hardware, network configuration, running services, and user accounts.
2. **Use appropriate commands**: Leverage system commands (e.g., `systeminfo`, `ipconfig`) for gathering specific types of information.
3. **Organize and analyze**: Ensure the collected data is structured and analyzed to understand the environment better.


#### Importance of Having a Plan
- Gaining initial access to a system without a structured plan for information gathering can lead to wasted time and confusion.
- Host enumeration provides an overall picture of the target host, its environment, and its interactions with other systems across the network.


#### Key Question: How Do We Know What to Look For?
- Understanding what types of information are available on a system is crucial for successful enumeration.
- The process involves identifying important data points to give structure to the enumeration process and avoid information overload.

![[InformationTypesChart_Updated.png]]

#### Types of Information to Gather (for Windows Systems):
1. **General System Information**:
    - Includes details like hostname, OS name and version, system configuration, installed patches, and hotfixes.
2. **Networking Information**:
    - Covers host IP addresses, network interfaces, subnets, DNS servers, known hosts, and accessible network resources.
3. **Basic Domain Information**:
    - Focuses on Active Directory (AD) information related to the domain the target system belongs to.
4. **User Information**:
    - Encompasses local users and groups, environment variables, running tasks, scheduled tasks, and services accessible to specific user accounts.

![[Screenshot_20240915_194444.png]]
#### Methodology for Host Enumeration:
- Use the following questions to guide your enumeration and gather relevant information efficiently:
    1. **What system information can we pull from the target host?**
    2. **What other systems is the target host interacting with over the network?**
    3. **What user accounts are accessible, and what data or tasks can we access from these accounts?**


#### Benefits of This Approach:
- Provides **situational awareness** by helping to focus on the most critical pieces of information.
- Prevents information overload and wasted effort on irrelevant data.
- Helps in developing a clearer methodology for enumeration during actual engagements.


#### Purpose of Gathering System Information
- **Objective**: Host enumeration provides a starting point and guide for attacking the system, especially in scenarios like assumed breach engagements where initial access is obtained with a potentially unprivileged user account.


#### Importance of Thorough Enumeration
- **Understanding Environment**:
    - **User Account**: Know which user account has been compromised.
    - **User Groups**: Determine the groups the user belongs to.
    - **Privileges**: Assess the current privileges associated with the user account.
    - **Network Resources**: Identify accessible network resources.
    - **Tasks and Services**: Review what tasks and services are running under the user account.


#### Example Scenario
- **Assumed Breach**: If provided initial access through an unprivileged account, the goal is to escalate privileges to gain administrative access.
- **Thorough Understanding**: Before attempting privilege escalation, it’s crucial to gather comprehensive information about the environment to understand potential attack vectors.


#### Risks of Insufficient Enumeration
- **Missed Opportunities**: Focusing solely on known vulnerabilities (e.g., CVEs) may overlook human errors or configuration issues that could be exploited.
- **System Complexity**: Human configuration errors and environmental nuances might be more significant than surface-level vulnerabilities.


#### Best Practices
- **Guided Structure**: Follow a structured approach to enumeration to ensure all relevant information is gathered.
- **Avoid Haphazard Exploitation**: Prioritize thorough information gathering over reckless attempts to exploit the system.


CMD provides a variety of commands to gather detailed system and network information. This is crucial for both sysadmins for troubleshooting and hackers for reconnaissance. Using these commands effectively can help in diagnosing issues or planning further actions while minimizing detection.


#### System Information with `systeminfo`
- **Command:** `systeminfo`
- **Purpose:** Provides comprehensive information about the host, including:
    - Hostname
    - OS Name and Version
    - Build Version
    - Domain membership
    - Installed hotfixes
    - System configuration details
**Example Output:**
```
Host Name:                 DESKTOP-htb
OS Name:                   Microsoft Windows 10 Pro
OS Version:                10.0.19042 N/A Build 19042
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Multiprocessor Free
```
- **Use Case:** Ideal for a quick overview of the system to understand the environment and identify potential vulnerabilities.



#### Basic System Information
- **Hostname:**
    - **Command:** `hostname`
    - **Purpose:** Displays the hostname of the machine.
    **Example Output:**
```
DESKTOP-htb
```
- **OS Version:**
	- **Command:** `ver`
	- **Purpose:** Shows the current operating system version.
**Example Output:**
```
Microsoft Windows [Version 10.0.19042.2006]
```
- **Use Case:** Useful for quickly retrieving basic system details without using `systeminfo`.


#### Network Information
- **IP Configuration:**
    - **Command:** `ipconfig`
    - **Purpose:** Displays TCP/IP network configurations, including:
        - Domain Name
        - IPv4 Address
        - Subnet Mask
        - Default Gateway
    **Example Output:**
```
Windows IP Configuration
Ethernet adapter Ethernet:
   IPv4 Address: 10.0.25.17
   Subnet Mask: 255.255.255.0
   Default Gateway: 10.0.25.1
```
**Full Configuration:** `ipconfig /all`
- Provides detailed information including MAC Address, DHCP settings, and DNS Servers.


**ARP Cache:**
- **Command:** `arp /a`
- **Purpose:** Displays the Address Resolution Protocol (ARP) cache, showing IP-to-MAC address mappings.
**Example Output:**
```
Interface: 10.0.25.17 --- 0x17
  Internet Address      Physical Address      Type
  10.0.25.1             00-e0-67-15-cf-43     dynamic
```
**Use Case:** Understanding network connectivity and discovering additional hosts.


#### User and Privilege Information
- **Current User:**
    - **Command:** `whoami`
    - **Purpose:** Displays the current logged-in user and domain information.  
    **Example Output:**
```
ACADEMY-WIN11\htb-student
```
**User Privileges:**
- **Command:** `whoami /priv`
- **Purpose:** Shows the privileges assigned to the current user.
**Example Output:**
```
Privilege Name                Description                          State
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled
```
**User Groups:**
- **Command:** `whoami /groups`
- **Purpose:** Lists all groups the current user is a member of.
**Example Output:**
```
Group Name                             Type             SID          Attributes
Everyone                               Well-known group S-1-1-0      Mandatory group, Enabled by default
BUILTIN\Users                          Alias            S-1-5-32-545 Mandatory group, Enabled by default
```
**Use Case:** Identifying user privileges and group memberships for assessing access and potential escalation paths.


#### Network Shares
- **Local Shares:**
    - **Command:** `net share`
    - **Purpose:** Displays shared resources on the local host.
    **Example Output:**
```
Share name   Resource                        Remark
C$           C:\                             Default share
Records      D:\Important-Files              Mounted share for records storage
```
**Network Shares:**
- **Command:** `net view`
- **Purpose:** Shows shared resources visible to the host, including domain resources, shares, and printers.
**Example Output:**
```
Server Name   Share Name
\\SERVER1     SharedDocs
\\SERVER2     Public
```
**Use Case:** Finding accessible network shares for data collection or persistence.


**Key Concept**: System-level access isn't necessary on every host during a pentest, unless specifically required by the assessment. Focus should be on the end goal, not just privilege escalation on every machine.



**CMD Usage for Limited Resources**:
- Command-line tools such as `net` commands and basic CMD operations can be useful for lateral movement and information gathering.
- While effective, these actions are noisy and easily detectable by a blue team monitoring network traffic and system logs.


**Operational Noise**:
- Using CMD excessively during an assessment will generate a lot of logs, making it easier for defenders to spot unusual activity.
- Endpoints and detection systems like EDR (Endpoint Detection and Response) or NIDS (Network Intrusion Detection Systems) will likely notice CMD usage if properly configured.


**Environment Considerations**:
- Regular users don’t typically use CMD prompts, and even administrators have limited reasons to execute `cmd.exe` often.
- Net commands in particular stand out in most environments and can serve as a red flag for potential infiltration, especially when monitoring and logging are enabled.


**Pentester Awareness**: 
- Always be mindful of the environment's defenses (EDR, NIDS, logging) and adjust tactics accordingly to avoid unnecessary detection while continuing with the assessment.


**Scope of Information**:
    - Understanding the breadth of information available on a system and its importance is crucial.
    - Efficiently gathering and utilizing this information is key to effective pentesting.


 **Mindset and Methodology**:
    - Developing a clear methodology for enumeration helps in systematically identifying what is needed and how to obtain it.
    - This approach aids in refining techniques and gaining a comprehensive understanding of the target environment.


**Value of Methodology**:
    - A solid enumeration methodology is an invaluable skill for pentesters, helping in organizing and streamlining the assessment process.


**Next Steps**:
    - Upcoming sections will build on the foundation laid in this part, with a focus on locating specific files and directories.
    - Continuation of the established mindset and methodology will be essential as the scope of exploration expands.


## Questions
- What command will output verbose system information such as OS configuration, security info, hardware info, and more?
	- systeminfo
- Access the target host and run the 'hostname' command. What is the hostname?
	- ICL-WIN11