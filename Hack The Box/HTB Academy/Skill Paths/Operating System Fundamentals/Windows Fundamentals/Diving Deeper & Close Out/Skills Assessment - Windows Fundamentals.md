## **1. Create a Shared Folder (Company Data)**
- Open **File Explorer** and navigate to the desired location.
- Create a new folder:
    - **Right-click > New > Folder**
    - Name it **Company Data**
- **Enable Sharing**:
    - **Right-click Company Data > Properties > Sharing tab > Advanced Sharing**
    - Check **"Share this folder"**
    - Click **"Permissions"**



## **2. Create HR Subfolder inside Company Data**
- Inside the **Company Data** folder, create another folder:
    - **Right-click > New > Folder**
    - Name it **HR**



## **3. Create a User (Jim)**
- Open **Computer Management** (`compmgmt.msc`)
- Navigate to **Local Users and Groups > Users**
- **Right-click > New User**
    - **Username**: `Jim`
    - **Uncheck**: _User must change password at logon_
    - Set a password and confirm



## **4. Create a Security Group (HR Group)**
- Open **Computer Management**
- Navigate to **Local Users and Groups > Groups**
- **Right-click > New Group**
    - **Group Name**: `HR`
    - Click **Create**



## **5. Add Jim to HR Security Group**
- In **Computer Management**, navigate to **Local Users and Groups > Groups**
- **Double-click the HR group** > Click **Add**
- Type **Jim** and click **OK**



## **6. Configure Sharing & NTFS Permissions for Company Data**
1. **Remove Default Group**
    - Go to **Company Data Properties > Security tab**
    - Click **Edit > Remove default group (e.g., Everyone)**
2. **Share Permissions (HR Group)**
    - Click **Sharing tab > Advanced Sharing > Permissions**
    - **Remove default group**, then **Add HR group**
    - Set **Allow: Change & Read**
3. **Disable Inheritance (NTFS Permissions)**
    - Go to **Company Data Properties > Security > Advanced**
    - Click **Disable inheritance > Convert existing permissions**
4. **Set NTFS Permissions for HR Group**
    - Click **Add > HR Group**
    - Grant **Modify, Read & Execute, List Folder Contents, Read, Write**



## **7. Configure NTFS Permissions for HR Subfolder**
1. **Remove Default Group**
    - Navigate to **HR folder Properties > Security tab**
    - Click **Edit > Remove default group**
2. **Disable Inheritance**
    - Go to **Security > Advanced**
    - Click **Disable inheritance > Convert existing permissions**
3. **Set NTFS Permissions for HR Group**
    - Click **Add > HR Group**
    - Grant **Modify, Read & Execute, List Folder Contents, Read, Write**



## **8. Use PowerShell to List Service Details**
- Open **PowerShell** and run:
    ```powershell
    Get-Service | Where-Object { $_.DisplayName -like "*Windows Defender*" }
    ```    
- OR, for a specific service like Windows Update:
    ```powershell
    Get-Service -Name wuauserv
    ```
- Output will show:
    - **Service Name**
    - **Display Name**
    - **Status (Running, Stopped)**
    - **Start Type (Automatic, Manual, Disabled)**



### **Key Takeaways**
- **Folder Sharing**: Use **specific security groups** instead of **default permissions**.
- **NTFS Permissions**: Use **Disable Inheritance** before setting **granular permissions**.
- **PowerShell for Services**: `Get-Service` helps monitor running services for **security checks**.



### Questions
- What is the name of the group that is present in the Company Data Share Permissions ACL by default?
	- everyone
- What is the name of the tab that allows you to configure NTFS permissions?
	- security
- What is the name of the service associated with Windows Update?
	- wuauserv
- List the SID associated with the user account Jim you created.
	- S-1-5-21-2614195641-1726409526-3792725429-1006
- List the SID associated with the HR security group you created.
	- S-1-5-21-2614195641-1726409526-3792725429-1007