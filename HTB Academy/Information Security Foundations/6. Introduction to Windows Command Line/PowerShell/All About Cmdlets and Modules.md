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


### Execution Policy in PowerShell
**Overview:**
- PowerShell's execution policy is a feature designed to control the execution of scripts and modules. It's not a security control but a way to manage and restrict script execution based on administrative preferences.



**Impact on Script Execution:**
- If the execution policy is restrictive, you might encounter errors when attempting to run scripts. For example:
```
PS C:\Users\htb-student\Desktop\PowerSploit> Import-Module .\PowerSploit.psd1
Import-Module : File C:\Users\htb-student\PowerSploit.psm1 cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
```



**Checking Current Execution Policy:**
- Use `Get-ExecutionPolicy` to determine the current policy setting:
```
PS C:\htb> Get-ExecutionPolicy
Restricted
```


**Changing Execution Policy:**
- To allow script execution, change the policy using `Set-ExecutionPolicy`. For example:
```
PS C:\htb> Set-ExecutionPolicy Undefined
```
- Setting it to `Undefined` removes restrictions.


**Testing Script Import:**
- After adjusting the execution policy, try importing the module again:
```
PS C:\Users\htb-student\Desktop\PowerSploit> Import-Module .\PowerSploit.psd1
```



**Temporary Policy Change:**
- To avoid permanent changes, adjust the execution policy at the process level:
```
PS C:\htb> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
PS C:\htb> Get-ExecutionPolicy -List
Scope       ExecutionPolicy
-----       ---------------
MachinePolicy   Undefined
UserPolicy      Undefined
Process         Bypass
CurrentUser     Undefined
LocalMachine    Bypass
```



**Viewing Imported Module's Cmdlets and Functions:**
- Use `Get-Command -Module <modulename>` to see what commands are available in the imported module:
```
PS C:\htb> Get-Command -Module PowerSploit
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Invoke-ProcessHunter                               3.0.0.0    PowerSploit
Alias           Invoke-ShareFinder                                 3.0.0.0    PowerSploit
Function        Add-Persistence                                    3.0.0.0    PowerSploit
Function        Find-AVSignature                                   3.0.0.0    PowerSploit
```



**Best Practices:**
- **Sysadmin Perspective:** Revert any execution policy changes after completing tasks to maintain system security.
- **Pentester Perspective:** Be cautious with execution policy changes as they may signal a compromise. Ensure to clean up after your testing.


**PowerShell Gallery:**
- The PowerShell Gallery is a repository for PowerShell scripts, modules, and more, created by Microsoft and the community.
- It provides a convenient platform for sharing and discovering PowerShell solutions.


**PowerShellGet Module:**
- `PowerShellGet` is built into PowerShell and helps manage modules and scripts from the PowerShell Gallery.



**Functions in PowerShellGet:**
- **Find-Command:** Searches for cmdlets, functions, workflows, aliases, and scripts.
- **Find-DscResource:** Finds Desired State Configuration (DSC) resources.
- **Find-Module:** Finds modules in the gallery.
- **Find-Script:** Finds scripts in the gallery.
- **Get-InstalledModule:** Lists installed modules.
- **Get-InstalledScript:** Lists installed scripts.
- **Get-PSRepository:** Lists registered repositories.
- **Install-Module:** Installs a module from the gallery.
- **Install-Script:** Installs a script from the gallery.
- **Publish-Module:** Publishes a module to a repository.
- **Register-PSRepository:** Registers a new repository.
- **Uninstall-Module:** Uninstalls a module.
- **Update-Module:** Updates an installed module.


**Example Commands:**
- **Finding a Module:**
```
PS C:\htb> Find-Module -Name AdminToolbox
Version    Name                                Repository           Description
-------    ----                                ----------           -----------
11.0.8     AdminToolbox                        PSGallery            Master module for a col...
```
- **Installing a Module:**
```
PS C:\htb> Install-Module -Name AdminToolbox
```
- **Combining Find and Install:**
```
PS C:\htb> Find-Module -Name AdminToolbox | Install-Module
```
This command uses PowerShell's Pipeline to find and install the module in one step.


**Auto-Import Behavior:**
- Modern versions of PowerShell automatically import a module when you first run a cmdlet or function from it, so manual import is not required.



**Manual Import for Custom Modules:**
- For modules downloaded from GitHub or other sources, you'll need to manually import them unless modified in your PowerShell Profile.
- PowerShell Profile locations can be found [here](https://docs.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-powershell-profiles?view=powershell-7.3).



**Using GitHub:**
- GitHub offers additional content from the IT community.
- Utilizing Git and GitHub requires knowledge of other tools and concepts, which will be covered in later sections.



**Best Practices:**
- Always review and validate modules and scripts from external sources before use.
- Regularly update and manage installed modules to ensure you are using the latest versions with the latest features and security updates.


### Tools To Be Aware Of
Here are some essential PowerShell modules and projects for penetration testers and sysadmins:
- **AdminToolbox:**
    - A collection of modules designed for system administration tasks.
    - Useful for managing Active Directory, Exchange, network management, file and storage issues, and more.
- **ActiveDirectory:**
    - Provides tools for managing Active Directory.
    - Capabilities include managing users, groups, permissions, and other AD-related tasks.
- **Empire / Situational Awareness:**
    - A suite of PowerShell modules and scripts for gaining situational awareness on hosts and domains.
    - Maintained by BC Security as part of the Empire Framework.
- **Inveigh:**
    - A tool for network spoofing and Man-in-the-Middle (MitM) attacks.
    - Useful for performing various network attack techniques.
- **BloodHound / SharpHound:**
    - Allows for visual mapping of an Active Directory environment.
    - Includes graphical analysis tools and data collectors written in C# and PowerShell.

**Note:** Mastering PowerShell modules and cmdlets is crucial for working effectively with these tools. Familiarity with installing, importing, and examining modules and cmdlets will be valuable for various tasks in this module. If you encounter difficulties, refer back to this section for guidance.

**Next Step:** Moving on to User and Group management.


## Questions
- What cmdlet can help us find modules that are loaded into our session?
	- Get-Module
- What module provides us with cmdlets built to manage package installation from the PowerShell Gallery?
	- PowerShellGet
- Take a moment to practice installing and loading modules on the target host. Answer "COMPLETE" when done.
	- COMPLETE