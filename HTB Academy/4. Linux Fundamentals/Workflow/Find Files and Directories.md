Efficiently locating files and directories is crucial in a Linux environment, especially for tasks such as finding configuration files, user-created scripts, and other critical data. Instead of manually browsing through directories, you can use specialized tools to simplify the search process.

#### **Tools for Searching**
1. **which**
    - **Purpose**: Finds the path of executable files.
    - **Usage**: Checks if a specific program is available on the system.
    - **Example**:
        - Command: `which python`
        - Output: `/usr/bin/python`
    - If the program does not exist, there will be no output.

**find**
- **Purpose**: Searches for files and directories based on various criteria.
- **Syntax**: `find <location> <options>`
- **Example**:
    - Command: `find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null`
    - Output:
```
-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
```
**Options**:
- `-type f`: Searches for files.
- `-name *.conf`: Filters files with the `.conf` extension.
- `-user root`: Filters files owned by the root user.
- `-size +20k`: Filters files larger than 20 KiB.
- `-newermt 2020-03-03`: Filters files modified after March 3, 2020.
- `-exec ls -al {} \;`: Executes `ls -al` on each found file.
- `2>/dev/null`: Redirects error messages to `/dev/null`.

**locate**
- **Purpose**: Quickly searches for files using a pre-built database.
- **Usage**: Faster than `find` but less flexible in filtering.
- **Update Database**: Run `sudo updatedb` to update the database.
- **Example**:
    - Command: `locate *.conf`
    - Output:
```
/etc/GeoIP.conf
/etc/NetworkManager/NetworkManager.conf
/etc/UPower/UPower.conf
/etc/adduser.conf
```

![[Screenshot_20240912_123457.png]]
#### **Optional Exercise**
- **Task**: Use the `which`, `find`, and `locate` commands to find all files related to the netcat (`nc`) tool.

### Questions
- What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
	- 00-mesa-defaults.conf
- How many files exist on the system that have the ".bak" extension?
	- 4
- Submit the full path of the "xxd" binary.
	- /usr/bin/xxd