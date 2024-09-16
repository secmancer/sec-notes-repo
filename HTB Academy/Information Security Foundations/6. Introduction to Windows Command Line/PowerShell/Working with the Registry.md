The Registry is a hierarchical database (tree structure) that stores essential information required by the operating system and installed software.
- It contains **keys** and **values**, which hold settings, installation directories, and configuration options.
- As Pentesters, the Registry is crucial for gathering information and planting persistence mechanisms. Attackers can exploit registry hives to maintain access to a host.


#### Keys in the Registry:
- **Keys** act as containers, representing specific system components.
- Keys can contain **sub-keys** and **values**.
- The names of keys are alphanumeric and case-insensitive.
- Keys are visually similar to folders, where each key can have its own sub-tree.
- Example: Keys are highlighted visually in registry management tools to show their hierarchical structure.



#### Registry Key Files:
- **Registry keys** are stored as files on the system and can be found in the `C:\Windows\System32\Config\` directory.
- These files include:
    - **BBI**
    - **COMPONENTS**
    - **DEFAULT**
    - **DRIVERS**
    - **SAM**
    - **SECURITY**
    - **SOFTWARE**
    - **SYSTEM**
    - Supporting directories, such as `Journal`, `RegBack`, and others, contain backups and configuration files.



#### Values in the Registry:
- **Values** are data objects stored within keys.
- Each value has:
    - A **name**
    - A **type specification**
    - The associated **data** for that value
- Values define specific parameters or configurations for the key they belong to.
- In the registry tree, values are represented as data stored inside a key.




**Values in the Registry**
- **Values** are data objects stored within **keys** in the Windows Registry.
- Each **value** has the following components:
    - **Name**: Identifies the value within the key.
    - **Type specification**: Defines the type of data stored (e.g., string, binary, or DWORD).
    - **Associated data**: The actual data or configuration settings linked to the value.
- Values specify parameters or configurations for the key they are associated with.
- In the Registry tree, values are visually represented as data objects stored inside the corresponding key.

![[Screenshot_20240916_074545.png]]




The **Registry** contains a wealth of information useful for pentesters, including:
- Installed software details
- Current OS revision
- Security settings
- Control of security tools like Microsoft Defender
- While this information can be found elsewhere, the Registry provides a **centralized source** for accessing and modifying system-wide settings.
- From an **offensive perspective**, the Registry is difficult for defenders to monitor:
    - The Registry hives are vast, containing hundreds of entries, making detection of specific changes challenging.
    - Defenders can struggle to track minor changes unless they maintain **solid backups** of their configurations.
- Having a good understanding of the Registry can help:
    - **Pentesters** act quickly by targeting specific keys and values.
    - **Defenders** detect and resolve issues more efficiently.



### Accessing the Information
- **Command-line interface (CLI) tools** to access and manage the Registry include:
    - **reg.exe**: A DOS executable designed for managing Registry settings.
    - **PowerShell cmdlets**:
        - **Get-Item** and **Get-ItemProperty**: Used to read Registry keys and values.
        - **New-ItemProperty**: Used to create or modify Registry values.




### Querying Registry Entries
#### Using `Get-Item`
- **Command**: `Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Select-Object -ExpandProperty Property`
- **Output**:
    - Displays the names of the services/applications currently running from the specified registry path.
    - Example output:
        - SecurityHealth
        - Acrobat Assistant 8.0
        - Focusrite Notifier
        - (default)


#### Using `Get-ChildItem` for Recursive Search
- **Command**: `Get-ChildItem -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Recurse`
- **Purpose**:
    - Lists all keys and associated values within a registry hive, providing a more detailed view.
    - Example output (partial):
        - 7zFM.exe
            - `(default)`: `C:\Program Files\7-Zip\7zFM.exe`
        - Acrobat.exe
            - `(default)`: `C:\Program Files\Adobe\Acrobat DC\Acrobat\Acrobat.exe`



#### Using `Get-ItemProperty` for Readable Output
- **Command**: `Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
- **Output**:
    - Displays a more detailed and readable format of registry entries, including the paths used to execute services/applications at user login.
    - Example output:
        - SecurityHealth: `C:\Windows\system32\SecurityHealthSystray.exe`
        - LogiOptions: `C:\Program Files\Logitech\LogiOptions\LogiOptions.exe`



#### Using `Reg.exe` for Querying
- **Command**: `reg query HKEY_LOCAL_MACHINE\SOFTWARE\7-Zip`
- **Output**:
    - Queries specific registry keys and displays their associated values, including the ValueType (e.g., `REG_SZ` for strings).
    - Example output:
        - Path64: `C:\Program Files\7-Zip\`
        - Path: `C:\Program Files\7-Zip\`



#### Overview
- **Registry**: A vital part of Windows where configurations, passwords, and usernames are often stored.
- **Reg.exe**: A command-line tool to search, query, and modify the Registry, crucial for administrators and pentesters.



#### Searching with Reg Query
**Command Example**:  
`REG QUERY HKCU /F "password" /t REG_SZ /S /K`
- **Command Breakdown**:
    - `REG QUERY`: Calls the `Reg.exe` tool to query data in the registry.
    - `HKCU`: Specifies the path to search within the `HKEY_CURRENT_USER` hive.
    - `/f "password"`: Sets the pattern to search for, in this case, the word "password".
    - `/t REG_SZ`: Specifies the type of data to search (string type in this example).
    - `/s`: Recursively searches all subkeys and values.
    - `/k`: Limits the search to key names only.
- **Example Output**:
    - Searches for the term "Password" in key names, outputting results if found.
    - Useful for searching keywords like `username`, `credentials`, or `keys`.



#### Creating and Modifying Registry Keys & Values
**Scenario**:
- Persistence through the `RunOnce` hive by adding a key that executes a payload upon user login.
**Creating a Registry Key**:  
`New-Item -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ -Name TestKey`
- **Explanation**:
    - Creates a new key `TestKey` in the `RunOnce` directory.
    - The `-Path` parameter ensures you can work from any directory by specifying the absolute path.
**Setting a Property**:  
`New-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\TestKey -Name "access" -PropertyType String -Value "C:\Users\htb-student\Downloads\payload.exe"`
- **Explanation**:
    - Adds a value to `TestKey` named `access` with a string that points to an executable payload.
    - This sets up the payload to run the next time the user logs in, useful for persistence.
**Alternative with Reg.exe**:  
`reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce\TestKey" /v access /t REG_SZ /d "C:\Users\htb-student\Downloads\payload.exe"`




#### Deleting Registry Properties
**Command**:  
`Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\TestKey -Name "access"`
- **Explanation**:
    - Safely removes the `access` property from the `TestKey`.
    - Always exercise caution when deleting registry values as improper removal can affect system functionality.


## Questions
- A registry entry is made up of two pieces, a 'Key' and ' ' . What is the second piece?
	- Values
- What is the abbreviation for " HKey_Current_User".
	- HKCU
- Take some time to practice adding and modifying the registry. Use the target host as a testbed and type "COMPLETE" as the answer below when you are done.
	- COMPLETE

