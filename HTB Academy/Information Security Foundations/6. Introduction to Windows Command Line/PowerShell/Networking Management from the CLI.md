### Notes: Networking with Windows Hosts
**1. Overview**
- PowerShell enhances capabilities for managing Windows networking settings and applications.
- This section covers:
    - Checking network settings (IP addresses, adapter settings, DNS settings).
    - Enabling and managing remote host access (WinRM and SSH).




**2. Scenario**
- **Objective:** Ensure Mr. Tanaka's host is functioning correctly and can be managed remotely from the IT office.
    - **Tasks:**
        - Perform a quick checkup.
        - Validate host settings.
        - Enable remote management.




**3. Networking Basics**
- **Similarities:**
    - Windows networking is similar to Linux/Unix in terms of TCP/IP stack, wireless protocols, and general network traffic.
    - Basic networking concepts are consistent across platforms.
- **Differences:**
    - Communication methods between Windows hosts, domains, and Linux hosts can vary.




**4. Protocols**
- **Standard Protocols:**
    - The module will cover some common protocols used in Windows networking, which you might encounter in administration or penetration testing.


![[Screenshot_20240916_080259.png]]

### Notes: Local vs. Remote Access and Networking Management
**1. Overview**
- This guide explores local vs. remote access and covers network management using PowerShell and built-in CLI tools.


**2. Local vs. Remote Access**
- **Local Access:**
    - Direct access at the terminal.
    - No specific access protocols required unless interacting with networked resources or the Internet.
    - Examples: Directly interacting with the host PC.
- **Remote Access:**
    - Accessing and managing a host from a different location.
    - Requires configuration and access protocols (e.g., WinRM, SSH).


3. **Querying Networking Settings**
- **IPConfig:**
    - Command to view basic network settings.
    - **Usage:**
        - `ipconfig` – Shows basic settings (IP address, subnet mask, gateway).
        - `ipconfig /all` – Displays detailed information (DHCP status, DNS servers, etc.).
        **Example Output:**
```
PS C:\htb> ipconfig 

Windows IP Configuration

Ethernet adapter Ethernet0:
   Connection-specific DNS Suffix  . : .htb
   IPv4 Address. . . . . . . . . . . : 10.129.203.105
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . : 10.129.0.1
```
**ARP (Address Resolution Protocol):**
- Command to display ARP entries, showing IP-to-MAC address mappings.
- **Usage:**
    - `arp -a` – Lists ARP table entries.
    **Example Output:**
```
PS C:\htb> arp -a

Interface: 10.129.203.105 --- 0xb
  Internet Address      Physical Address      Type
  10.129.0.1            00-50-56-b9-b9-fc     dynamic
```

**Nslookup:**
- Command to query DNS to resolve IP addresses or hostnames.
- **Usage:**
    - `nslookup [hostname]` – Resolves the DNS name to an IP address.
    **Example Output:**
```
PS C:\htb> nslookup ACADEMY-ICL-DC

DNS request timed out.
Server:  UnKnown
Address:  172.16.5.155

Name:    ACADEMY-ICL-DC.greenhorn.corp
Address:  172.16.5.155
```


**Netstat:**

- Command to display network connections, listening ports, and active connections.
- **Usage:**
    - `netstat -an` – Shows all connections and listening ports in numerical form.
    **Example Output:**
```
PS C:\htb> netstat -an 

Active Connections

  Proto  Local Address          Foreign Address        State
  TCP    0.0.0.0:22             0.0.0.0:0              LISTENING
  TCP    10.129.203.105:22      10.10.14.19:32557      ESTABLISHED
```




**PowerShell Networking Cmdlets**
- **PowerShell Cmdlets:**
    - PowerShell provides cmdlets for more granular network management.
    - **Modules:**
        - `NetAdapter`
        - `NetConnection`
        - `NetTCPIP`These modules offer detailed control and configuration of network interfaces, connections, and TCP/IP settings.


![[Screenshot_20240916_083100.png]]

### **Get-NetIPInterface**
- **Purpose**: Lists network interfaces and their properties.
- **Usage**:
```
Get-NetIPInterface
```
**Key Properties**:
- `ifIndex`: Interface index.
- `InterfaceAlias`: Friendly name of the interface.
- `AddressFamily`: IPv4 or IPv6.
- `InterfaceMetric`: Metric for the interface.
- `Dhcp`: DHCP status.
- `ConnectionState`: Connection status.
- `PolicyStore`: The store where settings are applied.



### **Get-NetIPAddress**
- **Purpose**: Retrieves IP address information for a specific interface.
- **Usage**:
```
Get-NetIPAddress -ifIndex <Index>
```
**Key Properties**:
- `IPAddress`: The assigned IP address.
- `InterfaceIndex`: Interface index.
- `AddressFamily`: IPv4 or IPv6.
- `Type`: Type of address (e.g., Unicast).
- `PrefixLength`: Subnet mask length.
- `PrefixOrigin`: How the prefix was obtained (e.g., DHCP).


### **Set-NetIPInterface**
- **Purpose**: Configures properties of a network interface.
- **Usage**:
```
Set-NetIPInterface -InterfaceIndex <Index> -Dhcp <Enabled|Disabled>
```
- **Example:**
```
Set-NetIPInterface -InterfaceIndex 25 -Dhcp Disabled
```



### **Set-NetIPAddress**
- **Purpose**: Configures IP address settings for a network interface.
- **Usage**:
```
Set-NetIPAddress -InterfaceIndex <Index> -IPAddress <IPAddress> -PrefixLength <Length>
```
- **Example**:
```
Set-NetIPAddress -InterfaceIndex 25 -IPAddress 10.10.100.54 -PrefixLength 24
```



### **Get-NetIPAddress** (Verification)
- **Purpose**: Verify changes to IP address settings.
- **Usage**:
```
Get-NetIPAddress -ifindex <Index> | Format-Table InterfaceIndex, InterfaceAlias, IPAddress, PrefixLength
```



### **Restart-NetAdapter**
- **Purpose**: Restarts a network adapter to apply changes.
- **Usage**:
```
Restart-NetAdapter -Name '<InterfaceAlias>'
```
- **Example**:
```
Restart-NetAdapter -Name 'Ethernet 3'
```





### **Test-NetConnection**
- **Purpose**: Tests network connectivity and provides detailed metrics.
- **Usage**:
```
Test-NetConnection -ComputerName <HostName> -SourceAddress <IPAddress>
```
- **Example**:
```
Test-NetConnection -ComputerName msedge.net -SourceAddress 10.10.100.54
```
- **Outputs**:
    - `PingSucceeded`: Indicates if ping was successful.
    - `PingReplyDetails (RTT)`: Round-trip time.



### **Remote Access**
- **Overview**: Methods for managing remote Windows systems include PowerShell, SSH, and RDP.



### How to Enable Remote Access? (SSH, PSSessions, etc.)
#### Enabling SSH Access
**Overview:** SSH allows remote access to PowerShell on a Windows system over the network. Starting from Windows Server and Client versions in 2018, SSH is included and accessible through OpenSSH client and server applications.
**Setting up SSH on a Windows Target:**
1. **Check Installed Capabilities:**
```
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```
2. **Install OpenSSH Client:**
```
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```
3. **Install OpenSSH Server:**
```
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```
4. **Verify Installation:**
```
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```




**Starting the SSH Service & Setting Startup Type:**
1. **Start SSH Service:**
```
Start-Service sshd
```
2. **Set SSH Service to Automatic:**
```
Set-Service -Name sshd -StartupType 'Automatic'
```
**Accessing PowerShell over SSH:**
- **From Windows:**
```
ssh htb-student@10.129.224.248
```
After connecting, enter PowerShell:
```
powershell
```
**From Linux:**
```
ssh htb-student@10.129.224.248
```
After connecting, enter PowerShell:
```
powershell
```




#### Enabling WinRM
**Overview:** Windows Remote Management (WinRM) is a service that allows remote management and command execution on Windows systems. It listens on ports 5985 and 5986. WinRM is enabled by default on Windows Server and can be configured on Windows desktops.
**Enabling & Configuring WinRM:**
1. **Enable WinRM:**
```
winrm quickconfig
```
**Note:** This command will:
- Enable the WinRM service.
- Allow WinRM through Windows Defender Firewall.
- Grant administrative rights remotely to local users.



**Hardening WinRM Configurations:**
- Configure TrustedHosts to limit access to specific IP addresses/hostnames.
- Configure HTTPS for secure transport.
- Join Windows systems to an Active Directory Domain and enforce Kerberos authentication.



**Testing PowerShell Remote Access:**
- **Testing Unauthenticated Access:**
```
Test-WSMan -ComputerName "10.129.224.248"
```
- **Testing Authenticated Access:**
```
Test-WSMan -ComputerName "10.129.224.248" -Authentication Negotiate
```




**PowerShell Remote Sessions:**
- **Establishing a PowerShell Session:**
```
Enter-PSSession -ComputerName 10.129.224.248 -Credential htb-student -Authentication Negotiate
```



**Using Enter-PSSession from Linux:**
```
Enter-PSSession -ComputerName 10.129.224.248 -Credential htb-student -Authentication Negotiate
```



## Questions
- What common protocol is used to resolve names to IP addresses.
	- DNS
- What PowerShell cmdlet will show us the IP configurations of the hosts network adapters.
	- Get-NetIPAddress
- What command can enable and configure Windows Remote Management on a host?
	- winrm quickconfig