### Introduction to Active Directory
- Active Directory (AD): directory service for Windows network environments.
	- Distributed, hierarchical structure for centralized management of an organization's resources.
		- Like: computers, groups, network devices, file shares, group policies, devices, and trusts.
	- Provides authentication/authorization functions for the Windows domain environment.
	- Recently has seen an influx of attacks towards it.
		- Reasons include its compatibility for older systems, its many features that are not secure by default, and its ability to be easily misconfigured.
	- Allows attackers to move laterally and vertically throughout the network if able to.
	- Sizeable read-only database accessible to all users within the domain, regardless of privilege level.
		- Basic AD user account with no added privileges can enumerate most objects within AD. 
		- Makes it extremely important to properly secure an AD implementation because ANY user account, regardless of their privilege level, can be used to enumerate the domain and hunt for misconfigurations and flaws thoroughly. 
		- Multiple attacks can be performed with only a standard domain user account, showing the importance of a defense-in-depth strategy and careful planning focusing on security and hardening AD, network segmentation, and least privilege. 
		- One example is the [noPac](https://www.secureworks.com/blog/nopac-a-tale-of-two-vulnerabilities-that-could-end-in-ransomware) attack that was first released in December of 2021.
- Active Directory makes information easy to find and use for administrators and users. AD is highly scalable, supports millions of objects per domain, and allows the creation of additional domains as an organization grows.
![image](https://academy.hackthebox.com/storage/modules/74/whyad5.png)
- Around **95% of Fortune 500** companies use Active Directory (AD), making it a prime target for attackers. A successful attack, such as phishing a standard domain user, can provide attackers with enough access to begin mapping and exploiting the domain.
- **Ransomware operators**, like those behind **Conti Ransomware**, are increasingly targeting AD in their attacks. They leverage critical AD flaws (e.g., **PrintNightmare** and **Zerologon**) to escalate privileges and move laterally within the network.
- Understanding AD's structure and function is essential for both attackers and defenders, as it helps identify vulnerabilities and prevent exploitation.
- Many open-source tools are available for penetration testers to enumerate and attack AD, but these tools are most effective when the operator understands how AD works.
- This module will cover the foundations of AD, including its structure, objects, user rights, privileges, management tools, and processes, and will provide hands-on examples of setting up a small AD environment for further learning.



## History of Active Directory
- **LDAP**, foundational to Active Directory (AD), was introduced in the **1970s** and was predated by the **X.500** directory system, released in 1993 as **Novell Directory Services**.
- **Active Directory** was first introduced in the mid-'90s and became part of **Windows Server 2000**. Microsoft’s earlier attempt at directory services was in **1990** with **Windows NT 3.0**, combining features from **LAN Manager** and **OS/2**.
- The first beta release of Active Directory was in **1997**.
- **Windows Server 2003** introduced extended AD functionality, including the **Forest** feature, which allows sysadmins to manage multiple domains under one umbrella.
- **Active Directory Federation Services (ADFS)**, introduced in **Server 2008**, enables **Single Sign-On (SSO)** and allows users to access applications across organizational boundaries with a single set of credentials.
- **Windows Server 2016** brought cloud migration capabilities and security enhancements, such as **Group Managed Service Accounts (gMSA)**, which secure automated tasks and services.
- **Azure AD Connect** was released in **2016** to support **Single Sign-On** for users migrating to **Office 365**.
- Active Directory continues to suffer from **misconfigurations** and **vulnerabilities**, requiring ongoing patching and security measures to address newly discovered flaws.
- A solid foundation in **AD fundamentals** is essential for security researchers, penetration testers, and administrators to identify vulnerabilities and provide effective remediation.
- Despite cloud transitions, **on-prem AD** remains prevalent, with **95% of Fortune 500 companies** relying on it, ensuring its continued relevance in penetration testing engagements.
- A deep understanding of AD will help both attackers and defenders in navigating complex AD environments and mitigating security risks effectively.