### Introduction
- **Information Gathering Phase**
    - Begins after the pre-engagement phase and contract signing.
    - Essential for gathering information about the company, employees, infrastructure, and organization.
    - This phase is central and frequently revisited throughout penetration testing.
    - All exploit attempts are based on information gathered during this phase.
- **Categories of Information Gathering**
    - **Open-Source Intelligence (OSINT)**
    - **Infrastructure Enumeration**
    - **Service Enumeration**
    - **Host Enumeration**
    - All four categories must be performed in every penetration test to ensure comprehensive data collection.
- **Importance of Information**
    - Information is critical for identifying vulnerabilities and guiding successful penetration testing.
    - Information is widely available and shared, including through social media, job postings, hosts, servers, and employees.
    - Both humans and network components share information with specific purposes in mind, such as triggering processes or storing data.
![](https://academy.hackthebox.com/storage/modules/90/0-PT-Process-IG.png)



### Open-Source Intelligence
- **Open Source Intelligence (OSINT)**
    - OSINT involves finding publicly available information about a target company or individuals, often from open-source platforms.
    - It can reveal sensitive data such as passwords, hashes, keys, tokens, and other critical information.
- **Sources of OSINT**
    - Common sources include social media, development platforms (like GitHub), and public repositories.
    - Sensitive data is often unintentionally exposed due to misconfigured repositories or public sharing.
- **Security Implications**
    - OSINT can quickly uncover vulnerabilities that provide access to the network.
    - The discovery of sensitive data (e.g., passwords or SSH keys) must be handled carefully, with protocols for reporting and mitigating these findings outlined in the Incident Handling and Report section of the Rules of Engagement (RoE).
- **Next Steps**
    - If sensitive information is found, the client's administrator should review and address it before further testing proceeds.



### Private and Public SSH Keys
- **StackOverflow and Code Sharing**
    - Developers frequently share code snippets on platforms like StackOverflow to help others understand and resolve issues.
    - This shared information can expose security vulnerabilities if not carefully reviewed.
- **Identifying and Closing Security Gaps**
    - Our role is to identify these potential security holes and ensure they are addressed to prevent exploitation.
- **Learning OSINT Techniques**
    - The _OSINT: Corporate Recon_ module provides various techniques for identifying sensitive information shared online and how to mitigate associated risks.
![](https://academy.hackthebox.com/storage/modules/90/searchcode3.png)



### Infrastructure Enumeration
- **Infrastructure Enumeration**
    - The goal is to map the company's internet and intranet infrastructure using OSINT and initial active scans.
    - We identify servers, hosts, name servers, mail servers, web servers, and cloud instances, creating a list of IP addresses for comparison against the scope.
- **Security Measures Identification**
    - This phase also involves identifying the company's security measures, such as firewalls and web application firewalls.
    - Understanding these allows us to plan evasive testing and determine methods that will avoid triggering alarms.
- **Internal vs. External Enumeration**
    - Whether performing external or internal enumeration, the objective is to identify potential attack vectors.
    - Internal enumeration aids in targeting systems for attacks like `Password Spraying`, where a single password is tested across multiple user accounts to gain access.
- **Further Exploration**
    - Detailed techniques for these methods will be covered in the relevant modules.



### Service Enumeration
- **Service Enumeration**
    - This phase focuses on identifying network services that allow interaction with the host or server, either from an external or internal perspective.
    - Key information to gather includes the service's version, the data it provides, and its purpose.
- **Version History and Vulnerabilities**
    - Services often have version histories, which help determine if the installed version is outdated.
    - Outdated versions are common targets for security vulnerabilities, as administrators may avoid updating working applications to prevent infrastructure disruptions. This can lead to unpatched vulnerabilities being left open.



### Host Enumeration
- **Host Enumeration**
    - After creating a detailed list of the client's infrastructure, we examine each host listed in the scope.
    - We identify the operating system, services, versions, and configurations using both active scans and OSINT methods.
- **Security Risks of Legacy Systems**
    - Many services, such as FTP servers, may still be in use despite being outdated or unsupported, presenting security vulnerabilities.
    - Older versions of operating systems and services often remain unpatched, endangering the client's infrastructure.
- **External vs. Internal Enumeration**
    - Both external and internal perspectives are important for host enumeration.
    - Internal enumeration often reveals services that are not exposed to the internet but may be misconfigured or insecure due to assumptions of safety.
- **Post-Exploitation and Internal Host Enumeration**
    - During internal enumeration, typically after successful exploitation, sensitive files, local services, scripts, and applications are explored.
    - This is a key part of the post-exploitation phase, where privilege escalation is attempted.



### Pillaging
- **Pillaging**
    - Performed during the **Post-Exploitation** stage to collect sensitive information from an already exploited host, such as employee names, customer data, and more.
    - The gathered information depends on the host's role, its position in the network, and the security measures in place.
- **Impact of Pillaging**
    - Information obtained during pillaging can help assess the impact of an attack and guide further actions, such as **privilege escalation** or **lateral movement** within the network.
- **HTB Academy and Pillaging**
    - **Pillaging** is not explicitly covered in a separate module in HTB Academy.
    - It is treated as part of the **information gathering** and **privilege escalation** phases and is integrated within those stages.
- Here is a small list of modules where `Pillaging` is covered, but this topic will be covered in many other modules as well:

|  |  |  |
| --- | --- | --- |
| `Network Enumeration with Nmap` | `Getting Started` | `Password Attacks` |
| `Active Directory Enumeration & Attacks` | `Linux Privilege Escalation` | `Windows Privilege Escalation` |
| `Attacking Common Services` | `Attacking Common Applications` | `Attacking Enterprise Networks` |

- We will interact with more than `150 targets` during the Penetration Tester Job Role Path and perform nine simulated mini penetration tests, giving us plenty of opportunities to work on and practice this topic
- Furthermore, operating system-specific modules should be considered from the pillaging point of view because much of what is shown in those modules can be used for information retrieval or privilege escalation on the target systems.