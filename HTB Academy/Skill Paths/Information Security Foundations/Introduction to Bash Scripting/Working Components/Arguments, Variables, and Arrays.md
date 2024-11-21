## Arguments
- The advantage of bash scripts is that we can always pass up to 9 arguments (`$0`-`$9`) to the script without assigning them to variables or setting the corresponding requirements for these. `9 arguments` because the first argument `$0` is reserved for the script. As we can see here, we need the dollar sign (`$`) before the name of the variable to use it at the specified position. The assignment would look like this in comparison:
```shell-session
secmancer@htb[/htb]$ ./script.sh ARG1 ARG2 ARG3 ... ARG9
       ASSIGNMENTS:       $0      $1   $2   $3 ...   $9
```
- This means that we have automatically assigned the corresponding arguments to the predefined variables in this place. These variables are called special variables. These special variables serve as placeholders. If we now look at the code section again, we will see where and which arguments have been used.
- #### CIDR.sh
```bash
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

<SNIP>
```
- There are several ways how we can execute our script. However, we must first set the script's execution privileges before executing it with the interpreter defined in it.
- #### CIDR.sh - Set Execution Privileges
```shell-session
secmancer@htb[/htb]$ chmod +x cidr.sh
```
- #### CIDR.sh - Execution without Arguments
```shell-session
secmancer@htb[/htb]$ ./cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```
- #### CIDR.sh - Execution without Execution Permissions
```shell-session
secmancer@htb[/htb]$ bash cidr.sh

You need to specify the target domain.

Usage:
	cidr.sh <domain>
```


## Special Variables
- Special variables use the [Internal Field Separator](https://bash.cyberciti.biz/guide/$IFS) (`IFS`) to identify when an argument ends and the next begins. Bash provides various special variables that assist while scripting. Some of these variables are:
![[Screenshot_20241111_151816.png]]
- Of the ones shown above, we have 3 such special variables in our `if-else` condition.
![[Screenshot_20241111_151830.png]]


## Variables
- We also see at the end of the if-else loop that we assign the value of the first argument to the variable called "`domain`". The assignment of variables takes place without the dollar sign (`$`). The dollar sign is only intended to allow this variable's corresponding value to be used in other code sections. When assigning variables, there must be no spaces between the names and values.
```bash
<SNIP>
else
	domain=$1
fi
<SNIP>
```
- In contrast to other programming languages, there is no direct differentiation and recognition between the types of variables in Bash like "`strings`," "`integers`," and "`boolean`." All contents of the variables are treated as string characters. Bash enables arithmetic functions depending on whether only numbers are assigned or not. It is important to note when declaring variables that they do `not` contain a `space`. Otherwise, the actual variable name will be interpreted as an internal function or a command.
- #### Declaring a Variable - Error
```shell-session
secmancer@htb[/htb]$ variable = "this will result with an error."

command not found: variable
```
- #### Declaring a Variable - Without an Error
```shell-session
secmancer@htb[/htb]$ variable="Declared without an error."
secmancer@htb[/htb]$ echo $variable

Declared without an error.
```



## Arrays
- There is also the possibility of assigning several values to a single variable in Bash. This can be beneficial if we want to scan multiple domains or IP addresses. These variables are called `arrays` that we can use to store and process an ordered sequence of specific type values. `Arrays` identify each stored entry with an `index` starting with `0`. When we want to assign a value to an array component, we do so in the same way as with standard shell variables. All we do is specify the field index enclosed in square brackets. The declaration for `arrays` looks like this in Bash:
- #### Arrays.sh
```bash
#!/bin/bash

domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)

echo ${domains[0]}
```
- We can also retrieve them individually using the index using the variable with the corresponding index in curly brackets. Curly brackets are used for variable expansion.
```shell-session
secmancer@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com
```
- It is important to note that single quotes (`'` ... `'`) and double quotes (`"` ... `"`) prevent the separation by a space of the individual values in the array. This means that all spaces between the single and double quotes are ignored and handled as a single value assigned to the array.
- #### Arrays.sh
```bash
#!/bin/bash

domains=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
echo ${domains[0]}
```
```shell-session
secmancer@htb[/htb]$ ./Arrays.sh

www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com
```


### Questions
- Submit the echo statement that would print "www2.inlanefreight.com" when running the last "Arrays.sh" script.
	- echo ${domains[1]}