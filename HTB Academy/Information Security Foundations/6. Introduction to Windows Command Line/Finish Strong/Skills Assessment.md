#### **Objective**
- **Primary Goal**: Collect user names and passwords from a non-critical Windows host.
- **Outcome**: Enable the team to focus on complex tasks by documenting all user passwords.



#### **Process Overview**
1. **Initial Access**:
    - **Host**: Recently gained access to a non-critical Windows host with many users.
    - **Objective**: Extract user names and passwords.
2. **Challenge Workflow**:
    - **User Authentication**:
        - **Method**: For each challenge, authenticate with a user to get the flag.
        - **Flag Usage**: The flag obtained from one user is used as the SSH password for the next user.
    - **Documentation**: Document all methods, one-liners, and scripts used to gather information.



#### **Detailed Steps**
1. **Identify and Enumerate Users**:
    - Use tools or commands to list all user accounts on the Windows host.
        - Example command:
```
Get-LocalUser
```
- Alternatively:
```
net user
```
2. **Gather Password Information**:
	- **Tools/Commands**: Utilize tools or commands to retrieve or crack passwords.
	    - Example command:
```
Get-ADUser -Filter * -Property PasswordLastSet
```
- Alternatively, use third-party tools for password extraction or cracking.
- 3. **Authenticate and Retrieve Flags**:
    - For each user, authenticate using the credentials obtained.
    - Retrieve the flag as specified in the challenge.
    - Use the flag as the password for the subsequent user.
- 4. **Multiple Approaches**:
    - **Experiment**: Try different methods or tools to achieve the same output.
    - **Documentation**: Keep detailed notes of different approaches and their results.
- 5. **Example Workflow**:
    - **User 1**: Authenticate and get flag1.
    - **User 2**: Use flag1 as SSH password to authenticate and get flag2.
    - **User 3**: Use flag2 as SSH password to authenticate and get flag3.
    - Continue this process as required.


#### **Documentation Tips**
- **One-Liners**: Record any concise commands or scripts used.
    - Example:
```
# Get list of local users
Get-LocalUser
```
**Scripts**: Save and document any scripts used for automation or repeated tasks.
- Example PowerShell Script:
```
$users = Get-LocalUser
foreach ($user in $users) {
    # Perform actions with each user
    # ...
}
```
- **General Notes**: Note down any observations, challenges, or insights gained during the process.

## Questions
- The flag will print in the banner upon successful login on the host via SSH.
	- D0wn_the_rabbit_H0!3
- Access the host as user1 and read the contents of the file "flag.txt" located in the users Desktop.
	- Nice and Easy!
- If you search and find the name of this host, you will find the flag for user2.
	- ACADEMY-ICL11
- How many hidden files exist on user3's Desktop?
	- 101
- User4 has a lot of files and folders in their Documents folder. The flag can be found within one of them.
	- Digging in The nest
- How many users exist on this host? (Excluding the DefaultAccount and WDAGUtility)
	- 14
- For this level, you need to find the Registered Owner of the host. The Owner name is the flag.
	- htb-student
- For this level, you must successfully authenticate to the Domain Controller host at 172.16.5.155 via SSH after first authenticating to the target host. This host seems to have several PowerShell modules loaded, and this user's flag is hidden in one of them.
	- Modules_make_pwsh_run!
- This flag is the GivenName of a domain user with the Surname "Flag".
	- Rick
- Use the tasklist command to print running processes and then sort them in reverse order by name. The name of the process that begins with "vm" is the flag for this user.
	- vmtoolsd.exe
- What user account on the Domain Controller has many Event ID (4625) logon failures generated in rapid succession, which is indicative of a password brute forcing attack? The flag is the name of the user account.
	- justalocaladmin