### Introduction
- When the investigation is complete and we have understood the type of incident and the impact on the business (based on all the leads gathered and the information assembled in the timeline), it is time to enter the containment stage to prevent the incident from causing more damage.



### Containment
- **Containment Actions**
    - **Short-term Containment**:
        - Aims to prevent the spread of the incident while leaving a minimal footprint on systems.
        - Actions include isolating systems (e.g., placing them in separate VLANs, disconnecting network cables, or altering attacker's C2 DNS).
        - Provides time for developing a more concrete remediation strategy and allows for forensic imaging to preserve evidence.
        - If systems need to be shut down, proper communication and permissions must be ensured.
    - **Long-term Containment**:
        - Focuses on persistent actions to secure systems, such as changing passwords, applying firewall rules, adding host intrusion detection systems, and patching systems.
        - Communication with the business and relevant stakeholders is essential during these activities.
        - Patching a system does not mark the end of the incident—further eradication, recovery, and post-incident activities are necessary.



### Eradication
- **Eradication Stage**:
    - Focuses on eliminating the root cause and remnants of the incident to ensure the adversary is fully removed from the systems and network.
    - Activities include:
        - Removing detected malware from systems.
        - Rebuilding compromised systems.
        - Restoring systems from backups.
        - Applying additional patches that were not immediately necessary during containment.
        - Performing system hardening activities, often extending beyond impacted systems to the entire network.



### Recovery
- Focuses on bringing systems back to normal operation after an incident.
- Business verification ensures systems are working as expected and contain necessary data before being reintroduced to the production environment.
-  Restored systems are subject to heavy logging and monitoring to detect any re-attempts by the adversary to regain access.
-  **Suspicious events to monitor**:
	- Unusual logons (e.g., unfamiliar user or service accounts).
        - Unusual processes.
        - Changes to the registry in locations commonly altered by malware.
    - The recovery process may take months, divided into phases:
        - **Early phases** focus on improving security through quick wins and eliminating immediate vulnerabilities.
        - **Later phases** focus on implementing permanent, long-term security changes.



### Questions
- True or False: Patching a system is considered a short term containment.
	- False