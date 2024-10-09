`Proof of Concept` (`PoC`) or `Proof of Principle` is a project management term. In project management, it serves as proof that a project is feasible in principle. The criteria for this can lie in technical or business factors. Therefore, it is the basis for further work, in our case, the necessary steps to secure the corporate network by confirming the discovered vulnerabilities. In other words, it serves as a decision-making basis for the further course of action. At the same time, it enables risks to be identified and minimized.

![[0-PT-Process-POC_png 1.png]]

### Lateral Movement Stage Overview

- **Purpose**: Test how far an attacker can **move** within the network and what vulnerabilities can be exploited from an **internal perspective**.
  - This stage often includes revisiting previous phases (e.g., **Information Gathering**, **Vulnerability Assessment**, etc.).
  - **Lateral Movement** is essential when direct privilege escalation on the initial system is not possible, but moving through the network is still achievable.

### Key Phases in Lateral Movement

1. **Pivoting**:
   - **Objective**: Use the compromised system as a **proxy** to access otherwise **inaccessible internal systems**.
   - **Technique**: Redirect network requests from the attacker’s machine through the compromised host to the internal network. This is also known as **Tunneling**.
     - Example: Compromising a host to access systems that are not publicly reachable (e.g., printers, internal servers).
   - **Importance**: Allows scanning and exploiting non-routable networks, providing deeper access into the target environment.

2. **Evasive Testing**:
   - **Goal**: Avoid detection by bypassing security defenses such as **IPS/IDS**, **EDR**, or **network segmentation**.
   - **Methods**: Adapt attack techniques based on how defenses operate and what alerts they trigger.
   - **Focus**: Understanding **internal threat monitoring** systems and how to disguise lateral movement activities to evade detection.

3. **Information Gathering (Internal)**:
   - **Overview**: After gaining access to the internal network, revisit the **Information Gathering** phase.
   - **Scope**: Discover all reachable hosts and servers, then **enumerate** them individually to understand their roles, services, and potential weaknesses.
   - **Internal Perspective**: Gathering information from **inside the network** reveals more hosts, configurations, and network architecture not visible externally.

4. **Vulnerability Assessment (Internal)**:
   - **Difference**: Internal vulnerability assessments often reveal more vulnerabilities than those exposed to the internet.
     - More **configuration errors** and **access control issues** exist within internal networks.
   - **Focus**: Identify vulnerabilities based on user roles and **group privileges** (e.g., a compromised developer account may have access to critical resources).
   - **Targeted Information**: Look for **internal documents**, shared resources, and information that could further the attack or provide sensitive data.

5. **(Privilege) Exploitation**:
   - **Objective**: Use identified vulnerabilities to **escalate privileges** and gain access to more sensitive systems.
   - **Methods**:
     - **Cracking passwords** and **hashes** to gain higher-level access.
     - Using existing credentials on other systems to exploit **shared accounts**.
     - **Pass-the-hash**: A technique where intercepted hashes (e.g., NTLMv2 hashes) are used to authenticate without cracking.
     - Tools like **Responder** can capture hashes for privilege escalation.
   - **Outcome**: The goal is to move through the network and gain access to **multiple hosts** and **servers**.

6. **Post-Exploitation (for each compromised system)**:
   - **Objective**: Once new hosts or servers are accessed, go through the **Post-Exploitation** steps again for each system.
     - **Collect data** from the system, created users, and business information.
   - **Data Handling**: Be mindful of **data sensitivity rules** as outlined in the engagement contract.

---

### Pivoting

- **Purpose**: Enable access to internal systems that are **not directly accessible** from the attacker's machine.
- **How it Works**:
  - The compromised host acts as a **gateway** or **proxy** for the attacker’s machine.
  - Allows access to **non-routable** internal networks, enabling further scanning and exploitation.
  
- **Example**: Compromising a device within a network (e.g., a server) and using it to reach systems that are not externally accessible (e.g., printers, local databases).

---

### Privilege Exploitation & Pass-the-Hash

- **Pass-the-Hash Attack**: 
  - Intercept a **NTLMv2 hash** from a compromised system.
  - Use the hash to **authenticate** as another user (e.g., an admin) on other systems without needing the password.
  
- **Privilege Escalation**:
  - Essential for gaining higher-level access, such as **root** on Linux or **domain administrator** on Windows.
  - Privileged access opens the door to **further lateral movement** and **network control**.

---

### Post-Exploitation for Each System

- **System Review**: Once a new system is compromised, conduct **Post-Exploitation** for each:
  - **Collect information** on user accounts, sensitive files, and system configurations.
  - **Document findings** thoroughly for the final report.
  
- **Proof-of-Concept**: 
  - After completing the assessment, demonstrate the findings and help the client reproduce the results for remediation.

---

### Key Takeaways

- **Lateral Movement** is critical to testing **real-world attacker scenarios**, showing how an attacker could move across the network to gain further access or control.
- **Pivoting** helps access otherwise unreachable systems, allowing for **deeper network penetration**.
- **Privilege Escalation** and tools like **Responder** or **pass-the-hash** are essential techniques for gaining broader access and moving laterally.
- **Post-Exploitation** must be performed for each compromised system, carefully handling sensitive data as per the engagement rules.