#### Types of Information to Gather

1. **System Information**
    
    - **OS Version:** Understand which operating system and version are in use. This can help identify specific vulnerabilities or configurations.
    - **Architecture:** Determine if the system is 32-bit or 64-bit, which affects compatibility and security considerations.
    - **Hostname:** Identify the name of the system on the network.
    - **System Uptime:** Check how long the system has been running since the last reboot.
2. **User Information**
    
    - **Current User:** Identify the currently logged-in user and their permissions.
    - **User Accounts:** List all user accounts on the system, including administrative and non-administrative accounts.
    - **Groups:** Understand user group memberships, which can impact permissions and access control.
3. **Network Information**
    
    - **IP Address:** Find the system's IP address, which is crucial for network interactions.
    - **Network Configuration:** Details about network interfaces, routing tables, and DNS settings.
    - **Open Ports:** Identify open ports and associated services that may be running on the system.
4. **System Services**
    
    - **Running Processes:** List all active processes to understand what applications and services are currently in use.
    - **Services:** Check which services are running, their status, and their configurations.
5. **File System Information**
    
    - **Disk Usage:** Assess disk space usage and available space.
    - **File and Directory Listing:** Review files and directories to identify sensitive or important data.
6. **Security Information**
    
    - **Firewall Status:** Check if the firewall is enabled and its configuration.
    - **Antivirus Status:** Determine if antivirus software is installed and active.

#### Importance of Thorough Enumeration

- **Vulnerability Identification:** Helps in finding unpatched software, insecure configurations, and other vulnerabilities that could be exploited.
- **Security Assessment:** Assists in evaluating the security posture of the system, including user privileges and system configurations.
- **Troubleshooting:** Provides essential information for diagnosing system issues and ensuring proper functionality.
- **Compliance:** Helps in ensuring that the system complies with security policies and standards.

#### General Methodology

1. **Start with Basic Information:**
    
    - Use commands to gather basic system information such as OS version, architecture, and hostname.
2. **Check User Accounts and Permissions:**
    
    - List users and their permissions to understand access levels and potential risks.
3. **Gather Network Details:**
    
    - Identify IP addresses, network configurations, and open ports to map out network interactions.
4. **Examine System Services and Processes:**
    
    - Review active processes and services to understand what is running on the system.
5. **Inspect File System and Security Settings:**
    
    - Check disk usage, file system details, and security settings to assess potential issues.

![[Screenshot_20240815_113311.png]]
![[Screenshot_20240815_113259.png]]

### Gathering System Information

**Host Enumeration Overview**

Host enumeration is a critical step for both penetration testers and system administrators to understand the target system and its environment. This process helps in identifying potential vulnerabilities, securing systems, and ensuring a comprehensive security assessment.

#### Categories of Information to Gather

1. **General System Information**
    
    - **Description:** Includes overall details about the system such as the hostname, operating system specifics (name, version, configuration), and installed updates or patches.
    - **Examples:**
        - Hostname of the machine
        - OS version and build
        - Installed hotfixes and patches
2. **Networking Information**
    
    - **Description:** Covers details about the network configuration and connectivity of the target system.
    - **Examples:**
        - IP address of the system
        - Network interfaces and their configurations
        - DNS server details
        - Accessible subnets and network resources
3. **Basic Domain Information**
    
    - **Description:** Pertains to Active Directory or domain-related information relevant to the target system.
    - **Examples:**
        - Domain name
        - Domain controllers
        - Domain users and groups
4. **User Information**
    
    - **Description:** Involves details about local user accounts and their permissions on the system.
    - **Examples:**
        - List of local users and groups
        - Environment variables
        - Currently running tasks and services
        - Scheduled tasks

#### Why Do We Need This Information?

Understanding the significance of the gathered information is crucial for effective enumeration. Here’s why thorough enumeration is important:

1. **Establishing a Baseline:**
    
    - **Purpose:** To get a comprehensive overview of the system and its environment, which helps in identifying potential vulnerabilities or misconfigurations.
    - **Example:** Knowing the OS version helps in determining applicable vulnerabilities or patches.
2. **Privilege Escalation:**
    
    - **Purpose:** To identify ways to escalate privileges from an unprivileged account to an administrative one.
    - **Example:** Understanding user groups and permissions can reveal possible escalation paths.
3. **Network Mapping:**
    
    - **Purpose:** To understand how the target interacts with other systems and what network resources it can access.
    - **Example:** Identifying open ports and network shares can help in discovering additional attack vectors.
4. **Resource Access:**
    
    - **Purpose:** To determine what resources (files, services, etc.) are accessible with current permissions.
    - **Example:** Listing running services and tasks can uncover potential security issues or misconfigurations.

#### Example Scenario

Imagine you are performing a security assessment with initial access through a low-privileged user account. Your goals might include:

1. **Understanding Current Privileges:**
    
    - What groups does the user belong to?
    - What tasks and services are running under this user account?
2. **Exploring Network Access:**
    
    - What network resources and systems can this user access?
    - Are there any potential vulnerabilities in the network configuration?
3. **Privilege Escalation:**
    
    - What are the possible methods to escalate privileges from the current user account?


### Gathering System Information: A Practical Approach

**Casting a Wide Net**

When gathering system information on a Windows host, several commands and utilities can be used to collect a variety of data. This section highlights some key commands and their outputs to help with both administrative tasks and penetration testing.

#### Systeminfo Command

The `systeminfo` command provides a comprehensive overview of the system. It gathers details such as:

- Hostname
- Operating System name, version, and build
- OS configuration (e.g., workstation, server)
- Hotfixes and updates installed

For example:

- Host Name: DESKTOP-htb
- OS Name: Microsoft Windows 10 Pro
- OS Version: 10.0.19042 N/A Build 19042
- OS Manufacturer: Microsoft Corporation

This command consolidates a lot of information into a single output, making it useful for initial reconnaissance with minimal footprint.

#### Basic System Commands

To retrieve basic information, you can use the following commands:

- **Hostname:** Displays the hostname of the machine.
    
    For example:
    
    - DESKTOP-htb
- **Ver:** Shows the version of the operating system.
    
    For example:
    
    - Microsoft Windows [Version 10.0.19042.2006]

#### Network Information

To understand network configuration, the following commands are valuable:

- **Ipconfig:** Displays current TCP/IP network configurations, including IP addresses, subnet masks, and default gateways.
    
    For example:
    
    - IPv4 Address: 10.0.25.17
    - Subnet Mask: 255.255.255.0
    - Default Gateway: 10.0.25.1
- **Ipconfig /all:** Provides detailed information, including MAC addresses, DHCP settings, and DNS servers.
    
- **Arp:** Shows the ARP cache, which includes IP-to-MAC address mappings.
    
    For example:
    
    - Internet Address: 10.0.25.1
    - Physical Address: 00-e0-67-15-cf-43
    - Type: dynamic

### Understanding Current User Details and System Enumeration

**Whoami Command**

- **Basic User Information**: Run `whoami` to get the current user and domain (or local computer name if not domain-joined). Example output: `ACADEMY-WIN11\htb-student`.
    
- **Privileges Information**: Run `whoami /priv` to view the user's security privileges. Example output:
    
    - SeShutdownPrivilege: Shut down the system (Disabled)
    - SeChangeNotifyPrivilege: Bypass traverse checking (Enabled)
    - SeUndockPrivilege: Remove computer from docking station (Disabled)
    - SeIncreaseWorkingSetPrivilege: Increase a process working set (Disabled)
    - SeTimeZonePrivilege: Change the time zone (Disabled)
- **Group Membership**: Run `whoami /groups` to see the groups the user belongs to. Example output:
    
    - Everyone: Well-known group, Mandatory group, Enabled by default, Enabled group
    - BUILTIN\Users: Alias, Mandatory group, Enabled by default, Enabled group
    - BUILTIN\Performance Log Users: Alias, Mandatory group, Enabled by default, Enabled group
    - NT AUTHORITY\INTERACTIVE: Well-known group, Mandatory group, Enabled by default, Enabled group
    - CONSOLE LOGON: Well-known group, Mandatory group, Enabled by default, Enabled group
    - NT AUTHORITY\Authenticated Users: Well-known group, Mandatory group, Enabled by default, Enabled group
    - NT AUTHORITY\This Organization: Well-known group, Mandatory group, Enabled by default, Enabled group
    - NT AUTHORITY\Local account: Well-known group, Mandatory group, Enabled by default, Enabled group
    - LOCAL: Well-known group, Mandatory group, Enabled by default, Enabled group
    - NT AUTHORITY\NTLM Authentication: Well-known group, Mandatory group, Enabled by default, Enabled group
    - Mandatory Label\Medium Mandatory Level Label

**Exploring User and Group Details**

- **Enumerating Users**: Use `net user` to list all user accounts on the host. Example output:
    
    - Administrator
    - DefaultAccount
    - Guest
    - htb-student
    - WDAGUtilityAccount
- **Enumerating Local Groups**: Use `net localgroup` to see local groups on the host. Example output:
    
    - _vmware_
    - _Access Control Assistance Operators_
    - _Administrators_
    - _Backup Operators_
    - _Cryptographic Operators_
    - _Device Owners_
    - _Distributed COM Users_
    - _Event Log Readers_
    - _Guests_
    - _Hyper-V Administrators_
    - _IIS_IUSRS_
    - _Network Configuration Operators_
    - _Performance Log Users_
    - _Performance Monitor Users_
    - _Power Users_
    - _Remote Desktop Users_
    - _Remote Management Users_
    - _Replicator_
    - _System Managed Accounts Group_
    - _Users_

**Network Resources**

- **Shared Resources**: Use `net share` to view shared resources on the host. Example output:
    
    - C$: C:\ (Default share)
    - IPC$ (Remote IPC)
    - ADMIN$: C:\Windows (Remote Admin)
    - Records: D:\Important-Files (Mounted share for records storage)
- **Network Shares**: Use `net view` to list shares and resources known to the host. Example command: `net view`.


### Questions
- What command will output verbose system information such as OS configuration, security info, hardware info, and more?
	- $systeminfo$
- Access the target host and run the 'hostname' command. What is the hostname?
	- $ICL-WIN11$