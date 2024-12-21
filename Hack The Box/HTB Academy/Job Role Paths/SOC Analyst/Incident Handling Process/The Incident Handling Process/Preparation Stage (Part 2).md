### Introduction
- Another part of the `preparation` stage is to protect against incidents. 
- While protection is not necessarily the responsibility of an incident handling team, any protection-related activities should be known to them to better understand the type and sophistication of an incident and know where to look for artifacts/evidence, that could aid the investigation.
- Let us now look at some of the highly recommended protective measures, which have a high mitigation impact against the majority of threats.



### DMARC
- **DMARC (Domain-based Message Authentication, Reporting, and Conformance)**:
    - Built on top of **SPF (Sender Policy Framework)** and **DKIM (DomainKeys Identified Mail)**, DMARC is an email protection mechanism against phishing.
    - It rejects emails that appear to come from your organization but are actually spoofed by an attacker, such as a phishing email pretending to be from an employee requesting a payment.
    - **Advantages**:
        - Easy and inexpensive to implement.
        - Provides a layer of security to prevent fraudulent emails from reaching recipients.
    - **Important Considerations**:
        - Thorough testing is essential to avoid blocking legitimate emails.
        - **Email Filtering Rules**: You can enhance DMARC protection by checking email headers for DMARC failures. However, this requires extensive testing to avoid false positives.
        - **False Positives**: Emails sent 'on behalf of' via email services often fail DMARC due to domain mismatches, so this needs careful handling in the filtering setup.



### Endpoint Hardening (& EDR)
- **Endpoint Hardening**:
    - **Critical Entry Points**: Endpoint devices like workstations and laptops are primary entry points for most cyberattacks, especially those originating from internet activity such as browsing, opening attachments, or executing malicious files.
    - **Hardening Standards**: Popular hardening baselines like **CIS** and **Microsoft baselines** provide solid frameworks for securing endpoints. These should form the foundation of an organization’s endpoint security strategy.
- **Effective Actions to Strengthen Endpoint Security**:
    - **Disable LLMNR/NetBIOS**: Prevents local network attacks by disabling unnecessary network protocols.
    - **Implement LAPS (Local Administrator Password Solution)**: Ensures that each endpoint has a unique, complex local administrator password, and remove administrative privileges from regular users.
    - **Constrain PowerShell**: Set PowerShell to **"ConstrainedLanguage"** mode to limit its potential misuse by attackers.
    - **Enable Attack Surface Reduction (ASR)**: Use **Microsoft Defender** to enable ASR rules that block common attack vectors.
    - **Whitelisting**: While challenging, consider blocking execution from user-writable folders like **Downloads, Desktop**, and **AppData**. Also, block script types like **.hta**, **.vbs**, **.cmd**, **.bat**, and **.js**, which are frequently used in attacks.
        - **LOLBin Considerations**: Be aware of **LOLBin** files, legitimate binaries abused by attackers to bypass whitelisting.
    - **Host-Based Firewalls**: Ensure that at a minimum, **workstation-to-workstation** communication is blocked and outbound traffic to **LOLBin** tools is prevented.
    - **Deploy an EDR (Endpoint Detection and Response)**: Use products that integrate with **AMSI (Antimalware Scan Interface)**, which enhances visibility and enables the detection of obfuscated malware in scripts.
- **Mindset for Hardening**:
    - **"Don't let perfect be the enemy of good"**: Focus on implementing effective security measures rather than waiting for a perfect, all-encompassing solution. Even incremental steps can significantly enhance your endpoint protection.



### Network Protection
- Network segmentation is a powerful technique to avoid having a breach spread across the entire organization. 
- Business-critical systems must be isolated, and connections should be allowed only as the business requires. 
- Internal resources should really not be facing the Internet directly (unless placed in a DMZ).
- Additionally, when speaking of network protection you should consider IDS/IPS systems. 
- Their power really shines when SSL/TLS interception is performed so that they can identify malicious traffic based on content on the wire and not based on reputation of IP addresses, which is a traditional and very inefficient way of detecting malicious traffic.
- Additionally, ensure that only organization-approved devices can get on the network. Solutions such as 802.1x can be utilized to reduce the risk of bring your own device (BYOD) or malicious devices connecting to the corporate network. 
- If you are a cloud-only company using, for example, Azure/Azure AD, then you can achieve similar protection with Conditional Access policies that will allow access to organization resources only if you are connecting from a company-managed device.



### Privilege Identity Management / MFA / Passwords
- **Credential Theft in Active Directory Environments**:
    - **Common Attack Path**: Stealing privileged user credentials is one of the most common escalation paths for attackers within Active Directory (AD) environments.
    - **Admin User Password Mistakes**: Many admin users fall into the trap of using weak but complex passwords, or they may use the same password for both regular and privileged accounts. These credentials can be easily obtained via various attack methods, such as keylogging.
    - **Weak but Complex Passwords**: A "complex" password like **Password1!** (combining uppercase, lowercase, numbers, and special characters) is still predictable and commonly found in password lists used by attackers. These passwords, though seemingly strong, can be easily cracked or guessed due to their simplicity in structure.
    - **Recommendation for Stronger Passwords**: Encourage employees to use **passphrases**, which are much harder to guess and significantly more difficult to brute-force. For example, **"i LIK3 my coffeE warm"** is long, complex, and memorable. For added security, passphrases in **multiple languages** can further protect accounts by adding complexity and reducing guessability.
- **Multi-Factor Authentication (MFA)**:
    - **Essential Protection**: Implement **MFA** for any **administrative access** to applications and devices, including systems in Active Directory. MFA adds an additional layer of security, ensuring that even if credentials are compromised, an attacker cannot easily access the system without the second authentication factor.



### Vulnerability Scanning
- Perform continuous vulnerability scans of your environment and remediate at least the "high" and "critical" vulnerabilities that are discovered. 
- While the scanning can be automated, the fixes usually require manual involvement. 
- If you can't apply patches for some reason, definitely segment the systems that are vulnerable!



### User Awareness Training
- Training users to recognize suspicious behavior and report it when discovered is a big win for us. 
- While it is unlikely to reach 100% success on this task, these trainings are known to significantly reduce the number of successful compromises. 
- Periodic "surprise" testing should also be part of this training, including, for example, monthly phishing emails, dropped USB sticks in the office building, etc.



### Active Directory Security Assessment
- The best way to detect security misconfigurations or exposed critical vulnerabilities is by looking for them from the perspective of an attacker. 
- Doing your own reviews (or hiring a third party if the skillset is missing from the organization) will ensure that when an endpoint device is compromised, the attacker will not have a one-step escalation possibility to high privileges on the network.
- The more additional tools and activity an attacker is generating, the higher the likelihood of you detecting them, so try to eliminate easy wins and low-hanging fruits as much as possible.
- Active Directory has a few known and unique escalation paths/bugs. 
- New ones are quite often discovered too. 
- Active Directory security assessments are crucial for the security posture of the environment as a whole. 
- Don't assume that your system administrators are aware of all discovered or published bugs, because in reality they probably aren't.



### Purple Team Exercises
- We need to train incident handlers and keep them engaged. 
- There is no question about that, and the best place to do it is inside an organization's own environment. 
- Purple team exercises are essentially security assessments by a red team that either continuously or eventually inform the blue team about their actions, findings, any visibility/security shortcomings, etc. 
- Such exercises will help in identifying vulnerabilities in an organization while testing the blue team's defensive capability in terms of logging, monitoring, detection, and responsiveness.
- If a threat goes unnoticed, there is an opportunity to improve. 
- For those that are detected, the blue team can test any playbooks and incident handling procedures to ensure they are robust and the expected result has been achieved.



### Questions
- What can we use to block phishing emails pretending to originate from our mail server?
	- DMARC
- True or False: "Summer2021!" is a complex password.
	- True