### **Understanding Windows File Sharing and Permissions**

**1. **Windows Market Share and Malware:**
- Windows has over 70% of the global desktop OS market share.
- This prevalence makes it a prime target for malware, which often explains why Windows is perceived as less secure.

**2. **Server Message Block (SMB) Protocol:**
- SMB is used in Windows to connect shared resources like files and printers.
- SMB vulnerabilities, like EternalBlue, can lead to severe issues, including ransomware attacks.

**3. **NTFS vs. Share Permissions:**
- **Share Permissions:** Control access to resources over the network.
    - **Full Control:** All actions including modifying permissions.
    - **Change:** Read, edit, delete, and add files.
    - **Read:** View file and folder contents.

- **NTFS Permissions:** Control access on the local file system.
    - **Full Control:** All actions including modifying permissions.
    - **Modify:** View and modify files.
    - **Read & Execute:** Read and run files.
    - **Read:** View contents.
    - **Write:** Write changes and add files.

**4. **NTFS Special Permissions:**
- **Full Control:** Same as NTFS Full Control but applied more granularly.
- **Traverse Folder/Execute File:** Access subfolders even if denied at parent level.
- **List Folder/Read Data:** View contents and open files.
- **Read Attributes/Extended Attributes:** View file attributes.
- **Create Files/Write Data:** Create files and write changes.
- **Create Folders/Append Data:** Create subfolders and add data.
- **Delete Subfolders and Files:** Delete subfolders and files but not parent folders.
- **Delete:** Delete parent folders, subfolders, and files.
- **Read Permissions:** View permissions.
- **Change Permissions:** Change permissions.
- **Take Ownership:** Take ownership of files or folders.

**5. **Creating and Configuring a Network Share:**
- **Creating the Share:**
    - Use the Advanced Sharing option to configure network shares.
    - Access control list (ACL) for shared resources controls access.

- **Testing Access:**
    - Use `smbclient` to test connectivity.
    - Verify Windows Defender Firewall settings if access issues occur.

**6. **Firewall Considerations:**
- **Windows Defender Firewall Profiles:**
    - Public, Private, and Domain profiles control traffic.
    - Firewall rules can block or allow traffic based on network type.

**7. **Mounting and Accessing Shares:**
- **Mounting the Share:**
    - Use `cifs-utils` for mounting shares on Linux-based systems.

- **Viewing Shares:**
    - Use `net share` to view all shared resources.
    - Computer Management can also monitor and manage shares.

- **Event Viewer:**
    - Check Event Viewer for logs related to share access and other system events.

**8. **Practical Insights:**
- **NTFS Inheritance:** Default inheritance can be customized.

- **Administrative Rights:** System administrators have significant influence over permissions and access.

### Questions
- What protocol discussed in this section is used to share resources on the network using Windows? (Format: case sensitive)
	- SMB
	
- What is the name of the utility that can be used to view logs made by a Windows system? (Format: 2 words, 1 space, not case sensitive)
	- Event Viewer

- What is the full directory path to the Company Data share we created?
	- C:\Users\htb-student\Desktop\Company Data