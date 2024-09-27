### User Accounts Overview
- **User accounts**: Created locally (not joined to AD) or in Active Directory (AD) for logging into computers and accessing resources based on assigned rights.
- **Access token**: Generated after login, contains user's security identity and group membership, presented during process interactions.
- **Groups**: Users can be grouped to simplify privilege management. Assigning rights to a group allows all members to inherit those rights.
- **Service accounts**: Used to run background applications or services with specific privileges.

### Active Directory User Accounts
- **AD user accounts**: Usually one per employee, but may have additional accounts for specific roles (e.g., IT admin). Service accounts are often prevalent.
- **Disabled accounts**: Many organizations keep accounts from former employees deactivated for auditing purposes.
- **Rights**: User accounts can have a wide range of rights, from read-only access to full domain control.
- **Misconfigurations**: Improperly configured user rights can be exploited by attackers during penetration tests. Users often introduce vulnerabilities (e.g., weak passwords).

### Local Accounts (Windows)
- **Local accounts**: Stored on the specific system and manage access only to that system.
  - **Administrator**: Full control, disabled by default in modern Windows versions, can’t be deleted or locked.
  - **Guest**: Limited access, disabled by default.
  - **SYSTEM**: Highest-level account, used for OS functions, has full control but no user profile.
  - **Network Service**: Used for services needing network communication.
  - **Local Service**: Minimal privileges, presents anonymous credentials.

### Domain Users (Active Directory)
- **Domain user accounts**: Access resources across the domain, not restricted to individual hosts. 
- **KRBTGT account**: A service account for the Key Distribution service, targeted by attackers for domain-wide access (e.g., in the Golden Ticket attack).
  
### Important AD User Naming Attributes
- **UserPrincipalName (UPN)**: The primary logon name, typically an email address.
- **ObjectGUID**: A unique identifier that persists even if the user is deleted.
- **SAMAccountName**: A backward-compatible logon name.
- **ObjectSID**: The user's Security Identifier, used in security interactions.
- **SIDHistory**: Contains previous SIDs, useful in domain migrations.

### Domain-Joined vs. Non-Domain-Joined Machines
- **Domain-joined**: Easier resource sharing and centralized management through Group Policy, users can log into any domain-joined machine.
- **Non-domain-joined**: Resources are not managed by domain policies, useful for home use or small LANs. User accounts exist only on individual hosts.
- **Machine account access**: SYSTEM-level access in a domain environment has many rights similar to a domain user account and can be used to gather domain information or attack AD.

## Questions
- True or False; A local user account can be used to login to any domain connected host.
	- False
- What default user account has the SID "S-1-5-domain-500" ?
	- Administrator
- What account has the highest permission level possible on a Windows host
	- SYSTEM
- What user naming attribute is unique to the user and will remain so even if the account is deleted?
	- ObjectGUID