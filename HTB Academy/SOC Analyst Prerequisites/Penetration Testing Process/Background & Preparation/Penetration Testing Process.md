
1. **Definition of Processes in Various Contexts:**
   - **Social sciences**: Processes are a directed sequence of events.
   - **Operational/organizational**: Refers to work, business, production, or value creation processes.
   - **Computer systems**: Processes are programs running, usually as part of the system software.
2. **Types of Processes:**
   - **Deterministic processes**: Each state is causally dependent on previous states.
   - **Stochastic processes**: States follow with certain probabilities, not determined by previous states.
3. **Application in Penetration Testing:**
   - The **penetration testing process** is modeled after the social sciences definition, as it is based on discovering or provoking events/results.
   - Penetration testing is defined as successive steps and events by the tester to reach a predefined objective.
4. **Characteristics of Penetration Testing Processes:**
   - Describes a sequence of operations leading to a desired result.
   - Not a fixed recipe or step-by-step guide—requires flexibility and adaptation based on client infrastructure, objectives, and received information.
5. **Penetration Testing Stages:**
   - Often represented as a circular process, where disruption of one component can disrupt the entire process.
   - If new information is obtained, it results in a new process approach, though it builds on the previous steps.
   - Flexibility is crucial—there are no rigid guidelines, but rather adaptable stages where the penetration tester can modify steps based on evolving information.
   - The tester must constantly adjust to each unique environment, adapting their methods accordingly.
6. **Playbooks in Penetration Testing:**
   - While stages can be pre-defined, the tester develops their own playbook for different things tried at each stage.
   - Flexibility is key as every environment is different, necessitating continuous adaptation.

![[0-PT-Process_png 1.png]]

1. **Study Plan Overview:**
   - The penetration testing process is divided into stages.
   - Study plan involves working through modules for each stage before proceeding to the next.
   - Modules focus on phases like Information Gathering, Lateral Movement, and Pillaging, which are repeated throughout the process.
   - Each module builds specific knowledge, and skipping them may lead to misunderstandings.

2. **Stages of Penetration Testing:**
   - **Pre-Engagement**: 
     - Educating the client and formalizing the contract.
     - Components include a Non-Disclosure Agreement (NDA), setting goals, defining the scope, estimating time, and establishing rules of engagement.

   - **Information Gathering**: 
     - Collecting information about the target company's systems, software, and hardware.
     - This stage aims to uncover potential security gaps for later exploitation.

   - **Vulnerability Assessment**: 
     - Analyzing the results from Information Gathering.
     - Manually and automatically evaluating vulnerabilities in the target systems.
     - Helps assess the threat level and susceptibility to attacks.

   - **Exploitation**: 
     - Testing and executing attacks based on the identified vulnerabilities.
     - Goal is to gain initial access to the target systems.

   - **Post-Exploitation**: 
     - Ensuring continuous access to the compromised system.
     - Privilege escalation and searching for sensitive data (e.g., credentials).
     - Sometimes performed to demonstrate impact, or as input for Lateral Movement.

   - **Lateral Movement**: 
     - Moving across the network to access additional hosts or higher privilege systems.
     - Often combined with Post-Exploitation to further penetrate deeper into the network.
     - Techniques are based on information gathered from the exploited systems.

   - **Proof-of-Concept**: 
     - Documenting the steps taken to compromise the network.
     - Shows how vulnerabilities were chained together to achieve goals.
     - May include scripts to automate steps for the client to reproduce findings.

   - **Post-Engagement**: 
     - Preparing detailed documentation for both technical staff and management.
     - Deliverables include a formal report, report walkthrough meetings, and possibly an executive presentation.
     - Cleanup of traces and archiving of test data based on contractual obligations.

3. **Importance of the Process:**
   - This procedure forms the basis for all technical engagements.
   - Helps pinpoint areas needing improvement and addresses gaps in knowledge.
   - Flexibility is key since no two environments are the same, requiring constant adaptation.

4. **Stage Breakdown for Web Application Testing:**
   - **Pre-Engagement**: Document creation and discussion of objectives.
   - **Information Gathering**: Investigate technologies and features of the web application.
   - **Vulnerability Assessment**: Search for known vulnerabilities in the application.
   - **Exploitation**: Test and exploit vulnerabilities using prepared tools and code.
   - **Post-Exploitation**: Further examination of the compromised system for sensitive information and potential privilege escalation.
   - **Lateral Movement**: If applicable, move across the network to access other systems.
   - **Proof-of-Concept**: Create documentation proving vulnerabilities and automation where possible.
   - **Post-Engagement**: Deliver the final report and walkthrough with the client.