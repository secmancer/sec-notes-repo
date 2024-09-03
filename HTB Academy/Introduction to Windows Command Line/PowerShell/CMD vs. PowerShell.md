### Differences Between PowerShell and CMD

|**Feature**|**CMD**|**PowerShell**|
|---|---|---|
|**Language**|Batch and basic CMD commands only.|PowerShell can interpret Batch, CMD, PS cmdlets, and aliases.|
|**Command Utilization**|The output from one command cannot be passed into another directly.|The output from one command can be passed into another directly.|
|**Command Output**|Text only|PowerShell outputs in object formatting.|
|**Parallel Execution**|CMD must finish one command before running another.|PowerShell can multi-thread commands to run in parallel.|

---

### Why Choose PowerShell Over CMD?

PowerShell is prominent among IT and Infosec professionals for its extensive capabilities:

- **Automation**: Automate tasks such as provisioning servers, managing Active Directory, and interacting with Azure.
- **Extensibility**: PowerShell can handle tasks CMD cannot and is built for automation and scripting.
- **Security**: It offers a more robust security implementation.
- **Tool Integration**: PowerShell’s module import capability allows integration of various tools and functionalities.
- **Logging**: PowerShell logs more interactions, which can be useful for auditing but may affect stealth during penetration testing.

---

### Calling PowerShell

- **Using Windows Search**: Type "PowerShell" in Windows Search to find and launch it.
- **Using the Windows Terminal Application**: This application allows access to multiple command-line interfaces through one app.
- **Using Windows PowerShell ISE**: A tool like an IDE for developing, debugging, and testing PowerShell scripts.
- **Using PowerShell in CMD**: Launch PowerShell from within CMD, which can be useful for further access on a compromised host.

---

### PowerShell Prompt

The prompt in PowerShell is similar to CMD but includes "PS" to denote that you are in PowerShell. It also shows the current working directory and the command or string to be executed.

---

### Getting Help in PowerShell

- **Using Get-Help**: Provides detailed information about cmdlets, including options, syntax, and usage. To get more detailed help, use `Get-Help <cmdlet> -Detailed` or `Get-Help <cmdlet> -Full`. For online help, use `Get-Help <cmdlet> -Online`.
- **Using Update-Help**: Updates the help files for cmdlets to ensure the most up-to-date information is available.

---

### Basic Navigation in PowerShell

- **Get-Location**: Displays the current working directory.
- **Get-ChildItem**: Lists contents of the current or specified directory.
- **Set-Location**: Changes the current directory.
- **Get-Content**: Displays the contents of a file.

---

### Tips & Tricks for PowerShell Usage

- **Get-Command**: Finds commands, aliases, or functions. Use `Get-Command -Verb <verb>` or `Get-Command -Noun <noun>` to filter commands.
- **History**: PowerShell maintains command history within the session using `Get-History`. The PSReadLine module stores history across sessions in a file located at `$env:APPDATA\Microsoft\Windows\PowerShell\PSReadLine`.

### Questions
- What command string can we use to view the help documentation for the command Get-Location? (full string)
	- Get-Help Get-Location
- What command can we use to show us our current location on the host system?
	- Get-Location
- What hotkey can be used to clear our input line completely?
	- ESCAPE