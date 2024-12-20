### Introduction
- **Windows Market Share:**
    - Microsoft owns over **70%** of the global desktop OS market, which makes Windows a primary target for malware.
- **Malware Targeting Windows:**
    - Malware authors target Windows because it is a high-value platform with a large user base.
    - No OS is immune to malware; if software can be written for it, so can viruses.
    - Malware, including ransomware, can spread over networks using shared resources with weak permissions.
- **EternalBlue Vulnerability:**    
    - The **EternalBlue** vulnerability, especially in unpatched systems running **SMBv1**, is still a significant threat, often exploited by ransomware.
- **Server Message Block (SMB):**
    - SMB is a protocol used by Windows to share resources (e.g., files, printers) in enterprise environments.
- This idea is shown below.
![[smb_diagram_png.png]]
- Note: Any time you see a visualization/diagram of a concept, take your time to understand it thoroughly. 
- A picture can be worth a thousand words but very tempting to skip over when reading.
- NTFS permissions and share permissions are often understood to be the same. 
- Please know that they are not the same but often apply to the same shared resource. 
- Let’s take a look at the individual permissions that can be set to secure/grant objects access to a network share hosted on a Windows OS running the NTFS file system.
![[Screenshot_20241109_112814.png]]
![[Screenshot_20241109_112819.png]]
![[Screenshot_20241109_112837.png]]
- Keep in mind that NTFS permissions apply to the system where the folder and files are hosted. 
- Folders created in NTFS inherit permissions from parent folders by default. It is possible to disable inheritance to set custom permissions on parent and subfolders, as we will do later in this module.
- The share permissions apply when the folder is being accessed through SMB, typically from a different system over the network. 
- This means someone logged in locally to the machine or via RDP can access the shared folder and files by simply navigating to the location on the file system and only need to consider NTFS permissions. 
- The permissions at the NTFS level provide administrators much more granular control over what users can do within a folder or file.



### Creating a Network Share
- To get a solid fundamental understanding of SMB and it's relationship to NTFS, we will create a network share on the `Windows 10 target box`.

> Note: It is an ideal learning experience to have the Pwnbox open full screen on a separate monitor so we may have at least one display dedicated to displaying the written content and one display for the boxes we are interacting with. Alternatively, if we only have access to one display, we can use that one for interactions with boxes and a smartphone or tablet to reference the written content.

- In this case, we will create a shared folder by first creating a new folder on the Windows 10 desktop. 
- Keep in mind that in most large enterprise environments, shares are created on a Storage Area Network (SAN), Network Attached Storage device (NAS), or a separate partition on drives accessed via a server operating system like Windows Server.
- If we ever come across shares on a desktop operating system, it will either be a small business or it could be a beachhead system used by a penetration tester or malicious attacker to gather and exfiltrate data.
- We will go through this process using the GUI in Windows.
- #### Creating the Folder
![[creating_directory_png.png]]
- We are going to use the `Advanced Sharing` option to configure our share.
- #### Making the Folder a Share
![[configuring_share_png.png]]
- Notice how the share name automatically defaults to the name of the folder. 
- Also, we can see that it is possible to limit the number of users that can be connected to this share simultaneously.
- In a real-world environment it is a good practice for administrators to set this number according to the number of users that regularly need access to the resource being shared.
- Similar to NTFS permissions, there is an `access control list` (`ACL`) for shared resources. 
- We can consider this the SMB permissions list. 
- Keep in mind that with shared resources, both the SMB and NTFS permissions lists apply to every resource that gets shared in Windows. 
- The ACL contains `access control entries` (`ACEs`). 
- Typically these ACEs are made up of `users` & `groups` (also called security principals) as they are a suitable mechanism for managing and tracking access to shared resources.
- Notice the default access control entry and permissions settings.
- #### Share Permissions ACL (Sharing Tab)
![[share_permissions_png.png]]
- For now, we are going to apply these settings to test the effect of this ACL and the permissions applied as-is. 
- We will test connectivity from the Pwnbox by opening terminal and using `smbclient`.
- Note: A server is technically a software function used to service the requests of a client. In this case, the Pwnbox is our client, and the Windows 10 target box is our server.



### Using smbclient to list avaliable shares
```shell-session
secmancer@htb[/htb]$ smbclient -L SERVER_IP -U htb-student
Enter WORKGROUP\htb-student's password: 

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	Company Data    Disk      
	IPC$            IPC       Remote IPC
```



### Connecting to the Company Data Share
```shell-session
secmancer@htb[/htb]$ smbclient '\\SERVER_IP\Company Data' -U htb-student
Password for [WORKGROUP\htb-student]:
Try "help" to get a list of possible commands.

smb: \> 
```
- What could potentially block us from accessing this share if all our entries are correct and our permissions list has the Everyone group present with at least Read permissions?



### Windows Defender Firewall Considerations
- It is the Windows Defender Firewall that could potentially be blocking access to the SMB share. 
- Since we are connecting from a Linux-based system the firewall has blocked access from any device that is not joined to the same `workgroup`. 
- It is also important to note that when a Windows system is part of a workgroup, all `netlogon` requests are authenticated against that particular Windows system's `SAM` database. 
- When a Windows system is joined to a Windows Domain environment, all netlogon requests are authenticated against `Active Directory`. 
- The primary difference between a workgroup and a Windows Domain in terms of authentication, is with a workgroup the local SAM database is used and in a Windows Domain a centralized network-based database (Active Directory) is used. 
- We must know this information when attempting to logon & authenticate with a Windows system. 
- Consider where the htb-student account is hosted to properly connect to the target.
- In terms of the firewall blocking connections, this can be tested by completely deactivating each firewall profile in Windows or by enabling specific predefined inbound firewall rules in the `Windows Defender Firewall advanced security settings`.
- Like most firewalls, Windows Defender Firewall permits or denies traffic (access & connection requests in this case) flowing `inbound` &/or `outbound`.
- The different inbound and outbound rules are associated with the different firewall profiles in defender.
- Windows Defender Firewall Profiles:
	- `Public`
	- `Private`
	- `Domain`
- It is a best practice to enable predefined rules or add custom exceptions rather than deactivating the firewall altogether. 
- Unfortunately, it is very common for firewalls to be left completely deactivated for the sake of convenience or lack of understanding. 
- Firewall rules on desktop systems can be centrally managed when joined to a Windows Domain environment through the use of Group Policy. 
- Group Policy concepts and configurations are outside of the scope of this module.
- Once the proper `inbound` firewall rules are enabled we will successfully connect to the share. Keep in mind that we can only connect to the share because the user account we are using (`htb-student`) is in the `Everyone group`. 
- Recall that we left the specific share permissions for the Everyone group set to Read, which quite literally means we will only be able to Read files on this share. 
- Once a connection is established with a share, we can create a `mount point` from our Pwnbox to the Windows 10 target box's file system. 
- This is where we must also consider that NTFS permissions apply alongside share permissions. 
- Recall that NTFS is the default file system in Windows. Lets jump back to our xfreerdp session with our Windows 10 target box and take a look at the NTFS permissions on the Company Data folder.
- #### NTFS Permissions ACL (Security Tab)
![[ntfs_png.png]]
- There's more granular control with NTFS permissions that can be applied to users and groups. 
- Anytime we see a gray checkmark next to a permission, it was inherited from a parent directory. By default, all NTFS permissions are inherited from the parent directory. In the Windows world, the `C:\ drive` is the parent directory to rule all directories unless a system administrator were to disable inheritance inside a newly created folder’s advanced Security settings.
- In many cases, the system administrator(s) of an organization would be responsible for deciding what permissions a user or group of users gets over network resources.
- This is why many spear-phishing attacks are directed at system administrators and other IT leaders. 
- They have lots of influence over what is allowed in the environments they oversee, even more so than an organization's non-technical c-level leaders in many cases. 
- For example, the doctors or executives working in a hospital will not have administrative rights over the network, but the system administrators will.
- Now lets give the everyone group `Full control` at the share level and test the impact of the change by trying to create a mount point to the share from the Desktop of our Pwnbox
- #### Mounting to the Share
```shell-session
secmancer@htb[/htb]$ sudo mount -t cifs -o username=htb-student,password=Academy_WinFun! //ipaddoftarget/"Company Data" /home/user/Desktop/
```
- If this command is not working check the syntax.
- If the syntax is correct yet the command is still not working, `cifs-utils` may need to be installed. 
- This can be done with the following command.
- #### Installing CIFS Utilities
```shell-session
secmancer@htb[/htb]$ sudo apt-get install cifs-utils
```
- Once we have successfully created the mount point on the Desktop on our Pwnbox, we should look at a couple of tools built-in to Windows that will allow us to track and monitor what we have done.
- The `net share` command allows us to view all the shared folders on the system. Notice the share we created and also the C:\ drive.
- `Do you remember us sharing the C:\ drive?`
- We didn't manually share C:. 
- The most important drive with the most critical files on a Windows system is shared via SMB at install. 
- This means anyone with the proper access could remotely access the entire C:\ of each Windows system on a network.
- We can also see the share we created.
- #### Displaying Shares using net share
```cmd-session
C:\Users\htb-student> net share

Share name   Resource                        Remark

-------------------------------------------------------------------------------
C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\WINDOWS                      Remote Admin
Company Data C:\Users\htb-student\Desktop\Company Data

The command completed successfully.
```
- `Computer Management` is another tool we can use to identify and monitor shared resources on a Windows system.
- #### Monitoring Shares from Computer Management
![[computer_management_png.png]]
- We can poke around in `Shares`, `Sessions`, and `Open Files` to get an idea of what information this provides us. 
- Should there be a situation where we assist an individual or organization with responding to a breach related to SMB, these are some great places to check and start to understand how the breach may have happened and what may have been left behind.



### Viewing Share Access Logs in Event Viewer
- `Event Viewer` is another good place to investigate actions completed on Windows. 
- Almost every operating system has a logging mechanism and a utility to view the logs that were captured. 
- Know that a log is like a journal entry for a computer, where the computer writes down all the actions that were performed and numerous details associated with that action. 
- We can view the logs created for every action we performed when accessing the Windows 10 target box, as well as when creating, editing and accessing the shared folder.
![[event_viewer_png.png]]



### Questions
- What protocol discussed in this section is used to share resources on the network using Windows? (Format: case sensitive)
	- SMB
- What is the name of the utility that can be used to view logs made by a Windows system? (Format: 2 words, 1 space, not case sensitive)
	- Event Viewer
- What is the full directory path to the Company Data share we created?
	- C:\Users\htb-student\Desktop\Company Data