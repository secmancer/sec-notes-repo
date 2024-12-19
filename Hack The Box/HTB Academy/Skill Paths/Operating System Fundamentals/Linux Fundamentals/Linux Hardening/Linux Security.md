### Introduction
- All computer systems have an inherent risk of intrusion, with some presenting higher risks, such as internet-facing web servers hosting complex applications. 
- While Linux systems are less prone to viruses that affect Windows and have a smaller attack surface compared to Active Directory domain-joined hosts, security measures are still crucial.
- One key security measure for Linux systems is keeping the OS and installed packages up to date.
- This can be achieved with the command shown below.
- Proper firewall configuration is essential, and `iptables` can be used to restrict traffic into and out of the Linux host if network-level rules are not set.
- SSH configuration should disallow password logins and root logins, and administrators should avoid using the root user for day-to-day tasks. Access should follow the principle of least privilege, with specific commands allowed via `sudoers` for users needing root-level access.
- Tools like `fail2ban` can help prevent brute-force attacks by banning hosts after a defined number of failed login attempts.
- Regular audits should be conducted to identify and address issues like outdated kernels, improper user permissions, world-writable files, misconfigured cron jobs, or services that may facilitate privilege escalation.
- Security-Enhanced Linux (SELinux) or AppArmor can enforce granular access control policies, ensuring only authorized users and applications access specific resources.
- Additional security tools such as Snort, chkrootkit, rkhunter, and Lynis can help identify and mitigate security risks.
- Security settings include disabling unnecessary services, enforcing strong passwords, implementing password aging, locking accounts after failed login attempts, and removing unwanted SUID/SGID binaries.
- Security is an ongoing process, and the effectiveness of protection depends on how well system administrators understand and manage the operating system. Proper training and continuous improvement of security measures are key.
```shell-session
secmancer@htb[/htb]$ apt update && apt dist-upgrade
```



### TCP Wrappers
- **TCP Wrapper** is a security feature on Linux systems that enables administrators to control which clients can access certain services based on their IP address or hostname. When a client attempts to connect, the system checks the **`/etc/hosts.allow`** and **`/etc/hosts.deny`** configuration files to determine whether access should be granted or denied.
- **`/etc/hosts.allow`** specifies which services and IP addresses/hostnames are allowed to access the system. If a client matches an entry in this file, they are permitted access to the corresponding service.
- **`/etc/hosts.deny`** lists services and IP addresses/hostnames that are explicitly denied access. If a client matches an entry here, the connection will be rejected.
- The two files work together to provide a layered access control mechanism:
    - If a client’s IP address or hostname is found in **`/etc/hosts.allow`**, they are granted access to the specified services.
    - If found in **`/etc/hosts.deny`**, access is blocked.
    - If no entry is found for the client, the default behavior depends on the configuration of the service, but typically, access will be denied if no other rule matches.
- #### /etc/hosts.allow
```shell-session
secmancer@htb[/htb]$ cat /etc/hosts.allow

# Allow access to SSH from the local network
sshd : 10.129.14.0/24

# Allow access to FTP from a specific host
ftpd : 10.129.14.10

# Allow access to Telnet from any host in the inlanefreight.local domain
telnetd : .inlanefreight.local
```
- #### /etc/hosts.deny
```shell-session
secmancer@htb[/htb]$ cat /etc/hosts.deny

# Deny access to all services from any host in the inlanefreight.com domain
ALL : .inlanefreight.com

# Deny access to SSH from a specific host
sshd : 10.129.22.22

# Deny access to FTP from hosts with IP addresses in the range of 10.129.22.0 to 10.129.22.255
ftpd : 10.129.22.0/24
```
- It is important to remember that the order of the rules in the files is important. 
- The first rule that matches the requested service and host is the one that will be applied. 
- It is also important to note that TCP wrappers are not a replacement for a firewall, as they are limited by the fact that they can only control access to services and not to ports.