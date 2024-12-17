### UNIX Permissions
- Within the file system structure, every object on the host belongs to a specific user or group. 
- When we create new files or directories, they belong to the user who initiated their creation (User Owner), and our primary group will also be the group owner of the file. 
- If a directory has specific permissions set for group ownership, those permissions will apply to the files created within.
- These permissions are shown utilizing the `octal` or Base 8 numbering system. 
- They are used to apply the `read`, `write`, and `execute` attributes to the contexts of `User owner`, `Group owner`, and `Others` on a file. These are represented as:
![[Screenshot_20241106_220936.png]]
> **Tip:** Converting between permission attributes and their octal value may be difficult to do in our heads, so there are tools like [chmod-calculator](https://chmod-calculator.com) that can help us do the conversion quickly.


### Basic File Permissions
![[Screenshot_20241106_221130.png]]
- From the output above, we can see the terminal output for the file `HTB-Wallpaper-1.png`. 
- This breakdown shows us how our permissions are implemented and other attributes, such as the date of creation/modification, the number of links associated with the file, size, and the object type.
- From this output, we can see that the User owner is the user `htb-user` and the group owner is `staff`. 
- This is likely due to the host being managed by a central IT department and their policies. 
- This means that others can view this directory. We can see the owner has `Read/Write` permissions over the file, and the staff group members have `Read`.
- All other groups and users have `Read` permissions as well.

> **Tip:** To make it easier to remember when reading the attributes from left to right, remember the acronym `UGO`, which stands for User/Group/Others.

- If we were to modify these permissions, we would notice that the attributes listed to the left would change to reflect the new permission set. 
- For example, below, we can see a script with the execute attribute set for the User owner. Notice the difference?
```
secmancer@htb[/htb]$ ls -l 

- rwx r-- r--@  1 htb-user staff 4663911 Aug 30  2019 ping-all-the-things.sh
d rwx r-x r-x@  1 htb-user staff 6512375 Aug 30  2019 nmap-output
```

- The script's permissions allow only the `User owner` to `execute` the script, while the group members and others can only read its contents. 
- Looking at the line for `nmap-output`, we can see that this is a directory because of the Filetype marked with `d` before our permissions. 
- The execute attribute is also required to traverse into the directory and read the contents. 
- Without it, a user would not be able to access the directory.


### GUI Permissions Management
- #### Viewing and Modifying Permissions
	- To get to the window seen above, we have to:
		- select the file you wish to view
		- right-click the file
		- select `get info`
	- We may also use the `Command + Option + I` keyboard shortcut after selecting the file/folder to do the same thing.
	- This will bring up the screen we see in the example above. Notice the current permission set on the file. 
	- If we wish to modify it, we need to do a few things first:
		- Click the lock in the bottom right corner (green square above) and authenticate. This will allow us to make changes to the file.
		- From here, we must select a user or group from the name column and use the dropdown menu to its right to modify the permissions. We can see it in use below.
- #### Change Permissions From GUI
	- Managing permissions from the GUI is pretty straightforward. 
	- We can click on any of the users shown under `Sharing and Permission` and select the appropriate permission from the drop-down menu, which will require us to enter our password to confirm the change. 
	- We may also click on the `+` icon to add a new user to this list or on the `-` icon to remove any of the shown users.
	- However, be careful how you set permissions on files and folders, as you could quickly expose data you may not wish for everyone to access.

### Terminal Permissions Management
- Next, let's take a bit to look at permissions from within the terminal. 
- We will utilize the [chmod](https://ss64.com/osx/chmod.html) and [chown](https://ss64.com/osx/chown.html) commands to manage file permissions and other attributes.

### chmod
```
secmancer@htb[/htb]$ ls -l  

total 8256
-rw-r--r--@ 1 htb-user  staff  2512910 Aug 30  2019 HTB-Wallpaper-1.png
-rw-r--r--@ 1 htb-user  staff  1710003 Aug 12  2019 HTB-Wallpaper-1920x1200.jpg
```
- Let's try to change the permission attribute for everyone to read, write, and execute. In octal format, this will equal `777`, which we can do as follows:
```
secmancer@htb[/htb]$ ls -l  

total 8256
-rw-r--r--@ 1 htb-user  staff  2512910 Aug 30  2019 HTB-Wallpaper-1.png
-rw-r--r--@ 1 htb-user  staff  1710003 Aug 12  2019 HTB-Wallpaper-1920x1200.jpg
```

```
secmancer@htb[/htb]$ ls -l  
  
-rwxrwxrwx@ 1 htb-user  staff  2512910 Aug 30  2019 HTB-Wallpaper-1.png  
```
- Notice the change from before? `htb-student` is now the file owner, and staff retained access to it as the group owner. 
- `chown` is handy because we can also change the group ownership if we wish. To do so, we would specify ownership with `chown` like so:
```
secmancer@htb[/htb]$ sudo chown htb-user:admins HTB-Wallpaper-1.png 

secmancer@htb[/htb]$ ls -l 
-rwxrwxrwx@ 1 htb-user  admins  2512910 Aug 30  2019 HTB-Wallpaper-1.png  
```
- Notice now that ownership of the file has changed again. `htb-user` is now the user owner, and `admins` is the group owner.
- These are just two different ways we can manage group ownership. 
- However, there is also the `chgrp` command that deals specifically with groups.
- Permissions are an essential aspect of any administrator's workload when it comes to ensuring systems are secure and that the integrity of a file is not compromised by someone without a need to access it. 
- Maintaining confidentiality, integrity, and availability is a constant process.

### Questions
- If a file has a permission set of "rw-rw-rw-" applied, what would that equal in Octal format? (number only)
	- 666