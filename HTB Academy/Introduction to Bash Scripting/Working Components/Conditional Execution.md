#### Overview:
Conditional execution is fundamental in scripting, allowing us to control the flow of a script by evaluating different conditions. This enables executing specific sections of code based on certain conditions, making scripts more dynamic and efficient.
#### Key Components in Conditional Execution:
1. **Shebang (`#!/bin/bash`):**
    - The shebang (`#!`) line at the beginning of a script specifies the interpreter to execute the script. For Bash scripts, it’s typically `#!/bin/bash`.
    - Other interpreters can be specified, such as:
        - Python: `#!/usr/bin/env python`
        - Perl: `#!/usr/bin/env perl`
2. **If-Else-Fi Structure:**
    - **`if-else-fi`:** A structure used to evaluate conditions and execute code based on those conditions.
    - **Pseudo-Code Example:**
        - If a condition is met, execute the corresponding block of code.
        - If not, move on to the next condition or execute an alternative block.
    - **Example Script (`Script.sh`):**
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
1. - **Explanation:**
        - `if [ $# -eq 0 ]`: Checks if no arguments were provided.
        - `echo -e`: Prints output with escaped characters (e.g., newlines).
        - `$#`: Represents the number of arguments provided.
        - `$0`: Represents the name of the script.
        - `$1`: Represents the first argument provided to the script.
        - `domain=$1`: Assigns the first argument to the variable `domain`.
2. **Special Variables:**
    - **`$#`:** Number of arguments passed to the script.
    - **`$0`:** The name of the script.
    - **`$1`, `$2`, etc.:** The arguments passed to the script.
    - **`domain`:** A variable used to store the first argument (in this case, the domain).
3. **Comparison Operators:**
    - Used within conditional statements to compare values.
    - **Example:**
        - `-eq`: Equal to.
        - `-lt`: Less than.
        - `-gt`: Greater than.

#### Examples of Conditional Execution:
1. **Simple If Statement:**
    - Executes a block of code if a condition is true.
    - **Example (`If-Only.sh`):**
```
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
    echo "Given argument is greater than 10."
fi
```
- **Execution:**
        - `bash if-only.sh 5`: No output because the condition is not met.
        - `bash if-only.sh 12`: Outputs "Given argument is greater than 10."
- **If-Elif-Else Statement:**
    - Adds alternatives to handle specific values or statuses.
    - **Example (`If-Elif-Else.sh`):**
```
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
    echo "Given argument is greater than 10."
elif [ $value -lt "10" ]
then
    echo "Given argument is less than 10."
else
    echo "Given argument is not a number."
fi
```
- **Execution:**
        - `bash if-elif-else.sh 5`: Outputs "Given argument is less than 10."
        - `bash if-elif-else.sh 12`: Outputs "Given argument is greater than 10."
        - `bash if-elif-else.sh HTB`: Outputs "Given argument is not a number."
- **Extended Conditional Execution:**
    - Allows for multiple conditions to be checked, with specific actions based on each condition.
    - **Example (`Script.sh`):**
```
#!/bin/bash

# Check for given argument
if [ $# -eq 0 ]
then
    echo -e "You need to specify the target domain.\n"
    echo -e "Usage:"
    echo -e "\t$0 <domain>"
    exit 1
elif [ $# -eq 1 ]
then
    domain=$1
else
    echo -e "Too many arguments given."
    exit 1
fi
```
#### Exercise Script Example:
- **Script to Encode a Variable:**
```
#!/bin/bash
# Count number of characters in a variable:
#     echo $variable | wc -c

# Variable to encode
var="nef892na9s1p9asn2aJs71nIsm"

for counter in {1..40}
do
        var=$(echo $var | base64)
done
```
**Explanation:**
- The script takes a variable (`var`) and encodes it 40 times using Base64 encoding.
- The `for` loop runs 40 times, each time encoding the variable again.

### Questions:
- Create an "If-Else" condition in the "For"-Loop of the "Exercise Script" that prints you the number of characters of the 35th generated value of the variable "var". Submit the number as the answer.
	- 1197735