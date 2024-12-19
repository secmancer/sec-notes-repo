### Introduction
- **Solaris** is a **Unix-based** OS developed by **Sun Microsystems** (acquired by **Oracle**), known for its **robustness**, **scalability**, and support for **high-end hardware**.
- It is widely used in **enterprise environments** for **mission-critical applications**, such as **database management**, **cloud computing**, and **virtualization**.
- **Solaris** includes built-in features like the **Oracle VM Server for SPARC**, enabling **virtualization** on a single physical server.
- The OS is designed for **high availability**, **fault tolerance**, and **system management**, making it ideal for industries where **security**, **reliability**, and **performance** are crucial (e.g., **banking**, **finance**, **government**).
- It is used by major companies like **Amazon**, **IBM**, and **Dell**, emphasizing its role in **large-scale data centers**, **cloud computing**, and **virtualization**.



### Linux Distros vs Solaris
- **Solaris** is a **proprietary** operating system owned by **Oracle Corporation**, with **closed-source code**, while **Linux distributions** are **open-source**, allowing anyone to modify and use the code.
- **Linux distributions** often use the **Zettabyte File System (ZFS)**, offering advanced features like **data compression**, **snapshots**, and **scalability**.
- **Solaris** uses the **Service Management Facility (SMF)**, a service management framework that enhances **reliability** and **availability** for system services.
- **Solaris** excels in supporting **high-end hardware** and **software systems**, making it ideal for large-scale **data centers** and **complex network infrastructures**.
- It uses the **Image Packaging System (IPS)** for **package management**, providing a **flexible** and **powerful** way to handle packages and updates.
- **Solaris** offers advanced **security features**, such as **Role-Based Access Control (RBAC)** and **mandatory access controls**, which are not universally available in all **Linux distributions**.
![[Screenshot_20241108_201827.png]]



### Differences
- Let's dive deeper into the differences between Solaris and Linux distributions. 
- One of the most important differences is that the source code is not open source and is only known in closed circles. 
- This means that unlike Ubuntu or many other distributions, the source code cannot be viewed and analyzed by the public. 
- In summary, the main differences can be grouped into the following categories:
	- Filesystem
	- Process management
	- Package management
	- Kernel and Hardware support
	- System monitoring
	- Security
- To better understand the differences, let's take a look at a few examples and commands.



### System Information
- On Ubuntu, we use the `uname` command to display information about the system, such as the kernel name, hostname, and operating system.
- This might look like something shown below.
```shell-session
secmancer@htb[/htb]$ uname -a

Linux ubuntu 5.4.0-1045 #48-Ubuntu SMP Fri Jan 15 10:47:29 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```
- On the other hand, in Solaris, the `showrev` command can be used to display system information, including the version of Solaris, hardware type, and patch level. 
- Here is an example output shown below.
```shell-session
$ showrev -a

Hostname: solaris
Kernel architecture: sun4u
OS version: Solaris 10 8/07 s10s_u4wos_12b SPARC
Application architecture: sparc
Hardware provider: Sun_Microsystems
Domain: sun.com
Kernel version: SunOS 5.10 Generic_139555-08
```
- The main difference between the two commands is that `showrev` provides more detailed information about the Solaris system, such as the patch level and hardware provider, while `uname` only provides basic information about the Linux system.



### Installing Packages
- On Ubuntu, the `apt-get` command is used to install packages. 
- This could look like the following example shown below.
```shell-session
secmancer@htb[/htb]$ sudo apt-get install apache2
```
- However, in Solaris, we need to use `pkgadd` to install packages like `SUNWapchr`.
```shell-session
$ pkgadd -d SUNWapchr
```
- The main difference between the two commands is the syntax, and the package manager used. 
- Ubuntu uses the Advanced Packaging Tool (APT) to manage packages, while Solaris uses the Solaris Package Manager (SPM). 
- Also, note that we do not use `sudo` in this case. 
- This is because Solaris used the `RBAC` privilege management tool, which allowed the assignment of granular permissions to users. 
- However, `sudo` has been supported since Solaris 11.



### Permission Management
- On Linux systems like Ubuntu but also on Solaris, the `chmod` command is used to change the permissions of files and directories.
- Here is an example command to give read, write, and execute permissions to the owner of the file:
```shell-session
secmancer@htb[/htb]$ chmod 700 filename
```
- To find files with specific permissions in Ubuntu, we use the `find` command.
- Let us take a look at an example of a file with the SUID bit set:
```shell-session
secmancer@htb[/htb]$ find / -perm 4000
```
- To find files with specific permissions, like with the SUID bit set on Solaris, we can use the find command, too, but with a small adjustment.
```shell-session
$ find / -perm -4000
```
- The main difference between these two commands is the use of the `-` before the permission value in the Solaris command. 
- This is because Solaris uses a different permission system than Linux.



### NFS in Solaris
- Solaris has its own implementation of NFS, which is slightly different from Linux distributions like Ubuntu. 
- In Solaris, the NFS server can be configured using the `share` command, which is used to share a directory over the network, and it also allows us to specify various options such as read/write permissions, access restrictions, and more. 
- To share a directory over NFS in Solaris, we can use the following command:
```shell-session
$ share -F nfs -o rw /export/home
```
- This command shares the `/export/home` directory with read and writes permissions over NFS.
- An NFS client can mount the NFS file system using the `mount` command, the same way as with Ubuntu. 
- To mount an NFS file system in Solaris, we need to specify the server name and the path to the shared directory. 
- For example, to mount an NFS share from a server with the IP address `10.129.15.122` and the shared directory `/nfs_share`, we use the following command.
```shell-session
secmancer@htb[/htb]$ mount -F nfs 10.129.15.122:/nfs_share /mnt/local
```
- In Solaris, the configuration for NFS is stored in the `/etc/dfs/dfstab` file. 
- This file contains entries for each shared directory, along with the various options for NFS sharing.
```shell-session
# cat /etc/dfs/dfstab

share -F nfs -o rw /export/home
```



### Process Mapping
- Process mapping is an essential aspect of system administration and troubleshooting. 
- The `lsof` command is a powerful utility that lists all the files opened by a process, including network sockets and other file descriptors that we can use in Debian distributions like Ubuntu. 
- We can use `lsof` to list all the files opened by a process. 
- For example, to list all the files opened by the Apache web server process, we can use the following command.
```shell-session
secmancer@htb[/htb]$ sudo lsof -c apache2
```
- In Solaris, the `pfiles` command can be used to list all the files opened by a process. 
- For example, to list all the files opened by the Apache web server process, we can use the following command:
```shell-session
$ pfiles `pgrep httpd`
```
- This command lists all the files opened by the Apache web server process. 
- The output of the `pfiles` command is similar to the output of the `lsof` command and provides information about the type of file descriptor, the file descriptor number, and the file name.



### Executable Access
- In Solaris, `truss` is used, which is a highly useful utility for developers and system administrators who need to debug complex software issues on the Solaris operating system.
- By tracing the system calls made by a process, `truss` can help identify the source of errors, performance issues, and other problems but can also reveal some sensitive information that may arise during application development or system maintenance. 
- The utility can also provide detailed information about system calls, including the arguments passed to them and their return values, allowing users to better understand the behavior of their applications and the underlying operating system.
- `Strace` is an alternative to `truss` but for Ubuntu, and it is an essential tool for system administrators and developers alike, helping them diagnose and troubleshoot issues in real-time.
- It enables users to analyze the interactions between the operating system and applications running on it, which is especially useful in highly complex and mission-critical environments. 
- With `truss`, users can quickly identify and isolate issues related to application performance, network connectivity, and system resource utilization, among others.
- For example, to trace the system calls made by the Apache web server process, we can use the following command.
```shell-session
secmancer@htb[/htb]$ sudo strace -p `pgrep apache2`
```
- Here's an example of how to use `truss` to trace the system calls made by the `ls` command in Solaris.
```shell-session
$ truss ls

execve("/usr/bin/ls", 0xFFBFFDC4, 0xFFBFFDC8)  argc = 1
...SNIP...
```
- The output is similar to `strace`, but the format is slightly different. 
- One difference between `strace` and `truss` is that `truss` can also trace the signals sent to a process, while `strace` cannot.
- Another difference is that `truss` has the ability to trace the system calls made by child processes, while `strace` can only trace the system calls made by the process specified on the command line.