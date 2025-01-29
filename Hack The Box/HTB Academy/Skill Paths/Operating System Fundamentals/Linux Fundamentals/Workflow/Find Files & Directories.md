### **1. Using the `which` Command**
- The `which` command tells us the path of a program or script that should be executed. It's typically used to verify the presence of a command in the system's `$PATH`.
- To find the path to the **netcat** (`nc`) tool, run:
```bash
secmancer@htb[/htb]$ which nc
```
- If `netcat` is installed, this will return something like:
```
/usr/bin/nc
```
- If there's no output, it means the tool isn't in the system's `PATH`.



### **2. Using the `find` Command**
- The `find` command is extremely powerful for searching through directories for files that match certain criteria.
- For example, to search for anything related to `nc` (such as a file or directory), we can use:
```bash
secmancer@htb[/htb]$ find / -name '*nc*' 2>/dev/null
```
- Here’s what each part of the command does:
	- `/`: Tells `find` to start the search from the root directory.
	- `-name '*nc*'`: Filters results to only include files or directories whose names contain the string `nc`.
	- `2>/dev/null`: Redirects error messages (such as "Permission denied") to the null device, so they don’t clutter the output.



### **3. Using the `locate` Command**
- `locate` works much faster than `find` because it uses a pre-built database of files. Before using `locate`, you need to update the database with:
```bash
secmancer@htb[/htb]$ sudo updatedb
```
- Then, you can search for all files related to `nc`:
```bash
secmancer@htb[/htb]$ locate nc
```
- This will return a list of all files that contain the string `nc` in their path or name, such as:
```
/usr/bin/nc
/etc/netcat.conf
```



### **Optional Exercise: Searching for Files Related to `netcat` / `nc`**
1. **Using `which`**: Find the location of `nc` using `which nc`.
2. **Using `find`**: Use `find` to search for any files or directories related to `nc` across the system.
3. **Using `locate`**: After updating the `locate` database with `sudo updatedb`, search for files related to `nc` with `locate nc`.



### Questions
- What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
	- 00-mesa-defaults.conf
- How many files exist on the system that have the ".bak" extension?
	- 4
- Submit the full path of the "xxd" binary.
	- /usr/bin/xxd