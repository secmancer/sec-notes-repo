### Active Directory (AD) Notes

- **Overview**:  
  AD is a directory service for Windows network environments. It operates as a distributed, hierarchical structure that enables centralized management of organizational resources such as users, computers, groups, network devices, file shares, group policies, devices, and trusts.

- **Functions**:  
  AD provides two critical functions:
  1. **Authentication**: Verifying the identity of users and devices within the domain.
  2. **Authorization**: Managing permissions and determining what resources users and devices can access.

- **Scalability**:  
  AD is highly scalable, capable of supporting millions of objects in a single domain. As organizations grow, additional domains can be created, enhancing AD's flexibility.

- **Security Challenges**:  
  - **Backwards Compatibility**: AD is designed to be compatible with older systems, which can expose it to vulnerabilities. Many of its features are not "secure by default."
  - **Misconfigurations**: AD is prone to misconfiguration, which can lead to severe security risks. Attackers can leverage these weaknesses to move laterally and escalate privileges within the network.
  - **Read-Only Database**: AD is essentially a read-only database accessible to all users in the domain, regardless of privilege level. Even basic user accounts can enumerate objects, making it crucial to secure AD configurations properly.

- **Risk of Enumeration**:  
  Any user account in the domain, regardless of privilege level, can be used to enumerate objects within AD. This makes it easier for attackers to search for misconfigurations and vulnerabilities, underlining the importance of robust security practices.

- **Common Attack Vectors**:  
  Many attacks can be performed using just a standard domain user account, highlighting the need for:
  - **Defense-in-Depth**: Implementing multiple layers of security to protect AD.
  - **Security Hardening**: Regularly reviewing and improving AD settings to minimize vulnerabilities.
  - **Network Segmentation**: Separating sensitive network areas to limit potential damage in case of a breach.
  - **Least Privilege**: Ensuring that user accounts only have the permissions necessary for their roles.

- **Example Attack - noPac (December 2021)**:  
  The noPac attack exploited vulnerabilities in AD, allowing attackers to bypass security measures and gain unauthorized access. This underscores the need for ongoing security vigilance and patching.

By maintaining a secure AD environment and enforcing proper security protocols, organizations can reduce the risks of unauthorized access and attacks.

![[whyad5.png]]