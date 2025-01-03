### **What is a SIEM Use Case?**
- **Definition**: A scenario designed to detect specific security events or patterns, enabling proactive identification and mitigation of potential security threats.
- **Purpose**: Helps organizations monitor and respond to both straightforward (e.g., failed logins) and complex scenarios (e.g., ransomware detection).



### **Example of a SIEM Use Case**
**Scenario**: A user experiences 10 consecutive failed login attempts.
- **Detection**:
    - The SIEM system correlates these attempts and triggers a "brute force" alert.
- **Response**:
    - The SOC team investigates whether the activity is legitimate or malicious.



### **SIEM Use Case Development Lifecycle**
1. **Requirements**:
    - Define the purpose (e.g., detect brute force attacks after 10 failed logins in 4 minutes).
    - Specify what triggers the alert.
2. **Data Points**:
    - Identify data sources (e.g., Windows/Linux logs, VPN activity).
    - Ensure logs capture key details (user, timestamp, source, destination).
3. **Log Validation**:
    - Verify that logs include essential fields and are complete across all relevant events.
4. **Design and Implementation**:
    - Define alert conditions, aggregations, and priority levels.
    - Example:
        - Condition: 10 failed logins in 4 minutes.
        - Aggregation: Group events to avoid duplicates.
        - Priority: Higher for privileged accounts.
5. **Documentation**:
    - Create SOPs for alert handling, including escalation and reporting protocols.
    - Include an escalation matrix.
6. **Onboarding**:
    - Test the alert in a controlled environment before production deployment.
    - Address gaps to reduce false positives.
7. **Periodic Update/Fine-Tuning**:
    - Collect feedback, refine correlation rules, and whitelist legitimate activity.



### **Building Effective SIEM Use Cases**
1. Understand organizational needs and risks.
2. Establish priority and impact.
3. Map alerts to frameworks like the MITRE ATT&CK or the cyber kill chain.
4. Define Time to Detection (TTD) and Time to Response (TTR).
5. Develop SOPs and Incident Response Plans (IRPs).
6. Set Service Level Agreements (SLAs) for handling alerts.
7. Implement auditing processes and maintain documentation for alert triggers.
8. Create a knowledge base for reference.



### **Example 1: Monitoring MSBuild Execution by Office Applications**
- **Risk**: Attackers may exploit MSBuild to execute malicious code.
- **Detection Use Case**:
    - Monitor when Office apps (e.g., Word, Excel) initiate MSBuild.
- **Priority and Mapping**:
    - **Severity**: High (LoLBins are significant threats).
    - **MITRE Mapping**:
        - Tactic: Defense Evasion (TA0005).
        - Technique: Trusted Developer Utilities Proxy Execution (T1127).
        - Sub-technique: MSBuild (T1127.001).
- **Response**:
    - Investigate command-line arguments and parent processes.
    - Analyze logs for suspicious user or system activity.



### **Example 2: Monitoring MSBuild Making Outbound Connections**
- **Risk**: Adversaries use MSBuild to establish malicious connections.
- **Detection Use Case**:
    - Identify MSBuild initiating outbound communication.
- **Priority and Mapping**:
    - **Severity**: Medium (higher chance of false positives due to legitimate activity).
    - **MITRE Mapping**:
        - Tactic: Execution (TA0002).
- **Response**:
    - Focus on the IP address, event actions, and threat intelligence.



### **Key Considerations for Use Case Fine-Tuning**
- **False Positives**:
    - Exclude legitimate activities (e.g., known parent processes or trusted IPs).
- **Response Optimization**:
    - Tailor SOPs to specific alerts, focusing on relevant event details.
- **Periodic Review**:
    - Continuously update rules based on feedback and evolving threat landscapes.