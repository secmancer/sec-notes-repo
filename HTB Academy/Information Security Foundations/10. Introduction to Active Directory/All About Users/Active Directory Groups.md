**Active Directory Groups Overview:**
- **Purpose of Groups:**  
  Groups are used in Active Directory (AD) to manage users by grouping them together and assigning rights or access to resources. They are a key component in access management but are also a target for attackers due to potential hidden privileges.
- **Types of Groups:**  
  Groups are categorized by **type** and **scope**:
  1. **Security Groups:** Used for assigning permissions to resources.
  2. **Distribution Groups:** Used for email distribution, not for permissions.
- **Group Scopes:**
  1. **Domain Local Group:** Only manages resources in the domain it was created in, can contain users from other domains.
  2. **Global Group:** Used across domains but can only contain users from the domain it was created in.
  3. **Universal Group:** Used across multiple domains and can contain users from any domain but triggers replication when membership changes.
- **Built-in vs Custom Groups:**  
  AD comes with built-in security groups, but organizations often create custom groups to define their access control strategies.
- **Nested Group Membership:**  
  Groups can contain other groups (nested), which can lead to users inheriting privileges indirectly. This concept can be exploited by attackers or penetration testers using tools like BloodHound.
- **Group Attributes:**
  1. **Common Name (CN):** The name of the group in AD.
  2. **Member:** Lists the objects (users, groups) that are members.
  3. **Group Type:** Specifies the group type and scope.
  4. **Object SID:** Unique security identifier for the group.

**Key Points to Remember:**
- **Group management is critical for maintaining security.** Misconfigurations or excessive group membership can lead to unintended access.
- **Group scopes affect where and how groups can be used** (e.g., Domain Local vs. Universal).
- **Nested groups and inherited permissions** need to be regularly audited to prevent privilege escalation.

![[bh_nested_groups.png]]

## Questions
- What group type is best utilized for assigning permissions and right to users?
	- Security
- True or False; A "Global Group" can only contain accounts from the domain where it was created.
	- True
- Can a Universal group be converted to a Domain Local group? (yes or no)
	- yes