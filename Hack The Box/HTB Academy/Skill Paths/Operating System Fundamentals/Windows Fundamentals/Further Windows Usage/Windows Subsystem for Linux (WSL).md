### **Overview**
- WSL allows Linux binaries to run natively on **Windows 10** and **Windows Server 2019**.
- Originally intended for developers needing **Bash, Ruby, and Linux command-line tools** (e.g., `sed`, `awk`, `grep`).
- **WSL 2 (May 2019)** introduced a real Linux kernel using **Hyper-V features**.
- #### **Installation**
	- Run PowerShell as **Administrator** and enable WSL:
    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```
- After enabling WSL, install a **Linux distribution** via:
    - **Microsoft Store**
    - **Manual download** and unpacking via the command line.
- #### **Usage**
	- WSL provides **Bash.exe**, which can be launched by typing:
    ```powershell
    bash
    ```
- Provides a **Linux-like environment** with a familiar directory structure.
- #### **Directory Structure**
	- Running `ls /` in WSL returns a **standard Linux file structure**:
    ```
    bin  dev  home  lib  lib64  media  opt  root  sbin  srv  tmp  var
    boot  etc  init  lib32  libx32  mnt  proc  run  snap  sys  usr
    ```
- Windows drives (e.g., `C$`) are accessible via the `/mnt` directory.
- #### **Checking System Information**
	- Use `uname -a` to display Linux kernel details:
    ```powershell
    PS C:\htb> uname -a
    ```
- Output:
    ```
    Linux WS01 4.4.0-18362-Microsoft #476-Microsoft Fri Nov 01 16:53:00 PST 2019 x86_64 x86_64 x86_64 GNU/Linux
    ```
- #### **Key Features**
	- **Seamless integration** between Windows and Linux environments.
	- Can install and update packages like a regular Linux system.
	- Ability to run **Linux-native applications** and scripts directly on Windows.