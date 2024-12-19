### Introduction
- **Network Configuration Skills**: Penetration testers must understand Linux's network settings to set up testing environments, control traffic, and exploit vulnerabilities. This includes configuring network interfaces, assigning IP addresses, and setting up network protocols (TCP/IP, DNS, DHCP, FTP).
- **Access Control**: Familiarity with **network access control (NAC)** is vital. Key NAC technologies include:
    - Discretionary access control (DAC)
    - Mandatory access control (MAC)
    - Role-based access control (RBAC)
- **NAC Enforcement**: Understand how to configure Linux network devices for NAC, including setting up **SELinux**, **AppArmor profiles**, and using **TCP wrappers** for access control.
- **Network Monitoring**: Penetration testers should be skilled in configuring network monitoring and logging tools such as **syslog**, **rsyslog**, **ss**, **lsof**, and the **ELK stack** to detect and analyze security issues.
- **Network Troubleshooting**: Tools like **ping**, **nslookup**, **nmap**, and **traceroute** are essential for diagnosing network problems, packet loss, DNS resolution, and latency issues, helping to identify vulnerabilities and resolve connectivity issues.



### Configuring Network Interfaces
- **Configuring Network Interfaces**: In Ubuntu, local network interfaces can be configured using the `ifconfig` or `ip` command, which allow users to view and modify network interface settings.
- **Importance of Network Interface Knowledge**: Understanding network interfaces is essential in the modern, interconnected world, enabling effective navigation and management of various network types.
- **Using `ifconfig` for Information**: The `ifconfig` command provides details on network interfaces, including IP addresses, netmasks, and statuses, making it useful for troubleshooting and configuring networks.
- **Transition to `ip` Command**: While `ifconfig` is deprecated in newer Linux versions in favor of the more feature-rich `ip` command, `ifconfig` remains a widely used tool for network management in many distributions.



### Network Settings
```shell-session
cry0l1t3@htb:~$ ifconfig

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 178.62.32.126  netmask 255.255.192.0  broadcast 178.62.63.255
        inet6 fe80::88d9:faff:fecf:797a  prefixlen 64  scopeid 0x20<link>
        ether 8a:d9:fa:cf:79:7a  txqueuelen 1000  (Ethernet)
        RX packets 7910  bytes 717102 (700.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7072  bytes 24215666 (23.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.106.0.66  netmask 255.255.240.0  broadcast 10.106.15.255
        inet6 fe80::b8ab:52ff:fe32:1f33  prefixlen 64  scopeid 0x20<link>
        ether ba:ab:52:32:1f:33  txqueuelen 1000  (Ethernet)
        RX packets 14  bytes 1574 (1.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15  bytes 1700 (1.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 15948  bytes 24561302 (23.4 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15948  bytes 24561302 (23.4 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


cry0l1t3@htb:~$ ip addr

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 8a:d9:fa:cf:79:7a brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname ens3
    inet 178.62.32.126/18 brd 178.62.63.255 scope global dynamic eth0
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::88d9:faff:fecf:797a/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether ba:ab:52:32:1f:33 brd ff:ff:ff:ff:ff:ff
    altname enp0s4
    altname ens4
    inet 10.106.0.66/20 brd 10.106.15.255 scope global dynamic eth1
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::b8ab:52ff:fe32:1f33/64 scope link 
       valid_lft forever preferred_lft forever
```
- When it comes to activating network interfaces, `ifconfig` and `ip` commands are two commonly used tools. 
- These commands allow users to modify and activate settings for a specific interface, such as `eth0`. 
- We can adjust the network settings to suit our needs by using the appropriate syntax and specifying the interface name.



### Activate Network Interface
```shell-session
secmancer@htb[/htb]$ sudo ifconfig eth0 up     # OR
secmancer@htb[/htb]$ sudo ip link set eth0 up
```
- One way to allocate an IP address to a network interface is by utilizing the `ifconfig` command. 
- We must specify the interface's name and IP address as arguments to do this. 
- This is a crucial step in setting up a network connection. 
- The IP address serves as a unique identifier for the interface and enables the communication between devices on the network.



### Assign IP Address to an Interface
```shell-session
secmancer@htb[/htb]$ sudo ifconfig eth0 192.168.1.2
```
- To set the netmask for a network interface, we can run the following command with the name of the interface and the netmask.
- #### Assign a Netmask to an Interface
```shell-session
secmancer@htb[/htb]$ sudo ifconfig eth0 netmask 255.255.255.0
```
- When we want to set the default gateway for a network interface, we can use the `route` command with the `add` option. 
- This allows us to specify the gateway's IP address and the network interface to which it should be applied. 
- By setting the default gateway, we are designating the IP address of the router that will be used to send traffic to destinations outside the local network.
- Ensuring that the default gateway is set correctly is important, as incorrect configuration can lead to connectivity issues.
- #### Assign the Route to an Interface
```shell-session
secmancer@htb[/htb]$ sudo route add default gw 192.168.1.1 eth0
```
- When configuring a network interface, it is often necessary to set Domain Name System (`DNS`) servers to ensure proper network functionality. 
- DNS servers translate domain names into IP addresses, allowing devices to connect with each other on the internet. 
- By setting those, we can ensure that their devices can communicate with other devices and access websites and other online resources. 
- Without proper DNS server configuration, devices may experience network connectivity issues and be unable to access certain online resources. 
- This can be achieved by updating the `/etc/resolv.conf` file with the appropriate DNS server information. 
- The `/etc/resolv.conf` file is a plain text file containing the system's DNS information. 
- The system can properly resolve domain names to IP addresses by adding the required DNS servers to this file. 
- It is important to note that any changes made to this file will only apply to the current session and must be updated if the system is restarted or the network configuration is changed.



### Editing DNS Settings
```shell-session
secmancer@htb[/htb]$ sudo vim /etc/resolv.conf
```
- #### /etc/resolv.conf
```txt
nameserver 8.8.8.8
nameserver 8.8.4.4
```
- After completing the necessary modifications to the network configuration, it is essential to ensure that these changes are saved to persist across reboots. 
- This can be achieved by editing the `/etc/network/interfaces` file, which defines network interfaces for Linux-based operating systems. 
- Thus, it is vital to save any changes made to this file to avoid any potential issues with network connectivity.



### Editing Interfaces
```shell-session
secmancer@htb[/htb]$ sudo vim /etc/network/interfaces
```
- This will open the `interfaces` file in the vim editor.
- We can add the network configuration settings to the file like this.
- #### /etc/network/interfaces
```txt
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```
- By setting the `eth0` network interface to use a static IP address of `192.168.1.2`, with a netmask of `255.255.255.0` and a default gateway of `192.168.1.1`, we can ensure that your network connection remains stable and reliable. 
- Additionally, by specifying DNS servers of `8.8.8.8` and `8.8.4.4`, we can ensure that our computer can easily access the internet and resolve domain names. 
- Once we have made these changes to the configuration file, saving the file and exiting the editor is important.
- After that, we must restart the networking service to apply the changes.



### Restart Networking Service
```shell-session
secmancer@htb[/htb]$ sudo systemctl restart networking
```



### Network Access Control
- Network access control (NAC) is a crucial component of network security, especially in today's era of increasing cyber threats. 
- As a penetration tester, it is vital to understand the significance of NAC in protecting the network and the various NAC technologies that can be utilized to enhance security measures. 
- NAC is a security system that ensures that only authorized and compliant devices are granted access to the network, preventing unauthorized access, data breaches, and other security threats. 
- By implementing NAC, organizations can be confident in their ability to protect their assets and data from cybercriminals who always seek to exploit system vulnerabilities. 
- The following are the different NAC technologies that can be used to enhance security measures:
	- Discretionary access control (DAC)
	- Mandatory access control (MAC)
	- Role-based access control (RBAC)
- These technologies are designed to provide different levels of access control and security. 
- Each technology has its unique characteristics and is suitable for different use cases. 
- As a penetration tester, it is essential to understand these technologies and their specific use cases to test and evaluate the network's security effectively.



### Discretionary Access Control
- DAC is a crucial component of modern security systems as it helps organizations provide access to their resources while managing the associated risks of unauthorized access.
- It is a widely used access control system that enables users to manage access to their resources by granting resource owners the responsibility of controlling access permissions to their resources.
- This means that users and groups who own a specific resource can decide who has access to their resources and what actions they are authorized to perform. 
- These permissions can be set for reading, writing, executing, or deleting the resource.



### Mandatory Access Control
- MAC is used in infrastructure that provides more fine-grained control over resource access than DAC systems.
- Those systems define rules that determine resource access based on the resource's security level and the user's security level or process requesting access. 
- Each resource is assigned a security label that identifies its security level, and each user or process is assigned a security clearance that identifies its security level. 
- Access to a resource is only granted if the user's or process's security level is equal to or greater than the security level of the resource. 
- MAC is often used in operating systems and applications that require a high level of security, such as military or government systems, financial systems, and healthcare systems. 
- MAC systems are designed to prevent unauthorized access to resources and minimize the impact of security breaches.



### Role-based Access Control
- RBAC assigns permissions to users based on their roles within an organization.
- Users are assigned roles based on their job responsibilities or other criteria, and each role is granted a set of permissions that determine the actions they can perform.
- RBAC simplifies the management of access permissions, reduces the risk of errors, and ensures that users can access only the resources necessary to perform their job functions.
- It can restrict access to sensitive resources and data, limit the impact of security breaches, and ensure compliance with regulatory requirements. 
- Compared to Discretionary Access Control (DAC) systems, RBAC provides a more flexible and scalable approach to managing resource access. 
- In an RBAC system, each user is assigned one or more roles, and each role is assigned a set of permissions that define the user's actions. 
- Resource access is granted based on the user's assigned role rather than their identity or ownership of the resource. 
- RBAC systems are typically used in environments with many users and resources, such as large organizations, government agencies, and financial institutions.



### Monitoring
- Network monitoring involves capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior. 
- The primary goal of analyzing and monitoring network traffic is identifying security threats and vulnerabilities. 
- For example, as penetration testers, we can capture credentials when someone uses an unencrypted connection and tries to log in to an FTP server. 
- As a result, we will obtain this user’s credentials that might help us to infiltrate the network even further or escalate our privileges to a higher level. 
- In short, by analyzing network traffic, we can gain insights into network behavior and identify patterns that may indicate security threats. 
- Such analysis includes detecting suspicious network activity, identifying malicious traffic, and identifying potential security risks.
- However, we cover this vast topic in the [Intro to Network Traffic Analysis](https://academy.hackthebox.com/module/details/81) module, where we use several tools for network monitoring on Linux systems like Ubuntu and Windows systems, like Wireshark, tshark, and Tcpdump.



### Troubleshooting
- Network troubleshooting is an essential process that involves diagnosing and resolving network issues that can adversely affect the performance and reliability of the network. 
- This process is critical for ensuring the network operates optimally and avoiding disruptions that could impact business operations during our penetration tests. 
- It also involves identifying, analyzing, and implementing solutions to resolve problems. 
- Such problems include connectivity problems, slow network speeds, and network errors. Various tools can help us identify and resolve issues regarding network troubleshooting on Linux systems. 
- Some of the most commonly used tools include:
	1. Ping
	2. Traceroute
	3. Netstat
	4. Tcpdump
	5. Wireshark
	6. Nmap
- By using these tools and others like them, we can better understand how the network functions and quickly diagnose any issues that may arise. 
- For example, `ping` is a command-line tool used to test connectivity between two devices.
- It sends packets to a remote host and measures the time to return them. To use `ping`, we can enter the following command:
- #### Ping
```shell-session
secmancer@htb[/htb]$ ping <remote_host>
```
- For example, pinging the Google DNS server will send ICMP packets to the Google DNS server and display the response times.
```shell-session
secmancer@htb[/htb]$ ping 8.8.8.8

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=119 time=1.61 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=119 time=1.06 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=119 time=0.636 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=119 time=0.685 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3017ms
rtt min/avg/max/mdev = 0.636/0.996/1.607/0.388 ms
```
- Another tool is the `traceroute`, which traces the route packets take to reach a remote host.
- It sends packets with increasing Time-to-Live (TTL) values to a remote host and displays the IP addresses of the devices that the packets pass through.
- For example, to trace the route to the Google DNS server, we would enter the following command.
- #### Traceroute
```shell-session
secmancer@htb[/htb]$ traceroute www.inlanefreight.com

traceroute to www.inlanefreight.com (134.209.24.248), 30 hops max, 60 byte packets
 1  * * *
 2  10.80.71.5 (10.80.71.5)  2.716 ms  2.700 ms  2.730 ms
 3  * * *
 4  10.80.68.175 (10.80.68.175)  7.147 ms  7.132 ms 10.80.68.161 (10.80.68.161)  7.393 ms
```
- This will display the IP addresses of the devices that the packets pass through to reach the Google DNS server. 
- The output of a traceroute command shows how it is used to trace the path of packets to the website [www.inlanefreight.com](http://www.inlanefreight.com/), which has an IP address of 134.209.24.248. 
- Each line of the output contains valuable information.
- When setting up a network connection, it's important to specify the destination host and IP address. 
- In this example, the destination host is 134.209.24.248, and the maximum number of hops allowed is 30.
- This ensures that the connection is established efficiently and reliably. 
- By providing this information, the system can route traffic to the correct destination and limit the number of intermediate stops the data needs to make.
- The second line shows the first hop in the traceroute, which is the local network gateway with the IP address 10.80.71.5, followed by the next three columns show the time it took for each of the three packets sent to reach the gateway in milliseconds (2.716 ms, 2.700 ms, and 2.730 ms).
- Next, we see the second hop in the traceroute. 
- However, there was no response from the device at that hop, indicated by the three asterisks instead of the IP address. 
- This could mean the device is down, blocking ICMP traffic, or a network issue caused the packets to drop.
- In the fourth line, we can see the third hop in the traceroute, consisting of two devices with IP addresses 10.80.68.175 and 10.80.68.161, and again the next three columns show the time it took for each of the three packets to reach the first device (7.147 ms, 7.132 ms, and 7.393 ms).



### Netstat
- `Netstat` is used to display active network connections and their associated ports.
- It can be used to identify network traffic and troubleshoot connectivity issues. 
- To use `netstat`, we can enter the following command.
```shell-session
secmancer@htb[/htb]$ netstat -a

Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 localhost:5901          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:sunrpc          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:http            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN
...SNIP...
```
- We can expect to receive detailed information about each connection when using this tool.
- This includes the protocol used, the number of bytes received and sent, IP addresses, port numbers of both local and remote devices, and the current connection state.
- The output provides valuable insights into the network activity on the system, highlighting four specific connections currently active and listening on specific ports. 
- These connections include the VNC remote desktop software, the Sun Remote Procedure Call service, the HTTP protocol for web traffic, and the SSH protocol for secure remote shell access. 
- By knowing which ports are used by which services, users can quickly identify any network issues and troubleshoot accordingly. 
- The most common network issues we will encounter during our penetration tests include the following:
	- Network connectivity issues
	- DNS resolution issues (it's always DNS)
	- Packet loss
	- Network performance issues
- Each issue, along with common causes that may include misconfigured firewalls or routers, damaged network cables or connectors, incorrect network settings, hardware failure, incorrect DNS server settings, DNS server failure, misconfigured DNS records, network congestion, outdated network hardware, incorrectly configured network settings, unpatched software or firmware, and lack of proper security controls. 
- Understanding these common network issues and their causes is important for effectively identifying and exploiting vulnerabilities in network systems during our testing.



### Hardening
- **Security Mechanisms**: SELinux, AppArmor, and TCP wrappers are crucial tools for securing Linux systems against unauthorized access and malicious attacks, especially during penetration testing.
- **SELinux**: A mandatory access control (MAC) system built into the Linux kernel, offering fine-grained control over system resources by enforcing access policies for processes and files.
- **AppArmor**: A MAC system implemented as a Linux Security Module (LSM), using application profiles to manage resource access, easier to configure than SELinux but with less fine-grained control.
- **TCP Wrappers**: A host-based network access control tool that restricts network service access based on client IP addresses, useful for limiting unauthorized network access.
- **Similarities**: All three mechanisms aim to secure Linux systems by restricting access to resources, reducing the risk of unauthorized access and data breaches.
- **Differences**: SELinux is more complex and integrated into the kernel, while AppArmor is simpler and uses application profiles. TCP wrappers are simpler than both, focusing on network access control based on IP addresses.



### Setting Up
- **Learning Security Tools**: Familiarizing yourself with security tools like `SELinux`, `AppArmor`, and `TCP wrappers` is crucial for improving cybersecurity expertise.
- **Self-Study Challenge**: Dedicating time to configure and understand these tools on your own can enhance your problem-solving skills and deepen your understanding. Using a personal VM with snapshots is recommended for experimentation.
- **No One-Size-Fits-All**: Implementing cybersecurity measures should be tailored to the specific data and tools you're working with. Consider the context when choosing and configuring security tools.
- **Collaborative Learning**: Engaging with others in community channels, such as Discord, allows for sharing knowledge and improving your skills. Explaining concepts to others reinforces your own learning and contributes to the group’s growth.



### SELinux
![[Screenshot_20241108_215111.png]]



### AppArmor
![[Screenshot_20241108_215130.png]]



### TCP Wrappers
![[Screenshot_20241108_215200.png]]
