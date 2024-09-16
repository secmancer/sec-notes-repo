### Notes: Arguments in Bash Scripts
#### **Overview of Arguments**
- **Purpose**: Allows passing multiple values to a script at runtime without explicitly defining them as variables within the script.
- **Special Variables**:
    - `$0`: Name of the script.
    - `$1` to `$9`: First to ninth arguments passed to the script.

#### **Usage of Arguments**
- **Execution with Arguments**:
```
./script.sh ARG1 ARG2 ARG3 ... ARG9
```
- **Assignments**:
	- `$0` → `script.sh`
	- `$1` → `ARG1`
	- `$2` → `ARG2`
	- `$3` → `ARG3`
	- ... up to `$9`
**Example**:
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
```


#### **Setting Execution Privileges**
- **Make the script executable**:
```
chmod +x cidr.sh
```


#### **Executing the Script**
1. **Without Arguments**:
```
./cidr.sh
```
- **Output**
```
You need to specify the target domain.

Usage:
    cidr.sh <domain>
```


2. **Without Execution Permissions**:
```
bash cidr.sh
```
- **Output**
```
You need to specify the target domain.

Usage:
    cidr.sh <domain>
```


![[Screenshot_20240916_091949.png]]


#### **Variables**
- **Assignment**:
    - Variables are assigned values without the dollar sign (`$`).
    - The dollar sign is used when referencing the variable's value.
    - **No spaces** allowed around the = during assignment
    **Example**:
```
domain=$1
```
- **Type Handling**:
	- Bash does not differentiate between variable types (strings, integers, booleans).
	- All variables are treated as strings by default.
	- Arithmetic operations can be performed if the variables contain numbers.
- **Error in Variable Declaration**:
	- Incorrect: `variable = "this will result with an error."`
	    - Error: `command not found: variable`
	- Correct:
```
variable="Declared without an error."
echo $variable
```
- Output: `Declared without an error.`


#### **Arrays**
- **Definition and Use**:
    - Arrays allow storing multiple values in a single variable.
    - Values are indexed starting from 0.
    **Declaration**:
```
domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)
```
**Accessing Array Elements**:
- Use curly brackets and index to retrieve elements.
- **Example**:
```
echo ${domains[0]}
```
**Output**:
```
www.inlanefreight.com
```
**Handling Spaces in Array Values**:
- Single quotes (`' ... '`) and double quotes (`" ... "`) ensure spaces are treated as part of the value.
- **Example**:
```
domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}
```
**Output**:
```
www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com
```



## Questions
- Submit the echo statement that would print "www2.inlanefreight.com" when running the last "Arrays.sh" script.
	- echo ${domains[1]}