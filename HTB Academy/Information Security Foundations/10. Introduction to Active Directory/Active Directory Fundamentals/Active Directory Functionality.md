### Active Directory (AD) FSMO Roles

1. **Schema Master**
   - **Description**: Manages the read/write copy of the AD schema, defining all attributes that can apply to AD objects.

2. **Domain Naming Master**
   - **Description**: Manages domain names and ensures unique domain creation within the forest.

3. **Relative ID (RID) Master**
   - **Description**: Allocates blocks of RIDs to domain controllers to ensure unique SIDs for objects within the domain.

4. **PDC Emulator**
   - **Description**: Acts as the authoritative domain controller for password changes, GPO management, and time synchronization within the domain.

5. **Infrastructure Master**
   - **Description**: Translates GUIDs, SIDs, and DNs between domains, especially important in multi-domain forests for correct ACL resolution.

- **Importance**: If FSMO roles malfunction, authentication and authorization issues arise within the domain.

---

### Domain and Forest Functional Levels in AD

#### Domain Functional Levels

| Functional Level | Features | Supported Domain Controller OS |
| ---------------- | -------- | ------------------------------- |
| **Windows 2000 native** | Universal groups, SID history, group nesting/conversion | Windows 2000, 2003, 2008, 2008 R2 |
| **Windows Server 2003** | lastLogonTimestamp, Netdom tool, constrained delegation, selective authentication | Windows 2003, 2008, 2008 R2, 2012, 2012 R2 |
| **Windows Server 2008** | DFS replication, AES for Kerberos, Fine-grained password policies | Windows 2008, 2008 R2, 2012, 2012 R2 |
| **Windows Server 2008 R2** | Managed Service Accounts, Authentication mechanism assurance | Windows 2008 R2, 2012, 2012 R2 |
| **Windows Server 2012** | KDC support for claims and Kerberos armoring | Windows 2012, 2012 R2 |
| **Windows Server 2012 R2** | Protected Users group, Authentication Policies, Silos | Windows 2012 R2 |
| **Windows Server 2016** | Smart card required for interactive logon, Kerberos enhancements | Windows 2016, 2019 |

- **Note**: Windows Server 2008 functional level is the minimum requirement for adding Server 2019 Domain Controllers.

#### Forest Functional Levels

| Version | Capabilities |
| ------- | ------------ |
| **Windows Server 2003** | Introduced forest trust, domain renaming, Read-Only Domain Controllers (RODC) |
| **Windows Server 2008** | All new domains default to Server 2008 domain functional level |
| **Windows Server 2008 R2** | Introduced Active Directory Recycle Bin |
| **Windows Server 2012** | Defaulted new domains to Server 2012 functional level |
| **Windows Server 2016** | Introduced Privileged Access Management (PAM) using Microsoft Identity Manager (MIM) |

---

### Trusts in Active Directory

Trusts allow users in one domain to access resources in another domain or forest. Trusts link authentication systems across domains.

#### Trust Types
1. **Parent-Child**: Two-way transitive trust between domains within the same forest.
2. **Cross-Link**: Trust between child domains to speed up authentication.
3. **External**: Non-transitive trust between separate domains in different forests.
4. **Tree-Root**: Two-way transitive trust between a forest root domain and a new tree root domain.
5. **Forest**: Transitive trust between two forest root domains.

#### Trust Characteristics
- **Transitive Trusts**: Extends trust to objects trusted by the child domain.
- **Non-Transitive Trusts**: Trust limited to the child domain only.
- **One-Way Trusts**: Only users in the trusted domain can access the trusting domain’s resources.
- **Two-Way Trusts (Bidirectional)**: Both domains trust each other and users can access resources in both directions.

- **Security Concerns**: Improperly configured trusts can introduce attack vectors, especially in mergers/acquisitions, leading to potential attacks like Kerberoasting across domains.


## Questions
- What role maintains time for a domain?
	- PDC Emulator
- What domain functional level introduced Managed Service Accounts?
	- Windows Server 2008 R2
- What type of trust is a link between two child domains in a forest?
	- Cross-Link
- What role ensures that objects in a domain are not assigned the same SID? (full name)
	- Relative ID Master