### Active Directory (AD) Attacks & Tools Timeline

#### **Overview**
Active Directory has been a key focus for security researchers, with a significant rise in the discovery of attacks and development of tools since 2014. Many attacks and techniques discovered over the years remain effective today, while new vulnerabilities continue to emerge, expanding the attack surface for both AD and Azure AD. As new tools and methods are released, both penetration testers and defenders must stay updated to secure AD environments effectively.

#### **Timeline of Key Events**

- **2021**
  - **PrintNightmare Vulnerability**: A critical remote code execution (RCE) flaw in the Windows Print Spooler service, enabling attackers to compromise AD environments.
  - **Shadow Credentials Attack**: Allows low-privileged users to impersonate other accounts and escalate privileges.
  - **noPac Attack**: Discovered in December 2021, allowing full domain control from a standard domain user account under specific conditions.

- **2020**
  - **ZeroLogon**: A critical vulnerability that allowed attackers to impersonate any unpatched domain controller, potentially gaining control of the entire domain.

- **2019**
  - **Kerberoasting Revisited** (by harmj0y): Introduced new approaches to Kerberoasting attacks.
  - **Resource-Based Constrained Delegation (RBCD)**: Techniques outlined by Elad Shamir to abuse RBCD in AD.
  - **Empire 3.0**: Re-release of PowerShell Empire, a key tool for AD exploitation and post-exploitation, now rewritten in Python.

- **2018**
  - **Printer Bug**: Discovered by Lee Christensen; the SpoolSample tool was released to exploit this flaw.
  - **Rubeus Toolkit**: Released by harmj0y for Kerberos attacks.
  - **Breaking Forest Trusts** (by harmj0y): Research on performing attacks across forest trusts.
  - **DCShadow Attack**: Released at BlueHat IL, allowing attackers to replicate domain controller behavior and push malicious changes to AD.
  - **Ping Castle**: A tool for auditing AD security, identifying misconfigurations and vulnerabilities.

- **2017**
  - **ASREPRoast**: A technique for attacking user accounts without requiring Kerberos preauthentication.
  - **ACE Up the Sleeve**: A pivotal talk on AD Access Control List (ACL) attacks by _wald0 and harmj0y.
  - **A Guide to Attacking Domain Trusts**: Blog by harmj0y focusing on enumerating and attacking domain trusts.

- **2016**
  - **BloodHound**: Released at DEF CON 24, BloodHound revolutionized AD security visualization, mapping attack paths and permissions across the network.

- **2015**
  - **PowerShell Empire Framework**: Released as a versatile post-exploitation tool, allowing for complex AD attacks and data exfiltration.
  - **PowerView 2.0**: Part of PowerTools, a powerful tool for AD reconnaissance.
  - **DCSync Attack**: Released by Benjamin Delpy and Vincent Le Toux, enabling attackers to impersonate domain controllers and extract password data.
  - **CrackMapExec**: Released as a versatile tool for automating AD attacks.
  - **Kerberos Unconstrained Delegation**: Sean Metcalf highlighted the risks in a Black Hat talk.
  - **Impacket Toolkit**: Python tools used for AD attacks, still actively maintained as of 2022.

- **2014**
  - **Veil-PowerView**: First released as a powerful AD reconnaissance tool, later integrated into the PowerSploit framework.
  - **Kerberoasting**: Introduced by Tim Medin at SANS Hackfest, a technique used to obtain service account credentials.

- **2013**
  - **Responder Tool**: Released by Laurent Gaffie, it remains a key tool for network poisoning and SMB relay attacks in AD environments.

#### **Conclusion**
AD continues to present a vast and complex attack surface, with new vulnerabilities and tools emerging regularly. Staying updated with the latest research, tools, and techniques is critical for both securing AD and conducting penetration tests to uncover potential weaknesses before attackers do.