### **Understanding PowerShell Scripting**
**PowerShell Overview:**
- PowerShell is highly modular, offering significant control and flexibility.
- Scripts and modules automate tasks and ease administrative burdens.
- PowerShell handles inputs from various languages and file types and supports numerous object types.

**Scripts vs. Modules:**
- **Scripts:**
    - Executable text files containing PowerShell cmdlets and functions.
    - Typically executed directly using `. \script` syntax.
- **Modules:**
    - Can be a simple script or a collection of script files, manifests, and functions bundled together.
    - Imported using `Import-Module` cmdlet, allowing access to all included scripts and functions.

**File Extensions:**
- Understanding file extensions is crucial when working with PowerShell scripts and modules.

![[Screenshot_20240916_084434.png]]


### **PowerShell Module Development**
**File Extensions:**
- PowerShell modules can include various file extensions, but essential ones for basic usage are:
    - **.ps1**: PowerShell script file
    - **.psm1**: PowerShell module file
    - **.psd1**: PowerShell module manifest file

**Creating a PowerShell Module:**
1. **Scenario Example:**
    - Task: Automate repetitive checks for administrative tasks.
    - Output Requirements: Computer name, IP address, domain info, and user directory contents.
2. **Module Components:**
    - **Directory:**
        - Contains all required files.
        - Should be placed within `$env:PSModulePath`.
        - Example command: `mkdir quick-recon`
    - **Manifest File:**
        - A `.psd1` file with a hash table describing module attributes.
        - Includes:
            - Metadata (e.g., module version, author)
            - Prerequisites (e.g., required PowerShell version)
            - Processing directives (e.g., scripts, types to process)
            - Export restrictions (e.g., functions, cmdlets)
        - **Creating a Manifest File:**
            - Use `New-ModuleManifest` cmdlet.
            - Example command:
```
New-ModuleManifest -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psd1 -PassThru
```
- Fill in the manifest with relevant information.
- **Sample Manifest Content:**
```
@{
  RootModule = 'C:\Users\MTanaka\WindowsPowerShell\Modules\quick-recon\quick-recon.psm1'
  ModuleVersion = '1.0'
  GUID = '0a062bb1-8a1b-4bdb-86ed-5adbe1071d2f'
  Author = 'MTanaka'
  CompanyName = 'Greenhorn.Corp.'
  Copyright = '(c) 2022 Greenhorn.Corp. All rights reserved.'
  Description = 'This module will perform several quick checks against the host for Reconnaissance of key information.'
  FunctionsToExport = @()
  CmdletsToExport = @()
  VariablesToExport = '*'
  AliasesToExport = @()
  ModuleList = @()
  FileList = @()
}
```
**Script File:**
- Create with `New-Item` cmdlet.
- Example command:
```
New-Item -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psm1 -ItemType File
```
- Add functionality and scripts as needed.




#### **Importing Modules**
- **Purpose**: Use `Import-Module` to load required modules before executing a script. This ensures that all necessary cmdlets and functions are available.
- **Example**:
```
Import-Module ActiveDirectory
```


#### **Module Components**
1. **Directory**:
    - **Location**: Place the module directory in one of the paths within `$env:PSModulePath`.
    - **Example**:
```
mkdir quick-recon
```
2. **Manifest File**:
- **File Extension**: `.psd1`
- **Purpose**: Contains metadata and configuration details about the module.
- **Key Sections**:
    - **Metadata**: Module version, author, description.
    - **Prerequisites**: Required PowerShell version, dependent modules.
    - **Processing Directives**: Scripts, formats, types to process.
    - **Export Restrictions**: Aliases, functions, variables, cmdlets.
- **Creation**:
```
New-ModuleManifest -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psd1 -PassThru
```
- **Sample Manifest**:
```
@{
  RootModule = 'C:\Users\MTanaka\WindowsPowerShell\Modules\quick-recon\quick-recon.psm1'
  ModuleVersion = '1.0'
  GUID = '0a062bb1-8a1b-4bdb-86ed-5adbe1071d2f'
  Author = 'MTanaka'
  CompanyName = 'Greenhorn.Corp.'
  Copyright = '(c) 2022 Greenhorn.Corp. All rights reserved.'
  Description = 'This module will perform several quick checks against the host for Reconnaissance of key information.'
  FunctionsToExport = @()
  CmdletsToExport = @()
  VariablesToExport = '*'
  AliasesToExport = @()
  ModuleList = @()
  FileList = @()  
}
```
3. **Code File**:
    - **File Extension**: `.psm1`
    - **Purpose**: Contains script functions and other information.
4. **Other Resources**:
    - **Examples**: Help files, additional scripts, supporting documents.



#### **Creating and Configuring the Module**
1. **Create the Script File**:
    - **Command**:
```
New-Item quick-recon.psm1 -ItemType File
```
2. **Define Functions**:
- **Purpose**: Perform specific tasks and return desired output.
- **Example**:
```
Import-Module ActiveDirectory

function Get-Recon {
    $Hostname = $env:ComputerName
    $IP = ipconfig
    $Domain = Get-ADDomain
    $Users = Get-ChildItem C:\Users\
    New-Item ~\Desktop\recon.txt -ItemType File
    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***", $IP, "***---USERS---***", $Users
    Add-Content ~\Desktop\recon.txt $Vars
}
```
3. **Add Comments**:
	- **Single-Line**: Use `#`
	- **Block Comments**: Use `<# #>`
	- **Example**:
```
# This is a single-line comment.

<#
This is a block comment.
It can span multiple lines.
#>
```
4. **Include Help**:
	- **Location**: Place within the function or at the top of the script.
	- **Keywords**: `.Description`, `.Example`, `.Notes`
	- **Example**:
```
<#
.Description
This function performs some simple recon tasks for the user.

.Example
After importing the module run "Get-Recon".

.Notes
Remote Recon functions coming soon!
#>
```
#### **Exporting and Protecting Functions**
- **Next Steps**: Learn about exporting functions and protecting the code to ensure proper usage and security.




#### **Exporting Functions**
- **Export-ModuleMember Cmdlet**: Used to control which functions, variables, and aliases are accessible from outside the module.
    - **Exclude from Export**:
```
Export-ModuleMember  
```
- This prevents any functions, variables, or aliases from being exported by default.
- **Export Specific Functions and Variables**:
```
Export-ModuleMember -Function Get-Recon -Variable Hostname
```
- Here, `Get-Recon` function and `Hostname` variable are explicitly exported.
- To export all functions and specific variables:
```
Export-ModuleMember -Function * -Variable Hostname
```



#### **Scope in PowerShell**
- **Scope Levels**: Determines the accessibility and lifetime of variables and functions.
    - **Global**: Default scope for all objects when PowerShell starts. Includes variables, aliases, functions, and profile settings.
    - **Local**: Current scope in use, can be the default or a child scope.
    - **Script**: Temporary scope for a script; affects only the script and its content.
    - **Child Scopes**: Created by functions or scripts and have access to the parent scope but not vice versa. Modifying scope ensures that variables and functions are not accessible outside their intended scope.



#### **Putting It All Together**
1. **Final Script Example**:
```
import-module ActiveDirectory

# Description of the module and function
<# 
.Description  
This function performs some simple recon tasks for the user. It imports the module and then issues the 'Get-Recon' command to retrieve our output. This only works on the local host, and the output is sent to 'recon.txt' on the Desktop. Remote functions are planned.

.Example  
Run "Get-Recon" after importing the module.
#>

function Get-Recon {  
    # Collect the hostname of our PC
    $Hostname = $env:ComputerName  
    # Collect the IP configuration
    $IP = ipconfig
    # Collect basic domain information
    $Domain = Get-ADDomain 
    # Output the users in "C:\Users"
    $Users = Get-ChildItem C:\Users\
    # Create a file for the recon results
    new-Item ~\Desktop\recon.txt -ItemType File 
    # Format the output
    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***",  $IP, "***---USERS---***", $Users
    # Write the results to the file
    Add-Content ~\Desktop\recon.txt $Vars
} 

Export-ModuleMember -Function Get-Recon -Variable Hostname 
```

2. **Importing the Module**:
```
Import-Module 'C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon.psm1'
```
3. **Checking Module Import**:
```
Get-Module
```
4. **Validating Help**:
```
Get-Help Get-Recon
```
