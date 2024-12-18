### Object
- An object can be defined as ANY resource present within an Active Directory environment such as OUs, printers, users, domain controllers, etc.



### Attributes
- Every object in Active Directory has attributes defining its characteristics, such as a computer object's hostname and DNS name.
- Attributes have associated LDAP names for queries, e.g., `displayName` for "Full Name" and `givenName` for "First Name."



### Schema
- The Active Directory schema is the blueprint of the enterprise environment, defining object types and their attributes in the AD database.
- AD objects belong to specific classes, such as "user" for user accounts and "computer" for computer objects, with attributes storing their information (some required, others optional).
- Creating an object from a class is called instantiation, and the object becomes an instance of that class (e.g., the computer object "RDS01" is an instance of the "computer" class).



### Domain
- A domain is a logical group of objects such as computers, users, OUs, groups, etc.
- We can think of each domain as a different city within a state or country. 
- Domains can operate entirely independently of one another or be connected via trust relationships.



### Forest
- A forest is the topmost container in Active Directory, containing domains, users, groups, computers, Group Policy objects, and more.
- It can consist of one or multiple domains and operates independently, similar to a state in the US or a country in the EU.
- Forests can establish trust relationships with other forests.



### Tree
- A tree is a collection of Active Directory domains starting at a single root domain; a forest is a collection of AD trees.
- Domains in a tree share boundaries, and a parent-child trust relationship forms when a domain is added under another.
- Trees in the same forest cannot share a namespace (e.g., `inlanefreight.local` and `ilfreight.local` are distinct trees).
- Child domains inherit the parent domain's namespace (e.g., `corp.inlanefreight.local` and `corp.ilfreight.local`).
- All domains in a tree share a common Global Catalog containing information about all objects in the tree.



### Container
- Container objects hold other objects and have a defined place in the directory subtree hierarchy.



### Leaf
- Leaf objects do not contain other objects and are found at the end of the subtree hierarchy.



### Global Unique Identifier (GUID)
- A GUID is a unique 128-bit value assigned to every object in Active Directory, similar to a MAC address.
- The GUID is stored in the `ObjectGUID` attribute and is used by AD to identify objects internally.
- AD objects can be queried by their `ObjectGUID` using PowerShell or by specifying their distinguished name, GUID, SID, or SAM account name.
- Searching by GUID ensures accurate and reliable results, avoiding confusion with similar object names in the global catalog.
- The `ObjectGUID` never changes and remains associated with the object for its entire existence in the domain.



### Security principals
- Security principals include anything the operating system can authenticate, such as users, computer accounts, or processes running under a user or service account.
- In Active Directory, security principals are domain objects used to manage access to resources within the domain.
- Local user accounts and security groups control access to resources on a specific computer and are managed by the Security Accounts Manager (SAM), not Active Directory.



### Security Identifier (SID)
- A security identifier (SID) uniquely identifies a security principal or group and is issued by the domain controller in an AD environment.
- SIDs are unique and can only be used once; even if the security principal is deleted, the SID cannot be reused.
- When a user logs in, an access token is created containing their SID, rights, and group SIDs, which is used to verify permissions during actions.
- Well-known SIDs, such as the `Everyone` group, are consistent across all operating systems and identify generic users or groups.



### Distinguished Name (DN)
- A Distinguished Name (DN) specifies the full path to an object in Active Directory (e.g., `cn=bjones, ou=IT, ou=Employees, dc=inlanefreight, dc=local`).
- It identifies the object’s location in the directory hierarchy, such as `bjones` being in the IT department under the Employees OU.
- The Common Name (CN) is one method to search for or access the object within the domain.



### Relative Distinguished Name (RDN)
- A Relative Distinguished Name (RDN) is a single component of the Distinguished Name (DN) that uniquely identifies an object within its current level in the naming hierarchy.
- In the example, `bjones` is the RDN of the object.
- AD does not allow duplicate RDNs under the same parent container, but objects with the same RDN can exist in different DNs, making them unique (e.g., `cn=bjones,dc=dev,dc=inlanefreight,dc=local` is distinct from `cn=bjones,dc=inlanefreight,dc=local`).
![image](https://academy.hackthebox.com/storage/modules/74/dn_rdn2.png)



### sAMAccountName
- The [sAMAccountName](https://docs.microsoft.com/en-us/windows/win32/ad/naming-properties#samaccountname) is the user's logon name. 
- Here it would just be `bjones`. 
- It must be a unique value and 20 or fewer characters.


### userPrincipalName
- The [userPrincipalName](https://social.technet.microsoft.com/wiki/contents/articles/52250.active-directory-user-principal-name.aspx) attribute is another way to identify users in AD.
- This attribute consists of a prefix (the user account name) and a suffix (the domain name) in the format of `bjones@inlanefreight.local`. 
- This attribute is not mandatory.



### FSMO Roles
- Early Active Directory (AD) had issues with multiple Domain Controllers (DCs) competing for changes, sometimes causing improper updates, leading to the "last writer wins" model.
- This led to a flawed design with a single "master" DC applying changes, causing problems if the master DC went down.
- To resolve this, Microsoft introduced Flexible Single Master Operation (FSMO) roles, which distribute responsibilities across DCs to maintain authentication and authorization without interruption.
- There are five FSMO roles: `Schema Master`, `Domain Naming Master` (one per forest), `RID Master`, `PDC Emulator`, and `Infrastructure Master` (one per domain).
- The first DC in the forest root domain is assigned all five roles, while new domains only receive the RID Master, PDC Emulator, and Infrastructure Master roles.
- FSMO roles are typically set during DC creation but can be transferred as needed by sysadmins.
- These roles ensure smooth replication and the proper operation of critical AD services.



### Global Catalog
- A global catalog (GC) is a domain controller that stores copies of all objects in an Active Directory forest, including a full copy of its own domain's objects and partial copies of objects from other domains.
- Unlike standard domain controllers, which hold full replicas of objects from only their own domain, GCs provide access to information from any domain in the forest.
- The GC enables users and applications to search for objects across all domains in the forest by storing essential attributes of objects.
- GC functions include:
    - Authentication, which provides authorization for all groups a user belongs to when generating an access token.
    - Object search, allowing transparent searches across the entire forest by providing just one attribute of an object.



### Read-Only Domain Controller (RODC)
- A Read-Only Domain Controller (RODC) has a read-only Active Directory database and does not cache AD account passwords (except for the RODC computer account and RODC KRBTGT passwords).
- No changes are pushed out from an RODC's AD database, SYSVOL, or DNS.
- RODCs include a read-only DNS server, enable administrator role separation, reduce replication traffic, and prevent SYSVOL modifications from being replicated to other DCs.



### Replication
- Replication in Active Directory occurs when AD objects are updated and transferred between Domain Controllers (DCs).
- When a new DC is added, connection objects are created to manage replication between DCs.
- The Knowledge Consistency Checker (KCC) service, present on all DCs, manages these replication connections.
- Replication ensures that changes are synchronized across all DCs in the forest, providing redundancy in case a DC fails.



### Service Principal Name (SPN)
- A Service Principal Name (SPN) uniquely identifies a service instance.
- SPNs are used by Kerberos authentication to associate a service instance with a logon account.
- This allows a client application to request service authentication without needing to know the account name.



### Group Policy Object (GPO)
- Group Policy Objects (GPOs) are virtual collections of policy settings with a unique GUID.
- GPOs can contain local file system settings or Active Directory settings.
- GPO settings can be applied to both user and computer objects.
- They can be applied domain-wide or more granularly at the Organizational Unit (OU) level.



### Access Control List (ACL)
- An [Access Control List (ACL)](https://docs.microsoft.com/en-us/windows/win32/secauthz/access-control-lists) is the ordered collection of Access Control Entries (ACEs) that apply to an object.



### Access Control Entries (ACEs)
- Each [Access Control Entry (ACE)](https://docs.microsoft.com/en-us/windows/win32/secauthz/access-control-entries) in an ACL identifies a trustee (user account, group account, or logon session) and lists the access rights that are allowed, denied, or audited for the given trustee.



### Discretionary Access Control List (DACL)
- DACLs (Discretionary Access Control Lists) define which security principals are granted or denied access to an object, containing a list of ACEs (Access Control Entries).
- When a process tries to access an object, the system checks the ACEs in the DACL to determine if access should be granted.
- If an object lacks a DACL, full access is granted to everyone, but if the DACL has no ACEs, all access attempts are denied.
- ACEs in the DACL are checked sequentially until a matching entry allows or denies access.



### System Access Control Lists (SACL)
- Allows for administrators to log access attempts that are made to secured objects. 
- ACEs specify the types of access attempts that cause the system to generate a record in the security event log.



### Fully Qualified Domain Name (FQDN)
- An FQDN (Fully Qualified Domain Name) is the complete name for a specific computer or host, consisting of the hostname, domain name, and top-level domain (TLD), written as `[hostname].[domain].[tld]`.
- It specifies an object's location in the DNS hierarchy and allows locating hosts in Active Directory without needing the IP address.
- For example, the host `DC01` in the domain `INLANEFREIGHT.LOCAL` would have the FQDN `DC01.INLANEFREIGHT.LOCAL`.



### Tombstone
- A **tombstone** is a container object in Active Directory that holds deleted AD objects.
- When an object is deleted, it remains in the tombstone state for a set period known as the **Tombstone Lifetime**, with the `isDeleted` attribute set to `TRUE`.
- After the Tombstone Lifetime expires, the object is fully removed from AD.
- The recommended Tombstone Lifetime is 180 days, though this may vary across environments, and defaults to 60 or 180 days depending on the DC operating system version.
- If AD Recycle Bin is not enabled, deleted objects become tombstones, with most of their attributes stripped and placed in the `Deleted Objects` container. While the object can be recovered, lost attributes cannot be restored.



### AD Recycle Bin
- The **AD Recycle Bin** was introduced in Windows Server 2008 R2 to simplify the recovery of deleted AD objects.
- It eliminates the need for restoring from backups, restarting AD DS, or rebooting a Domain Controller.
- When enabled, deleted objects are preserved for a specified period, with the default retention period being 60 days if not configured otherwise.
- The AD Recycle Bin preserves most attributes of deleted objects, making it easier to fully restore them to their previous state.



### SYSVOL
- The **SYSVOL** folder stores public files in the domain, such as system policies, Group Policy settings, logon/logoff scripts, and other administrative scripts.
- It is replicated to all Domain Controllers (DCs) within the environment using File Replication Services (FRS).
- SYSVOL ensures that these critical files are consistently available across all DCs in the Active Directory environment.



### AdminSDHolder
- The **AdminSDHolder** object manages ACLs for members of privileged groups in Active Directory (AD), ensuring they have the correct security settings.
- It acts as a container for the Security Descriptor applied to protected group members.
- The **SDProp (SD Propagator)** process runs every hour by default on the PDC Emulator Domain Controller, checking and enforcing the correct ACL for members of protected groups.
- If an attacker modifies the ACL of a privileged group member, the SDProp process will correct the settings during its scheduled run, removing unauthorized changes.



### dsHeuristics
- The **dsHeuristics** attribute is a string value set on the Directory Service object to define forest-wide configuration settings.
- One of these settings allows for the exclusion of built-in groups from the **Protected Groups** list.
- Groups in the Protected Groups list are protected from modification via the **AdminSDHolder** object, and any changes to them are reverted by the SDProp process.
- If a group is excluded via the **dsHeuristics** attribute, changes affecting it will not be reverted by the SDProp process.



### adminCount
- The **adminCount** attribute determines if the SDProp process protects a user in Active Directory.
- If **adminCount** is set to `0` or not specified, the user is not protected by SDProp.
- If **adminCount** is set to `1`, the user is considered protected and subject to SDProp enforcement.
- Attackers often target accounts with **adminCount** set to `1`, as these are usually privileged accounts, potentially leading to further access or domain compromise.



### Active Directory Users and Computers (ADUC)
- ADUC is a GUI console commonly used for managing users, groups, computers, and contacts in AD. Changes made in ADUC can be done via PowerShell as well.



### ADSI Edit
- **ADSI Edit** is a GUI tool for managing AD objects, offering more functionality than ADUC.
- It allows users to set or delete attributes, add, remove, and move objects in AD.
- It provides deep access to AD, making it a powerful but risky tool.
- Changes made with ADSI Edit can cause significant problems in AD, so caution is required when using it.



### sIDHistory
- The **SIDHistory** attribute stores previously assigned SIDs for an object, often used during migrations to retain access levels.
- It can be exploited if not securely managed, allowing attackers to gain elevated access from prior domains if **SID Filtering** is not enabled.
- If SID Filtering is disabled, attackers could potentially use old SIDs for unauthorized access.



### NTDS.DIT
- The **NTDS.DIT** file, located at `C:\Windows\NTDS\`, is the core database of Active Directory, storing crucial data like user and group information, group memberships, and password hashes.
- Attackers can steal this file after a domain compromise to extract password hashes and perform pass-the-hash attacks or crack them offline using tools like Hashcat.
- If **Store password with reversible encryption** is enabled, the NTDS.DIT file will also contain cleartext passwords for users who changed their password after the policy was set, which can be exploited.



### MSBROWSE
- **MSBROWSE** is a Microsoft networking protocol used in early Windows-based LANs to maintain a list of network resources (like shared printers and files) and facilitate browsing and access.
- In older versions of Windows, `nbtstat -A <ip-address>` could be used to identify the **Master Browser**, with MSBROWSE indicating its presence. The `nltest` utility could also query a Master Browser for Domain Controller names.
- Today, **MSBROWSE** is largely obsolete, replaced by **SMB** for file and printer sharing and **CIFS** for browsing services in modern Windows networks.



### Questions
- What is known as the "Blueprint" of an Active Directory environment?
	- schema
- What uniquely identifies a Service instance? (full name, space-separated, not abbreviated)
	- Service Principal Name
- True or False; Group Policy objects can be applied to user and computer objects.
	- True
- What container in AD holds deleted objects?
	- tombstone
- What file contains the hashes of passwords for all users in a domain?
	- NTDS.DIT