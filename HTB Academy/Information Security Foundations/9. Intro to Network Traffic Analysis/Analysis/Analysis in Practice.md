### Network Traffic Analysis Workflow
#### Overview
This section outlines the workflow for performing network traffic analysis, breaking down the process into key components. The analysis is not a strict loop but a dynamic process influenced by specific goals, visibility, and the nature of the issue.

### 1. Descriptive Analysis
- **Purpose**: Describe the dataset and detect potential errors or outliers.
- **Steps**:
    - **Identify the Issue**:
        - Determine if it is a suspected breach or networking issue.
    - **Define Scope and Goals**:
        - **Target**: Multiple hosts downloading a malicious file from `bad.example.com`.
        - **Timeframe**: Last 48 hours + 2 hours from now.
        - **Supporting Info**: Filenames/types such as `superbad.exe`, `new-crypto-miner.exe`.
    - **Define Targets**:
        - **Scope**: Network `192.168.100.0/24`.
        - **Protocols**: HTTP, FTP.

### 2. Diagnostic Analysis
- **Purpose**: Clarify causes, effects, and interactions by analyzing correlations and interpreting data.
- **Steps**:
    - **Capture Network Traffic**:
        - Connect to the `192.168.100.0/24` network to capture live traffic.
        - Retrieve PCAP and/or netflow data from SIEM if available.
    - **Identify Required Traffic Components**:
        - Filter out irrelevant packets; focus on HTTP and FTP traffic related to the suspect files.
    - **Understand Captured Traffic**:
        - Filter on relevant data (e.g., `ftp-data` for file transfers, `http.request.method == "GET"` for requests matching filenames).

### 3. Predictive Analysis
- **Purpose**: Use historical and current data to predict future occurrences and detect trends.
- **Steps**:
    - **Note-taking and Mind Mapping**:
        - Document everything: timeframes, suspicious hosts, file conversations (include timestamps and packet numbers).
    - **Summarize Analysis**:
        - Provide a clear summary of findings for decision-making.

### 4. Prescriptive Analysis
- **Purpose**: Determine actions to solve or prevent issues based on analysis results.
- **Steps**:
    - **Define Actions**:
        - Develop solutions and prevention strategies.
    - **Reflection and Lessons Learned**:
        - Document what was done correctly and areas for improvement.

### Key Components of Effective Analysis
1. **Know Your Environment**:
    - Maintain asset inventories and network maps to identify rogue hosts and understand the environment.
2. **Placement is Key**:
    - Place capture tools close to the source of the issue for the best visibility.
3. **Persistence**:
    - Issues may not always be frequent; persistent monitoring is crucial.

### Analysis Approach
- **Start with Standard Protocols**:
    - Focus on common protocols like HTTP/S, FTP, email, and basic TCP/UDP traffic before delving into more specific protocols.
- **Look for Patterns**:
    - Identify regular patterns or deviations, such as hosts checking in with external servers at specific intervals.
- **Check Host-to-Host Traffic**:
    - Be cautious of unusual internal traffic patterns.
- **Identify Unique Events**:
    - Look for anomalies, such as unusual port bindings or different User-Agent strings.
- **Seek Help**:
    - Collaborate with others to gain additional perspectives.