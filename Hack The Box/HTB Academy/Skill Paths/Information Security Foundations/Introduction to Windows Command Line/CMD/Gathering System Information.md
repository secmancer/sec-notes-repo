### Introduction
- **Purpose**: Gathering system information (host enumeration) is crucial for both Systems Administrators (Blue Team) and Penetration Testers (Red Team).
  - **Red Team**: Identifies vulnerabilities and exploitable services.
  - **Blue Team**: Diagnoses issues, secures hosts, and ensures network integrity.
- **Key Questions**:
  1. What information can we gather from the system?
  2. Why is this information important?
  3. How do we gather this information using Command Prompt?



### Types of Information to Gather
1. **General System Information**:
   - Hostname, OS details (name, version, configuration), installed patches/hotfixes.
2. **Networking Information**:
   - IP address, network interfaces, subnets, DNS servers, network resources.
3. **Basic Domain Information**:
   - Active Directory details (if the system is domain-joined).
4. **User Information**:
   - Local users/groups, environment variables, running tasks, scheduled tasks, services.



### Why Gather System Information?
- **Goal**: Understand the environment to guide further actions (e.g., privilege escalation, securing systems).
- **Example Scenario**:
  - **Assumed Breach**: Start with an unprivileged user account and escalate privileges.
  - **Questions to Answer**:
    - What user account do we have access to?
    - What groups does the user belong to?
    - What privileges does the user have?
    - What network resources are accessible?
    - What tasks/services are running under the user?



### How to Gather System Information
1. **Using `systeminfo`**:
   - Provides a comprehensive overview of the system.
   - **Command**: `systeminfo`
   - **Output Includes**: Hostname, OS version, hotfixes, domain information, and more.
   - **Use Case**: Quick initial enumeration for both sysadmins and attackers.
2. **Basic System Information**:
   - **Hostname**: `hostname`
   - **OS Version**: `ver`
3. **Networking Information**:
   - **IP Configuration**: `ipconfig`
     - Displays IP address, subnet mask, default gateway, DNS servers.
   - **Detailed IP Configuration**: `ipconfig /all`
     - Includes MAC address, DHCP settings, and more.
   - **ARP Cache**: `arp /a`
     - Lists devices the host has communicated with (IP and MAC addresses).
4. **User Information**:
   - **Current User**: `whoami`
     - Displays the current logged-in user.
   - **User Privileges**: `whoami /priv`
     - Lists privileges assigned to the current user.
   - **User Groups**: `whoami /groups`
     - Shows groups the user belongs to (built-in and custom).



### Key Commands and Their Outputs
1. **`systeminfo`**:
   ```
   Host Name:                 DESKTOP-htb
   OS Name:                   Microsoft Windows 10 Pro
   OS Version:                10.0.19042 N/A Build 19042
   OS Manufacturer:           Microsoft Corporation
   OS Configuration:          Standalone Workstation
   OS Build Type:             Multiprocessor Free
   ```
2. **`ipconfig`**:
   ```
   Ethernet adapter Ethernet:
      IPv4 Address. . . . . . . . . . . : 10.0.25.17
      Subnet Mask . . . . . . . . . . . : 255.255.255.0
      Default Gateway . . . . . . . . . : 10.0.25.1
   ```
3. **`arp /a`**:
   ```
   Interface: 10.0.25.17 --- 0x17
     Internet Address      Physical Address      Type
     10.0.25.1             00-e0-67-15-cf-43     dynamic
     10.0.25.5             54-9f-35-1c-3a-e2     dynamic
   ```
4. **`whoami`**:
   ```
   ACADEMY-WIN11\htb-student
   ```
5. **`whoami /priv`**:
   ```
   Privilege Name                Description                          State
   ============================= ==================================== ========
   SeChangeNotifyPrivilege       Bypass traverse checking             Enabled
   SeShutdownPrivilege           Shut down the system                 Disabled
   ```
6. **`whoami /groups`**:
   ```
   Group Name                             Type             SID          Attributes
   ====================================== ================ ============ ==================================================
   BUILTIN\Users                          Alias            S-1-5-32-545 Mandatory group, Enabled by default, Enabled group
   NT AUTHORITY\Authenticated Users       Well-known group S-1-5-11     Mandatory group, Enabled by default, Enabled group
   ```



### Methodology for Enumeration
1. **Start Broad**: Use `systeminfo` for a quick overview.
2. **Narrow Down**:
   - Use `hostname` and `ver` for basic system details.
   - Use `ipconfig` and `arp /a` for network details.
   - Use `whoami`, `whoami /priv`, and `whoami /groups` for user details.
3. **Prioritize Information**:
   - Focus on user privileges, group memberships, and network connectivity.
4. **Stay Under the Radar**:
   - Use fewer commands to minimize detection (e.g., `systeminfo` instead of multiple commands).



### Importance of Thorough Enumeration
- **Avoid Missing Critical Details**: Human configuration errors or overlooked vulnerabilities can be exploited.
- **Build a Clear Picture**: Understand the environment to plan effective attacks or defenses.
- **Save Time**: Structured enumeration prevents wasted effort on irrelevant information.



### **1. Investigating Other Users and Groups**
- **Objective**: Identify other users and groups on the system or domain to expand access and maintain persistence.
- **Key Commands**:
  1. **`net user`**:
     - Lists all user accounts on the host.
     - **Example**:
       ```
       C:\htb> net user
       User accounts for \\ACADEMY-WIN11
       -------------------------------------------------------------------------------
       Administrator            DefaultAccount           Guest
       htb-student              WDAGUtilityAccount
       ```
     - **Use Case**: Identify potential target accounts for privilege escalation or lateral movement.

  2. **`net group`**:
     - Displays domain groups (must be run on a Domain Controller).
     - **Example**:
       ```
       C:\htb> net group
       This command can be used only on a Windows Domain Controller.
       ```
     - **Use Case**: Enumerate domain groups to identify privileged accounts (e.g., Domain Admins).

  3. **`net localgroup`**:
     - Lists local groups on the host.
     - **Example**:
       ```
       C:\htb> net localgroup
       Aliases for \\ACADEMY-WIN11
       -------------------------------------------------------------------------------
       *Administrators
       *Backup Operators
       *Guests
       *Remote Desktop Users
       *Users
       ```
     - **Use Case**: Identify local groups and their members to find privileged accounts.



### **2. Exploring Network Resources**
- **Objective**: Locate shared resources (e.g., file shares, printers) to identify valuable data or persistence mechanisms.
- **Key Commands**:
  1. **`net share`**:
     - Lists shared resources on the host.
     - **Example**:
       ```
       C:\htb> net share
       Share name   Resource                        Remark
       -------------------------------------------------------------------------------
       C$           C:\                             Default share
       IPC$                                         Remote IPC
       ADMIN$       C:\Windows                      Remote Admin
       Records      D:\Important-Files              Mounted share for records storage
       ```
     - **Use Case**:
       - Identify accessible shares.
       - Check permissions (read/write/execute) on shares.
       - Look for valuable data or drop payloads for lateral movement.

  2. **`net view`**:
     - Displays shared resources known to the host (e.g., domain resources, printers).
     - **Example**:
       ```
       C:\htb> net view
       Server Name            Remark
       -------------------------------------------------------------------------------
       \\FS01                 File Server
       \\PRINT01              Network Printer
       ```
     - **Use Case**: Map the network environment and identify additional targets.



### **3. Piecing Information Together**
- **Goal**: Use gathered information to escalate privileges or move laterally.
- **Key Considerations**:
  1. **User Accounts**:
     - Identify high-privilege accounts (e.g., Administrators, Domain Admins).
     - Check for weak passwords or misconfigurations.
  2. **Groups**:
     - Identify membership in privileged groups (e.g., Backup Operators, Remote Desktop Users).
     - Look for custom groups with elevated permissions.
  3. **Network Shares**:
     - Identify accessible shares and their contents.
     - Check for sensitive data or opportunities to drop payloads.
  4. **Persistence**:
     - Use shared resources to maintain access across the network.
     - Exploit misconfigured permissions to escalate privileges.



### **4. Final Thoughts and Considerations**
- **Noise and Detection**:
  - Using `net` commands is noisy and can trigger alerts in monitored environments.
  - Avoid excessive use of commands to minimize detection.
- **Logging and Monitoring**:
  - Blue Teams can detect unusual `cmd.exe` usage and `net` commands.
  - Proper logging and monitoring can quickly identify suspicious activity.
- **Methodology**:
  - Develop a structured approach to enumeration.
  - Focus on high-value targets (e.g., privileged accounts, sensitive shares).
  - Balance thoroughness with stealth to avoid detection.



### **Summary of Key Commands**
| **Command**      | **Description**                                                                 | **Use Case**                                                 |
| ---------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| `net user`       | Lists all user accounts on the host.                                            | Identify potential target accounts.                          |
| `net group`      | Lists domain groups (must be run on a Domain Controller).                       | Enumerate domain groups and privileged accounts.             |
| `net localgroup` | Lists local groups on the host.                                                 | Identify local group memberships and privileges.             |
| `net share`      | Lists shared resources on the host.                                             | Locate accessible shares and check permissions.              |
| `net view`       | Displays shared resources known to the host (e.g., domain resources, printers). | Map the network environment and identify additional targets. |



### Summary
- **What to Gather**: System, network, domain, and user information.
- **Why Gather It**: To understand the environment and guide further actions.
- **How to Gather It**: Use Command Prompt utilities like `systeminfo`, `ipconfig`, `arp`, and `whoami`.
- **Key Takeaway**: Thorough enumeration is essential for both attackers and defenders to achieve their goals effectively.
 - **File and Directory Enumeration**:
  - Search for specific files and directories on the system.
  - Identify sensitive data or configuration files.
- **Privilege Escalation**:
  - Exploit misconfigurations or vulnerabilities to gain higher privileges.
- **Lateral Movement**:
  - Use gathered information to move across the network and compromise additional hosts.



### Questions
- What command will output verbose system information such as OS configuration, security info, hardware info, and more?
	- systeminfo
- Access the target host and run the 'hostname' command. What is the hostname?
	- ICL-WIN11