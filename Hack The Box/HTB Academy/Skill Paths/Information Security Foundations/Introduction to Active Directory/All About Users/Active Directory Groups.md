### Introduction
- **Groups** in Active Directory are used to organize users and manage permissions, but they can be a target for attackers due to potential excessive or unintended privileges.
- Active Directory includes many **built-in groups**, and organizations often create **custom groups** to manage access.
- The number of groups can become overwhelming, leading to potential misconfigurations and unintended access if not properly managed.
- Regular **audits** of groups and their privileges are necessary to ensure users have appropriate access.
- **Groups** assign resource permissions, while **Organizational Units (OUs)** are used for management and Group Policy deployment. OUs also help delegate administrative tasks without granting full admin rights.



### Types of Groups
- **Groups** are used to manage users, computers, and contact objects in Active Directory, simplifying the administration of permissions and resource access (e.g., printers, file shares).
- Instead of assigning permissions individually, a sysadmin can create a **group** and grant it permissions, making it easier to manage access for multiple users.
- **Group membership** allows users to inherit permissions, and modifying access can be done by removing users from the group without affecting others.
- **Group Type** and **Group Scope** are the two main characteristics of groups in Active Directory:
    - **Security groups** are used to assign permissions and rights to a collection of users, simplifying management.
    - **Distribution groups** are used for email distribution, like mailing lists, but cannot be used for resource permissions in a domain.
![image](https://academy.hackthebox.com/storage/modules/74/group-options2.png)



### Group Scopes
- There are three different `group scopes` that can be assigned when creating a new group.
	1. Domain Local Group
	2. Global Group
	3. Universal Group



### Domain Local Group
- Domain local groups can only be used to manage permissions to domain resources in the domain where it was created. 
- Local groups cannot be used in other domains but `CAN` contain users from `OTHER` domains.
- Local groups can be nested into (contained within) other local groups but `NOT` within global groups.



### Global Group
- Global groups can be used to grant access to resources in `another domain`. 
- A global group can only contain accounts from the domain where it was created. 
- Global groups can be added to both other global groups and local groups.



### Universal Group
- **Universal Groups** are used to manage resources across multiple domains and can be given permissions within the same **forest**. They are available to all domains within an organization and can contain users from any domain.
- Universal groups are stored in the **Global Catalog (GC)** and trigger **forest-wide replication** when objects are added or removed, which can create network overhead if managed improperly.
- It's recommended to use **global groups** as members of universal groups, as global group membership is more stable than individual user membership, reducing replication events.
- **Replication** occurs at the domain level for changes in global groups, but forest-wide replication occurs when changes are made to universal groups containing individual users or computers.
- **Group Scope Changes**:
    - A **Global Group** can only be converted to a **Universal Group** if it is not part of another global group.
    - A **Domain Local Group** can only be converted to a **Universal Group** if it does not contain other domain local groups.
    - **Universal Groups** can be converted to a **Domain Local Group** without restrictions.
    - **Universal Groups** can be converted to a **Global Group** only if they do not contain other universal groups.

```powershell-session
PS C:\htb> Get-ADGroup  -Filter * |select samaccountname,groupscope

samaccountname                           groupscope
--------------                           ----------
Administrators                          DomainLocal
Users                                   DomainLocal
Guests                                  DomainLocal
Print Operators                         DomainLocal
Backup Operators                        DomainLocal
Replicator                              DomainLocal
Remote Desktop Users                    DomainLocal
Network Configuration Operators         DomainLocal
Distributed COM Users                   DomainLocal
IIS_IUSRS                               DomainLocal
Cryptographic Operators                 DomainLocal
Event Log Readers                       DomainLocal
Certificate Service DCOM Access         DomainLocal
RDS Remote Access Servers               DomainLocal
RDS Endpoint Servers                    DomainLocal
RDS Management Servers                  DomainLocal
Hyper-V Administrators                  DomainLocal
Access Control Assistance Operators     DomainLocal
Remote Management Users                 DomainLocal
Storage Replica Administrators          DomainLocal
Domain Computers                             Global
Domain Controllers                           Global
Schema Admins                             Universal
Enterprise Admins                         Universal
Cert Publishers                         DomainLocal
Domain Admins                                Global
Domain Users                                 Global
Domain Guests                                Global

<SNIP>
```



### Built-in vs. Custom Groups
- When a domain is created, several **built-in security groups** with a **Domain Local Group** scope are automatically created for specific administrative purposes.
- These built-in groups do not allow for **group nesting** (groups within groups). For example, the **Domain Admins** group is a **Global security group** and can only contain accounts from its own domain.
- To grant an account from **domain B** administrative access to a domain controller in **domain A**, the account would need to be added to the **Domain Local** Administrators group.
- While Active Directory comes with many prepopulated groups, **organizations often create additional groups** for their own purposes, both **security** and **distribution** groups.
- Adding services like **Microsoft Exchange** can trigger the creation of additional highly privileged security groups, which, if not managed properly, may lead to privileged access within the domain.



### Nested Group Membership
- **Nested group membership** in Active Directory allows a **Domain Local Group** to be a member of another Domain Local Group within the same domain, enabling users to inherit privileges indirectly.
- This inheritance can lead to **unintended privileges** being granted to users, which are difficult to uncover without a thorough domain assessment.
- Tools like **BloodHound** help uncover inherited privileges, making it easier for penetration testers and sysadmins to identify security misconfigurations and gain a deep visual understanding of the domain's security posture.
- For example, a user like `DCorner` may not directly belong to the **Helpdesk Level 1** group, but their membership in **Help Desk** grants them the same privileges, such as adding members to the **Tier 1 Admins** group, which could provide elevated access.
- If a group like **Tier 1 Admins** grants administrative privileges, it can become a key target for attackers to exploit, allowing them to escalate privileges and gain further access.
- #### Examining Nested Groups via BloodHound
![image](https://academy.hackthebox.com/storage/modules/74/bh_nested_groups.png)




### Important Group Attributes
- Like users, groups have many [attributes](http://www.selfadsi.org/group-attributes.htm). Some of the most [important group attributes](https://docs.microsoft.com/en-us/windows/win32/ad/group-objects) include:
- `cn`: The `cn` or Common-Name is the name of the group in Active Directory Domain Services.
- `member`: Which user, group, and contact objects are members of the group.
- `groupType`: An integer that specifies the group type and scope.
- `memberOf`: A listing of any groups that contain the group as a member (nested group membership).
- `objectSid`: This is the security identifier or SID of the group, which is the unique value used to identify the group as a security principal.
- Groups are fundamental objects in AD that can be used to group other objects together and facilitate the management of rights and access. 
- Take the time to study the differences between group types and scopes.
- This knowledge is useful for administering AD as well as understanding the relationships between groups in the same and different domains and what information can be enumerated during the recon phase of a penetration test. 
- Understanding how different group types can be utilized to perform attacks in a single domain and across trust boundaries is an excellent bit of knowledge to have. 
- We deep-dived into Groups in this section, now let's examine the differences between `Rights` and `Privileges`.



### Questions
- What group type is best utilized for assigning permissions and right to users?
	- Security
- True or False; A "Global Group" can only contain accounts from the domain where it was created.
	- True
- Can a Universal group be converted to a Domain Local group? (yes or no)
	- yes