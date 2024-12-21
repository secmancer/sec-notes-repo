### Overview
- **Cyber Kill Chain vs. Incident Handling Process**:
    - Understanding the cyber kill chain helps predict attacker steps and determine appropriate defensive measures.
    - The **incident handling process** is a separate but related concept for responding to security events, with stages that don't directly map to the cyber kill chain.
- **Incident Handling Process**:
    - As defined by NIST, it consists of four stages: **Preparation**, **Detection & Analysis**, **Containment, Eradication, and Recovery**, and **Post-Incident Activity**.
    - **Preparation and Detection & Analysis**: These stages involve ongoing efforts to improve readiness and identify malicious events. Most time is spent here before moving to response.
    - The process is **cyclic**; as new evidence emerges, responses may change. All steps must be completed before progressing to the next.
- **Investigation and Recovery**:
    - **Investigation**:
        - Identify the first compromised system ("patient zero").
        - Determine tools and malware used by the attacker.
        - Document impacted systems and actions taken by the adversary.
    - **Recovery**:
        - Develop and implement a recovery plan.
        - Resume normal business operations if disruptions occurred due to the incident.
- **Post-Incident**:
    - Once the incident is resolved, a report detailing the cause, impact, and cost is created.
    - **Lessons learned** activities follow to improve future prevention strategies.
![Handling Process](https://academy.hackthebox.com/storage/modules/148/handling_process.png)



### Questions
- True or False: Incident handling contains two main activities. These are investigating and reporting.
	- False
