**Hack The Box Origins and Evolution**  
- HTB was initially a competitive platform for experienced professionals to practice hacking.
- It wasn't designed for beginners, offering only CTF-style challenges with no hints or guidance.
- Over time, HTB recognized the need for beginner-friendly content, leading to the creation of HTB Academy.
- HTB Academy aims to guide beginners while also helping advanced practitioners upskill.
- HTB also launched **Starting Point**, a guided approach to help users ease into the platform and eventually tackle competitive boxes.

**IT Overview and Importance of Fundamentals**  
- IT encompasses various subfields: Cybersecurity, Information Security, Network Administration, etc.
- Becoming proficient in IT requires dedication and effort, especially in cybersecurity, which demands a deeper understanding of many areas (networking, systems, databases, etc.).
- Expertise in penetration testing relies on having in-depth knowledge of the systems being tested.
- For example, web developers may master web technologies like HTML, CSS, and SQL but can still make critical security errors.

**HTB’s Teaching Philosophy**  
- HTB aims to provide a structured, efficient learning path that focuses on building fundamental skills.
- Many tasks are designed to encourage critical thinking and analytical skills, which are essential for success in penetration testing.
- Learning analytical thinking requires practice, similar to mastering a musical instrument—it can’t be taught in one module.
- The goal is to craft professionals who question everything and find nuances others miss.

**Hands-on Learning and Practice**  
- Practical, hands-on experience is crucial to developing skills in penetration testing.
- Knowing the theory or history of computers is not enough without the ability to apply knowledge in real-world scenarios.
  
**Module Structure**  
- HTB has structured its learning materials to be challenging but effective.
- Beginners or advanced users looking to improve can follow a recommended module sequence for specific penetration testing processes.

![[0-PT-Process_png.png]]


**Pre-Engagement Stage**  
- The stage where key details are documented and agreed upon.
- Main commitments, tasks, scope, and limitations are outlined.
- Contractual documents are drafted during this phase.
- Essential information is exchanged between penetration testers and the client, depending on the type of assessment.

![[0-PT-Process-PRE_png.png]]

**Path: Information Gathering**  
- Focuses on identifying target systems before examination or attack.
- Customers may provide minimal information, such as a domain name or IP addresses.

**Foundational Modules:**  
1. **Learning Process**
   - Learn how the brain works to improve learning efficiency.
   - Tier 0, 12 sections, 3 hours.

2. **Linux Fundamentals**
   - Understand the structure of Linux for exploitation.
   - Tier 0, 18 sections, 6 hours.
   - Learn Windows basics to handle systems efficiently.
   - Tier 0, 14 sections, 6 hours.

4. **Introduction to Networking**
   - Essential to understand communication between hosts in internal/external networks.
   - Tier 0, 12 sections, 3 hours.

5. **Introduction to Web Applications**
   - Learn how web applications function and their processes.
   - Tier 0, 17 sections, 3 hours.

6. **Web Requests**
   - Understand various types of web requests and misconfigurations for potential exploitation.
   - Tier 0, 8 sections, 4 hours.

7. **JavaScript Deobfuscation**
   - Understand and deobfuscate JavaScript to analyze dynamic web pages.
   - Tier 0, 11 sections, 4 hours.

8. **Introduction to Active Directory**
   - Learn how companies manage large networks using Active Directory.
   - Tier 0, 16 sections, 7 hours.

9. **Getting Started**
   - Includes tips and tricks for beginners, a walkthrough for solving vulnerable boxes.
   - Tier 0, 23 sections, 8 hours.

### Information Gathering Notes:
- **Essential Part of Any Assessment:**
  - Information gathering is foundational to all assessments.
  
- **Importance of Information:**
  - The conclusions and actions taken are based on the information available.
  
- **Retrieval Skills:**
  - Knowing how to retrieve information effectively is critical.

- **Goal-Oriented Approach:**
  - The method of gathering information should align with the assessment's goals. 

![[0-PT-Process-IG_png.png]]

### Vulnerability Assessment Path Notes:

- **Vulnerability Assessment:**
  - **Next stage after information gathering.**
  - Involves using vulnerability scanners and manual analysis to find weaknesses in the target systems.

- **Influence on Exploitation Stage:**
  - The quality of information gathered determines how successful the exploitation will be.
  - Detailed notes and thoroughness during information gathering are crucial for effective vulnerability assessment.

- **Common Pitfall:**
  - Jumping into exploitation without sufficient information gathering can waste time and cause missed opportunities.

- **Key Focus Areas:**
  - **Organization and patience** are essential.
  - Keeping track of findings to revisit during exploitation is critical.
  - **Time management** is vital to avoid wasting time during assessments.

---

### Modules and Tools for Vulnerability Assessment:

1. **Network Enumeration with Nmap:**
   - Perform network enumeration, identify targets, and bypass security measures like firewalls and IPS/IDS.
   - **Level:** Tier I (Easy, Offensive)
   - **Duration:** 12 sections, 7 hours

2. **Footprinting:**
   - Examine services running on hosts, identify footprints, and learn how to exploit misconfigurations.
   - **Level:** Tier II (Medium, Offensive)
   - **Duration:** 20 sections, 2 days

3. **Information Gathering - Web Edition:**
   - Focus on web servers and applications, identifying hidden or developer-focused apps that may provide vulnerabilities.
   - **Level:** Tier II (Easy, Offensive)
   - **Duration:** 10 sections, 7 hours

4. **OSINT: Corporate Recon:**
   - Open-source intelligence for finding information about target companies from public sources, including social media.
   - **Level:** Tier IV (Hard, Offensive)
   - **Duration:** 23 sections, 2 days


### Vulnerability Assessment Notes:
- **Two Main Approaches:**
  1. **Automated Scanning:**
     - Uses tools to check for known vulnerabilities by comparing target systems against a vulnerability database.
     - Common practice in companies for regularly scheduled vulnerability assessments.

  2. **Manual Analysis:**
     - Involves looking beyond automated results to identify potential vulnerabilities that may not be detected by tools.
     - Requires a deeper understanding of systems, creativity, and the ability to connect various information points.

- **Purpose:**
  - Identify weaknesses that can be exploited for gaining unauthorized access or privileges.

- **Key Skills Required:**
  - **Technical Knowledge:** Understanding how systems and applications function.
  - **Creativity:** Thinking outside the box to exploit gaps that may not be obvious.
  - **Problem-Solving:** Recognizing and interpreting connections between different pieces of information.

- **Importance in Security Audits:**
  - Regular audits help ensure infrastructure remains protected against new vulnerabilities as databases and tools are updated.

![[0-PT-Process-VA_png.png]]

### Paths After Vulnerability Assessment:

1. **Exploitation:**
   - Involves actively exploiting a discovered vulnerability when we do not yet have access to a system.
   - Requires preparing the tools and methods necessary to exploit identified gaps.

2. **Post-Exploitation:**
   - Focuses on **privilege escalation** after gaining initial access.
   - Involves interacting with the system and elevating privileges to gain more control over the system.

3. **Lateral Movement:**
   - Moving from the exploited system to other systems in the network.
   - May or may not require privilege escalation, depending on the circumstances.

4. **Information Gathering (Revisiting):**
   - Returning to gather more information if there’s insufficient data to proceed.
   - Helps refine the understanding of the target and identify further vulnerabilities or entry points.

---

### Key Concepts:

- **Analysis & Experience:**
  - Analysis improves with experience, helping to connect patterns and recognize vulnerabilities.
  - This is similar to learning to read; familiarity with specific behaviors and setups helps us identify weak points.

- **Vulnerability Assessment:**
  - Using automated tools to detect known vulnerabilities.
  - These tools provide insight into potential weaknesses and can reveal new attack paths.
  
---

### Skills for Future Stages:

1. **File Transfers:**
   - Essential for transferring required data to exploit vulnerabilities.
   - Mastering file transfer techniques for both **Windows** and **Linux** systems is critical to avoid dead ends.

2. **Shells & Payloads:**
   - Knowing how to generate and transfer the right payloads to gain further access.
   - Shells and payloads must be customized for the specific environment and system.

3. **Metasploit Framework:**
   - A versatile tool that aids in various attacks, including enumeration and privilege escalation.
   - Learning its capabilities can speed up the exploitation process, but understanding its limitations is also important.


### Exploitation Notes

- **Definition:**
  - Exploitation refers to the process of attacking a system or application by leveraging identified vulnerabilities found during the Information Gathering and Vulnerability Assessment stages.

- **Process Overview:**
  - **Information Gathering Stage:** Collecting data about the target systems and applications.
  - **Vulnerability Assessment Stage:** Analyzing the collected information to identify potential weaknesses.
  - **Preparation:** Developing strategies and methods for executing attacks based on the assessed vulnerabilities.

- **Considerations:**
  - Many organizations may use the same applications, but configuration choices vary based on individual objectives and requirements.
  - Understanding the unique configurations and contexts of each organization is critical, as the same application can serve different purposes across different environments.

- **Key Takeaway:**
  - A successful exploitation relies on a thorough understanding of the vulnerabilities and the specific configurations of the target system, allowing for tailored attack strategies that align with the organization’s use of its applications.

![[0-PT-Process-EX_png.png]]

### Exploitation Stage Notes

#### Paths After Initial Access
1. **Information Gathering:**
   - Once access is obtained, regardless of privileges, gather local system information.
   - Information will be used for privilege escalation, lateral movement, or data exfiltration.
   - Leads to the Vulnerability Assessment stage for analyzing findings.

2. **Post-Exploitation:**
   - Focuses on escalating privileges if the highest rights have not yet been attained.
   - Involves Information Gathering, Vulnerability Assessment, Exploitation, and Lateral Movement from an internal perspective.
   - Can lead back to Information Gathering if highest privileges are already achieved.

3. **Lateral Movement:**
   - Can skip directly to this stage if the highest privileges are obtained on a dual-homed system.
   - Allows enumeration of hosts previously inaccessible.

4. **Proof-of-Concept:**
   - After gaining high privileges (e.g., Domain Admin in Active Directory), create a proof-of-concept to detail and potentially automate paths and activities.
   - Available for technical department use.

#### Network Protocols and Web Exploitation
- The exploitation stage is divided into two areas:
  1. **Network Protocols:**
     - Understanding common protocols and their vulnerabilities is critical.
     - Web servers and applications may contain exploitable information.
     - Remotely exposed services may have misconfigurations or public vulnerabilities.

- **Web Exploitation:**
  - A vital area due to the variety of web technologies and frequent updates.
  - Emphasizes strong enumeration and exploitation skills as web applications are often primary targets during penetration testing.

#### Key Modules in Exploitation
1. **Password Attacks:**
   - Techniques for obtaining credentials remotely and locally on Windows and Linux systems.
   - *Tier I, Medium, 18 Sections, 8 hours.*

2. **Attacking Common Services:**
   - Covers attacks on essential network services and web applications.
   - *Tier II, Medium, 19 Sections, 8 hours.*

3. **Pivoting, Tunneling & Port Forwarding:**
   - Using exploited systems to communicate between networks or internal systems.
   - *Tier II, Medium, 18 Sections, 2 days.*

4. **Active Directory Enumeration & Attacks:**
   - Understanding Active Directory's vulnerabilities and management.
   - *Tier II, Medium, 36 Sections, 7 days.*

#### Web Exploitation Modules
1. **Using Web Proxies:**
   - Analyze and manipulate HTTP/HTTPS requests and responses.
   - *Tier II, Easy, 15 Sections, 8 hours.*

2. **Attacking Web Applications with Ffuf:**
   - Discovering application parameters for further exploitation.
   - *Tier 0, Easy, 13 Sections, 5 hours.*

3. **Login Brute Forcing:**
   - Gaining access through authentication mechanism vulnerabilities.
   - *Tier II, Easy, 11 Sections, 6 hours.*

4. **SQL Injection Fundamentals:**
   - Exploiting databases linked to web applications.
   - *Tier 0, Medium, 17 Sections, 8 hours.*

5. **SQLMap Essentials:**
   - Using SQLMap to streamline attacks against web application databases.
   - *Tier II, Easy, 11 Sections, 8 hours.*

6. **Cross-Site Scripting (XSS):**
   - Leveraging XSS vulnerabilities for various attacks.
   - *Tier II, Easy, 10 Sections, 6 hours.*

7. **File Inclusion:**
   - Exploiting vulnerabilities to access or execute files.
   - *Tier 0, Medium, 11 Sections, 8 hours.*

8. **Command Injections:**
   - Executing system commands directly through command injection vulnerabilities.
   - *Tier II, Medium, 12 Sections, 6 hours.*

9. **Advanced Web Attacks:**
   - Involves vulnerabilities like HTTP Verb Tampering, IDOR, and XXE.
   - *Tier II, Medium, 18 Sections, 2 days.*

10. **Attacking Common Applications:**
    - Strategies for attacking commonly used web applications.
    - *Tier II, Medium, 22 Sections, 2 days.*


### Post-Exploitation Notes
- **Overview**: 
  - After exploiting services to gain access to a system, obtaining the highest privileges is often not achieved immediately.
  - Services are usually configured to be "isolated" to thwart potential attackers.
  
- **Privilege Escalation**:
  - The primary focus in this stage is to bypass restrictions and escalate privileges.
  - It can be challenging to escalate privileges effectively.

- **Understanding Operating Systems**:
  - A deep understanding of how the operating systems (OS) function is crucial for successful escalation.
  - Techniques must be adapted based on the specific OS in use.

- **Linux vs. Windows**:
  - Familiarity with both **Linux Privilege Escalation** and **Windows Privilege Escalation** techniques is essential.
  - Each OS has its own unique methods and vulnerabilities that can be exploited for privilege escalation.

![[0-PT-Process-POEX_png.png]]

### Post-Exploitation Paths

**Overview**: After gaining access to a system, there are four potential paths depending on the progress made during exploitation.

| **Path**                       | **Description**                                                                                                                                                                                                                                                                                                                             |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Information Gathering / Pillaging** | - Before escalating privileges, gather an overview of the system's inner workings. <br>- Identify users and available options. <br>- This step, known as Pillaging, is essential and not optional. <br>- Leads to the vulnerability assessment stage for analysis and evaluation of gathered information.                                                      |
| **Exploitation**               | - If sensitive information about the system is discovered, it can be used to exploit local applications or services with higher privileges. <br>- This allows for executing commands with escalated privileges.                                                                                                                                                           |
| **Lateral Movement**           | - Directly move to Lateral Movement if certain conditions are met. <br>- If the highest privileges are achieved on a dual-homed system connecting two networks, use this host to enumerate previously inaccessible hosts.                                                                                                                                       |
| **Proof-of-Concept**          | - After gaining the highest privileges, create a Proof-of-Concept by exploiting an internal system. <br>- Even if not all systems are taken over, having Domain Admin privileges in an Active Directory environment allows for free movement across the network. <br>- Document and potentially automate paths and activities for the technical department. |

---

### Considerations for Operating Systems

- During penetration testing, it’s crucial to assess how far an attacker could go within a network.
- There are various versions of operating systems, including:
  - **Windows**: XP, 7, 8, 10, 11, and Server 2008, 2012, 2016, 2019.
  - **Linux Distributions**: Ubuntu, Debian, Parrot OS, Arch, Deepin, Red Hat, Pop!_OS, etc.
- Understanding each system’s individual weak points is essential for effective exploitation.

---

### Linux Privilege Escalation

- Most web servers and critical infrastructure services run on Linux.
- A strong understanding of Linux fundamentals is necessary due to widespread usage.
- Many misconfigurations can occur in Linux systems, and identifying these flaws is crucial for privilege escalation.

---

### Windows Privilege Escalation

- Modern Windows systems may have stronger security measures, but administrator errors can occur.
- Understanding how to find misconfigurations in Windows systems is essential for privilege escalation.

### Lateral Movement

**Definition**: Lateral movement refers to the techniques used to navigate through a corporate network after gaining initial access. It is crucial for expanding access and privileges within the network.

**Key Points**:
- **Purpose**: 
  - Allows for overlapping with other internal hosts.
  - Facilitates further privilege escalation within the current subnet or other areas of the network.

- **Access Requirements**:
  - Requires access to at least one system within the corporate network.
  - Initial privileges gained during the Exploitation stage do not significantly impact the ability to move laterally, as movement can occur without administrator rights.

- **Importance**:
  - Enables attackers to explore and exploit other systems, potentially increasing their foothold and control within the network.
  
- **Techniques**:
  - Utilize tools and techniques to discover other hosts and services within the network.
  - Can involve the use of legitimate network protocols and tools to avoid detection.

![[0-PT-Process-LA_png.png]]

### Lateral Movement Paths

After achieving lateral movement within a network, there are three possible paths to take:

| **Path**                     | **Description**                                                                                                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Vulnerability Assessment** | - If the penetration test is ongoing, we can transition to the Vulnerability Assessment stage. <br> - Here, we analyze information gathered during pillaging to identify vulnerable network services or applications with exploitable authentication mechanisms. |
| **Information Gathering / Pillaging** | - Following successful lateral movement, we can return to the Pillaging stage. <br> - This involves local information gathering on the newly accessed target system to collect valuable data for further exploitation. |
| **Proof-of-Concept**         | - After completing the last lateral movement and finalizing the attack on the corporate network, we summarize our findings. <br> - This may include automating certain processes to demonstrate the vulnerabilities identified during the engagement. |

### Additional Notes
- Both Lateral Movement and Pillaging require access to a previously exploited system.
- Techniques related to these paths are covered in various modules, including:
  - Getting Started
  - Linux Privilege Escalation
  - Windows Privilege Escalation
  - Other relevant areas to enhance understanding and effectiveness during penetration testing activities.

### Proof-of-Concept (POC)
- **Definition**: 
  - The Proof-of-Concept (POC) serves as evidence that a discovered vulnerability exists.

- **Administrator Actions**:
  - Upon receiving the penetration test report, administrators will attempt to reproduce the vulnerabilities to confirm their existence.
  - No changes to business-critical processes will be made without verifying the vulnerability.

- **Considerations in Large Networks**:
  - Large networks often consist of multiple interoperating systems and dependencies, necessitating thorough checks after any changes.
  - Changes can be time-consuming and costly, as they may affect various systems and processes.

- **Impact of Vulnerability Findings**:
  - Just because a vulnerability is identified does not mean remediation is straightforward.
  - Administrators must ensure that fixes do not negatively impact other systems or business operations.

- **Role of POCs in Penetration Testing**:
  - POCs are included in the documentation provided as part of a high-quality penetration test.
  - They allow administrators to independently confirm and validate the reported vulnerabilities.

![[0-PT-Process-POC_png.png]]

### Post-Engagement Notes

- **Single Path**:
  - **Path**: Post-Engagement
  - **Description**: This stage involves optimizing and improving the documentation from the penetration testing process. The refined documentation is sent to the customer after thorough review.

- **Information Utilization**:
  - After gathering all relevant information and exploiting identified vulnerabilities, automating individual steps becomes relatively straightforward.

### Introduction to Python 3

- **Overview**:
  - Python is recognized as one of the easiest programming languages to learn while being powerful enough for various applications, including automation.

- **Benefits of Using Python for Automation**:
  - **Ease of Learning**: Its straightforward syntax makes it accessible for beginners.
  - **Powerful Capabilities**: Suitable for automating many steps in penetration testing processes.
  - **Code Documentation**: Python allows the inclusion of comments, enhancing understanding of how vulnerabilities are exploited step-by-step.

- **Course Structure**:
  - **Tier**: I
  - **Difficulty**: Easy
  - **Sections**: 14
  - **Estimated Time**: 10 hours

### Post-Engagement Notes

- **Objective**:
  - Clean up exploited systems to ensure they cannot be exploited using the tools deployed during testing.
  
- **Risks**:
  - Leaving behind tools (e.g., bind shells) on systems can compromise security and endanger the network.
  
- **Actions Required**:
  - Remove all content transferred during the penetration test to restore the corporate network to its original state.
  - Document system changes, successful exploitation attempts, captured credentials, and uploaded files in the report's appendices.
    - This helps clients correlate any alerts they receive with testing activities to differentiate between test actions and actual attacks.

- **Documentation**:
  - Reconcile all notes with ongoing documentation to ensure no steps are overlooked.
  - Provide a comprehensive, well-formatted report to clients.

### Documentation & Reporting

- **Importance**:
  - Proper documentation and reporting are crucial for organizing notes and delivering high-quality client deliverables.

- **Benefits**:
  - Streamlines report preparation, saving time and effort.
  - Helps optimize note-taking and organization to enhance efficiency.

- **Course Structure**:
  - **Tier**: II
  - **Difficulty**: Easy
  - **Sections**: 8
  - **Estimated Time**: 20 hours (2 days)

### Attacking Enterprise Networks

- **Overview**:
  - Maintaining a comprehensive view of the various stages, contents, and challenges involved in attacking enterprise networks is vital.
  
- **Challenges**:
  - The complexity of large networks can be daunting, leading to potential oversight of essential vulnerabilities.

- **Focus Areas**:
  - Understand strategies for effectively attacking enterprise networks.
  - Identify vulnerabilities associated with a multitude of systems within a network.

- **Course Structure**:
  - **Tier**: II
  - **Difficulty**: Medium
  - **Sections**: 14
  - **Estimated Time**: 20 hours (2 days)

### Additional Note
- Brief overview of HTB Academy exercises and question presentation will follow, detailing their approach to penetration testing training.