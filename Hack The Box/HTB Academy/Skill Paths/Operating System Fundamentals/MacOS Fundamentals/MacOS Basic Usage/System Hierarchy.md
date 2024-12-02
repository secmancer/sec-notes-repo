> **Note:** As macOS is essentially unix-based, many of the things and commands covered in the [Linux Fundamentals](https://academy.hackthebox.com/module/details/18) module also apply here and can be used with macOS, though some may use slightly difference syntax. This module will not repeat the Linux basics as covered in the [Linux Fundamentals](https://academy.hackthebox.com/module/details/18) module, but will mainly be covering macOS-specific topics, so you are advised to also go through that module to have a wholistic understanding of both macOS and Linux.


### MacOS Domains

![[D3.png]]

- In macOS, a file system is divided into multiple domains that separate files and resources depending on their intended usage.
- Domains apply `access privilege` to the files and resources in that domain, preventing unauthorized users from changing files.

| Domain         | Description                                                                                                                                |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Local Domain   | Contains resources such as apps that are local to the current computer and shared among all computer users.                                |
| System Domain  | Contains the system software installed by Apple.                                                                                           |
| User Domain    | Contains resources specific to the users who log in to the system. This domain reflects the home directory of the current user at runtime. |
| Network Domain | Contains resources such as apps and documents that are shared among users of a local area network.                                         |

### macOS File System Structure
![[D1.png]]
#### Standard Directories
- #### /Applications
	- The `Applications` directory contains applications that users would commonly use. 
	- There are multiple `/Applications` folders, each belonging to a different domain.

| Domain        | Description                                                                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| User Domain   | Applications that are installed and related to a particular user are saved under `/Users/username/Applications`                                              |
| Local Domain  | Applications which are installed by a user, installed by `Apple`, and which can be used by `all` users present in a computer are saved under `/Applications` |
| System Domain | Applications which are related to the system or installed by `Apple` are saved under `/System/Applications`                                                  |
- #### /Users
	- The `Users` directory belongs to the `User Domain`. It contains user-related applications, files, and resources. 
	- Each user account has its own user folder, located under `/Users/username`. 
	- Each user has access `only` to their user directory and `cannot` access items on another user's directory.
	- For example, if two users, `htb-student` and `htb-dev`, are present in the system, then the `/Users` directory would consist of two directories, with each user account having its own directory.
```
[root@htb]/Users$ ls

htb-dev
htb-student
```

- #### /Library
	- The `Library` directory stores custom data files for applications, caches, configurations, resources, preferences, and user data. 
	- The Local and system domain Library directories are Global in scope, while the user Library directory is specific to that user.

| Domain        | Description                                                                                                                            |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| User Domain   | Information about the applications related to the current user is stored in `/Users/username/Library`                                  |
| Local Domain  | Information related to an application that is shared by all the users who are using that application is stored in `/Library` directory |
| System Domain | Information about system applications is stored in `/System/Library`                                                                   |
	- The `Library` directory contains some key subdirectories:
		- `Library/Application Support`: Contains app-specific support files, data files & configuration files
		- `Library/Caches`: Contains app-specific support files that the app can re-create easily
		- `Library/Frameworks`: Stores libraries that are used, or needed, to create an application
		- `Library/Preferences`: contains the application preferences (PowerManagement, SoftwareUpdate, Logging, Calendar, etc.)

- #### /Network
	- The `Network` directory contains files that belong to the network domain. 
	- This directory contains the list of computers in the local area network.

- #### /System
	- The `System` directory contains the system resources required by macOS to run. 
	- These files are installed by Apple and shouldn't be modified.

### Unix-Specific Directories
- macOS also has some Unix-specific directories structured in a tree-like hierarchy.
- #### Directory Tree
![[D2.png]]
![[Screenshot_20241106_220812.png]]
- This was not an exhaustive list of every directory or subdirectory on our hosts. 
- We recommend if you run into a specific folder you do not quite understand the purpose of, check the man page or Google what that specific directory is for. 
- The `man hier` command is also helpful for getting an initial understanding of the standard Unix folder structure.


### Questions
- Where are the Applications related to the system stored at?
	- /System/Applications