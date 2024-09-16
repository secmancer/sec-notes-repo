To compare specific values in Bash, we use comparison operators. These operators help determine how defined values will be compared. They are categorized into different types:

#### **1. String Operators**
- **Purpose**: Compare string values to determine if they are equal, not equal, or if one is greater or less than the other.
- **Operators**:
- =: Checks if two strings are equal.
```
[ "$string1" = "$string2" ]
```
- !=: Checks if two strings are not equal.
```
[ "$string1" != "$string2" ]
```
- <: Checks if the first string is less than the second string in ASCII value.
```
[ "$string1" \< "$string2" ]
```
- >: Checks if the first string is greater than the second string in ASCII value.
```
[ "$string1" \> "$string2" ]
```


**Note**: For `<` and `>`, you need to escape these characters with a backslash (`\`) to prevent them from being interpreted by the shell.



#### **2. Integer Operators**
- **Purpose**: Compare integer values to determine if they are equal, not equal, or if one is greater or less than the other.
- **Operators**:
- `-eq`: Checks if two integers are equal.
```
[ "$int1" -eq "$int2" ]
```
- `-ne`: Checks if two integers are not equal.
```
[ "$int1" -ne "$int2" ]
```
- `-lt`: Checks if the first integer is less than the second integer.
```
[ "$int1" -lt "$int2" ]
```
- `-le`: Checks if the first integer is less than or equal to the second integer.
```
[ "$int1" -le "$int2" ]
```
- `-gt`: Checks if the first integer is greater than the second integer.
```
[ "$int1" -gt "$int2" ]
```
- `-ge`: Checks if the first integer is greater than or equal to the second integer.
```
[ "$int1" -ge "$int2" ]
```



#### **3. File Operators**
- **Purpose**: Compare files to determine if they exist, are readable, writable, or executable.
- **Operators**:
- `-e`: Checks if a file exists.
```
[ -e "$file" ]
```
- `-f`: Checks if a file is a regular file.
```
[ -f "$file" ]
```
- `-d`: Checks if a file is a directory.
```
[ -d "$file" ]
```
- `-r`: Checks if a file is readable.
```
[ -r "$file" ]
```
`-w`: Checks if a file is writable.
```
[ -w "$file" ]
```
`-x`: Checks if a file is executable.
```
[ -x "$file" ]
```


#### **4. Boolean Operators**
- **Purpose**: Combine multiple conditions in logical expressions.
- **Operators**:
- &&`: Logical AND. Both conditions must be true.
```
[ "$cond1" ] && [ "$cond2" ]
```
- `||`: Logical OR. At least one condition must be true.
```
[ "$cond1" ] || [ "$cond2" ]
```
- `!`: Logical NOT. The condition must be false.
```
! [ "$cond" ]
```

![[Screenshot_20240916_092747.png]]


#### **1. Handling Variables with Double Quotes**
- **Purpose**: To ensure that the content of a variable is treated as a string, especially when the variable might contain spaces or special characters.
- **Example**:
```
# Check the given argument
if [ "$1" != "HackTheBox" ]
then
  echo -e "You need to give 'HackTheBox' as argument."
  exit 1
elif [ $# -gt 1 ]
then
  echo -e "Too many arguments given."
  exit 1
else
  domain=$1
  echo -e "Success!"
fi
```
**Explanation**:
- Using `"$1"` ensures that if `$1` contains spaces or special characters, it will be correctly interpreted as a single string rather than multiple arguments or causing errors.
- Without quotes, Bash could misinterpret the content, especially if there are spaces or if the variable is empty.


#### **2. String Comparison Operators**
- **Operators**:
    - **`<`** and **`>`**: These operators work only within double square brackets `[[ <condition> ]]` for string comparisons. They compare the ASCII values of the characters in the strings.
    - **Example**:
```
if [[ "$string1" < "$string2" ]]
then
  echo "$string1 is less than $string2"
elif [[ "$string1" > "$string2" ]]
then
  echo "$string1 is greater than $string2"
fi
```
**Getting ASCII Values**:
- You can find ASCII values using the following command in the terminal:
```
man ascii
```
- This command displays the ASCII table, which is useful for understanding how string comparisons are made based on ASCII values.

![[Screenshot_20240916_092821.png]]

![[Screenshot_20240916_092923.png]]


```
#!/bin/bash

# Check the given argument
if [ $# -lt 1 ]
then
	echo -e "Number of given arguments is less than 1"
	exit 1

elif [ $# -gt 1 ]
then
	echo -e "Number of given arguments is greater than 1"
	exit 1

else
	domain=$1
	echo -e "Number of given arguments equals 1"
fi
```

![[Screenshot_20240916_093005.png]]


```
#!/bin/bash

# Check if the specified file exists
if [ -e "$1" ]
then
	echo -e "The file exists."
	exit 0

else
	echo -e "The file does not exist."
	exit 2
fi
```

## Boolean and Logical Operators

We get a boolean value "`false`" or "`true`" as a result with logical operators. Bash gives us the possibility to compare strings by using double square brackets `[[ <condition> ]]`. To get these boolean values, we can use the string operators. Whether the comparison matches or not, we get the boolean value "`false`" or "`true`".

```
#!/bin/bash

# Check the boolean value
if [[ -z $1 ]]
then
	echo -e "Boolean value: True (is null)"
	exit 1

elif [[ $# > 1 ]]
then
	echo -e "Boolean value: True (is greater than)"
	exit 1

else
	domain=$1
	echo -e "Boolean value: False (is equal to)"
fi
```


## Logical Operators

With logical operators, we can define several conditions within one. This means that all the conditions we define must match before the corresponding code can be executed.

![[Screenshot_20240916_093113.png]]

```
#!/bin/bash

# Check if the specified file exists and if we have read permissions
if [[ -e "$1" && -r "$1" ]]
then
	echo -e "We can read the file that has been specified."
	exit 0

elif [[ ! -e "$1" ]]
then
	echo -e "The specified file does not exist."
	exit 2

elif [[ -e "$1" && ! -r "$1" ]]
then
	echo -e "We don't have read permission for this file."
	exit 1

else
	echo -e "Error occured."
	exit 5
fi
```


## Exercise Script
```
#!/bin/bash

var="8dm7KsjU28B7v621Jls"
value="ERmFRMVZ0U2paTlJYTkxDZz09Cg"

for i in {1..40}
do
        var=$(echo $var | base64)
		
		#<---- If condition here:
done
```


## Questions
- Create an "If-Else" condition in the "For"-Loop that checks if the variable named "var" contains the contents of the variable named "value". Additionally, the variable "var" must contain more than 113,450 characters. If these conditions are met, the script must then print the last 20 characters of the variable "var". Submit these last 20 characters as the answer.
	- 2paTlJYTkxDZz09Cg==