## Overview
- While the incident handling team may not directly handle protection, understanding protection-related activities is crucial. 
- These measures aid in anticipating threats, understanding incidents, and locating artifacts or evidence during investigations.



## Highly Recommended Protective Measures
- ### DMARC 
	- (Domain-based Message Authentication, Reporting, and Conformance)
	- **Purpose**: Protects against phishing by rejecting spoofed emails pretending to originate from your organization.
	- **Benefits**:
	    - Prevents phishing emails from reaching recipients.
	    - Inexpensive and effective.
	- **Cautions**:
	    - Thorough testing is mandatory to avoid blocking legitimate emails.
	    - Advanced implementations can detect phishing emails from domains not owned by the organization using email filtering rules.
- ### Endpoint Hardening & Endpoint Detection and Response (EDR)
	- **Why?** Endpoint devices are common entry points for attacks.
	- **Standards**: Use CIS and Microsoft baselines for hardening.
	- **Best Practices**:
	    - Disable LLMNR/NetBIOS.
	    - Implement LAPS and remove admin privileges from regular users.
	    - Configure PowerShell in "ConstrainedLanguage" mode.
	    - Enable Attack Surface Reduction (ASR) rules.
	    - Implement whitelisting (focus on blocking user-writable folders like Downloads, Desktop, AppData).
	    - Utilize host-based firewalls to block workstation-to-workstation communication.
	    - Deploy an EDR product integrated with AMSI for script visibility.
	- **Key Advice**: "Don’t let perfect be the enemy of good."
- ### Network Protection
	- **Network Segmentation**: Isolate business-critical systems, allowing only required connections.
	- **IDS/IPS Systems**:
	    - Enhance detection by performing SSL/TLS interception.
	    - Avoid relying solely on IP reputation for detecting malicious traffic.
	- **Device Control**: Allow only approved devices on the network using solutions like 802.1x or Azure Conditional Access policies.
- ### Privilege Identity Management, MFA, and Password Security
	- **Password Hygiene**:
	    - Avoid weak but complex passwords (e.g., "Password1!").
	    - Encourage pass phrases (e.g., "i LIK3 my coffeE warm").
	- **MFA**: Require MFA for administrative access to all applications and devices.
	- **Identity Management**: Mitigate risks associated with stolen privileged user credentials.
- ### Vulnerability Scanning
	- Perform continuous scans to identify "high" and "critical" vulnerabilities.
	- **Action**: Prioritize remediation; segment systems if patches cannot be applied.
- ### User Awareness Training
	- Train users to recognize and report suspicious activity.
	- **Periodic Testing**: Conduct surprise tests (e.g., phishing emails, dropped USB sticks) to measure training effectiveness.
- ### Active Directory Security Assessment
	- **Goal**: Identify security misconfigurations and vulnerabilities from an attacker’s perspective.
	- **Benefits**:
	    - Reduce the chance of one-step escalations for attackers.
	    - Increase the likelihood of detecting malicious activities.
	- **Advice**: Perform assessments regularly, internally or via a third party.
- ### Purple Team Exercises
	- **Purpose**: Train and evaluate incident handlers in a real-world context.
	- **Methodology**:
	    - Red teams simulate attacks and share findings with blue teams.
	    - Blue teams test logging, monitoring, and incident response.
	- **Outcome**: Identify vulnerabilities and refine detection and response strategies.



## Questions
- What can we use to block phishing emails pretending to originate from our mail server?
	- DMARC
- True or False: "Summer2021!" is a complex password.
	- True