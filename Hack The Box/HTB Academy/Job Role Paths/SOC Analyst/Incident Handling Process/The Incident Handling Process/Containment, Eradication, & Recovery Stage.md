## Containment
- ### Objective
	- Prevent the incident from spreading or causing further damage.
- ### Types of Containment
1. **Short-Term Containment**:
    - Minimal impact actions to stop damage while preserving evidence.
    - Examples:
        - Isolate the system by placing it in a separate VLAN.
        - Disconnect the network cable.
        - Redirect attacker’s Command & Control (C2) DNS names to a controlled or nonexistent address.
    - Purpose:
        - Buy time to develop a remediation strategy.
        - Preserve evidence by taking forensic images (if not already done).
    - **Important**: Notify the business and gain permissions for impactful actions (e.g., shutting down systems).
2. **Long-Term Containment**:
    - Persistent changes to improve security and stop the attack.
    - Examples:
        - Change user passwords.
        - Apply firewall rules.
        - Deploy a host intrusion detection system.
        - Apply patches or shut down systems.
    - **Important**: Maintain communication with stakeholders and update them regularly.



## Eradication
- ### Objective
	- Remove the root cause and all remnants of the incident to ensure the adversary is fully removed from the environment.
- ### Activities
	- Remove malware from systems.
	- Rebuild affected systems or restore from backups.
	- Apply additional patches and system-hardening measures.
	- Extend containment efforts to strengthen the environment.
- ### Scope
	- Focus on both impacted systems and the broader network to prevent recurrence.



## Recovery
- ### Objective
- Restore systems to normal business operations and ensure they are functioning as expected.
- ### Steps
	1. **Verification**:
	    - Confirm systems are operational and contain all necessary data.
	    - Validate functionality before reintegrating systems into the production environment.
	2. **Monitoring**:
	    - Subject restored systems to heightened logging and monitoring to detect:
	        - Unusual logons (e.g., from accounts that haven’t logged in there before).
	        - Unusual processes or activity.
	        - Registry changes often associated with malware.
	3. **Gradual Approach**:
	    - Recovery may take months for large incidents, with phased objectives:
	        - **Early Phases**:
	            - Address immediate vulnerabilities with quick wins.
	            - Eliminate low-hanging fruits.
	        - **Later Phases**:
	            - Implement permanent, long-term security measures.



## Key Points Across All Stages
- **Coordination**: Containment actions must be executed simultaneously across all affected systems to avoid alerting the attacker.
- **Stakeholder Communication**: Keep relevant parties informed of actions and progress.
- **Monitoring**: Post-recovery systems are at increased risk of being targeted again; close observation is essential.



## Questions
- True or False: Patching a system is considered a short term containment.
	- False