### Descriptive Analysis

Descriptive analysis is the initial step, focusing on defining the problem and setting the scope of the investigation. This involves:

- **Identifying the issue**: Determine whether it's a suspected breach, a networking issue, or something else.
- **Defining the scope and goal**: Establish what you're looking for and over what time period.
    - Example: Multiple hosts potentially downloading a malicious file (`superbad.exe` or `new-crypto-miner.exe`) from `bad.example.com` within the last 48 hours.
- **Target identification**: Specify the networks, hosts, and protocols involved (e.g., 192.168.100.0/24 network, HTTP, and FTP).
- **Understanding descriptive analysis**: Helps in setting clear objectives and understanding the nature of the data before diving into deeper analysis.

### Diagnostic Analysis

This step involves capturing and analyzing network traffic to diagnose the issue. It includes:

- **Traffic capture**: Connect to the appropriate network segment to capture live traffic or retrieve historical data from sources like SIEM.
- **Filtering traffic**: Exclude irrelevant data, focusing on the traffic related to the investigation (e.g., filtering for specific HTTP or FTP traffic related to the suspected files).
- **Analyzing the filtered data**: Investigate the remaining traffic to find evidence of the issue, such as identifying file transfers or suspicious GET requests.
- **Diagnostic analysis**: Provides insights into the root causes of the issue by examining network interactions and correlations.

### Predictive Analysis

Predictive analysis uses the data gathered from previous steps to forecast future events and inform decision-making:

- **Documentation**: Take detailed notes on timeframes, suspicious hosts, and relevant network conversations.
- **Summary of findings**: Clearly and concisely summarize the analysis to support decision-making, such as quarantining affected hosts.
- **Predictive analysis**: Helps in anticipating future occurrences by comparing findings against baseline data and known indicators of compromise.

### Prescriptive Analysis

In the prescriptive analysis, you decide on the actions to take based on the findings:

- **Actionable recommendations**: Based on the analysis, prescribe solutions to mitigate or prevent the problem (e.g., network reconfigurations, further investigations).
- **Reflection and lessons learned**: Document what worked, what didn't, and how the process can be improved for future incidents.
- **Prescriptive analysis**: Ensures that appropriate and informed actions are taken to resolve the issue and prevent recurrence.

### Key Components of an Effective Analysis

1. **Know your environment**: Understanding your network, including asset inventories and network maps, is crucial for identifying anomalies.
2. **Placement is key**: Position your capture tools as close to the source of the issue as possible to get accurate data.
3. **Persistence**: Some issues, like intermittent attacks, may require long-term monitoring and persistence to identify.

### Analysis Approach

The approach to analysis should start broad and then narrow down:

- **Start with standard protocols**: Examine common traffic (HTTP/S, FTP, etc.) and then move to more specific, organization-related protocols.
- **Look for patterns**: Identify recurring behaviors, such as hosts communicating with external servers at regular intervals.
- **Check host-to-host traffic**: Unusual internal communications may indicate lateral movement or other suspicious activities.
- **Identify unique events**: Spot deviations from normal patterns, such as unusual user-agent strings or rare port bindings.
- **Collaborate**: Don’t hesitate to seek help or a second opinion during the investigation to avoid missing critical details.