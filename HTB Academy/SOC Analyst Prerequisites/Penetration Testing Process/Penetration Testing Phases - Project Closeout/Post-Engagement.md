Much like there is considerable legwork before an engagement officially starts (when testing begins), we must perform many activities (many of them contractually binding) after our scans, exploitation, lateral movement, and post-exploitation activities are complete. No two engagements are the same, so these activities may differ slightly but generally must be performed to close out an engagement fully.

![[0-PT-Process_png 2.png]]

### Cleanup Phase

- **Objective**: Remove all tools, scripts, and any changes made during testing, and document any artifacts or configurations that were altered.
  - **Actions**:
    - **Delete tools/scripts** uploaded to target systems.
    - **Revert configuration changes** (e.g., removing accounts, restoring settings).
    - If access is lost to a system where cleanup is needed, **alert the client** and list the artifacts in the report appendices.
  
- **Documentation**: Record any actions taken (e.g., added admin accounts) in the report, even if they were reverted, to ensure the client is aware and can follow up on alerts.

---

### Documentation and Reporting

- **Before Ending Testing**: Ensure complete documentation of findings and steps taken during the assessment.
  - **Include**:
    - Command outputs, screenshots, affected hosts.
    - **Scan and log outputs** from client-hosted environments (e.g., internal VMs).
    - **No retention** of Personal Identifiable Information (PII) or sensitive data found during testing.

- **Report Deliverable**:
  - **Components**:
    1. **Attack chain**: Steps taken to achieve compromise.
    2. **Executive summary**: Simplified overview for non-technical audiences.
    3. **Detailed findings**:
       - **Risk rating**, impact, remediation recommendations, and external references.
       - Steps to **reproduce findings** for remediation teams.
    4. **Recommendations**:
       - Short, medium, and long-term suggestions tailored to the client's environment.
    5. **Appendices**:
       - Target scope, OSINT data, compromised accounts/hosts, port and service scans, password cracking analysis, Active Directory analysis, system modifications, etc.

- **Draft Report**: Delivered for client review, allowing them to request clarifications or modifications before issuing the final version.

---

### Report Review Meeting

- **Purpose**: Walk the client through the assessment findings.
  - **Structure**:
    - Briefly discuss each major finding (without reading the entire report).
    - Client may bring subject matter experts (SMEs) for technical issues or specific systems.
    - Focus on addressing **client questions** and **clarifying findings**.

- **Client Feedback**: The client reviews the draft, provides feedback, and may ask for changes or additional evidence.

---

### Deliverable Acceptance

- **Draft Report Review**: The report is marked as "DRAFT" until the client has reviewed and accepted it.
  - Once the feedback is addressed, issue a **FINAL version** of the report.
  - Some organizations, particularly those under regulatory compliance (e.g., audit firms), will not accept a report marked as "DRAFT."

---

### Post-Remediation Testing

- **Objective**: Verify the effectiveness of the client's remediation efforts.
  - **Review client-provided evidence** of remediation and re-test each issue to ensure it has been resolved.

- **Post-Remediation Report**: Clearly shows the status of each finding after remediation.
  - **Example Table**:

| #  | Severity | Finding Title                         | Status         |
|----|----------|---------------------------------------|----------------|
| 1  | High     | SQL Injection                         | Remediated     |
| 2  | High     | Broken Authentication                 | Remediated     |
| 3  | High     | Unrestricted File Upload              | Remediated     |
| 4  | High     | Inadequate Web and Egress Filtering   | Not Remediated |
| 5  | Medium   | SMB Signing Not Enabled               | Not Remediated |
| 6  | Low      | Directory Listing Enabled             | Not Remediated |

- **Evidence**: Include scan outputs or proof that the original exploitation techniques fail after remediation.

---

### Role of the Penetration Tester in Remediation

- **Impartial Role**: Penetration testers **do not perform remediation** on the findings.
  - Instead, they act as **trusted advisors**, providing general guidance on how to fix the issue.
  - Example: For SQL Injection, say "sanitize user input" but do **not provide specific code fixes**.

- **Objective**: Maintain the integrity of the assessment by avoiding conflicts of interest.

---

### Data Retention

- **Data Retention Guidelines**:
  - Retain evidence for a period (defined in the **Scope of Work** and **Rules of Engagement**) in case of questions or post-remediation retests.
  - **Best Practice** (per PCI DSS): Retain evidence for a specified time while adhering to any applicable laws.
  
- **Secure Storage**:
  - Client-specific data (e.g., scan results, logs, credentials) should be stored securely, encrypted at rest.
  - Data should be **wiped** from tester systems after the conclusion of the assessment.

- **Post-Engagement**: Any further testing or investigation should be performed in a **new virtual machine** specific to the client.

---

### Close-Out Phase

- **Final Steps**:
  - Deliver the final report, assist with questions, and perform post-remediation testing if included.
  - Wipe or destroy any systems used for testing, and securely store artifacts per company policy and client agreements.
  
- **Invoicing & Follow-Up**: 
  - Send the client the invoice for services rendered.
  - Consider conducting a **client satisfaction survey** to gather feedback on what went well and where improvements can be made.

- **Post-Engagement Reflection**: 
  - **Self-reflection** on the engagement can help improve **technical skills** and **soft skills**.
  - The client will often remember the **quality of interactions** and communication more than the technical intricacies, making it essential to focus on overall professionalism during the assessment.


## Questions
- What designation do we typically give a report when it is first delivered to a client for a chance to review and comment? (One word)
	- Draft