### Information Gathering Phase
- **Initiation**:
  - Begins once the pre-engagement phase is complete and all contractual terms have been signed.

- **Purpose**:
  - To gather comprehensive information about the company, its employees, and infrastructure.
  - This phase is crucial for identifying potential vulnerabilities and attack vectors.

- **Importance**:
  - Information gathering is the most frequent and vital phase throughout the penetration testing process.
  - It serves as the foundation for further testing and assessment activities, making it essential for successful outcomes.

- **Activities Involved**:
  - **Research**: Collect data on the organization’s structure, technologies in use, and operational practices.
  - **Employee Information**: Identify key personnel, their roles, and potential targets for social engineering.
  - **Infrastructure Mapping**: Understand the organization's network architecture, systems, and applications.

- **Revisiting**:
  - Information gathering is not a one-time activity; it may need to be revisited throughout the penetration testing process as new information is obtained or as tests evolve.

- **Key Techniques**:
  - **Open Source Intelligence (OSINT)**: Utilize publicly available information from various sources (e.g., social media, websites, public records) to gather insights.
  - **Network Scanning**: Identify active devices and services within the organization’s network.
  - **Passive and Active Reconnaissance**: Collect data without alerting the target (passive) and engage directly with the systems (active) to gather further information.

![[0-PT-Process-IG_png 1.png]]
### Importance of Information Gathering

- **Foundation of Exploitation**:
  - Exploitation steps depend on the information gathered about targets.
  - Information gathering is considered the cornerstone of penetration testing.

- **Categories of Information Gathering**:
  1. **Open-Source Intelligence (OSINT)**
  2. **Infrastructure Enumeration**
  3. **Service Enumeration**
  4. **Host Enumeration**

- **Necessity**:
  - All four categories must be performed for each penetration test.
  - Information is crucial for identifying security vulnerabilities and achieving successful penetration testing.

- **Information Sources**:
  - Data can be found on social media, job postings, individual hosts and servers, or employee information.
  - Information sharing is prevalent and continuous in both human and network communications.

### Open-Source Intelligence (OSINT)

- **Definition**:
  - A process for finding publicly available information on a target company or individuals.
  - Helps identify events, dependencies, and connections related to the target.

- **Sources**:
  - Publicly available sources provide insights into sensitive information, including passwords, hashes, keys, and tokens.
  - Repositories on platforms like GitHub can expose sensitive data if not properly secured.

- **Risks**:
  - Finding sensitive information early on can lead to critical security gaps.
  - Client administrators must review any discovered vulnerabilities before proceeding.

### Infrastructure Enumeration

- **Objective**:
  - To map the company’s position on the internet and intranet using OSINT and active scans.
  - Identify and document the organization’s servers, hosts, and infrastructure.

- **Key Components**:
  - Identify name servers, mail servers, web servers, cloud instances, etc.
  - Determine the company’s security measures to disguise attacks (Evasive Testing).

- **Internal vs. External Enumeration**:
  - External enumeration provides an overview from outside the network.
  - Internal enumeration reveals targets for attacks like Password Spraying.

### Service Enumeration

- **Purpose**:
  - Identify services allowing interaction with hosts or servers.
  - Understand the versions of services and their functionalities.

- **Version Analysis**:
  - Check if services are up to date to uncover potential vulnerabilities.
  - Administrators may avoid updates to maintain functionality, leaving vulnerabilities exposed.

### Host Enumeration

- **Process**:
  - Examine each host listed in the scoping document to identify the operating system and running services.
  - Use OSINT and active scans for configuration insights.

- **Vulnerabilities**:
  - Older, unsupported services may still pose security risks.
  - Internal enumeration may reveal "secure" services that are misconfigured.

- **Internal Examination**:
  - Investigate hosts after exploitation to find sensitive files and data during the Post-Exploitation phase.

### Pillaging

- **Definition**:
  - Performed during the Post-Exploitation stage to collect sensitive information from exploited hosts.
  - Involves gathering data such as employee names and customer information.

- **Importance**:
  - Information obtained can demonstrate the impact of an attack and guide privilege escalation and lateral movement within the network.

- **Module Coverage**:
  - Pillaging is integrated within various modules rather than being a standalone category.
  - Relevant modules include:
    - Network Enumeration with Nmap
    - Active Directory Enumeration & Attacks
    - Linux and Windows Privilege Escalation
    - Attacking Common Services and Applications

Here are the detailed notes on the **Penetration Testing Process**, focusing on the importance of information gathering and its various categories:

### Importance of Information Gathering

- **Foundation of Exploitation**:
  - Exploitation steps depend on the information gathered about targets.
  - Information gathering is considered the cornerstone of penetration testing.

- **Categories of Information Gathering**:
  1. **Open-Source Intelligence (OSINT)**
  2. **Infrastructure Enumeration**
  3. **Service Enumeration**
  4. **Host Enumeration**

- **Necessity**:
  - All four categories must be performed for each penetration test.
  - Information is crucial for identifying security vulnerabilities and achieving successful penetration testing.

- **Information Sources**:
  - Data can be found on social media, job postings, individual hosts and servers, or employee information.
  - Information sharing is prevalent and continuous in both human and network communications.

### Open-Source Intelligence (OSINT)

- **Definition**:
  - A process for finding publicly available information on a target company or individuals.
  - Helps identify events, dependencies, and connections related to the target.

- **Sources**:
  - Publicly available sources provide insights into sensitive information, including passwords, hashes, keys, and tokens.
  - Repositories on platforms like GitHub can expose sensitive data if not properly secured.

- **Risks**:
  - Finding sensitive information early on can lead to critical security gaps.
  - Client administrators must review any discovered vulnerabilities before proceeding.

### Infrastructure Enumeration

- **Objective**:
  - To map the company’s position on the internet and intranet using OSINT and active scans.
  - Identify and document the organization’s servers, hosts, and infrastructure.

- **Key Components**:
  - Identify name servers, mail servers, web servers, cloud instances, etc.
  - Determine the company’s security measures to disguise attacks (Evasive Testing).

- **Internal vs. External Enumeration**:
  - External enumeration provides an overview from outside the network.
  - Internal enumeration reveals targets for attacks like Password Spraying.

### Service Enumeration

- **Purpose**:
  - Identify services allowing interaction with hosts or servers.
  - Understand the versions of services and their functionalities.

- **Version Analysis**:
  - Check if services are up to date to uncover potential vulnerabilities.
  - Administrators may avoid updates to maintain functionality, leaving vulnerabilities exposed.

### Host Enumeration

- **Process**:
  - Examine each host listed in the scoping document to identify the operating system and running services.
  - Use OSINT and active scans for configuration insights.

- **Vulnerabilities**:
  - Older, unsupported services may still pose security risks.
  - Internal enumeration may reveal "secure" services that are misconfigured.

- **Internal Examination**:
  - Investigate hosts after exploitation to find sensitive files and data during the Post-Exploitation phase.

### Pillaging

- **Definition**:
  - Performed during the Post-Exploitation stage to collect sensitive information from exploited hosts.
  - Involves gathering data such as employee names and customer information.

- **Importance**:
  - Information obtained can demonstrate the impact of an attack and guide privilege escalation and lateral movement within the network.

- **Module Coverage**:
  - Pillaging is integrated within various modules rather than being a standalone category.
  - Relevant modules include:
    - Network Enumeration with Nmap
    - Active Directory Enumeration & Attacks
    - Linux and Windows Privilege Escalation
    - Attacking Common Services and Applications

