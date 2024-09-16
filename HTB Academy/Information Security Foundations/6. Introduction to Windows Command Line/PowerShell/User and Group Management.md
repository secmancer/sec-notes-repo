As a system administrator, managing users and groups is a crucial skill due to their role as primary assets and major attack vectors. For penetration testers, understanding user and group enumeration, interpretation, and exploitation is vital for gaining access and escalating privileges during engagements. This section will cover user and group management using PowerShell and introduce Active Directory concepts.


#### What are User Accounts?
User accounts provide access to a host's resources and can be used for various purposes, including:
1. **Service Accounts**: Special accounts used by the system or applications to perform specific actions.
2. **Built-in Accounts**: Default accounts created by the operating system for managing the system and basic tasks.
3. **Local Users**: Accounts created on a local machine, typically for individual user access.
4. **Domain Users**: Accounts created and managed within a domain environment, often used in enterprise settings.



#### Default Local User Accounts
When Windows is installed, several default accounts are created for host management and basic usage. These accounts include:
- **Administrator**: The primary account with full system access and control.
- **Guest**: A limited account used for temporary access.
- **DefaultAccount**: A special account used for system services.
- **LocalService**: A built-in account with minimal privileges used for local system services.
- **NetworkService**: A built-in account with network-related privileges used for network services.
**Note:** Understanding these accounts is essential for both system administration and penetration testing, as they play a significant role in managing and securing a system.


![[Screenshot_20240915_211620.png]]

**Active Directory (AD)** is a directory service used in Windows environments that centralizes the management of:
- **Users**
- **Computers**
- **Groups**
- **Network devices**
- **File shares**
- **Group policies**
- **Devices**
- **Trusts with other organizations**



**Key Points:**
- **Central Management**: AD acts as the central hub for managing various resources and security policies within an enterprise environment.
- **Access Control**: Users within the domain can access resources freely, while those outside the domain are restricted or require special permissions.



**Managing AD Users and Groups:**
- **PowerShell**: You can manage AD users and groups from any domain-joined host using the `ActiveDirectory` module in PowerShell.
```
Import-Module ActiveDirectory
```



### Local vs. Domain Joined Users
**Differences:**
- **Domain Users:**
    - **Rights and Access:** Granted rights from the domain to access resources like file servers, printers, and intranet hosts.
    - **Log-in Flexibility:** Can log in to any host within the domain.
- **Local Users:**
    - **Rights and Access:** Limited to accessing only the specific host where the account was created.
    - **Log-in Flexibility:** Restricted to the local host only.



**Understanding Accounts:**
- **Documentation Review:** It's important to review documentation on various account types to understand how they interact on both individual Windows systems and across domain networks. This knowledge is crucial for penetration testers to effectively gain privileged access or perform lateral movement during tests.



### What Are User Groups?
**Purpose:**
- **Logical Organization:** Groups are used to sort user accounts logically, simplifying permission management and access control.
- **Granular Permissions:** Allow administrators to grant or restrict access to resources without managing each user individually.
**Types of Groups:**
- **Local Groups:** Manage permissions on a single host.
- **Domain Groups:** Can include users, end devices (e.g., PCs, printers), and other groups. Essential for security posture management in large environments.
**Management:**
- **Groups Management:** Understanding how to manage groups is key. For a deeper dive into how Active Directory uses groups for security, refer to more specialized modules.


### Get-LocalGroup Cmdlet
**Command Example:**
```
Get-LocalGroup
```

**Output Description:**
- **Administrators:** Full and unrestricted access to the computer/domain.
- **Backup Operators:** Can override security restrictions for backups.
- **Cryptographic Operators:** Authorized for cryptographic operations.
- **Device Owners:** Can change system-wide settings.
- **Distributed COM Users:** Allowed to use Distributed COM objects.
- **Event Log Readers:** Can read event logs from the local machine.
- **Guests:** Limited access similar to Users group.
- **Hyper-V Administrators:** Full access to Hyper-V features.
- **IIS_IUSRS:** Used by Internet Information Services.
- **Network Configuration Operators:** Limited admin privileges for network configuration.
- **Performance Log Users:** Schedule and log performance counters.
- **Performance Monitor Users:** Access performance counter data.
- **Power Users:** Limited administrative rights for compatibility.
- **Remote Desktop Users:** Rights to log on remotely.
- **Remote Management Users:** Access WMI resources over management protocols.
- **Replicator:** Supports file replication in a domain.
- **System Managed Accounts Group:** Managed by the system.
- **Users:** Standard users with restricted system-wide changes.



### Adding/Removing/Editing User Accounts & Groups
**PowerShell Commands Overview:**
- **Local Users and Groups:**
    - **`LocalUser` & `LocalGroup`:** Use these cmdlets to manage local user and group accounts.
- **Domain Users and Groups:**
    - **`ADUser` & `ADGroup`:** Use these cmdlets for managing domain user and group accounts.
- **Command Discovery:**
    - Use `Get-Command *user*` to list available commands related to user management.



### Identifying Local Users
**Command:**
```
Get-LocalUser
```
**Output Example:**
```
Name               Enabled Description
----               ------- -----------
Administrator      False   Built-in account for administering the computer/domain
DefaultAccount     False   A user account managed by the system.
DLarusso           True    High kick specialist.
Guest              False   Built-in account for guest access to the computer/domain
sshd               True
WDAGUtilityAccount False   A user account managed and used by the system for Windows Defender...

```


**Creating a New User:**
**Command:**
```
New-LocalUser -Name "JLawrence" -NoPassword
```
**Note:** By not setting a password, Windows may treat this as a Microsoft live account and attempt to log in with that method.


### Modifying a User
**Commands:**
1. **Prompt for Password:**
```
$Password = Read-Host -AsSecureString
```
2. **Set Password and Description:**
```
Set-LocalUser -Name "JLawrence" -Password $Password -Description "CEO EagleFang"
```
3. **Verify Changes:**
```
Get-LocalUser
```


**Output Example:**
```
Name               Enabled Description
----               ------- -----------
Administrator      False   Built-in account for administering the computer/domain
DefaultAccount     False   A user account managed by the system.
demo               True
Guest              False   Built-in account for guest access to the computer/domain
JLawrence          True    CEO EagleFang
```


### Managing Local Groups
**List Groups:**
**Command:**
```
Get-LocalGroup
```
**Output Example:**
```
Name                                Description
----                                -----------
Access Control Assistance Operators Members of this group can remotely query authorization attributes and permission...
Administrators                      Administrators have complete and unrestricted access to the computer/domain
Backup Operators                    Backup Operators can override security restrictions for the sole purpose of backups
Cryptographic Operators             Members are authorized to perform cryptographic operations.
Device Owners                       Members of this group can change system-wide settings.
Distributed COM Users               Members are allowed to launch, activate and use Distributed COM objects on this machine.
Event Log Readers                   Members of this group can read event logs from local machine
Guests                              Guests have the same access as members of the Users group by default, except for...
Hyper-V Administrators              Members of this group have complete and unrestricted access to all features of Hyper-V.
IIS_IUSRS                           Built-in group used by Internet Information Services.
Network Configuration Operators     Members in this group can have some administrative privileges to manage configuration.
Performance Log Users               Members of this group may schedule logging of performance counters, enable tracing, etc.
Performance Monitor Users           Members of this group can access performance counter data locally and remotely
Power Users                         Power Users are included for backwards compatibility and possess limited administrative privileges.
Remote Desktop Users                Members in this group are granted the right to logon remotely.
Remote Management Users             Members of this group can access WMI resources over management protocols (such as DCOM, WMI, etc.)
Replicator                          Supports file replication in a domain
System Managed Accounts Group       Members of this group are managed by the system.
Users                               Users are prevented from making accidental or intentional system-wide changes and have restricted access.
```


**View Group Members:**
**Command:**
```
Get-LocalGroupMember -Name "Users"
```
**Output Example:**
```
ObjectClass Name                             PrincipalSource
----------- ----                             ---------------
User        DESKTOP-B3MFM77\demo             Local
User        DESKTOP-B3MFM77\JLawrence        Local
Group       NT AUTHORITY\Authenticated Users Unknown
Group       NT AUTHORITY\INTERACTIVE         Unknown
```


**Adding a Member to a Group:**
**Command:**
```
Add-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrence"
```



**Verify Membership:**
**Command:**
```
Get-LocalGroupMember -Name "Remote Desktop Users"
```
**Output Example:**
```
ObjectClass Name                      PrincipalSource
----------- ----                      ---------------
User        DESKTOP-B3MFM77\JLawrence Local
```



### Managing Domain Users and Groups
To manage domain users and groups, follow these steps:

#### 1. **Installing the Active Directory PowerShell Module**
Before managing Active Directory (AD), ensure the Active Directory PowerShell module is installed. If it's not installed, follow these steps:

**Install RSAT:**
```
Get-WindowsCapability -Name RSAT* -Online | Add-WindowsCapability -Online
```
This command installs all Remote Server Administration Tools (RSAT) features. For a more specific installation:
```
Add-WindowsFeature RSAT-AD-PowerShell
```
**Verify Installation:**
```
Get-Module -Name ActiveDirectory -ListAvailable
```


#### 2. **Managing Domain Users**
**Get a List of All Users:**
```
Get-ADUser -Filter *
```
**Get a Specific User:**
```
Get-ADUser -Identity TSilver
```
**Search by Attribute:**
```
Get-ADUser -Filter {EmailAddress -like '*greenhorn.corp'}
```
**Create a New User:**
```
New-ADUser -Name "MTanaka" -Surname "Tanaka" -GivenName "Mori" -Office "Security" -OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"} -AccountPassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true
```
**Modify User Attributes:**
```
Set-ADUser -Identity MTanaka -Description "Sensei to Security Analyst's Rocky, Colt, and Tum-Tum"
```
**Verify User Attributes:**
```
Get-ADUser -Identity MTanaka -Properties Description
```


#### 3. **Managing Domain Groups**
**Get a List of All Groups:**
```
Get-ADGroup -Filter *
```
**Get Group Membership:**
```
Get-ADGroupMember -Identity "GroupName"
```
**Add a User to a Group:**
```
Add-ADGroupMember -Identity "GroupName" -Members "Username"
```
**Remove a User from a Group:**
```
Remove-ADGroupMember -Identity "GroupName" -Members "Username"
```



### Why Enumerating Users & Groups is Important
**1. Identifying Misconfigurations:**
- **Excessive Permissions**: Users might have more permissions than necessary, which could be exploited to gain unauthorized access.
- **Unnecessary Group Memberships**: Users may be part of groups that they don’t need to be in, potentially leading to privilege escalation.
- **Weak or No Passwords**: Accounts with weak or no passwords are vulnerable to attacks.
**2. Exploiting Nested Group Memberships:**
- **Nested Memberships**: Groups can contain other groups, creating a hierarchy that can grant users higher privileges indirectly.
- **Privilege Escalation**: Users might gain elevated privileges through nested group memberships, which can be exploited by attackers.
**3. Using Tools for Visualization:**
- **BloodHound**: A tool that can visualize Active Directory environments and identify privilege escalation paths and misconfigurations.
**4. Further Reading:**
- **Windows Privilege Escalation Module**: For a more detailed understanding of how to enumerate and exploit user and group configurations.
**Key Takeaways:**
- **Enumeration**: Essential for identifying and understanding misconfigurations in user and group settings.
- **Security Assessment**: Helps in assessing and improving the security posture by addressing potential vulnerabilities related to user and group configurations.


## Questions
- What resource can provide Windows environments with directory services to manage users, computers, and more? (full name not abbreviation)
	- Active Directory
- What PowerShell Cmdlet will display all LOCAL users on a host?
	- Get-LocalUser
- Connect to the target host and search for a domain user with the given name of Robert. What is this users Surname?
	- Loxley