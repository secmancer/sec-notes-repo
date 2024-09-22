### Active Directory (AD) Objects Overview

#### Objects in Active Directory
- **Objects** are fundamental components in AD, representing any resource such as Organizational Units (OUs), printers, users, or domain controllers.
  
---

#### Key AD Objects

1. **Users**
   - **Definition**: Individuals within the organization’s AD environment.
   - **Type**: Leaf object (cannot contain other objects).
   - **Identifiers**: Has both a **Security Identifier (SID)** and a **Global Unique Identifier (GUID)**.
   - **Attributes**: Attributes include display name, last login time, password change date, email, account description, etc. AD allows for over 800 possible attributes.
   - **Security**: Users are security principals, making them critical targets for attackers due to their access to many objects and resources.

2. **Contacts**
   - **Definition**: Represents external users (e.g., vendors or customers).
   - **Type**: Leaf object (cannot contain other objects).
   - **Identifiers**: Only has a **GUID**, not a SID.
   - **Attributes**: Includes first name, last name, email, phone number.

3. **Printers**
   - **Definition**: Represents printers accessible within the AD network.
   - **Type**: Leaf object.
   - **Identifiers**: Only has a **GUID**.
   - **Attributes**: Includes printer name, driver info, port number.

4. **Computers**
   - **Definition**: Any computer joined to the AD network (workstations or servers).
   - **Type**: Leaf object.
   - **Identifiers**: Has both a **SID** and a **GUID**, making it a security principal.
   - **Security**: Full administrative access to a computer can allow attackers similar rights as domain users.

5. **Shared Folders**
   - **Definition**: Points to a shared folder on a computer.
   - **Type**: Leaf object.
   - **Identifiers**: Only has a **GUID**.
   - **Attributes**: Includes name, location, and security access rights.

6. **Groups**
   - **Definition**: A container object that can include users, computers, and even other groups.
   - **Type**: Container object.
   - **Identifiers**: Has both a **SID** and a **GUID** (security principal).
   - **Purpose**: Simplifies permission management by grouping users for access control.

7. **Organizational Units (OUs)**
   - **Definition**: Containers that hold similar objects for easier administration.
   - **Type**: Container object.
   - **Purpose**: Used for delegating administrative tasks (e.g., password resets, group management) and applying **Group Policy Objects (GPOs)**.
   - **Attributes**: Include name, members, security settings.

8. **Domain**
   - **Definition**: The structure of an AD network, containing users and computers.
   - **Purpose**: Manages its own database and policies for objects within the domain.
   - **Attributes**: Includes policies such as password policies and others specific to organizational needs.

9. **Domain Controllers (DCs)**
   - **Definition**: Servers that handle authentication and control access to domain resources.
   - **Role**: Brain of the AD network, enforcing security policies and storing all domain object information.

10. **Sites**
    - **Definition**: A collection of computers across subnets, typically with high-speed connections.
    - **Purpose**: Ensures efficient replication between domain controllers.

11. **Built-in**
    - **Definition**: A container holding default AD domain groups created when a domain is set up.

12. **Foreign Security Principals (FSPs)**
    - **Definition**: Objects created in AD to represent security principals from external forests.
    - **Purpose**: Holds the SID of a foreign object for resolving names via trust relationships.

---

![[adobjects.png]]


## Questions
- True or False; Computers are considered leaf objects.
	- True
- <___> are objects that are used to store similar objects for ease of administration. (Fill in the blank)
	- Organizational Units
- What AD object handles all authentication requests for a domain?
	- Domain Controller