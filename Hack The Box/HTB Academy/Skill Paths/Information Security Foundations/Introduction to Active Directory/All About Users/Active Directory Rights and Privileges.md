### Introduction
- **Rights** and **privileges** are critical aspects of AD management and must be carefully managed to avoid abuse by attackers or penetration testers.
- **Rights** are permissions to access objects (e.g., files), while **privileges** grant permission to perform actions (e.g., run programs, reset passwords).
- Privileges can be assigned individually or granted through group membership, either built-in or custom.
- Windows has a concept of **User Rights Assignment**, which assigns privileges to users but is often referred to as rights.
- Understanding the difference between rights and privileges is essential for effective AD management and security.



### Built-in AD Groups
- AD has many **default or built-in security groups**, some of which grant powerful rights and privileges that can be abused to escalate privileges and gain Domain Admin or SYSTEM access on a Domain Controller (DC).
- **Excessive group membership/privileges** is a common security flaw in AD environments, often targeted by attackers.
- Tight management of membership in these built-in groups is crucial to prevent privilege escalation within the domain.
- Some of the most common built-in groups should be carefully monitored to avoid misuse.

| Group Name                           | Description                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Account Operators`                  | Members can create and modify most types of accounts, including those of users, local groups, and global groups, and members can log in locally to domain controllers. They cannot manage the Administrator account, administrative user accounts, or members of the Administrators, Server Operators, Account Operators, Backup Operators, or Print Operators groups.            |
| `Administrators`                     | Members have full and unrestricted access to a computer or an entire domain if they are in this group on a Domain Controller.                                                                                                                                                                                                                                                     |
| `Backup Operators`                   | Members can back up and restore all files on a computer, regardless of the permissions set on the files. Backup Operators can also log on to and shut down the computer. Members can log onto DCs locally and should be considered Domain Admins. They can make shadow copies of the SAM/NTDS database, which, if taken, can be used to extract credentials and other juicy info. |
| `DnsAdmins`                          | Members have access to network DNS information. The group will only be created if the DNS server role is or was at one time installed on a domain controller in the domain.                                                                                                                                                                                                       |
| `Domain Admins`                      | Members have full access to administer the domain and are members of the local administrator's group on all domain-joined machines.                                                                                                                                                                                                                                               |
| `Domain Computers`                   | Any computers created in the domain (aside from domain controllers) are added to this group.                                                                                                                                                                                                                                                                                      |
| `Domain Controllers`                 | Contains all DCs within a domain. New DCs are added to this group automatically.                                                                                                                                                                                                                                                                                                  |
| `Domain Guests`                      | This group includes the domain's built-in Guest account. Members of this group have a domain profile created when signing onto a domain-joined computer as a local guest.                                                                                                                                                                                                         |
| `Domain Users`                       | This group contains all user accounts in a domain. A new user account created in the domain is automatically added to this group.                                                                                                                                                                                                                                                 |
| `Enterprise Admins`                  | Membership in this group provides complete configuration access within the domain. The group only exists in the root domain of an AD forest. Members in this group are granted the ability to make forest-wide changes such as adding a child domain or creating a trust. The Administrator account for the forest root domain is the only member of this group by default.       |
| `Event Log Readers`                  | Members can read event logs on local computers. The group is only created when a host is promoted to a domain controller.                                                                                                                                                                                                                                                         |
| `Group Policy Creator Owners`        | Members create, edit, or delete Group Policy Objects in the domain.                                                                                                                                                                                                                                                                                                               |
| `Hyper-V Administrators`             | Members have complete and unrestricted access to all the features in Hyper-V. If there are virtual DCs in the domain, any virtualization admins, such as members of Hyper-V Administrators, should be considered Domain Admins.                                                                                                                                                   |
| `IIS_IUSRS`                          | This is a built-in group used by Internet Information Services (IIS), beginning with IIS 7.0.                                                                                                                                                                                                                                                                                     |
| `Pre–Windows 2000 Compatible Access` | This group exists for backward compatibility for computers running Windows NT 4.0 and earlier. Membership in this group is often a leftover legacy configuration. It can lead to flaws where anyone on the network can read information from AD without requiring a valid AD username and password.                                                                               |
| `Print Operators`                    | Members can manage, create, share, and delete printers that are connected to domain controllers in the domain along with any printer objects in AD. Members are allowed to log on to DCs locally and may be used to load a malicious printer driver and escalate privileges within the domain.                                                                                    |
| `Protected Users`                    | Members of this [group](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups#protected-users) are provided additional protections against credential theft and tactics such as Kerberos abuse.                                                                                                                   |
| `Read-only Domain Controllers`       | Contains all Read-only domain controllers in the domain.                                                                                                                                                                                                                                                                                                                          |
| `Remote Desktop Users`               | This group is used to grant users and groups permission to connect to a host via Remote Desktop (RDP). This group cannot be renamed, deleted, or moved.                                                                                                                                                                                                                           |
| `Remote Management Users`            | This group can be used to grant users remote access to computers via [Windows Remote Management (WinRM)](https://docs.microsoft.com/en-us/windows/win32/winrm/portal)                                                                                                                                                                                                             |
| `Schema Admins`                      | Members can modify the Active Directory schema, which is the way all objects with AD are defined. This group only exists in the root domain of an AD forest. The Administrator account for the forest root domain is the only member of this group by default.                                                                                                                    |
| `Server Operators`                   | This group only exists on domain controllers. Members can modify services, access SMB shares, and backup files on domain controllers. By default, this group has no members.                                                                                                                                                                                                      |



### Server Operators Group Details

```powershell-session
PS C:\htb>  Get-ADGroup -Identity "Server Operators" -Properties *

adminCount                      : 1
CanonicalName                   : INLANEFREIGHT.LOCAL/Builtin/Server Operators
CN                              : Server Operators
Created                         : 10/27/2021 8:14:34 AM
createTimeStamp                 : 10/27/2021 8:14:34 AM
Deleted                         : 
Description                     : Members can administer domain servers
DisplayName                     : 
DistinguishedName               : CN=Server Operators,CN=Builtin,DC=INLANEFREIGHT,DC=LOCAL
dSCorePropagationData           : {10/28/2021 1:47:52 PM, 10/28/2021 1:44:12 PM, 10/28/2021 1:44:11 PM, 10/27/2021 
                                  8:50:25 AM...}
GroupCategory                   : Security
GroupScope                      : DomainLocal
groupType                       : -2147483643
HomePage                        : 
instanceType                    : 4
isCriticalSystemObject          : True
isDeleted                       : 
LastKnownParent                 : 
ManagedBy                       : 
MemberOf                        : {}
Members                         : {}
Modified                        : 10/28/2021 1:47:52 PM
modifyTimeStamp                 : 10/28/2021 1:47:52 PM
Name                            : Server Operators
nTSecurityDescriptor            : System.DirectoryServices.ActiveDirectorySecurity
ObjectCategory                  : CN=Group,CN=Schema,CN=Configuration,DC=INLANEFREIGHT,DC=LOCAL
ObjectClass                     : group
ObjectGUID                      : 0887487b-7b07-4d85-82aa-40d25526ec17
objectSid                       : S-1-5-32-549
ProtectedFromAccidentalDeletion : False
SamAccountName                  : Server Operators
sAMAccountType                  : 536870912
sDRightsEffective               : 0
SID                             : S-1-5-32-549
SIDHistory                      : {}
systemFlags                     : -1946157056
uSNChanged                      : 228556
uSNCreated                      : 12360
whenChanged                     : 10/28/2021 1:47:52 PM
whenCreated                     : 10/27/2021 8:14:34 AM
```

- The **`Server Operators`** group is by default empty and is a domain local group.
- The **`Domain Admins`** group has several members and service accounts assigned, and it is a global group.
- It's critical to be cautious about who is given access to these groups, as they confer powerful administrative privileges.
- If an attacker gains access to a user in these groups, they could potentially gain full control over the enterprise.



### Domain Admins Group Membership

```powershell-session
PS C:\htb>  Get-ADGroup -Identity "Domain Admins" -Properties * | select DistinguishedName,GroupCategory,GroupScope,Name,Members

DistinguishedName : CN=Domain Admins,CN=Users,DC=INLANEFREIGHT,DC=LOCAL
GroupCategory     : Security
GroupScope        : Global
Name              : Domain Admins
Members           : {CN=htb-student_adm,CN=Users,DC=INLANEFREIGHT,DC=LOCAL, CN=sharepoint
                    admin,CN=Users,DC=INLANEFREIGHT,DC=LOCAL, CN=FREIGHTLOGISTICSUSER,OU=Service
                    Accounts,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL, CN=PROXYAGENT,OU=Service
                    Accounts,OU=Corp,DC=INLANEFREIGHT,DC=LOCAL...}
```
- The **`Server Operators`** group is by default empty and is a domain local group.
- The **`Domain Admins`** group has several members and service accounts assigned, and it is a global group.
- It's critical to be cautious about who is given access to these groups, as they confer powerful administrative privileges.
- If an attacker gains access to a user in these groups, they could potentially gain full control over the enterprise.



### User Rights Assignment
- Users can have various rights assigned to their accounts based on their group membership and Group Policy settings.
- The [User Rights Assignment](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/user-rights-assignment) article from Microsoft provides a detailed breakdown of the rights that can be configured in Windows.
- While not all rights are crucial from a security perspective, some can lead to privilege escalation or unauthorized access to sensitive files.
- For instance, gaining write access over a Group Policy Object (GPO) applied to an OU could allow an attacker to assign targeted rights to a user.
- Tools like [SharpGPOAbuse](https://github.com/FSecureLABS/SharpGPOAbuse) can be used to exploit such privileges for further access in the domain.
- There are various techniques available to abuse user rights, detailed in resources like [this blog post](https://blog.palantir.com/windows-privilege-abuse-auditing-detection-and-defense-3078a403d74e) and [HackTricks](https://book.hacktricks.xyz/windows/windows-local-privilege-escalation/privilege-escalation-abusing-tokens).
- It's crucial to understand the significant impact of incorrectly assigning privileges in Active Directory.
- A small administrative mistake in privilege assignment can lead to a complete system or enterprise compromise.

| **Privilege**                   | **Description**                                                                                                                                                                                                                                                                                   |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `SeRemoteInteractiveLogonRight` | This privilege could give our target user the right to log onto a host via Remote Desktop (RDP), which could potentially be used to obtain sensitive data or escalate privileges.                                                                                                                 |
| `SeBackupPrivilege`             | This grants a user the ability to create system backups and could be used to obtain copies of sensitive system files that can be used to retrieve passwords such as the SAM and SYSTEM Registry hives and the NTDS.dit Active Directory database file.                                            |
| `SeDebugPrivilege`              | This allows a user to debug and adjust the memory of a process. With this privilege, attackers could utilize a tool such as [Mimikatz](https://github.com/ParrotSec/mimikatz) to read the memory space of the Local System Authority (LSASS) process and obtain any credentials stored in memory. |
| `SeImpersonatePrivilege`        | This privilege allows us to impersonate a token of a privileged account such as `NT AUTHORITY\SYSTEM`. This could be leveraged with a tool such as JuicyPotato, RogueWinRM, PrintSpoofer, etc., to escalate privileges on a target system.                                                        |
| `SeLoadDriverPrivilege`         | A user with this privilege can load and unload device drivers that could potentially be used to escalate privileges or compromise a system.                                                                                                                                                       |
| `SeTakeOwnershipPrivilege`      | This allows a process to take ownership of an object. At its most basic level, we could use this privilege to gain access to a file share or a file on a share that was otherwise not accessible to us.                                                                                           |



### Viewing a User's Privileges
- The command `whoami /priv` lists all user rights assigned to the current user after logging into a host. Some rights are restricted to administrative users and can only be accessed with an elevated CMD or PowerShell session.
- Elevated rights and **User Account Control (UAC)**, introduced in Windows Vista, limit applications from running with full permissions unless necessary. These security features help prevent unauthorized actions from gaining full system control.
- A comparison of rights between a non-elevated and elevated console shows significant differences in available privileges for an admin.
- The next step is to examine the rights available to a standard Active Directory user.
- #### Standard Domain User's Rights

```powershell-session
PS C:\htb> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== ========
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled
```

- We can see that the rights are very `limited`, and none of the "dangerous" rights outlined above are present. 
- Next, let's take a look at a privileged user. Below are the rights available to a Domain Admin user.



### Domain Admin Rights Non-Elevated
- In a **non-elevated** console, standard domain users typically see only the basic rights available to them. Windows systems don't grant all rights unless the console is run with elevated privileges.
- This approach helps prevent every application from running with the highest possible privileges, a process controlled by **User Account Control (UAC)**.
- UAC is designed to restrict the escalation of privileges for applications unless explicitly required, ensuring a layer of security.

```powershell-session
PS C:\htb> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                          State
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege       Bypass traverse checking             Enabled
SeUndockPrivilege             Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set       Disabled
SeTimeZonePrivilege           Change the time zone                 Disabled
```



### Domain Admin Rights Elevated
- If we enter the same command from an elevated PowerShell console, we can see the complete listing of rights available to us.
- **User rights** increase depending on the groups a user belongs to or the privileges assigned to them. For example, a **Backup Operators** group member gains additional rights compared to a standard user.
- Even though **UAC** may restrict some rights (such as `SeBackupPrivilege`), a user in this group can still have rights like `SeShutdownPrivilege`, which allows them to shut down a domain controller.
- While this privilege doesn’t directly provide access to sensitive data, it can cause significant service interruptions if the user logs onto a domain controller locally (as opposed to remotely via RDP or WinRM).

```powershell-session
PS C:\htb> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                            Description                                                        State
========================================= ================================================================== ========
SeIncreaseQuotaPrivilege                  Adjust memory quotas for a process                                 Disabled
SeMachineAccountPrivilege                 Add workstations to domain                                         Disabled
SeSecurityPrivilege                       Manage auditing and security log                                   Disabled
SeTakeOwnershipPrivilege                  Take ownership of files or other objects                           Disabled
SeLoadDriverPrivilege                     Load and unload device drivers                                     Disabled
SeSystemProfilePrivilege                  Profile system performance                                         Disabled
SeSystemtimePrivilege                     Change the system time                                             Disabled
SeProfileSingleProcessPrivilege           Profile single process                                             Disabled
SeIncreaseBasePriorityPrivilege           Increase scheduling priority                                       Disabled
SeCreatePagefilePrivilege                 Create a pagefile                                                  Disabled
SeBackupPrivilege                         Back up files and directories                                      Disabled
SeRestorePrivilege                        Restore files and directories                                      Disabled
SeShutdownPrivilege                       Shut down the system                                               Disabled
SeDebugPrivilege                          Debug programs                                                     Enabled
SeSystemEnvironmentPrivilege              Modify firmware environment values                                 Disabled
SeChangeNotifyPrivilege                   Bypass traverse checking                                           Enabled
SeRemoteShutdownPrivilege                 Force shutdown from a remote system                                Disabled
SeUndockPrivilege                         Remove computer from docking station                               Disabled
SeEnableDelegationPrivilege               Enable computer and user accounts to be trusted for delegation     Disabled
SeManageVolumePrivilege                   Perform volume maintenance tasks                                   Disabled
SeImpersonatePrivilege                    Impersonate a client after authentication                          Enabled
SeCreateGlobalPrivilege                   Create global objects                                              Enabled
SeIncreaseWorkingSetPrivilege             Increase a process working set                                     Disabled
SeTimeZonePrivilege                       Change the time zone                                               Disabled
SeCreateSymbolicLinkPrivilege             Create symbolic links                                              Disabled
SeDelegateSessionUserImpersonatePrivilege Obtain an impersonation token for another user in the same session Disabled
```



### Backup Operator Rights
- Both **attackers** and **defenders** must understand the rights granted to users through membership in **built-in security groups** in Active Directory.
- It's common to find low-privileged users mistakenly added to high-privileged groups, which can be exploited to compromise the domain.
- Access to these groups should be **strictly controlled**. It's recommended to leave most groups empty and only add accounts when necessary for specific tasks.
- Accounts in these groups or granted additional privileges should be **carefully monitored**, have **strong passwords** or **passphrases**, and be separate from sysadmin accounts used for daily tasks.
- Now that we've covered security considerations around user privileges and group memberships, let’s review **best practices** for securing an **Active Directory** installation.
```powershell-session
PS C:\htb> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                Description                    State
============================= ============================== ========
SeShutdownPrivilege           Shut down the system           Disabled
SeChangeNotifyPrivilege       Bypass traverse checking       Enabled
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled
```



## Questions
- What built-in group will grant a user full and unrestricted access to a computer?
	- Administrators
- What user right grants a user the ability to make backups of a system?
	- SeBackupPrivilege
- What Windows command can show us all user rights assigned to the current user?
	- whoami /priv