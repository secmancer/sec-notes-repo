### Active Directory Security Hardening Overview

Active Directory (AD) facilitates centralized management and rapid information sharing across a large user base. While these functionalities are beneficial, they also pose security risks, as AD is often considered insecure by default without appropriate hardening measures. To mitigate potential attacks, balancing the **Confidentiality, Integrity, and Availability (CIA)** triad is essential, although AD typically leans towards **Availability and Confidentiality**. By tweaking built-in features, organizations can better secure their AD environments. Below are some key hardening measures and security best practices.

---

### General AD Hardening Measures

- **Microsoft Local Administrator Password Solution (LAPS)**:
  - Randomizes and rotates local administrator passwords on Windows hosts to prevent lateral movement.
  - Reduces the impact of a single compromised host.

- **Audit Policy Settings (Logging and Monitoring)**:
  - Enable robust logging to detect unauthorized changes, account modifications, or advanced attacks like Kerberos abuse.

- **Group Policy Security Settings**:
  - **Account Policies**: Manage passwords, account lockout, and Kerberos ticket settings.
  - **Local Policies**: Control security settings such as administrative privileges and network access.
  - **Software and Application Control Policies**: Restrict software and app execution, with tools like AppLocker limiting access to PowerShell or CMD.
  - **Advanced Audit Policy Configuration**: Monitor activities like file access, logon/logoff, policy changes, etc.

- **Update Management (SCCM/WSUS)**:
  - Ensure timely deployment of patches via WSUS or SCCM to cover all critical hosts, preventing vulnerabilities from going unpatched.

- **Group Managed Service Accounts (gMSA)**:
  - Provide automatic password management for non-interactive applications, eliminating the need for password knowledge and reducing password risks.

---

### Security Groups & Account Separation

- **Security Groups**:
  - Use these to assign rights and permissions, ensuring specific access to resources like file shares, printers, and folders.

- **Account Separation**:
  - Admins should have separate accounts for day-to-day tasks and privileged operations to minimize risks from phishing or compromised hosts.

---

### Password Management & Multi-Factor Authentication

- **Password Complexity**:
  - Encourage long passphrases or randomly generated passwords. Set a minimum of 12 characters for standard users, with longer passwords for admins.

- **Multi-Factor Authentication (MFA)**:
  - Enable MFA for Remote Desktop Protocol (RDP) access to reduce the risk of lateral movement.

---

### Limiting Domain Admin Account Usage

- **Domain Admins** should only log in to **Domain Controllers** to limit password exposure in hosts' memory. 

---

### Periodic Audits and Monitoring

- **Remove Stale Accounts**: Periodically audit and disable unused accounts to minimize the attack surface.
  
- **Audit Permissions**: Limit the number of **Domain Admins** and **Enterprise Admins** and regularly review local admin rights and file share access.

- **Robust Logging**: Implement audit policies to detect anomalous activities, such as failed login attempts indicative of password spraying or AD enumeration.

---

### Other Security Measures

- **Restricted Groups**: Use Group Policy to control group memberships, such as the local administrator group and key administrative groups.
  
- **Server Role Limitation**: Avoid installing unnecessary roles (e.g., IIS on Domain Controllers) to reduce the attack surface.

- **Limiting Local Admin and RDP Rights**: Restrict local admin rights to reduce the risk of privilege escalation. Limit RDP access to minimize potential exposure to attacks.

---

By implementing these security measures, organizations can harden their AD environment and enhance their defense-in-depth strategy. Microsoft's best practices for securing AD provide further guidance for maintaining a secure infrastructure.

![[CIA-triad-diag.png]]


## Questions
- Confidentiality, <___>, and Availability are the pillars of the CIA Triad. What term is missing? (fill in the blank)
	- Integrity
- What security policies can block certain users from running all executables?
	- Application Control Policies