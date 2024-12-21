### What Is A SOC?
- A **Security Operations Center (SOC)** is a facility housing experts who monitor and evaluate an organization's security status, identifying and addressing cybersecurity incidents.
- The SOC team includes **security analysts**, **engineers**, and **managers**, who collaborate with incident response teams to detect and resolve security concerns quickly.
- The SOC uses technology solutions like **SIEM**, **IDS/IPS**, and **EDR** tools, along with threat intelligence and proactive **threat hunting**, to detect potential threats.
- The SOC follows defined processes for **incident triage**, **containment**, **elimination**, and **recovery**, working with incident response teams to handle security incidents.
- In summary, the SOC provides **continuous monitoring and response** to minimize the impact of security breaches and reduce the likelihood of future attacks.



### How Does A SOC Work?
- The **SOC team** focuses on managing ongoing operational aspects of **enterprise information security**, rather than developing strategies or designing architecture.
- The team consists primarily of **security analysts** who work together to detect, assess, respond to, report on, and prevent **cybersecurity incidents**.
- Some SOCs have advanced capabilities, such as **forensic analysis** and **malware analysis**, to conduct in-depth investigations and identify the root causes of security incidents.
- The SOC collaborates closely with the **incident response team** to ensure proper handling of security incidents and maintain the organization's **security posture**.



### Roles Within A SOC
- A SOC team consists of diverse roles responsible for handling the continuous, operational aspect of enterprise information security. These roles may encompass:
	- `SOC Director`: Responsible for overall management and strategic planning of the SOC, including budgeting, staffing, and alignment with organizational security objectives.
	- `SOC Manager`: Oversees day-to-day operations, manages the team, coordinates incident response efforts, and ensures smooth collaboration with other departments.
	- `Tier 1 Analyst`: Monitors security alerts and events, triages potential incidents, and escalates them to higher tiers for further investigation.
	- `Tier 2 Analyst`: Performs in-depth analysis of escalated incidents, identifies patterns and trends, and develops mitigation strategies to address security threats.
	- `Tier 3 Analyst`: Provides advanced expertise in handling complex security incidents, conducts threat hunting activities, and collaborates with other teams to improve the organization's security posture.
	- `Detection Engineer`: A Detection Engineer is responsible for developing, implementing, and maintaining detection rules and signatures for security monitoring tools, such as SIEM, IDS/IPS, and EDR solutions. They work closely with security analysts to identify gaps in detection coverage and continuously improve the organization's ability to detect and respond to threats.
	- `Incident Responder`: Takes charge of active security incidents, carries out in-depth digital forensics and containment and remediation efforts, and collaborates with other teams to restore affected systems and prevent future occurrences.
	- `Threat Intelligence Analyst`: Gathers, analyzes, and disseminates threat intelligence data to help SOC team members better understand the threat landscape and proactively defend against emerging risks.
	- `Security Engineer`: Develops, deploys, and maintains security tools, technologies, and infrastructure, and provides technical expertise to the SOC team.
	- `Compliance and Governance Specialist`: Ensures that the organization's security practices and processes adhere to relevant industry standards, regulations, and best practices, and assists with audit and reporting requirements.
	- `Security Awareness and Training Coordinator`: Develops and implements security training and awareness programs to educate employees about cybersecurity best practices and promote a culture of security within the organization.
- It is important to note that the specific roles and responsibilities within each tier can vary depending on the organization's size, industry, and specific security requirements.
- In general, the tiered structure can be described as follows:
	- `Tier 1 Analysts`: Also known as "first responders," these analysts monitor security events and alerts, perform initial triage, and escalate potential incidents to higher tiers for further investigation. Their main goal is to quickly identify and prioritize security incidents.
	- `Tier 2 Analysts`: These analysts are more experienced and perform deeper analysis of escalated incidents. They identify patterns and trends, develop mitigation strategies, and sometimes assist in incident response efforts. They may also be responsible for tuning security monitoring tools to reduce false positives and improve detection capabilities.
	- `Tier 3 Analysts`: Often considered the most experienced and knowledgeable analysts on the team, Tier 3 analysts handle the most complex and high-profile security incidents. They may also engage in proactive threat hunting, develop advanced detection and prevention strategies, and collaborate with other teams to improve the organization's overall security posture.



### SOC Stages
- **SOC Evolution**: SOCs have transitioned from **SOC 1.0**, which focused on network security and lacked integration, to **SOC 2.0**, addressing advanced threats with better integration of threat intelligence, anomaly detection, and more sophisticated analysis.
- **SOC 1.0**: Early SOCs used isolated security layers, resulting in uncorrelated alerts and missed threats, relying heavily on network and perimeter security.
- **SOC 2.0**: Introduces threat intelligence, anomaly detection, and layer-7 analysis to detect multi-vector, persistent attacks, with a focus on **botnets** and evolving malware. It emphasizes situational awareness, vulnerability management, and post-event analysis.
- **Cognitive SOC**: The next-generation SOC seeks to address the gaps in SOC 2.0, such as the lack of business-process-specific threat detection and standardized incident response, by incorporating **learning systems** to improve security decision-making over time.



### Questions
- True or false? SOC 2.0 follows a proactive defense approach.
	- True