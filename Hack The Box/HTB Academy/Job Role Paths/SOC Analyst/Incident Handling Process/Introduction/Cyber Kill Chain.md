## Overview
- The cyber kill chain outlines the stages of an attack lifecycle. 
- Understanding this lifecycle is essential for determining an attacker's position in a network and their potential access during an investigation.



### The Seven Stages of the Cyber Kill Chain
- #### 1. Reconnaissance (Recon)
	- **Objective**: Identify and gather information about the target.
	- **Tactics**:
	  - Passive gathering: Utilizing web sources like LinkedIn, Instagram, and target organization websites.
	  - Active scanning: Probing external web applications and IP addresses.
	- **Sources**: Job ads, partner information, and documentation can reveal tools, technologies, and systems in use.
- #### 2. Weaponization
	- **Objective**: Develop and embed malware into an exploit or payload.
	- **Characteristics**:
	  - Lightweight and undetectable by security tools.
	  - Provides remote access and persistence.
	  - Capable of deploying additional tools on demand.
- #### 3. Delivery
- **Objective**: Deliver the exploit or payload to the victim(s).
	- **Methods**:
	  - Phishing emails with malicious attachments or links.
	  - Fake websites mimicking legitimate ones for credential theft or payload hosting.
	  - Social engineering calls to persuade victims to execute the payload.
	  - Physical delivery: USB devices and other storage tools left strategically.
- #### 4. Exploitation
	- **Objective**: Trigger the exploit or payload to gain access or control.
	- **Action**: Execute code on the target system.
- #### 5. Installation
	- **Objective**: Deploy malware onto the compromised machine.
	- **Techniques**:
	  - **Droppers**: Install and execute malware.
	  - **Backdoors**: Maintain ongoing access to the system.
	  - **Rootkits**: Hide malware to evade detection.
- #### 6. Command and Control (C2)
	- **Objective**: Establish remote access to the compromised machine.
	- **Tactics**:
	  - Modular stagers load additional scripts dynamically.
	  - Advanced groups ensure multiple malware variants coexist to retain access if one is detected.
- #### 7. Actions on Objectives
	- **Objective**: Achieve the attack's goal.
	- **Examples**:
	  - Data exfiltration.
	  - Gaining high-level network access to deploy ransomware.
	  - Ransomware: Encrypts data, demanding payment for decryption (not recommended to pay).



### Key Considerations
- The kill chain is not strictly linear. Stages may repeat, such as returning to **Reconnaissance** after **Installation** to identify new targets and vulnerabilities.
- Early detection and interruption in the chain are critical to halting an attack's progression.



### Goal of Incident Response
- Prevent attackers from advancing through the kill chain, ideally stopping them in the early stages.



### Questions
- In which stage of the cyber kill chain is malware developed?
	- weaponize