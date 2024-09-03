### What Is The Windows Registry?

The Windows Registry is a hierarchical database that contains configuration settings and options for the operating system and installed applications. It consists of keys and values, organized into a tree-like structure.

- **Keys**: Act as containers within the Registry. They can contain other keys and values. Keys are named with alphanumeric characters and are not case-sensitive.
    
- **Values**: Contain data related to a specific key. Each value includes a name, a type specification, and the data it holds.
    

### Registry Hives

Registry hives are primary divisions within the Registry that store different types of information:

- **HKEY_LOCAL_MACHINE (HKLM)**: Contains information about the computer’s hardware and system settings.
- **HKEY_CURRENT_CONFIG (HKCC)**: Contains information about the hardware profile currently in use.
- **HKEY_CLASSES_ROOT (HKCR)**: Stores file type associations and UI extension settings.
- **HKEY_CURRENT_USER (HKCU)**: Stores settings for the currently logged-in user.
- **HKEY_USERS (HKU)**: Contains information about all user profiles on the computer.

### Accessing the Registry

To interact with the Registry from the command line, you can use:

- **Get-Item** and **Get-ItemProperty** in PowerShell to read keys and values.
- **Reg.exe** for querying and modifying registry entries.

For example:

- **Get-Item** retrieves the properties of a specified registry key.
- **Get-ItemProperty** provides detailed information about properties and their values.
- **Reg.exe query** allows you to search for specific values or data within the Registry.

### Creating and Modifying Registry Keys and Values

To create or modify registry entries:

- Use **New-Item** to create a new key.
- Use **New-ItemProperty** to set a new value within a key.

For example, to create a new key named "TestKey" under `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`:

- **New-Item** creates the key.
- **New-ItemProperty** adds a new value to this key, specifying the value name, type, and data.

### Searching the Registry

To search for specific terms within the Registry:

- Use **Reg.exe query** with options to specify the search path, search pattern, value type, and whether to search recursively.

For example, searching for "Password" in `HKEY_CURRENT_USER` will display entries containing that term.

### Questions
- A registry entry is made up of two pieces, a 'Key' and ' ' . What is the second piece?
	- Values
- What is the abbreviation for " HKey_Current_User"?
	- HKCU
- Take some time to practice adding and modifying the registry. Use the target host as a testbed and type "COMPLETE" as the answer below when you are done.
	- COMPLETE