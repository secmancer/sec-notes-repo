### **Overview**
- **Windows security** is complex due to the many built-in applications, settings, and features that can be misconfigured or exploited.
- Over time, **Microsoft** has improved security by adding **hardening features, detection mechanisms, and intrusion prevention** tools.



### **Security Identifier (SID)**
- Each **user, computer, thread, or process** has a unique **SID** (Security Identifier).
- **SID Structure:**
    ```
    (SID)-(revision level)-(identifier-authority)-(subauthority1)-(subauthority2)-(etc)
    ```
- Example:
    ```powershell
    whoami /user
    ```
    ```
    User Name      SID
    ws01\bob      S-1-5-21-674899381-4069889467-2080702030-1002
    ```
- Components:
    - **Identifier Authority** – Identifies the system or domain.
    - **RID (Relative ID)** – Distinguishes between accounts (Admin, Guest, User).



### **Security Accounts Manager (SAM) & Access Control Entries (ACE)**
- **SAM** controls **user rights** and authentication.
- **Access Control Lists (ACLs)** use **Access Control Entries (ACEs)** to grant or deny permissions.
- **Types of ACLs**:
    - **DACL (Discretionary ACL)** – Defines which users can access an object.
    - **SACL (System ACL)** – Used for auditing access attempts.
- **Local Security Authority (LSA)** validates **access tokens**, which include the **SID** and other security settings.



### **User Account Control (UAC)**
- **Prevents malware** from making unauthorized changes.
- Uses **Admin Approval Mode** to require confirmation for actions needing admin rights.
- Standard users **must enter credentials** for elevated tasks.



### **Windows Registry**
- The **Registry** is a **hierarchical database** storing system settings.
- Open it via:
    ```powershell
    regedit
    ```
- **Root Keys:**
    - `HKEY_LOCAL_MACHINE (HKLM)` – System-wide settings.
    - `HKEY_CURRENT_USER (HKCU)` – User-specific settings.
- **Important Paths:**
    - System registry: `C:\Windows\System32\Config\`
    - User registry: `C:\Users\<USERNAME>\Ntuser.dat`
- **Registry Key Types:**
    |**Type**|**Description**|
    |---|---|
    |REG_DWORD|32-bit number|
    |REG_QWORD|64-bit number|
    |REG_SZ|String|
    |REG_BINARY|Binary data|
    |REG_MULTI_SZ|Multiple strings|



### **Run and RunOnce Registry Keys**
- **Persist software across reboots** (can be abused for persistence).
- Keys:
    ```powershell
    HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
    HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce
    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
    ```
- Example:
    ```powershell
    reg query HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
    ```
- Output:
    ```
    SecurityHealth   REG_EXPAND_SZ    %windir%\system32\SecurityHealthSystray.exe
    Greenshot        REG_SZ    C:\Program Files\Greenshot\Greenshot.exe
    ```



### **Application Whitelisting**
- **Whitelisting** allows **only approved applications** to run.
- **Blacklisting** blocks known **malicious software** but allows everything else.
- **Whitelisting is preferred** for high-security environments.



### **AppLocker**
- **Microsoft's whitelisting tool** (introduced in **Windows 7**).
- **Controls which apps, scripts, and DLLs can run**.
- Supports rules based on:
    - **Publisher (digital signature)**
    - **File path**
    - **File hash**
- **Audit Mode** allows testing before enforcement.



### **Local Group Policy**
- **Manages system settings** via **Group Policy Objects (GPOs)**.
- Open with:
    ```powershell
    gpedit.msc
    ```
- **Can be used to:**
    - **Enable Credential Guard** (protects passwords).
    - **Restrict user privileges** (e.g., disable certain programs).
    - **Configure AppLocker policies**.



### **Windows Defender Antivirus**
- **Built-in antivirus**, renamed from **Windows Defender**.
- **Features:**
    - **Real-time protection**
    - **Cloud-based scanning**
    - **Tamper Protection** (prevents unauthorized changes)
    - **Controlled folder access** (anti-ransomware)
- Check Defender status:
    ```powershell
    Get-MpComputerStatus | findstr "True"
    ```
- Example Output:
    ```
    AMServiceEnabled                : True
    AntispywareEnabled              : True
    AntivirusEnabled                : True
    BehaviorMonitorEnabled          : True
    IoavProtectionEnabled           : True
    IsTamperProtected               : True
    ```
- **Effectiveness:**
    - Competes with **paid antivirus solutions**.
    - Detects **common hacking tools** (e.g., **Metasploit, Mimikatz**).
    - Can be bypassed with advanced **evasion techniques**.



### **Key Takeaways**
- **Windows Security** is built on **SIDs, ACLs, UAC, and Defender**.
- **Registry settings and Group Policy** can be used for **security hardening**.
- **Application Whitelisting & AppLocker** improve security by limiting executable permissions.
- **Windows Defender is strong** but must be combined with **other security best practices**.



### Questions
- Find the SID of the bob.smith user.
	- S-1-5-21-2614195641-1726409526-3792725429-1003
- What 3rd party security application is disabled at startup for the current user? (The answer is case sensitive).
	- NordVPN