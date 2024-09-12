**Key Skills:**
- Configuring and managing network settings on Linux systems
- Setting up testing environments
- Controlling network traffic
- Identifying and exploiting vulnerabilities through tailored network configurations


**Network Interface Configuration:**
- Tasks:
    - Assigning IP addresses
    - Configuring network devices (routers, switches)
    - Setting up network protocols
- Essential Network Protocols:
    - TCP/IP
    - DNS
    - DHCP
    - FTP
- Key Concepts:
    - Understanding wireless and wired network interfaces
    - Troubleshooting connectivity issues


**Network Access Control (NAC):**
- NAC Types:
    - **Discretionary Access Control (DAC)**
    - **Mandatory Access Control (MAC)**
    - **Role-Based Access Control (RBAC)**
- Tasks:
    - Configuring Linux network devices for NAC
    - Implementing **SELinux** policies and **AppArmor** profiles
    - Using **TCP wrappers** to control access


**Network Monitoring:**
- Monitoring and logging tools:
    - **syslog**, **rsyslog**, **ss**, **lsof**
    - ELK stack for deeper analysis
- Goal:
    - Analyze network traffic for security vulnerabilities
    - Identify and log security issues


**Network Troubleshooting Tools:**
- Tools:
    - **ping**
    - **nslookup**
    - **nmap**
- Use Cases:
    - Diagnosing network vulnerabilities
    - Enumerating networks and hosts
    - Insight into network traffic, packet loss, latency, DNS resolution

#### Key Commands for Configuring Network Interfaces on Ubuntu:
- **ifconfig**: Used to view and configure network interfaces, though deprecated in newer versions of Linux.
- **ip**: Replaces `ifconfig`, offering more advanced features for managing network interfaces.

#### Viewing Network Interfaces:
- `ifconfig`: Displays network interfaces with details like IP address, netmask, and status.
- `ip addr`: Provides a more detailed view of network interfaces, including IPv4 and IPv6 addresses.

#### Example of `ifconfig` Output:
- **Interface `eth0`**:
    - IPv4 Address: 178.62.32.126
    - Netmask: 255.255.192.0
    - Broadcast: 178.62.63.255
    - Status: Running with no errors

#### Example of `ip addr` Output:
- **Interface `eth0`**:
    - IPv4 Address: 178.62.32.126/18
    - IPv6 Address: fe80::88d9:faff:fecf:797a


### Activating Network Interfaces:
- Use **ifconfig** or **ip** to activate a network interface:
    - `sudo ifconfig eth0 up`
    - `sudo ip link set eth0 up`

### Assigning an IP Address:
- Assign an IP address to an interface using `ifconfig`:
    - `sudo ifconfig eth0 192.168.1.2`

### Setting a Netmask:
- Assign a netmask to an interface:
    - `sudo ifconfig eth0 netmask 255.255.255.0`

### Configuring a Default Gateway:
- Use the `route` command to set the default gateway:
    - `sudo route add default gw 192.168.1.1 eth0`

### Configuring DNS Servers:
- Update the `/etc/resolv.conf` file to set DNS servers:
    - Add nameservers (e.g., Google DNS) to the file:
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```


### Persisting Network Configurations Across Reboots:
- Edit the `/etc/network/interfaces` file to make changes persistent:
    - Example configuration for a static IP:
```
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

### Applying Changes:
- Restart the networking service to apply changes:
    - `sudo systemctl restart networking`


### Network Access Control (NAC) - Overview
- **Definition**: NAC is a security system that ensures only authorized and compliant devices gain access to the network, helping prevent unauthorized access and security breaches.
- **Importance**: Crucial for protecting network assets from cybercriminals who target system vulnerabilities.

### NAC Technologies
- **Discretionary Access Control (DAC)**:
    - Resource owners control access permissions (e.g., read, write, execute, delete).
    - Common in user-managed environments.
- **Mandatory Access Control (MAC)**:
    - Access is controlled by security levels assigned to resources and users.
    - Used in high-security environments (e.g., military, financial, healthcare).
- **Role-Based Access Control (RBAC)**:
    - Permissions assigned based on user roles within an organization.
    - More scalable and flexible than DAC, used in large organizations for ease of management.

### Discretionary Access Control (DAC)
- **Key Points**: Resource owners manage who can access their resources.
- **Use Case**: Commonly used in environments where users need to control their data's accessibility.

### Mandatory Access Control (MAC)
- **Key Points**: Access is based on security labels; users or processes must have a security clearance equal to or higher than the resource.
- **Use Case**: High-security environments, such as government or financial institutions, to minimize unauthorized access.

### Role-Based Access Control (RBAC)
- **Key Points**: Permissions are tied to roles, not individual users, simplifying large-scale access management.
- **Use Case**: Large organizations, government agencies, and financial institutions where managing access by individual users would be too complex.


### Network Monitoring
- **Definition**: Involves capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior.
- **Purpose**: Detecting security threats, vulnerabilities, and suspicious network activity.
- **Use Case**: As penetration testers, monitoring can capture unencrypted credentials (e.g., FTP logins) and help infiltrate or escalate privileges within a network.
- **Tools for Monitoring**:
    - **Wireshark**
    - **tshark**
    - **Tcpdump**


### Troubleshooting
- **Definition**: Diagnosing and resolving network issues that affect performance and reliability.
- **Importance**: Ensures network operates optimally, avoids disruptions during penetration tests, and identifies connectivity problems, slow speeds, and network errors.
- **Common Tools**:
    - **Ping**: Tests connectivity between devices by sending packets and measuring response times.
    - **Traceroute**: Tracks the route packets take to reach a remote host.
    - **Netstat**: Displays active network connections and ports for monitoring traffic and troubleshooting.
    - **Nmap**: Scans for open ports, services, and hosts on a network.


### Ping Example
- **Command**: `ping 8.8.8.8` (sends ICMP packets to Google DNS)
- **Output**: Displays packet transmission details (e.g., time, packet loss, response times).


### Traceroute Example
- **Command**: `traceroute www.inlanefreight.com`
- **Output**: Shows the path packets take to reach the destination, displaying each hop's IP and response times. Any non-responsive devices show as `* * *`.


### Netstat Example
- **Command**: `netstat -a`
- **Output**: Displays active connections, protocols, local and foreign addresses, and connection states.


### Common Network Issues
- **Network Connectivity Issues**: Misconfigured firewalls/routers, damaged cables, incorrect settings.
- **DNS Resolution Issues**: Incorrect DNS server settings or DNS record misconfiguration.
- **Packet Loss**: Could be caused by network congestion or faulty hardware.
- **Performance Issues**: Outdated hardware or software, congestion, or lack of security controls.

- **SELinux (Security-Enhanced Linux)**
    - Mandatory Access Control (MAC) system built into the Linux kernel.
    - Provides fine-grained access control for system resources and applications.
    - Enforces security policies that define access controls for each process and file on the system.
    - Limits the damage of compromised processes by restricting their access.
- **AppArmor (Application Armor)**
    - MAC system implemented as a Linux Security Module (LSM).
    - Uses application profiles to define what resources each application can access.
    - Easier to configure and use compared to SELinux, but provides less fine-grained control.
    - Useful for restricting the behavior of specific applications.
- **TCP Wrappers**
    - Host-based network access control mechanism.
    - Restricts access to network services based on the IP address of the client system.
    - Simple and effective for limiting access to unauthorized systems.
    - Works by intercepting incoming network requests and comparing the client’s IP address against access control rules.

**Similarities:**
- All three aim to improve Linux system security by limiting unauthorized access and protecting resources.
- Readily available in most Linux distributions.
- Customizable and configurable through standard Linux tools.

**Differences:**
- **SELinux**: Integrated into the kernel, complex to configure but offers fine-grained control.
- **AppArmor**: Easier to use and configure than SELinux, but not as detailed in control.
- **TCP Wrappers**: Focuses on network access control, simpler than SELinux and AppArmor, but effective for basic network protection.


**Best Practices for Security Setup:**
- Learn and practice configuring **SELinux**, **AppArmor**, and **TCP Wrappers** on your own system (recommended via VM with snapshots for rollback).
- Consider the specific security needs of the data and applications you're protecting when choosing which mechanism to implement.
- Use resources such as Discord channels or forums to share knowledge and troubleshoot issues with others. Teaching is an effective way to reinforce learning.


These tools are critical in securing Linux systems, especially during penetration testing, to prevent the risk of unauthorized access and data breaches. Proper use of these tools can reduce vulnerabilities and protect systems from malicious threats.

![[Screenshot_20240912_143917.png]]