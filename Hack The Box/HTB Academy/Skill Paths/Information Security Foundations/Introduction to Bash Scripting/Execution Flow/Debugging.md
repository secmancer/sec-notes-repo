### Introduction
- Bash provides great tools for finding, tracking, and fixing errors in code through debugging.
- Debugging in Bash involves removing errors (bugs) and can be done in various ways, such as checking for typos or analyzing code to identify the causes of errors.
- It also helps identify vulnerabilities, such as manipulating input types to track error handling and potentially inject code.
- The process is discussed in further detail in other modules, with Bash offering the `-x` (`xtrace`) and `-v` options for debugging, as shown in the `CIDR.sh` script example.



### CIDR.sh - Debugging
```shell-session
secmancer@htb[/htb]$ bash -x CIDR.sh

+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```
- Here Bash shows us precisely which function or command was executed with which values. 
- This is indicated by the plus sign (`+`) at the beginning of the line. 
- If we want to see all the code for a particular function, we can set the "`-v`" option that displays the output in more detail.



### CIDR.sh - Verbose Debugging
```shell-session
secmancer@htb[/htb]$ bash -x -v CIDR.sh

#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi
+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
	CIDR.sh <domain>
+ exit 1
```
- In comparison to normal debugging, we see the entire code section that has been processed so far and then the individual steps that have been taken.