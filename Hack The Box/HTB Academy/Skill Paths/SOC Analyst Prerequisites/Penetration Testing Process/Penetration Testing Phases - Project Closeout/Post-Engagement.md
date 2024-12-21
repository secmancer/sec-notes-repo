### Introduction
- Much like there is considerable legwork before an engagement officially starts (when testing begins), we must perform many activities (many of them contractually binding) after our scans, exploitation, lateral movement, and post-exploitation activities are complete. 
- No two engagements are the same, so these activities may differ slightly but generally must be performed to close out an engagement fully.
![](https://academy.hackthebox.com/storage/modules/90/0-PT-Process.png)



### Cleanup
- Once testing is complete, we should perform any necessary cleanup, such as deleting tools/scripts uploaded to target systems, reverting any (minor) configuration changes we may have made, etc. 
- We should have detailed notes of all of our activities, making any cleanup activities easy and efficient.
- If we cannot access a system where an artifact needs to be deleted, or another change reverted, we should alert the client and list these issues in the report appendices.
- Even if we can remove any uploaded files and revert changes (such as adding a local admin account), we should document these changes in our report appendices in case the client receives alerts that they need to follow up on and confirm that the activity in question was part of our sanctioned testing.



### Documentation and Reporting
- **Pre-report Documentation**
    - Ensure all findings are documented, including command output, screenshots, affected hosts, and relevant client data.
    - Retrieve all scan and log output, especially for internal penetration tests using client-hosted VMs.
    - Do not retain Personal Identifiable Information (PII) or sensitive data encountered during testing.
- **Report Deliverable Requirements**
    - Include an attack chain, executive summary, detailed findings, remediation recommendations, and steps to reproduce each finding.
    - Provide tailored recommendations (near, medium, long-term) and appendices containing relevant supporting information (e.g., OSINT, password cracking, compromised accounts).
- **Draft Report and Client Review**
    - Create a draft report as the first deliverable for client feedback, allowing for clarification and modifications before finalizing.



### Report Review Meeting
- Once the draft report is delivered, and the client has had a chance to distribute it internally and review it in-depth, it is customary to hold a report review meeting to walk through the assessment results. 
- The report review meeting typically includes the same folks from the client and the firm performing the assessment. 
- Depending on the types of findings, the client may bring in additional technical subject matter experts if the finding is related to a system or application they are responsible for. 
- Typically we will not read the entire report word for word but walk through each finding briefly and give an explanation from our own perspective/experience. 
- The client will have the opportunity to ask questions about anything in the report, ask for clarifications, or point out issues that need to be corrected. 
- Often the client will come with a list of questions about specific findings and will not want to cover every finding in detail (such as low-risk ones).



### Deliverable Acceptance
- The Scope of Work should clearly define the acceptance of any project deliverables. 
- In penetration test assessments, generally, we deliver a report marked `DRAFT` and give the client a chance to review and comment. 
- Once the client has submitted feedback (i.e., management responses, requests for clarification/changes, additional evidence, etc.) either by email or (ideally) during a report review meeting, we can issue them a new version of the report marked `FINAL`. 
- Some audit firms that clients may be beholden to will not accept a penetration test report with a `DRAFT` designation. 
- Other companies will not care, but keeping a uniform approach across all customers is best.



### Post-Remediation Testing
- Most engagements include post-remediation testing as part of the project's total cost. 
- In this phase, we will review any documentation provided by the client showing evidence of remediation or just a list of remediated findings. 
- We will need to reaccess the target environment and test each issue to ensure it was appropriately remediated. 
- We will issue a post-remediation report that clearly shows the state of the environment before and after post-remediation testing.

| # | Finding Severity | Finding Title | Status |
| --- | --- | --- | --- |
| 1 | High | SQL Injection | Remediated |
| 2 | High | Broken Authentication | Remediated |
| 3 | High | Unrestricted File Upload | Remediated |
| 4 | High | Inadequate Web and Egress Filtering | Not Remediated |
| 5 | Medium | SMB Signing Not Enabled | Not Remediated |
| 6 | Low | Directory Listing Enabled | Not Remediated |

- For each finding (where possible), we will want to show evidence that the issue is no longer present in the environment through scan output or proof that the original exploitation techniques fail.



### Role of the Pentester in Remediation
- **Impartiality in Penetration Testing**
    - Penetration testers must remain impartial and not perform remediation tasks (e.g., fixing code, patching systems, or making configuration changes).
    - Act as trusted advisors by providing general remediation advice or explaining findings, but do not implement changes or offer precise remediation solutions.
    - This approach ensures the integrity of the assessment and prevents conflicts of interest.



### Data Retention
- After a penetration test, retain client-specific data (scan results, logs, credentials, screenshots, etc.) as per the contract's Scope of Work and Rules of Engagement.
- The **PCI DSS** recommends retaining evidence for a certain period, considering local laws and regulations.
- Evidence should be securely stored, encrypted, and wiped from tester systems after the assessment.
- Retained data may be used for post-remediation testing or to assist with any follow-up client inquiries, using a new VM for such activities.



### Close Out
- Once we have delivered the final report, assisted the client with questions regarding remediation, and performed post-remediation testing/issued a new report, we can finally close the project. 
- At this stage, we should ensure that any systems used to connect to the client's systems or process data have been wiped or destroyed and that any artifacts leftover from the engagement are stored securely (encrypted) per our firm's policy and per contractual obligations to our client.
- The final steps would be invoicing the client and collecting payment for services rendered. 
- Finally, it is always good to follow up with a post-assessment client satisfaction survey so the team and management, in particular, can see what went well during the engagement and what could be improved upon from a company process standpoint and the individual consultant assigned to the project.
- Discussions for follow-on work may arise in the weeks or months after if the client was pleased with our work and day-to-day interactions.
- As we continually grow our technical skillset, we should always look for ways to improve our soft skills and become more well-rounded professional consultants. 
- In the end, the `client will usually remember interactions` during the assessment, communication, and how they were treated/valued by the firm they engage, `not the fancy exploit chain the pentester pulled off to pwn their systems`.
- Take this time to self-reflect and work on continuous improvement in all aspects of your role as a professional penetration tester.



### Questions
- What designation do we typically give a report when it is first delivered to a client for a chance to review and comment? (One word)
	- Draft