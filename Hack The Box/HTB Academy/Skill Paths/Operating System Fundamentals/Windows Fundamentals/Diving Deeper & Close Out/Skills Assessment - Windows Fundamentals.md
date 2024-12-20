### Debrief
- **Incident Overview:**
    - A disgruntled marketing employee accessed and deleted confidential HR files.
    - The IT team restored the deleted data from backups, but concerns arose regarding the employee's access to the HR share.
- **Findings from Security Assessment:**
    - IT team may not fully understand how **permissions work in Windows** file sharing.
- **Training and Demonstration Focus:**
    - **File Sharing Best Practices in Windows:**
        - Demonstrate how to properly **set and manage file/folder permissions** using **NTFS** and **Share Permissions**.
        - Emphasize the **principle of least privilege** — ensure users only have the permissions they absolutely need.
        - Use **group policies** to manage and enforce permissions effectively.
    - **Checking Services for Tampering:**
        - Train on using the **command line** (e.g., `net share`, `icacls`) to **view and audit file shares**.
        - Show how to identify any unauthorized changes or tampering with permissions or shares using **Windows Event Logs** or **PowerShell** scripts.
        - Demonstrate using **Windows Security Auditing** to track access and modifications to sensitive files.

> Note: It is important that each step is completed in the order they are presented. Starting with step 1 and working your way through step 8, including all associated specifications with each step. Please know that each step is designed to give you the opportunity to apply the skills & concepts taught throughout this module. Take your time, have fun and feel free to reach out if you get stuck.

- In this demonstration, you are going to do the following steps.
	- #### 1. Creating a shared folder called Company Data
	- #### 2. Creating a subfolder called HR inside of the Company Data folder
	- #### 3. Creating a user called Jim
		- `Uncheck: User must change password at logon`
	- #### 4. Creating a security group called HR
	- #### 5. Adding Jim to the HR security group
	- #### 6. Adding the HR security group to the shared Company Data folder and NTFS permissions list
		- `Remove the default group that is present`
		- `Share Permissions: Allow Change & Read`
		- `Disable Inheritance before issuing specific NTFS permissions`
		- `NTFS permissions: Modify, Read & Execute, List folder contents, Read, Write`
	- #### 7. Adding the HR security group to the NTFS permissions list of the HR subfolder
		- `Remove the default group that is present`
		- `Disable Inheritance before issuing specific NTFS permissions`
		- `NTFS permissions: Modify, Read & Execute, List folder contents, Read, and Write`
	 - #### 8. Using PowerShell to list details about a service



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