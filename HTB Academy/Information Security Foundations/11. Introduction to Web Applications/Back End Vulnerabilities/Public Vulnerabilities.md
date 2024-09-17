**Critical Back-End Vulnerabilities**
- **External vs. Local Access**: The most critical vulnerabilities are those that can be exploited externally to take control of the back-end server without needing local access. These are often due to coding mistakes in the web application's back-end components.
- **Variety of Vulnerabilities**: These can range from basic issues easily exploited to sophisticated ones requiring in-depth knowledge of the application.



**Public CVE**
- **Common Vulnerabilities and Exposures (CVE)**: Public vulnerabilities are often discovered and reported, leading to CVE records and scores. These are published to help organizations understand and address security risks.
- **Proof of Concept Exploits**: Penetration testers often create and share proof of concept exploits for public vulnerabilities, useful for testing and education.
- **Finding Public Exploits**:
    - **Identify Application Version**: Find the version of the web application (e.g., from the source code or a specific version page).
    - **Search for Exploits**: Look for public exploits for this version using databases like Exploit DB, Rapid7 DB, or Vulnerability Lab.
    - **Focus Areas**: Prioritize exploits with high CVE scores (8-10) or those leading to Remote Code Execution. Also consider other exploits if no high-severity ones are found.
- **External Components**: If the web application uses external components (e.g., plugins), search for vulnerabilities in these as well.



**Common Vulnerability Scoring System (CVSS)**
- **Purpose**: CVSS is used to assess the severity of security vulnerabilities and prioritize responses.
- **Scoring Metrics**:
    - **Base Metrics**: Reflect the inherent characteristics of the vulnerability, providing a score from 0 to 10.
    - **Temporal Metrics**: Reflect changes over time due to external factors.
    - **Environmental Metrics**: Reflect the potential impact on a specific organization.
- **CVSS Versions**:
    - **CVSS v2**:
        - Low: 0.0-3.9
        - Medium: 4.0-6.9
        - High: 7.0-10.0
    - **CVSS v3**:
        - None: 0.0
        - Low: 0.1-3.9
        - Medium: 4.0-6.9
        - High: 7.0-8.9
        - Critical: 9.0-10.0
- **NVD Scoring**: The National Vulnerability Database (NVD) provides Base scores but not Temporal and Environmental metrics. The CVSS calculators on the NVD site can help fine-tune scores based on additional risk factors.



**Back-End Server Vulnerabilities**
- **Web Servers**: Critical vulnerabilities often found in web servers (e.g., Shellshock in Apache) are publicly accessible and can be exploited remotely.
- **Database and Server Vulnerabilities**: These are typically exploited after gaining access to the back-end network. They can be used to escalate privileges or compromise other servers within the network.
- **Importance of Patching**: Even if not directly exploitable externally, these vulnerabilities are critical and need to be patched to protect the entire web application.


## Questions
- What is the CVSS score of the public vulnerability CVE-2017-0144?
	- 9.3