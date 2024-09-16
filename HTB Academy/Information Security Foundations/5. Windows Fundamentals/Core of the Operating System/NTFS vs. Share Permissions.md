### Overview of Windows and Malware
- **Market Share**: Microsoft Windows holds over 70% of the global desktop operating system market share.
- **Malware Targeting**: The high market share makes Windows a prime target for malware authors, as it is a high-value target. This contributes to the perception that Windows is less secure compared to other operating systems.
- **Technical Fallacy**: No operating system is immune to malware. Any OS with software can be targeted by a virus, which is defined as software with malicious intent.

### SMB and NTFS Permissions
- **Server Message Block (SMB)**: Protocol used in Windows to connect shared resources like files and printers. Commonly used in various enterprise environments.
- **EternalBlue Vulnerability**: An unpatched vulnerability in SMBv1 that can lead to ransomware attacks and is still a concern for unpatched Windows systems.

## Share permissions
![[Screenshot_20240912_152522.png]]

## NTFS Basic and special permissions

![[Screenshot_20240912_152528.png]]

![[Screenshot_20240912_152553.png]]
#### SMB Diagram
- Visual representation of SMB’s function can help understand its role in network resource sharing.


### NTFS vs. Share Permissions

#### Share Permissions:
- **Full Control**: Allows all actions provided by Change and Read permissions plus the ability to change NTFS permissions.
- **Change**: Permits reading, editing, deleting, and adding files and subfolders.
- **Read**: Allows viewing of file and folder contents.

#### NTFS Basic Permissions:
- **Full Control**: Allows adding, editing, moving, deleting files and folders, and changing NTFS permissions.
- **Modify**: Permission to view and modify files and folders.
- **Read & Execute**: Permission to read files and execute programs.
- **List Folder Contents**: Permission to view a listing of files and subfolders.
- **Read**: Permission to read file contents.
- **Write**: Permission to write changes to a file and add new files to a folder.
- **Special Permissions**: Advanced permission options.

#### NTFS Special Permissions:
- **Full Control**: Includes all NTFS permissions and the ability to change NTFS permissions.
- **Traverse Folder/Execute File**: Access subfolders and execute programs.
- **List Folder/Read Data**: View files and folders and open files.
- **Read Attributes**: View basic file or folder attributes.
- **Read Extended Attributes**: View extended file or folder attributes.
- **Create Files/Write Data**: Create files and make changes.
- **Create Folders/Append Data**: Create subfolders and add data to files.
- **Write Attributes**: Change file attributes.
- **Write Extended Attributes**: Change extended attributes.
- **Delete Subfolders and Files**: Delete subfolders and files.
- **Delete**: Delete parent folders, subfolders, and files.
- **Read Permissions**: Read permissions of a folder.
- **Change Permissions**: Change permissions of a file or folder.
- **Take Ownership**: Take ownership of a file or folder.

### Creating a Network Share
- **Folder Creation**: Create a folder on the Windows 10 desktop.
- **Sharing**: Use Advanced Sharing to configure the share. This process involves setting permissions and naming the share.
- **Access Control List (ACL)**: The ACL for shared resources includes access control entries (ACEs) for users and groups.

#### Using `smbclient`:
- **List Shares**: Use `smbclient -L SERVER_IP -U username` to list available shares.
- **Connect to Share**: Use `smbclient '\\SERVER_IP\ShareName' -U username` to connect to a share.

### Windows Defender Firewall
- **Potential Blockage**: The firewall may block SMB share access if the connection is from a non-workgroup system.
- **Firewall Profiles**:
    - **Public**
    - **Private**
    - **Domain**
- **Firewall Rules**: Enable predefined rules or custom exceptions rather than deactivating the firewall. Firewalls can also be centrally managed in Windows Domain environments through Group Policy.

### Accessing and Monitoring Shares
- **Mounting a Share**: Use the `mount` command with CIFS to create a mount point on Linux.
    - Example: `sudo mount -t cifs -o username=username,password=password //IP_Address/ShareName /mount/point`
    - Install CIFS utilities if needed: `sudo apt-get install cifs-utils`
- **Viewing Shares**:
    - **`net share` Command**: View all shared folders on a system.
    - **Computer Management**: Use Computer Management to monitor shared resources.
    - **Event Viewer**: Check Event Viewer for logs of actions related to shared folders.

### Key Takeaways
- NTFS and share permissions both apply to shared resources but at different levels: NTFS permissions for local access and share permissions for network access.
- Understanding both permission types and how to configure and monitor them is crucial for managing security and access to shared resources in a Windows environment.


## Questions:
- What protocol discussed in this section is used to share resources on the network using Windows? (Format: case sensitive)
	- SMB
- What is the name of the utility that can be used to view logs made by a Windows system? (Format: 2 words, 1 space, not case sensitive)
	- Event Viewer
- What is the full directory path to the Company Data share we created?
	- C:\Users\htb-student\Desktop\Company Data