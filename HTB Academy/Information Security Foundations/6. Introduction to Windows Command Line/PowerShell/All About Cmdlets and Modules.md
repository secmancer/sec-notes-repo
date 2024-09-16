#### Overview
In this section, we will explore:
- What cmdlets and modules are
- How to interact with them
- How to install and load new modules from the web
Understanding these concepts is essential for leveraging PowerShell effectively as both a sysadmin and a pentester. PowerShell's modularity and expandability make it a powerful tool in our toolkit. Let's dive into the details.


#### Cmdlets
**Definition:** A cmdlet is a single-function command in PowerShell that manipulates objects.

**Structure:** Cmdlets follow a `Verb-Noun` structure, making it easier to understand their function. For example, in `Test-WSMan`, "Test" is the verb, and "Wsman" is the noun. The verb and noun are separated by a dash (`-`). After specifying the verb and noun, additional options can be used to perform the desired action.

**Characteristics:**
- Cmdlets are not written in PowerShell but in C# or another language, then compiled.
- Use `Get-Command` to list available cmdlets, functions, and applications. The `CommandType` trait helps identify the type.
- Use `Get-Help` to view the options and functionality of a specific cmdlet.
- Use `Get-Member` to examine the properties and methods of objects returned by cmdlets.


#### PowerShell Modules
**Definition:** A PowerShell module is a structured collection of PowerShell code designed for ease of use and sharing.

**Components:** A module can include:
- Cmdlets
- Script files
- Functions
- Assemblies
- Related resources (manifests, help files)

**Example: PowerSploit Project**
- PowerSploit is a collection of PowerShell modules created by the PowerShellMafia for penetration testing of Windows Domain/Active Directory environments.
- **Note:** While the project has been archived, many tools within are still relevant and useful for pen-testing as of August 2022.

**Module Manifest (.psd1):**
- Contains metadata about the module.
- Includes:
    - Reference to the module
    - Version numbers
    - GUID
    - Author and copyright information
    - PowerShell compatibility
    - Modules and cmdlets included
    - Other metadata

**Script Module File (.psm1):**
- A script containing PowerShell code.
- Represents the core functionality of a module.

#### Example Usage with PowerSploit
**PowerSploit.psd1**

- Contains metadata and references related to the module.

**PowerSploit.psm1**
- Contains the PowerShell code for the module.

**Example Code:**
```
Get-ChildItem $PSScriptRoot | ? { $_.PSIsContainer -and !('Tests','docs' -contains $_.Name) } | % { Import-Module $_.FullName -DisableNameChecking }
```
- **Explanation:**
	- `Get-ChildItem $PSScriptRoot` retrieves items in the current directory.
	- `Where-Object` (aliased as `?`) filters out non-folder items and folders named "Tests" or "docs".
	- `ForEach-Object` (aliased as `%`) imports each remaining module, using `Import-Module` with `-DisableNameChecking` to avoid errors due to name conflicts.


### Using PowerShell Modules

#### Overview
When working with PowerShell modules, it's important to determine:

- How and from where to run the module
- Whether the module or scripts are already on the host or need to be transferred

**Key Commands:**
- `Get-Module`: Lists modules that are currently loaded in the session.
- `Get-Module -ListAvailable`: Lists all installed modules, including those not currently loaded.

#### Checking Loaded Modules
Use `Get-Module` to see what modules are currently loaded:
```
PS C:\htb> Get-Module 

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Script     0.0        chocolateyProfile                   {TabExpansion, Update-SessionEnvironment, refreshenv}
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Script     0.7.3.1    posh-git                            {Add-PoshGitToProfile, Add-SshKey, Enable-GitColors, Expan...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```
#### Listing Available Modules
Use `Get-Module -ListAvailable` to see all modules installed on the system:
```
PS C:\htb> Get-Module -ListAvailable 

 Directory: C:\Users\tru7h\Documents\WindowsPowerShell\Modules

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Script     1.1.0      PSSQLite                            {Invoke-SqliteBulkCopy, Invoke-SqliteQuery, New-SqliteConn...

    Directory: C:\Program Files\WindowsPowerShell\Modules

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Script     1.0.1      Microsoft.PowerShell.Operation.V... {Get-OperationValidation, Invoke-OperationValidation}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Get-Package, Get-PackageProvider, Get-Packa...
Script     3.4.0      Pester                              {Describe, Context, It, Should...}
Script     1.0.0.1    PowerShellGet                       {Install-Module, Find-Module, Save-Module, Update-Module...}
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Set-PSReadLineKeyHandler, Remov...
```
The `-ListAvailable` modifier shows all installed modules, even those not currently loaded into the session.

#### Importing Modules
**`Import-Module` Command:**
The `Import-Module` cmdlet is used to add a module to the current PowerShell session.
**Syntax:**
```
Import-Module [-Name] <System.String[]> [-Alias <System.String[]>] [-ArgumentList <System.Object[]>] [-AsCustomObject] [-CimNamespace <System.String>] [-CimResourceUri <System.Uri>] -CimSession <Microsoft.Management.Infrastructure.CimSession> [-Cmdlet <System.String[]>] [-DisableNameChecking] [-Force] [-Function <System.String[]>] [-Global] [-MaximumVersion <System.String>] [-MinimumVersion <System.Version>] [-NoClobber] [-PassThru] [-Prefix <System.String>] [-RequiredVersion <System.Version>] [-Scope {Local | Global}] [-Variable <System.String[]>] [<CommonParameters>]
```
**Example: Importing a Module**

To use a cmdlet from the PowerSploit module, you must import it first. For example:
```
PS C:\Users\htb-student\Desktop\PowerSploit> Import-Module .\PowerSploit.psd1
```
After importing, you can run cmdlets such as `Get-NetLocalgroup`:
```
PS C:\Users\htb-student\Desktop\PowerSploit> Get-NetLocalgroup

ComputerName GroupName                           Comment
------------ ---------                           -------
WS01         Access Control Assistance Operators Members of this group can remotely query authorization attributes a...
WS01         Administrators                      Administrators have complete and unrestricted access to the compute...
...
```


#### Viewing and Modifying PSModulePath

**`$env:PSModulePath`:**
This environment variable lists the directories where PowerShell looks for modules:
```
PS C:\Users\htb-student> $env:PSModulePath

C:\Users\htb-student\Documents\WindowsPowerShell\Modules;C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules
```


**Adding Modules Permanently:**

Modules can be permanently added by placing them in one of the directories listed in `PSModulePath`. However, in a penetration testing scenario, it's often more efficient to transfer specific scripts and import them as needed rather than modifying the module path permanently.


