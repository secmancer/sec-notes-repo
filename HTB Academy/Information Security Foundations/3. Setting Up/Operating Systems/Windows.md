Windows is useful as both a victim and a testbed for penetration testers.
- It blends in enterprise environments, making testers less suspicious.
- Easier navigation of Active Directory domains compared to Linux.
- Better for interacting with SMB and network shares.

**Advantages of Building a Custom Platform:**
- Custom-built platforms give a deeper understanding of what runs under the hood.
- Ensures no unnecessary services, reducing risk during engagements.
- Can serve as a testbed for exploits and payloads.
- Building and testing beforehand reduces troubleshooting during live engagements.

**Windows Subsystem for Linux (WSL):**
- Allows Linux tools to run alongside Windows without needing a hypervisor.
- Useful for running Linux-based tools on a Windows host.

**Core Components to Install:**
- **WSL**
- **Visual Studio Code**
- **Python**
- **Git**
- **Chocolatey Package Manager**
- Adjust security settings to prevent Windows Defender from quarantining important tools.

**Hardware Requirements for a Windows 10 VM:**
- **Processor:** 1 GHz or greater, dual-core ideal.
- **RAM:** Minimum 2GB, 4GB or more preferred.
- **Storage:** Minimum 60GB, 80GB or more ideal for tools and updates.
- **Network:** Preferably two network adapters.

**Software Requirements:**
- Use a licensed Windows product to comply with terms of use.
- Start with a **Developer VM**:
    - Windows 10 Version 2004
    - Visual Studio 2019
    - WSL with Ubuntu
    - Pre-configured user: IEUser, password: Passw0rd!

**Core System Changes Before Installing Tools:**
- Update the system to the latest version.
- Install **WSL** and **Chocolatey**.
- Exclude necessary tools from Windows Defender scans.
- Take a snapshot of the host for backup.

**Installing and Managing Updates via PowerShell:**
- Check the execution policy:
    - `Get-ExecutionPolicy -List`
    - Temporarily set the execution policy for the process: `Set-ExecutionPolicy Unrestricted -Scope Process`.
- Install the **PSWindowsUpdate** module:
    - `Install-Module PSWindowsUpdate`
    - Apply updates: `Install-WindowsUpdate -AcceptAll`
    - Reboot the system: `Restart-Computer -Force`.

### Chocolatey Package Manager
- Chocolatey is a free and open-source software package management solution for Windows.
- It automates the installation of software packages and handles dependencies.
- Compatible with automation tools such as PowerShell, Ansible, and more.
- Allows for centralized management of tools and scripts.

**Key Features:**
- **Automation**: Automates software installations, updates, and configurations.
- **Dependencies**: Automatically handles dependencies required by the packages.
- **Integration**: Works with PowerShell and other automation tools for efficient deployment.

**Installation Process:**
- Install via PowerShell:
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
- Downloads and installs Chocolatey.
- Adds `choco` command to system path.
- Restart PowerShell to ensure changes take effect.

**Updating Chocolatey**:
- Update to the latest version of Chocolatey using the following command:
```
choco upgrade chocolatey -y
```
- Ensures that Chocolatey is up-to-date.

**Installing Packages:**
- Install packages using the command:
```
choco install pkg1 pkg2 pkg3
```
- Installs multiple packages at once (e.g., Python, VSCode, Git).

**Example**:
```
choco install python vscode git wsl2 openssh openvpn
```
- Installs listed packages along with necessary dependencies.****

**Package Information:**
- View details about a package using:
```
choco info pkg
```
- Shows metadata such as version, description, and download link.****

**Helpful Commands:**
- **Refreshing Environment Variables**:
```
RefreshEnv
```
- Updates PowerShell session with any new environment variables after installing packages.

**Automation:**
- Chocolatey allows automating the installation of frequently used tools through scripting.
- A **packages.config** file (XML format) can be used to install a list of packages at once.

**Commonly Used Packages for Penetration Testing:**
- Python
- VSCode
- Git
- WSL2
- OpenSSH
- OpenVPN

Windows Terminal is a modern, customizable terminal emulator from Microsoft.
- It supports multiple shell environments, including:
	- Command Prompt
	- PowerShell
	- Windows Subsystem for Linux (WSL)


**Installation using Chocolatey:**
1. Open PowerShell with administrator privileges.
2. Run the following command to install Windows Terminal:
```
choco install microsoft-windows-terminal
```

**Key Points:**
- If a system reboot is pending, Chocolatey may ignore it based on your settings.
- After installation, the terminal can be used for various command-line tasks with any of the supported shells.

WSL2 is the second version of Microsoft’s architecture to run Linux distributions on Windows.
- It allows running Bash scripts and Linux applications such as Vim and Python directly on Windows.
- No need for a hypervisor (like VirtualBox or Hyper-V).

**Benefits:**
- Hybrid environment: Use Linux tools alongside Windows.
- Interact with the Windows file-system from Linux.

**Installation using Chocolatey:**
1. Install WSL2 by running the following command:
```
choco install wsl2
```

**Supported Linux Distributions:**
- Ubuntu (16.04 LTS, 18.04 LTS, 20.04 LTS)
- openSUSE Leap 15.1
- SUSE Linux Enterprise Server 12 SP5, 15 SP1
- Kali Linux
- Debian GNU/Linux
- Fedora Remix for WSL
- Pengwin and Pengwin Enterprise
- Alpine WSL

**How to Use WSL2:**
- After installing a Linux distribution from the Microsoft Store, open PowerShell and run:
```
bash
```
- This starts the Linux environment within Windows, allowing for seamless operations.

Since the platform is being used for penetration testing, Windows Defender may flag some tools as harmful.
- To prevent Windows Defender from disrupting operations, it's essential to add folder exclusions for key tools and scripts.

**Exempting Folders from Windows Defender:**
- Add exclusions to ensure Defender does not interfere with your tools:
```
C:\Users\your_user\AppData\Local\Temp\chocolatey\
C:\Users\your_user\Documents\git-repos\
C:\Users\your_user\Documents\scripts\
```
- To add these exclusions via PowerShell, use:
```
Add-MpPreference -ExclusionPath "C:\Users\your_user\AppData\Local\Temp\chocolatey\"
```
- Repeat this step for each folder you want to exclude.

**Automating with Chocolatey:**
- Use Chocolatey for package management to streamline the installation of core tools and applications.
- Create a PowerShell script to automate the initial install of key packages.

Sample PowerShell Script:
```
# Choco build script

write-host "*** Initial app install for core tools and packages. ***"

write-host "*** Configuring chocolatey ***"
choco feature enable -n allowGlobalConfirmation

write-host "*** Beginning install, go grab a coffee. ***"
choco upgrade wsl2 python git vscode openssh openvpn netcat nmap wireshark burp-suite-free-edition heidisql sysinternals putty golang neo4j-community openjdk

write-host "*** Build complete, restoring GlobalConfirmation policy. ***"
choco feature disable -n allowGlobalConfirmation
```

**Best Practices for Chocolatey Scripts:**
- Always use `choco` or `choco.exe` for commands, avoiding shortcuts like `cup` or `cinst`.
- Use extended options like `--name` instead of shorthand like `-n`.
- Avoid using `--force` in scripts to maintain Chocolatey’s default behavior.

**Cloning GitHub Repositories:**
- Not all tools are available on Chocolatey, but most can be sourced from GitHub.

Sample Git Clone Command:
```
git clone https://github.com/dafthack/DomainPasswordSpray.git
```
- The repository is cloned into the designated folder, where you can access and run the tools.

Folder Structure Example:
```
Directory: C:\Users\your_user\Documents\scripts

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----               4/16/2021   4:58 PM           DomainPasswordSpray
```

Testing VMs for penetration testing is essential to simulate target environments and test exploits before running them on live systems.

Setting up VMs with different operating system versions and patch levels helps prepare for a variety of scenarios.

**Why Use Testing VMs:**
- Test how systems and exploits will react in a controlled environment.
- Mirrors the target systems to ensure reliability when executing the exploit on real machines.

**Windows 10 VM Example:**
- Create Windows 10 VMs based on different versions, patches, and releases (e.g., Windows 10 version 1607, OS build 14393).
- Instead of setting up multiple VMs, use **snapshots** to save configurations at various patch levels.

**Steps for Creating Windows 10 Snapshots:**
1. Start with a clean Windows 10 installation.
2. Apply updates and patches incrementally, creating a snapshot after each patch.
3. Download patches and updates from the **Microsoft Update Catalog** using the KB article number.

### Tools for Installing Older Windows Versions
These tools can help download and install older versions of Windows to create your testing VMs.
- **Chocolatey**
- **MediaCreationTool.bat**
- **Microsoft Windows and Office ISO Download Tool**
- **Rufus**