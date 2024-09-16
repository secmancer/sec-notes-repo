**Overview**
- **Debugging in Bash**: The process of identifying, tracking, and fixing errors (bugs) in your code. It helps find and resolve issues, such as typos and logic errors, and can also be used for vulnerability assessment.
- **Debugging Techniques**: Include checking for typos, analyzing code to understand error origins, and exploring vulnerabilities through error handling.



**Bash Debugging Options**
- **`-x` (xtrace)**: Displays each command and its arguments as they are executed. Useful for tracking command execution and identifying errors.
- **`-v` (verbose)**: Displays the input lines as they are read. Useful for seeing the code execution in detail.



**Example: Debugging with CIDR.sh**
1. **Using `-x` Option**:
```
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
**Output Explanation**: The `+` sign indicates which commands and values are being executed. This helps in tracing the script’s execution and finding where things might be going wrong.


2. **Using `-x -v` Options**:
```
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
- **Output Explanation**: This shows the entire code section processed so far, along with the individual steps. It provides a comprehensive view of how the script is executed, including both the code and the results of each command.