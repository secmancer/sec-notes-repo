### Securing Linux Systems

**1. Keeping Software Updated:**

- Regularly update the OS and installed packages using: sudo apt update && sudo apt dist-upgrade

**2. Firewall Configuration:**

- Use Linux's built-in firewall (e.g., `ufw` or `iptables`) to restrict traffic.

**3. SSH Configuration:**

- Disable password logins and root access via SSH in `/etc/ssh/sshd_config`:
	- PasswordAuthentication no
	- PermitRootLogin no
- Use SSH keys for authentication.

**4. Access Control:**

- Apply the principle of least privilege for user permissions.
- Use `sudo` for privilege escalation instead of logging in as root.
- Configure `sudoers` to specify which commands a user can run with elevated privileges.

**5. Intrusion Prevention:**

- Use `fail2ban` to protect against brute force attacks by banning IPs after a number of failed login attempts.

**6. Regular Audits:**

- Check for privilege escalation vectors like outdated kernels, improper permissions, world-writable files, and misconfigured cron jobs.

**7. SELinux/AppArmor:**

- Implement SELinux or AppArmor for granular access control policies:
    - SELinux: Enforces access control based on labels assigned to processes and files.
    - AppArmor: Uses profiles to restrict applications' capabilities.

**8. Security Tools:**

- Utilize tools such as Snort, chkrootkit, rkhunter, and Lynis for system security and monitoring.

**9. Basic Security Settings:**

- Remove or disable unnecessary services and software.
- Avoid unencrypted authentication mechanisms.
- Ensure NTP and Syslog services are running.
- Enforce strong passwords and configure password aging.
- Lock user accounts after failed login attempts.
- Disable unwanted SUID/SGID binaries.

**10. Continuous Improvement:**

- Security is an ongoing process; administrators should stay informed and regularly review security practices.

### TCP Wrappers

**TCP Wrappers Overview:**

- A security mechanism to control access to services based on IP addresses or hostnames.
- Configured using `/etc/hosts.allow` and `/etc/hosts.deny`.

**Configuration Files:**

1. **/etc/hosts.allow:**
    
    - Specifies which services and hosts are allowed access.
    - Example:
	    - sshd : 10.129.14.0/24
		- ftpd : 10.129.14.10
		- telnetd : .inlanefreight.local
2. **/etc/hosts.deny:*
	- Specifies which services and hosts are denied access.
	- Example:
		- ALL : .inlanefreight.com
		- sshd : 10.129.22.22
		- ftpd : 10.129.22.0/24

**Important Considerations:**

- Rules in `/etc/hosts.allow` and `/etc/hosts.deny` are evaluated in order. The first matching rule applies.
- TCP Wrappers do not replace firewalls but add an additional layer of access control.

These practices and configurations are foundational to maintaining a secure Linux environment and should be complemented with ongoing monitoring and updates.
