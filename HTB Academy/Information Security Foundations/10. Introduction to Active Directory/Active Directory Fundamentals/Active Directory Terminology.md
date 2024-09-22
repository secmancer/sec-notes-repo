Here’s a concise version of the key Active Directory terminology from the provided text:

1. **Object**: Any resource in AD (e.g., users, computers).
2. **Attributes**: Characteristics of AD objects, defined by schema, and accessible via LDAP (e.g., `displayName`).
3. **Schema**: The blueprint defining object types and attributes in AD.
4. **Domain**: A logical group of AD objects that can function independently or have trust relationships.
5. **Forest**: A collection of AD domains sharing a common schema and catalog.
6. **Tree**: A hierarchy of domains within a forest that share a namespace.
7. **Container**: Holds other objects within the directory hierarchy.
8. **Leaf**: Objects at the end of a directory branch, not containing other objects.
9. **Global Unique Identifier (GUID)**: A unique 128-bit identifier for AD objects.
10. **Security Principals**: AD objects like users and computers that the system can authenticate.
11. **Security Identifier (SID)**: A unique identifier for users, groups, or processes.
12. **Distinguished Name (DN)**: The full path to an AD object.
13. **Relative Distinguished Name (RDN)**: A unique name of an object at its current directory level.
14. **sAMAccountName**: A unique user login name (20 characters max).
15. **userPrincipalName (UPN)**: Alternative unique user identifier in email format.
16. **FSMO Roles**: Five roles assigned to DCs to prevent conflicts: Schema Master, Domain Naming Master, RID Master, PDC Emulator, Infrastructure Master.
17. **Global Catalog (GC)**: Stores a full copy of all objects in the current domain and partial copies of objects from other domains.
18. **Read-Only Domain Controller (RODC)**: A domain controller that stores a read-only AD database, typically used in remote or less secure locations.
19. **Replication**: Synchronization of AD objects between domain controllers.
20. **Service Principal Name (SPN)**: Uniquely identifies services for Kerberos authentication.
21. **Group Policy Object (GPO)**: Virtual collections of policy settings applied to users and computers.
22. **Access Control List (ACL)**: List of permissions for accessing objects.
23. **Access Control Entries (ACE)**: Defines specific permissions for a trustee in the ACL.
24. **Discretionary Access Control List (DACL)**: Grants or denies access to an object.
25. **System Access Control List (SACL)**: Logs access attempts to secured objects.
26. **Fully Qualified Domain Name (FQDN)**: The complete name for a computer or host, specifying its location in DNS.
27. **Tombstone**: Temporary container for deleted AD objects, with a set lifetime.
28. **AD Recycle Bin**: Allows recovery of deleted AD objects, preserving most attributes.
29. **SYSVOL**: Folder storing copies of public domain files, like system policies and logon scripts.
30. **AdminSDHolder**: Manages ACLs for privileged AD groups.
31. **dsHeuristics**: Configures forest-wide settings, including AdminSDHolder protection exclusions.
32. **adminCount**: Attribute determining if an account is protected by SDProp.
33. **Active Directory Users and Computers (ADUC)**: GUI for managing AD objects like users and computers.
34. **ADSI Edit**: A more powerful GUI tool for managing AD, with access to advanced object attributes.
35. **sIDHistory**: Holds previous SIDs, typically used in domain migrations.
36. **NTDS.DIT**: The AD database, containing user/group data and password hashes.
37. **MSBROWSE**: An older protocol for network resource browsing, largely obsolete today.

![[dn_rdn2.png]]

## Questions
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