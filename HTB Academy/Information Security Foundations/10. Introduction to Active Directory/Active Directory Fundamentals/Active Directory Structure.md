### Active Directory (AD) Overview Notes

- **Definition**:  
  Active Directory (AD) is a directory service for Windows environments, providing **centralized management** of resources like users, computers, groups, file shares, and more. It handles **authentication** and **authorization** within Windows domain environments.

- **AD Components**:  
  - **Users**: Manageable user accounts.
  - **Computers**: Manageable computers within the network.
  - **Groups**: Collections of users or computers for policy management.
  - **Network Devices & File Shares**: Includes printers and shared network resources.
  - **Group Policies**: Defines rules for user and computer settings.
  - **Servers/Workstations**: Manageable devices for services and functions.
  - **Trusts**: Establish relationships between domains for resource sharing.

- **Directory Service (AD DS)**:  
  Active Directory Domain Services (AD DS) stores **directory data** (e.g., usernames, passwords) and manages user access rights. It was first introduced with **Windows Server 2000**.

- **Challenges & Security Concerns**:
  - **Backward Compatibility**: AD was designed to be backward-compatible, which leads to security vulnerabilities.
  - **Not Secure by Default**: Misconfigurations and improper management in large environments make AD prone to attacks.
  - **Attacks**: AD flaws can allow attackers to move **laterally** (across systems) and **vertically** (privilege escalation) to access sensitive resources (databases, file shares, etc.).

- **Enumeration and Information Disclosure**:  
  Basic AD users can enumerate most objects in the directory, including:
  - **Domain Computers**
  - **Domain Users**
  - **Domain Group Information**
  - **Organizational Units (OUs)**
  - **Group Policy Objects (GPOs)**
  - **Password Policies**
  - **Domain Trusts**
  - **Access Control Lists (ACLs)**

  This highlights the need for careful **AD security planning** and **administration**.

- **AD Hierarchy**:  
  AD uses a **hierarchical tree structure** consisting of:
  - **Forest**: The top-most container, acting as the **security boundary**. A forest can have one or more **domains**.
  - **Domains**: A structure containing objects like users, groups, and computers. Domains can have sub-domains.
  - **Organizational Units (OUs)**: Containers within a domain for organizing objects (users, groups, computers) and applying group policies.
  
- **Example AD Structure**:
    ```
    INLANEFREIGHT.LOCAL/
    ├── ADMIN.INLANEFREIGHT.LOCAL
    │   ├── GPOs
    │   └── OU
    │       └── EMPLOYEES
    │           ├── COMPUTERS
    │           │   └── FILE01
    │           ├── GROUPS
    │           │   └── HQ Staff
    │           └── USERS
    │               └── barbara.jones
    ├── CORP.INLANEFREIGHT.LOCAL
    └── DEV.INLANEFREIGHT.LOCAL
    ```

- **Domain Trusts**:
  - **Trust Relationships**: Allow domains and forests to share resources without duplicating users. Trusts simplify organizational structures that involve **acquisitions** or **multiple domains**.
  - **Security Concerns with Trusts**: Trusts introduce potential security risks if not properly managed, as users in one domain can potentially access resources in another domain or forest.

- **Cross-Forest Trusts Example**:
  - **Bidirectional Trusts**: Trusts allow users from one forest to access resources in another.
    - For example, if **INLANEFREIGHT.LOCAL** has a bidirectional trust with **FREIGHTLOGISTICS.LOCAL**, users in either domain can access each other’s resources.
    - **Child Domain Trusts**: However, trust between the parent domains doesn’t automatically extend to child domains. Separate **trust configurations** may be needed to allow cross-domain access between child domains.

### Key Takeaways:
- **AD's Complex Structure** requires careful management and security practices.
- **Misconfigurations** can lead to major security breaches.
- **Understanding AD’s Architecture** is essential before attempting to secure or attack it.
- **Domain Trusts** should be managed carefully to avoid potential security vulnerabilities.

![[ad_forests.png]]

![[ilflog2.png]]


## Questions
- What Active Directory structure can contain one or more domains?
	- forest
- True or False; It can be common to see multiple domains linked together by trust relationships?
	- true
- Active Directory provides authentication and <____> within a Windows domain environment.
	- authorization