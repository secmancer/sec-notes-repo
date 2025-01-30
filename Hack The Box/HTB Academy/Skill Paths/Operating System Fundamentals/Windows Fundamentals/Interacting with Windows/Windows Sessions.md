### **1. Interactive vs. Non-Interactive Sessions**
- **Interactive Sessions (Local Logon):**
    - **Requires user authentication (username & password).**
    - Can be initiated by:
        - **Direct login** (physically or remotely).
        - **Secondary logon** (`runas` command).
        - **Remote Desktop (RDP) login.**
- **Non-Interactive Sessions:**
    - **Used by system processes, services, and scheduled tasks.**
    - **Do not require login credentials.**
    - **Have no associated passwords.**



### **2. Types of Non-Interactive Accounts**

|**Account**|**Description**|**Privileges**|
|---|---|---|
|**Local System Account** (`NT AUTHORITY\SYSTEM`)|Most powerful built-in Windows account. Runs OS-related tasks and services.|More powerful than local admins.|
|**Local Service Account** (`NT AUTHORITY\LocalService`)|Runs services with minimal privileges. Has similar permissions to a standard user.|**Limited** access to system resources.|
|**Network Service Account** (`NT AUTHORITY\NetworkService`)|Used by services that need to authenticate over a network.|Similar to Local Service but **can access network resources**.|



### **Key Differences**
- **Local System Account (`SYSTEM`)** → **Highest privileges**, full control over system.
- **Local Service (`LocalService`)** → **Minimal privileges**, runs local services.
- **Network Service (`NetworkService`)** → **Similar to LocalService but can authenticate on the network.**



### **3. Security Implications**
-  **`SYSTEM` account can be abused for privilege escalation.**  
- **Services running as `SYSTEM` have full control and can be exploited.**  
- **Least privilege principle should be applied to service accounts.**