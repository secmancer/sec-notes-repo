### **What is Alert Triaging?**
- **Definition**: The process performed by SOC analysts to evaluate, categorize, and prioritize security alerts based on their severity, urgency, and potential impact.
- **Purpose**: Ensures efficient allocation of resources and effective responses to security incidents.
- **Key Component**: **Escalation**:
    - Notifies supervisors or incident response teams about critical alerts.
    - Facilitates coordination and decision-making for mitigating threats.
    - Ensures prompt attention to high-severity incidents.



### **Ideal Triaging Process**
- #### **1. Initial Alert Review**
	- Review alert metadata (e.g., timestamp, source IP, destination IP).
	- Analyze associated logs (network traffic, system, application) for context.
- #### **2. Alert Classification**
	- Categorize alerts using a predefined classification system:
	    - Severity
	    - Impact
	    - Urgency
- #### **3. Alert Correlation**
	- Cross-reference with related alerts, incidents, or indicators of compromise (IOCs).
	- Query SIEM/log management systems and check threat intelligence feeds.
- #### **4. Enrichment of Alert Data**
	- Collect additional data for context:
	    - Packet captures, memory dumps, or suspicious file samples.
	    - Analyze URLs, IP addresses, or files via external threat intelligence or sandboxes.
	    - Recon systems for anomalies (network processes, file modifications).
- #### **5. Risk Assessment**
	- Assess potential risks to critical assets, data, or infrastructure:
	    - Evaluate system/data value, compliance needs, and regulatory impact.
	    - Determine the likelihood of success or lateral movement.
- #### **6. Contextual Analysis**
	- Review affected assets and criticality.
	- Examine security control effectiveness (e.g., firewalls, endpoint protection).
	- Evaluate compliance and regulatory implications.
- #### **7. Incident Response Planning**
	- If significant, initiate an incident response plan:
	    - Document alert details, affected systems, and observed behaviors.
	    - Assign roles within the incident response team.
	    - Coordinate with relevant teams (e.g., IT, vendors).
- #### **8. Consultation with IT Operations**
	- Collaborate to fill gaps in context or data:
	    - Gather insights on affected systems, configurations, and activities.
	    - Confirm known issues, misconfigurations, or benign triggers.
	    - Document findings.
- #### **9. Response Execution**
	- Take actions based on triaging insights:
	    - Resolve benign alerts without escalation.
	    - Escalate alerts indicating security concerns.
 - #### **10. Escalation**
	- **Triggers for Escalation**:
	    - Critical systems/assets compromised.
	    - Active attacks or widespread impact.
	    - Insider threats or advanced techniques.
	- Notify appropriate teams or management with a detailed alert summary:
	    - Severity
	    - Impact
	    - Enrichment data
	    - Risk assessment
	- Document all escalation communication.
	- Escalate to external entities (e.g., law enforcement, CERTs) if required.
- #### **11. Continuous Monitoring**
	- Monitor incident response progress.
	- Provide updates and collaborate with escalated teams.
- #### **12. De-escalation**
	- De-escalate when the incident is contained and risk mitigated.
	- Notify stakeholders with a summary of actions and lessons learned.



### **Best Practices for Alert Triaging**
1. **Periodic Review**:
    - Update processes to address new threats and organizational needs.
2. **Documentation**:
    - Maintain thorough records of triaging, escalation, and de-escalation processes.
3. **Training**:
    - Equip SOC analysts with skills to identify patterns, enrich data, and respond effectively.
4. **Automation**:
    - Leverage tools to automate low-priority alerts, enabling focus on critical incidents.
5. **Collaboration**:
    - Foster seamless communication between SOC, IT, and external stakeholders.