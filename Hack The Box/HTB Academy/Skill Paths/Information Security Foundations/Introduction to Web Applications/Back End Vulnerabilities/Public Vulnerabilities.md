### Introduction
- Critical back-end component vulnerabilities are those exploitable externally, potentially allowing attackers to take control of the server during external penetration testing.
- These vulnerabilities often stem from coding errors in the web application's back-end development.
- They vary widely in complexity, ranging from simple, easily exploited issues to advanced vulnerabilities requiring extensive knowledge of the web application.



### Public CVE
- Public web applications, both open-source and proprietary, are frequently tested by experts, leading to vulnerabilities being patched, shared publicly, and assigned CVEs.
- Penetration testers often create and share proof-of-concept exploits for testing and educational purposes, making the search for public exploits the first step in testing web applications.
- **Tip**: Identify the version of the web application (e.g., from source code or version files) to search for corresponding public exploits.
- Use online exploit databases such as [Exploit DB](https://www.exploit-db.com/), [Rapid7 DB](https://www.rapid7.com/db/), or [Vulnerability Lab](https://www.vulnerability-lab.com/) to find exploits for the identified version.
- Prioritize CVE scores of 8-10 or exploits leading to Remote Code Execution; consider others if these are unavailable.
- Also, investigate vulnerabilities in external components (e.g., plugins) used by the web application.



### Common Vulnerability Scoring System (CVSS)
- The [Common Vulnerability Scoring System (CVSS)](https://en.wikipedia.org/wiki/Common_Vulnerability_Scoring_System) is an industry standard for assessing security vulnerability severity, aiding organizations in prioritizing resources and responding to threats.
- CVSS scores are calculated using `Base`, `Temporal`, and `Environmental` metrics, with `Base` scores ranging from 0 to 10. These are further refined by `Temporal` and `Environmental` metrics.
- The [National Vulnerability Database (NVD)](https://nvd.nist.gov/) provides CVSS scores for publicly disclosed vulnerabilities, focusing on `Base` scores.
- CVSS has two versions, v2 and v3, which differ in the metrics used, particularly in the `Base` and `Environmental` groups.
- For details on differences between CVSS v2 and v3, see [this resource](https://www.balbix.com/insights/cvss-v2-vs-cvss-v3).

| CVSS V2.0 Ratings |  |
| --- | --- |
| **Severity** | **Base Score Range** |
| Low | 0.0-3.9 |
| Medium | 4.0-6.9 |
| High | 7.0-10.0 |

| **CVSS V3.0 Ratings** |  |
| --- | --- |
| **Severity** | **Base Score Range** |
| None | 0.0 |
| Low | 0.1-3.9 |
| Medium | 4.0-6.9 |
| High | 7.0-8.9 |
| Critical | 9.0-10.0 |
- The NVD does not include `Temporal` and `Environmental` metrics in CVSS scores because `Temporal` metrics change over time due to external events, and `Environmental` metrics are organization-specific.
- The NVD provides interactive [CVSS v2](https://nvd.nist.gov/vuln-metrics/cvss/v2-calculator) and [CVSS v3](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) calculators for organizations to incorporate these additional metrics.
- These calculators allow fine-tuning of CVSS scores by exploring each metric and determining its applicability to a specific environment.
![image](https://academy.hackthebox.com/storage/modules/75/cvssv3_calc.png)
- Experiment with the CVSS calculator to understand how adjusting various metrics affects the final score.
- Review CVEs and attempt to match their CVSS scores using the calculator.
- Observe how applying `Temporal` and `Environmental` metrics changes the overall CVSS score.
- Refer to this [guide](https://www.first.org/cvss/user-guide) for a comprehensive understanding of CVSS v2 and v3 and guidance on using the calculators effectively.



### Back-end Server Vulnerabilities
- Beyond web applications, vulnerabilities in back-end components, such as back-end servers or web servers, should also be investigated.
- Web server vulnerabilities, like `Shell-Shock` (affecting Apache web servers before 2014 via `HTTP` requests), are critical due to their public accessibility over the `TCP` protocol.
- Back-end server and database vulnerabilities typically require local access, often gained through external vulnerabilities or internal penetration testing, and are used to escalate privileges or compromise other network servers.
- Even though these vulnerabilities may not be directly exploitable externally, they remain critical and must be patched to protect the entire web application.



### Questions
- What is the CVSS score of the public vulnerability CVE-2017-0144?
	- 9.3