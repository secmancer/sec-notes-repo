### Introduction
- We will often see the term "objects" when referring to AD. 
- What is an object? 
	- An object can be defined as ANY resource present within an Active Directory environment such as OUs, printers, users, domain controllers.


### AD Objects Overview
![image](https://academy.hackthebox.com/storage/modules/74/adobjects.png)



### Users
- Considered `leaf objects`, which means they cannot have any other objects within them.
	- Example: mailbox in Microsoft Exchange
- Considered a security principal with a security identifier (SID), along with a global unique identifier (GUID)
	- Many possible [attributes](http://www.kouti.com/tables/userattributes.htm), like display name, last login time, date of last password change, email address, account description, manager, address, and more.
- Depending on the setup, we can choose from 800 possible attributes.
	- ALL possible attributes are detailed [here](https://www.easy365manager.com/how-to-get-all-active-directory-user-object-attributes/). 
- Crucial target for attacks as having access to even a low privileged user allows for them to interact with many objects/resources.
	- This allows for detailed enumeration of the entire forest.



### Contacts
- Usually represents an external users.
	- Contains attributes like first name, last name, email address, telephone number, etc.
- They're leaf objects, but NOT a security principal.
	- So, no SID is given to them, only a GUID.
- Example: contact card for a third party vendor/customer.



### Printers
- Object that points to a printer that can be accessed from within the AD network.
- Similar to a contact, it's a leaf object, while not being a security principal.
- Has attributes like the name, driver information, port number, etc.



### Computers
- Object for any computer that has ever joined the AD network, whether a workstation or server.
- Leaf objects, but is a security principal.
	- Has both a SID and GUID.
- Prime targets for attackers, as full administrative access to them gives them similar rights to that of a standard domain user.
	- Can be used to perform a lot of enumeration tasks a user account can do, with a few exceptions when dealing with domain trusts.



### Shared Folders
- Object that points to a shared folder on a specific computer that stores it.
- Stringent access control applied to them.
- Can be accessed by everyone, regardless of account status, only open to authenticated users, or to only certain users/groups.
- Anyone with the proper permissions will be denied from accessing it.
- Not a security principal.
- Attributes for it include the name, location on the system, and security access rights.



### Groups
- Considered a `container object` as it contains other objects within it.
- Does have a ID and a GUID, so is a security principal.
- Manages user permissions and access to other securable objects in a more easy and effective way.
- We often see what is called "[nested groups](https://docs.microsoft.com/en-us/windows/win32/ad/nesting-a-group-in-another-group)", or a group that was added to another group.
	- This leads to users getting unintended rights that they probably shouldn't have.
	- This can be leveraged during penetration tests.
- Example: [BloodHound](https://github.com/BloodHoundAD/BloodHound) can help us discover attack paths and give us an GUI interface of it.
	- This can include these groups, along with the many attributes that are associated with them.


### Organizational Units (OUs)
- Organizational Units (OUs) are containers used by system administrators to group similar objects for easier administration and delegation of tasks.
- OUs allow delegation of tasks like resetting passwords, creating/deleting users, modifying group memberships, managing Group Policy links, etc., without granting full administrative rights.
- **Hierarchy and Permissions**:
    - Top-level OUs (e.g., "Employees") can have child OUs for departments (e.g., "Marketing," "HR").
    - Permissions granted at a parent OU (e.g., "Help Desk") can extend to its child OUs, enabling delegation within specific scopes.
- OUs are instrumental in applying Group Policy settings to subsets of users and groups, such as enforcing specific password policies for accounts placed in a designated OU.
- Key attributes of OUs include their name, members, and security settings.



### Domain
- A domain is the foundational structure of an Active Directory (AD) network, containing objects like users and computers organized into containers such as groups and OUs.
- **Each domain has its own database and policies that govern its objects.
- Domains come with default policies (e.g., domain password policy) that can be customized.
- Organizations can create and apply policies tailored to their needs, such as restricting cmd.exe access for non-admin users or mapping shared drives at login.


### Domain Controllers
- Domain Controllers: brains of an AD network. 
- Handle authentication requests, verification of users, and control access to the various resources in the domain. 
- All requests are validated using the domain controller, with privileged access requests being based on predetermined roles assigned to users. 
- It also enforces security policies and stores information about every other object in the domain.



### Sites
- A site in AD is a set of computers across one or more subnets connected using high-speed links. 
- They are used to make replication across domain controllers run efficiently.



### Built-in
- In AD, built-in is a container that holds [default groups](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups) in an AD domain. 
- They are predefined when an AD domain is created.



### Foreign Security Principals
- Object to represent a security principal that belongs to a trusted external forest. 
	- Created when an object such as a user, group, or computer from an external forest is added to a group in the current domain. 
- Automatically created after adding a security principal to a group. 
- Every foreign security principal is a placeholder object that holds the SID of the foreign object. 
- Windows uses this SID to resolve the object's name via the trust relationship. 
- FSPs are created in a specific container named ForeignSecurityPrincipals with a distinguished name like `cn=ForeignSecurityPrincipals,dc=inlanefreight,dc=local`.



### Questions
- True or False; Computers are considered leaf objects.
	- True
- <___> are objects that are used to store similar objects for ease of administration. (Fill in the blank)
	- Organizational Units
- What AD object handles all authentication requests for a domain?
	- Domain Controller