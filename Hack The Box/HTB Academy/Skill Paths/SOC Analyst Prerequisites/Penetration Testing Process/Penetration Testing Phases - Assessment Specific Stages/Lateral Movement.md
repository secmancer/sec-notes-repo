### Introduction
- **Lateral Movement**
    - Occurs after successful **Exploitation** and **Post-Exploitation**, with the goal of testing what an attacker could do across the entire network.
    - It simulates the spread of attacks like **ransomware**, which can infect multiple systems and disrupt business operations.
- **Importance of IT Security**
    - Demonstrates the financial and legal risks that companies face when security is neglected.
    - CEOs are often held liable for failing to protect customer data adequately.
- **Testing Steps in Lateral Movement**
    - Includes phases like **Pivoting**, **Evasive Testing**, **Information Gathering**, **Vulnerability Assessment**, **Exploitation**, and **Post-Exploitation**.
    - Focuses on finding internal vulnerabilities and exploring network movement options when privilege escalation on the target system is not possible.
![](https://academy.hackthebox.com/storage/modules/90/0-PT-Process-LA.png)



### Pivoting
- **Pivoting/Tunneling**
    - When the attack system lacks the tools to enumerate the internal network, the exploited host is used as a proxy to route network requests to the internal network.
    - This allows access to non-routable, publicly unreachable networks, enabling vulnerability scans and deeper penetration.
- **Example**
    - A compromised host can be used to access an otherwise inaccessible printer, illustrating the concept of pivoting where an intermediary system facilitates access to secure systems.



### Evasive Testing
- Also, at this stage, we should consider whether evasive testing is part of the assessment scope. 
- There are different procedures for each tactic, which support us in disguising these requests to not trigger an internal alarm among the administrators and the blue team.
- There are many ways to protect against lateral movement, including network (micro) `segmentation`, `threat monitoring`, `IPS`/`IDS`, `EDR`, etc. 
- To bypass these efficiently, we need to understand how they work and what they respond to. 
- Then we can adapt and apply methods and strategies that help avoid detection.



### Information Gathering
- Before we target the internal network, we must first get an `overview` of which systems and how many can be reached from our system. 
- This information may already be available to us from the last post-exploitation stage, where we took a closer look at the settings and configurations of the system.
- We return to the Information Gathering stage, but this time, we do it from inside the network with a different view of it. 
- Once we have discovered all hosts and servers, we can enumerate them individually.



### Vulnerability Assessment
- Vulnerability assessment from the inside of the network differs from the previous procedures. 
- This is because far more errors occur inside a network than on hosts and servers exposed to the Internet. 
- Here, the `groups` to which one has been assigned and the `rights` to different system components play an essential role.
- In addition, it is common for users to share information and documents and work on them together.
- This type of information is of particular interest to us when planning our attacks. 
- For example, if we compromise a user account assigned to a developer group, we may gain access to most of the resources used by company developers. 
- This will likely provide us with crucial internal information about the systems and could help us to identify flaws or further our access.



### (Privilege) Exploitation
- **Lateral Movement**
    - After identifying prioritized paths, attackers can access other systems by cracking passwords, hashes, or using existing credentials.
    - Tools like [Responder](https://github.com/lgandx/Responder) can intercept NTLMv2 hashes, enabling the **pass-the-hash** technique to authenticate as an administrator across multiple hosts.
    - The goal of this stage is to move through the internal network using available data and information in various ways.



### Post-Exploitation
- Once we have reached one or more hosts or servers, we go through the steps of the post-exploitation stage again for each system. 
- Here we again collect system information, data from created users, and business information that can be presented as evidence. 
- However, we must again consider how this different information must be handled and the rules defined around sensitive data in the contract.
- Finally, we are ready to move on to the `Proof-of-Concept` phase to show off our hard work and help our client, and those responsible for remediation efficiently reproduce our results.