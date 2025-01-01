## Overview
- This phase focuses on detecting incidents through sensors, logs, trained personnel, and threat intelligence. 
- A clear understanding of the network architecture and segmentation is essential to locate and analyze threats effectively.



## Detection Sources
- Threats can be detected from:
	- An employee reporting abnormal behavior.
	- Alerts from tools (e.g., EDR, IDS, firewalls, SIEM).
	- Threat hunting activities.
	- Notifications from third parties about a compromise.



## Levels of Detection
1. **Network Perimeter**: Firewalls, internet-facing IDS/IPS, DMZ systems.
2. **Internal Network**: Local firewalls, host-based intrusion systems.
3. **Endpoint Level**: Antivirus, endpoint detection and response (EDR) systems.
4. **Application Level**: Application logs, service logs.



## Initial Investigation
- When an incident is detected, conduct a preliminary investigation before declaring an organization-wide response:
	- Gather details about:
	    - **Date/Time** of report, **detector**, and **how it was detected**.
	    - Nature of the incident (e.g., phishing, system unavailability).
	    - Impacted systems (if relevant).
	    - Actions taken and access details of affected systems.
	    - Physical location, OS, IP addresses, hostnames, owners, and system purposes.
	    - **For malware**: Document malicious IPs, detection times, malware type, impacted systems, and forensic information (e.g., file hashes).
	- Use this information to:
	    - Assess incident severity.
	    - Formulate targeted responses.
	    - Decide appropriate actions based on the context (e.g., CEO’s laptop vs. an intern’s laptop).



## Incident Timeline
- **Purpose**: Organize evidence and maintain an event overview.
- **Structure**:
    - Date
    - Time of the event
    - Hostname
    - Event description
    - Data source
- **Example Entry**:
    ```
    Date        Time        Hostname        Event Description                  Data Source
    09/09/2021  13:31 CET   SQLServer01     Hacker tool 'Mimikatz' detected    Antivirus Software
    ```
- **Focus**: Primarily on attacker behavior (e.g., network connections, file downloads).
- **Goal**: Determine related and unrelated activities for better context.



## Incident Severity & Extent Questions
- Key questions to assess severity and extent:
	1. What is the exploitation impact?
	2. What are the exploitation requirements?
	3. Are business-critical systems affected?
	4. What remediation steps are available?
	5. How many systems are impacted?
	6. Is the exploit active in the wild?
	7. Does the exploit have worm-like capabilities?
- **Implications**:
    - High-impact incidents require immediate action.
    - Incidents involving many systems may need escalation.



## Incident Confidentiality & Communication
- **Confidentiality**: Share information on a need-to-know basis, except where laws or management mandate otherwise.
    - **Reasons**:
        - The adversary may be an internal employee.
        - Controlled communication is necessary during a breach.
- **Communication Handling**:
    - Use designated points of contact.
    - Coordinate with legal and compliance teams.
- **Investigation Goals**:
    - Define incident type, evidence sources, and timeline.
    - Update stakeholders as new information emerges.



## Questions
- True or False: Can a third party vendor be a source of detecting a compromise?
	- True