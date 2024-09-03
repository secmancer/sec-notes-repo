- **Overview**:
    
    - **Debugging** in Bash is the process of finding, tracking, and fixing errors (bugs) in the code.
    - It can be used for code analysis to determine why specific errors occur or to find vulnerabilities in programs.
- **Purpose**:
    
    - Debugging helps identify and correct typos, logical errors, or potential security vulnerabilities in the script.
- **Debugging Techniques**:
    
    - **Bash Debugging Options**:
        - `-x (xtrace)`: Shows each command and its arguments as they are executed. Useful for tracking the flow of execution and understanding which commands were run with which values.
        - `-v (verbose)`: Displays the entire script as it is being processed, including the commands and their outputs.
- **Example: Debugging with `-x` in CIDR.sh**:
    
    - Running the script with `-x`:
```
secmancer@htb[/htb]$ bash -x CIDR.sh
```
Example output:
```
+ '[' 0 -eq 0 ']'
+ echo -e 'You need to specify the target domain.\n'
You need to specify the target domain.

+ echo -e Usage:
Usage:
+ echo -e '\tCIDR.sh <domain>'
CIDR.sh <domain>
+ exit 1
```
- **Explanation**:
        - The `+` sign indicates each function or command executed along with the values passed.
        - This helps identify the exact point of failure or incorrect behavior in the script.
- **Verbose Debugging Example with `-v` and `-x`**:
    - Running the script with both `-v` and `-x`:
```
secmancer@htb[/htb]$ bash -x -v CIDR.sh
```
- Example output:
```
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
- **Explanation**:
        - In addition to the execution trace (`+` lines), the entire code section being processed is shown.
        - This provides a more detailed view of what the script is doing and helps pinpoint where things go wrong.
- **Use Cases**:
    - **Basic Debugging**: Using `-x` to track execution flow and identify unexpected behavior.
    - **Verbose Debugging**: Using `-v` along with `-x` for an in-depth analysis, especially useful for complex scripts.