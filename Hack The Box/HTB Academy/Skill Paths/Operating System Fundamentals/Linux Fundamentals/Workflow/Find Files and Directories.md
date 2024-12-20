### Importance of the Search
- Finding specific files and folders on a Linux system is essential, especially for identifying configuration files or user-created scripts.
- Manual browsing is inefficient; instead, tools can simplify locating and analyzing files and folders.
- These tools can help identify recently modified files or specific targets without manually inspecting every directory.



### Which
- One of the common tools is `which`. 
- This tool returns the path to the file or link that should be executed. 
- This allows us to determine if specific programs, like cURL, netcat, wget, python, gcc, are available on the operating system. 
- Let us use it to search for Python in our interactive instance.
```shell-session
secmancer@htb[/htb]$ which python

/usr/bin/python
```
- If the program we search for does not exist, no results will be displayed.



### Find
- Another handy tool is `find`. 
- Besides the function to find files and folders, this tool also contains the function to filter the results. 
- We can use filter parameters like the size of the file or the date. 
- We can also specify if we only search for files or folders.
- #### Syntax - find
```shell-session
secmancer@htb[/htb]$ find <location> <options>
```
- Let us look at an example of what such a command with multiple options would look like.
```shell-session
secmancer@htb[/htb]$ find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```
- Now let us take a closer look at the options we used in the previous command. 
- If we hover the mouse over the respective options, a small window will appear with an explanation. 
- These explanations will also be found in other modules, which should help us if we are not yet familiar with one of the tools.
![[Screenshot_20241108_101019.png]]



### Locate
- It will take much time to search through the whole system for our files and directories to perform many different searches. 
- The command `locate` offers us a quicker way to search through the system. 
- In contrast to the `find` command, `locate` works with a local database that contains all information about existing files and folders.
- We can update this database with the following command.
```shell-session
secmancer@htb[/htb]$ sudo updatedb
```
- If we now search for all files with the "`.conf`" extension, you will find that this search produces results much faster than using `find`.
```shell-session
secmancer@htb[/htb]$ locate *.conf

/etc/GeoIP.conf
/etc/NetworkManager/NetworkManager.conf
/etc/UPower/UPower.conf
/etc/adduser.conf
<SNIP>
```
- However, this tool does not have as many filter options that we can use. 
- So it is always worth considering whether we can use the `locate` command or instead use the `find` command. It always depends on what we are looking for.

> Optional Exercise: Try the different utilities and find everything related to the **netcat** / **nc** tool.



### Questions
- What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
	- 00-mesa-defaults.conf
- How many files exist on the system that have the ".bak" extension?
	- 4
- Submit the full path of the "xxd" binary.
	- /usr/bin/xxd