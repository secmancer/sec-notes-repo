When working with different Linux systems, it's crucial to understand the structure and obtain information about the system, including processes, network configurations, users, directories, and settings. Below is a list of useful commands for gathering such information, many of which are installed by default:
![[Screenshot_20240912_122017.png]]

#### Examples
- **Hostname**
```
secmancer@htb[/htb]$ hostname
nixfund
```
- **Description:** Prints the name of the computer.
- **Whoami**
```
cry0l1t3@htb[/htb]$ whoami
cry0l1t3
```
- **Description:** Displays the current username.
- **Id**
```
cry0l1t3@htb[/htb]$ id
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```
- **Description:** Shows user ID, group ID, and group memberships.
- **Uname**
```
cry0l1t3@htb[/htb]$ uname -a
Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```
- **Description:** Prints detailed system information including kernel name, hostname, kernel release, and more.
```
cry0l1t3@htb[/htb]$ uname -r
4.15.0-99-generic
```
- **Description:** Prints the kernel release version, useful for searching potential exploits.

### Recommended Practices
- **Study Commands:** Understanding and practicing with these commands is essential for effective system management and security assessments.
- **Man Pages:** Read the `man` pages for detailed command usage and options.
- **Explore Options:** Use commands like `--help` or `-h` for a quick overview of command options.
- **Apropos:** Use `apropos <keyword>` to find related commands and tools based on descriptions.

### Optional Exercises
- **Practice Commands:** Solve exercises to get comfortable with these commands and their outputs.
- **SSH Login:** Use Secure Shell (SSH) to connect and execute commands on remote systems.
```
secmancer@htb[/htb]$ ssh [username]@[IP address]
```
- **Description:** Connects to a remote host to execute commands securely.

### Questions:
- Find out the machine hardware name and submit it as the answer.
	- x86_64
- What is the path to htb-student's home directory?
	- /home/htb-student
- What is the path to the htb-student's mail?
	- /var/mail/htb-student
- Which shell is specified for the htb-student user?
	- /bin/bash
- Which kernel version is installed on the system? (Format: 1.22.3)
	- 4.15.0
- What is the name of the network interface that MTU is set to 1500?
	- ens192