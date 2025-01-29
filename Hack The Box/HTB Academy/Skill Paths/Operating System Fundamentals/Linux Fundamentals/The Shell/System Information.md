### **Exploring System Information in Linux**
- When managing Linux systems, whether for regular tasks or security assessments, understanding how to gather key system information is crucial. 
- The following tools will help you collect details about users, the system, network configurations, and processes. 
- These tools are useful in both day-to-day administration and during security audits or penetration testing.
- Here’s a rundown of common system information commands:



### **Common System Information Commands**

| **Command**    | **Description**                                                                              |
| -------------- | -------------------------------------------------------------------------------------------- |
| **`whoami`**   | Displays the current logged-in username.                                                     |
| **`id`**       | Returns the user’s identity, including user ID (UID), group ID (GID), and group memberships. |
| **`hostname`** | Displays or sets the system's hostname.                                                      |
| **`uname`**    | Prints basic information about the operating system and system hardware.                     |
| **`pwd`**      | Prints the current working directory.                                                        |
| **`ifconfig`** | Configures network interfaces and displays IP addresses.                                     |
| **`ip`**       | A more modern tool for viewing or manipulating network interfaces and routing.               |
| **`netstat`**  | Displays network status and active connections.                                              |
| **`ss`**       | Another utility to investigate socket connections.                                           |
| **`ps`**       | Displays information about running processes.                                                |
| **`who`**      | Shows who is logged into the system.                                                         |
| **`env`**      | Displays environment variables or sets and executes commands with modified environments.     |
| **`lsblk`**    | Lists block devices like hard drives and partitions.                                         |
| **`lsusb`**    | Lists USB devices attached to the system.                                                    |
| **`lsof`**     | Lists open files and associated processes.                                                   |
| **`lspci`**    | Lists PCI devices like network cards, video cards, etc.                                      |



### **Working with SSH**
- Secure Shell (SSH) is commonly used to remotely access and manage Linux systems. You can securely connect to remote machines using SSH, as shown below:
- #### **Connecting via SSH:**
```bash
ssh <username>@<IP address>
```
- Once logged in, you can run the system information commands from the list to explore the machine.



### **Using System Information Commands**
- Let’s go over some practical examples using commands discussed earlier:
- #### **1. `hostname`**
	- Prints the name of the machine.
```bash
hostname
```
- Example Output:
```
nixfund
```
- #### **2. `whoami`**
	- Displays the username of the current user.
```bash
whoami
```
- Example Output:
```
cry0l1t3
```
- #### **3. `id`**
	- Shows detailed user information including group memberships.
```bash
id
```
- Example Output:
```
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```
- This shows the user’s UID, GID, and group memberships. Groups like `sudo` are particularly important, as they grant administrative privileges.
- #### **4. `uname`**
	- Displays kernel and system information.
```bash
uname -a
```
- Example Output:
```
Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```
- #### **5. `uname -r`**
	- Displays the kernel release, useful for identifying potential exploits for a specific kernel version.
```bash
uname -r
```
- Example Output:
```
4.15.0-99-generic
```
- This version could be researched for known vulnerabilities.



### **Practical Application and Security Context**
- Many of these commands are essential for security assessments or penetration testing, especially when you gain remote access to a system.
- For example, `id` helps identify the privileges of the user you're operating as, and `uname` provides kernel details which are crucial when searching for exploits.



### **Next Steps: Hands-On Practice**
- The key to mastering these tools is continuous practice. Here are some exercises to improve your command line proficiency:
	1. **Explore System Information:**
	    - Use the `uname -a` command and research any potential exploits for the kernel version shown.
	    - Check the system's disk and network configurations with `lsblk`, `ifconfig`, and `netstat`.
	2. **Audit User Accounts:**
	    - Use `id` and `whoami` to audit the current user and their privileges.
	    - Investigate which users are logged in with the `who` command.
	3. **Network Exploration:**
	    - Run `ss` or `netstat` to see active connections and listening services on the machine.
	    - Identify open ports and attempt to correlate them with the system’s running services.



### Questions
- Find out the machine hardware name and submit it as the answer.
	- x86_64
- What is the path to htb-student's home directory?
	- /home/htb-student
- What is the path to the htb-student's mail?
	- /var/mail/htb-student
- Which shell is specified for the htb-student user?
	- /bin/bash
-  Which kernel release is installed on the system? (Format: 1.22.3)
	- 4.15.0
- What is the name of the network interface that MTU is set to 1500?
	- ens192