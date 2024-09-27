### Notes on Active Directory (AD) Rights, Privileges, and Built-in Groups

#### **Key Concepts: Rights vs. Privileges**
- **Rights**: Assigned to users/groups and deal with *permissions to access objects* (e.g., files).
- **Privileges**: Enable a user to *perform actions* (e.g., running programs, shutting down systems, resetting passwords). Can be assigned directly or via group membership.
- Windows uses the concept of **User Rights Assignment**, which, while termed as "rights," actually refers to privileges.

#### **Built-in AD Groups**
Many default AD groups grant significant rights and privileges, often targeted by attackers. Membership should be tightly managed. Some critical groups include:
1. **Account Operators**: Create/modify user and group accounts. Cannot manage Admin or other key operator accounts.
2. **Administrators**: Full access to computers/domains.
3. **Backup Operators**: Can back up/restore all files and log onto domain controllers (DCs).
4. **DnsAdmins**: Manage DNS server roles if installed on DCs.
5. **Domain Admins**: Full domain control and admin rights across domain-joined machines.
6. **Domain Users/Computers**: Contains user accounts or computers in the domain.
7. **Enterprise Admins**: Configuration access for the entire forest. Exists only in the root domain.
8. **Server Operators**: Modify services, access file shares, and manage domain controller backups. Should be carefully managed.

#### **Key Privileges to Monitor**
Some privileges, if misused, can lead to privilege escalation or data theft. Examples include:
- **SeRemoteInteractiveLogonRight**: Allows RDP login, potentially exposing sensitive data or escalating privileges.
- **SeBackupPrivilege**: Enables system backups, which can be exploited to extract sensitive files (e.g., SAM/NTDS.dit).
- **SeDebugPrivilege**: Allows access to process memory, often used by tools like Mimikatz to extract credentials.
- **SeImpersonatePrivilege**: Allows impersonation of privileged accounts like SYSTEM.
- **SeLoadDriverPrivilege**: Can load drivers, leading to potential system compromise.
- **SeTakeOwnershipPrivilege**: Enables taking ownership of objects like files or shares.

#### **Viewing User Privileges**
- The `whoami /priv` command can list assigned privileges, which differ for standard vs. elevated users.
- Elevated sessions (e.g., with admin rights) will show more extensive privileges compared to standard users.

Understanding these concepts is crucial for both defending against attacks and conducting penetration testing within Active Directory environments. Mismanagement of rights and privileges can lead to significant security vulnerabilities.


## Questions
- What built-in group will grant a user full and unrestricted access to a computer?
	- Administrators
- What user right grants a user the ability to make backups of a system?
	- SeBackupPrivilege
- What Windows command can show us all user rights assigned to the current user?
	- whoami /priv