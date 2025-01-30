### **1. Importance of Network Configuration**
- Essential for penetration testers to set up environments, analyze traffic, and identify vulnerabilities.
- Involves configuring network interfaces, managing access controls, and troubleshooting connectivity.
- Key protocols:
    - **TCP/IP** – Core internet communication protocol.
    - **DNS** – Resolves domain names to IPs.
    - **DHCP** – Assigns dynamic IP addresses.
    - **FTP** – File transfer protocol.



### **2. Network Access Control (NAC)**
- **Discretionary Access Control (DAC)** – Owners set access permissions.
- **Mandatory Access Control (MAC)** – OS enforces access policies (e.g., SELinux, AppArmor).
- **Role-Based Access Control (RBAC)** – Permissions assigned based on roles.
- **Security Tools:**
    - **syslog/rsyslog** – Log monitoring.
    - **ss** – Socket statistics.
    - **lsof** – Lists open files and network connections.
    - **ELK stack** – Centralized log analysis.



### **3. Configuring Network Interfaces**
- #### **Viewing Network Interfaces**
```sh
ifconfig
ip addr
```
- Example Output (`ifconfig`):
```sh
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
      inet 192.168.1.2  netmask 255.255.255.0  broadcast 192.168.1.255
      ether 8a:d9:fa:cf:79:7a
```
- #### **Activating an Interface**
```sh
sudo ifconfig eth0 up     # OR
sudo ip link set eth0 up
```
- #### **Assigning an IP Address**
```sh
sudo ifconfig eth0 192.168.1.2
```
- #### **Setting a Netmask**
```sh
sudo ifconfig eth0 netmask 255.255.255.0
```
- #### **Configuring Default Gateway**
```sh
sudo route add default gw 192.168.1.1 eth0
```



### **4. DNS Configuration**
- #### **Editing `/etc/resolv.conf` (Temporary DNS Settings)**
```sh
sudo vim /etc/resolv.conf
```

```txt
nameserver 8.8.8.8
nameserver 8.8.4.4
```
- _Note: Changes are not persistent. Use a network manager for permanent settings._



### **5. Persistent Network Configuration**
- #### **Editing `/etc/network/interfaces`**
```sh
sudo vim /etc/network/interfaces
```
```txt
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```
- Ensures a **static** IP configuration.
- #### **Restarting Networking Service**
```sh
sudo systemctl restart networking
```
- _Required to apply configuration changes._



### **Key Takeaways**
- **Mastering network settings** enables better security testing and troubleshooting.  
- **Tools like `ifconfig`, `ip`, and `route`** help configure interfaces efficiently.  
- **Persistent configurations** should be set in `/etc/network/interfaces`.  
- **Network security** depends on **NAC, logging tools, and monitoring traffic**.



### **Network Access Control (NAC) and Security Hardening**
- #### **1. Network Access Control (NAC) Overview**
	- Ensures only **authorized and compliant** devices can access the network.
	- Prevents unauthorized access, data breaches, and security threats.
	- **Key NAC Models:**
	    - **Discretionary Access Control (DAC)** – Owners set access permissions.
	    - **Mandatory Access Control (MAC)** – OS enforces strict access rules.
    - **Role-Based Access Control (RBAC)** – Access assigned based on roles.
- #### **2. NAC Models**
	- #### **Discretionary Access Control (DAC)**
		- Owners manage access permissions (read, write, execute, delete).
		- Flexible but can lead to security risks if owners misconfigure settings.
	- #### **Mandatory Access Control (MAC)**
		- **Stricter security model** than DAC.
		- Users/processes must have security clearance to access resources.
		- Used in **military, financial, and healthcare** systems.
	- #### **Role-Based Access Control (RBAC)**
		- **Users assigned roles**, and roles determine access permissions.
		- Simplifies access management and reduces errors.
		- Used in **large organizations, government, and financial institutions**.
- #### **3. Network Monitoring**
	- **Captures, analyzes, and interprets network traffic** to detect threats.
	- Examples:
	    - Capturing **unencrypted credentials** from FTP logins.
	    - Identifying **suspicious traffic** and **potential security risks**.
	- **Tools for Network Monitoring:**
	    - **Wireshark** – GUI-based network traffic analyzer.
	    - **Tshark** – CLI version of Wireshark.
	    - **Tcpdump** – Packet capture tool.
- #### **4. Network Troubleshooting**
	- Identifying and resolving **connectivity issues, slow speeds, and network errors**.
	- **Common Tools:**
	    - `ping` – Test connectivity.
	    - `traceroute` – Trace network packet path.
	    - `netstat` – View active network connections.
	    - `tcpdump` – Analyze packets.
	    - `nmap` – Scan open ports and services.
- #### **Using `ping` to Test Connectivity**
```sh
ping 8.8.8.8
```
- Example output:
```sh
64 bytes from 8.8.8.8: icmp_seq=1 ttl=119 time=1.61 ms
```
- #### **Using `traceroute` to Track Packet Path**
```sh
traceroute www.example.com
```
- Example output:
```sh
1  192.168.1.1  2.716 ms
2  10.80.71.5  7.132 ms
```
- #### **Using `netstat` to Check Active Connections**=
```sh
netstat -a
```
- Example output:
```sh
tcp 0 0 0.0.0.0:ssh 0.0.0.0:* LISTEN
tcp 0 0 localhost:5901 0.0.0.0:* LISTEN
```
- #### **5. Network Hardening Techniques**
	- #### **Security-Enhanced Linux (SELinux)**
		- **MAC-based system** that enforces strict security policies.
		- Configures access control at the **kernel level**.
		- Used in **high-security environments** (government, financial institutions).
	- #### **AppArmor**
		- **Profile-based MAC system**, simpler than SELinux.
		- Defines what resources **an application can access**.
		- Used in **Ubuntu and Debian-based** systems.
	- #### **TCP Wrappers**
		- **Restricts network access based on IP addresses**.
		- Controls access to **network services**.
		- Example: Blocking unauthorized systems from accessing SSH.
- #### **6. Practical NAC Security Tasks**
	- #### **SELinux Challenges**
		1. **Install SELinux** on a virtual machine.
		2. **Block user access** to a specific file.
		3. **Allow only one user** to access a network service.
		4. **Deny a user/group** access to a network service.\
	- #### **AppArmor Challenges**
		1. **Prevent user access** to a file.
		2. **Restrict network service access** to a single user.
		3. **Block a user/group** from a network service.
	- #### **TCP Wrappers Challenges**
		1. **Allow access** to a service from a specific IP.
		2. **Deny access** from a specific IP.
		3. **Allow access** from a range of IPs.



### **Key Takeaways**
- NAC prevents **unauthorized access** and strengthens **network security**.  
- **Monitoring tools** like Wireshark and Tcpdump help detect threats.  
- **Troubleshooting tools** like Ping, Traceroute, and Netstat resolve network issues.  
- **Security hardening** via **SELinux, AppArmor, and TCP Wrappers** enhances Linux security.