### Introduction
- User accounts are created on both local systems and Active Directory to provide login access and resource permissions based on assigned rights.
- When a user logs in, their password is verified, and an **access token** is created, which includes their security identity and group membership.
- User accounts allow individuals or services to log in, run programs or services under specific security contexts, and manage access to resources like files and applications.
- Users can be assigned to groups to simplify privilege management, as group members inherit the privileges assigned to the group.
- User account provisioning and management are key elements of Active Directory, with most organizations having at least one AD user account per person.
- Service accounts may also be used to run applications or services in the background, adding to the total number of accounts in an organization.
- In large organizations (e.g., 1,000 employees), there may be over 1,200 user accounts, with some disabled accounts remaining for audit purposes (e.g., former employees or temporary staff) stored in organizational units like `FORMER EMPLOYEES`.
![image](https://academy.hackthebox.com/storage/modules/74/all_users.png)
- User accounts in Active Directory can be provisioned with a wide range of rights, from basic read-only access (Domain User) to full control (Enterprise Admin).
- Due to the broad spectrum of rights that can be assigned, user accounts are prone to misconfigurations that could be exploited by attackers or penetration testers.
- User accounts are a significant attack surface and a primary focus for gaining access during penetration tests.
- Human behavior, such as weak passwords, unauthorized software, and administrative mistakes, makes users often the weakest link in an organization's security.
- Organizations need policies and defense-in-depth strategies to mitigate risks posed by user accounts and address potential security vulnerabilities.
- While specifics on user-related attacks are beyond this module's scope, understanding the potential impact of users in Active Directory is crucial.



### Local Accounts
- **Local Accounts**: Stored on individual servers or workstations, granting rights only on that specific host. They cannot be used across a domain.
- **Default Local User Accounts**:
    - **Administrator**: Full control over the system, cannot be deleted or locked, but can be disabled or renamed. Disabled by default in Windows 10 and Server 2016.
    - **Guest**: Disabled by default, allows temporary limited access for users without an account, and typically has a blank password.
    - **SYSTEM**: The highest permission level account used by Windows to perform internal functions, granted Full Control to all files. Cannot be added to groups and does not have a profile.
    - **Network Service**: Used by the Service Control Manager to run services, presenting credentials to remote services.
    - **Local Service**: Used by the Service Control Manager with minimal privileges, presenting anonymous credentials to the network.
- For more details, study Microsoft's documentation on [local default accounts](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/local-accounts).



### Domain Users
- **Domain Users**: Granted rights by the domain to access resources (e.g., file servers, printers) based on their account permissions or group membership. They can log in to any host within the domain.
- **KRBTGT Account**: A built-in local account in Active Directory that supports the Key Distribution Service for authentication and domain resource access. It is a common target for attackers.
    - **KRBTGT Attack**: Gaining control of the KRBTGT account allows attackers to execute a **Golden Ticket** attack, granting them unrestricted access to the domain and enabling privilege escalation and persistence.
- For more information on Active Directory account types, refer to [this Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-accounts).



### User Naming Attributes
- Security in Active Directory can be improved using a set of user naming attributes to help identify user objects like logon name or ID. 
- The following are a few important Naming Attributes in AD.

|                           |                                                                                                                                                                                                                                                                                  |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `UserPrincipalName` (UPN) | This is the primary logon name for the user. By convention, the UPN uses the email address of the user.                                                                                                                                                                          |
| `ObjectGUID`              | This is a unique identifier of the user. In AD, the ObjectGUID attribute name never changes and remains unique even if the user is removed.                                                                                                                                      |
| `SAMAccountName`          | This is a logon name that supports the previous version of Windows clients and servers.                                                                                                                                                                                          |
| `objectSID`               | The user's Security Identifier (SID). This attribute identifies a user and its group memberships during security interactions with the server.                                                                                                                                   |
| `sIDHistory`              | This contains previous SIDs for the user object if moved from another domain and is typically seen in migration scenarios from domain to domain. After a migration occurs, the last SID will be added to the `sIDHistory` property, and the new SID will become its `objectSID`. |

- #### Common User Attributes
	- For a deeper look at user object attributes, check out this [page](https://docs.microsoft.com/en-us/windows/win32/ad/user-object-attributes). 
	- Many attributes can be set for any object in AD. 
	- Many objects will never be used or are not relevant to us as security professionals. 
	- Still, it is essential to familiarize ourselves with the most common and more obscure ones that may contain sensitive data or help mount an attack.
```powershell-session
PS C:\htb Get-ADUser -Identity htb-student

DistinguishedName : CN=htb student,CN=Users,DC=INLANEFREIGHT,DC=LOCAL
Enabled           : True
GivenName         : htb
Name              : htb student
ObjectClass       : user
ObjectGUID        : aa799587-c641-4c23-a2f7-75850b4dd7e3
SamAccountName    : htb-student
SID               : S-1-5-21-3842939050-3880317879-2865463114-1111
Surname           : student
UserPrincipalName : htb-student@INLANEFREIGHT.LOCAL
```




### Domain-joined vs. Non-Domain-joined Machines
- **Domain-Joined Hosts**:
    
    - Easier information sharing and centralized management via Domain Controllers (DCs).
    - Hosts acquire configurations and updates through Group Policy.
    - Users can log in and access resources from any domain-joined host, common in enterprise environments.
- **Non-Domain-Joined Hosts (Workgroup)**:
    
    - Not managed by domain policies; resource sharing outside the local network is more complex.
    - Users have control over changes on their individual host; accounts and profiles don't migrate across machines.
    - **SYSTEM account** on a domain-joined host has rights similar to a standard domain user and can be leveraged to enumerate and attack the domain, even without obtaining individual user credentials.
    - **SYSTEM access** can be used as a starting point for domain enumeration and gathering domain-related information.



## Questions
- True or False; A local user account can be used to login to any domain connected host.
	- False
- What default user account has the SID "S-1-5-domain-500" ?
	- Administrator
- What account has the highest permission level possible on a Windows host
	- SYSTEM
- What user naming attribute is unique to the user and will remain so even if the account is deleted?
	- ObjectGUID