## Why Investigate?
- Understanding how an incident occurred and its impact is critical to ensure attackers cannot replicate their actions.
- Without knowledge of the adversary's tools, methods, and affected systems, remediation is incomplete, leaving the organization vulnerable to repeated attacks.



## Investigation Process
- ### Initial Information
- The investigation begins with the limited data gathered during the initial phase, evolving through a 3-step cyclic process:
	1. **Creation and usage of Indicators of Compromise (IOC).**
	2. **Identification of new leads and impacted systems.**
	3. **Data collection and analysis from new leads and impacted systems.**
- ### 1. Creation & Usage of IOCs
	- **Definition**: IOCs are artifacts or evidence that indicate an incident occurred (e.g., IP addresses, file hash values, file names).
	- **Tools and Standards**:
	    - **OpenIOC**: A structured language for documenting IOCs.
	    - **Yara**: A standard for writing rules to identify malware patterns.
	    - **Free Tools**: E.g., Mandiant's IOC Editor.
	- **Obtaining IOCs**:
	    - From the investigation.
	    - From third parties if the adversary is known.
	- **Deployment**:
	    - Use IOC-obtaining/searching tools (native or third-party, possibly at scale).
	    - Use tools like WMI or PowerShell for IOC operations in Windows environments.
- **Caution**: Prevent caching of privileged user credentials on potentially compromised systems.
	- Example: Using **PsExec**:
	    - Credentials cached when used with explicit credentials.
	    - Credentials not cached when used without explicit credentials via the currently logged-on session.
- ### 2. Identification of New Leads & Impacted Systems
	- **Goal**: Analyze IOC hits to identify systems showing signs of compromise.
	- **Challenges**:
	    - IOCs may be too generic, resulting in false positives.
	    - Large numbers of hits may require prioritization.
	- **Focus**: Prioritize systems that are likely to provide new leads or critical forensic insights.
- ### 3. Data Collection & Analysis
	- **Collection**:
	    - Systems with IOCs are preserved for analysis.
	    - **Approaches**:
	        - **Live Response**: Collect data from a running system (preferred for artifact-rich data).
	        - **Post-shutdown Analysis**: Rare but sometimes necessary; risks losing volatile data like RAM contents.
	    - **Minimal Interaction**: Avoid altering evidence or artifacts during collection.
	- **Analysis**:
	    - Types of examination:
	        - Malware analysis.
	        - Disk forensics.
	        - Memory forensics (increasingly relevant for advanced attacks).
	    - Newly discovered leads are added to and aligned with the incident timeline.
	- **Chain of Custody**:
	    - Ensure all data collected is traceable and admissible in court if legal action is pursued.



## Key Points for Investigation
- **Iterative Process**: Continually revisit and refine findings.
- **Valid Leads**: Avoid narrow focus; investigate broadly for a comprehensive understanding.
- **Documentation**:
    - Maintain a detailed and up-to-date timeline.
    - Include date, time, hostname, event description, and data source for all events.



## Questions
- During an investigation, we discovered a malicious file with an MD5 hash value of 'b40f6b2c167239519fcfb2028ab2524a'. How do we usually call such a hash value in investigations? Answer format: Abbreviation
	- IOC