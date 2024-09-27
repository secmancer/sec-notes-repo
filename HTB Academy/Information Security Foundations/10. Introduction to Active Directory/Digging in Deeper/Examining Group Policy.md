Here are your notes on Group Policy:

### Overview of Group Policy
- **Definition**: Group Policy is a Windows feature allowing administrators to manage settings for user and computer accounts in a Windows environment.
- **Local Group Policy**: Every Windows host has a Local Group Policy editor for managing local settings.
- **Domain Context**: Focus on managing users and computers in Active Directory (AD).
- **Management Tool**: Group Policy is powerful for managing user settings, operating systems, applications, and security in a domain.

### Security Context
- **Enhances Security**: Properly used Group Policy can significantly improve an enterprise's security posture.
- **Vulnerable to Abuse**: Attackers can exploit Group Policy Objects (GPOs) for lateral movement, privilege escalation, and domain compromise.
- **Understanding GPOs**: Knowledge of Group Policy aids in defending against attackers and assists in penetration testing.

### Group Policy Objects (GPOs)
- **Definition**: A GPO is a collection of policy settings applied to users or computers.
- **Settings Include**:
  - Screen lock timeout
  - Disabling USB ports
  - Custom domain password policies
  - Software installation
  - Remote access settings
- **Linking**: GPOs can be linked to Organizational Units (OUs), domains, or sites and can apply to individual users or groups.

### Examples of GPOs
- Different password policies for service/admin/standard accounts
- Preventing removable media usage
- Enforcing screensaver passwords
- Restricting access to certain applications (e.g., cmd.exe, PowerShell)
- Enforcing audit and logging policies
- Deploying software domain-wide
- Displaying logon banners
- Disallowing LM hash usage

### Password Complexity Example (Windows Server 2008)
- **Requirements**:
  - Minimum of 7 characters
  - Must include characters from at least three categories:
    - Uppercase (A-Z)
    - Lowercase (a-z)
    - Numbers (0-9)
    - Special characters (e.g., !@#$%^&*()_+|~-=`{}[]:";'<>?,./)

### RDP GPO Settings
- Detailed settings can be applied for Remote Desktop sessions.

### GPO Processing Order
1. **Local Group Policy**: Overrides domain settings if defined locally.
2. **Site Policy**: Specific policies for the enterprise site.
3. **Domain-wide Policy**: Applies settings across the entire domain.
4. **Organizational Unit (OU)**: Unique settings for specific OUs.
5. **Nested OU Policies**: Specific permissions for objects within nested OUs.

### Managing Group Policy
- **Tools**: Group Policy Management Console, custom applications, PowerShell GroupPolicy module.
- **Default Domain Policy**: Automatically created, applies domain-wide settings.
- **Default Domain Controllers Policy**: Sets baseline security/auditing for domain controllers.

### GPO Precedence
- GPOs are processed from top to bottom; settings in lower OUs take precedence.
- **Computer policies** have higher priority over user policies.
- **Enforced Option**: GPO settings cannot be overridden by lower OU policies.
- **Block Inheritance Option**: Prevents higher-level policies from applying to specific OUs.

### Group Policy Refresh Frequency
- Default refresh every 90 minutes (+/- 30 minutes offset).
- Domain controllers refresh every 5 minutes.
- Use `gpupdate /force` to manually refresh settings.

### Security Considerations
- **Potential for Abuse**: GPOs can be exploited for attacks, e.g., modifying user rights, creating admin accounts, or deploying malware.
- **Example Attack Path**: Using tools like BloodHound to identify vulnerabilities and potential targets.

### Conclusion
- Active Directory and Group Policy are complex and essential for managing network security and configurations. Further exploration and practical application are necessary to master these concepts.

![[bh_gpo.png]]


![[gpo_levels.png]]


## Questions
- Computer settings for Group Policies are gathered and applied at a <___> minute interval? (answer is a number, fill in the blank )
	- 90
- True or False: A policy applied to a user at the domain level would be overwritten by a policy at the site level.
	- False
- What Group Policy Object is created when the domain is created?
	- Default Domain Policy