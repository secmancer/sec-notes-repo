### 1. Create a Shared Folder Called "Company Data"
1. **Create the Folder:**
    - Navigate to the location where you want to create the folder (e.g., C:\ or D:).
    - Right-click in the directory, select **New** > **Folder**, and name it **Company Data**.
2. **Share the Folder:**
    - Right-click the **Company Data** folder, select **Properties**.
    - Go to the **Sharing** tab.
    - Click on **Advanced Sharing**.
    - Check the box for **Share this folder**.
    - Click **Permissions** to set share permissions.

### 2. Create a Subfolder Called "HR" Inside the "Company Data" Folder
1. **Create the Subfolder:**
    - Open the **Company Data** folder.
    - Right-click inside the folder, select **New** > **Folder**, and name it **HR**.

### 3. Create a User Called "Jim"
1. **Create the User:**
    - Open **Computer Management** (right-click **This PC** or **My Computer** on the desktop or in File Explorer and select **Manage**).
    - Navigate to **Local Users and Groups** > **Users**.
    - Right-click **Users**, select **New User**.
    - Enter **Jim** as the username.
    - Uncheck **User must change password at next logon**.
    - Set a password and complete the creation process.

### 4. Create a Security Group Called "HR"
1. **Create the Security Group:**
    - In **Computer Management**, navigate to **Local Users and Groups** > **Groups**.
    - Right-click **Groups**, select **New Group**.
    - Enter **HR** as the group name.
    - Click **Create** to finalize.

### 5. Add Jim to the HR Security Group
1. **Add User to the Group:**
    - In **Computer Management**, navigate to **Local Users and Groups** > **Groups**.
    - Double-click the **HR** group.
    - Click **Add**.
    - Enter **Jim** and click **Check Names** to verify.
    - Click **OK** to add Jim to the group.

### 6. Add the HR Security Group to the Shared "Company Data" Folder and NTFS Permissions List
1. **Remove Default Group:**
    - Right-click the **Company Data** folder, select **Properties**.
    - Go to the **Sharing** tab and click **Advanced Sharing**.
    - Click **Permissions**.
    - Remove the default group (e.g., **Everyone**).
2. **Set Share Permissions:**
    - Add the **HR** group.
    - Check **Change** and **Read** permissions.
    - Click **Apply** and **OK**.
3. **Configure NTFS Permissions:**
    - Go to the **Security** tab in the **Company Data** folder properties.
    - Click **Advanced**.
    - Click **Disable inheritance** and choose **Convert inherited permissions into explicit permissions on this object**.
    - Click **Add**, enter **HR**, and configure permissions:
        - **Modify**
        - **Read & Execute**
        - **List folder contents**
        - **Read**
        - **Write**
    - Click **Apply** and **OK**.

### 7. Add the HR Security Group to the NTFS Permissions List of the HR Subfolder
1. **Remove Default Group:**
    - Right-click the **HR** subfolder, select **Properties**.
    - Go to the **Security** tab and click **Advanced**.
    - Remove the default group (e.g., **Everyone**).
2. **Configure NTFS Permissions:**
    - Click **Disable inheritance** and choose **Convert inherited permissions into explicit permissions on this object**.
    - Click **Add**, enter **HR**, and configure permissions:
        - **Modify**
        - **Read & Execute**
        - **List folder contents**
        - **Read**
        - **Write**
    - Click **Apply** and **OK**.

### 8. Use PowerShell to List Details About a Service
1. **Open PowerShell:**
    - Press `Win + X` and select **Windows PowerShell** (or **Windows Terminal** if PowerShell is the default).
2. **List Service Details:**
    - Use the following command to list details about a specific service (e.g., the **wuauserv** service): Get-Service -Name wuauserv | Format-List *
	- Replace **wuauserv** with the service you want to check. This command will display detailed information about the service, including its status and configuration.

### Questions:
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