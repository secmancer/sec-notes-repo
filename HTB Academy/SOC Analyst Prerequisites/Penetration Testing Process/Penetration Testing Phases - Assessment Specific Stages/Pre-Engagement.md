**Pre-engagement Stage (Penetration Testing)**
- **Purpose**: Preparation for the actual penetration test.
- **Key Activities**:
  - Asking detailed questions to clarify scope and objectives.
  - Making contractual agreements regarding the test.
- **Client's Role**: 
  - Provides information about what they want to be tested (specific systems, applications, etc.).
- **Penetration Tester’s Role**:
  - Explains how to conduct the test efficiently.
  - Discusses testing methods, timelines, and reporting expectations.

![[0-PT-Process-PRE_png 1.png]]

**Pre-engagement Process (Penetration Testing)**

**1. Components**:
   - **Scoping Questionnaire**: Identifies the systems, applications, and scope of the test.
   - **Pre-engagement Meeting**: Discusses specifics of the test, including methods and timelines.
   - **Kick-off Meeting**: Initiates the penetration test and finalizes agreements.

**2. NDA (Non-Disclosure Agreement)**: Must be signed before detailed discussions. Several types:
   - **Unilateral NDA**: Obligates only one party to confidentiality.
   - **Bilateral NDA**: Both parties must maintain confidentiality (most common for penetration tests).
   - **Multilateral NDA**: Multiple parties commit to confidentiality (used for cooperative networks).

**3. Authorized Parties**:
   - It is critical to verify who is authorized to hire for penetration testing. Unauthorized requests may pose legal risks.
   - Authorized individuals may include:
     - CEO, CTO, CISO, CSO, CRO, CIO
     - VP of Internal Audit, Audit Manager, VP/Director of IT or Information Security

**4. Key Points**:
   - Establish the signatory authority for contracts, Rules of Engagement (RoE), and the primary/secondary points of contact for the project.
   - Legal and operational documents must be prepared and signed by both parties to ensure compliance with laws like the Computer Misuse Act.

**5. Required Documents**:
   - **Non-Disclosure Agreement (NDA)**: After initial contact.
   - **Scoping Questionnaire**: Before the pre-engagement meeting.
   - **Scoping Document**: During the pre-engagement meeting.
   - **Penetration Testing Proposal (SoW)**: During the pre-engagement meeting.
   - **Rules of Engagement (RoE)**: Before the kick-off meeting.
   - **Contractors Agreement (Physical Assessments)**: Before the kick-off meeting.
   - **Reports**: Created during and after the test.

**6. Additional Notes**:
   - Separate scoping documents may be provided by the client for in-scope IPs/URLs.
   - All documents should be reviewed and adapted by a lawyer to ensure legal compliance.

**Scoping Questionnaire (Penetration Testing)**

**Purpose**: Sent after initial client contact to understand their testing needs and clarify services.

**Services Offered**:
   - ☐ Internal Vulnerability Assessment
   - ☐ External Vulnerability Assessment
   - ☐ Internal Penetration Test
   - ☐ External Penetration Test
   - ☐ Wireless Security Assessment
   - ☐ Application Security Assessment
   - ☐ Physical Security Assessment
   - ☐ Social Engineering Assessment
   - ☐ Red Team Assessment
   - ☐ Web Application Security Assessment

**Service Customization**: Allows the client to specify details such as:
   - Web or mobile application assessment
   - Secure code review
   - Black box, semi-evasive, or phishing assessments (e.g., phishing or vishing calls)
   - Depth of social engineering and other tests

**Key Information Requested**:
   - Client name, address, key contact details
   - Number of expected live hosts
   - Number of IPs/CIDR ranges in scope
   - Number of domains/subdomains
   - Number of wireless SSIDs in scope
   - Number of web/mobile applications; authentication roles (standard user, admin)
   - For phishing assessments: number of targeted users; client-provided or OSINT-generated list
   - Physical assessments: number of locations; geographic dispersion
   - Red Team assessment objectives; out-of-scope activities (phishing, physical attacks)
   - Active Directory Security Assessment request
   - Network testing requirements (anonymous user vs. domain user, bypassing Network Access Control (NAC))

**Information Disclosure and Evasiveness**:
   - Penetration Test type:
     - Black box (no information provided)
     - Grey box (IP address/CIDR ranges/URLs provided)
     - White box (detailed information provided)
   - Testing approach:
     - Non-evasive, hybrid-evasive (start quietly, gradually increase activity)
     - Fully evasive

**Purpose of Scoping Questionnaire**:
   - Helps align resources to meet the client's expectations
   - Used to prepare an accurate proposal and timeline
   - Cost estimation based on complexity (e.g., vulnerability assessment vs. red team)
   
**Next Step**: Information is summarized into the **Scoping Document** for the pre-engagement phase.

Here are the notes on the **Pre-Engagement Meeting** and associated processes:

### Pre-Engagement Meeting

- **Purpose**: 
  - Discuss all relevant components with the client before the penetration test.
  - Explain findings from the scoping questionnaire.
  - Information gathered will inform the **Penetration Testing Proposal** (Contract/SoW).
  
- **Format**: 
  - Conducted via email, online conference call, or in-person meeting.

- **Key Consideration**:
  - Some clients may be unfamiliar with penetration testing. Use part of the meeting to review the scoping questionnaire step-by-step if necessary.

### Contract - Checklist

| Checkpoint                    | Description                                                                                                                                                             |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ☐ NDA                         | Non-Disclosure Agreement ensuring confidentiality of information. Should be signed before detailed discussions.                                                         |
| ☐ Goals                       | Establish milestones to be achieved during the project, from significant goals to smaller objectives.                                                                   |
| ☐ Scope                       | Define components to be tested (e.g., domains, IPs, accounts) with legal authorization being the highest priority.                                                     |
| ☐ Penetration Testing Type    | Discuss and recommend types of tests (e.g., external/internal, vulnerability assessments) and justify recommendations.                                                 |
| ☐ Methodologies               | Specify methodologies to be used (e.g., OSSTMM, OWASP) for testing.                                                                                                   |
| ☐ Penetration Testing Locations| Define how testing will occur (remote/internal via VPN).                                                                                                             |
| ☐ Time Estimation             | Provide start and end dates for the test; clarify testing windows for attacks.                                                                                        |
| ☐ Third Parties               | Identify any third-party services involved; ensure written consent from these providers for simulated attacks.                                                          |
| ☐ Evasive Testing             | Discuss the use of evasive testing techniques if required by the client.                                                                                              |
| ☐ Risks                       | Inform client of risks and consequences; set limitations and precautions based on potential severity.                                                                  |
| ☐ Scope Limitations & Restrictions | Identify critical components to avoid impacting client operations.                                                                                               |
| ☐ Information Handling        | Ensure compliance with regulations (HIPAA, PCI, HITRUST, etc.).                                                                                                       |
| ☐ Contact Information         | Compile contact details for all involved parties, including escalation priority.                                                                                       |
| ☐ Lines of Communication      | Document communication channels (email, phone, in-person).                                                                                                           |
| ☐ Reporting                   | Outline report structure and any client-specific requirements.                                                                                                        |
| ☐ Payment Terms               | Explain pricing and terms of payment.                                                                                                                                  |

- **Focus**: 
  - Detailed presentation of the penetration test to prioritize client expectations.
  - Adjust testing to unique client infrastructure and goals.

### Rules of Engagement - Checklist

| Checkpoint                    | Contents                                                                                                                                                                 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ☐ Introduction                | Description of the document.                                                                                                                                          |
| ☐ Contractor                  | Company name, contractor's full name, and job title.                                                                                                                 |
| ☐ Penetration Testers         | Company name and names of penetration testers.                                                                                                                         |
| ☐ Contact Information          | Mailing addresses, emails, and phone numbers for all parties involved.                                                                                                 |
| ☐ Purpose                     | Description of the purpose of the penetration test.                                                                                                                   |
| ☐ Goals                       | Description of the goals of the penetration test.                                                                                                                     |
| ☐ Scope                       | All relevant IPs, domain names, URLs, or CIDR ranges included in testing.                                                                                             |
| ☐ Lines of Communication      | Specify methods for communication (e.g., conference calls, emails).                                                                                                   |
| ☐ Time Estimation             | Start and end dates for testing.                                                                                                                                      |
| ☐ Time of the Day to Test    | Designate specific times for testing activities.                                                                                                                       |
| ☐ Penetration Testing Type    | Specify type of tests (External/Internal/Vulnerability Assessments/Social Engineering).                                                                                |
| ☐ Penetration Testing Locations| Explain connection methods to the client’s network.                                                                                                                   |
| ☐ Methodologies               | List methodologies used (e.g., OSSTMM, PTES, OWASP).                                                                                                                  |
| ☐ Objectives / Flags          | Identify users, specific files, or information targeted.                                                                                                              |
| ☐ Evidence Handling           | Procedures for handling evidence (e.g., encryption, secure protocols).                                                                                                 |
| ☐ System Backups              | Identify what needs to be backed up (e.g., configuration files, databases).                                                                                            |
| ☐ Information Handling        | Ensure strong data encryption is used.                                                                                                                                 |
| ☐ Incident Handling and Reporting | Protocols for interruptions, including who to contact and types of reports.                                                                                       |
| ☐ Status Meetings             | Schedule for status meetings, including frequency and attendees.                                                                                                       |
| ☐ Reporting                   | Type of reports to be generated, target readers, and focus.                                                                                                           |
| ☐ Retesting                   | Establish start and end dates for retesting.                                                                                                                           |
| ☐ Disclaimers and Limitation of Liability | Outline system damage and data loss disclaimers.                                                                                                      |
| ☐ Permission to Test          | Confirm existence of a signed contract/contractor's agreement.                                                                                                         |

### Kick-Off Meeting

- **Purpose**: 
  - Held after all contracts are signed, involving all relevant parties (client POCs, technical support staff, penetration testing team).
  
- **Content**:
  - Discuss the nature of the penetration test and outline procedures.
  - Emphasize the absence of Denial of Service (DoS) testing.
  - Communicate the protocol for reporting critical vulnerabilities.
  - Discuss potential risks (log entries, account lockouts) and ensure clients understand their responsibilities.

### Contractor's Agreement (Physical Assessments)

- **Purpose**: 
  - Required for physical penetration tests due to different legal implications.
  
- **Checklist**:
  - Similar to the standard contractor agreement but includes specifics about physical locations and addresses.

### Setting Up

- **Post-Preparation**:
  - After addressing all points, prepare tools and systems for the penetration test.
  - Focus on configuring VMs, VPS, and other necessary systems for various scenarios.
  
## Questions
- How many documents must be prepared in total for a penetration test?
	- 7