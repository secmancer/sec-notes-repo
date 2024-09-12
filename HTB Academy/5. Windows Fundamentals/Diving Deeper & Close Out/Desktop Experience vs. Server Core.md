**Windows Server Core** was introduced with Windows Server 2008 as a minimalistic server environment designed to contain only essential server functionalities. It provides several advantages over the Desktop Experience (GUI) version:
- **Lower Management Requirements**: Due to its minimalistic nature, Server Core requires less maintenance.
- **Smaller Attack Surface**: Fewer components mean a reduced risk of vulnerabilities.
- **Reduced Resource Usage**: Server Core consumes less disk space and memory compared to the GUI version.
#### Management and Configuration
- **Command-Line Interface**: All configuration and maintenance tasks are performed via the command-line interface or PowerShell.
- **Remote Management**: Server Core can be managed remotely using MMC or Remote Server Administration Tools (RSAT).
- **Sconfig Tool**: Provides a text-based interface for initial setup and common tasks:
    - Configuring networking
    - Checking/installing Windows updates
    - Account management
    - Configuring remote management
    - Activating Windows

#### Graphical Program Support
While Server Core does not include a GUI, it supports some graphical programs:
- **Registry Editor**
- **Notepad**
- **System Information**
- **Windows Installer**
- **Task Manager**
- **PowerShell**
- **Sysinternals Suite Tools**:
    - Active Directory Explorer
    - Process Explorer
    - Process Monitor
    - TCPView

#### Limitations
Certain server applications are incompatible with Server Core:
- Microsoft Server Virtual Machine Manager 2019 (SCVMM)
- System Center Data Protection Manager 2019
- SharePoint Server 2019
- Project Server 2019

#### Installation and Conversion
- **Selection at Installation**: You must choose between Server Core and Desktop Experience during installation. It is not possible to convert from Server Core to Desktop Experience once installed.


![[Screenshot_20240912_154803.png]]