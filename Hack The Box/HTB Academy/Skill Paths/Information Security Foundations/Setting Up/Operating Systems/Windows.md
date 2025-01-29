### Benefits of Using Windows as a Penetration Testing Platform
1. **Blending into Enterprise Environments**:
    - Windows is common in enterprise environments, reducing suspicion during testing.
    - Better integration with Active Directory domains and SMB shares.
2. **Custom-built Platform**:
    - Building your own setup increases understanding of internal workings.
    - Reduces unnecessary services, improving security and performance.
    - Serves as a testbed for payloads and exploits before deploying them on engagements.
3. **New Features Enhancing Functionality**:
    - **Windows Subsystem for Linux (WSL)**:
        - Runs Linux tools natively without third-party applications.
        - Eliminates the need for hypervisors like VirtualBox or Docker.



### Key Installation Requirements
- #### **Hardware Requirements**:
	- **Processor**: Minimum 1 GHz; dual-core or better recommended.
	- **RAM**: Minimum 2 GB; 4 GB or more ideal.
	- **Storage**: At least 60 GB; 80 GB+ recommended for tool installations and updates.
	- **Network**: Preferably two network adapters.
- #### **Software Requirements**:
	- Licensed Windows installation (adhering to terms of use).
	- A good starting point: **Developer Evaluation VM**, which includes:
	    - Windows 10 Version 2004.
	    - Windows SDK and Visual Studio pre-configured for development.
	    - WSL with Ubuntu installed.
	    - Developer mode enabled.



### Setup and Configuration
- #### **Initial Preparations**:
	1. Update the Windows host to the latest version.
	2. Install necessary tools:
	    - **Windows Subsystem for Linux (WSL)**.
	    - **Chocolatey Package Manager**.
	3. Configure Windows Defender exclusions for penetration testing tools to prevent them from being quarantined.
- #### **Creating a Snapshot**:
	- Take a backup or VM snapshot after the setup to ensure recovery in case of issues.
- #### Updating the Windows Host Using PowerShell
1. **Check Execution Policy**:
    ```powershell
    Get-ExecutionPolicy -List
    ```
    - Ensure the execution policy is set for the current session only:
        ```powershell
        Set-ExecutionPolicy Unrestricted -Scope Process
        ```
2. **Install and Use the `PSWindowsUpdate` Module**:
    - Install the module:
        ```powershell
        Install-Module PSWindowsUpdate
        ```
    - Import the module and install updates:
        ```powershell
        Import-Module PSWindowsUpdate
        Install-WindowsUpdate -AcceptAll
        Restart-Computer -Force
        ```
3. Regular updates are critical, especially if the host will not be destroyed after use.



### Next Steps
- Install core tools (e.g., Git, Python, VS Code).
- Secure the environment with careful tool selection and isolation measures.
- Regularly test and refine the setup for optimal functionality during engagements.



### Chocolatey Package Manager
- Chocolatey is a free and open-source package manager for Windows that allows for easy software installation and dependency management. 
- It supports automation with **PowerShell, Ansible**, and other management solutions.
- #### **Installing Chocolatey**
	- Run the following PowerShell command to install Chocolatey:
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
- This command:
    - Bypasses execution policy for the session.
    - Ensures TLS 1.2 is used for secure web requests.
    - Downloads and installs Chocolatey from its official repository.
- #### **Updating Chocolatey**
```powershell
choco upgrade chocolatey -y
```
- Ensures Chocolatey is up-to-date before installing packages.
- #### **Installing Packages with Chocolatey**
	1. **Check Package Info:**
    ```powershell
    choco info vscode
    ```
    - Displays details about the package, including version, repository, and dependencies.
2. **Install Multiple Packages at Once:**
    ```powershell
    choco install python vscode git wsl2 openssh openvpn -y
    ```
    - Installs **Python, VSCode, Git, WSL2, OpenSSH, OpenVPN**, and any required dependencies.
3. **Refresh Environment Variables (if needed):**
    ```powershell
    RefreshEnv
    ```




### **Installing Windows Terminal**
- Windows Terminal is a modern command-line tool that supports:
	- **Command Prompt, PowerShell, and WSL**.
	- Custom themes, tabs, and key bindings.
- To install:
```powershell
choco install microsoft-windows-terminal -y
```



### **Installing Windows Subsystem for Linux 2 (WSL2)**
- WSL2 allows running Linux distributions natively on Windows without using a hypervisor like **VirtualBox or Hyper-V**.
- #### **Install WSL2 using Chocolatey**
```powershell
choco install wsl2 -y
```
- This installs the latest WSL2 package.
 - #### **Installing a Linux Distribution**
	- Once WSL2 is installed, install a Linux distribution from the **Microsoft Store**:
		- Ubuntu (16.04, 18.04, 20.04 LTS)
		- Kali Linux
		- Debian GNU/Linux
		- Fedora Remix for WSL
		- openSUSE, Alpine WSL, Pengwin, etc.
- To check if WSL is installed:
```powershell
wsl --list --verbose
```
- To start using it, open PowerShell and type:
```powershell
bash
```
- This launches a **Linux terminal** inside Windows.



### **Summary**
- **Chocolatey** simplifies software installation and dependency management.
- **WSL2** allows running Linux within Windows without virtualization.
- **Windows Terminal** provides an enhanced command-line experience.



### **1. Windows Defender Modifications**
- Since penetration testing tools may trigger Windows Defender, exclusions need to be added for specific folders to prevent disruptions.
- **Example Folders for Exclusion**:
1. `C:\Users\your_user_here\AppData\Local\Temp\chocolatey\`
2. `C:\Users\your_user_here\Documents\git-repos\`
3. `C:\Users\your_user_here\Documents\scripts\`
- **Command to Add Exclusions**:
```powershell
Add-MpPreference -ExclusionPath "C:\Users\your_user_here\AppData\Local\Temp\chocolatey\"
```
- Repeat this command for each folder.



### **2. Tool Installation Automation Using Chocolatey**
- **Chocolatey Script Example**:
```powershell
# Choco build script
write-host "*** Initial app install for core tools and packages. ***"

write-host "*** Configuring Chocolatey ***"
choco feature enable -n allowGlobalConfirmation

write-host "*** Beginning install, go grab a coffee. ***"
choco upgrade wsl2 python git vscode openssh openvpn netcat nmap wireshark burp-suite-free-edition heidisql sysinternals putty golang neo4j-community openjdk

write-host "*** Build complete, restoring GlobalConfirmation policy. ***"
choco feature disable -n allowGlobalConfirmation
```
- **Best Practices for Chocolatey Scripting**:
	1. Always use `choco` or `choco.exe` instead of shorthand commands (`cup` or `cinst`).
	2. Use extended options (`--name`) for clarity.
	3. Avoid `--force` in scripts to maintain Chocolatey's expected behavior.



### **3. Automating Git Repository Cloning**
- For tools not available on Chocolatey, clone repositories from GitHub.
- **Example Command**:
```powershell
git clone https://github.com/dafthack/DomainPasswordSpray.git
```
- **Steps**:
	1. Navigate to the scripts directory.
	2. Use `git clone <repository_url>` to download the tool.
	3. Extract and organize scripts/tools as needed.



### **4. Testing VMs for Exploit Validation**
- Testing VMs with different operating system versions and patch levels is crucial to simulate target environments and validate exploits.
	- **Example Workflow**:
	1. Set up a Windows 10 VM (e.g., Version 1607, OS Build 14393).
	2. Apply updates incrementally and create snapshots at each stage.
	3. Use snapshots to quickly revert to a clean state for testing.
- **Tools for Installing Older Windows Versions**:
	- **Chocolatey**
	- **MediaCreationTool.bat**
	- **Microsoft Windows and Office ISO Download Tool**
	- **Rufus**



### **Next Steps**
- After configuring Linux and Windows VMs:
	- Explore setting up and using Virtual Private Servers (VPS) for remote testing and hosting tools.