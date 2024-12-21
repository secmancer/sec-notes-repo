### Introduction
- **Purpose of Incident Investigation**:
    - Understanding how the incident happened is critical to preventing future occurrences and ensuring that attackers cannot regain access.
- **Importance of Knowledge**:
    - Without knowing the attack method, tools used, and impacted systems, remediation steps may not prevent the attacker from exploiting the same vulnerabilities again. Knowing these details allows for more effective, targeted remediation.



### The Investigation
- The investigation starts based on the initially gathered (and limited) information that contain what we know about the incident so far. 
- With this initial data, we will begin a 3-step cyclic process that will iterate over and over again as the investigation evolves. 
- This process includes:
	- Creation and usage of indicators of compromise (IOC)
	- Identification of new leads and impacted systems
	- Data collection and analysis from the new leads and impacted systems

![Investigation](https://academy.hackthebox.com/storage/modules/148/investigation_new.png)

- Let us now elaborate more on the process depicted above.



### Initial Investigation Data
- In order to reach a conclusion, an investigation should be based on valid leads that have been discovered not only during this initial phase but throughout the entire investigation process. 
- The incident handling team should bring up new leads constantly and not go solely after a specific finding, such as a known malicious tool. 
- Narrowing an investigation down to a specific activity often results in limited findings, premature conclusions, and an incomplete understanding of the overall impact.



### Creation & Usage Of IOCs
- **Indicators of Compromise (IOCs)**:
    - IOCs are signs that an incident has occurred and include artifacts like IP addresses, file hash values, and file names.
    - They are documented in structured formats such as OpenIOC or Yara, which facilitate sharing and analysis.
    - Free tools like Mandiant's IOC Editor help create or edit IOCs.
- **Using IOCs in Investigations**:
    - IOCs can be obtained from third parties or identified during an investigation.
    - IOC-obtaining tools (native or third-party) can be deployed to search for these indicators, often using WMI or PowerShell in Windows environments.
- **Security Considerations**:
    - It's crucial to avoid caching credentials during an investigation, especially when connecting to potentially compromised systems.
    - Tools like WinRM, which do not cache credentials, should be used instead of tools like PsExec, which cache credentials when used with explicit credentials.



### Identification Of New Leads & Impacted Systems
- After searching for IOCs, you expect to have some hits that reveal other systems with the same signs of compromise.
- These hits may not be directly associated with the incident we are investigating. 
- Our IOC could be, for example, too generic. 
- We need to identify and eliminate false positives. 
- We may also end up in a position where we come across a large number of hits. 
- In this case, we should prioritize the ones we will focus on, ideally those that can provide us with new leads after a potential forensic analysis.



### Data Collection & Analysis From The New Leads & Impacted Systems
- **Data Collection and Preservation**:
    - After identifying systems with IOCs, it's crucial to collect and preserve the state of these systems for further analysis.
    - **Live Response**: Most common method where data is collected while the system is running, ensuring minimal interaction to avoid altering evidence.
    - **Shutting Down Systems**: Sometimes done for deeper analysis, but it risks losing volatile data in RAM, which may contain important artifacts.
    - Minimizing interaction with systems during data collection is key to preserving evidence.
- **Data Analysis**:
    - Data analysis is often the most time-consuming part of an investigation, involving malware analysis and disk forensics.
    - **Memory Forensics** is gaining importance, especially for advanced attacks.
    - Any new findings should be added to the incident timeline.
- **Chain of Custody**:
    - It's important to track the chain of custody during the data collection process to ensure the data is legally admissible if needed in court.



### Questions
- During an investigation, we discovered a malicious file with an MD5 hash value of 'b40f6b2c167239519fcfb2028ab2524a'. How do we usually call such a hash value in investigations? Answer format: Abbreviation
	- IOC