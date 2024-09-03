### What Are User Accounts?

User accounts provide access to a host's resources. They can be categorized into:

- **Service Accounts:** Used by services to perform tasks.
- **Built-in Accounts:** Default accounts created by Windows (e.g., Administrator, Guest).
- **Local Users:** Specific to a single host.
- **Domain Users:** Managed by Active Directory (AD), allowing access to domain-wide resources.

### Default Local User Accounts

- **Administrator:** For administrative tasks.
- **Default Account:** Used by the system for multi-user authentication.
- **Guest Account:** Limited access account, disabled by default.
- **WDAGUtility Account:** Used by Windows Defender Application Guard.

### Active Directory (AD) Overview

AD is a directory service for Windows environments, centralizing the management of users, computers, groups, and more within a domain. It plays a crucial role in managing domain users and groups, allowing for centralized administration.

### Local vs. Domain Users

- **Local Users:** Access only the specific host they were created on.
- **Domain Users:** Can log in to any host in the domain and access domain resources based on group membership.

### User Groups

Groups are collections of users that allow for managing permissions and access to resources. They simplify administration, especially in large environments, by enabling group-based access control rather than managing each user individually.

### PowerShell Commands for Managing Users and Groups

- **Get-LocalUser:** Lists all local users on a host.
- **New-LocalUser -Name "Username" -NoPassword:** Creates a new local user without a password.
- **Set-LocalUser -Name "Username" -Password $Password -Description "Description":** Modifies an existing user, e.g., setting a password.
- **Get-LocalGroup:** Lists all local groups on a host.
- **Get-LocalGroupMember -Name "Group":** Lists all members of a specified group.
- **Add-LocalGroupMember -Group "Group" -Member "Username":** Adds a user to a group.

### Managing Domain Users and Groups

To manage AD users and groups, the **ActiveDirectory PowerShell Module** is required. Install it via:

- __Get-WindowsCapability -Name RSAT_ -Online | Add-WindowsCapability -Online:_* Installs all RSAT features, including AD management tools.

Once installed, use the following commands:

- *_Get-ADUser -Filter _:__ Retrieves all users in the AD domain.
- **Get-ADUser -Identity "Username":** Retrieves a specific AD user.


### Questions
- What resource can provide Windows environments with directory services to manage users, computers, and more? (full name not abbreviation)
	- Active Directory
- What PowerShell Cmdlet will display all LOCAL users on a host?
	- Get-LocalUser
- Connect to the target host and search for a domain user with the given name of Robert. What is this users Surname?
	- Loxley