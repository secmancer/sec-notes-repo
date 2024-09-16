#### **Overview of Conditional Execution**
- **Purpose**: Allows control over the flow of a script by executing different sections of code based on specified conditions.
- **Importance**: Essential for creating scripts that perform tasks differently based on inputs or state, rather than executing commands sequentially.

#### **Script Components and Syntax**
1. **Shebang (`#!/bin/bash`)**
    - **Purpose**: Specifies the interpreter for the script.
    - **Usage**: Must be the first line of the script.
    - **Examples**:
        - Bash: `#!/bin/bash`
        - Python: `#!/usr/bin/env python`
        - Perl: `#!/usr/bin/env perl`
2. **If-Else-Fi**
    - **Purpose**: Checks conditions and executes code based on whether the condition is true or false.
    - **Syntax**:
```
if [ condition ]
then
    # Code to execute if condition is true
else
    # Code to execute if condition is false
fi
```
- **Example**:
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
3. **If-Only Example**
- **Code**:
```
#!/bin/bash

value=$1

if [ $value -gt "10" ]
then
    echo "Given argument is greater than 10."
fi
```
- **Execution:**
```
bash if-only.sh 5   # No output
bash if-only.sh 12  # Given argument is greater than 10.
```
4. **If-Elif-Else**
- **Purpose**: Handles multiple conditions. Allows more than two paths of execution.
- **Syntax**:
```
if [ condition1 ]
then
    # Code if condition1 is true
elif [ condition2 ]
then
    # Code if condition2 is true
else
    # Code if no condition is true
fi
```
- **Example**:
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
- **Execution**:
```
bash if-elif-else.sh 5   # Given argument is less than 10.
bash if-elif-else.sh 12  # Given argument is greater than 10.
bash if-elif-else.sh HTB # Given argument is not a number.
```
5. **Handling Multiple Conditions**
- **Example**:
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
#### **Exercise: Encoding Variable**
- **Purpose**: Demonstrates use of loops and commands to process data.
- **Code**:
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


#### **Key Takeaways**
- **Conditional Execution**: Crucial for directing script flow based on conditions.
- **Components**:
    - **Shebang**: Specifies interpreter.
    - **If-Else-Fi**: Basic conditional execution.
    - **If-Elif-Else**: Handles multiple conditions.
    - **Extending Scripts**: Multiple conditions can be used to manage different scenarios and inputs.


## Questions
- Create an "If-Else" condition in the "For"-Loop of the "Exercise Script" that prints you the number of characters of the 35th generated value of the variable "var". Submit the number as the answer.
	- 1197735