### **Overview**
- **Server Core** (introduced in **Windows Server 2008**) is a **minimalist** Windows Server environment with essential server functionality.
- It requires **lower resources**, has a **smaller attack surface**, and **reduces management overhead** compared to **Desktop Experience** (GUI version).
- **Management** is done through:
    - **Command-line**
    - **PowerShell**
    - **Remote tools** (MMC, RSAT)



### **GUI & Supported Applications**
- Server Core **lacks a full GUI** but supports some graphical tools:
    - **Registry Editor (Regedit)**
    - **Notepad**
    - **Task Manager**
    - **System Information**
    - **Windows Installer**
    - **Sysinternals tools** (e.g., Process Explorer, TCPView)



### **Installation & Configuration**
- **Windows Server 2019** requires a **permanent choice** between **Server Core** and **Desktop Experience** during installation.
- **Sconfig** (a VBScript-based tool) is used for **initial setup** in Server Core:
    - **Network configuration**
    - **Windows Updates**
    - **User account management**
    - **Remote management**
    - **Windows activation**



### **Limitations of Server Core**
- **Some applications are not supported**, such as:
    - **Microsoft System Center Virtual Machine Manager (SCVMM) 2019**
    - **System Center Data Protection Manager 2019**
    - **SharePoint Server 2019**
    - **Project Server 2019**
- **Certain GUI tools are missing**, making management harder.



### **Comparison: Server Core vs. Desktop Experience**

|**Application/Feature**|**Server Core**|**Desktop Experience**|
|---|---|---|
|**Command Prompt**|✅ Available|✅ Available|
|**PowerShell/.NET**|✅ Available|✅ Available|
|**Registry Editor (Regedit)**|✅ Available|✅ Available|
|**Disk Management (diskmgmt.msc)**|❌ Not Available|✅ Available|
|**Server Manager**|❌ Not Available|✅ Available|
|**MMC (mmc.exe)**|❌ Not Available|✅ Available|
|**Event Viewer (eventvwr.msc)**|❌ Not Available|✅ Available|
|**Services (services.msc)**|❌ Not Available|✅ Available|
|**Control Panel**|❌ Not Available|✅ Available|
|**Windows Explorer**|❌ Not Available|✅ Available|
|**Task Manager**|✅ Available|✅ Available|
|**Internet Explorer/Edge**|❌ Not Available|✅ Available|
|**Remote Desktop Services**|✅ Available|✅ Available|



### **Choosing Between Server Core and Desktop Experience**
- **Server Core** is best for:
    - **Minimalist, resource-efficient setups**
    - **Security-focused environments** (smaller attack surface)
    - **Headless server administration**
- **Desktop Experience** is better when:
    - A **GUI is required** for management.
    - Administrators **lack experience** with PowerShell/CLI.
    - Running applications that **require a full Windows environment**.
