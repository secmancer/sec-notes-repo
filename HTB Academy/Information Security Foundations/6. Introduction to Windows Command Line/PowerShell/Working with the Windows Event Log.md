**Importance**:
- Monitoring, collecting, and categorizing events across all machines in a network is critical for proactively detecting suspicious activity.
- Attackers can also use event logs to gain insight into the environment, hide their tracks, or disrupt information flow.
- Event logs can contain sensitive information such as credentials or help assess the level of logging in place (default or more granular).



### What is the Windows Event Log?
- **Event Definition**:
    - **Event**: Any identifiable action or occurrence triggered by hardware or software.
    - **Examples of Events**:
        - **User-Generated Events**: Mouse movement, keyboard usage, peripheral interactions.
        - **Application-Generated Events**: Software updates, crashes, memory consumption.
        - **System-Generated Events**: Uptime, updates, driver loading, user login.
- **Event Logging**:
    - Defined by Microsoft as a standardized, centralized way for the operating system and applications to log significant events.
    - **Event Logging** provides:
        - A method to handle, record, and categorize events from multiple sources (hardware, software, etc.).
        - A **standardized format** for event information.
- **How Events Are Managed**:
    - Windows uses the **Windows Event Log** service to manage and record events.
    - The Event Log also provides an **API** for applications to maintain and manage their logs.
    - The Event Log service is a core Windows service that starts at system initialization.




### Types of Events and Event Logs
- **Types of Events**:
    - **User-Generated**: Events triggered by user interaction with devices or peripherals.
    - **Application-Generated**: Events caused by software, such as crashes or updates.
    - **System-Generated**: Events triggered by system processes like logins, updates, or driver activity.
- **Elements of a Log**:
    - Logs contain detailed event information that is recorded in a structured format.
    - Each event includes:
        - **Source**: What triggered the event.
        - **Type**: Whether it was user, application, or system-generated.
        - **Details**: Information about the event, such as time, severity, and context.



### Interacting with Event Logs
#### 1. **Using `wevtutil`**
- `wevtutil` is a command-line tool for querying and managing event logs.
- It allows administrators to:
    - Query logs
    - Export logs
    - View or clear event logs


#### 2. **Using PowerShell Cmdlets**
- PowerShell offers more advanced interaction with event logs through cmdlets.
- Cmdlets allow for:
    - Querying specific logs and filtering results.
    - Exporting, clearing, and managing logs programmatically.


![[Screenshot_20240916_075410.png]]

![[Screenshot_20240916_075417.png]]

![[Screenshot_20240916_075424.png]]


### Elements of a Windows Event Log
- **Log Name**: Identifies the log where the event is recorded (e.g., system, security, applications).
- **Event Date/Time**: Timestamp of when the event occurred.
- **Task Category**: Classifies the type of event logged.
- **Event ID**: Unique identifier for each logged event, useful for system administrators.
- **Source**: Specifies where the log originated (e.g., program or software).
- **Level**: Severity of the event (e.g., information, warning, error, critical).
- **User**: Username of the person logged into the system during the event.
- **Computer**: The name of the computer where the event is logged.



### Windows Event Log Technical Details
- Managed by the **EventLog service**, which runs under `svchost.exe`.
- Starts automatically at system boot.
- Logs are stored in `C:\Windows\System32\winevt\logs` with a `.evtx` extension.




### Interacting with Windows Event Log
You can interact with the Event Log via:
1. **Event Viewer (GUI)**.
2. **Command-line tools**:
    - `wevtutil`: Manage event logs.
    - `Get-WinEvent`: PowerShell cmdlet to query logs locally or remotely.




### Common `wevtutil` Commands
- **`el`**: List all log names.
- **`gl`**: Get log configuration info.
- **`sl`**: Modify log configuration.
- **`qe`**: Query events from a log.
- **`epl`**: Export logs for offline processing.




**Listing All Logs**
- Use `Get-WinEvent` to list all event logs on the computer:
    - `Get-WinEvent -ListLog *`
    - Output includes details like log mode, maximum size, and record count for each log.
Example:
- PowerShell:
    - `PS C:\htb> Get-WinEvent -ListLog *`




**Viewing a Specific Log**
- To view details of a specific log, such as the Security log:
    - `Get-WinEvent -ListLog Security`
    - Shows size, record count, and log mode.




**Querying Recent Events**
- Retrieve the last 5 events from a specific log (e.g., Security):
    - `Get-WinEvent -LogName 'Security' -MaxEvents 5`
    - Reverse order using `-Oldest` to view oldest logs first.
Example:
- PowerShell:
    - `Get-WinEvent -LogName 'Security' -MaxEvents 5 | Select-Object -ExpandProperty Message`




**Filtering Events by ID**
- Focus on specific event types by filtering event IDs, e.g., logon failures (Event ID 4625):
    - `Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625'}`
Example:
- PowerShell:
    - `PS C:\htb> Get-WinEvent -FilterHashTable @{LogName='Security';ID='4625'}`




**Filtering by Event Level**
- Filter logs by information level (e.g., level 1 for critical events):
    - `Get-WinEvent -FilterHashTable @{LogName='System';Level='1'}`
    - Useful for identifying critical errors such as system reboots.
Example:
- PowerShell:
    - `PS C:\htb> Get-WinEvent -FilterHashTable @{LogName='System';Level='1'} | Select-Object -ExpandProperty Message`



**Overview of Windows Event Logs**
- Windows Event Log is a vast and critical topic.
- This section provided an introduction, but future modules will go into deeper details, including potential sensitive data discovery in logs (e.g., passwords).




**Importance of Familiarity**
- **For Penetration Testers:**
    - Windows Event Logs can provide insights into the environment.
    - Potentially sensitive data (e.g., passwords) can sometimes be extracted from logs.
- **For Blue Teamers:**
    - In-depth knowledge of Windows Event Logs is vital for setting up alerts and monitoring.




**Logging and Granularity**
- Windows generates a massive number of logs, making manual queries difficult.
- Logs can be granular; specific Event IDs can help pinpoint relevant information.




**SIEM Integration**
- Logs are most effective when forwarded to a **Security Information and Event Management (SIEM)** tool.
    - SIEMs can automate alerts for specific Event IDs (e.g., **Kerberoasting**, **Password Spraying**).
    - SIEMs enhance monitoring and detect suspicious activities.



## Questions
- Explore the targets provided and practice your Event Log PowerShell Kung-Fu. Type COMPLETE as the answer when finished.
	- COMPLETE