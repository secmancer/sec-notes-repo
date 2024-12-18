### FSMO
- As mentioned before, there are five Flexible Single Master Operation (FSMO) roles.
- These roles may be assigned to specific DCs or has a default DC depending on the organization.
- Issues with FSMO can lead to authentication/authorization difficulties within a domain.

| **Roles**                  | **Description**                                                                                                                                                                                                                                                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Schema Master`            | This role manages the read/write copy of the AD schema, which defines all attributes that can apply to an object in AD.                                                                                                                                                                                            |
| `Domain Naming Master`     | Manages domain names and ensures that two domains of the same name are not created in the same forest.                                                                                                                                                                                                             |
| `Relative ID (RID) Master` | The RID Master assigns blocks of RIDs to other DCs within the domain that can be used for new objects. The RID Master helps ensure that multiple objects are not assigned the same SID. Domain object SIDs are the domain SID combined with the RID number assigned to the object to make the unique SID.          |
| `PDC Emulator`             | The host with this role would be the authoritative DC in the domain and respond to authentication requests, password changes, and manage Group Policy Objects (GPOs). The PDC Emulator also maintains time within the domain.                                                                                      |
| `Infrastructure Master`    | This role translates GUIDs, SIDs, and DNs between domains. This role is used in organizations with multiple domains in a single forest. The Infrastructure Master helps them to communicate. If this role is not functioning properly, Access Control Lists (ACLs) will show SIDs instead of fully resolved names. |




### Domain and Forest Functional Levels
- Functional levels determine various features/capabilities available to us in Active Directory Domain Services (AD DS) at both the domain and forest level.
- Used to specify which Window Server versions can run a Domain Controller at the domain or forest level.
	- [This](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754918\(v=ws.10\)?redirectedfrom=MSDN) and [this](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels) article shows this, from Windows 2000 to Windows Server 2012.
- Below is a table of differences in `domain functional levels` from different Windows Server operating systems.
- A new functional level was not added with the release of Windows Server 2019. 
	- However, Windows Server 2008 functional level is the minimum requirement for adding Server 2019 Domain Controllers to an environment. 
	- Also, the target domain has to use [DFS-R](https://docs.microsoft.com/en-us/windows-server/storage/dfs-replication/dfsr-overview) for SYSVOL replication.
- Forest functional levels have introduced a few key capabilities over the years.

| Domain Functional Level | Features Available                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Supported Domain Controller Operating Systems                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| Windows 2000 native     | Universal groups for distribution and security groups, group nesting, group conversion (between security and distribution and security groups), SID history.                                                                                                                                                                                                                                                                                                                               | Windows Server 2008 R2, Windows Server 2008, Windows Server 2003, Windows 2000                                |
| Windows Server 2003     | Netdom.exe domain management tool, lastLogonTimestamp attribute introduced, well-known users and computers containers, constrained delegation, selective authentication.                                                                                                                                                                                                                                                                                                                   | Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 |
| Windows Server 2008     | Distributed File System (DFS) replication support, Advanced Encryption Standard (AES 128 and AES 256) support for the Kerberos protocol, Fine-grained password policies                                                                                                                                                                                                                                                                                                                    | Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008                      |
| Windows Server 2008 R2  | Authentication mechanism assurance, Managed Service Accounts                                                                                                                                                                                                                                                                                                                                                                                                                               | Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2                                           |
| Windows Server 2012     | KDC support for claims, compound authentication, and Kerberos armoring                                                                                                                                                                                                                                                                                                                                                                                                                     | Windows Server 2012 R2, Windows Server 2012                                                                   |
| Windows Server 2012 R2  | Extra protections for members of the Protected Users group, Authentication Policies, Authentication Policy Silos                                                                                                                                                                                                                                                                                                                                                                           | Windows Server 2012 R2                                                                                        |
| Windows Server 2016     | [Smart card required for interactive logon](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/interactive-logon-require-smart-card) new [Kerberos](https://docs.microsoft.com/en-us/windows-server/security/kerberos/whats-new-in-kerberos-authentication) features and new [credential protection](https://docs.microsoft.com/en-us/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection) features | Windows Server 2019 and Windows Server 2016                                                                   |

| **Version**              | **Capabilities**                                                                                                                                                                                               |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Windows Server 2003`    | saw the introduction of the forest trust, domain renaming, read-only domain controllers (RODC), and more.                                                                                                      |
| `Windows Server 2008`    | All new domains added to the forest default to the Server 2008 domain functional level. No additional new features.                                                                                            |
| `Windows Server 2008 R2` | Active Directory Recycle Bin provides the ability to restore deleted objects when AD DS is running.                                                                                                            |
| `Windows Server 2012`    | All new domains added to the forest default to the Server 2012 domain functional level. No additional new features.                                                                                            |
| `Windows Server 2012 R2` | All new domains added to the forest default to the Server 2012 R2 domain functional level. No additional new features.                                                                                         |
| `Windows Server 2016`    | [Privileged access management (PAM) using Microsoft Identity Manager (MIM).](https://docs.microsoft.com/en-us/windows-server/identity/whats-new-active-directory-domain-services#privileged-access-management) |



### Trusts
- Used to establish both `forest-forest` or `domain-domain` authentication.
	- Allows users to access resources or administer other domains outside of the domain that user was originally created in.
	- Creates a link between the authentication systems of two domains.
- Several trust types exist, which are shown in the table below.
- Example is given in the image below.
- Can be either transitive or non-transitive.
	- Transitive: trust is extended to objects that the child domain trusts
	- Non-transitive: only the child domain itself is trusted.
- Can also either be one-way or two way.
	- One-way: only users within a trusted domain can access those resources
	- Two way:  both uses from a trust domain can access those resources
- Often, these are created improperly, allowing for unintended attack paths.
- They can also may not be reviewed for a god time for potential security implications.
- Merges/acquisitions can result in these trusts, especially from acquired companies, to become vulnerable.
- It's uncommon to be able to perform an attack, like Kerberoasting, against a domain outside the principle domain, to get access to an administrator account.
![image](https://academy.hackthebox.com/storage/modules/74/trusts-diagram.png)

| **Trust Type** | **Description**                                                                                                                                                        |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Parent-child` | Domains within the same forest. The child domain has a two-way transitive trust with the parent domain.                                                                |
| `Cross-link`   | a trust between child domains to speed up authentication.                                                                                                              |
| `External`     | A non-transitive trust between two separate domains in separate forests which are not already joined by a forest trust. This type of trust utilizes SID filtering.     |
| `Tree-root`    | a two-way transitive trust between a forest root domain and a new tree root domain. They are created by design when you set up a new tree root domain within a forest. |
| `Forest`       | a transitive trust between two forest root domains.                                                                                                                    |



### Questions
- What role maintains time for a domain?
	- PDC Emulator
- What domain functional level introduced Managed Service Accounts?
	- Windows Server 2008 R2
- What type of trust is a link between two child domains in a forest?
	- Cross-Link
- What role ensures that objects in a domain are not assigned the same SID? (full name)
	- Relative ID Master