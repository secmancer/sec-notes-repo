**Purpose of Functions**
- **Improves Code Clarity**: Functions help manage and organize code, especially in larger scripts.
- **Avoids Code Repetition**: Encapsulate repeated commands or blocks of code in functions to simplify and shorten the script.
- **Enhances Readability**: Makes the script easier to understand and maintain.


**Defining Functions**
**Method 1**:
```
function name {
    <commands>
}
```
- Uses the `function` keyword for clarity.
**Method 2**:
```
name() {
    <commands>
}
```
- More concise, but functionally equivalent.


**Example Function Definition in CIDR.sh**
```
<SNIP>
# Identify Network range for the specified IP address(es)
function network_range {
    for ip in $ipaddr
    do
        netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
        cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
        cidr_ips=$(prips $cidr)
        echo -e "\nNetRange for $ip:"
        echo -e "$netrange"
    done
}
<SNIP>
```
 - **Function Call**: The function `network_range` is called in the case statement.


**Function Execution**
```
<SNIP>
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "3") network_range && ping_host ;;
    "*") exit 0 ;;
esac
```



**Parameter Passing**
- **Parameters**: Functions can take parameters like `$1`, `$2`, `$3`, etc.
- **Scope**: Variables defined within functions are global by default unless declared with `local`.
- **Example**:
```
#!/bin/bash

function print_pars {
    echo $1 $2 $3
}

one="First parameter"
two="Second parameter"
three="Third parameter"

print_pars "$one" "$two" "$three"
```
- **Output**: `First parameter Second parameter Third parameter`



#### Return.sh
```
#!/bin/bash

function given_args {

        if [ $# -lt 1 ]
        then
                echo -e "Number of arguments: $#"
                return 1
        else
                echo -e "Number of arguments: $#"
                return 0
        fi
}

# No arguments given
given_args
echo -e "Function status code: $?\n"

# One argument given
given_args "argument"
echo -e "Function status code: $?\n"

# Pass the results of the funtion into a variable
content=$(given_args "argument")

echo -e "Content of the variable: \n\t$content"
```


#### Return.sh - Execution
```
secmancer@htb[/htb]$ ./Return.sh

Number of arguments: 0
Function status code: 1

Number of arguments: 1
Function status code: 0

Content of the variable:
    Number of arguments: 1
```