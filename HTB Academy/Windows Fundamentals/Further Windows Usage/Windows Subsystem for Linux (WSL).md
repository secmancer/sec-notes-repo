### Overview of WSL
- **Purpose**: WSL enables the execution of Linux binaries natively on Windows 10 and Windows Server 2019, catering primarily to developers needing Linux command-line tools and scripts.
- **Versions**:
    - **WSL 1**: Original version, introduced a compatibility layer to run Linux binaries.
    - **WSL 2**: Released in May 2019, introduces a full Linux kernel utilizing Hyper-V features for improved performance and compatibility.

### Installation
1. **Enable WSL Feature**:
    - Open PowerShell as Administrator.
    - Run: `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
    - This installs the necessary components for WSL.
2. **Install a Linux Distro**:
    
    - **Microsoft Store**: Search for and install a Linux distribution like Ubuntu, Debian, or Fedora.
    - **Manual Installation**: Download a Linux distro package, then follow instructions to unpack and install it from the command line.

### Using WSL
1. **Launch Bash Shell**:
    - Open a Windows console (Command Prompt or PowerShell) and type `bash` to start a Bash shell.
    - Alternatively, use the installed distro’s executable (e.g., `ubuntu`).
2. **Linux Environment**:
    - **Directory Structure**: Standard Linux directories are available.
	    - ls /
	- Output example:
		- bin  dev  home  lib  lib64  media  opt  root  sbin  srv  tmp  var
		- boot  etc  init  lib32  libx32  mnt  proc  run  snap  sys  usr
	- **Accessing Windows Files**: Access Windows files through the `/mnt` directory (e.g., `/mnt/c/` for C: drive).
3. **Run Commands and Manage Packages**:
	- Use Linux commands and package managers just as you would on a native Linux system.
		- uname -a
	- Output example:
		- Linux WS01 4.4.0-18362-Microsoft #476-Microsoft Fri Nov 01 16:53:00 PST 2019 x86_64 x86_64 x86_64 GNU/Linux

### Key Points
- **Integration**: WSL allows seamless integration between Linux and Windows environments, making it easy to run Linux commands and scripts on a Windows system.
- **File Access**: Access Windows files and directories from within the WSL environment through the `/mnt` directory.

WSL enhances productivity by enabling the use of Linux tools directly within a Windows environment, facilitating development and cross-platform tasks.