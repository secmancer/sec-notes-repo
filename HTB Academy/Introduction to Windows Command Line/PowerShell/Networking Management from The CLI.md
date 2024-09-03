**Overview of PowerShell Networking Capabilities**

- PowerShell enhances management of Windows OS network settings, applications, and remote access.
- Key areas include checking network settings (IP addresses, adapter settings, DNS) and managing remote access via WinRM and SSH.

**Scenario**

- Objective: Ensure Mr. Tanaka's host is functioning correctly and set up for remote management.

**Networking Protocols in Windows**

- **SMB**: Shares resources and files, authenticates between hosts. For other distros, SAMBA is used.
- **Netbios**: A mechanism for connections and conversations in networks, previously used for SMB but now acts as an alternative identification if DNS fails.
- **LDAP**: An open-source protocol for authentication and authorization, often used with directory services like Active Directory.
- **LLMNR**: Multicast name resolution service that works when DNS is unavailable, limited to local links.
- **DNS**: Resolves hostnames to IP addresses, commonly used across networks and the Internet.
- **HTTP/HTTPS**: Protocols for requesting and utilizing resources over the Internet, HTTP (insecure) and HTTPS (secure).
- **Kerberos**: Network authentication protocol used in Active Directory for domain resource access.
- **WinRM**: Implements WS-Management for managing hardware and software, used in IT administration and scripting.
- **RDP**: Provides graphical interface access to hosts over a network, including keyboard and mouse input.
- **SSH**: Secure protocol for host access, file transfer, and communication over insecure networks.

**Local vs. Remote Access**

- **Local Access**: Direct terminal use, typically no specific protocols needed unless accessing network resources or the Internet.

**Querying Networking Settings**

- **IPConfig**: Shows basic network settings. Use `/all` modifier for detailed information, including adapter details and IP configuration.

**Arp Settings**

- **ARP**: Translates IP addresses to physical addresses. The `-a` switch shows current ARP entries.

**DNS Configuration**

- **nslookup**: Queries DNS to resolve IP addresses or DNS names.

**Checking Open Ports**

- **netstat**: Displays current network connections and listening ports. Use `-an` to show all connections and listening ports numerically.

**PowerShell Cmdlets for Network Management**

- PowerShell cmdlets offer granular control for managing network connections beyond basic Windows commands.

### PowerShell Net Cmdlets Overview

PowerShell offers several cmdlets for network management and diagnostics. Here's a quick reference guide for some key cmdlets in the NetAdapter, NetConnection, and NetTCPIP modules:

#### Key Cmdlets

- **Get-NetIPInterface**
    
    - Retrieves properties of all network adapters.
    - Example usage: `Get-NetIPInterface`
- **Get-NetIPAddress**
    
    - Retrieves IP configurations for each adapter, similar to `ipconfig`.
    - Example usage: `Get-NetIPAddress -ifIndex 25`
- **Get-NetNeighbor**
    
    - Retrieves neighbor entries from the cache, similar to `arp -a`.
    - Example usage: `Get-NetNeighbor`
- **Get-NetRoute**
    
    - Prints the current route table, similar to `route print`.
    - Example usage: `Get-NetRoute`
- **Set-NetAdapter**
    
    - Sets basic adapter properties like VLAN ID, description, and MAC address.
    - Example usage: `Set-NetAdapter -Name "Ethernet 3" -Description "Updated Adapter"`
- **Set-NetIPInterface**
    
    - Modifies interface settings such as DHCP status and MTU.
    - Example usage: `Set-NetIPInterface -InterfaceIndex 25 -Dhcp Disabled`
- **New-NetIPAddress**
    
    - Creates and configures a new IP address.
    - Example usage: `New-NetIPAddress -IPAddress 192.168.1.100 -PrefixLength 24 -InterfaceAlias "Ethernet"`
- **Set-NetIPAddress**
    
    - Modifies the configuration of an existing IP address.
    - Example usage: `Set-NetIPAddress -InterfaceIndex 25 -IPAddress 10.10.100.54 -PrefixLength 24`
- **Disable-NetAdapter**
    
    - Disables network adapter interfaces.
    - Example usage: `Disable-NetAdapter -Name "Ethernet 3"`
- **Enable-NetAdapter**
    
    - Enables network adapter interfaces.
    - Example usage: `Enable-NetAdapter -Name "Ethernet 3"`
- **Restart-NetAdapter**
    
    - Restarts a network adapter, useful to apply changes.
    - Example usage: `Restart-NetAdapter -Name "Ethernet 3"`
- **Test-NetConnection**
    
    - Performs diagnostic checks on a connection, including ping, TCP, and route tracing.
    - Example usage: `Test-NetConnection -ComputerName "msedge.net"`

#### Example Usage

**Retrieve Adapter Information:**

`Get-NetIPInterface`

**Get IP Configuration for a Specific Adapter:**

`Get-NetIPAddress -ifIndex 25`

**Modify DHCP Status and IP Address:**

`Set-NetIPInterface -InterfaceIndex 25 -Dhcp Disabled`

`Set-NetIPAddress -InterfaceIndex 25 -IPAddress 10.10.100.54 -PrefixLength 24`

**Restart Network Adapter:**

`Restart-NetAdapter -Name "Ethernet 3"`

**Test Network Connectivity:**

`Test-NetConnection -ComputerName "msedge.net"`

### Remote Access

To manage Windows systems remotely, consider the following options:

1. **PowerShell Remoting**: Allows you to run PowerShell commands on remote systems. Ensure the remote machine has PowerShell Remoting enabled.
    
    - Example usage: `Enter-PSSession -ComputerName "RemoteComputer"`
2. **SSH**: Provides secure remote access via the SSH protocol. Ensure OpenSSH server is installed and configured on the remote machine.
    
    - Example usage: `ssh user@remotehost`
3. **RDP (Remote Desktop Protocol)**: Provides a graphical interface for connecting to another computer over a network. Ensure Remote Desktop is enabled on the remote system.
    
    - Example usage: Use the Remote Desktop application or `mstsc` command in Windows.

### Enabling Remote Access on Windows Systems

**Enabling SSH Access**

1. **Install OpenSSH Server:**
    
    - **Check Installed Capabilities:** Use `Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'` to view the status of SSH components.
        
    - **Install OpenSSH Client (if not installed):** Use `Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0`.
        
    - **Install OpenSSH Server:** Use `Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0`.
        
2. **Start and Configure the SSH Service:**
    
    - **Start the SSH Service:** Use `Start-Service sshd`.
        
    - **Set SSH Service to Start Automatically:** Use `Set-Service -Name sshd -StartupType 'Automatic'`.
        
3. **Accessing PowerShell Over SSH:**
    
    - **From Windows:** Connect using `ssh username@remote-ip`. Once connected, type `powershell` to start a PowerShell session.
        
    - **From Linux:** Connect using `ssh username@remote-ip`. After connecting, type `powershell` to start a PowerShell session.
        

**Enabling PowerShell Remoting (WinRM)**

1. **Enable WinRM:**
    
    - **Run the Configuration Command:** Use `winrm quickconfig`. This command will enable the WinRM service, configure the firewall exceptions, and set up the LocalAccountTokenFilterPolicy.
2. **Test WinRM Configuration:**
    
    - **Test Unauthenticated Access:** Use `Test-WSMan -ComputerName "remote-ip"` to check if WinRM is running without credentials.
        
    - **Test Authenticated Access:** Use `Test-WSMan -ComputerName "remote-ip" -Authentication Negotiate` to check WinRM with authentication.
        
3. **Establish a PowerShell Remote Session:**
    
    - **From Windows:** Use `Enter-PSSession -ComputerName remote-ip -Credential username -Authentication Negotiate`.
        
    - **From Linux (with PowerShell Core installed):** Use `Enter-PSSession -ComputerName remote-ip -Credential username -Authentication Negotiate`.
        

**Additional WinRM Hardening Steps:**

- **Configure TrustedHosts:** Limit the TrustedHosts setting to only the IP addresses or hostnames used for remote management.
    
- **Configure HTTPS for Transport:** Set up HTTPS for secure WinRM traffic.
    
- **Active Directory Integration:** Join systems to an Active Directory Domain to use Kerberos authentication for improved security.

### Questions
- What common protocol is used to resolve names to IP addresses.
	- DNS
- What PowerShell cmdlet will show us the IP configurations of the hosts network adapters.
	- `Get-NetIPAddress`
- What command can enable and configure Windows Remote Management on a host?
	- winrm quickconfig