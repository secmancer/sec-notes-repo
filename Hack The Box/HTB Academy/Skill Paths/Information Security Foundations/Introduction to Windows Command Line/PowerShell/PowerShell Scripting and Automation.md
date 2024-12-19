### Introduction
- **PowerShell Versatility**: PowerShell's strength lies in its ability to automate tasks effectively, making it invaluable for both administrators and pentesters.
- **Script and Module Creation**: Developing PowerShell scripts and modules, whether simple or complex, can streamline workflows and reduce manual effort.
- **Focus of the Module**: This section covers the components of PowerShell scripts and modules, guiding users to create their own customizable and reusable tools.
- **End Goal**: By the module's conclusion, users will have built a functional and user-friendly PowerShell module to enhance their automation capabilities.

### Understanding PowerShell Scripting
- **Modular Nature**: PowerShell's modular design allows extensive control and flexibility, making it suitable for various scripting and automation tasks.
- **Versatile Input Handling**: PowerShell scripts can process inputs from multiple languages, file types, and object types, enhancing their utility.
- **Executing Scripts**: Scripts can be executed directly using the `.\script` syntax.
- **Using Modules**: Modules can be imported with the `Import-Module` cmdlet, extending functionality and reusability.
- **Overview**: This section introduces scripts and modules, laying the foundation for effective PowerShell usage.



### Scripts vs. Modules
- **Script Definition**: A script is an executable text file containing PowerShell cmdlets and functions.
- **Module Definition**: A module can be a single script or a collection of scripts, manifests, and functions bundled together.
- **Usage Difference**: Scripts are executed directly, while modules are imported to access their scripts and functions as needed.
- **Unified Discussion**: For simplicity, this section treats scripts and modules similarly since module concepts apply to standard scripts.
- **File Extensions**: Understanding file extensions is essential to distinguish between script and module functionalities.



### File Extensions
- To familiarize ourselves with some file extensions we will encounter while working with PowerShell scripts and modules, we have put together a small table with the extensions and their descriptions.
![[Screenshot_20241111_145822 1.png]]
- These are the main extensions we are concerned with right now. 
- In reality, PowerShell modules can have many different accompanying files with various extensions, but they are not requirements for what we are trying to do. 
- If you wish for a deeper dive into PowerShell script files, and help files, check out this [Post](https://learn.microsoft.com/en-us/powershell/scripting/developer/module/writing-a-windows-powershell-module?view=powershell-7.2)



### Making a Module
- So let's get down to it. 
- From this point on, we will cover the components of a PowerShell module, what they contain, and how to create them. 
- This process is simple. It just takes a bit of prior planning. 
- Consider this scenario:

> **Scenario**: We have found ourselves performing the same checks over and over when administering hosts. So to expedite our tasks, we will create a PowerShell module to run the checks for us and then output the information we ask for. Our module, when used, should output the host's `computer name`, `IP address`, and basic `domain information`, and provide us with the output of the `C:\Users\` directory so we can see what users have interactively logged into that host.

- Now that we know what's going into our module, it's time to start building it out.



### Module Components
- A module is made up of `four` essential components:
	1. A `directory` containing all the required files and content, saved somewhere within `$env:PSModulePath`.
	- This is done so that when you attempt to import it into your PowerShell session or Profile, it can be automatically found instead of having to specify where it is.
	2. A `manifest` file listing all files and pertinent information about the module and its function.
	- This could include associated scripts, dependencies, the author, example usage, etc.
	3. Some code file - usually either a PowerShell script (`.ps1`) or a (`.psm1`) module file that contains our script functions and other information.
	4. Other resources the module needs, such as help files, scripts, and other supporting documents.
- This setup is standard practice but not strictly necessary. 
- We could have our module be just a `*.psm1` file that contains our scripts and context, skipping the manifest and other helper files.
- PowerShell would be able to interpret and understand what to do in either instance. 
- For the sake of propriety, we will work on building out a standard PowerShell module, including the manifest file and some built-in help functionality.



### Making a Directory to Hold Our Module
- Making a directory is super simple, as discussed in earlier sections. 
- Before we go any further, we need to create the directory to hold our module. 
- This directory should be in one of the paths within `$env:PSModulePath`. 
- If unsure as to what those paths are, you can call the variable to see where the best place would be. 
- So we are going to make a folder named `quick-recon`.
- #### Mkdir
```powershell-session

    Directory: C:\Users\MTanaka\Documents\WindowsPowerShell\Modules


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        10/31/2022   7:38 AM                quick-recon
```
- Now that we have our directory, we can create the module. 
- Let's discuss a `module manifest` file for a second.



### Module Manifest
- A module manifest is a simple `.psd1` file that contains a hash table. 
- The keys and values in the hash table perform the following functions:
	- Describe the `contents` and `attributes` of the module.
	- Define the `prerequisites`. ( specific modules from outside the module itself, variables, functions, etc.)
	- Determine how the `components` are `processed`.
- If you add a manifest file to the module folder, you can reference multiple files as a single unit by referencing the manifest. 
- The `manifest` describes the following information:
	- `Metadata` about the module, such as the module version number, the author, and the description.
	- `Prerequisites` needed to import the module, such as the Windows PowerShell version, the common language runtime (CLR) version, and the required modules.
	- `Processing` directives, such as the scripts, formats, and types to process.
	- `Restrictions` on the module members to export, such as the aliases, functions, variables, and cmdlets to export.
- We can quickly create a manifest file by utilizing `New-ModuleManifest` and specifying where we want it placed.
- #### New-ModuleManifest
```powershell-session
PS C:\htb> New-ModuleManifest -Path C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon\quick-recon.psd1 -PassThru

# Module manifest for module 'quick-recon'
#
# Generated by: MTanaka
#
# Generated on: 10/31/2022
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

<SNIP>
```
- By issuing the command above, we have provisioned a `new` manifest file populated with the default considerations. 
- The `-PassThru` modifier lets us see what is being printed in the file and on the console. 
- We can now go in and fill in the sections we want with the relevant info. 
- Remember that all the lines in the manifest files are optional except for the `ModuleVersion` line. 
- Editing the manifest will be easiest done from a GUI where you can utilize a text editor or IDE such as VSCode.
- If we were to complete our manifest file now for this module, it would appear something like this.
- #### Sample Manifest
```powershell
# Module manifest for module 'quick-recon'
#
# Generated by: MTanaka
#
# Generated on: 10/31/2022
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = 'C:\Users\MTanaka\WindowsPowerShell\Modules\quick-recon\quick-recon.psm1'

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '0a062bb1-8a1b-4bdb-86ed-5adbe1071d2f'

# Author of this module
Author = 'MTanaka'

# Company or vendor of this module
CompanyName = 'Greenhorn.Corp.'

# Copyright statement for this module
Copyright = '(c) 2022 Greenhorn.Corp. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This module will perform several quick checks against the host for Reconnaissance of key information.'

# Functions to export from this module, for best performance, do not use wildcards and do not delete the entry, use an empty array if there are no functions to export.
FunctionsToExport = @()

# Cmdlets to export from this module, for best performance, do not use wildcards and do not delete the entry, use an empty array if there are no cmdlets to export.
CmdletsToExport = @()

# Variables to export from this module
VariablesToExport = '*'

# Aliases to export from this module, for best performance, do not use wildcards and do not delete the entry, use an empty array if there are no aliases to export.
AliasesToExport = @()

# List of all modules packaged with this module
# ModuleList = @()

# List of all files packaged with this module
# FileList = @()  
}
```
- We can come back to the manifest later and add in the `functions, cmdlets, and variables` we want to allow for export. We need to build and finish the script first.



### Create Our Script File
- We can use the `New-Item` (ni) cmdlet to create our file.
- #### New-Item
```powershell-session
PS C:\htb>  ni quick-recon.psm1 -ItemType File


    Directory: C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        10/31/2022   9:07 AM              0 quick-recon.psm1
```
- Easy enough, right? Now to fill in this beast.



### Importing Modules You Need
- **Importing Modules**: To ensure our PowerShell script operates correctly with necessary cmdlets or functions, we include an `Import-Module` line at the beginning of the script.
- **Purpose of Import-Module**: This command loads the required modules before executing the script, similar to running it directly in the PowerShell shell.
- **Built-in Cmdlets**: Many cmdlets and functions used in the script are already built into PowerShell.
- **Active Directory Module**: For specific functionality, like interacting with Active Directory, we need to import the `ActiveDirectory` module.
- #### Import Into Our Module
```powershell
Import-Module ActiveDirectory 
```
- Pretty simple right?
- Now we have our module script file `quick-recon.psm1`, and we have added an `import-module` statement within. 
- Now we can get to the meat of the file, our `functions`.



### Functions and doing work with Powershell
- We need to do four main things with this module:
	- Retrieve the host ComputerName
	- Retrieve the hosts IP configuration
	- Retrieve basic domain information
	- Retrieve an output of the "C:\Users" directory
- **Getting ComputerName**: The script will use the environment variable `$env:ComputerName` to capture the hostname of the machine. The output will be stored in the variable `$Hostname` for easy reference.
- **Capturing IP Address**: The IP address of active host adapters will be captured using the `IPConfig` command and stored in the `$IP` variable.
- **Basic Domain Information**: The script will use `Get-ADDomain` to gather domain information and store it in the `$Domain` variable.
- **Listing User Folders**: The script will list user folders in `C:\Users\` with `Get-ChildItem` and store the output in the `$Users` variable.
- **Creating Variables**: Variables are created by assigning a name, the = symbol, and the action or value to store (e.g., $Hostname = $env:ComputerName).
- #### Variables
```powershell
Import-Module ActiveDirectory 

$Hostname = $env:ComputerName
$IP = ipconfig 
$Domain = Get-ADDomain  
$Users = Get-ChildItem C:\Users\ 
  
```
- Our variables are now set to run singular commands or functions, grabbing the needed output. 
- Now let's format that data and give ourselves some nice output. 
- We can do this by writing the result to a `file` using `New-Item` and `Add-Content`. 
- To make things easier, we will make this output process into a callable function called `Get-Recon`.
- #### Output Our Info
```powershell
Import-Module ActiveDirectory

function Get-Recon {  

    $Hostname = $env:ComputerName  

    $IP = ipconfig

    $Domain = Get-ADDomain 

    $Users = Get-ChildItem C:\Users\

    new-Item ~\Desktop\recon.txt -ItemType File 

    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***",  $IP, "***---USERS---***", $Users

    Add-Content ~\Desktop\recon.txt $Vars
  } 
```
- `New-Item` creates our output file for us first, then notice how we utilized one more variable (`$Vars`) to format our output. 
- We call each variable and insert a descriptive line in between each. 
- Lastly, the `Add-Content` cmdlet appends the data we gather into a file called recon.txt by writing the results of $Vars. 
- Our function is shaping up now. 
- Next, we need to add some comments to our file so that others can understand what we are trying to accomplish and why we did it the way we did.



### Comments within the Script
- The (`#`) will tell PowerShell that the line contains a comment within your script or module file.
- If your comments are going to encompass several lines, you can use the `<#` and `#>` to wrap several lines as one large comment like seen below.
- #### Comment Blocks
```powershell

# This is a single-line comment.  

<# This line and the following lines are all wrapped in the Comment specifier. 
Nothing with this window will be ready by the script as part of a function.
This text exists purely for the creator and us to convey pertinent information.

#>  
```
- #### Comments Added
```powershell
Import-Module ActiveDirectory

function Get-Recon {  
    # Collect the hostname of our PC.
    $Hostname = $env:ComputerName  
    # Collect the IP configuration.
    $IP = ipconfig
    # Collect basic domain information.
    $Domain = Get-ADDomain 
    # Output the users who have logged in and built out a basic directory structure in "C:\Users\".
    $Users = Get-ChildItem C:\Users\
    # Create a new file to place our recon results in.
    new-Item ~\Desktop\recon.txt -ItemType File 
    # A variable to hold the results of our other variables. 
    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***",  $IP, "***---USERS---***", $Users
    # It does the thing 
    Add-Content ~\Desktop\recon.txt $Vars
  } 
```
- It's as simple as that. 
- Nothing too crazy with comments. 
- Now we need to include a bit of `help` syntax so others can understand how to use our module.



### Including Help
- **Comment-based Help**: PowerShell allows embedding help information within scripts or modules using comment blocks and recognized keywords, which can later be accessed using `Get-Help`.
- **Placement of Help**:
    - Inside the function: It should be placed right after the function's opening line or at the end of the function, one line after the last action.
    - Outside the function: It must be placed above the function, with no more than one line between the help section and the function.
- **Example Setup**: For now, the help section will be placed outside the function, at the top of the script.
- **Further Learning**: A deeper dive into help can be explored through the official [PowerShell help article](https://learn.microsoft.com/en-us/powershell/scripting/developer/help/writing-help-for-windows-powershell-scripts-and-functions?view=powershell-7.2).
- #### Module Help
```powershell
Import-Module ActiveDirectory

<# 
.Description  
This function performs some simple recon tasks for the user. We import the module and issue the 'Get-Recon' command to retrieve our output. Each variable and line within the function and script are commented for our understanding. Right now, this module will only work on the local host from which you run it, and the output will be sent to a file named 'recon.txt' on the Desktop of the user who opened the shell. Remote Recon functions are coming soon!  

.Example  
After importing the module run "Get-Recon"
'Get-Recon


    Directory: C:\Users\MTanaka\Desktop


Mode                 LastWriteTime         Length Name                                                                                                                                        
----                 -------------         ------ ----                                                                                                                                        
-a----         11/3/2022  12:46 PM              0 recon.txt '

.Notes  
Remote Recon functions coming soon! This script serves as our initial introduction to writing functions and scripts and making PowerShell modules.  

#>

function Get-Recon {  
<SNIP>  
```
- Notice our use of `keywords`. 
- To specify a keyword within the comment block, we use the syntax `.<keyword>` and then place the flavor text underneath.
- We only specified `Description, Example, and Notes`, but several more keywords can be placed in the help block. 
- To see all the available keywords, reference this article on [Comment Based Help Keywords](https://learn.microsoft.com/en-us/powershell/scripting/developer/help/comment-based-help-keywords?view=powershell-7.2). 
- Our last portion to discuss before wrapping everything up into our nice PowerShell Module file, is Exporting and Protecting functions.



### Protecting Functions
- We may add functions to our scripts that we do not want to be accessed, exported, or utilized by other scripts or processes within PowerShell. 
- To protect a function from being exported or to explicitly set it for export, the `Export-ModuleMember` is the cmdlet for the job. 
- The contents are exportable if we leave this out of our script modules. 
- If we place it in the file but leave it blank like so:
- #### Exclude From Export
```powershell
Export-ModuleMember  
```
- It ensures that the module's variables, aliases, and functions cannot be `exported`. 
- If we wish to specify what to export, we can add them to the command string like so:
- #### Export Specific Functions and Variables
```powershell
Export-ModuleMember -Function Get-Recon -Variable Hostname 
```
- Alternatively, if you only wanted to export all functions and a specific variable, for example, you could issue the `*` after -Function and then specify the Variables to export explicitly. 
- So let's add the `Export-ModuleMember` cmdlet to our script and specify that we want to allow our function `Get-Recon` and our variable `Hostname` to be available for export.
- #### Export Line Addition
```powershell
<SNIP>  
function Get-Recon {  
    # Collect the hostname of our PC
    $Hostname = $env:ComputerName  
    # Collect the IP configuration
    $IP = ipconfig
    # Collect basic domain information
    $Domain = Get-ADDomain 
    # Output the users who have logged in and built out a basic directory structure in "C:\Users"
    $Users = Get-ChildItem C:\Users\
    # Create a new file to place our recon results in
    new-Item ~\Desktop\recon.txt -ItemType File 
    # A variable to hold the results of our other variables 
    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***",  $IP, "***---USERS---***", $Users
    # It does the thing 
    Add-Content ~\Desktop\recon.txt $Vars
  } 

Export-ModuleMember -Function Get-Recon -Variable Hostname  
```



### Scope
- When dealing with scripts, the PowerShell session, and how stuff is recognized at the Commandline, the concept of Scope comes into play. 
- Scope, in essence, is how PowerShell recognizes and protects objects within the session from unauthorized access or modification. 
- PowerShell currently uses `three` different Scope levels.
![[Screenshot_20241111_150149.png]]
- This matters to us if we do not want anything outside the scope we are running the script in to access its contents. 
- Additionally, we can have child scopes created within the main scopes. 
- For example, when you run a script, the script scope is instantiated, and then any function that is called can also spawn a child scope surrounding that function and its included variables. 
- If we wanted to ensure that the contents of that specific function were not accessible to the rest of the script or the PowerShell session itself, we could modify its scope. 
- This is a complex topic and something above the level of this module currently, but we felt it was worth mentioning. 
- For more on Scope in PowerShell, check out the documentation [here](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-7.2).



### Putting It All Together
- Now that we have gone through and created our pieces and parts let's see it all together.
- #### Final Product
```powershell
import-module ActiveDirectory

<# 
.Description  
This function performs some simple recon tasks for the user. We import the module and then issue the 'Get-Recon' command to retrieve our output. Each variable and line within the function and script are commented for your understanding. Right now, this only works on the local host from which you run it, and the output will be sent to a file named 'recon.txt' on the Desktop of the user who opened the shell. Remote Recon functions coming soon!  

.Example  
After importing the module run "Get-Recon"
'Get-Recon


    Directory: C:\Users\MTanaka\Desktop


Mode                 LastWriteTime         Length Name                                                                                                                                        
----                 -------------         ------ ----                                                                                                                                        
-a----         11/3/2022  12:46 PM              0 recon.txt '

.Notes  
Remote Recon functions coming soon! This script serves as our initial introduction to writing functions and scripts and making PowerShell modules.  

#>
function Get-Recon {  
    # Collect the hostname of our PC
    $Hostname = $env:ComputerName  
    # Collect the IP configuration
    $IP = ipconfig
    # Collect basic domain information
    $Domain = Get-ADDomain 
    # Output the users who have logged in and built out a basic directory structure in "C:\Users"
    $Users = Get-ChildItem C:\Users\
    # Create a new file to place our recon results in
    new-Item ~\Desktop\recon.txt -ItemType File 
    # A variable to hold the results of our other variables 
    $Vars = "***---Hostname info---***", $Hostname, "***---Domain Info---***", $Domain, "***---IP INFO---***",  $IP, "***---USERS---***", $Users
    # It does the thing 
    Add-Content ~\Desktop\recon.txt $Vars
  } 

Export-ModuleMember -Function Get-Recon -Variable Hostname 
```
- And there we have it, our full module file. 
- Our use of Comment-based help, functions, variables and content protection makes for a dynamic and clear-to-read script.
- From here we can save this file in our Module directory we created and import it from within PowerShell for use.
- #### Importing the Module For Use
```powershell-session
PS C:\htb> Import-Module 'C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon.psm1`

PS C:\Users\MTanaka\Documents\WindowsPowerShell\Modules\quick-recon> get-module

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
Script     0.0        quick-recon                         Get-Recon
```
- Perfect. 
- We can see that our module was imported using the `Import-Module` cmdlet, and to ensure it was loaded into our session, we ran the `Get-Module` cmdlet. 
- It has shown us that our module `quick-recon` was imported and has the command `Get-Recon` that could be exported. 
- We can also test the Comment-based help by trying to run `Get-Help` against our module.
- #### Help Validation
```powershell-session
PS C:\htb> get-help get-recon

NAME
    Get-Recon

SYNOPSIS


SYNTAX
    Get-Recon [<CommonParameters>]


DESCRIPTION
    This function performs some simple recon tasks for the user. We simply import the module and then issue the
    'Get-Recon' command to retrieve our output. Each variable and line within the function and script are commented for
    your understanding. Right now, this only works on the local host from which you run it, and the output will be sent
    to a file named 'recon.txt' on the Desktop of the user who opened the shell. Remote Recon functions coming soon!


RELATED LINKS

REMARKS
    To see the examples, type: "get-help Get-Recon -examples."
    For more information, type: "get-help Get-Recon -detailed."
    For technical information, type: "get-help Get-Recon -full."
```
- Our help works as well. 
- So we now have a fully functioning module for our use. 
- We can use this as a basis for anything we build further and could even modify this one to encompass more reconnaissance functions in the future.
- This was a simple example of what can be done from an automation perspective with PowerShell, but a great way to see it built and in use. 
- We can use module building and scripting to our advantage and simplify our processes as we go. 
- Saving time ultimately enables us to do more as operators and spend time on other tasks that need our attention.
- If you would like a copy of the quick-recon module for your use, there is a copy saved in the `Resources` of this module at the top right corner of any section page.