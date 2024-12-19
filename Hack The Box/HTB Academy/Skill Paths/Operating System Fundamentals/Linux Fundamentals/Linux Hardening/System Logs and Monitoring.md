### Introduction
- **System logs** in Linux are crucial for monitoring system behavior, application activity, and security events, helping identify potential security weaknesses and vulnerabilities.
- By analyzing these logs, penetration testers can identify abnormal activities, such as unauthorized logins, attempted attacks, or unusual file access, indicating potential security breaches.
- Reviewing system logs post-security testing helps assess the effectiveness of testing activities and refine testing strategies.
- Proper configuration of system logs includes setting log levels, configuring log rotation, securing log storage, and regularly reviewing logs for potential security risks.
- Common types of **system logs** on Linux include:
    - Kernel Logs
    - System Logs
    - Authentication Logs
    - Application Logs
    - Security Logs



### Kernel Logs
- **Kernel logs** contain information about the system's kernel, including hardware drivers, system calls, and kernel events, stored in the `/var/log/kern.log` file.
- They can reveal vulnerable or outdated drivers, system crashes, resource limitations, and other events that may lead to security issues, such as denial of service.
- Kernel logs can help identify suspicious system calls or activities that may indicate malware or malicious software.
- Monitoring the `/var/log/kern.log` file allows detection of unusual behavior, enabling timely action to prevent further damage.



### System Logs
- **System logs** record system-level events, such as service starts, stops, login attempts, and system reboots, and are stored in the `/var/log/syslog` file.
- Analyzing these logs helps detect access attempts and system activities, identifying potential vulnerabilities and security risks.
- The `syslog` can also highlight performance or availability issues, such as failed service starts or unexpected reboots.
- This information is crucial for recommending security measures and resolving issues that could affect system stability or performance.



### Syslog
```shell-session
Feb 28 2023 15:00:01 server CRON[2715]: (root) CMD (/usr/local/bin/backup.sh)
Feb 28 2023 15:04:22 server sshd[3010]: Failed password for htb-student from 10.14.15.2 port 50223 ssh2
Feb 28 2023 15:05:02 server kernel: [  138.303596] ata3.00: exception Emask 0x0 SAct 0x0 SErr 0x0 action 0x6 frozen
Feb 28 2023 15:06:43 server apache2[2904]: 127.0.0.1 - - [28/Feb/2023:15:06:43 +0000] "GET /index.html HTTP/1.1" 200 13484 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36"
Feb 28 2023 15:07:19 server sshd[3010]: Accepted password for htb-student from 10.14.15.2 port 50223 ssh2
Feb 28 2023 15:09:54 server kernel: [  367.543975] EXT4-fs (sda1): re-mounted. Opts: errors=remount-ro
Feb 28 2023 15:12:07 server systemd[1]: Started Clean PHP session files.
```



### Authentication Logs
- **Authentication logs** store information about user login attempts, both successful and failed, and are located in the `/var/log/auth.log` file.
- Unlike the general system logs in `/var/log/syslog`, the `/var/log/auth.log` file specifically focuses on authentication events, making it a crucial resource for detecting potential security threats.
- Penetration testers should regularly review these logs to identify suspicious activities, such as brute-force attacks or unauthorized login attempts, ensuring the system's security.



### Auth.log
```shell-session
Feb 28 2023 18:15:01 sshd[5678]: Accepted publickey for admin from 10.14.15.2 port 43210 ssh2: RSA SHA256:+KjEzN2cVhIW/5uJpVX9n5OB5zVJ92FtCZxVzzcKjw
Feb 28 2023 18:15:03 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/bin/bash
Feb 28 2023 18:15:05 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/usr/bin/apt-get install netcat-traditional
Feb 28 2023 18:15:08 sshd[5678]: Disconnected from 10.14.15.2 port 43210 [preauth]
Feb 28 2023 18:15:12 kernel: [  778.941871] firewall: unexpected traffic allowed on port 22
Feb 28 2023 18:15:15 auditd[9876]: Audit daemon started successfully
Feb 28 2023 18:15:18 systemd-logind[1234]: New session 4321 of user admin.
Feb 28 2023 18:15:21 CRON[2345]: pam_unix(cron:session): session opened for user root by (uid=0)
Feb 28 2023 18:15:24 CRON[2345]: pam_unix(cron:session): session closed for user root
```
- In this example, we can see in the first line that a successful public key has been used for authentication for the user `admin`. 
- Additionally, we can see that this user is in the `sudoers` group because he can execute commands using `sudo`. 
- The kernel message indicates that unexpected traffic was allowed on port 22, which could indicate a potential security breach.
- After that, we see that a new session was created for user "admin" by `systemd-logind` and that a `cron` session opened and closed for the user `root`.



### Application Logs
- **Application logs** contain information about the activities of specific applications on the system, such as web servers or databases. They are typically stored in their own dedicated files, like `/var/log/apache2/error.log` for Apache or `/var/log/mysql/error.log` for MySQL.
- These logs are crucial for identifying vulnerabilities, misconfigurations, unauthorized access attempts, and data exfiltration, especially when targeting specific applications.
- **Access and audit logs** are key for tracking user and process activities, and are vital for security and compliance. Access logs record user interactions with the system (e.g., login attempts, file accesses), while audit logs track security-relevant events (e.g., modifications to system configurations).
- Reviewing these logs helps identify potential security threats, breaches, or misconfigurations that could expose the system to attacks.
- #### Access Log Entry
```shell-session
2023-03-07T10:15:23+00:00 servername privileged.sh: htb-student accessed /root/hidden/api-keys.txt
```
- In this log entry, we can see that the user `htb-student` used the `privileged.sh` script to access the `api-keys.txt` file in the `/root/hidden/` directory. 
- On Linux systems, most common services have default locations for access logs:
![[Screenshot_20241108_202323.png]]



### Security Logs
- **Security logs** are stored in various log files, depending on the tool or application. For example:
    - **Fail2ban** logs failed login attempts in `/var/log/fail2ban.log`.
    - **UFW** (Uncomplicated Firewall) records activity in `/var/log/ufw.log`.
    - General security events like system file changes may be logged in `/var/log/syslog` or `/var/log/auth.log`.
- **Penetration testers** can use log analysis to identify security issues by searching for specific events or patterns, helping to detect vulnerabilities or attack vectors.
- Familiarity with default log locations is essential for effective security assessments, as it enables better identification of security-related events.
- Logs can be analyzed using tools like built-in log file viewers, or command-line tools (`tail`, `grep`, `sed`), aiding in the detection of security breaches and system troubleshooting.