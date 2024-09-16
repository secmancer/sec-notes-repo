WSL is a Windows feature that allows the execution of Linux binaries natively on Windows 10 and Windows Server 2019. It was initially designed for developers needing to run Linux command-line tools and applications directly on their Windows systems.

#### WSL Versions
- **WSL 1**: The original version designed to run Linux binaries natively using a compatibility layer.
- **WSL 2**: Released in May 2019, this version introduced a real Linux kernel using a subset of Hyper-V features, offering improved performance and compatibility.

#### Installation
1. **Enable WSL**:
    - Open PowerShell as an Administrator and run:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
**Install a Linux Distro**:
- **Microsoft Store**: Download and install a Linux distribution from the Microsoft Store.
- **Manual Installation**: Download a Linux distribution of your choice, then unpack and install it from the command line.

#### Using WSL
- **Launch Bash Shell**:
    - Run `bash` in the Windows console to open a Bash shell.
    - This shell provides a full Linux environment, including the Linux directory structure.
```
PS C:\htb> bash
```
- **Access Files**:
	- Access the Windows file system via the `/mnt` directory. For example, the C$ volume is accessible at `/mnt/c`.
```
PS C:\htb> ls /
bin dev home lib lib64 media opt root sbin srv tmp var
boot etc init lib32 libx32 mnt proc run Snap sys usr
```
- **View System Information**:
	- Check Linux kernel details and other system information with:
```
PS C:\htb> uname -a
Linux WS01 4.4.0-18362-Microsoft #476-Microsoft Fri Nov 01 16:53:00 PST 2019 x86_64 x86_64 x86_64 GNU/Linux
```