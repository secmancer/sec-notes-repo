### Cmdlets

- **Definition**: Cmdlets are single-feature commands in PowerShell that manipulate objects.
- **Structure**: They follow a Verb-Noun naming convention (e.g., `Test-WSMan`).
- **Creation**: Written in C# or other languages and then compiled.
- **Viewing Cmdlets**: Use `Get-Command` to list available cmdlets.
- **Help**: Use `Get-Help` and `Get-Member` to explore cmdlet options and functionality.

### PowerShell Modules

- **Definition**: A module is a package of PowerShell code that includes cmdlets, functions, and other resources.
- **Components**:
    - **Cmdlets**: Predefined commands.
    - **Script Files**: `.ps1` scripts.
    - **Functions**: Reusable code blocks.
    - **Assemblies**: Compiled code.
    - **Resources**: Metadata and help files.
- **Manifest File**: `.psd1` file containing metadata about the module.
- **Script Module File**: `.psm1` file containing the PowerShell code.

### Working with Modules

- **Loading Modules**: Use `Import-Module` to add a module to the current session.
    - Example: `Import-Module .\PowerSploit.psd1`
- **List Loaded Modules**: Use `Get-Module` to view modules currently loaded.
- **List Available Modules**: Use `Get-Module -ListAvailable` to see all installed modules.

### Execution Policy

- **Definition**: Determines script execution permissions.
- **Checking**: Use `Get-ExecutionPolicy`.
- **Changing**: Use `Set-ExecutionPolicy`. To bypass restrictions temporarily, use `-Scope Process`.
    - Example: `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass`

### Finding and Installing Modules

- **PowerShell Gallery**: Repository for PowerShell scripts and modules.
- **PowerShellGet Module**: Provides cmdlets to interact with the PowerShell Gallery.
    - **Find Modules**: `Find-Module`
    - **Install Modules**: `Install-Module`
    - **List Installed Modules**: `Get-InstalledModule`
    - **Update Modules**: `Update-Module`

### Example Commands

- **List Available Cmdlets in a Module**:
    - `Get-Command -Module <ModuleName>`
- **View PowerShell Module Path**:
    - `$env:PSModulePath`

### Notes

- **Testing**: Use `Get-Command -Module <ModuleName>` to see what cmdlets and functions are available after importing a module.
- **Cleanup**: Always revert execution polic

### Questions
- What cmdlet can help us find modules that are loaded into our session?
	- Get-Module
- What module provides us with cmdlets built to manage package installation from the PowerShell Gallery?
	- PowerShellGet
- Take a moment to practice installing and loading modules on the target host. Answer "COMPLETE" when done.
	- COMPLETE