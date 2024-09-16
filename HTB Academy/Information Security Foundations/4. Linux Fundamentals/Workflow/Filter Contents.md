#### Pagers: `more` and `less`
- **more**: A basic pager for viewing file content interactively.
    - Command: `more /etc/passwd`
    - Navigates through the file; press `[Q]` to quit.
    - Example Output:
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
...
--More--
```

- **less**: An advanced pager with more features than `more`.
    - Command: `less /etc/passwd`
    - Similar navigation as `more`, but does not retain the output in the terminal after quitting.
    - Example Output:
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
...
:
```

#### File Viewing Commands
- **head**: Displays the first ten lines of a file.
    - Command: `head /etc/passwd`
    - Example Output:
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
...
```
- **tail**: Displays the last ten lines of a file.
	- Command: `tail /etc/passwd`
	- Example Output:
```
miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
...
```


#### Sorting and Filtering Commands
- **sort**: Sorts lines of text files.
    - Command: `cat /etc/passwd | sort`
    - Example Output:
```
_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
...
```
**grep**: Searches for patterns in files.
- Basic Search Command: `cat /etc/passwd | grep "/bin/bash"`
- Exclude Results Command: `cat /etc/passwd | grep -v "false\|nologin"`
- Example Output for Search:
```
root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
...
```
- Example Output for Exclusion:
```
root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
...
```

**cut**: Removes sections from each line of files.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1`
- Example Output:
```
root
sync
mrb3n
...
```


**tr**: Translates or deletes characters.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "`
- Example Output:
```
root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
...
```


**column**: Formats text into columns.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t`
- Example Output:
```
root         x  0     0      root               /root        /bin/bash
sync         x  4     65534  sync               /bin         /bin/sync
...
```


**awk**: A programming language for pattern scanning and processing.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'`
- Example Output:
```
root /bin/bash
sync /bin/sync
...
```

**sed**: A stream editor for filtering and transforming text.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'`
```
root /HTB/bash
sync /HTB/sync
...
```

**wc**: Counts lines, words, and characters.
- Command: `cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l`
- Example Output:
```
5
```

![[Screenshot_20240912_124017.png]]

### Questions
- How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
	- 7
- Determine what user the ProFTPd server is running under. Submit the username as the answer.
	- proftpd
- Use cURL from your Pwnbox (not the target machine) to obtain the source code of the "https://www.inlanefreight.com" website and filter all unique paths of that domain. Submit the number of these paths as the answer.
	- 34