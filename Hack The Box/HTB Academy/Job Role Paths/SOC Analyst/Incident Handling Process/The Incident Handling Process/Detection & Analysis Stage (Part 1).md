### Introduction
- **Detection & Analysis Phase**:
    - Involves detecting incidents through sensors, logs, trained personnel, and context-based threat intelligence.
    - Key factors include segmentation of architecture, network visibility, and information sharing.
- **Threat Detection Sources**:
    - Employee observations of abnormal behavior.
    - Alerts from tools like EDR, IDS, Firewall, SIEM.
    - Threat hunting activities.
    - Third-party notifications about potential compromises.
- **Levels of Detection**:
    - **Network Perimeter**: Firewalls, intrusion detection/prevention systems, DMZ.
    - **Internal Network**: Local firewalls, host intrusion detection/prevention systems.
    - **Endpoint Level**: Antivirus, endpoint detection & response systems.
    - **Application Level**: Application logs, service logs.



### Initial Investigation
- **Initial Investigation**:
    - Collect critical information before assembling the incident response team, such as the date/time, who detected and reported the incident, and how it was detected.
    - Document details like impacted systems, actions taken, physical location, operating systems, IP addresses, and hostnames.
    - For malware-related incidents, gather data on IP addresses, type of malware, and forensic information like file hashes.
- **Decision Making**:
    - Use gathered information to guide actions based on the severity and context of the incident (e.g., CEO's laptop vs. intern's).
- **Building an Incident Timeline**:
    - Create a time-sorted timeline of events to organize findings and understand the sequence of the incident.
    - The timeline should include date, time, hostname, event description, and data source.
- **Example of Timeline Entry**:
    - `09/09/2021 13:31 CET | SQLServer01 | Hacker tool 'Mimikatz' detected | Antivirus Software`
- **Focus on Attacker Behavior**:
    - Record key attacker actions, such as system access, network connections, and file downloads, with corresponding system associations and data sources.



### Incident Severity & Extent Questions
- **Questions to Assess Incident Severity and Extent**:
    - What is the impact of the exploitation?
    - What are the exploitation requirements?
    - Can business-critical systems be affected?
    - Are there any suggested remediation steps?
    - How many systems have been impacted?
    - Is the exploit being used in the wild?
    - Does the exploit have worm-like capabilities?
- **Indicators of Sophistication**:
    - The last two questions can reveal the adversary's level of sophistication, particularly if the exploit is widely used or has worm-like capabilities.
- **Handling High-Impact Incidents**:
    - High-impact incidents require prompt handling, and incidents affecting many systems should be escalated for more resources and attention.



### Incident Confidentiality & Communication
- Incidents are very confidential topics and as such, all of the information gathered should be kept on a need-to-know basis, unless applicable laws or a management decision instruct us otherwise.
- There are multiple reasons for this. 
- The adversary may be, for example, an employee of the company, or if a breach has occurred, the communication to internal and external parties should be handled by the appointed person in accordance with the legal department.
- When an investigation is launched, we will set some expectations and goals. 
- These often include the type of incident that occurred, the sources of evidence that we have available, and a rough estimation of how much time the team needs for the investigation. 
- Also, based on the incident, we will set expectations on whether we will be able to uncover the adversary or not.
- Of course, a lot of the above may change as the investigation evolves and new leads are discovered. It is important to keep everyone involved and the management informed about any advancements and expectations.



### Questions
- True or False: Can a third party vendor be a source of detecting a compromise?
	- True