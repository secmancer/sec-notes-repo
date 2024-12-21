### Introduction
- **Processes in Context**: Processes refer to sequences of events, whether in social sciences, business operations, or computer systems. In computing, processes are programs running within systems.
- **Deterministic vs. Stochastic Processes**:
    - **Deterministic**: Each state depends directly on previous states and events.
    - **Stochastic**: States progress based on probabilities rather than fixed causality.
- **Penetration Testing as a Process**: Defined as a series of steps and events aimed at achieving a specific objective, penetration testing relies on deterministic processes where each step builds on prior findings.
- **Flexibility in Processes**: Penetration testing processes are adaptable rather than rigid, allowing adjustments to suit unique client infrastructures, goals, and expectations.



### Penetration Testing Stages
- **Stages in Penetration Testing**: Penetration testing is best represented through interdependent stages rather than linear steps, allowing flexibility to adapt based on new findings.
- **Circular Processes**: Testing often follows a circular process, where disruptions in any stage can cause failures. Restarting the process with new information effectively creates a new approach rather than undoing previous steps.
- **Flexibility Over Fixed Steps**: Instead of rigid step-by-step guides, penetration testing relies on adaptable stages, enabling testers to modify approaches based on results.
- **Playbooks for Adaptation**: While testers may develop playbooks for common tasks, each environment is unique, requiring continuous adjustments throughout the process.
![](https://academy.hackthebox.com/storage/modules/90/0-PT-Process.png)
- **Study Plan and Process Overview**
    - Structured approach with iterative learning phases focused on TTPs.
    - Optional study plan covering modules for each stage to avoid knowledge gaps.
- **Penetration Testing Stages**
    1. **Pre-Engagement**
        - Define goals, scope, timeline, rules, and NDAs through contracts.
    2. **Information Gathering**
        - Collect details about target systems, hardware, and software to identify vulnerabilities.
    3. **Vulnerability Assessment**
        - Analyze data to find and evaluate vulnerabilities manually and automatically.
    4. **Exploitation**
        - Execute attacks to gain access and test identified vulnerabilities.
    5. **Post-Exploitation**
        - Escalate privileges, maintain access, and extract sensitive data.
    6. **Lateral Movement**
        - Move through the network to expand access and escalate privileges iteratively.
    7. **Proof-of-Concept**
        - Document exploitation steps to help clients understand vulnerabilities and plan remediation.
    8. **Post-Engagement**
        - Provide final reports, clean up traces, deliver presentations, and archive data securely.
- **Key Takeaways**
    - Modules emphasize detailed topic coverage to avoid misunderstandings.
    - Focused documentation ensures clarity and supports remediation efforts.
    - The process combines technical execution with thorough reporting and cleanup.



### Importance
- We must internalize this procedure and use it as a basis for all our technical engagements. 
- Each stage's components allow us to precisely understand which areas we need to improve upon and where most of our difficulties and gaps in knowledge are. 
- For example, we can think of a website as a target we need to study.

| **Stage**                     | **Description**                                                                                                                                                                                                                                                                            |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `1. Pre-Engagement`           | The first step is to create all the necessary documents in the pre-engagement phase, discuss the assessment objectives, and clarify any questions.                                                                                                                                         |
| `2. Information Gathering`    | Once the pre-engagement activities are complete, we investigate the company's existing website we have been assigned to assess. We identify the technologies in use and learn how the web application functions.                                                                           |
| `3. Vulnerability Assessment` | With this information, we can look for known vulnerabilities and investigate questionable features that may allow for unintended actions.                                                                                                                                                  |
| `4. Exploitation`             | Once we have found potential vulnerabilities, we prepare our exploit code, tools, and environment and test the webserver for these potential vulnerabilities.                                                                                                                              |
| `5. Post-Exploitation`        | Once we have successfully exploited the target, we jump into information gathering and examine the webserver from the inside. If we find sensitive information during this stage, we try to escalate our privileges (depending on the system and configurations).                          |
| `6. Lateral Movement`         | If other servers and hosts in the internal network are in scope, we then try to move through the network and access other hosts and servers using the information we have gathered.                                                                                                        |
| `7. Proof-of-Concept`         | We create a proof-of-concept that proves that these vulnerabilities exist and potentially even automate the individual steps that trigger these vulnerabilities.                                                                                                                           |
| `8. Post-Engagement`          | Finally, the documentation is completed and presented to our client as a formal report deliverable. Afterward, we may hold a report walkthrough meeting to clarify anything about our testing or results and provide any needed support to personnel tasked with remediating our findings. |