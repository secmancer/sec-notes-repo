### Differences Between PowerShell and CMD

|Feature|CMD (Command Prompt)|PowerShell|
|---|---|---|
|**Command Language**|Legacy command language|Advanced scripting language|
|**Scripting Capability**|Limited scripting support|Extensive scripting and automation|
|**Command Syntax**|Simple and basic syntax|More complex and versatile syntax|
|**Object Handling**|Text-based output only|Object-oriented output|
|**Pipelines**|Limited pipeline support|Full pipeline support for objects|
|**Cmdlets**|Not available|Supports cmdlets for various tasks|
|**Access to .NET Framework**|Limited access|Full access to .NET Framework|
|**Help System**|Basic help system with `help` command|Advanced help with `Get-Help` cmdlet|
|**Execution Policies**|Not applicable|Execution policies for security|
|**Remote Management**|Limited remote capabilities|Advanced remote management capabilities|
|**Integration with Windows Management Instrumentation (WMI)**|Basic integration|Deep integration with WMI|


### PowerShell Overview
- **Extensibility**: PowerShell is designed to be highly extensible, allowing integration with various tools and functionalities beyond its native capabilities.
- **Scripting Language**: Unlike CMD, PowerShell is not just a command-line interface (CLI); it is also a full-fledged scripting language, offering advanced scripting features.
- **Cross-Platform**: Originally exclusive to Windows, PowerShell is now an open-source project. It has been extended to support Linux-based systems, enhancing its versatility and cross-platform capabilities.
- **Object-Based Interaction**: PowerShell leverages the .NET framework, enabling an object-oriented approach to interaction and output. This contrasts with CMD’s text-based approach, allowing for more sophisticated data manipulation and handling.


**Importance for IT and Infosec Professionals**:
- **IT Administrators**:
    - **Automation**: PowerShell is widely used by IT admins for automating tasks, which helps manage large Windows environments efficiently.
    - **Tasks**:
        - Provisioning servers and installing roles.
        - Managing Active Directory (AD) user accounts and permissions.
        - Handling file share permissions.
        - Interacting with Azure AD and Azure VMs.
        - Monitoring and managing directories and files.
        - Setting up Microsoft Exchange email inboxes.


 **Penetration Testers**:
    - **Capabilities**: PowerShell offers extensive built-in functionalities that are useful for penetration testing, including the ability to import and use various modules.
    - **Tools**: Easy integration of custom tools and scripts within the PowerShell environment.


**Defenders**:
- **Security**: PowerShell provides robust security features and extensive logging, which can be leveraged for monitoring and defending against attacks.



**Comparison with CMD**:
- **Expandability**: PowerShell is designed to be expandable, supporting a wide range of functionalities beyond CMD's capabilities.
- **Automation and Scripting**: It supports advanced scripting and automation, making it ideal for repetitive or complex tasks.
- **Security**: PowerShell offers more robust security features compared to CMD. It has a more comprehensive logging and history capability, which can be both beneficial and a concern depending on the context.
- **Stealth**: From a stealth perspective, PowerShell's extensive logging might expose more of your interactions with the host. In scenarios where stealth is crucial, CMD might be preferable.


### Calling PowerShell
**Access Methods**:
1. **Using Windows Search**:
    - **How**: Type "PowerShell" into the Windows Search bar.
    - **Purpose**: Quickly locate and launch the PowerShell application and command console.
2. **Using the Windows Terminal Application**:
    - **Description**: A modern terminal emulator developed by Microsoft.
    - **Features**: Allows access to multiple command-line interfaces, systems, and sub-systems within a single application.
    - **Future**: Likely to become the default terminal emulator on Windows operating systems.
    - **Usage**: Open PowerShell from within Windows Terminal for an integrated command-line experience.
3. **Using Windows PowerShell ISE**:
    - **Description**: An Integrated Scripting Environment for PowerShell.
    - **Features**: Provides an IDE-like environment to develop, debug, and test PowerShell scripts.
    - **Benefits**: Useful for script development and learning PowerShell with its enhanced features for editing and debugging.
4. **Using PowerShell in CMD**:
    - **How**: Launch PowerShell from within the Command Prompt (CMD).
    - **Purpose**: Useful when you have access to CMD on a vulnerable Windows target and need to leverage PowerShell for further access or network operations.


### Taking a Look at the Shell
**PowerShell Prompt**:
- **Example**:
```
PS C:\Users\htb-student> ipconfig
```
- **Components**:
	- **PS**: Indicates PowerShell.
	- **C:\Users\htb-student>**: Current working directory.
	- **ipconfig**: The cmdlet or command being executed.
	- **Output**: Results of the command execution.

**Differences from CMD**:
- The prompt structure in PowerShell is similar to CMD, but PowerShell commands (cmdlets) and functionalities extend beyond what CMD offers.
- PowerShell can execute most CMD commands, but provides additional cmdlets and scripting capabilities.


**Getting Help in PowerShell**:
1. **Using `Get-Help`**:
    - **Purpose**: Provides details on cmdlets, including syntax, parameters, and usage.
    - **Example**:
```
PS C:\Users\htb-student> Get-Help Test-WSMan
```
- **Output**:
	- **NAME**: Name of the cmdlet.
	- **SYNTAX**: Options and keywords for the cmdlet.
	- **ALIASES**: Shorter names for the cmdlet.
	- **REMARKS**: Additional information and options.
	- **Online Help**: Provides a link to online documentation.


**Using `Update-Help`**:
- **Purpose**: Updates the local help files to ensure they are current.
- **Example**:
```
PS C:\Windows\system32> Update-Help
```


**Getting Updated Help**:
- **After Running `Update-Help`**:
```
PS C:\Windows\system32> Get-Help Test-WSMan
```
- **Additional Information**:
	- **SYNOPSIS**: Brief description of the cmdlet’s purpose.
	- **DESCRIPTION**: Detailed explanation of the cmdlet’s functionality.
	- **RELATED LINKS**: Links to related cmdlets and online resources.
	- **REMARKS**: Further guidance on using the cmdlet, including examples and detailed help.


**Basic Navigation and Usage**:
1. **Current Working Directory**:
    - **Command**: `Get-Location`
    - **Purpose**: Displays the current directory path.
    - **Example**:
```
PS C:\htb> Get-Location

Path
----
C:\Users\DLarusso
```
2. **Listing Directory Contents**:
	- **Command**: `Get-ChildItem`
	- **Purpose**: Lists all items (files and directories) in the current directory or a specified one.
	- **Example**:
```
PS C:\htb> Get-ChildItem

Directory: C:\Users\DLarusso

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10/26/2021  10:26 PM                .ssh
d-----         1/28/2021   7:05 PM                .vscode
d-r---         1/27/2021   2:44 PM                3D Objects
d-r---         1/27/2021   2:44 PM                Contacts
d-r---         9/18/2022  12:35 PM                Desktop
d-r---         9/18/2022   1:01 PM                Documents
d-r---         9/26/2022  12:27 PM                Downloads
d-r---         1/27/2021   2:44 PM                Favorites
d-r---         1/27/2021   2:44 PM                Music
dar--l         9/26/2022  12:03 PM                OneDrive
d-r---         5/22/2022   2:00 PM                Pictures
```
3. **Changing Directory**:
	- **Command**: `Set-Location`
	- **Purpose**: Changes the current directory to a new location.
	- **Examples**:
```
PS C:\htb> Set-Location .\Documents\

PS C:\Users\DLarusso\Documents> Get-Location

Path
----
C:\Users\DLarusso\Documents

```

```
PS C:\htb> Set-Location C:\Users\DLarusso\Documents
```
4. **Viewing File Contents**:
	- **Command**: `Get-Content`
	- **Purpose**: Displays the contents of a file.
	- **Example**:
```
PS C:\htb> Get-Content Readme.md

# ![logo][] PowerShell

Welcome to the PowerShell GitHub Community!
PowerShell Core is a cross-platform (Windows, Linux, and macOS) automation and configuration tool/framework that works well with your existing tools and is optimized
for dealing with structured data (e.g., JSON, CSV, XML, etc.), REST APIs, and object models.
It includes a command-line shell, an associated scripting language and a framework for processing cmdlets.

<SNIP>
```



**Finding Commands with `Get-Command`**:
- **Purpose**: Helps find commands that may not be immediately remembered.

**Basic Usage**:
```
**List All Commands**:
PS C:\htb> Get-Command

**Filter by Verb**:
PS C:\htb> Get-Command -verb get


_Alternative_: Use wildcard `get*`:
PS C:\htb> Get-Command get*

**Filter by Noun**:
PS C:\htb> Get-Command -noun windows*
```

**Example Output**:
- Lists cmdlets, aliases, and functions that match the search criteria.


**Command History with `Get-History`**:
- **Purpose**: View commands run in the current session.
**Basic Usage**:
```
PS C:\htb> Get-History
```
**Re-run Commands**:
- Use alias `r` followed by the command ID:
```
PS C:\htb> r 14
```
**Persistent History with PSReadLine**:
- **View History File**:
```
PS C:\htb> Get-Content C:\Users\DLarusso\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```
- **Automatic Filtering**: PSReadLine filters sensitive information such as passwords, tokens, and API keys.

**Clearing the Screen**:
- **Purpose**: Remove all output from the console for a cleaner view.
- **Commands**:
- **Full Command**:
```
Clear-Host
```
- **Aliases**
```
clear
cls
```


When working in a CLI environment, especially during tasks like pentesting, using hotkeys efficiently can greatly enhance productivity. Here are some useful hotkeys for PowerShell:

**Hotkeys**
- **CTRL+R**: Searchable history. Start typing after pressing this to see results that match previous commands.
- **CTRL+L**: Quickly clears the screen.
- **CTRL+ALT+Shift+?**: Displays the entire list of keyboard shortcuts recognized by PowerShell.
- **Escape**: Clears the entire line being typed, instead of holding backspace.
- **↑ (Up Arrow)**: Scrolls up through previous commands in the history.
- **↓ (Down Arrow)**: Scrolls down through previous commands in the history.
- **F7**: Opens a TUI (Text User Interface) with a scrollable interactive history of the current session.

![[Screenshot_20240915_203349.png]]


**Tab Completion**
Tab completion is a powerful feature in PowerShell that helps speed up command input and reduces errors by suggesting and completing command names and parameters as you type. Here’s how to use it:
- **Tab**: Pressing the Tab key will auto-complete the command or parameter based on the current context.
- **SHIFT+Tab**: Use this combination to cycle backwards through possible completions.

**Autocomplete Example**
- As you type a command, pressing Tab will cycle through available options or complete the command for you.



**Aliases**
Aliases in PowerShell are shorthand names for cmdlets, commands, or executable files, making them quicker and easier to use. Here’s how to work with aliases:
- **Get-Alias**: Lists all the default aliases available.
```
PS C:\Windows\system32> Get-Alias
```
**Sample Output:**
```
CommandType     Name                                               Version    Source
-----------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           clear -> Clear-Host
Alias           cls -> Clear-Host
Alias           del -> Remove-Item
Alias           dir -> Get-ChildItem
```
- **Set-Alias**: Creates a custom alias for a cmdlet.
```
PS C:\Windows\system32> Set-Alias -Name gh -Value Get-Help
```
This command sets `gh` as an alias for `Get-Help`.


**Helpful Aliases**
- `%` for `ForEach-Object`
- `?` for `Where-Object`
- `ac` for `Add-Content`
- `cat` for `Get-Content`
- `cd` for `Set-Location`
- `clear` for `Clear-Host`
- `cls` for `Clear-Host`
- `del` for `Remove-Item`
- `dir` for `Get-ChildItem`

![[Screenshot_20240915_203547.png]]



**Comparison with BASH**
- Many PowerShell aliases are similar to commands widely used in BASH (Linux distributions).
- This similarity can ease the transition for those familiar with BASH, as they might find equivalent commands and aliases in PowerShell that match their BASH counterparts.



**Next Steps**
- This section provided a comprehensive overview of essential PowerShell functionalities, including tab completion and aliases.
- The next focus will be on exploring **PowerShell modules and cmdlets** in greater detail to enhance PowerShell proficiency.


## Questions
- What command string can we use to view the help documentation for the command Get-Location? (full string)
	- Get-Help Get-Location
- What command can we use to show us our current location on the host system?
	- Get-Location
- What hotkey can be used to clear our input line completely?
	- ESCAPE