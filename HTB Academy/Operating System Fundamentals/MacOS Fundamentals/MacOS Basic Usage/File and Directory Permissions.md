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

