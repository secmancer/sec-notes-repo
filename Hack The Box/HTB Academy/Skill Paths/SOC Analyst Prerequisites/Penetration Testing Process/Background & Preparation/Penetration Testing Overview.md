### Introduction
- **IT as a Critical Component**: IT is vital for nearly all companies, with data growing in both importance and sensitivity. 
- The increasing frequency of cyber-attacks, including ransomware, targeting critical company data highlights the importance of securing IT infrastructure. 
- When breaches occur, sensitive information can be exploited, sold, or leaked, potentially causing significant harm to an organization’s reputation and operations. 
- The rising complexity of these attacks makes them harder to prevent and mitigate.
- **Penetration Testing (Pentest)**: A pentest is a structured, authorized attempt to exploit vulnerabilities in an IT system, simulating real-world attacks to identify weaknesses.
- By using real attack methods, penetration testers evaluate the impact vulnerabilities can have on an organization's confidentiality, integrity, and availability. 
- This proactive approach allows organizations to detect flaws before malicious actors can exploit them.
- **Pentest Objective**: The goal of a pentest is to identify all vulnerabilities within the tested systems and enhance their security posture by addressing these weaknesses.
- **Red Team Assessment**: Unlike a pentest, a red team assessment is scenario-based, focusing on specific objectives like gaining access to high-value targets (e.g., CEO’s inbox or a critical server’s flag). 
- It often mimics more sophisticated, targeted attacks with a strategic goal in mind, rather than attempting to find every vulnerability.



### Risk Management
- **IT Security Risk Management**: Focuses on identifying, evaluating, and mitigating risks to protect the confidentiality, integrity, and availability of data. Security controls like access control and encryption are implemented to reduce risks to acceptable levels.
- **Residual and Inherent Risks**: Not all risks can be eliminated, and inherent risks remain despite controls. Companies can accept, transfer, avoid, or mitigate risks through measures such as insurance, contracts, preventive actions, and financial instruments.
- **Penetration Testing (Pentest)**: Provides a snapshot of security vulnerabilities, including detailed documentation and remediation recommendations. However, fixing vulnerabilities is the client’s responsibility, not the tester’s. Pentests do not monitor systems continuously but highlight issues at a specific point in time.



### Vulnerability Assessments
- **Vulnerability Analysis vs. Penetration Testing**: Vulnerability analysis uses automated tools (e.g., Nessus, Qualys, OpenVAS) to detect known issues, while penetration tests combine automated and manual methods for deeper validation tailored to specific systems.
- **Authorization and Scope**: Pentests require explicit written authorization to avoid legal issues, and clients must confirm asset ownership. Providers like AWS may not require prior approval for specific tests, but this varies, so scoping and approvals must be clarified beforehand.
- **Pentest Preparation**: Effective pentesting requires thorough planning, a flexible process model, and clear communication—especially with clients unfamiliar with the process—to ensure accurate scoping and expectations.
- **Employee Awareness**: Employees may not be informed about upcoming pentests unless management decides otherwise, balancing operational transparency with security testing effectiveness.
- **Data Protection**: Testers may access sensitive data (e.g., names, credit card details), so compliance with laws like the Data Protection Act is critical. Recommendations include updating passwords and encrypting databases to safeguard exposed information.



### Testing Methods
- An essential part of the process is the starting point from which we should perform our pentest.
- Each pentest can be performed from two different perspectives:
	- `External` or `Internal`
- #### External Penetration Test
	- Many pentests are performed from an external perspective or as an anonymous user on the Internet. 
	- Most customers want to ensure that they are as protected as possible against attacks on their external network perimeter.
	- We can perform testing from our own host (hopefully using a VPN connection to avoid our ISP blocking us) or from a VPS. Some clients will not care about stealth, while others will request that we proceed as quietly as possible and approach the target systems to avoid being banned by the firewalls and IDS/IPS systems and avoid triggering an alarm. 
	- They may ask for a stealthy or "hybrid" approach where we gradually become "noisier" to test their detection capabilities. 
	- Ultimately our goal here is to access external-facing hosts, obtain sensitive data, or gain access to the internal network.
- #### Internal Penetration Test
	- In contrast to an external pentest, an internal pentest is when we perform testing from within the corporate network. 
	- This stage may be executed after successfully penetrating the corporate network via the external pentest or starting from an assumed breach scenario. 
	- Internal pentests may also access isolated systems with no internet access whatsoever, which usually requires our physical presence at the client's facility.



### Types of Penetration Testing
- No matter how we begin the pentest, the type of pentest plays an important role. 
- This type determines how much information is made available to us.

| **Type**         | **Information Provided**                                                                                                                                                                                                                                              |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Blackbox`       | `Minimal`. Only the essential information, such as IP addresses and domains, is provided.                                                                                                                                                                             |
| `Greybox`        | `Extended`. In this case, we are provided with additional information, such as specific URLs, hostnames, subnets, and similar.                                                                                                                                        |
| `Whitebox`       | `Maximum`. Here everything is disclosed to us. This gives us an internal view of the entire structure, which allows us to prepare an attack using internal information. We may be given detailed configurations, admin credentials, web application source code, etc. |
| `Red-Teaming`    | May include physical testing and social engineering, among other things. Can be combined with any of the above types.                                                                                                                                                 |
| `Purple-Teaming` | It can be combined with any of the above types. However, it focuses on working closely with the defenders.                                                                                                                                                            |

- The less information we are provided with, the longer and more complex the approach will take. 
- For example, for a blackbox penetration test, we must first get an overview of which servers, hosts, and services are present in the infrastructure, especially if entire networks are tested. 
- This type of recon can take a considerable amount of time, especially if the client has requested a more stealthy approach to testing.



### Types of Testing Environments
- Apart from the test method and the type of test, another consideration is what is to be tested.

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| Network | Web App | Mobile | API | Thick Clients |
| IoT | Cloud | Source Code | Physical Security | Employees |
| Hosts | Server | Security Policies | Firewalls | IDS/IPS |

- It is important to note that these categories can often be mixed. 
- All listed test components may be included depending on the type of test to be performed. 
- Now we'll shift gears and cover the Penetration Process in-depth to see how each phase is broken down and depends on the previous one.