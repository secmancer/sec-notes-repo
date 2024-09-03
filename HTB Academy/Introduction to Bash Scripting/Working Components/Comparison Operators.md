### String Operators
	- == : Equal to
	- != : Not equal to
	- < : Less than
	- > : Greater than
	- -z: String is empty
	- -n: String is not empty
**Example**:
```
#!/bin/bash

if [ "$1" != "HackTheBox" ]; then
    echo -e "You need to give 'HackTheBox' as an argument."
    exit 1
elif [ $# -gt 1 ]; then
    echo -e "Too many arguments given."
    exit 1
else
    domain=$1
    echo -e "Success!"
fi
```
### Integer Operators
- **`-eq`**: Equal to
- **`-ne`**: Not equal to
- **`-lt`**: Less than
- **`-le`**: Less than or equal to
- **`-gt`**: Greater than
- **`-ge`**: Greater than or equal to
**Example**:
```
#!/bin/bash

if [ $# -lt 1 ]; then
    echo -e "Number of given arguments is less than 1."
    exit 1
elif [ $# -gt 1 ]; then
    echo -e "Number of given arguments is greater than 1."
    exit 1
else
    domain=$1
    echo -e "Number of given arguments equals 1."
fi

```
### File Operators
- **`-e`**: File exists
- **`-f`**: File is a regular file
- **`-d`**: File is a directory
- **`-L`**: File is a symbolic link
- **`-N`**: File was modified since it was last read
- **`-O`**: File is owned by the current user
- **`-G`**: File's group ID matches the current user's
- **`-s`**: File size is greater than 0
- **`-r`**: File is readable
- **`-w`**: File is writable
- **`-x`**: File is executable

**Example**:
```
#!/bin/bash

if [ -e "$1" ]; then
    echo -e "The file exists."
    exit 0
else
    echo -e "The file does not exist."
    exit 2
fi

```
### Boolean and Logical Operators
- **Boolean Operators**:
    - **`-z`**: Checks if a string is empty.
    - **`!`**: Logical NOT.
    - **`&&`**: Logical AND.
    - **`||`**: Logical OR.

**Example**:
```
#!/bin/bash

if [[ -z $1 ]]; then
    echo -e "Boolean value: True (is null)"
    exit 1
elif [[ $# > 1 ]]; then
    echo -e "Boolean value: True (is greater than)"
    exit 1
else
    domain=$1
    echo -e "Boolean value: False (is equal to)"
fi

```
### Logical Operators
- **`!`**: Logical negation (NOT).
- **`&&`**: Logical conjunction (AND).
- **`||`**: Logical disjunction (OR).
**Example**:
```
#!/bin/bash

if [[ -e "$1" && -r "$1" ]]; then
    echo -e "We can read the file that has been specified."
    exit 0
elif [[ ! -e "$1" ]]; then
    echo -e "The specified file does not exist."
    exit 2
elif [[ -e "$1" && ! -r "$1" ]]; then
    echo -e "We don't have read permission for this file."
    exit 1
else
    echo -e "Error occurred."
    exit 5
fi

```
### Exercise Script
Here's a script to use the `base64` encoding and perform a conditional check:
```
#!/bin/bash

var="8dm7KsjU28B7v621Jls"
value="ERmFRMVZ0U2paTlJYTkxDZz09Cg"

for i in {1..40}; do
    var=$(echo $var | base64)

    if [ "$var" == "$value" ]; then
        echo "Match found at iteration $i"
        break
    fi
done

```
This script iterates 40 times, encoding `var` each time, and compares it to `value`. It exits if a match is found.

### Questions
- **Create an "If-Else" condition in the "For"-Loop that checks if the variable named "var" contains the contents of the variable named "value". Additionally, the variable "var" must contain more than 113,450 characters. If these conditions are met, the script must then print the last 20 characters of the variable "var". Submit these last 20 characters as the answer.**
	- 2paTlJYTkxDZz09Cg==